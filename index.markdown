---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

title: Home
layout: default
menu: /
---

<!-- ======= Hero Section ======= -->
<div id="hero" class="hero route bg-image" style="background-image: url(assets/img/hero-bg.jpg)">
    <div class="overlay-itro"></div>
    <div class="hero-content display-table">
        <div class="table-cell">
            <div class="container">
                <!--<p class="display-6 color-d">Hello, world!</p>-->
                <h1 class="hero-title mb-4">Antonio Vargas</h1>
                <p class="hero-subtitle"><span class="typed" data-typed-items="Desarrollador Web, Programador, Entusiasta de la tecnología, Ciberseguridad, IA, Amante del código, Innovador tecnológico"></span></p>
                <!-- <p class="pt-3"><a class="btn btn-primary btn js-scroll px-4" href="#about" role="button">Learn More</a></p> -->
            </div>
        </div>
    </div>
</div><!-- End Hero Section -->

<main id="main">
    <section id="blog" class="blog-mf sect-pt4 route">
        <div class="container">
            <div class="row">
                <div class="col-sm-12">
                    <div class="title-box text-center">
                        <h3 class="title-a">
                            Blog
                        </h3>
                        <p class="subtitle-a">
                            Últimos Posts.
                        </p>
                        <div class="line-mf"></div>
                    </div>
                </div>
            </div>
            <div class="row">
                {% for post in site.posts limit: 3 %}
                <div class="col-md-4 d-flex align-items-stretch">
                    <div class="card card-blog">
                        <div class="card-img">
                            <a href="{{ post.url }}"><img src="{{ site.url }}/{% if post.image %}assets/img/{{ post.image }}{% else %}{{ site.default_post_image }}{% endif %}" 
                                        alt="" class="img-fluid"></a>
                        </div>
                        <div class="card-body">
                            <div class="card-category-box">
                                <div class="card-category">
                                    <h6 class="category">{% if post.post_category %}{{ post.post_category }}{% else %}Post{% endif %}</h6>
                                </div>
                            </div>
                            <h3 class="card-title"><a href="{{ post.url }}">{{ post.title }}</a></h3>
                            <p class="card-description">
                                {% if post.excerpt %}
                                    {{ post.excerpt }}
                                {% endif %}
                            </p>
                        </div>
                        <div class="card-footer">
                            <div class="post-author">
                                <a href="#">
                                    <img src="assets/img/testimonial-2.jpg" alt="" class="avatar rounded-circle">
                                    <span class="author">
                                        {% if post.author %}
                                        {{ post.author }}
                                        {% else %}
                                        {{ site.default_author }}
                                        {% endif %}
                                    </span>
                                </a>
                            </div>
                            <div class="post-date">
                                <span class="bi bi-clock"></span> 10 min
                            </div>
                        </div>
                    </div>
                </div>
                {% endfor %}
            </div>
        </div>
    </section>
</main>
<!-- End #main -->

<!--
You can use HTML elements in Markdown, such as the comment element, and they won't
be affected by a markdown parser. However, if you create an HTML element in your
markdown file, you cannot use markdown syntax within that element's contents.
-->
