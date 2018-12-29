---
layout: page
title: Projects
permalink: /projects/
---

This page denotes a selection of my favorite projects, all developed in my free time.

<ul class="unstyled">
{% for project in site.data.projects %}
  <li>
   <div>
    <h3>
      <a href="{{ project.url }}">
        {{ project.name }}
      </a>
    </h3>
    <p>
      {{ project.description | markdownify }}
    </p>
    <!-- <ul>
      {% for tag in project.tags %}
        <li>{{ tag }}</li> 
      {% endfor %}
    </ul> -->
   </div>
  </li>
{% endfor %}
</ul>

[jekyll-organization]: https://github.com/jekyll
