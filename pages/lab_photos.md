---
layout: page
title: Lab Updates
slim: true
css:
  - "/index.css"
full-width: true
---

<div class="container-fluid">
  <div class="mx-auto" style="width: 80vw;">
    {% assign posts_sorted = site.posts | sort: 'date' | reverse %}
    <div class="row">
      <div class="col-lg-9 col-md-12">
        {% for post in posts_sorted %}
          {% assign collapse_id = 'lp-' | append: forloop.index0 %}
          {% assign card_id = 'lp-card-' | append: forloop.index0 %}
          <div id="{{ card_id }}">
            <div class="card mb-3" style="border-radius: 12px; overflow: hidden;">
              <div class="card-header p-0" style="background: #ffffff;">
                <button class="btn btn-link text-left w-100" type="button" data-toggle="collapse" data-target="#{{ collapse_id }}" aria-expanded="false" aria-controls="{{ collapse_id }}" style="text-decoration: none; color: inherit;">
                  <div class="row no-gutters align-items-center">
                    <div class="col-md-3 d-none d-md-block">
                      {% if post.cover-img %}
                        <img src="{{ post.cover-img | relative_url }}" alt="{{ post.title }}" class="img-fluid" style="height: 240px; width: 100%; object-fit: cover;">
                      {% elsif post.thumbnail-img %}
                        <img src="{{ post.thumbnail-img | relative_url }}" alt="{{ post.title }}" class="img-fluid" style="height: 240px; width: 100%; object-fit: cover;">
                      {% else %}
                        <div style="height: 240px; background: #f0f4f8;"></div>
                      {% endif %}
                    </div>
                    <div class="col-md-9 p-3">
                      <h3 class="h5 mb-1" style="margin: 0;">{{ post.title }}</h3>
                      <div class="text-muted" style="font-size: 0.9em;">{{ post.date | date: "%B %d, %Y" }}</div>
                      {% if post.subtitle %}
                        <div class="text-muted" style="font-size: 0.95em;">{{ post.subtitle }}</div>
                      {% endif %}
                      <div class="mt-2" style="font-size: 0.95em; color: #5f6b7a;">
                        {% if post.excerpt %}
                          {{ post.excerpt | strip_html | truncatewords: 26 }}
                        {% else %}
                          {{ post.content | strip_html | truncatewords: 26 }}
                        {% endif %}
                      </div>
                    </div>
                  </div>
                </button>
              </div>
              <div id="{{ collapse_id }}" class="collapse">
                <div class="card-body">
                  {{ post.content }}
                </div>
              </div>
            </div>
          </div>
        {% endfor %}
      </div>
      <div class="col-lg-3 d-none d-lg-block" style="border-left: 1px solid #eee;">
        <div class="pl-3" style="position: sticky; top: 80px; max-height: calc(100vh - 100px); overflow: auto;">
          <h6 class="text-muted mt-3">Posts</h6>
          <ul class="list-unstyled">
            {% for post in posts_sorted %}
              {% assign card_id = 'lp-card-' | append: forloop.index0 %}
              <li class="mb-2"><a href="#{{ card_id }}">{{ post.title }}</a></li>
            {% endfor %}
          </ul>
        </div>
      </div>
    </div>
  </div>
</div>
