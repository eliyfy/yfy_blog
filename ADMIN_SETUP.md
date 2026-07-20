# 管理员登录与 Secrets 配置

GitHub Pages 是纯静态站点，浏览器端 JS **无法直接读取** 仓库环境变量。  
正确做法：把账号/密码哈希放进 **GitHub Secrets**，在 Actions 部署时注入到 `index.html`。

## 1. 计算密码哈希（SHA-256）

```bash
python3 -c "import hashlib; print(hashlib.sha256('你的密码'.encode()).hexdigest())"
```

## 2. 添加 Secrets

路径：`Settings → Secrets and variables → Actions → New repository secret`

| Name | 说明 |
|------|------|
| `ADMIN_USER` | 管理员账号 |
| `ADMIN_PASS_HASH` | 密码的 SHA-256 十六进制 |
| `BLOG_GH_TOKEN` | （可选）repo 写权限 PAT，登录后自动用于云端同步 |

## 3. 开启 Pages（Actions）

`Settings → Pages → Source` 选 **GitHub Actions**。

## 4. 未配置 Secrets 时的兜底

- 账号：`admin`
- 密码：`admin123`

请尽快改成你自己的。
