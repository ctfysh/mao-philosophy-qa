# Phase 4: 优化与扩展 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use subagent-driven-development (recommended) or executing-plans to implement this plan task-by-task.

**Goal:** 为 mao-philosophy-qa Skill 添加反模式防御、对话持久化和扩展测试

**Architecture:** 三个独立模块，互不依赖，可并行实施。每个模块 +1-2 文件，SKILL.md 追加引用。

**Tech Stack:** Markdown 文档

## Global Constraints

- 所有文件名英文小写+连字符
- 文件结构遵循现有 conventions（references/、protocols/、tests/）
- SKILL.md 修改仅追加引用行和 session 行为指令，不改动现有逻辑
- L 引用必须锚定原文实际存在的内容行

---

### Task 1: 反模式模块 — references/anti-patterns.md

**Files:**
- Create: `references/anti-patterns.md`
- Modify: `SKILL.md`（追加反模式引用行）

**Interfaces:**
- Consumes: 无
- Produces: `references/anti-patterns.md` — 被 SKILL.md 引用表引用

- [ ] **Step 1: 创建 anti-patterns.md**

内容结构：
- 4 个反模式（AP1-AP4），每个含：表现、危害、自查清单、修正示例
- 格式与 philosophical-pillars.md 的条目风格一致（### 标题 + 定义 + 实践指引）

- [ ] **Step 2: 修改 SKILL.md**

在引用表的 `references/article-index.md` 行之后追加一行：
`references/anti-patterns.md` | AI 常见反模式自查：过早建议/替用户结论/原理堆砌/跳过共情

---

### Task 2: 对话持久化 — protocols/session-state.md

**Files:**
- Create: `protocols/session-state.md`
- Modify: `SKILL.md`（追加 session 行为指令）

- [ ] **Step 1: 创建 session-state.md**

内容：
- session 状态 JSON schema 定义
- 两条新增行为指令：
  1. 对话结束时，将当前状态写入 `.omo/sessions/mao-qa-session.json`
  2. 对话开始时，检查是否存在 session 文件，询问用户是否继续
- 状态字段：session_id, user_problem, stage, last_principle, last_question, insights[]

- [ ] **Step 2: 修改 SKILL.md**

在 SKILL.md 的"运行规则"部分追加两条 session 行为指令

---

### Task 3: 扩展测试 — tests/

**Files:**
- Create: `tests/test-mapping-engine.md`
- Create: `tests/test-boundary-cases.md`

- [ ] **Step 1: 创建 test-mapping-engine.md**

预设 20 个新场景，覆盖 9 个类别中当前测试盲区：
- 每个场景包含：场景描述、预期映射原理、预期追问方向
- 格式：表格 + 验证 checklist

- [ ] **Step 2: 创建 test-boundary-cases.md**

5 个边界场景：
1. 用户拒绝回答追问（"不知道"）
2. 用户情绪化输入（愤怒、沮丧）
3. 用户一次性描述多个问题
4. 用户要求直接给答案
5. 用户完全沉默/简短回复
- 每个场景含：输入示例、预期 AI 响应策略、成功标准
