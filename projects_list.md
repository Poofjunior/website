---
layout: bootstrap
years: [2015, 2014, 2013, 2012, 2011]
---
<div class="container">
  <div class="row">
    <div class="col-md-2">
      <div class="well sidebar-nav-fixed">
{% for year in page.years %}
<center>
<h3><a href="#{{ year }}"><i class="icon-chevron-right"></i>{{ year }}</a></h3>
</center>
{% endfor %}
      </div>
    </div>
    <div class="col-md-10 offset2">
      <div class="jumbotron">

{% comment %}
  Note: Projects must be named in format
  <year>-<month>-<date>-<project_name>.md
  such that they appear in site.pages in alphabetical order.

  Running time on this list generator is O(N^2), but no big deal, right??
{% endcomment %}

{% for year in page.years %}
<section id="{{ year }}">
<h2> {{ year }} </h2>
  {% for p in site.pages reversed%}
    {% if p.layout == "project_entry" %}
      {% if p.year == year %}
<div class="row">
  <div class="col-md-3">
    <a href="{{ p.url }}">
      <img src="{{ p.top_image_link }}" width=100/>
    </a>
  </div>
  <div class="col-md-9">
    <a href="{{ p.url }}">
      <h4>{{ p.title }}</h4>
    </a>
    {{ p.tagline }}
  </div>
</div>
<br>
      {% endif %}
    {% endif %}
  {% endfor %}
{% endfor %}

      </div>
    </div>
  </div>
</div>
