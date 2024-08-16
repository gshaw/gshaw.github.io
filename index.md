---
title: Gerry Shaw's Home Page
hide_header: true
links:
  -
    title: Favorite Books
    description: I like to read. Here are some of the books that have influenced me.
    url: /books/
    image_url: /books/index.jpg
    image_alt: "Sample of one of my favorite books"
  -
    title: Favorite Recipes
    description: I like to cook. Double the vegetables, half (or none) of the meat.
    url: /recipes/
    image_url: /recipes/index.jpg
    image_alt: "Delicious meal I made"
---
![Gerry Shaw](/gerry.jpg#header-pic)

# 👋 Hey, I'm Gerry

I'm an independent software developer living in Vancouver, Canada.

- [gerry_shaw@yahoo.com](mailto:gerry_shaw@yahoo.com)
- <a rel="me" href="https://mas.to/@gshaw">Mastodon</a>
- [GitHub](https://github.com/gshaw)
- [Stack Overflow](https://stackoverflow.com/users/265940/gerry-shaw)
- [Resume](/resume)

## My Apps

---

<section>
  {% for app in site.data.apps %}
    <div class="card">
      <a href="{{app.link_url}}">
        <img
          class="card-pic"
          src="{{app.icon_url}}"
          alt="{{app.title}} app icon"
        >
      </a>
      <div class="card-details">
        <h3><a href="{{app.link_url}}">{{app.title}}</a></h3>
        <p>
          {{app.description | newline_to_br}}
        </p>
      </div>
    </div>
  {% endfor %}
</section>

## Other Stuff

---

<section>
  {% for link in page.links %}
    <div class="card">
      <a href="{{link.url}}">
        <img
          alt="{{link.image_alt}}"
          src="{{link.image_url}}"
          class="card-pic"
        >
      </a>
      <div class="card-details">
        <h3><a href="{{link.url}}">{{link.title}}</a></h3>
        <p>{{link.description | newline_to_br}}</p>
      </div>
    </div>
  {% endfor %}
</section>
