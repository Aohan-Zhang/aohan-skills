# aohan-skills

aohan 的个人 Claude Code skill 集合。按领域分类组织——既能**软链到本地自用**,也能作为**插件市场**让别人一键安装。

## 目录结构

```
aohan-skills/
├── .claude-plugin/
│   └── marketplace.json          # 插件市场清单(分发入口)
├── plugins/
│   ├── coding/                   # 分类插件:编码开发
│   │   ├── .claude-plugin/plugin.json
│   │   └── skills/<skill名>/SKILL.md
│   └── workflow/                 # 分类插件:工程效率
│       ├── .claude-plugin/plugin.json
│       └── skills/<skill名>/SKILL.md
├── docs/
└── README.md
```

**一个分类 = 一个插件(plugin)**,插件下 `skills/<名字>/SKILL.md` 会被 Claude Code 自动发现。顶层不会散放 `SKILL.md`。

## 使用方式

### 方式一:本地自用(软链,推荐用于自己开发)

把每个分类插件软链到个人 skills 目录,之后修改仓库即时生效:

```bash
ln -s "$(pwd)/plugins/coding"   ~/.claude/skills/coding
ln -s "$(pwd)/plugins/workflow" ~/.claude/skills/workflow
```

新会话自动加载,skill 调用名形如 `/coding:<skill名>`。

### 方式二:作为插件市场一键安装(分享给别人)

```text
# 在 Claude Code 里:
/plugin marketplace add aohan/aohan-skills
/plugin install coding@aohan-skills        # 或 workflow@aohan-skills
```

## 新增一个 skill

1. 建目录:`mkdir -p plugins/<分类>/skills/<skill名>`
2. 写 `SKILL.md`:

   ```markdown
   ---
   name: <skill名>                # kebab-case 英文,与目录名一致
   description: |
     <触发条件——告诉 Claude 何时用,这是质量决定性字段>
   ---

   # <标题>

   <正文:工作流程、约束、示例>
   ```

3. 校验:`claude plugin validate . --strict`
4. 提交。

## 约定

| 对象 | 规则 | 例 |
|---|---|---|
| 仓库名 / marketplace 名 | kebab-case | `aohan-skills` |
| 分类(plugin)目录 | kebab-case 英文 | `coding`、`workflow` |
| skill 目录 = frontmatter `name` | kebab-case 英文 | `code-review` |

目录名和 skill 名用英文(kebab-case 是硬要求 + 路径安全);**`description` 与正文用中文完全没问题**。

## 分类

| 分类 | 内容 | 官方 category |
|---|---|---|
| `coding` | 代码评审、重构、TDD、调试等 | `development` |
| `workflow` | git 提交、部署、任务管理等自动化 | `productivity` |

设计决策与更多背景见 [`docs/`](./docs)。

## License

MIT
