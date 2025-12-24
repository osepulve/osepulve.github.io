o---
layout: book-shelf
title: bookshelf
permalink: /books/
nav: false
collection: books
---

<div class="bookshelf">

  {% comment %} 1. Separate 'Mentoring' from everything else {% endcomment %}
  {% assign mentoring_books = site.books | where: "category", "Mentoring" %}
  {% assign other_books = site.books | where_exp: "item", "item.category != 'Mentoring'" %}

  {% comment %} 2. Mentoring Section with your custom description {% endcomment %}
  {% if mentoring_books.size > 0 %}
    <h2 class="category">For current/prospective students</h2>
    
    <div class="mentoring-description" style="margin-bottom: 2rem;">
      <blockquote>
        These books have helped me get to where I am right now. They are not the holy grail, but there are lucid bits in each chapter of them that may help you navigate academia, too. Besides my own mentors, these are the sources of most of the practical and/or philosophical advice I will give you.
      </blockquote>
      <p><em>*Please note that I do not endorse or back any author's political views.</em></p>
    </div>

    <div class="container">
      <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3">
        {% assign sorted_mentoring = mentoring_books | sort: "importance" %}
        {% for item in sorted_mentoring %}
          {% include projects.html %}
        {% endfor %}
      </div>
    </div>
  {% endif %}

  <hr class="category-separator" style="margin: 3rem 0;">

  {% comment %} 3. Group the rest by Year {% endcomment %}
  {% assign grouped_by_year = other_books | group_by_exp: "item", "item.date | date: '%Y'" %}
  {% assign sorted_years = grouped_by_year | sort: "name" | reverse %}

  {% for year_group in sorted_years %}
    <h2 class="category">{{ year_group.name }}</h2>
    <div class="container">
      <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3">
        {% for item in year_group.items %}
          {% include projects.html %}
        {% endfor %}
      </div>
    </div>
  {% endfor %}

</div>
