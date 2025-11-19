# Url-Shorten-Worker
基于 Cloudflare Worker 的短链接服务

## ✨ 新功能

- 🔒 **验证码防护**：集成 [CAP Worker](https://captcha.gurl.eu.org) 进行人机验证与滥用防护
- 可配置在“创建短链”和“访问短链”阶段启用验证码
- 当验证码服务异常时支持降级策略，保证高可用
- 安全性与可用性兼顾的优雅回退机制

📚 文档： [CAPTCHA 英文](docs/CAPTCHA.md) | [CAPTCHA 中文](docs/CAPTCHA_zh-hans.md)

## API 文档

- [API 英文文档](docs/API.md)
- [API 中文文档](docs/API_zh-hans.md)

## 快速开始

### 1. 创建 Workers KV 命名空间

前往 Cloudflare Workers KV 创建命名空间。

![](docs/kv_create_namespace.png)

### 2. 绑定 KV 命名空间

在 Worker 设置中绑定一个 KV 命名空间实例，以便在代码中访问其数据。

![](docs/worker_settings.jpg)

### 3. 配置绑定

变量名填写为 `LINKS`，KV 命名空间选择你在第一步创建的命名空间。

![](docs/worker_kv_binding.png)

### 4. 部署代码

将本项目中的 `index.js` 复制到 Cloudflare Worker 中并保存。

### 5. 配置验证码（可选）

在 `index.js` 中修改 `captcha` 配置，例如：

```javascript
captcha: {
  enabled: true,              // 是否启用验证码
  require_on_create: true,    // 创建短链接时需要验证码
  require_on_access: false,   // 访问短链接时需要验证码
  fallback_on_error: true,    // 验证码服务异常时允许降级放行
}
```

默认行为：创建短链接需要验证码，访问短链接不需要验证码。

更多验证码配置说明参见：
- [CAPTCHA 英文文档](docs/CAPTCHA.md)
- [CAPTCHA 中文文档](docs/CAPTCHA_zh-hans.md)

### 6. 保存并部署

点击 Save and Deploy 完成部署。

## 演示站点

https://lnks.eu.org/

说明：由于滥用情况，演示站点生成的短链接将自动在 24 小时后失效。如需长期使用请自行部署。

## 修改版（crazypeace）

https://github.com/xyTom/Url-Shorten-Worker/tree/crazypeace

支持功能：
1. 自定义短链
2. 页面缓存设置过的短链
3. 长链接文本框预搜索 localStorage
4. 增加删除某条短链的按钮
5. 密码保护

## 项目结构

```
Url-Shorten-Worker/
├─ index.js                 # Cloudflare Worker 主入口脚本
├─ README.md                # 项目说明（中文）
├─ LICENSE                  # 许可证
└─ docs/                    # 文档与配图
   ├─ API.md               # API 英文文档
   ├─ API_zh-hans.md      # API 中文文档
   ├─ CAPTCHA.md          # CAPTCHA 英文文档
   ├─ CAPTCHA_zh-hans.md  # CAPTCHA 中文文档
   ├─ kv_create_namespace.png
   ├─ worker_kv_binding.png
   └─ worker_settings.jpg
```

## 许可证

本项目遵循开源许可证，详见 `LICENSE` 文件。
