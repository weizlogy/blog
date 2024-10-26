---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---

# Index

## About

- [ME](/about/)

## Updated Posts
{% assign updated_posts = site.posts | where_exp: 'post', 'post.last_modified_at != nil' %}
{% for post in updated_posts limit: 5 offset: 0 %}

- [{{ post.title }}]({{ post.url }})
> {{ post.date | date: "%Y/%m/%d" }} {% if post.last_modified_at %} ~ {{ post.last_modified_at | date: "%Y/%m/%d" }}{% endif %}

{% endfor %}

## Latest Posts

{% assign sorted_posts = site.posts | sort: 'date' | reverse %}
{% for post in sorted_posts limit: 5 offset: 0 %}

- [{{ post.title }}]({{ post.url }})
> {{ post.date | date: "%Y/%m/%d" }}

{% endfor %}