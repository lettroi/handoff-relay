# 推送到 GitHub（换电脑后照做）

本项目已初始化 git、完成一次 commit、remote 指向 `https://github.com/lettroi/handoff-relay.git`，分支为 `main`。在你的电脑上只需以下步骤：

## 1. 先在 GitHub 网页创建空仓库

登录 GitHub → 右上角 `+` → `New repository`：
- Repository name 填 `handoff-relay`
- Owner 选 `lettroi`
- **不要**勾选 Initialize with README / .gitignore / license（保持完全空仓库，否则推送会冲突）
- 点 Create repository

> 如果仓库名或 owner 与上面不同，改一下第 2 步的 URL 即可。

## 2. 推送

在本目录打开终端，执行：

```bash
git push -u origin main
```

会弹出 GitHub 登录（浏览器或凭据窗口），登录成功后即完成。

若没有弹出登录，可改用 Personal Access Token（Settings → Developer settings → Personal access tokens，勾选 `repo` 权限），当密码输入：

```bash
git remote set-url origin https://<你的用户名>:<TOKEN>@github.com/lettroi/handoff-relay.git
git push -u origin main
```

## 3. 验证

打开 `https://github.com/lettroi/handoff-relay`，应能看到 README 和全部文件。

---

## 附：本地常用命令

```bash
git status                 # 查看状态
git add -A                 # 暂存全部改动
git commit -m "说明"       # 提交
git push                   # 推送
```
