# GoTap UI

跨引擎的 JSON 驱动 UI 框架。在 Godot 中可视化编辑，在 UrhoX (TapTap 制造) 中运行。

## 工作流

```
Godot 编辑器 → 导出 JSON → UrhoX 运行时渲染
                  ↑
            唯一真相源
```

## 核心理念

- **JSON 是 UI 的唯一描述格式** — 引擎无关，可移植
- **MVC 分离** — JSON 只管视图(View)，逻辑在代码侧通过 id 绑定
- **Flexbox 子集** — 两端都能精确实现的布局模型
- **渐进式** — 从基础组件开始，按需扩展

## 项目结构

```
/
├── docs/                    # 设计文档
│   ├── PLAN.md              # 决策与路线
│   └── SPEC.md              # 当前技术规格
├── scripts/                 # UrhoX 实现 (json_to_ui.lua)
├── gotap-ui/                # 框架源码
│   ├── examples/            # 示例 JSON 文件
│   ├── schemas/             # JSON Schema 定义
│   └── godot/               # Godot 插件工程
└── skill.md                 # UrhoX skill 复用文件
```

## 快速开始

### 在 UrhoX 项目中使用

```lua
local UILoader = require("json_to_ui")

local view = UILoader.load("UI/main_menu.json")
view:FindById("btn_start").onClick = function() StartGame() end
view:FindById("score_label"):SetText(tostring(score))
```

### 在 Godot 中编辑

1. 安装 `gotap-ui/godot/addons/gotap_ui` 插件
2. 使用 Container 节点搭建 UI
3. 导出 JSON → 放入 UrhoX 项目 assets/UI/

## 文档

- [docs/PLAN.md](docs/PLAN.md) — 设计决策与路线
- [docs/SPEC.md](docs/SPEC.md) — 当前技术规格

## 许可证

MIT
