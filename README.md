# 艺航卫浴官网 · 源码镜像

泉州宝宏厨卫有限公司 · 艺航卫浴 &nbsp;|&nbsp; 官网 https://www.yihangweiyu.com &nbsp;|&nbsp; 闽ICP备2026047144号

| 文件 | 说明 |
|------|------|
| 404.html | 品牌 404 页 |
| sitemap.xml | 站点地图（指向 www.yihangweiyu.com） |
| obots.txt | 爬虫策略 |
| set-domain.ps1 | 一键写入域名 / canonical / og / sitemap / robots / ICP 备案号 |
| 部署说明.md | 上线三步指南 + Nginx 配置 + 自检清单 |

## 为什么 index.html 和 images/ 不在本仓库

GitHub MCP Connector 的写入接口以 **UTF-8 文本**传输内容（由服务端自行 base64 后调用 REST API），
因此：

1. images/ 下 171 张 JPG/PNG 会被存成 base64 **文本**，字节损坏 → 线上全部裂图；
2. index.html（2.7 MB，内嵌 9 张证书 base64）超过 Connector 单次请求载荷上限 → 推送被拒。

已实测确认：同一张 avicon-64.png 传入其 base64 后，GitHub 存储的 blob SHA
（781ae484…）等于 base64 文本的 SHA，而非原图的 SHA（2145e093…），二进制不可保真。

**结论：静态整站不适合通过该接口托管到 GitHub Pages。**

## 正确的部署方式

- **正式站点**：整站包上传到阿里云服务器（宝塔面板），域名 A 记录指向服务器 IP，开启 HTTPS。
  详见本仓库 部署说明.md。
- **源码版本管理**：用本机 git 直接 clone 本仓库后 push 完整站点（含 images/），
  绕过 Connector 的文本与载荷限制。

## 一键写域名（幂等，可重复执行）

```powershell
powershell -ExecutionPolicy Bypass -File set-domain.ps1 -Domain www.yihangweiyu.com -Icp "闽ICP备2026047144号"
```