# GoTap UI - 计划文档

> 记录项目的设计决策、架构选型和开发路线。

---

## 项目背景

### 问题

TapTap 制造（UrhoX 引擎）缺乏可视化 UI 编辑器。开发者在编写 UI 时无法直观预览，只能反复修改代码 → 构建 → 预览，消耗大量时间。

### 解决方案

建立 **JSON 驱动的 UI 描述格式**，作为跨引擎的中间表示：

1. 在 Godot 中可视化编辑 UI → 导出为 JSON
2. 在 UrhoX 中加载 JSON → 自动构建 UI 树
3. JSON 是唯一真相源（Single Source of Truth）

---

## 架构决策

### D1: 选择 Godot 作为可视化编辑器

**决策日期**: 2026-06-20

**理由**:
- 开发者已熟悉 Godot
- Godot 轻量（~60MB），启动快
- GDScript 编写导出插件简单高效
- 长远考虑：如果未来移植游戏到其他平台，Godot 侧已有完整 UI 运行时，降低移植成本

**否决方案**:
- Cocos Creator：开发者不熟悉，安装体积大
- Web (HTML/CSS)：Flexbox 映射精度最高，但缺乏现成可视化拖拽编辑器

### D2: 布局模型选择 Flexbox 子集

**决策日期**: 2026-06-20

**理由**:
- UrhoX UI 系统底层使用 Yoga (Flexbox)，JSON schema 对齐 Flexbox 语义可减少映射损耗
- Flexbox 是行业事实标准（React Native、Flutter 概念类似）
- Godot 的 Container 系统在"安全子集"范围内可精确映射

**安全子集原则**:
- 只纳入两边都能精确实现的特性
- 不依赖 flex-shrink 压缩行为
- flexGrow 只用整数
- 百分比尺寸只对有明确尺寸的父容器使用

### D3: MVC 分离 — JSON 只描述 View

**决策日期**: 2026-06-20

**理由**:
- UI 描述（View）与交互逻辑（Controller）解耦
- JSON 保持纯数据，可被任意引擎渲染
- 事件绑定通过 id 在代码侧完成
- 利于测试、复用、多语言适配

### D4: Godot 定位为"编辑器 + 备用运行时"

**决策日期**: 2026-06-20

**理由**:
- Godot 侧不是"凑合能预览"，而是完整实现
- 未来移植时可直接作为 UI 运行时使用
- 这要求 JSON schema 必须引擎无关，不暴露任何引擎专有概念

---

## 开发阶段

### Phase 1 - 最小可用

**目标**: 基础布局 + 核心组件，两端都能正确渲染

**组件**:
- Panel (容器)
- Label (文本)
- Button (按钮)
- Image (图片)

**布局属性**:
- flexDirection (row / column)
- justifyContent (flex-start / center / flex-end / space-between)
- alignItems (flex-start / center / flex-end / stretch)
- width / height (px 和 %)
- padding / margin / gap
- flexGrow (整数)
- position: absolute (用于浮动层)

**样式属性**:
- fontSize, color, backgroundColor
- borderRadius
- opacity

**两端实现**:
- UrhoX: json_to_ui.lua - 加载 JSON 构建 UI.* 组件树
- Godot: 导出插件（Container 树 → JSON）+ 导入预览（JSON → Container 树）

### Phase 2 - 丰富组件

**新增组件**:
- ScrollView (滚动容器)
- Grid (网格布局，固定列数)
- Input (文本输入)
- Slider (滑动条)
- ProgressBar (进度条)
- Toggle / Checkbox

**新增特性**:
- 组件状态样式（hover / pressed / disabled）
- 图片九宫格（9-slice）

### Phase 3 - 高级功能

**候选项（按需评估）**:
- 样式继承（父节点 fontSize/color 传递给子节点）
- 主题/皮肤系统（一套 JSON 切换整体风格）
- i18n 支持（text 字段用 key，运行时查表替换）
- 动画描述（简单的 transition 定义）
- flex-wrap（如果 Grid 不能满足需求）
- align-self

---

## 未来考虑（暂不实现，记录备忘）

| 话题 | 思考 |
|------|------|
| 样式继承 | 可能参考 CSS 的继承规则，但游戏 UI 嵌套通常不深，优先级低 |
| 主题系统 | 可以用"变量替换"机制，如 color: "$primary" 指向主题定义 |
| i18n | text 字段可支持 "$key.title" 格式，运行时按语言查表 |
| 响应式断点 | 手机/平板不同布局，可用条件节点或多套 JSON |
| 动画 | 描述入场/离场/过渡动画，两端各自实现 Tween |

---

*最后更新: 2026-06-20*
