---
title: Favorite Books
permalink: /books/
---

# {{page.title}}

---

Below is a selection of books that have shaped me in some way and that I recommend. If these look interesting I post all of my reading on my [GoodReads account](https://www.goodreads.com/user/show/5720682-gerry).

{% assign books = site.data.books | sort: 'date' | reverse %}

<section>
  {% for book in books %}
    <a href="#{{book.title | slugify}}">
      <img
        alt="{{book.title}} by {{book.author}}"
        src="/books/{{book.id}}.jpg"
        class="tile-pic"
      >
    </a>
  {% endfor %}
</section>

<section>
  {% for book in books %}
    <div id="{{book.title | slugify}}" class="card card-wide-images">
      <a href="https://www.goodreads.com/book/show/{{book.id}}">
        <img
          alt="{{book.title}} by {{book.author}}"
          src="/books/{{book.id}}.jpg"
          class="card-pic"
        >
      </a>
      <div class="card-details">
        <hgroup>
          <h3><a href="https://www.goodreads.com/book/show/{{book.id}}">{{book.title}}</a></h3>
          <p>by {{book.author}}</p>
        </hgroup>
        <p>
          {{book.review | newline_to_br}}
        </p>
      </div>
    </div>
  {% endfor %}
</section>
