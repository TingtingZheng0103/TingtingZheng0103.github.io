# 郑婷婷 · Personal Archive / 个人档案馆

双语静态网站，无需安装依赖。打开 index.html 即可预览；评论联网功能需部署后测试。

## 发布到 GitHub Pages
1. 在 GitHub 创建 Public 仓库 `TingtingZheng0103.github.io`。不要覆盖已有网站。
2. 上传此目录内的文件，index.html 必须在仓库根目录。提交到 main。
3. Settings → Pages → Source: Deploy from a branch → main → / (root) → Save。
4. 等待 Actions 的 Pages 部署成功，访问 https://tingtingzheng0103.github.io/ 。
学术主页：https://tingtingzheng0103.github.io/academic.html 。它有独立页面与导航，当前与个人站共享仓库和双语内容配置；以后可拆成独立仓库。
官方：https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site

## 添加作品：只编辑 content.js
GitHub 打开 content.js → 铅笔 Edit → 保存 Commit changes。上传图片至 assets，例如 assets/stockholm.jpg。建议上传适合网页的压缩副本而非相机原片。
在 entries 数组中新增（多个条目之间以逗号分隔）：
```js
{
  "id": "first-light",
  "category": "photography",
  "title": {"zh": "第一束光", "en": "First light"},
  "subtitle": {"zh": "地点 · 年份", "en": "Place · Year"},
  "image": "assets/stockholm.jpg",
  "images": ["assets/stockholm.jpg"],
  "body": {"zh": "你的摄影文字。", "en": "Your words."}
}
```
category 可选 photography、art、books。id 唯一且发布后不要改，否则评论关联会变化。两种语言共享同一评论串。只有中文时可把 en 留空，系统显示中文并提示待翻译。书评正文可用 \n 换行。艺术作品可添加 source 字段记录出处，只使用允许公开展示的图片。无图条目会显示简洁的文字封面。

学术信息在 academic 对象中：role（机构/职位）、bio（简介）、research（双语文本数组）、publications 与 links（title 双语对象 + url 的数组）。例如：
```js
{"title":{"zh":"论文标题","en":"Paper title"},"url":"https://doi.org/你的DOI"}
```
CV PDF 可上传 assets/cv.pdf 后加入 links。尚未提供的个人资料未填；英文姓名 Tingting Zheng 为拼音，可自行修改。

## 评论：尚未启用，不能提交留言
客户端已接入 Waline，需你拥有并配置服务和数据库。GitHub 登录本身不足以启用评论。Waline 为开源软件，托管平台免费额度和资格以实际注册页面为准；不要选择付费方案。
1. 按官方 https://waline.js.org/en/guide/get-started/ 部署 Waline（当前指南为 Vercel + Neon 数据库）。相关账号注册、协议和数据库密码由你完成。
2. 按官方指南初始化数据库，设置服务环境变量 COMMENT_AUDIT=true、IPQPS=60、DISABLE_REGION=true、DISABLE_USERAGENT=true，SECURE_DOMAINS 加入网站与评论服务地址。不要设置 LOGIN=force。
3. 环境变量调整后重新部署。立刻进入服务 /ui 注册站主账号并确认管理员身份，不要在公开启用评论后才创建管理员。
4. 在 content.js 把 walineServer 从空字符串改为 HTTPS 服务地址。不要把数据库密码或密钥写入公开仓库。
5. 用无痕窗口填写昵称与测试留言：确认提交后未公开；进入 /ui 审核通过，再检查中英文页面均可见。再测删除、空昵称、重复提交和失败提示。
6. 按官方安全指南配置 Turnstile/反垃圾策略；客户端当前使用 Waline 默认反垃圾能力与服务端频率限制。实际效果必须在部署后检查。
服务器配置：https://waline.js.org/en/reference/server/env.html
客户端配置：https://waline.js.org/reference/client/props.html

## 已知边界
作品与学术经历尚未提供，因此首页显示真实空状态；浅色画框是设计占位，不是摄影作品。评论服务尚未部署，审核和反垃圾能力未做线上验证。页面不含分析跟踪代码；启用评论后会连接外部服务，按实际服务完善隐私说明。
