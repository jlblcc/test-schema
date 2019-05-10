---
title: Sample Custom Schemas
layout: default
---

# {{ page.title }}

{% assign files = site.static_files | where: "extname", ".json" | group_by_exp: "item",
"item.path | remove_first: '/' | split: '/' | first" %}
<!-- {{ files | jsonify }} -->
<!-- {% for folder in files %}
  - {{ folder.name }}
  {% for file in folder.items %}
    - [{{ file.name }}]({{ file.path }}): {{ site.url }}{{ file.path }}
  {% endfor %}

{% endfor %} -->

{% for folder in files %}
<div class="card mb-3">
  <h5 class="card-header">{{ folder.name }}</h5>
  <ul class="list-group list-group-flush">
  {% for file in folder.items %}
    <li class="list-group-item"><a href="{{ file.path }}">{{ file.name }}</a>: {{ site.url }}{{ file.path }}</li>
  {% endfor %}
  </ul>
</div>
{% endfor %}
