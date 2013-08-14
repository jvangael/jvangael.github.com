---
layout: page
---
{% include JB/setup %}

<div style="float: left" markdown="1">
  ![Profile Picture]({{ BASE_PATH }}/assets/images/profile.jpg)
</div>

<div style="float: left; margin-left: 40px" markdown="1">
  ###Jurgen Van Gael

  **Data Science Director, [Rangespan](http://www.rangespan.com)**

  **Profile** at [LinkedIn](http://uk.linkedin.com/in/jvangael/)

  **Code** at [GitHub](https://github.com/jvangael)

  **Twitter** at [GitHub](https://twitter.com/jvangael)

  **Google+** at [Google](https://plus.google.com/104063489577052626944)
</div>

<div style="clear:both"></div>

### Latest Posts

{% for post in site.posts limit:3 %}
<article class="unit-article layout-post">
  <div>
    <span class="lead">{{ post.title }}</span> &raquo; <span class="date">{{ post.date | date_to_string }}</span>
  </div>
  <div class="unit-inner unit-article-inner">
    <div class="content">
    {{ post.content | strip_html | truncatewords:25}}
    </div>
    <a href="{{ post.url }}">Read more...</a><br><br>
  </div>
</article>
{% endfor %}
