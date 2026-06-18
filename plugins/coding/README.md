# coding

编码开发辅助类 skill。本目录是一个 Claude Code 插件(plugin),其下 `skills/<名字>/SKILL.md` 会被自动发现。

## 包含的 skill

(陆续添加中)

## 新增 skill

```bash
mkdir -p skills/<skill名>        # skill 名用 kebab-case 英文,如 code-review
# 编辑 skills/<skill名>/SKILL.md
```

`SKILL.md` 必填 `name`(与目录名一致)和 `description`(触发条件,告诉 Claude 何时用)。
