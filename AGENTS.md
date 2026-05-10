# 仓库协作规则

## 项目定位

本仓库用于维护自定义 Codex Skills。核心产物位于 `skills/` 目录，每个 Skill 都必须有独立目录和入口文件。

## 目录规范

每个正式 Skill 必须遵循以下结构：

```text
skills/{skill-name}/
├── SKILL.md
└── references/
```

`skills/_template/` 是模板目录，只用于复制创建新 Skill，不应作为正式 Skill 对外使用。

## SKILL.md 规范

`SKILL.md` 必须包含 frontmatter：

```md
---
name: skill-name
description: 简短说明这个 Skill 的使用场景和能力边界。
metadata:
  author: your-name
  version: "YYYY.MM.DD"
---
```

正文应包含：

- 使用场景
- 能力边界
- 工作流程
- 参考资料链接

## references 规范

`references/` 用于保存详细资料。建议一个主题一个文件，避免入口文件过长。

参考文档应优先描述规则、取舍和示例，不应堆放无关内容。

## 文档留存规范

涉及方案、优化、实施、思路或总结时，文档文件名必须使用：

```text
YYYY-MM-DDTHH-mm-ss-主题-文档类型.md
```

同一任务产生的主要文档、思路文档和总结文档应放在同一目录。

## 编码和注释规范

如果后续 Skill 中包含脚本或示例代码，数学计算、坐标、向量、投影、光照、位运算、非直观算法和 Shader 相关逻辑必须使用中文注释。

注释必须解释思路、变量意义和为什么这么算，禁止只写无意义描述。

## 验证要求

修改后必须做闭环验证，至少确认：

- 新增文件存在。
- Markdown 链接路径合理。
- 目录结构符合约定。

## Git 要求

每次编码或文档结构调整结束后，应执行：

```bash
git add <modified_files>
```

如果 Git 操作失败，必须在最终说明中明确原因。
