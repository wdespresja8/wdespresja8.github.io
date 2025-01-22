上述内容详细介绍了 ChatGPT 的功能以及注册获取 API Key 的方法，接下来我们将重点讲解如何使用 ChatGPT 接口。

## 使用代理服务器的正确姿势

由于国内网络限制，我们无法直接访问 ChatGPT 的接口，因此需要通过代理服务器进行连接。推荐使用 [AWS 亚马逊云](https://bit.ly/bewildcard) 作为代理服务器，原因如下：

- **注册使用方便**：只需提供邮箱并绑定信用卡信息，即可免费试用三个月。
- **稳定不封号**：作为全球最大的服务器供应商，AWS 不存在虚拟代理的情况。相比之下，国内一些小厂商可能会使用虚拟代理手段，导致封号风险。
- **网络延迟低**：AWS 的全球服务器布局使其网络延迟相对较低。

### 排雷提示
不要使用国内大厂的境外服务器（如腾讯云函数的 Node.js 反代），虽然成本低，但封号风险极高。根据经验，使用国内大厂的境外服务器 IP 很可能已被备案，建议避免使用。

## 搭建代理服务器

在获取 AWS 服务器后，接下来需要安装 Nginx 作为代理工具。以下是搭建步骤：

1. **安装 Nginx**  
   安装时需确保编译了 `http_ssl_module` 模块，以支持 HTTPS 代理。

2. **Nginx 配置示例**  
   以下是一个简单的 Nginx 配置文件：

   nginx
   server {
       listen       80; # 端口号，可根据需要修改，记得在安全组中开放对应端口
       server_name  你的服务器IP;
       location / {
           proxy_pass https://api.openai.com;
       }
   }
   

完成配置后，启动 Nginx 即可实现代理。

## ChatGPT 官方接口使用指南

以下是 ChatGPT 的两个常用接口及其使用方法。

### 1. 文字聊天接口

**接口地址**：
bash
curl https://api.openai.com/v1/chat/completions
-H "Content-Type: application/json"
-H "Authorization: Bearer $OPENAI_API_KEY" # 替换为你的 API Key


**参数说明**：

| 参数名       | 值                                                                                     | 必填 | 解释                                                                                     |
|--------------|----------------------------------------------------------------------------------------|------|------------------------------------------------------------------------------------------|
| model        | gpt-3.5-turbo                                                                          | 是   | 数据模型，目前推荐使用 `gpt-3.5-turbo`。                                                |
| messages     | {“role”: “user”, “content”: “Who won the world series in 2020?”} 等                   | 是   | 请求内容，支持上下文聊天格式。                                                          |
| temperature  | 1                                                                                      | 否   | 回答相关度，范围 0-1，默认为 1。                                                        |
| top_p        | 1                                                                                      | 否   | 相关度参数，通常不需要修改，默认值为 1。                                                |
| n            | 1                                                                                      | 否   | 返回回答的数量。                                                                        |
| stream       | false                                                                                  | 否   | 是否开启流式传输，默认关闭。                                                            |
| max_tokens   | chatgpt 支持的最大值                                                                   | 否   | 单次请求返回的最大数据长度，建议设置以避免浪费 Token。                                   |
| 其他         | 更多参数请参考 [官方文档](https://bit.ly/bewildcard)。                                 |      |                                                                                          |

### 2. 图片生成接口

**接口地址**：
bash
curl https://api.openai.com/v1/images/generations
-H "Content-Type: application/json"
-H "Authorization: Bearer $OPENAI_API_KEY" # 替换为你的 API Key


## 总结

以上是 ChatGPT 的两个常用接口的使用方法。如果有任何疑问或建议，欢迎留言指正。

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)

---

> 本作品采用 [《CC 协议》](https://bit.ly/bewildcard)，转载请注明作者和本文链接。