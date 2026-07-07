# 对话持久化 — 会话状态协议

> **用途**：允许用户跨会话继续之前的对话，避免每次从零开始。

---

## 会话状态文件

路径：`.omo/sessions/mao-qa-session.json`

## 数据结构

```json
{
  "session_id": "ses_<随机8位>",
  "created_at": "2026-07-03T10:30:00+08:00",
  "updated_at": "2026-07-03T12:15:00+08:00",
  "user_problem": "用户最初描述的问题摘要",
  "stage": "追问阶段|原理映射阶段|行动指引阶段|总结阶段",
  "last_principle": "最后引用的原理编号，如 2.4",
  "last_question": "最后问用户的问题",
  "insights": ["用户已产出的关键洞察1", "关键洞察2"],
  "depth": 2,
  "category": "B"
}
```

## 行为规则

### AI 启动时

1. 检查 `.omo/sessions/mao-qa-session.json` 是否存在
2. 若存在，读取 `user_problem` + `last_question`
3. 向用户发出提示：

> "我看到你上次在聊关于 [problem] 的问题，上次问到了 [question]。要接着聊，还是聊新问题？"

### 对话结束时

1. 将当前状态写入 `.omo/sessions/mao-qa-session.json`
2. 覆盖旧文件（只保留最近一次 session）
3. 字段更新规则：
   - `updated_at` → 当前时间
   - `stage` → 判断当前进度
   - `last_principle` → 最后讨论的原理编号
   - `last_question` → 最后一句追问（如果已经结束，则为 null）
   - `insights` → 追加本次新洞察（最多保留 5 条，先进先出）
   - `depth` → 追问轮数
