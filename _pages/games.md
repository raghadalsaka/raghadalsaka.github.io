---
layout: archive
title: "Classroom Games"
permalink: /games/
author_profile: true
---

Dear parents, these are the learning games I use in class. Each one runs in the browser, so your child can also play at home on a computer, tablet, or phone.

{% for game in site.data.games %}
<div class="list__item">
  <article class="archive__item">
    <h2 class="archive__item-title"><a href="{{ game.url }}">{{ game.title }}</a></h2>
    <p>{{ game.summary }}</p>
    <p><strong>How to play:</strong> {{ game.how_to_play }}</p>
    <p><a href="{{ game.url }}" class="btn btn--primary">Play {{ game.title }}</a></p>
  </article>
</div>
{% endfor %}
