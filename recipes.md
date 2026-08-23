---
title: Favorite Recipes
permalink: /recipes/
---

# {{page.title}}

---

{% assign recipes = site.pages | where: 'layout', 'recipe' %}

<section>
  {% for recipe in recipes %}
    <div class="card card-wide-images">
      {% if recipe.picture.placeholder %}
      <div></div>
      {% else %}
      <a href="{{recipe.url}}">
        <img
          alt="{{recipe.picture.title}}"
          src="/recipes/{{recipe.picture.filename}}"
          class="card-pic"
        >
      </a>
      {% endif %}
      <div class="card-details">
        <h3><a href="{{recipe.url}}">{{recipe.title}}</a></h3>
        <p>{{recipe.summary  | newline_to_br}}</p>
      </div>
    </div>
  {% endfor %}
</section>
