---
layout: default
title: 日々駄文
---
# 日々駄文

<ul>
	{% for post in site.posts %}
	<li>
		<a href="{{ site.baseurl }}{{ post.url }}">{{ post.date | date: '%Y/%m/%d' }} : {{ post.title }}</a>
	</li>
	{% endfor %}
</ul>

