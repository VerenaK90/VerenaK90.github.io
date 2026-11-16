---
layout: page
title: Team
nav_key: team
wide: true
permalink: /team/
redirect_from:
  - /people.html
---

{% assign current = site.data.team | where: "alumnus", false %}
<div class="team-grid">
{% for person in current %}
  <article class="team-card">
    {% if person.photo and person.photo != "TODO" %}
      <img class="team-card__photo" src="{{ "/assets/images/team/" | append: person.photo | relative_url }}" alt="Portrait of {{ person.name }}">
    {% else %}
      <div class="team-card__photo team-card__photo--missing" aria-hidden="true"></div>
      <!-- TODO: add a 4:5 portrait to assets/images/team/ and set photo: in _data/team.yml -->
    {% endif %}
    <h2 class="team-card__name">{{ person.name }}</h2>
    <p class="team-card__role">{{ person.role }}</p>
    <p class="team-card__bio">{{ person.bio }}</p>
    {% if person.email %}<p class="team-card__email"><a href="mailto:{{ person.email }}">Email</a></p>{% endif %}
  </article>
{% endfor %}
</div>

<h2>Alumni</h2>
{% assign alumni = site.data.team | where: "alumnus", true %}
<ul class="alumni-list">
{% for person in alumni %}
  <li>{{ person.name }}{% if person.now and person.now != "TODO" %} — now {{ person.now }}{% endif %}</li>
{% endfor %}
</ul>
