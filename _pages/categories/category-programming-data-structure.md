---
title: "Data Structure"
layout: archive
permalink: /categories/data_structure
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.data_structure %}
{% if posts %}
  {% assign posts = posts | sort: 'title' %}
{% endif %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}
