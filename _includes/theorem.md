<div class="{{ include.type }}"
    {% if include.id %}
    id="{{ include.id }}"
    {% endif %}>
    <div class="theorem-title">{{ include.type  | capitalize }}
        {% if include.num %}
            {{ include.num }}
        {% endif %}
        {% if include.name %}
            ({{ include.name }})
        {% endif %}
    </div>
    <div class="theorem-contents">
        {{ include.statement }}
    </div>
</div>