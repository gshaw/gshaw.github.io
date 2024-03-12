---
title: Bass Coast 2024
artists:
  -
    name: Shiba San
    youtube_id: sfD954UrNG4??si=2JsdlXudaD3ChuHt

---
<!-- markdownlint-disable MD025 MD033 -->

<style>
  .artist-pic {
  border-radius: 0.25em;
  box-shadow: 0 0 1px #777;
  width: 150px;
  margin: 0.25em;
}
</style>

![Bass Coast 2019](/bass-coast.jpg#header-pic)

# {{ page.title }}

Going to [Bass Coast 2024](https://basscoast.ca) this year as a volunteer. To get an idea of all the artists performing I collected samples. Genre with music is always subjective but I did my best. If you disagree or have a better example let me know.

---
{% assign artists = site.data.bass_coast_2024 | sort: 'name' %}

{% for artist in artists %}<a href="#{{artist.name | slugify}}"><img src="{{ artist.image_url }}" class="artist-pic" alt="{{artist.name}}"></a>
{% endfor %}
<hr>

{% for artist in artists %}
<div  id="{{artist.name | slugify}}" class="card">
  {% if artist.image_url %}
  <img src="{{ artist.image_url }}" alt="{{artist.name}}">
  {% else %}
  <img src="https://placehold.co/150x150?text=?" alt="{{artist.name}}">
  {% endif %}
  <div class="card-details">
    <div><strong>{{ artist.name }}</strong> - <small>{{ artist.genre }}</small></div>
    <div><a target="_blank" href="{{ artist.url }}">{{ artist.title }}</a></div>
    {% if artist.icon %}
    <div>{{ artist.icon }}</div>
    {% endif %}
  </div>
</div>
{% endfor %}
<br>

❤️‍🔥 indicates the performances I'm hoping not to miss.
