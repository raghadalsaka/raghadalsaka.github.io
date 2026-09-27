---
layout: archive
title: "Classroom Games"
permalink: /games/
og_title: "Classroom Games by Dr. Raghad Alsaka"
description: "Free learning games created by Dr. Raghad Alsaka, Ph.D. in Education — Curriculum and Instruction. Play in any web browser on a computer, tablet, or phone, with no download or sign-in."
author_profile: true
---

These are learning games I created and use in my classes. Each one runs in the browser, so anyone can play them in class or at home on a computer, tablet, or phone.

{% for game in site.data.games %}
<div class="list__item">
  <article class="archive__item">
    <h2 class="archive__item-title"><a href="{{ game.url }}">{{ game.title }}</a></h2>
    <p>{{ game.summary }}</p>
    <p><strong>How to play:</strong> {{ game.how_to_play }}</p>
    <p><a href="{{ game.url }}" class="btn btn--primary">Play {{ game.topic | default: game.title }}</a></p>
  </article>
</div>
{% endfor %}
