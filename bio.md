---
layout: page
title: Bio
description: Who the hell are you?
permalink: /bio/
menu: true
---

{% assign author = site.authors | where: "name", "nilslappe" | first %}
<style>
li {
padding: 0 !important; //Yes i did this dirty - you caught me :)
}
</style>
<h1>Bio</h1>
<h3 style="padding-top: 0; padding-bottom: 3rem">So, who the hell are you?</h3>
<div class="details">
  {% if author.photo %}
  <img class="img-rounded" src="{{ author.photo }}" alt="{{ author.display_name }}">
  {% else %}
  <img class="img-rounded" src="/assets/img/user.jpg" alt="{{ author.display_name }}">
  {% endif %}
</div>
Well, you were interested enough to check out the Bio soooo... Yeah, this is me - Nils.
Born 1992 in Germany where i still live and work.

Since the 01.01.2018 i'm an offical, employed Software Developer with quite a thirst for knowledge. - Even though i graduated later in March 2019. According to my degree I'm an "IT-Analyst" now.

Since then i had to get familiar with an enormous TechStack.

- Javascript/Typescript/Angular2+
- PHP/Laravel
- Dart/Flutter,
- GO/Mux/IRIS
- Elasticsearch
- Docker
- (Gitlab) CI/CD
- Microservice- & Softwarearchitecture

I'm fascinated by Software and try to learn and improve in as many things as i can. Which also explains why i come home from programming at work... to fire up the IDE on my private notebook and start to code.

I won't win a prize for designs though. I'm more of a logic guy 😄

The aim of this Blog is to document and give back some of the things i learned.