---
layout: book-shelf
title: bookshelf
permalink: /books/
nav: false
collection: books
---

<div class="bookshelf">
  {% if site.books %}
    
    {% assign mentoring_books = site.books | where: "category", "Mentoring" %}
    {% assign other_books = site.books | where_exp: "item", "item.category != 'Mentoring'" %}

    {% comment %} 1. Mentoring Section {% endcomment %}
    {% if mentoring_books.size > 0 %}
      <h2 class="category">Mentoring</h2>
      
      <h3 class="category-subtitle" style="font-weight: 300; margin-bottom: 1.5rem; color: var(--global-text-color-light);">
        For current/prospective students
      </h3>
      
      <div class="mentoring-description" style="margin-bottom: 2.5rem;">
        <blockquote style="border-left: 5px solid var(--global-theme-color); padding-left: 1.5rem; font-style: italic;">
          These books have helped me get to where I am right now. They are not the holy grail, but there are lucid bits in each chapter of them that may help you navigate academia, too. Besides my own mentors, these are the sources of most of the practical and/or philosophical advice I will give you.
        </blockquote>
        <p><em>*Please note that I do not endorse or back any author's political views.</em></p>
      </div>

      <div class="container">
        <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3">
          {% for item in mentoring_books %}
            {% include projects.html %}
          {% endfor %}
        </div>
      </div>
    {% endif %}

    <hr class="category-separator" style="margin: 3rem 0;">

    {% comment %} 2. Group the rest by Year {% endcomment %}
    {% assign grouped_by_year = other_books | group_by_exp: "item", "item.date | date: '%Y'" %}
    {% assign sorted_years = grouped_by_year | sort: "name" | reverse %}

    {% for year_group in sorted_years %}
      {% if year_group.name != "" and year_group.name != nil %}
        <h2 class="category">{{ year_group.name }}</h2>
        <div class="container">
          <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3">
            {% for item in year_group.items %}
              {% include projects.html %}
            {% endfor %}
          </div>
        </div>
      {% endif %}
    {% endfor %}

  {% else %}
    <p>No books found in the _books collection. Please check your _config.yml.</p>
  {% endif %}
</div>
