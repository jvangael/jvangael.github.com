---
layout: page
---
{% include JB/setup %}

{% for post in site.posts limit 4 %}
<article class="unit-article layout-post">
  <div>
    <a href="{{ BASE_PATH }}{{ post.url }}" class="lead">{{ post.title }}</a> &raquo; <span class="date">{{ post.date | date_to_string }}</span>
  </div>
  <div class="unit-inner unit-article-inner">
    <div class="content">
    {{ post.content | strip_html | truncatewords:75}}
    </div>
    <a href="{{ post.url }}">Read more...</a><br><br>
  </div>
</article>
{% endfor %}
