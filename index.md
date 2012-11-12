---
layout: post
title: Hello World!
tagline: Supporting tagline
---
{% include JB/setup %}

This is my first article.

## Posts list

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



{% for post in site.posts limit:3 %}
  <article class="post">
    <header>
      <h2>{{ post.title }}</h2>
     
    </header>

    <div>
   {% include post-info.html %}
    </div>
    <a href="{{ post.url }}">Read more&hellip;</a>
  </article>
{% endfor %}

