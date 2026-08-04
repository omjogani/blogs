---
title: Devlogs
icon: fas fa-terminal
order: 0
---

<!-- ponytail: home-layout card markup with a category filter, no new collection
     and no pagination. Add pagination if devlogs ever outgrow one page. -->

{% include lang.html %}

<div id="post-list" class="flex-grow-1 px-xl-1">
  {% for post in site.categories['devlog'] %}
    <article class="card-wrapper card">
      <a href="{{ post.url | relative_url }}" class="post-preview row g-0 flex-md-row-reverse">
        {% assign card_body_col = '12' %}

        {% if post.image %}
          {% assign src = post.image.path | default: post.image %}
          {% unless src contains '//' %}
            {% assign src = post.img_path | append: '/' | append: src | replace: '//', '/' %}
          {% endunless %}

          {% assign alt = post.image.alt | xml_escape | default: 'Preview Image' %}

          {% assign lqip = null %}

          {% if post.image.lqip %}
            {% capture lqip %}lqip="{{ post.image.lqip }}"{% endcapture %}
          {% endif %}

          <div class="col-md-5">
            <img src="{{ src }}" alt="{{ alt }}" {{ lqip }}>
          </div>

          {% assign card_body_col = '7' %}
        {% endif %}

        <div class="col-md-{{ card_body_col }}">
          <div class="card-body d-flex flex-column">
            <h1 class="card-title my-2 mt-md-0">{{ post.title }}</h1>

            <div class="card-text content mt-0 mb-3">
              <p>
                {% include no-linenos.html content=post.content %}
                {{ content | markdownify | strip_html | truncate: 200 | escape }}
              </p>
            </div>

            <div class="post-meta flex-grow-1 d-flex align-items-end">
              <div class="me-auto">
                <!-- posted date -->
                <i class="far fa-calendar fa-fw me-1"></i>
                {% include datetime.html date=post.date lang=lang %}

                <!-- tags -->
                {% if post.tags.size > 0 %}
                  <i class="fa fa-tag fa-fw me-1"></i>
                  <span class="categories">
                    {% for tag in post.tags %}
                      {{ tag }}
                      {%- unless forloop.last -%},{%- endunless -%}
                    {% endfor %}
                  </span>
                {% endif %}
              </div>
            </div>
            <!-- .post-meta -->
          </div>
          <!-- .card-body -->
        </div>
      </a>
    </article>
  {% endfor %}
</div>
<!-- #post-list -->
