---
layout: page
title: ivan's blog
tagline: Supporting tagline
---
{% include JB/setup %}

<div class="home-page-content">
	{% for post in site.posts limit:5 %}
	<div class="home-page-post">
		<div class="post-header">
			<div class="date">{{ post.date | date_to_string }}</div>
				<div class="tags"> 
					<label>Tags: </label>{{ post.tags | array_to_sentence_string }}
				</div>
				<div class="category"> 
					<label>Category: </label>
					<span>{{ post.category }}</span>
				</div>
			</div>
			<div class="post-content">
				<div class="title"><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></div>
				<div class="abstract">{{ post.description | markdownify }}</div>
				<div style="float:right;"><a href="{{ BASE_PATH }}{{ post.url }}">阅读全文</a></div>
			</div>
			{% if forloop.index != 5 %}
		<div class="post-footer">&nbsp;</div>
		{% endif %}
	</div>
	{% endfor %}
</div>
<hr>
<div style="width:50%;margin-left:auto;margin-right:auto;text-align:center;clear:both;">
	<a href="/archive.html">查看所有{{site.posts.size}}篇文章...</a>
</div>


