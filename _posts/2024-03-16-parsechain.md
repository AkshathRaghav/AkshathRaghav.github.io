---
layout: post
title: Working with `GrammarFlow` to constrain your LLM chains 🪢
date: 2024-01-27 19:22:00
description: this is how you can display code diffs
tags: formatting code
categories: sample-posts
code_diff: true
---

# 🪢 [GrammarFlow](https://github.com/e-lab/SyntaxShaper/tree/main)

Find a larger list of examples to get started with [here](https://github.com/e-lab/SyntaxShaper/blob/main/demo.ipynb)!

## 🤔 What is this?

[This repository](https://github.com/e-lab/SyntaxShaper/) contains code to abstract the LLM output constraining process. It helps you define your grammar rules using Pydantic and Typing in a pythonic way, and inherently embeds metadata from these dataclasses into the prompt. Parsing is enabled in JSON, TOML and XML formats, with custom parsers that avoid the issues faced by `json.loads` (..etc) while parsing direct outputs. It can also create GNBF grammr from the same, which is used by the `llama.cpp` package for sampling logits smartly. 

The goal of this package was to overcome the issues faced when using langchain's output parsers with local language models. While GPT-4 produces consistent results in returning the correct formats, Llama-7B would cause parsing errors in my testing chains with more complex prompts. Moreover, across LLMs, it's a pain for me to keep re-defining grammar formats into my prompt and then making custom parsers. I use this in my workflow daily to simplify the process and speed-up my productivity. 

## 📚 Quick Install

`pip install parsechain`

## 📃 Walkthrough

Let's try out making a agent-thinking-chain. I used something similar in [euGenie](https://viktor1223.github.io/AI-Assistant/)! 

### Quick Background 

> HotpotQA is a question answering dataset featuring natural, multi-hop questions, with strong supervision for supporting facts to enable more explainable question answering systems.

[ReAct](https://github.com/ysymyth/ReAct) adds a bunch of useful helper functions to their evaluation code for prompting against this dataset. This sample directory cleans up their code and adds GrammarFlow to it. 

1. Create a Pydantic model to constrain our thinking state. We'll ask the model for 'thought', 'action', and 'action_input'. 
2. Create a Prompt for our ReAct flow. Our `make_prompt()` function below takes care of it. 
3. Within the original `webthink()` function, we make changes along the lines of: 
    - Tracking and logging all steps between iterations\n
    - Use `Constrain()` from GrammarFlow to make the extraction of 'Thought', 'Action' and 'Action_Input' pythonic and error-prone. 
Note: Prompts are stateful, and thus need to be discarded after every `Constrain()` block. That's why we use `make_prompt()` within every run. 

### Implementation 

1. Map out what your agent chain is doing. Understand what it's goals are and what data needs to be carried forward from one step to the next. In every call, we want to pass in the Action and subsequent Observation to the next call. 

2. Make a Pydantic Model for the above case. Here's a sample: 
```python 
class Step(BaseModel):
    thought: str 
    action: str = Field(..., description="You only have 3 options: search | lookup | finish")
    action_input: str = Field(..., description="Your input to the above action.")
```

3. [Optional] Create a prompt template using parsechain's PromptBuilder. 
For simpler prompts, you do not need to create a PromptBuilder() object, but for the purpose of showing what can be done, we will. 

```python 
from parsechain import PromptBuilder

# Using this to ignore certain sections in my main loop
def check_previous_interaction(id_): return id_ > 1

def make_prompt(): 
  prompt = PromptBuilder() 
  prompt.add_section(
    text="""
  Goal: {question}

  Your goal is to solve the above QA task in steps. First, think about what information you need to answer the question. 
  Use `search` to get the information you need. This needs a single keyword or noun as input. If it can't find anything, itll give alternate keywords. You can find them in your thinking history below, use them to search again. 
  Use `lookup` to find more information from the paragraph returned by search. This matches the action_input you give to setences in search. 
  Use `finish` to return your final complete answer as input field. Use this if you believe you have enough information to completely answer the task.""",
    placeholders=["question"]
  ) 
  prompt.add_section(
    define_grammar=True
  ) 
  prompt.add_section(
    text="\nExample thinking process:{example}\n", 
    placeholders=["example"]
  )
  prompt.add_section(
    text="Create the next Step using the information available you to below.\n",
  )
  prompt.add_section(
    text="DO NOT REPEAT THOUGHTS OR ACTIONS FROM YOUR PAST. ENSURE EACH STEP IS UNIQUE. Below is the history of your thinking process and corresponding observations.\n{history}\n",
    placeholders=["history"],
    enable_on=check_previous_interaction
  ) 
  return prompt 
```

**Here's an example of the [Llama2 Prompt](https://github.com/e-lab/SyntaxShaper/blob/main/README.md#-code-usage). 
You can find an in-depth explanation on making prompts [here](https://github.com/e-lab/SyntaxShaper/blob/main/demo.ipynb)!**

4. [Optional] If you decide to make your own template, define your `placeholders`. 
```python
example = wrappers.EXAMPLE
question = "What government position was held by the woman who portrayed Corliss Archer in the film Kiss and Tell?" 

def load_history(history_):
    "\n".join([f"Thought {id_}: {value['thought']}\nAction {id_}: {value['action']}\nAction_Input {id_}: {value['action_input']}\nObservation {id_}: {value['observation']}" for id_, value in history.items()])
```

5. Invoke the `Constrain` block with the prompt. Set the configuration metadata, and format the prompt with the required `grammars` and `placeholders`. The below codeblock is taken from the ReAct repository with just a few changes. 
```python
from parsechain import Constrain 

def webthink(idx=None, env=env, to_print=False): 
  # Initializing Stateful vars
  thought = None 
  action = None
  observation = None
  id_ = 1
  history, history_ = {}, None

  for i in range(10):
    if history:
      history_ = load_history(history_)

    # The only major change we've made! 
    with Constrain(make_prompt()) as manager: 
      manager.set_config(
        format='xml'
      ) 
      manager.format_prompt(
        placeholders={ 
          "question": question,
          'example': example, 
          "history": history_
        }, 
        grammars=[{
          'description': 'Your thinking state', 
          'model': Step
        }], 
        enable_on={
          'id_':id_ 
        }
      ) 
      
      response = llm(manager.prompt, temperature=0.01)
      response = manager.parse(response)  

      thought = response.Step.thought 
      action = response.Step.action
      action_input = response.Step.action_input

    observation, r, done, info = step(env, f"{action}[{action_input}]")
    observation = observation.replace("\\n", " ")

    history[id_] = { 
      "thought": thought, 
      "action": action, 
      "action_input": action_input, 
      "observation": observation
    }

    id_ += 1
    
    if done: 
      final = action_input
      break 

  if not done:
      final = "Failed!"
      observation, r, done, info = step(env, "finish[]")

  return final, info['gt_answer'], id_
```

6. Extract the required values from the response to perform necessary functions on. The below statements perform these actions in the above code. 

```python 
...
        response = llm(manager.prompt, temperature=0.01)
        response = manager.parse(response)  

        thought = response.Step.thought 
        action = response.Step.action
        action_input = response.Step.action_input
...
```

7. Continue to the next iteration in your agent chain! 

### GNBF Grammar 

GrammarFlow also has functionality to convert a pydantic model into GNBF grammar. 
> "GBNF (GGML BNF) is a format for defining formal grammars to constrain model outputs in llama.cpp. For example, you can use it to force the model to generate valid JSON, or speak only in emojis."
> Read more about it here: https://github.com/ggerganov/llama.cpp/blob/master/grammars/README.md

This can then be passed into llama.cpp using llama-cpp-python to ensure that sampling of logits can take place with rules in mind. 

```python
# Define your model 
class TeamMember(BaseModel):
    name: str
    role: str

class TaskUpdate(BaseModel):
    update_time: float
    comment: Optional[str] = None
    status: bool

class Task(BaseModel):
    title: str
    description: str
    assigned_to: List[TeamMember]
    due_date: List[str]
    updates: List[TaskUpdate]

class Project(BaseModel):
    name: str
    description: str
    project_url: Optional[str] = None
    team_members: List[TeamMember]
    grammars: Task

# Convert to grammar
from parsechain import GNBF

grammar = GNBF(Project).generate_grammar()

# Verify with LlamaGrammar
GNBF.verify_grammar(grammar)

# Use it with the model 
with Constrain(llama_prompt) as manager: 
    manager.set_config(...)
    manager.format_prompt(...)

    llm_response = llm(
        manager.prompt,
        grammar=grammar, max_tokens=-1
    )
    response = manager.parse(llm_response)
```

