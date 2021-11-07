---
title: "English"
layout: archive
permalink: categories/English
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.English %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}