# Vesta Claude Code 插件

Vesta 团队的 Claude Code 插件仓库。

| 插件 | 干什么 | 需要令牌 |
|---|---|---|
| [`vesta-design-doc`](plugins/vesta-design-doc/README.md) | 按团队模板新建技术方案（本地 / 飞书 / 其他平台） | 本地否；飞书需 `lark-cli` 授权 |

## 安装

```
/plugin marketplace add jupiter-eng/vesta-claude-plugins
/plugin install vesta-design-doc@vesta
```

斜杠命令只在**终端的 Claude Code CLI** 可用；
桌面版 Code 标签页不认 `/plugin`，要用输入框旁的 **`+` → Plugins → Add plugin**。

## vesta-design-doc —— 技术方案

按团队模板新建一份空白技术方案，只建模板不写正文。只能**手动调用**：

```
/vesta-design-doc:create-template 在 docs/design/ 下建一份 xxx 的技术方案
/vesta-design-doc:create-template 在飞书文件夹 <链接> 下建一份 xxx 的技术方案
```

本地直接复制模板文件；飞书用 `lark-*` skill 导入；其他平台找会话里对应的工具。

## 更新与版本

装过的人**不会自动收到**你的改动 —— Claude Code 的后台自动更新默认关闭，
而且 `marketplace.json` 里没有字段能替用户打开。用户要么自己在
`/plugin` → Marketplaces → Enable auto-update，要么手动跑：

```
/plugin marketplace update vesta
```

**本仓库刻意不写 `version`**（`plugin.json` 和 marketplace 条目都没有）。
原因：Claude Code 只在插件的**版本字符串变化**时才给用户发新副本 ——
如果钉死 `"version": "0.1.0"` 然后不停 push，用户 update 了也拿不到新代码。
省掉 `version` 之后，用户跟随本仓库的 commit，push 完 update 一下就生效。

所以 `claude plugin validate` 会报一条 `No version specified` 的 **warning，这是预期的**，
不要为了消掉它而加回 `version`。等插件稳定、需要按版本发布时再加，
并且**只加在一处**（`plugin.json` 或 marketplace 条目，不要两处都写）。

## 加新插件

1. 在 `plugins/<name>/` 下放 `.claude-plugin/plugin.json` 和组件目录
2. 在根 `.claude-plugin/marketplace.json` 的 `plugins` 数组里加一项
3. `claude plugin validate .` 过了再提

更新已装插件见上面「更新与版本」。
