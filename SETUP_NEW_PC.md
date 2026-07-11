# 另一台电脑配置指南

## 情况A：云端/另一台电脑也是 Windows（有 Claude Code）

### 第1步：拉取 skill
在另一台电脑的 Claude Code 里说：
> 帮我装git，然后执行：
> git clone https://github.com/MIER/claude-skills.git C:\Users\你的用户名\.claude\skills

（如果你用的是Gitee，把github.com换成gitee.com）

### 第2步：配置权限（不再摁yes）
在另一台电脑的 Claude Code 里说：
> 帮我配置settings.json，让以后所有操作都免确认：defaultMode设为bypassPermissions，skipDangerousModePermissionPrompt设为true，然后把当前工作目录加到additionalDirectories

Claude Code 会自动帮你改好 settings.json。

---

## 情况B：纯云端 Linux 机器

```bash
# 1. 克隆 skill 仓库
git clone https://github.com/MIER/claude-skills.git ~/.claude/skills

# 2. 修改 settings.json 免确认
# 在 ~/.claude/settings.json 中加入：
# "defaultMode": "bypassPermissions",
# "skipDangerousModePermissionPrompt": true
```

---

## 之后每次改完 skill 怎么同步

```
改skill的电脑：          另一台电脑：
git add -A              git pull
git commit -m "xxx"
git push
```

---

## 用 Gitee（码云）代替 GitHub（国内更快）

如果你访问 GitHub 很慢，用 Gitee：
1. 打开 https://gitee.com 注册账号
2. 点击 "+" → "新建仓库"，名称填 `claude-skills`，选择"私有"
3. 创建后复制仓库地址，类似 `https://gitee.com/你的用户名/claude-skills.git`
4. 在本机执行（把地址换成你的）：
   git remote add origin https://gitee.com/你的用户名/claude-skills.git
   git push -u origin master
