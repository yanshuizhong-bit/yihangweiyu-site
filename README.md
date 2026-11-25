# 艺航卫浴官网

泉州宝宏厨卫有限公司 · 艺航卫浴
官网：https://www.yihangweiyu.com

本仓库为官网**源码镜像**（index.html / 404.html / set-domain.ps1 / 部署说明.md）。

> 说明：站点图片资源（images/ 目录，171 张 JPG/PNG）体积约 9.4 MB，

> 通过 GitHub API 推送时二进制会被 base64 文本化而损坏，因此图片不入库。

> 线上完整站点由整站包部署，见 部署说明.md。

## 整站包内容

- index.html — 单页官网（首页/公司简介/资质荣誉/产品中心/品牌动态/联系我们）
- images/ — 90 张产品图 + 65 张缩略图 + 4 张工厂实拍 + 7 张品牌动态 + 9 张证书
- 404.html — 品牌 404 页
- set-domain.ps1 — 一键写入域名配置（canonical / og / sitemap / robots / ICP）
- 部署说明.md — 上线三步指南 + 自检清单

## 一键写域名

```powershell
powershell -ExecutionPolicy Bypass -File set-domain.ps1 -Domain www.yihangweiyu.com
```