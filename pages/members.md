---
layout: page
title: Members
slim: true
full-width: true
css:
  - "/index.css"
  - "/assets/css/publications.css"
---

<div class="container-fluid">
    <div class="mx-auto" style="width: 80vw;">
    {% for big_group in site.data.members %}
        {% unless big_group.name == 'Faculty' %}
            <div class="row">
                <div class="col-12 text-center">
                    {% if big_group.website %}
                        <a target="_blank" href="{{ big_group.website }}"><h1 class="display-4">{{ big_group.name }}</h1></a>
                    {% else %}
                        <h1 class="display-4">{{ big_group.name }}</h1>
                    {% endif %}
                </div>
            </div>
        {% endunless %}
        {% if big_group.name == 'Faculty' %}
            <div class="faculty-section pb-5">
                {% assign faculty_members = "" | split: "" %}
                {% for group in big_group.list %}
                    {% assign faculty_members = faculty_members | concat: group.list %}
                {% endfor %}
                {% for member in faculty_members %}
                    <div class="row mt-4 align-items-center">
                        <div class="col-md-4 col-sm-12 text-center mb-3 mb-md-0">
                            {% if member.image %}
                                <div class="position-relative d-inline-block" style="max-width: 30vh;">
                                    <div class="decor-shape shape-1" style="z-index: 1; border-radius: 10px;"></div>
                                    <div class="decor-shape shape-2" style="z-index: 1; border-radius: 10px;"></div>
                                    <a target="_blank" href="{{ member.website }}">
                                        <img class="img-fluid" src="{{ member.image }}" alt="{{ member.name }}" style="position: relative; z-index: 2; border-radius: 10px; max-height: 30vh; max-width: 30vh; object-fit: cover; width: 80%;">
                                    </a>
                                </div>
                            {% endif %}
                        </div>
                        <div class="col-md-8 col-sm-12">
                            <h2 class="h3 mb-2">
                                {% if member.website %}
                                    <a target="_blank" href="{{ member.website }}">{{ member.name }}</a>
                                {% else %}
                                    {{ member.name }}
                                {% endif %}
                            </h2>
                            {% if member.role %}
                                <div class="text-muted mb-2">{{ member.role }}</div>
                            {% endif %}
                            {% if member.alt %}
                                <p style="color: #5f6b7a; font-size: 0.98em; line-height: 1.6;">{{ member.alt }}</p>
                            {% endif %}
                        </div>
                    </div>
                {% endfor %}
            </div>
        {% elsif big_group.name == 'Alumni' %}
            <div style="width: 60vw;">
            {% for group in big_group.list %}
                <div class="row mt-4">
                    {% if group.name %}
                        <div class="col-12">
                            {% if group.website %}
                                <a target="_blank" href="{{ group.website }}"><h2 class="h4">{{ group.name }}</h2></a>
                            {% else %}
                                <h2 class="h4">{{ group.name }}</h2>
                            {% endif %}
                        </div>
                    {% endif %}
                </div>
                <div class="row">
                    <div class="col-12">
                        {% assign sorted_group = group.list | sort: 'name' %}
                        <ul class="pub-list list-unstyled" style="padding-left: 0; font-size: 0.92em;">
                            {% for member in sorted_group %}
                                <li>
                                    {% if member.website %}
                                        <a target="_blank" href="{{ member.website }}">{{ member.name }}</a>
                                    {% else %}
                                        {{ member.name }}
                                    {% endif %}
                                    {% if member.role %}
                                        <span class="text-muted" style="font-size: smaller;"> — {{ member.role }}</span>
                                    {% endif %}
                                </li>
                            {% endfor %}
                        </ul>
                    </div>
                </div>
            {% endfor %}
            </div>
        {% else %}
            {% for group in big_group.list %}
                <div class="row mt-4">
                    {% if group.name %}
                        <div class="col-12 text-center">
                            {% if group.website %}
                                <a target="_blank" href="{{ group.website }}"><h2 class="h4">{{ group.name }}</h2></a>
                            {% else %}
                                <h2 class="h4">{{ group.name }}</h2>
                            {% endif %}
                        </div>
                    {% endif %}
                </div>

                <div class="row">
                    {% for member in group.list %}
                        <div class="col-xl-3 col-lg-4 col-md-6 col-sm-6 col-12 text-center mb-4">
                            {% if member.image %}
                                <div class="position-relative d-inline-block" style="max-width: 20vh;">
                                    <div class="decor-shape shape-1" style="z-index: 1; width: 60px; height: 60px; border-radius: 10px;"></div>
                                    <div class="decor-shape shape-2" style="z-index: 1; width: 80px; height: 80px; border-radius: 10px;"></div>
                                    <a target="_blank" href="{{ member.website }}">
                                        <img class="img-fluid" src="{{ member.image }}" alt="{{ member.name }}" style="position: relative; z-index: 2; border-radius: 10px; max-height: 20vh; max-width: 20vh; object-fit: cover; width: 80%;">
                                    </a>
                                </div>
                            {% endif %}
                            <div class="mt-2" style="padding-top: 2.5vh; padding-bottom: 2.5vh">
                                {% if member.website %}
                                    <a target="_blank" href="{{ member.website }}">{{ member.name }}</a>
                                {% else %}
                                    {{ member.name }}
                                {% endif %}
                                {% if member.role %}
                                    <div class="text-muted" style="font-size: smaller;">{{ member.role }}</div>
                                {% endif %}
                                {% if member.alt %}
                                    <p style="color: #5f6b7a; font-size: 0.9em; line-height: 1.5; margin-top: 6px;">{{ member.alt }}</p>
                                {% endif %}
                            </div>
                        </div>
                    {% endfor %}
                </div>
            {% endfor %}
        {% endif %}
    {% endfor %}
    </div>
</div>
