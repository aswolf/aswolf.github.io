---
layout: default
active: notes
title: Research Notes

---

Welcome to my online research notebook. I intend to store a set of notes here useful for my own research and student mentoring. 

The notes are organized by tags. **Click on a tag to jump down to a sorted list of relevant pages.** Since notes are continuously updated, the dates reflect the most recent modification.

<ul class="tags">
{% for tag in site.tags %}
  {% assign t=tag|first %}
  <li><a href="/notes.html#{{t | downcase | replace:" ","-"}}">{{ t | downcase}}</a></li>
{% endfor %}
</ul>

---

{% for tag in site.tags %}
  {% assign t = tag | first %}
  {% assign posts = tag | last %}

<h4><a name="{{t | downcase | replace:" ","-" }}"></a><a class="internal" href="/notes.html#{{t | downcase | replace:" ","-" }}">{{ t | downcase }}</a></h4>

<ul>
{% for post in posts %}
  {% if post.tags contains t %}
  <li>
    <span class="date">{{ post.date | date: "%Y-%m-%d"  }}</span>
    <a href="{{ post.url }}">{{ post.title }}</a> -- {% for itag in post.tags %} <a class="tagvec" href="/notes.html#{{itag | downcase | replace:" ","-"}}">{{ itag | downcase}}</a> {% endfor %}
  </li>
  {% endif %}
{% endfor %}
</ul>


---

{% endfor %}
