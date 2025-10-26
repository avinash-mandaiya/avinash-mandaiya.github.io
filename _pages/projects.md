---
layout: page
title: Research
permalink: /research/
#description: A growing collection of your cool projects.
nav: true
nav_order: 2
# To show categories later, simply uncomment or redefine:
# display_categories: [work, fun]
horizontal: true
---

<!-- pages/projects.md -->

<div class="projects">

  {% comment %}
    If display_categories is defined, show category sections.
    Otherwise, show a simple list (no categories).
  {% endcomment %}

  {% if page.display_categories %}
    {% for category in page.display_categories %}
      <h2 class="category-title">{{ category | capitalize }}</h2>

      {% assign projects_in_category = site.projects | where_exp: "item", "item.categories contains category" %}
      {% assign sorted_projects = projects_in_category | sort: "importance" %}

      {% if page.horizontal %}
        <div class="container mb-5">
          <div class="row">
            {% for project in sorted_projects %}
              <div class="col-12 mb-4">
                {% include projects_horizontal.liquid %}
              </div>
            {% endfor %}
          </div>
        </div>
      {% else %}
        <div class="row row-cols-1 row-cols-md-3 mb-5">
          {% for project in sorted_projects %}
            {% include projects.liquid %}
          {% endfor %}
        </div>
      {% endif %}
    {% endfor %}

  {% else %}
    <!-- No categories defined: show all projects -->
    {% assign sorted_projects = site.projects | sort: "importance" %}

    {% if page.horizontal %}
      <div class="container">
        <div class="row">
          {% for project in sorted_projects %}
            <div class="col-12 mb-4">
              {% include projects_horizontal.liquid %}
            </div>
          {% endfor %}
        </div>
      </div>
    {% else %}
      <div class="row row-cols-1 row-cols-md-3">
        {% for project in sorted_projects %}
          {% include projects.liquid %}
        {% endfor %}
      </div>
    {% endif %}
  {% endif %}

</div>
