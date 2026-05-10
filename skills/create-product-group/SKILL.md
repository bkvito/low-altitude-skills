---
  name: create-product-group
  description: 用于快速创建产品组配置，生成符合 SceneProps 规范的配置代码。
---


# create-product-group

用于快速创建各种产品组（色斑图 / 风场），生成符合 `SceneProps` 规范的配置代码。

## 触发关键词

创建产品组、新建产品组、新建回波产品组、新建风场产品组

## 使用流程

当用户触发本 skill 时，按以下步骤收集信息并生成配置代码：

### 第一步：交互式参数收集

使用 AskUserQuestion 工具向用户询问以下必要信息，采用交互式问答方式：

#### 视图类型推断

- 如果用户请求中包含"色斑图"、"回波"、"COLOR_MAP"等关键词，视图类型为 `COLOR_MAP`
- 如果用户请求中包含"风场"、"风"、"WIND"等关键词，视图类型为 `WIND`
- 如果无法推断，需要询问用户

#### 问答参数

1. **产品组所属模块名称**
   - 选项：实况立方体、预报立方体、多源观测设备、新建模块
   - 描述：选择现有模块或创建新模块

2. **时间维度**
   - 选项：实况（实时观测数据产品）、预报（预报数据产品）

3. **产品组标识（productGroupIdentify）**
   - 选项：ObsCube（实况立方体产品组标识）、FcstCube_0_3（0-3小时预报立方体产品组标识）、自定义
   - 描述：选择现有标识或输入自定义标识

4. **产品组标题（title）**
   - 选项：回波测试（测试用回波产品标题）、实况立方体（实况立方体产品标题）、自定义
   - 描述：选择现有标题或输入自定义标题

5. **placeholderHeight（可选，默认100）**
   - 选项：100（默认）、自定义

**注意**：参数收集时应使用标准的 AskUserQuestion 工具调用格式，确保选项数量合规（2-4个选项），问题数量不超过4个。

### 第二步：参数验证与处理

1. **模块名称处理**：
   - 如果选择"新建模块"，提示输入新模块名称
   - 根据模块名称确定 `siteName`（如：OBS、FCST、MULTISOURCE等）

2. **产品组标识处理**：
   - 如果选择"自定义"，提示输入自定义标识
   - 验证标识格式是否符合规范

3. **产品标题处理**：
   - 如果选择"自定义"，提示输入自定义标题

4. **配置生成规则**：
   - 预报产品必须包含 `productConfig` 配置
   - 实况产品不传 `productConfig`
   - 默认绑定高度轴（`bindHeightAxis: true`）

### 第三步：生成配置代码

根据用户输入的参数，按以下规则生成 `SceneProps` 配置项：

详细生成规则见 [references/product-group-spec.md](references/product-group-spec.md)。

配置模板见 [assets/product-group-template.json](assets/product-group-template.json)。

### 第四步：输出代码

将生成的配置代码片段输出给用户，并说明插入位置：

1. **配置项定义**：插入到 `Scene/src/data.ts` 中合适的位置（与其他同类配置项放在一起）
2. **注册到 `listData`**：按 key 递增规则添加新条目
   - 确定下一个可用的 key（检查现有 key）
   - 生成唯一的 `siteName`
   - 添加到 `listData` ref 数组中

## 组件与视图类型映射

| viewType | 组件目录 | loader | componentProps 标识字段 |
|----------|---------|--------|------------------------|
| `COLOR_MAP` | `ColorMap` | `() => import('../../ColorMap')` | `productGroupIdentify` |
| `WIND` | `WindTest` | `() => import('../../WindTest')` | `productGroupIdentify` |

## 问答示例

```json
{
  "questions": [
    {
      "question": "产品组所属模块名称是什么？",
      "header": "模块名称",
      "options": [
        {"label": "实况立方体", "description": "添加到现有实况立方体模块"},
        {"label": "预报立方体", "description": "添加到现有预报立方体模块"},
        {"label": "多源观测设备", "description": "添加到多源观测设备模块"},
        {"label": "新建模块", "description": "创建一个新的模块"}
      ],
      "multiSelect": false
    },
    {
      "question": "时间维度是什么？",
      "header": "时间维度",
      "options": [
        {"label": "实况", "description": "实时观测数据产品"},
        {"label": "预报", "description": "预报数据产品"}
      ],
      "multiSelect": false
    },
    {
      "question": "产品组标识（productGroupIdentify）是什么？",
      "header": "产品组标识",
      "options": [
        {"label": "ObsCube", "description": "实况立方体产品组标识"},
        {"label": "FcstCube_0_3", "description": "0-3小时预报立方体产品组标识"},
        {"label": "自定义", "description": "输入自定义的产品组标识"}
      ],
      "multiSelect": false
    },
    {
      "question": "产品组标题（title）是什么？",
      "header": "产品标题",
      "options": [
        {"label": "回波测试", "description": "测试用回波产品标题"},
        {"label": "实况立方体", "description": "实况立方体产品标题"},
        {"label": "自定义", "description": "输入自定义的产品组标题"}
      ],
      "multiSelect": false
    }
  ]
}
```

## 参考

- 完整使用案例：`src/components/platform/Meteorology/src/components/Scene/src/data.ts`
- 类型定义：`src/components/platform/Meteorology/src/components/Scene/src/typing.ts`
- 详细规格说明：[references/product-group-spec.md](references/product-group-spec.md)
