# aohan-skills 仓库设计

- 日期:2026-06-19
- 状态:已确认,脚手架已落地

## 目标

- 创建一批 Claude Code skill 供自己使用,并发布到 GitHub。
- 一份目录结构同时满足两种用法:**本地软链自用** + **作为插件市场一键安装**。
- 目录分类清晰、浅显易懂(按领域分,如编码、工程效率)。

## 关键决策:分类即插件

仓库 = 一个 marketplace,内含若干 plugin。**一个分类 = 一个 plugin**,plugin 下 `skills/<名字>/SKILL.md` 自动发现。

考虑过的三种方案:

| 方案 | 说明 | 取舍 |
|---|---|---|
| **A. 分类即插件 ✅** | 一个分类 = 一个插件,打包该类所有 skill | 目录最直观、marketplace 条目少、自用软链少(每类一条);代价是别人只能整类装 |
| B. 每个 skill 一个插件 | 每个 skill 独立,用 category 字段分类 | 安装粒度最细;但目录扁平、分类不直观 |
| C. 混合 | 目录按分类分组,每个 skill 仍独立插件 | 最灵活;但每个 skill 要一份 plugin.json、软链最繁琐 |

**选 A 的理由**:个人自用为主,软链越少越好;目录分类最直观;唯一代价(无法只装单 skill)对个人仓库影响小。

## 结构、自用与分发、命名约定

详见 [`README.md`](../README.md)。

## 复用官方 category 词表

`marketplace.json` 的 `category` 字段复用官方词表(`development` / `productivity` / ...),保证 `/plugin` 界面分类对齐。

## 硬约束

- 顶层**不得**散放 `SKILL.md`,必须放进 `skills/<名字>/`。
- 每个分类插件目录内必须有 `.claude-plugin/plugin.json`,其 `name` 与目录名、marketplace 条目名三者一致。
- skill 名 / 目录名 / marketplace 名必须是 kebab-case(小写字母、数字、连字符)。

## YAGNI(刻意不加)

- `commands/` / `agents/` / `hooks/` 目录——等真有需要再加。
- 每个 skill 一份 `plugin.json`——已选「分类即插件」。
- 脚手架脚本(`scripts/new-skill.sh`)——先手动加,等觉得烦再补。
- 多语言 README。

## 参考规范

- 创建 marketplace:https://code.claude.com/docs/en/plugin-marketplaces
- 创建 plugin:https://code.claude.com/docs/en/plugins
- 技术规范:https://code.claude.com/docs/en/plugins-reference
