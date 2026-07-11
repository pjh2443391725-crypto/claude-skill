---
name: video-pipeline
description: Use when the user wants to produce an AI-generated video — script rewriting, storyboard creation, AI image generation via DashScope, and CapCut import. Triggers include: "做视频", "生成视频", "文生图视频", "AI视频", "继续视频项目", "分镜表", "批量生图".
---

# Video Pipeline — AI 视频制作工作流

## 概述

端到端 AI 视频制作流水线：**文案 → 分镜表 → 批量文生图 → 导入剪映**。每个环节由 Claude Code 直接操作，无需手动切换工具。

## 触发词

"做视频" / "AI视频" / "批量生图" / "分镜表" / "继续XXX视频项目" / "文生图"

## 流水线步骤

### 第1步：文案准备
- 用户提供主题文案（txt/docx），或由 Claude Code 直接洗稿
- 输出：一段完整的视频旁白文案（中文）
- 如果用户已提供文案文件，直接读取（docx 用 python zipfile+xml 解析）

### 第2步：角色与风格设定
- 定义角色外观锚定词（年龄、体型、五官、服装、气质）
- 定义画面风格（大眼风格/块面平涂/角色背景分离等）
- 所有锚定词保存为英文，供文生图 prompt 拼接使用
- 关键变量：`PROTAGONIST_LOOK`、`STYLE_SUFFIX` 等

### 第3步：分镜表
- 把旁白文案拆成 6-12 个镜头
- 每个镜头包含：镜头编号、镜头名、对应旁白、英文 prompt、时长
- 英文 prompt = 角色外观 + 场景动作描述 + 风格锚定词
- 保存在 `iwo_jima_storyboard.py`，`SHOTS` 列表结构

### 第4步：批量文生图
- **API**: 阿里云百炼 DashScope `wan2.6-t2i` 同步模式
- **接口**: `POST https://dashscope.aliyuncs.com/api/v1/services/aigc/multimodal-generation/generation`
- **返回**: JSON 中 `output.choices[].message.content[].image` 是 OSS URL，需下载
- **参数**: `size="1664*928"` (16:9), `prompt_extend=True`, `watermark=False`
- **注意**:
  - API 返回的是 **URL 不是 base64**，不要尝试 base64 decode
  - 内容审核会拦截敏感词（`Green net check failed`），需修改 prompt 避开
  - 每张图间隔 5 秒冷却，单图超时 180 秒
  - prompt 全部用英文，AI 生图英文效果更好

### 第5步：导入剪映
- 全部图片在 `iwo_jima_output/` 目录，PNG 格式
- 用户手动拖入剪映轨道，按旁白时长对齐
- 对照表 `分镜对照表.txt` 记录每个镜头对应关系和时长

## API 配置模板

```python
API_KEY = "sk-ws-H.EMXMLHM.QQoC..."  # 用户提供，不硬编码
BASE_URL = "https://dashscope.aliyuncs.com"
MODEL = "wan2.6-t2i"  # 同步模式，一次请求直接出图
```

## 关键文件结构

```
项目目录/
├── 主题文案.docx              # 旁白文案
├── 视频风格人物锚定词.txt      # 角色/风格定义
├── iwo_jima_storyboard.py     # 分镜表 + SHOTS 数据
├── iwo_jima_generate.py       # 批量生图脚本
└── iwo_jima_output/           # 生成的图片
    ├── shot_01_*.png
    ├── shot_02_*.png
    ├── ...
    └── 分镜对照表.txt
```

## Must-Call Skills

| 步骤 | Skill | 原因 |
|------|-------|------|
| 生图脚本编写后 | `code-review` | 检查 API 解析逻辑、错误处理、资源泄漏 |

## Common Mistakes

| 错误 | 修复 |
|------|------|
| 把 API 返回的 image URL 当 base64 解码 | API 返回 URL（`https://dashscope-*.oss-accelerate.aliyuncs.com/...`），用 `requests.get()` 下载 |
| prompt 含敏感词被拦截 | "Rising Sun flag"→"flag"，"天皇"→去掉，"grotesque fangs"→"mechanical gears" |
| 图片只有 80 字节 | 解析逻辑错误导致，检查 image 字段是 URL 还是 base64 |
| docx 二进制读不了 | 用 `python -c "import zipfile; ..."` 直接解析 XML |
| 编码乱码 | 始终 `sys.stdout = io.TextIOWrapper(sys.stdout.buffer, encoding='utf-8')` |

## 移植到另一台电脑

1. **复制 skill 文件**：把 `~/.claude/skills/video-pipeline/SKILL.md` 拷到另一台电脑同样路径
2. **安装 Python 依赖**：`pip install requests`（只有这一个依赖）
3. **配置 API Key**：在新电脑上告诉 Claude Code 你的百炼 API Key（skill 不存储密钥）
4. **启动项目**：新电脑上说"用 video-pipeline 做视频，主题是XXX"
5. **迭代优化**：改 `SKILL.md`，两台电脑同步即可

## Example

User: "继续绝命硫磺岛项目"

→ 读取记忆 `[[video-pipeline-iwo-jima]]` 确认进度 → 读 docx 提取文案 → 设计分镜 → 写生图脚本 → 调用百炼 API 批量生图 → 输出对照表 → 更新记忆
