---
layout: page
title: Sinema
---
<center>
<h2>
  Sinema Hakkında
</h2>

  
</center>

<ul>
  {% for sinema in site.sinema %}
    <li class="spaced">
      <a href="{{ sinema.url }}">{{ sinema.title }}</a> {{ sinema.date | date_to_long_string }}
    </li>
  {% endfor %}
</ul>
