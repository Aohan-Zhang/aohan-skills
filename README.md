# aohan-skills

个人 AI coding agent skill 集合，按领域分类。支持 Claude Code、OpenCode。

## Skills

### coding

| Skill | 说明 |
|---|---|
| `whole-codebase-search` | 全仓库代码搜索与探索，多维度扫描避免遗漏 |

### workflow

| Skill | 说明 |
|---|---|
| `ral-review` | 设计文档审查 (Review → Attack → Refine)，输出 Agent Ready 级别的文档 |

## 安装

```bash
npx skills add https://github.com/aohan/aohan-skills/plugins/coding
npx skills add https://github.com/aohan/aohan-skills/plugins/workflow
```

**Claude Code 插件方式**

```bash
/plugin marketplace add aohan/aohan-skills
/plugin install coding@aohan-skills
/plugin install workflow@aohan-skills
```

## License

MIT
