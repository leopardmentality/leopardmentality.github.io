---
icon: fas fa-list
order: 5
---
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <span>{{ post.date | date: "%b %d, %Y" }}</span>
    </li>
  {% endfor %}
</ul>
