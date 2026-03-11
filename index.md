---
layout: default
---

# 欢迎来到我的博客

<div class="publish-info">
    📅 本博客创建于 <strong><span id="publish-time"></span></strong>
</div>
<p>当前时间：<span class="current-time" id="current-time"></span></p>
<p>这是我通过 GitHub Pages 搭建的个人博客，使用 Netlify CMS 管理内容。</p>

---

## 📚 最新文章

{% for post in site.posts %}
### [{{ post.title }}]({{ post.url }})
*{{ post.date | date: "%Y-%m-%d" }}*

{{ post.excerpt | strip_html | truncate: 200 }}

[阅读全文]({{ post.url }})  
---
{% endfor %}

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
</style>

<script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>

<script>
// Netlify Identity 登录跳转
if (window.netlifyIdentity) {
  window.netlifyIdentity.on("init", function (user) {
    if (!user) {
      window.netlifyIdentity.on("login", function () {
        document.location.href = "/admin/";
      });
    }
  });
}

// =============================================
// 功能1：记录并显示第一次发布的时间（永久保存）
// =============================================
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
        console.log('🎯 首次发布时间已记录：', publishTime);
    } else {
        console.log('📌 读取到已保存的发布时间：', publishTime);
    }
    
    return publishTime;
}

// 把发布时间显示到页面上
document.getElementById('publish-time').innerText = getPublishTime();

// =============================================
// 功能2：实时更新当前时间（每秒跳动）
// =============================================
function updateCurrentTime() {
    const now = new Date();
    const year = now.getFullYear();
    const month = now.getMonth() + 1;
    const day = now.getDate();
    const hour = now.getHours().toString().padStart(2, '0');
    const minute = now.getMinutes().toString().padStart(2, '0');
    const second = now.getSeconds().toString().padStart(2, '0');
    
    const currentTimeStr = `${year}年${month}月${day}日${hour}时${minute}分${second}秒`;
    
    const currentTimeEl = document.getElementById('current-time');
    if (currentTimeEl) {
        currentTimeEl.innerText = currentTimeStr;
    }
}

// 立即执行一次，让时间马上显示
updateCurrentTime();

// 设置定时器，每秒更新一次
setInterval(updateCurrentTime, 1000);
</script>
