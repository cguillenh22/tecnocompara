---
layout: default
title: "Últimas actualizaciones"
description: "Comparativas y guías de TecnoCompara revisadas más recientemente."
permalink: /actualizaciones/
---
<div class="container">
  <section class="hero">
    <span class="eyebrow">Frescura de contenido</span>
    <h1>Últimas actualizaciones</h1>
    <p class="lede">
      Nuestras comparativas de precios y modelos ("actualizables") se
      revisan cada 2-3 meses. Aquí puedes ver qué se actualizó más
      recientemente.
    </p>
  </section>

  {% assign updated = site.articulos | sort: "date_modified" | reverse %}
  <div class="card-grid">
    {% for post in updated limit: 24 %}
    <div class="card">
      <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
      <div class="meta">
        {% if post.content_type == 'volatil' %}Actualizable{% else %}Guía{% endif %}
        · <span class="update-badge">Actualizado {{ post.date_modified | date: "%-d %b %Y" }}</span>
      </div>
    </div>
    {% endfor %}
  </div>
</div>
