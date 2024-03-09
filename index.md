---
title: Gerry Shaw's Home Page
---

<img class="profile-pic" src="gerry.jpg" alt="Gerry Shaw">

# 👋 Hey, I'm Gerry

I'm an independent software developer living in Vancouver, Canada.

- [gerry_shaw@yahoo.com](mailto:gerry_shaw@yahoo.com)
- <a rel="me" href="https://mas.to/@gshaw">Mastodon</a>
- [GitHub](https://github.com/gshaw)
- [Stack Overflow](https://stackoverflow.com/users/265940/gerry-shaw)
- [Resume](/resume)

## My Apps

---

{% for app in site.data.apps %}
<div class="card">
  <a href="{{app.link_url}}">
    <img src="{{app.icon_url}}" alt="{{app.title}} app icon">
  </a>
  <div class="card-details">
    <h3><a href="{{app.link_url}}">{{app.title}}</a></h3>
    <p>
      {{ app.description }}
    </p>
  </div>
</div>
{% endfor %}

## Other Stuff

---

<div class="card">
  <a href="/books/">
    {% assign latest_book = site.data.books | sort: 'date' | reverse | first %}
    <img src="/books/{{latest_book.id}}.jpg" alt="Books">
  </a>
  <div class="card-details">
    <h3><a href="/books/">Favorite Books</a></h3>
    <p>
      I like to read. Here are some of the books that have influenced who I am.
    </p>
  </div>
</div>

<div class="card">
  <a href="/recipes/">
    <img src="/recipes/thumb.jpg" alt="Delicious food">
  </a>
  <div class="card-details">
    <h3><a href="/recipes/">Favorite Recipes</a></h3>
    <p>
      I like to cook. Double the vegetables, half (or none) of the meat.
    </p>
  </div>
</div>

{% include footer.html %}
