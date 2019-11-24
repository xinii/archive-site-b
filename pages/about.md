---
layout: page
title: About
permalink: /about/
weight: 3
---

# **About Me**

Here is backend of **{{ site.author.name }}**'s blog,<br>
<a href=https://xinii.github.io/>Go to homepage</a>


<div class="row">
{% include about/skills.html title="Programming Skills" source=site.data.programming-skills %}
{% include about/skills.html title="Other Skills" source=site.data.other-skills %}
</div>

## Educational experience

<div class="row">
{% include about/timeline_education.html %}
</div>

## Work experience and internships

<div class="row">
{% include about/timeline_work.html %}
</div>

## Research and software works

<div class="row">
{% include about/timeline_research.html %}
</div>
