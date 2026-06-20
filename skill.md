# Skill: gotap-ui

> JSON 驱动的跨引擎 UI 框架。Godot 可视化编辑，UrhoX 运行时渲染。

## 仓库

- **GitHub**: https://github.com/benzoscode/gotap-ui

## 何时使用

当用户需要以数据驱动方式构建游戏 UI（菜单、HUD、背包等）。

## 使用规范

1. 将 `scripts/json_to_ui.lua` 放入项目 scripts/
2. 将 UI JSON 放入 assets/UI/
3. Lua 中加载：

```lua
local UILoader = require("json_to_ui")
local view = UILoader.load("UI/main_menu.json")
view:FindById("btn_start").onClick = function() end
```

## 关键约束

- JSON 只描述视图，不含逻辑
- 事件通过 id 在 Lua 侧绑定
- flexGrow 只用整数
- 详见 docs/SPEC.md
