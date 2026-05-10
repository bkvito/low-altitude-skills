# My Skills

这是一个用于集中维护自定义 Codex Skills 的合集仓库。

## 目录结构

```text
low-altitude-skills/
├── README.md
├── AGENTS.md
├── LICENSE.md
└── skills/
    └── _template/
        ├── SKILL.md
        └── references/
            └── overview.md
```

## Skill 约定

每个 Skill 使用独立目录：

```text
skills/{skill-name}/
├── SKILL.md
└── references/
    └── overview.md
```

`SKILL.md` 是入口文件，用于描述 Skill 的名称、触发场景、能力边界和参考资料。

`references/` 用于保存详细规则、示例、背景说明和扩展资料。建议按主题拆分，不要把所有内容都堆在 `SKILL.md` 中。

## 新增 Skill 流程

1. 复制 `skills/_template/`。
2. 将目录名改为目标 Skill 名称。
3. 修改 `SKILL.md` 的 frontmatter、使用场景和参考链接。
4. 在 `references/` 中补充详细说明。
5. 更新本 README 的 Skill 列表。

## Skill 列表

| Skill | Description |
|-------|-------------|
| `_template` | 新 Skill 的目录和文档模板，不作为正式 Skill 使用。 |

## 维护建议

先以手写维护为主。等 Skill 数量变多，或者需要从外部项目文档同步时，再逐步增加 `scripts/`、`sources/`、`vendor/`、`instructions/` 和 `meta.ts`。
