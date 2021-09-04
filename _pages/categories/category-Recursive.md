---
title: "Recursive"
layout: archive
permalink: categories/Recursive
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Recursive %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}