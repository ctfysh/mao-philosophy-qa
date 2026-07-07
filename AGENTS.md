> [!DEV-ONLY]
> # AGENTS.md — 项目入口/开发参考
> **本文件仅供开发参考，AI 运行时不需要加载。**
> 当运行 `/mao-qa` 时，请直接载入 `skills/mao-philosophy-qa/SKILL.md`。

# mao-philosophy-qa

毛选哲学问对 — 用毛泽东哲学方法论分析人生困惑的 Socratic coach Skill。

## STRUCTURE

```
.
├── README.md                                             # 用户使用指南 (124行)
├── docs/superpowers/
│   ├── specs/2026-07-03-mao-philosophy-qa-design.md      # 完整设计文档 (910行)
│   └── plans/2026-07-03-phase4-implementation.md         # Phase 4 实施计划
├── skills/mao-philosophy-qa/
│   ├── SKILL.md                                           # AI 指令入口 (124行)
│   ├── references/
│   │   ├── philosophical-pillars.md                       # 53条原理 + 原文锚定 (468行)
│   │   ├── questioning-protocol.md                        # 5层追问协议 (135行)
│   │   ├── mapping-table.md                               # 场景↔原理↔原文映射 (266行)
│   │   ├── article-index.md                               # 32篇文章索引 (101行)
│   │   └── anti-patterns.md                               # AI 反模式自查 (112行)
│   ├── seeds/                                             # 9类112个种子问题
│   │   ├── 01-epistemology.md                             # A: 认知与学习 (12问)
│   │   ├── 02-dilemmas-and-choices.md                     # B: 困境与选择 (15问)
│   │   ├── 03-hardship-and-setbacks.md                    # C: 困难与挫折 (13问)
│   │   ├── 04-work-and-methodology.md                     # D: 工作与方法论 (13问)
│   │   ├── 05-interpersonal-relations.md                  # E: 人际关系 (13问)
│   │   ├── 06-self-growth.md                              # F: 自我成长 (13问)
│   │   ├── 07-character-cultivation.md                    # G: 个人品格修养 (10问)
│   │   ├── 08-conflict-resolution.md                      # H: 冲突解决 (11问)
│   │   └── 09-public-private-and-perspective.md           # I: 公私关系与视野 (12问)
│   ├── protocols/
│   │   ├── dialogue-examples.md                           # 5个完整对话案例 (1055行)
│   │   └── session-state.md                               # 跨会话状态保持协议
│   ├── tests/
│   │   ├── test-mapping-engine.md                         # 20个扩展测试场景
│   │   └── test-boundary-cases.md                         # 5个边界情况测试
│   └── coverage/
│       └── audit-report.md                                # 覆盖度审计报告 (249行)
└── AGENTS.md                                              # 本文件
```

## WHERE TO LOOK

| 目标 | 位置 |
|------|------|
| 用户使用说明 | `README.md` |
| Skill 入口 + 核心指令 | `skills/mao-philosophy-qa/SKILL.md` |
| 设计文档 | `docs/superpowers/specs/2026-07-03-mao-philosophy-qa-design.md` |
| 53 条哲学原理 | `skills/mao-philosophy-qa/references/philosophical-pillars.md` |
| 场景↔原理映射 | `skills/mao-philosophy-qa/references/mapping-table.md` |
| 种子问题（112 问） | `skills/mao-philosophy-qa/references/seeds-compact.md` |
| 对话案例 | `skills/mao-philosophy-qa/protocols/dialogue-examples.md` |
| 反模式自查 | `skills/mao-philosophy-qa/references/anti-patterns.md` |
| 测试用例 | `skills/mao-philosophy-qa/tests/` |
| 实施计划 | `docs/superpowers/plans/2026-07-03-phase4-implementation.md` |

## COMMANDS

| 命令 | 说明 |
|------|------|
| `/mao-qa` | 主命令，启动持续追问模式 |
| 自动触发 | 检测"矛盾""实践""实事求是""调查""辩证法""主观""客观""主要矛盾""方法论"等关键词时自动推荐 |

## CONVENTIONS

- **SKILL.md** 为 AI 指令入口，定义了核心身份（Socratic coach）、响应协议（5步处理管线）、追问协议（5层深度递进）
- **README.md** 为终端用户使用指南，说明如何触发、对话示例、9类场景表
- **seeds-compact.md** 取代了原有 9 个种子文件（已被删除）
- **所有原理引用必须锚定毛泽东原文线号**（格式：`《实践论》L3044`）
- **每个回答必须以追问结尾**，遵循承→转→问结构
- **默认每轮只引用一条原理**，避免信息过载
- 文件名全部英文小写+连字符
- `docs/superpowers/` 存放设计规格和实施计划
- `skills/mao-philosophy-qa/` 为 skill 主体

## NOTES

- 所引原理仅提取哲学方法论核心（认识论/辩证法/方法论/人生观），不涉及政治立场
- 53 条哲学原理全部锚定原文线号，可追溯验证
- 112 个种子问题覆盖 9 大人生场景类别
- 自由映射引擎支持种子库之外的任意问题
