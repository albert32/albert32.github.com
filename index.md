---
layout: post
title: 
tagline: 
---
{% include JB/setup %}

{% include post-info.html %}


<div class="row">
    <div class="span8" style="margin-top:20px;">
      <!--[> iterate through the posts on this page <]-->
      {% for page in paginator.posts %}
        <div class="post">
          <h1><a href="{{ page.url }}">{{ page.title }}</a></h1>
          <p class="meta">{{ page.date | date: "%B %e, %Y" }}</p>
            {{ page.content | postmorefilter: page.url, "More..." }}
        </div>
      {% endfor %}

      <!--[> links to prev and next pages for browsing thru archives <]-->
      {% if paginator.previous_page == 1 %}
        <span id="newer"><a href="/">&laquo;&laquo; Newer Entries</a></span>
      {% elsif paginator.previous_page %}
        <span id="newer"><a href="/page{{ paginator.previous_page }}">&laquo;&laquo; Newer Entries</a></span>
      {% endif %}
      {% if paginator.next_page %}
        <span id="older"><a href="/page{{ paginator.next_page }}">Older Entries &raquo;&raquo;</a></span>
      {% endif %}

    </div>

    <div class="span4" style="margin-top:20px;">
        <h3>���з���</h3>
        <ul class="categories">
            {% assign categories_list = site.categories %}
            {% include JB/categories_list %}
        </ul>
        <!--{% for category in site.categories %} -->
          <!--<h2 id="{{ category[0] }}-ref">{{ category[0] | join: "/" }}</h2>-->
          <!--<ul>-->
            <!--{% assign pages_list = category[1] %} -->
            <!--{% include JB/pages_list %}-->
          <!--</ul>-->
        <!--{% endfor %}-->
    </div>
</div>