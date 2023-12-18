---
layout: page
icon: fas fa-list
order: 5
---

<article class="px-1">
  <div class="content">
    <ul>
      {% for post in site.posts %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
      {% endfor %}
    </ul>
  </div>
</article>
