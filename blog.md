---
title: Blog
layout: blog
menu: /blog
---

{% for post in site.posts %}
<article class="blog-post">
    <h2 class="display-5 link-body-emphasis mb-1 subtitle-a"><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></h2>
    <p class="blog-post-meta">{{ post.date | date: "%-d %B %Y" }} por <a href="#">{% if page.author %}
    {{ page.author }}
    {% else %}
    {{ site.default_author }}
    {% endif %}</a></p>

    {% if post.excerpt %}
        {{ post.excerpt }}
    {% endif %}
   <p class="link-read fw-bold text-end mb-0"><a href="{{ site.url }}/{{ post.url }}">LEER MÁS<i class="bi bi-chevron-right"></i></a></p>
</article>
{% endfor %}