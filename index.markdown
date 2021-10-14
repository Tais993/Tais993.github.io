---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
title: Yeet
menus: header
---
<ul>
{% for item in site.menus.header %}
  <li class="menu-item-{{ loop.index }}">
    <a href="{{ item.url }}" title="Go to {{ item.title }}">{{ item.title }}</a>
  </li>
{% endfor %}
</ul>


