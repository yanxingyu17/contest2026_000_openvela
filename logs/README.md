# logs/ — AI Coding 日志目录

本目录用于存放你在开发过程中与 AI 工具的**对话日志**。比赛要求把使用 AI 辅助开发的过程沉淀到这里，和作品代码一并提交。

> 本目录现在放的是一个**示例**：
> `logs/your-github-login/2026-01-01/claude-code__example.jsonl`
> 请把它替换成你自己导出的真实日志（删掉示例的 `your-github-login/` 目录即可）。

## 一、目录结构规范

```text
logs/
└── <github_login>/            # 你的 GitHub 用户名，一人一目录
    └── <date>/                # 会话日期，格式 YYYY-MM-DD
        └── <tool>__<sid>.jsonl  # 单个会话一个文件
```

- `<github_login>`：你的 GitHub 用户名（多人协作时各自一个目录）。
- `<date>`：会话发生的日期，例如 `2026-03-15`。
- `<tool>`：产生该会话的 AI 工具，取值之一：`claude-code` / `opencode` / `codex` / `kiro`。
- `<sid>`：该会话在工具内部的 session id。
- 文件名形如 `claude-code__528e005f-....jsonl`，工具名与 session id 之间用**两个下划线** `__` 连接。

## 二、文件格式（JSONL）

每个 `.jsonl` 文件是一个会话，**每行一个 JSON 对象**（一个事件 event），按 `seq` 从 0 递增。常见字段：

| 字段             | 说明                                                       |
| ---------------- | ---------------------------------------------------------- |
| `schema_version` | 固定为 `"1.0"`                                             |
| `session_id`     | 会话 id                                                    |
| `team_id`        | 队伍仓名，例如 `contest2026_000_openvela`                  |
| `github_login`   | 产生该事件的 GitHub 用户名                                 |
| `tool`           | `claude-code` / `opencode` / `codex` / `kiro`              |
| `seq`            | 会话内序号，从 0 开始逐条 +1                               |
| `ts`             | ISO 8601 UTC 时间戳                                        |
| `role`           | `user` / `assistant` / `tool` / `system`                  |
| `text`           | 文本内容（user / assistant / system 事件）                 |
| `tool_name`      | 工具调用名（`role=tool` 时），如 `read` / `edit` / `bash`  |
| `model`          | 使用的模型名（可选）                                       |
| `tokens_in/out`  | token 计数（可选）                                         |
| `files_touched`  | 本次事件读写的文件列表（可选）                             |

完整字段定义见日志归集工具内的 `schema/event.schema.json`。

## 三、如何生成

这些 JSONL 由组委会提供的「AI Coding 日志归集工具」从你的 AI 工具会话中导出，**只提交 JSONL 文件本身**（评委侧可在本地渲染成可读视图）。导出与提交的完整步骤见：

[《AI Coding 日志归集与提交手册》](https://github.com/open-vela/docs/blob/dev-ai-contest-2026/zh-cn/contest_2026/ai_coding_log_guide.md)
