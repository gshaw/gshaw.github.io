---
title: Gerry Shaw's Home Page
---

<img class="profile-pic" src="gerry.jpg" alt="Gerry Shaw">

<hgroup>
  <h1>👋 Hey, I'm Gerry!</h1>
  <p>
    He/Him. I'm an independent software developer living in Vancouver, Canada.
  </p>
</hgroup>

- [gerry_shaw@yahoo.com](mailto:gerry_shaw@yahoo.com)
- <a rel="me" href="https://mas.to/@gshaw">Mastodon</a>
- [GitHub](https://github.com/gshaw)
- [Stack Overflow](https://stackoverflow.com/users/265940/gerry-shaw)
- [Resume](/resume)

## My Apps

---

<div class="app-card">
  <a href="https://landnav.app/">
    <img src="/landnav/icon.png" alt="Land Nav app icon">
  </a>
  <hgroup>
    <h3><a href="https://landnav.app/">Land Nav</a></h3>
    <p>
      A land navigation tool built for iOS with pro features everybody can use.
    </p>
  </hgroup>
</div>

<div class="app-card">
  <a href="https://aedsim.com">
    <img src="/aedsim/icon.png" alt="AED Simu app icon">
  </a>
  <hgroup>
    <h3><a href="https://aedsim.com">AED Sim</a></h3>
    <p>
      A realistic defibrillator simulator for iOS built for CPR training.
    </p>
  </hgroup>
</div>
<div class="app-card">
  <a href="https://birdsnearme.com">
    <img src="/birdsnearme/icon.jpg" alt="Birds Near Me app icon">
  </a>
  <hgroup>
    <h3><a href="https://birdsnearme.com">Birds Near Me</a></h3>
    <p>
      Worldwide bird field guide. Find what birds are near you anywhere in the world. Free. No ads.
    </p>
  </hgroup>
</div>

<div class="app-card">
  <a href="/littlefaker/">
    <img src="/littlefaker/icon.png" alt="Little Faker app icon">
  </a>
  <hgroup>
    <h3><a href="/littlefaker/">Little Faker</a></h3>
    <p>
      Fast fake text generation for macOS. Free. No ads.
    </p>
  </hgroup>
</div>

## Other Pages

---

{% assign latest_book = site.data.books | sort: 'date' | reverse | first %}

<div class="app-card">
  <a href="/books/">
    <img src="/books/{{latest_book.id}}.jpg" alt="Books">
  </a>
  <hgroup>
    <h3><a href="/books/">Favorite Books</a></h3>
    <p>
      I like to read. Here are some of the books that have influenced who I am.
    </p>
  </hgroup>
</div>

<div class="app-card">
  <a href="/recipes/">
    <img src="/recipes/thumb.jpg" alt="Delicous food">
  </a>
  <hgroup>
    <h3><a href="/recipes/">Favorite Recipes</a></h3>
    <p>
      I like to cook. Double the vegetables, half (or none) of the meat.
    </p>
  </hgroup>
</div>

{% include footer.html %}
