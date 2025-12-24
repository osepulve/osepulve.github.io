---
layout: book-shelf
title: bookshelf
permalink: /books/
nav: false
collection: books
---

<div class="bookshelf">

  {% comment %} 1. Separate 'Mindfulness' from everything else {% endcomment %}
  {% assign mindfulness_books = site.books | where: "category", "Mindfulness" %}
  {% assign other_books = site.books | where_exp: "item", "item.category != 'Mindfulness'" %}

  {% comment %} 2. Render the Mindfulness Section {% endcomment %}
  {% if mindfulness_books.size > 0 %}
    <h2 class="category">Mindfulness</h2>
    <div class="container">
      <div class="row row-cols-2">
        {% for item in mindfulness_books %}
          {% include projects.html %}
        {% endfor %}
      </div>
    </div>
  {% endif %}

  <hr>

  {% comment %} 3. Group the remaining books by year {% endcomment %}
  {% assign grouped_by_year = other_books | group_by_exp: "item", "item.date | date: '%Y'" %}
  
  {% comment %} Sort years descending (newest first) {% endcomment %}
  {% assign sorted_years = grouped_by_year | sort: "name" | reverse %}

  {% for year_group in sorted_years %}
    <h2 class="category">{{ year_group.name }}</h2>
    <div class="container">
      <div class="row row-cols-2">
        {% for item in year_group.items %}
          {% include projects.html %}
        {% endfor %}
      </div>
    </div>
  {% endfor %}

</div>

## For current/prospective students

> These books have helped me get to where I am right now. They are not the holy grail, but there are lucid bits in each chapter of them that may help you navigate academia, too. Besides my own mentors, these are the sources of most of the practical and/or philosophical advice I will give you.

*Please note that I do not endorse or back any author's political views.*
