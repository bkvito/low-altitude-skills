# create-product-group

  用于快速创建各种产品组（色斑图/风场），生成符合`SceneProps`规范的配置代码。

## 功能特性

- 交互式参数收集：通过问答方式收集产品组参数
- 支持色斑图（COLOR_MAP）和风场（WIND）产品
- 支持实况和预报产品类型
- 自动生成Scene/src/data.ts配置代码
- 自动注册到listData

## 安装使用

### 方式一：Git克隆

  ```bash
  cd your-project/skills/
  git clone https://github.com/your-username/create-product-group.git
  ```

### 方式二：手动安装

  1. 下载skill目录
  2. 复制到项目的skills/目录下
  3. 重启Claude Code

  使用方法

  在Claude Code中触发关键词：

- "创建产品组"
- "新建产品组"
- "新建回波产品组"
- "新建风场产品组"

  配置说明

  详细配置说明见SKILL.md
