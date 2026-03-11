---
layout: default
---

# 欢迎来到我的博客

{% for post in site.posts %}
## [{{ post.title }}]({{ post.url }})
*{{ post.date | date: "%Y-%m-%d" }}*

{{ post.excerpt }}

[阅读全文]({{ post.url }})  
---
{% endfor %}
