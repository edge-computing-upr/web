---
layout: page
title: Members
slim: true
---

<div class="container">
    {% for big_group in site.data.members %}
        <div class="row">
            <div class="col-12 text-center">
                {% if big_group.website %}
                    <a target="_blank" href="{{ big_group.website }}"><h1 class="display-4">{{ big_group.name }}</h1></a>
                {% else %}
                    <h1 class="display-4">{{ big_group.name }}</h1>
                {% endif %}
            </div>
        </div>
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
                        <a target="_blank" href="{{ member.website }}">
                            <img class="img-fluid rounded-circle" src="{{ member.image }}" alt="{{ member.alt }}">
                        </a>
                        <div class="mt-2">
                            {% if member.website %}
                                <a target="_blank" href="{{ member.website }}">{{ member.name }}</a>
                            {% else %}
                                {{ member.name }}
                            {% endif %}
                            {% if member.role %}
                                <br><span class="text-muted" style="font-size: smaller;">{{ member.role }}</span>
                            {% endif %}
                        </div>
                    </div>
                {% endfor %}
            </div>
        {% endfor %}
    {% endfor %}
</div>
