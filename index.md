---
layout: index
title:  "Niklas Lindblad"
---

## A blog about software engineering, tools and agile practices!

### Posts

{% for post in site.posts %}
  <p>{{ post.date | date_to_string }} - <a href="{{ post.url }}">{{ post.title }}</a></p>
{% endfor %}
