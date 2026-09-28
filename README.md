# Vesta Claude Code 插件

Vesta 团队内部用的 Claude Code 插件 marketplace。

| 插件 | 干什么 | 需要令牌 |
|---|---|---|
| [`vesta-design-doc`](plugins/vesta-design-doc/README.md) | 按团队模板写功能技术方案 | 否，纯本地 |

## 安装

在终端的 Claude Code CLI 里：

```
/plugin marketplace add jupiter-eng/claude-plugins
/plugin install vesta-design-doc@vesta
```

没配 GitHub SSH key 的话，第一条改用完整 HTTPS 地址（`owner/repo` 简写默认走 SSH）：

```
/plugin marketplace add https://github.com/jupiter-eng/claude-plugins.git
```

斜杠命令只在**终端的 Claude Code CLI** 可用。桌面版 Code 标签页不认 `/plugin`，
要用输入框旁的 **`+` → Plugins → Add plugin**。

## vesta-design-doc —— 技术方案

按团队模板写功能技术方案。纯本地，不连任何服务。

初版只能**手动调用**：

```
/vesta-design-doc:write 根据 @prd/xxx_PRD.md 写一份技术方案，涉及 A 和 B 两个服务
```

之所以不让它自动触发，是为了 eval 阶段每次产出可控可复现 —— 原因和放开方式
写在[插件 README](plugins/vesta-design-doc/README.md) 里。

## 加新插件

1. 在 `plugins/<name>/` 下放 `.claude-plugin/plugin.json` 和组件目录
2. 在根 `.claude-plugin/marketplace.json` 的 `plugins` 数组里加一项
3. `claude plugin validate .` 过了再提

装完更新用 `/plugin marketplace update vesta`。
