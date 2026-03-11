---
layout: default
---

<style>
.publish-info {
    color: #666;
    font-size: 0.95em;
    border-left: 4px solid #0366d6;
    padding: 12px 15px;
    margin: 25px 0;
    background-color: #f8f9fa;
    border-radius: 0 8px 8px 0;
    box-shadow: 0 2px 4px rgba(0,0,0,0.05);
}
.current-time {
    color: #28a745;
    font-weight: bold;
}
/* 给文章列表加点样式 */
.post-item {
    margin-bottom: 30px;
    padding-bottom: 20px;
    border-bottom: 1px solid #eee;
}
.post-title {
    color: #0366d6;
    text-decoration: none;
}
.post-title:hover {
    text-decoration: underline;
}
.post-date {
    color: #666;
    font-size: 0.9em;
}
.read-more {
    display: inline-block;
    margin-top: 10px;
    color: #0366d6;
    text-decoration: none;
}
.read-more:hover {
    text-decoration: underline;
}
</style>

# 👋 欢迎来到我的博客

<div class="publish-info">
    📅 本博客创建于 <strong><span id="publish-time"></span></strong>
</div>
<p>⏰ 当前时间：<span class="current-time" id="current-time"></span></p>
<p>✍️ 这是我通过 GitHub Pages 搭建的个人博客，使用 Netlify CMS 管理内容。</p>

---

## 📚 最新文章

{% for post in site.posts %}
<div class="post-item">
    <h3><a href="{{ post.url }}" class="post-title">{{ post.title }}</a></h3>
    <span class="post-date">{{ post.date | date: "%Y年%m月%d日" }}</span>
    <p>{{ post.excerpt | strip_html | truncate: 200 }}</p>
    <a href="{{ post.url }}" class="read-more">阅读全文 →</a>
</div>
{% endfor %}

<!-- Netlify Identity Widget -->
<script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>

<script>
// 你原来的 JavaScript 代码保持不变
if (window.netlifyIdentity) {
  window.netlifyIdentity.on("init", function (user) {
    if (!user) {
      window.netlifyIdentity.on("login", function () {
        document.location.href = "/admin/";
      });
    }
  });
}

function getPublishTime() {
    let publishTime = localStorage.getItem('blogPublishTime');
    if (!publishTime) {
        const now = new Date();
        const year = now.getFullYear();
        const month = now.getMonth() + 1;
        const day = now.getDate();
        const hour = now.getHours().toString().padStart(2, '0');
        const minute = now.getMinutes().toString().padStart(2, '0');
        const second = now.getSeconds().toString().padStart(2, '0');
        publishTime = `${year}年${month}月${day}日${hour}时${minute}分${second}秒`;
        localStorage.setItem('blogPublishTime', publishTime);
    }
    return publishTime;
}

document.getElementById('publish-time').innerText = getPublishTime();

function updateCurrentTime() {
    const now = new Date();
    const year = now.getFullYear();
    const month = now.getMonth() + 1;
    const day = now.getDate();
    const hour = now.getHours().toString().padStart(2, '0');
    const minute = now.getMinutes().toString().padStart(2, '0');
    const second = now.getSeconds().toString().padStart(2, '0');
    document.getElementById('current-time').innerText = `${year}年${month}月${day}日${hour}时${minute}分${second}秒`;
}

updateCurrentTime();
setInterval(updateCurrentTime, 1000);
</script>
