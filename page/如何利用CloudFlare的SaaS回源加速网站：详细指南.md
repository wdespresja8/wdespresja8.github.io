## 引言

利用SaaS回源来加速网站的效果吸引了广泛关注。虽然之前没有亲自尝试过，但最近我对这个方法进行了探索，并将在此分享我的经验和详细步骤，希望能对你有所帮助。

## 1. SaaS回源概述

### 1.1 什么是SaaS？

SaaS（Software as a Service，软件即服务）是指在需要进行某项业务时，无需自行编写或部署代码，而是使用现成的软件供应商提供的服务。例如，Gmail、百度网盘和Netflix等都是通过互联网提供的SaaS服务。

### 1.2 什么是SaaS回源？

对于使用SaaS服务的用户，出于品牌展示的考虑，可能希望通过自定义的域名来访问这些服务。例如，某公司如果购买了Gmail服务，出于品牌要求希望使用自家域名@xxx.com，而非默认的@gmail.com，这时便可利用SaaS回源技术。

### 1.3 如何利用SaaS回源加速网站？

在处理静态资源（如图片、CSS、JS等）时，Cloudflare的全球分布式节点可以缓存这些内容。当用户请求资源时，访问路径变为：**浏览器 → Cloudflare节点（国内/最近） → 直接返回缓存内容**。相比之下，原始访问路径则是：**浏览器 → 国外源站**。因此，配置了SaaS回源后，无需访问源站，大大提升访问速度。

## 2. 配置概述

在配置SaaS回源前，你需要准备以下内容：

- **必须**：希望加速的域名 `a.com`（无需托管到Cloudflare）
- **必须**：回源域名 `b.com`（需托管到Cloudflare）
- **必须**：国外信用卡，用于绑定Cloudflare，推荐使用 [ACCPAY](https://bit.ly/bewildcard)。
- **非必须**：DNSPod，用于将海外线路和国内线路分开解析。

### 步骤概述：

1. 将 `b.com` 托管到Cloudflare，并解析到你的服务器（如Github Pages）。
2. 配置Cloudflare SaaS回源（此功能免费，但需要绑定信用卡），将 `b.com` 设置为回退源。
3. 在DNSPod上，配置 `a.com` 的DNS，将其指向Cloudflare。

## 3. 详细步骤

### 3.1 注册CloudFlare并托管b.com

首先，注册并登录到CloudFlare，将 `b.com` 添加到你的CloudFlare账户中，并记录Cloudflare分配的NS服务器。

在你的域名注册商处，设置DNS服务器为Cloudflare提供的两个NS域名，设置生效可能需要一些时间。

### 3.2 启用CloudFlare for SaaS

进入SSL设置中的自定义主机名，点击启用CloudFlare SaaS。此时需绑定外国信用卡，没有外国卡可以使用虚拟卡，推荐使用 [ACCPAY](https://bit.ly/bewildcard)。

填写卡片信息完成绑定。

### 3.3 解析回源域名

进入 `b.com` 的管理界面，进入DNS设置，将 `b.com` 的A记录或AAAA记录指向你的实际网站服务器IP。

### 3.4 添加回源

在 `b.com` 的管理界面，选择SSL/TLS设置中的自定义主机名，并添加回源，输入刚刚解析的 `b.com` 地址。

### 3.5 添加自定义主机名

添加回源成功后，继续在同一界面添加你的希望加速的域名 `a.com` 的自定义主机名，并执行相应设置。

随后，需要在DNSPod中为 `a.com` 添加两条记录，用于验证域名所有权。

### 3.6 设置SSL

在CloudFlare中进入 `b.com` 的管理界面，选择SSL/TLS设置，将SSL/TLS加密模式改为“完全”。

## 验证配置效果

通过测速工具（例如itdog测速）验证配置后的访问速度，较之前明显提升。

通过以上步骤，你可以成功配置CloudFlare的SaaS回源，以加速你的网站访问。

👉 [野卡 | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)