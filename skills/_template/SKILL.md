---
name: template-skill
description: 新 Skill 的模板文件。复制本目录后，替换为真实 Skill 的名称、描述和工作流程。
metadata:
  author: your-name
  version: "2026.05.10"
---

## 使用场景

当任务符合这个 Skill 的专门领域时使用。这里应说明触发条件、适用项目类型和典型任务。

## 能力边界

说明这个 Skill 能处理什么，也说明不适合处理什么，避免 Agent 在无关任务中误用。

## 工作流程

1. 先读取本文件，确认 Skill 是否适用。
2. 再读取 `references/` 中与当前任务直接相关的文件。
3. 按参考资料中的规则执行任务。
4. 完成后验证结果，并说明修改范围。

## References

| Topic | Description | Reference |
|-------|-------------|-----------|
| Overview | Skill 的详细说明模板 | [overview](references/overview.md) |
