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

### weekly-report-ppt

**场景**：根据工作记录自动提炼并生成结构精美、节奏合理的周报 PPT 大纲。

- **编辑风 (warm-editorial)**：视觉精髓为暖奶油底、墨黑文字与极克制的珊瑚强调色。Regular 字重的衬线页标题与无衬线正文的双轨混排。
- **节奏交替 (surface-rhythm)**：页面在“奶油画布、内容卡片、深色表面”三种模式间交替过渡。若 PPT 总页数超 5 页，必须在中间插入过渡节奏页，且尾页使用深色表面收尾。
- **代码考古 (git-archaeology)**：当用户输入记录过于简短时，可获得授权后扫描最近 7 天的个人 Git 提交记录及本周代码变动，智能挖掘并扩写技术细节。

## 安装

### 方式一：通过 `npx skills` 安装（OpenCode / Codex / Cursor 等）

> 注意：旧版 `npx skills`（≤0.1.0）只识别仓库根目录的 `SKILL.md`，无法扫描 `skills/<name>/SKILL.md` 结构，会报 “No SKILL.md found”。请使用最新版：

```bash
# 列出仓库里的所有 skill
npx skills@latest add https://github.com/Aohan-Zhang/aohan-skills --list

# 安装全部 skill
npx skills@latest add https://github.com/Aohan-Zhang/aohan-skills --skill '*' -y

# 或安装单个 skill
npx skills@latest add https://github.com/Aohan-Zhang/aohan-skills --skill whole-codebase-search
npx skills@latest add https://github.com/Aohan-Zhang/aohan-skills --skill ral-review
```

可用 `-a <agent>` 指定目标 agent，例如：

```bash
npx skills@latest add https://github.com/Aohan-Zhang/aohan-skills --skill '*' -a opencode -y
```

### 方式二：通过 Claude Code Plugin / Marketplace 安装

仓库已包含 `.claude-plugin/plugin.json` 与 `marketplace.json`，可直接作为 Claude Code plugin 使用。

```bash
# 添加 marketplace
claude plugin marketplace add Aohan-Zhang/aohan-skills

# 安装插件
claude plugin install aohan-skills@aohan-skills-marketplace
```

或在 Claude Code 交互式会话中：

```
/plugin marketplace add Aohan-Zhang/aohan-skills
/plugin install aohan-skills@aohan-skills-marketplace
```

安装后 skill 会以插件命名空间形式加载，例如 `aohan-skills:whole-codebase-search`。

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

**weekly-report-ppt**

直接提供本周的简要工作记录，或者在输入极简时授权 Agent 扫描 Git 提交记录：

```
这是我本周的简要工作记录：重构了商户端提现状态机，修复了两个bug。帮我做成周报 PPT 大纲。
```

## 项目结构

```
aohan-skills/
├── .claude-plugin/
│   ├── plugin.json          # Claude Code plugin 单插件描述
│   └── marketplace.json     # Claude Code marketplace 目录
├── skills/
│   ├── whole-codebase-search/
│   │   └── SKILL.md
│   ├── ral-review/
│   │   ├── SKILL.md
│   │   └── references/
│   └── weekly-report-ppt/
│       ├── SKILL.md
│       ├── examples/
│       └── references/
├── README.md
└── LICENSE
```

## License

MIT
