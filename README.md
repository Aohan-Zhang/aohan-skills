# aohan-skills

个人 AI coding agent skill 集合。支持 Claude Code、OpenCode、Codex 等。

## Skills

### whole-codebase-search

**场景**：代码搜索不够用的时候。

默认的代码搜索往往停在第一个匹配，或者只读一个文件就下结论。这个 skill 强制进行全仓库多维度扫描：

- **调用者** — 谁在用这个函数/接口？
- **被调用者** — 这个函数依赖什么？
- **同级模块** — 同层还有哪些相关代码？
- **关联功能** — 哪些功能共享同一份数据或流程？
- **数据流** — 数据从哪来、存哪、怎么变？
- **架构边界** — 哪个层负责，什么跨层了？

适用于：追踪功能实现、理解模块关系、重构前摸底、排查问题根源。

### ral-review

**场景**：写了 spec，但不确定质量，想来一次超级审核。

RAL = Review → Attack → Refine，多轮迭代审查：

1. **Review** — 4 个 Agent（架构师、资深工程师、QA、魔鬼代言人）并行审查
2. **Attack** — 挑战假设、找漏洞、评风险
3. **Refine** — 修复问题、更新文档，进入下一轮

最多 5 轮，直到没有新的 Medium+ 问题。最终输出成熟度评分（0-100），≥80 分且无 Critical/High 问题即为 "Agent Ready"。

适用于：PRD 审核、架构文档审查、API 设计评审、任何需要高质量 spec 的场合。

## 安装

```bash
npx skills add Aohan-Zhang/aohan-skills --skill whole-codebase-search
npx skills add Aohan-Zhang/aohan-skills --skill ral-review
```

## 使用

**whole-codebase-search**

直接描述你要找的内容，agent 会自动全仓库扫描：

```
帮我找出所有处理用户认证的代码
这个 UserService 被哪些地方调用了？
追踪一下订单状态的完整数据流
```

**ral-review**

```bash
/ral-review <文档路径> [模式]
```

| 模式 | 说明 |
|------|------|
| `auto`（默认） | 跑完全部轮次，自动修复问题，输出评分 |
| `dry` | 只审查不修改，输出问题列表 |
| `quick` | 只跑第 1 轮（需求完整性），快速检查 |

示例：

```bash
/ral-review docs/specs/payment-system.md
/ral-review docs/specs/payment-system.md dry
/ral-review docs/specs/payment-system.md quick
```

## 项目结构

```
aohan-skills/
├── skills/
│   ├── whole-codebase-search/
│   │   └── SKILL.md
│   └── ral-review/
│       ├── SKILL.md
│       └── references/
├── README.md
└── LICENSE
```

## License

MIT
