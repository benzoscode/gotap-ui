# GoTap UI - 规格文档

> 当前有效的技术规格。本文档只保留最新规格，不包含历史变更记录。
> 标注 [已实现] / [未实现] 表示各特性的实装状态。

---

## 1. JSON 文件格式

### 1.1 顶层结构

```json
{
  "version": "1.0",
  "root": { ... }
}
```

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| version | string | 是 | Schema 版本号，当前 "1.0" |
| root | Node | 是 | UI 树的根节点 |

### 1.2 节点结构 (Node)

```json
{
  "id": "btn_start",
  "type": "Panel",
  "props": { ... },
  "children": [ ... ]
}
```

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| id | string | 否 | 唯一标识，用于代码侧查找和绑定事件 |
| type | string | 是 | 组件类型（见第 2 节） |
| props | object | 否 | 属性集合（布局 + 样式 + 组件专属） |
| children | Node[] | 否 | 子节点列表 |

---

## 2. 组件类型

### Phase 1 组件 [未实现]

| type | 说明 | 专属属性 |
|------|------|----------|
| Panel | 通用容器，可嵌套 | 无 |
| Label | 文本显示 | text, fontSize, fontWeight, textAlign |
| Button | 可点击按钮 | text, variant |
| Image | 图片显示 | src, fit |

### Phase 2 组件 [未实现]

| type | 说明 | 专属属性 |
|------|------|----------|
| ScrollView | 可滚动容器 | direction |
| Grid | 网格布局 | columns, rowGap, columnGap |
| Input | 文本输入框 | placeholder, maxLength |
| Slider | 滑动条 | min, max, step, value |
| ProgressBar | 进度条 | value, max |
| Toggle | 开关 | checked |

---

## 3. 布局属性 (Layout Props)

所有 Panel 类型（含 ScrollView、Grid）可使用布局属性。

### 3.1 Flex 容器属性 [未实现]

| 属性 | 类型 | 默认值 | 可选值 | 说明 |
|------|------|--------|--------|------|
| flexDirection | string | "column" | "row", "column" | 主轴方向 |
| justifyContent | string | "flex-start" | "flex-start", "center", "flex-end", "space-between", "space-around" | 主轴对齐 |
| alignItems | string | "stretch" | "flex-start", "center", "flex-end", "stretch" | 交叉轴对齐 |
| gap | number | 0 | - | 子元素间距 (px) |

### 3.2 尺寸属性 [未实现]

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| width | number 或 string | auto | 像素值(number)或百分比(string如"50%") |
| height | number 或 string | auto | 同上 |
| minWidth | number | - | 最小宽度 (px) |
| minHeight | number | - | 最小高度 (px) |
| maxWidth | number | - | 最大宽度 (px) |
| maxHeight | number | - | 最大高度 (px) |

### 3.3 Flex 子元素属性 [未实现]

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| flexGrow | number (整数) | 0 | 占据剩余空间的比例 |

### 3.4 间距属性 [未实现]

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| padding | number | 0 | 内边距，四边相同 (px) |
| paddingTop | number | - | 单独设置上内边距 |
| paddingRight | number | - | 单独设置右内边距 |
| paddingBottom | number | - | 单独设置下内边距 |
| paddingLeft | number | - | 单独设置左内边距 |
| margin | number | 0 | 外边距，四边相同 (px) |
| marginTop | number | - | 单独设置上外边距 |
| marginRight | number | - | 单独设置右外边距 |
| marginBottom | number | - | 单独设置下外边距 |
| marginLeft | number | - | 单独设置左外边距 |

### 3.5 定位属性 [未实现]

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| position | string | "relative" | "relative" 或 "absolute" |
| top | number | - | 绝对定位时距父容器顶部 (px) |
| right | number | - | 绝对定位时距父容器右侧 (px) |
| bottom | number | - | 绝对定位时距父容器底部 (px) |
| left | number | - | 绝对定位时距父容器左侧 (px) |

---

## 4. 样式属性 (Style Props)

所有组件均可使用。

### 4.1 通用样式 [未实现]

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| backgroundColor | string | "transparent" | 背景颜色，格式 "#RRGGBB" 或 "#RRGGBBAA" |
| borderRadius | number | 0 | 圆角半径 (px) |
| opacity | number | 1.0 | 透明度 0.0 ~ 1.0 |
| visible | boolean | true | 是否可见 |

### 4.2 文本样式 [未实现]

适用于 Label、Button 等含文本的组件。

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| fontSize | number | 16 | 字体大小 (px) |
| color | string | "#FFFFFF" | 文本颜色 |
| fontWeight | string | "normal" | "normal" 或 "bold" |
| textAlign | string | "left" | "left", "center", "right" |

---

## 5. 组件专属属性

### 5.1 Label [未实现]

| 属性 | 类型 | 必填 | 说明 |
|------|------|------|------|
| text | string | 是 | 显示文本 |

### 5.2 Button [未实现]

| 属性 | 类型 | 必填 | 说明 |
|------|------|------|------|
| text | string | 是 | 按钮文本 |
| variant | string | 否 | 预设样式: "primary", "secondary", "danger" |

### 5.3 Image [未实现]

| 属性 | 类型 | 必填 | 说明 |
|------|------|------|------|
| src | string | 是 | 图片路径（相对于项目资源目录） |
| fit | string | 否 | 填充模式: "contain", "cover", "fill", "none" |

---

## 6. 运行时接口约定 (Controller API)

两端实现必须提供以下统一接口，供 Controller 层使用：

### 6.1 加载 [未实现]

```
UILoader.load(jsonPath) → ViewRoot
```

### 6.2 查找 [未实现]

```
ViewRoot:FindById(id) → Component | nil
```

### 6.3 组件通用方法 [未实现]

| 方法 | 说明 |
|------|------|
| :SetText(string) | 设置文本内容 |
| :SetVisible(bool) | 设置可见性 |
| :SetDisabled(bool) | 设置禁用状态 |
| :SetStyle(propName, value) | 动态修改单个样式属性 |

### 6.4 事件绑定 [未实现]

```
component.onClick = function(self) ... end
component.onValueChange = function(self, value) ... end
```

---

## 7. 映射规则

### 7.1 JSON → UrhoX (urhox-libs/UI)

| JSON type | UrhoX 组件 |
|-----------|-----------|
| Panel | UI.Panel |
| Label | UI.Label |
| Button | UI.Button |
| Image | UI.Image |
| ScrollView | UI.ScrollView |
| Grid | UI.Grid |

布局属性直接对应 Yoga Flexbox 属性，UrhoX UI 原生支持。

### 7.2 JSON → Godot

| JSON type | Godot 节点 |
|-----------|-----------|
| Panel (column) | VBoxContainer |
| Panel (row) | HBoxContainer |
| Panel (absolute children) | Control |
| Label | Label |
| Button | Button |
| Image | TextureRect |
| ScrollView | ScrollContainer |
| Grid | GridContainer |

布局属性映射:

| JSON 属性 | Godot 实现方式 |
|-----------|---------------|
| flexDirection | 选择 VBox 或 HBox Container |
| justifyContent | Container alignment 属性 |
| alignItems | 子节点 size_flags_vertical/horizontal |
| width/height (px) | custom_minimum_size |
| width/height (%) | size_flags_expand + stretch_ratio |
| flexGrow | size_flags_expand + stretch_ratio |
| gap | theme_override "separation" |
| padding | MarginContainer 包装或 theme override |
| margin | 外层 MarginContainer |
| position: absolute | 不放入 Container，直接用 anchors |

---

## 8. 约束与限制

为保证两端行为一致，以下规则必须遵守：

1. **flexGrow 只用整数** (1, 2, 3)，不用小数
2. **百分比尺寸** 只对有明确固定尺寸的父容器使用
3. **不依赖 shrink 行为** — 设计时确保内容不会溢出父容器
4. **id 全局唯一** — 同一 JSON 文件内不可重复
5. **颜色格式统一** — 只用 "#RRGGBB" 或 "#RRGGBBAA"
6. **单位统一** — 所有数值型尺寸/间距单位为 px（逻辑像素）

---

## 9. 示例

### 9.1 简单主菜单

```json
{
  "version": "1.0",
  "root": {
    "type": "Panel",
    "props": {
      "width": "100%",
      "height": "100%",
      "flexDirection": "column",
      "justifyContent": "center",
      "alignItems": "center",
      "gap": 20,
      "backgroundColor": "#1a1a2e"
    },
    "children": [
      {
        "id": "title",
        "type": "Label",
        "props": {
          "text": "我的游戏",
          "fontSize": 48,
          "color": "#ffffff",
          "fontWeight": "bold"
        }
      },
      {
        "id": "btn_start",
        "type": "Button",
        "props": {
          "text": "开始游戏",
          "width": 240,
          "height": 56,
          "variant": "primary"
        }
      },
      {
        "id": "btn_settings",
        "type": "Button",
        "props": {
          "text": "设置",
          "width": 240,
          "height": 56
        }
      }
    ]
  }
}
```

### 9.2 带顶栏的游戏 HUD

```json
{
  "version": "1.0",
  "root": {
    "type": "Panel",
    "props": {
      "width": "100%",
      "height": "100%",
      "flexDirection": "column",
      "justifyContent": "space-between"
    },
    "children": [
      {
        "id": "top_bar",
        "type": "Panel",
        "props": {
          "width": "100%",
          "height": 60,
          "flexDirection": "row",
          "alignItems": "center",
          "padding": 12,
          "gap": 8,
          "backgroundColor": "#000000AA"
        },
        "children": [
          {
            "id": "avatar",
            "type": "Image",
            "props": {
              "src": "Textures/avatar.png",
              "width": 40,
              "height": 40,
              "borderRadius": 20
            }
          },
          {
            "id": "hp_bar_bg",
            "type": "Panel",
            "props": {
              "flexGrow": 1,
              "height": 20,
              "backgroundColor": "#333333",
              "borderRadius": 10
            },
            "children": [
              {
                "id": "hp_bar_fill",
                "type": "Panel",
                "props": {
                  "width": "75%",
                  "height": "100%",
                  "backgroundColor": "#e74c3c",
                  "borderRadius": 10
                }
              }
            ]
          },
          {
            "id": "score_label",
            "type": "Label",
            "props": {
              "text": "0",
              "fontSize": 24,
              "color": "#f1c40f",
              "fontWeight": "bold"
            }
          }
        ]
      }
    ]
  }
}
```

---

*规格版本: 1.0*
*最后更新: 2026-06-20*
