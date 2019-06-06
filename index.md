---
title: Sample Custom Schemas
layout: default
---

# {{ page.title }}
{: .text-primary}

{% assign files = site.static_files | where: "extname", ".json" | group_by_exp: "item",
"item.path | remove_first: '/' | split: '/' | shift | first" %}
<!-- {{ files | jsonify }}
{% for folder in files %}
  - {{ folder.name }}
  {% for file in folder.items %}
    - [{{ file.name }}]({{ file.path }}): {{ site.url }}{{ file.path }}
  {% endfor %}
{% endfor %} -->
{% for folder in files %}
<div class="card mb-3">
  <h4 class="card-header">{{ folder.name }}</h4>
  <ul class="list-group list-group-flush">
  {% for file in folder.items %}  
    {% assign fpath = file.path | split: "/" %}
    {% assign fsize = fpath.size | minus: 2 %}
    {% assign ffolder = fpath[fsize] %}
    {% assign fobj = site.data[ffolder][file.basename] %}

    <li class="list-group-item">
    <h5 class="list-group-item-header">{{fobj.title}}</h5>
    <div><a href="{{ file.path | relative_url }}">{{ site.url }}{{ file.path | relative_url }}</a></div>
    <div>{{fobj.description}}</div>
    <div>Version: <span class="text-success">{{fobj.version}}</span></div>
    </li>
  {% endfor %}
  </ul>
</div>
{% endfor %}
