---
layout: page
title: Publications
css:
  - "/index.css"
  - "/assets/css/publications.css"
---

<script>
function showhide(d) {
  var x = document.getElementById(d);
  if (x.style.display === "none") {
    x.style.display = "block";
  } else {
    x.style.display = "none";
  }
}
</script>

{% comment %}
  Build sections based on availability and display IEEE-style citations.
  IEEE style (simplified with available fields):
  Authors, "Title," <em>Venue</em>, Year.
{% endcomment %}

{% assign pubs_sorted = site.data.publications | sort: 'id' | reverse %}

{% assign has_preprints = false %}
{% for pub in pubs_sorted %}
  {% if pub.type and pub.type == "preprint" %}
    {% assign has_preprints = true %}
    {% break %}
  {% endif %}
{% endfor %}

{% if has_preprints %}
# Preprints
<ol class="pub-list">
{% for pub in pubs_sorted %}
  {% if pub.type and pub.type == "preprint" %}
    <li>
      {{ pub.authors }}. “{{ pub.title }},” <em>{{ pub.venue }}</em>, {{ pub.year }}.
      <span class="pub-links">
        {% if pub.pdf %}<a href="{{ pub.pdf }}">PDF</a>{% endif %}
        {% if pub.arxiv %} <a href="{{ pub.arxiv }}">arXiv</a>{% endif %}
        {% if pub.projectpage %} <a href="{{ pub.projectpage }}">Project Page</a>{% endif %}
        {% if pub.code %} <a href="{{ pub.code }}">Code</a>{% endif %}
        {% if pub.video %} <a href="{{ pub.video }}">Video</a>{% endif %}
        {% if pub.bibtex %} <a href="javascript:showhide('bib{{ pub.id }}')">Bibtex</a>{% endif %}
        {% if pub.abstract %} <a href="javascript:showhide('abs{{ pub.id }}')">Abstract</a>{% endif %}
      </span>
      <div id="bib{{ pub.id }}" style="display:none"><blockquote><div style="white-space: pre-wrap;">{{ pub.bibtex }}</div></blockquote></div>
      <div id="abs{{ pub.id }}" class="pub-abstract" style="display:none">{{ pub.abstract }}</div>
    </li>
  {% endif %}
{% endfor %}
</ol>
{% endif %}

{% assign has_pubs = false %}
{% for pub in pubs_sorted %}
  {% if pub.type != "preprint" %}
    {% assign has_pubs = true %}
    {% break %}
  {% endif %}
{% endfor %}

{% if has_pubs %}
{% if has_preprints %}
# Peer-Reviewed Publications
{% endif %}

<ol class="pub-list">
{% for pub in pubs_sorted %}
  {% if pub.type != "preprint" %}
    <li>
      {{ pub.authors }}. “{{ pub.title }},” <em>{{ pub.venue }}</em>, {{ pub.year }}.
      {% if pub.awards %} <span class="pub-award">{{ pub.awards }}</span>{% endif %}
      <span class="pub-links">
        {% if pub.pdf %} <a href="{{ pub.pdf }}">PDF</a>{% endif %}
        {% if pub.arxiv %} <a href="{{ pub.arxiv }}">arXiv</a>{% endif %}
        {% if pub.projectpage %} <a href="{{ pub.projectpage }}">[Project Page]</a>{% endif %}
        {% if pub.code %} <a href="{{ pub.code }}">Code</a>{% endif %}
        {% if pub.video %} <a href="{{ pub.video }}">Video</a>{% endif %}
        {% if pub.news %} <a href="{{ pub.news }}">In The News</a>{% endif %}
        {% if pub.news2 %} <a href="{{ pub.news2 }}">In The News 2</a>{% endif %}
        {% if pub.bibtex %} <a href="javascript:showhide('bib{{ pub.id }}')">[Bibtex]</a>{% endif %}
        {% if pub.abstract %} <a href="javascript:showhide('abs{{ pub.id }}')">Abstract</a>{% endif %}
      </span>
      <div id="bib{{ pub.id }}" style="display:none"><blockquote><div style="white-space: pre-wrap;">{{ pub.bibtex }}</div></blockquote></div>
      <div id="abs{{ pub.id }}" class="pub-abstract" style="display:none">{{ pub.abstract }}</div>
    </li>
  {% endif %}
{% endfor %}
</ol>
{% endif %}