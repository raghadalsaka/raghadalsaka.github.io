---
layout: archive
title: "Classroom Projects"
permalink: /projects/
og_title: "Classroom Projects by Dr. Raghad Alsaka"
description: "Classroom projects and the tools created for them by Dr. Raghad Alsaka, Ph.D. in Education — Curriculum and Instruction. Each tool runs in any web browser on a computer, tablet, or phone, with no download."
author_profile: true
---

These are projects my students work on in class, with the tools I created for them. Each tool runs in the browser, so students can work in class or at home on a computer, tablet, or phone.

{% for project in site.data.projects %}
<div class="list__item">
  <article class="archive__item">
    <h2 class="archive__item-title"><a href="{{ project.url }}">{{ project.title }}</a></h2>
    <p>{{ project.summary }}</p>
    {% for note in project.notes %}
    <p><strong>{{ note.label }}:</strong> {{ note.text }}</p>
    {% endfor %}
    <p><a href="{{ project.url }}" class="btn btn--primary">{{ project.button }}</a></p>
  </article>
</div>
{% endfor %}
