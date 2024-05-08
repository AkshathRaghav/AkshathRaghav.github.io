---
layout: page
title: maskformer
description: Re-engineering MaskFormer for Google's TF Model Garden (Funded) 🚀
img: assets/img/dualityxtfmg.jpg
importance: 1
category: research
related_publications: false 
---

This page is the culmination of the work I did at [Duality Lab](https://github.com/PurdueDualityLab/tf-maskformer) (Fall '23 + Spring '24) as a research assistant under [Vishal S P](https://www.linkedin.com/in/vishalsp/) and [Wenxin Jiang](https://wenxin-jiang.github.io/cv/).

{% include theorem.md 
  type="remark"
  name="What & Why?"
  statement="
  Re-engineered the state-of-the-art MaskFormer computer-vision model to publish into the TensorFlow Model Garden; Developed an implementation which ran efficiently on GCP TPUs out-of-box.
  "
%}


* Wrote the evaluation module, including the implementation of panoptic inference metrics to work with tf2's inbuilt task workflow. Fixed and integrated code for multi-scale (auxillary) losses to address inability of loss convergence. 
* Conducted experiments on GPUs & TPUs to ensure layer precision across the meta-architecture and implemented functions to ensure data consistency through the dataloader. Fixed run-time issues in main task file related to running across different computes. 
* Responsible for the PR to [TF Model Garden](https://github.com/tensorflow/models), from re-writing modules (across layers) for guidelines adherence to creating/annotating results for the report. Wrote unit tests for all modules used in the architecture for tensor shape validation and expected results. Wrote [differential testing module](https://gist.github.com/AkshathRaghav/9f81ea6f997a2972732fb3d955b5b444) for comparison of modules between PyTorch and TensorFlow. 

Find our code [here](https://github.com/PurdueDualityLab/tf-maskformer/tree/PR_Draft/models/official/projects/maskformer).

Find the paper [here](https://arxiv.org/pdf/2404.18801).


# Description

MaskFormer, a universal architecture based on MaskFormer meta-architecture that achieves SOTA on panoptic, instance and semantic segmentation across four popular datasets (ADE20K, Cityscapes, COCO, Mapillary Vistas).

MaskFormer transforms any per-pixel classification model into a mask classification method. It utilizes a Transformer decoder to compute a set of pairs, each comprising a class prediction and a mask embedding vector. The binary mask prediction is obtained via a dot product between the mask embedding vector and per-pixel embedding from a fully-convolutional network. This model addresses both semantic and instance-level segmentation tasks without requiring changes to the model, losses, or training procedure. For both semantic and panoptic segmentation tasks, MaskFormer is supervised using the same per-pixel binary mask loss and a single classification loss per mask. A straightforward inference strategy is designed to convert MaskFormer outputs into a task-dependent prediction format.

<p align="center">
{% include figure.liquid loading="eager" path="assets/img/maskformer/maskformer_real.png" class="img-fluid rounded z-depth-1" %}
</p>


# Results 

Here are our results: 

<div align="center">
  {% include figure.liquid loading="eager" path="assets/img/maskformer/train_results.png" class="img-fluid rounded z-depth-1" %}
  <div class="caption">
      Annotated results of our results on the training split of the COCO TFRecords
  </div>
  {% include figure.liquid loading="eager" path="assets/img/maskformer/val_results.png" class="img-fluid rounded z-depth-1" %}
  <div class="caption">
      Annotated results of our results on the eval split of the COCO TFRecords
  </div>
  {% include figure.liquid loading="eager" path="assets/img/maskformer/losses.png" class="img-fluid rounded z-depth-1" %}
  <div class="caption">
    Comparison of our training losses vs PyTorch's logs. From left to right: 'cls_loss', 'dice_loss', 'focal_loss/mask_loss', 'total_loss'
  </div>
</div>


# Architecture 

### DataLoader
<div align="center">
  {% include figure.liquid loading="eager" path="assets/img/maskformer/maskformer_data.png" class="img-fluid rounded z-depth-1" %}
  <div class="caption">
      PreProcessing Outline
  </div>
</div>
The process begins with the raw image and annotation files (JSON format), which are serialized into TFRecord format, a TensorFlow-specific binary storage format. Subsequently, these TFRecords are deserialized, and the data is passed through a series of preprocessing steps including normalization, augmentation, and padding to ensure uniformity of the input data. The binary mask generation and the label mapping are integral to preparing segmentation tasks. The output is then converted to a format compatible with the models data loader, which feeds the processed data into the training pipeline. (zoom in for a better viewing experience)

### Overview  
<div align="center">
  {% include figure.liquid loading="eager" path="assets/img/maskformer/maskformer(3).png" class="img-fluid rounded z-depth-1" %}
</div>

The process
begins with an input image (A), which is processed by a ResNet-50 backbone to extract feature maps.
Multi-scale features (B) are generated from the backbone and then decoded by a Pixel Decoder (C) to create
refined feature maps. These are fed into a Transformer Decoder (D), along with a set of learned queries that
interact with the feature maps to generate mask embeddings (F). An MLP head (E) processes the mask
embedding to produce the final segmentation output, which consists of binary masks for each query, along
with their corresponding output labels, indicating the presence of specific objects or regions within the input
image.

### Implementation 

<div align="center">
  {% include figure.liquid loading="eager" path="assets/img/maskformer/transformer_pixel_decoder(1).png" class="img-fluid rounded z-depth-1" %}
  <div class="caption">
      Annotated results of our results on the training split of the COCO TFRecords
  </div>
</div>

The architecture begins with the backbone features extracted from the input image. These features are then projected and enriched with positional embeddings before being passed through multiple layers of a Transformer encoder.
The resulting encoded features are processed by a Transformer Pixel Decoder, which combines them with mask features to enhance localization capability. Simultaneously, query embeddings are combined with positional embeddings and processed by the Transformer Decoder to generate predictions. The decoded features are then passed through an MLP head, which classifies each pixel, resulting in the final output comprising predicted binary masks and their associated labels.

- Backbone Network A : The original work explored a diverse array of backbone networks for fea-
ture extraction, encompassing both convolutional architectures, such as ResNet-50 He et al. (2016),
and transformer-based models like the Swin Transformer Liu et al. (2021). The ResNet50 imple-
mentation is readily available in TFMG under official > vision > modeling > backbones and
the pre-trained checkpoint for ResNet are made available at TF-Vision Model Garden found under
official > vision.

- Multiscale Features B : In our model’s architecture, a key component is the utilization of mul-
tiscale features, as indicated by the ‘B’ in Figure 5. This design choice allows for flexibility in feature
extraction from the backbone network, specifically ResNet. Our implementation supports both the
extraction of deep, high-level features from the final layer of ResNet and the rich, intermediate
features available from earlier layers. An important consideration when employing the multiscale
features is the increased demand for memory during the model training phase. The inclusion of data
from multiple layers escalates the volume of information processed, which can strain available mem-
ory resources. In our implementation, the use of multi-scale features is controlled by the parameter
deep_supervision

- Transformer Pixel Decoder C : A comprehensive depiction of the transformer pixel decoder’s
architecture is illustrated in Figure 6. At its core, the transformer pixel decoder is an assembly of
two primary components: the transformer encoder and a series of convolutional and normalization
layers. We have incorporated the transformer encoder layers into our architecture by utilizing the
existing implementation available in the TensorFlow Model Garden, specifically from the directory
official > nlp > layers. To maintain consistency and interoperability with models developed in
other frameworks, particularly PyTorch, we have undertaken a process to ensure that our adopted
transformer encoder layers exhibit functional parity with their PyTorch counterparts. 

- Transformer Decoder D : Similar to our approach with the Pixel Decoder, we have adopted
the Transformer Decoder component from the pre-existing implementations provided in the Ten-
sorFlow Model Garden, specifically sourced from the directory official > nlp > layers. While
integrating the Transformer Decoder from the TensorFlow Model Garden, we ensure that it seam-
lessly interfaces with other components of our model, such as the transformer pixel decoder and the
backbone network. This involves aligning input and output dimensions, ensuring compatible data
types, and configuring the decoder appropriately to match our specific requirements. We validate
and test the functionality of the integrated transformer decoder and the transformer pixel decoder
within our architecture.

- MLP Projection E : The MLP (Multi-Layer Perceptron) projection layers, in conjunction with
the linear classifier, are used to obtain the predicted binary masks and corresponding labels. The
Transformer Decoder processes the Transformer Encoder Features to extract high-dimensional fea-
tures, Transformer Features, that encapsulate both spatial and contextual information are used by
the linear classifier to predict the label of each binary mask. Simultaneously, Mask Features that
are obtained from the Transformer Pixel Decoder are fed into the MLP projection layers to obtain
the predicted binary masks. We implement the Head of MaskFormer using TensorFlow API.

# Getting Started
---

```
git clone https://github.com/PurdueDualityLab/tf-maskformer.git
cd models/official/projects/maskformer
```

## Environment Creation
Create and activate a new conda environment to isolate the project dependencies:
```
conda create -n tfmaskformer
conda activate tfmaskformer
pip install -r /models/official/requirements.txt
pip install tensorflow-text-nightly
```

## COCO Dataset to TFRecord Conversion Guide

Below are detailed instructions on how to convert the COCO dataset annotations and images into TensorFlow's TFRecord format using the `create_coco_tf_record.py` script. 

### Overview

The `create_coco_tf_record.py` script processes raw COCO dataset files, including images and their annotations (object annotations, panoptic annotations, and captions), and encodes them into TFRecord files. Each image and its corresponding annotations are encapsulated in a `tf.Example` protobuf message, serialized, and written to a TFRecord file.

To use this script, ensure you have the following COCO dataset files:
- **Images Directory**: For example, `train2017/`
- **Annotations Files**: Such as `instances_train2017.json`, `captions_train2017.json`, `panoptic_train2017.json`
- **Panoptic Masks Directory** (if using panoptic segmentation): Typically named similar to `train2017/`

### Running the Script

Use the following command template to run the conversion script. Make sure to adjust the paths and filenames to match your dataset's location and your specific requirements:

```bash
python create_coco_tf_record.py \
    --image_dir="/path/to/coco/images/train2017" \
    --object_annotations_file="/path/to/coco/annotations/instances_train2017.json" \
    --caption_annotations_file="/path/to/coco/annotations/captions_train2017.json" \
    --panoptic_annotations_file="/path/to/coco/annotations/panoptic_train2017.json" \
    --panoptic_masks_dir="/path/to/coco/panoptic_masks/train2017" \
    --include_masks=True \
    --include_panoptic_masks=True \
    --output_file_prefix="/path/to/output/tfrecords/train" \
    --num_shards=100
```

Replace `/path/to/` with the actual paths where your COCO dataset images and annotations are stored. The `output_file_prefix` flag specifies the output directory and filename prefix for the generated TFRecord files, while the `num_shards` flag indicates how many shard files to create for the dataset.

### Important Options

- **Include Masks**: Set `--include_masks=True` to include instance segmentation masks in the TFRecords. 
- **Include Panoptic Masks**: Use `--include_panoptic_masks=True` for panoptic segmentation tasks, which require both instance and semantic segmentation data.
- **Sharding**: Splitting the dataset into multiple shards (`--num_shards`) can significantly improve data loading efficiency during model training.
- **Panoptic Annotations**: For panoptic segmentation, both `--panoptic_annotations_file` and `--panoptic_masks_dir` must be specified.


## Example Scripts 
After completing the above steps, you can get started with training your model! Within the scripts folder you can find the training and evaluation scripts for different compute platforms (CPU/GPU/TPU).  
*Remember to load the correct modules as required by each compute platform!*

```
scripts/
  eval_cpu.sh
  eval_gpu.sh
  eval_tpu.sh
  train_cpu.sh
  train_gpu.sh
  train_tpu.sh
```

## (Recommended) Working with TPUs

### Environment Variables 
Manually set the environment variables as follows:
```
export PYTHONPATH=$PYTHONPATH:~/models
export RESNET_CKPT={}
export MODEL_DIR={} # filepath to store logs
export TRAIN_BATCH_SIZE={}
export EVAL_BATCH_SIZE={}

export TPU_NAME={}
export TPU_SOFTWARE={}
export TPU_PROJECT={}
export TPU_ZONE={}
export TFRECORDS_DIR={} # .tfrecord datafolder

export ON_TPU=True 

export BASE_LR=0.0001
export IMG_SIZE=640
export NO_OBJ_CLS_WEIGHT=0.001

export DEEP_SUPERVISION=False 
```

### Training 
```
export OVERRIDES="runtime.distribution_strategy=tpu,runtime.mixed_precision_dtype=float32,\
task.train_data.global_batch_size=$TRAIN_BATCH_SIZE,\
task.model.which_pixel_decoder=transformer_fpn,\
task.init_checkpoint=$RESNET_CKPT"
python3 models/official/projects/maskformer/train.py \
  --experiment maskformer_coco_panoptic \
  --mode train \
  --model_dir $MODEL_DIR \
  --tpu $TPU_NAME \
  --params_override $OVERRIDES
```

### Evaluation 
```
export OVERRIDES="runtime.distribution_strategy=tpu,runtime.mixed_precision_dtype=float32,\
task.validation_data.global_batch_size=$EVAL_BATCH_SIZE,task.model.which_pixel_decoder=transformer_fpn,\
task.init_checkpoint_modules=all,\
task.init_checkpoint=$MASKFORMER_CKPT"
python3 train.py \
  --experiment maskformer_coco_panoptic \
  --mode eval \
  --model_dir $MODEL_DIR \
  --tpu $TPU_NAME \
  --params_override=$OVERRIDES
```


