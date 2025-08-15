---
layout: page
title: Guides
slim: true
css:
  - "/index.css"
full-width: true
---

<div class="container-fluid">
  <div class="mx-auto" style="width: 80vw;">
    {% assign guides = site.pages | where_exp: "p", "p.path contains 'tutorials/'" %}
    <div class="row">
      <div class="col-lg-9 col-md-12">

    <div class="row mt-4">
      <div class="col-12 text-center">
        <h2 class="h4">Environment Setup</h2>
      </div>
    </div>
        {% assign env_count = 0 %}
        {% for page in guides %}
      {% if page.path contains 'jupyter_from_lambda' or page.path contains 'TensorRT_Container' %}
        {% assign env_count = env_count | plus: 1 %}
        {% assign collapse_id = 'guide-env-' | append: env_count %}
        <div class="card mb-3" style="border-radius: 12px; overflow: hidden;">
          <div class="card-header p-0" style="background: #ffffff;">
            <button class="btn btn-link text-left w-100" type="button" data-toggle="collapse" data-target="#{{ collapse_id }}" aria-expanded="false" aria-controls="{{ collapse_id }}" style="text-decoration: none; color: inherit;">
              <div class="row no-gutters align-items-center">
                <div class="col-md-3 d-none d-md-block">
                  {% if page.cover-img %}
                    <img src="{{ page.cover-img | relative_url }}" alt="{{ page.title }}" class="img-fluid" style="height: 240px; width: 100%; object-fit: cover;">
                  {% else %}
                    <div style="height: 240px; background: #f0f4f8;"></div>
                  {% endif %}
                </div>
                <div class="col-md-9 p-3">
                  <h3 class="h5 mb-1" style="margin: 0;">{{ page.title }}</h3>
                  <div class="mt-2" style="font-size: 0.95em; color: #5f6b7a;">
                    {{ page.content | strip_html | truncatewords: 26 }}
                  </div>
                </div>
              </div>
            </button>
          </div>
          <div id="{{ collapse_id }}" class="collapse">
            <div class="card-body">
              {{ page.content }}
            </div>
          </div>
        </div>
      {% endif %}
    {% endfor %}

    <div class="row mt-4">
      <div class="col-12 text-center">
        <h2 class="h4">Hardware Setup</h2>
      </div>
    </div>
        {% assign hw_count = 0 %}
        {% for page in guides %}
      {% if page.path contains 'Jetson_Setup' %}
        {% assign hw_count = hw_count | plus: 1 %}
        {% assign collapse_id = 'guide-hw-' | append: hw_count %}
        <div class="card mb-3" style="border-radius: 12px; overflow: hidden;">
          <div class="card-header p-0" style="background: #ffffff;">
            <button class="btn btn-link text-left w-100" type="button" data-toggle="collapse" data-target="#{{ collapse_id }}" aria-expanded="false" aria-controls="{{ collapse_id }}" style="text-decoration: none; color: inherit;">
              <div class="row no-gutters align-items-center">
                <div class="col-md-3 d-none d-md-block">
                  {% if page.cover-img %}
                    <img src="{{ page.cover-img | relative_url }}" alt="{{ page.title }}" class="img-fluid" style="height: 240px; width: 100%; object-fit: cover;">
                  {% else %}
                    <div style="height: 240px; background: #f0f4f8;"></div>
                  {% endif %}
                </div>
                <div class="col-md-9 p-3">
                  <h3 class="h5 mb-1" style="margin: 0;">{{ page.title }}</h3>
                  <div class="mt-2" style="font-size: 0.95em; color: #5f6b7a;">
                    {{ page.content | strip_html | truncatewords: 26 }}
                  </div>
                </div>
              </div>
            </button>
          </div>
          <div id="{{ collapse_id }}" class="collapse">
            <div class="card-body">
              {{ page.content }}
            </div>
          </div>
        </div>
      {% endif %}
    {% endfor %}
      </div>
      <div class="col-lg-3 d-none d-lg-block" style="border-left: 1px solid #eee;">
        <div class="pl-3" style="position: sticky; top: 80px; max-height: calc(100vh - 100px); overflow: auto;">
          <h6 class="text-muted mt-3">Guides</h6>
          <ul class="list-unstyled">
            {% assign index_counter = 0 %}
            {% for page in guides %}
              {% if page.path contains 'jupyter_from_lambda' or page.path contains 'TensorRT_Container' %}
                {% assign index_counter = index_counter | plus: 1 %}
                {% assign collapse_id = 'guide-env-' | append: index_counter %}
                <li class="mb-2"><a href="#{{ collapse_id }}">{{ page.title }}</a></li>
              {% endif %}
            {% endfor %}
            {% assign index_counter = 0 %}
            {% for page in guides %}
              {% if page.path contains 'Jetson_Setup' %}
                {% assign index_counter = index_counter | plus: 1 %}
                {% assign collapse_id = 'guide-hw-' | append: index_counter %}
                <li class="mb-2"><a href="#{{ collapse_id }}">{{ page.title }}</a></li>
              {% endif %}
            {% endfor %}
          </ul>
        </div>
      </div>
    </div>
  </div>
</div>
