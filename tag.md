---
layout: default
active: tag
title: Blog Posts by Tag
desc: "A list of posts organized by tags"

---

Click on a tag to see relevant list of posts.

<ul class="tags">
{% for tag in site.tags %}
  {% assign t=tag|first %}
  <li><a href="/tag.html#{{t | downcase | replace:" ","-"}}">{{ t | downcase}}</a></li>
{% endfor %}
</ul>

---

{% for tag in site.tags %}
  {% assign t = tag | first %}
  {% assign posts = tag | last %}

<h4><a name="{{t | downcase | replace:" ","-" }}"></a><a class="internal" href="/tag.html#{{t | downcase | replace:" ","-" }}">{{ t | downcase }}</a></h4>

<ul>
{% for post in posts %}
  {% if post.tags contains t %}
  <li>
    <span class="date">{{ post.date | date: "%Y-%m-%d"  }}</span>
    <a href="{{ post.url }}">{{ post.title }}</a> -- {% for itag in post.tags %} <a class="tagvec" href="/tag.html#{{itag | downcase | replace:" ","-"}}">{{ itag | downcase}}</a> {% endfor %}
  </li>
  {% endif %}
{% endfor %}
</ul>


---

{% endfor %}
