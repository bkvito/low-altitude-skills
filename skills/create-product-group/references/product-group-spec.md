# 产品组配置规格说明

## 参数收集流程

创建产品组时，通过交互式问答收集以下参数：

### 1. 产品组所属模块名称
- **选项**：实况立方体、预报立方体、多源观测设备、新建模块
- **描述**：选择现有模块或创建新模块
- **对应字段**：`listData` 中的 `title`

### 2. 时间维度
- **选项**：实况、预报
- **描述**：确定产品类型（实况观测或预报数据）
- **影响**：预报产品需要包含 `productConfig` 配置

### 3. 产品组标识（productGroupIdentify）
- **选项**：ObsCube、FcstCube_0_3、自定义
- **描述**：产品组的唯一标识符
- **对应字段**：`componentProps.productGroupIdentify`

### 4. 产品组标题（title）
- **选项**：回波测试、实况立方体、自定义
- **描述**：产品组在界面中显示的标题
- **对应字段**：配置项的 `title`

### 5. placeholderHeight（可选）
- **默认值**：100
- **描述**：组件高度占位

## 视图类型枚举（ViewEnum）

```ts
enum ViewEnum {
  COLOR_MAP = 'COLOR_MAP', // 色斑图
  WIND = 'WIND',           // 风场
}
```

## SceneProps 类型定义

```ts
export interface SceneProps<
  T extends Pick<T, 'placeholderHeight' | 'loader' | 'componentProps'>,
> {
  key?: string;
  title: string;                    // 必填：组件名称
  backgroundImage: string;          // 必填：二级菜单背景图
  placeholderHeight?: number;       // 可选：组件高度占位，默认 100
  loader: T['loader'];              // 必填：组件动态加载器
  componentProps?: T['componentProps']; // 可选：组件的 props
}
```

## 各视图类型组件 Props 定义

### ColorMap 组件 Props（COLOR_MAP）

```ts
interface ColorMapProps {
  productGroupIdentify: string;   // 产品组标识
  viewType: ViewEnum.COLOR_MAP;   // 视图类型
  productConfig?: ProductConfig;  // 预报产品需传此配置
}
```

### WindTest 组件 Props（WIND）

```ts
interface WindTestProps {
  productGroupIdentify: string;   // 产品组标识
  viewType: ViewEnum.WIND;        // 视图类型
  productConfig?: ProductConfig;  // 预报产品需传此配置
}
```

## ProductConfig 配置

### 实况产品

实况产品**不需要**传 `productConfig`。

```ts
componentProps: {
  productGroupIdentify: 'ObsCube',
  viewType: ViewEnum.COLOR_MAP,
}
```

### 预报产品

预报产品**必须**传 `productConfig`，包含 `isForecastProduct: true`、`matcher` 对象，并默认绑定高度轴（`bindHeightAxis: true`）。

```ts
componentProps: {
  productGroupIdentify: 'FcstCube_0_3',
  viewType: ViewEnum.COLOR_MAP,
  productConfig: {
    bindHeightAxis: true,
    isForecastProduct: true,
    matcher: {
      time: '',   // 时间匹配器，由业务方填写具体值
      height: '', // 高度匹配器，由业务方填写具体值
    },
  },
}
```

## 完整配置生成模板

### 色斑图产品组 - 实况

```ts
const TODO_CONFIG_NAME: SceneProps<DynamicAsyncComponentProps<ColorMapProps>>[] = [
  {
    title: 'TODO_TITLE',
    backgroundImage: secondMenu,
    placeholderHeight: 100,
    loader: () => import('../../ColorMap'),
    componentProps: {
      productGroupIdentify: 'TODO_IDENTIFY',
      viewType: ViewEnum.COLOR_MAP,
    },
  },
];
```

### 色斑图产品组 - 预报

```ts
const TODO_CONFIG_NAME: SceneProps<DynamicAsyncComponentProps<ColorMapProps>>[] = [
  {
    title: 'TODO_TITLE',
    backgroundImage: secondMenu,
    placeholderHeight: 100,
    loader: () => import('../../ColorMap'),
    componentProps: {
      productGroupIdentify: 'TODO_IDENTIFY',
      viewType: ViewEnum.COLOR_MAP,
      productConfig: {
        bindHeightAxis: true,
        isForecastProduct: true,
        matcher: {
          time: '',
          height: '',
        },
      },
    },
  },
];
```

### 风场产品组 - 实况

```ts
const TODO_CONFIG_NAME: SceneProps<DynamicAsyncComponentProps<WindTestProps>>[] = [
  {
    title: 'TODO_TITLE',
    backgroundImage: secondMenu,
    placeholderHeight: 100,
    loader: () => import('../../WindTest'),
    componentProps: {
      productGroupIdentify: 'TODO_IDENTIFY',
      viewType: ViewEnum.WIND,
    },
  },
];
```

### 风场产品组 - 预报

```ts
const TODO_CONFIG_NAME: SceneProps<DynamicAsyncComponentProps<WindTestProps>>[] = [
  {
    title: 'TODO_TITLE',
    backgroundImage: secondMenu,
    placeholderHeight: 100,
    loader: () => import('../../WindTest'),
    componentProps: {
      productGroupIdentify: 'TODO_IDENTIFY',
      viewType: ViewEnum.WIND,
      productConfig: {
        bindHeightAxis: true,
        isForecastProduct: true,
        matcher: {
          time: '',
          height: '',
        },
      },
    },
  },
];
```

## 注册到 listData

生成配置项后，需在 `Scene/src/data.ts` 的 `listData` ref 中注册：

```ts
{
  key: 'TODO_NEXT_KEY',        // 递增的唯一 key（字符串）
  title: 'TODO_MODULE_TITLE',  // 所属模块名称（如：实况立方体）
  siteName: 'TODO_SITE_NAME',  // 站点标识
  sumMenu: TODO_CONFIG_NAME,   // 对应的配置变量名
}
```

### listData 现有 key 参考（避免重复）

| key | title | siteName |
|-----|-------|----------|
| '1' | 实况立方体 | OBS |
| '2' | 预报立方体 | FCST |
| '3' | 多源观测设备 | MULTISOURCE |
| '4' | 数据质控 | DATAQUALITYCONTROL |
| '11' | 北斗网格 | BEIDOUGRID |
