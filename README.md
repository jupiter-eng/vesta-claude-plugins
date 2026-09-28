# Vesta Claude Code 插件

Vesta 团队的 Claude Code 插件仓库。

| 插件 | 干什么 | 需要令牌 |
|---|---|---|
| [`vesta-design-doc`](plugins/vesta-design-doc/README.md) | 按团队模板写功能技术方案 | 否，纯本地 |

## 安装

团队统一走 zettabyte 的 marketplace —— 注册表在那边，插件代码在本仓库：

```
/plugin marketplace add zettabyte-inc/claude-plugins
/plugin install vesta-design-doc@zettabyte
```

也可以直接从本仓库装，不经过 zettabyte：

```
/plugin marketplace add jupiter-eng/vesta-claude-plugins
/plugin install vesta-design-doc@vesta
```

两条路装的是同一份代码。斜杠命令只在**终端的 Claude Code CLI** 可用；
桌面版 Code 标签页不认 `/plugin`，要用输入框旁的 **`+` → Plugins → Add plugin**。

## 为什么是两个仓库

插件代码和迭代都在本仓库，团队自己说了算；
`zettabyte-inc/claude-plugins` 只在它的 `marketplace.json` 里留一条指向这里的记录：

```json
{
  "name": "vesta-design-doc",
  "source": {
    "source": "git-subdir",
    "url": "jupiter-eng/vesta-claude-plugins",
    "path": "plugins/vesta-design-doc"
  }
}
```

这样团队只需要记一个 marketplace，两个插件（`ops-report` 和这个）在同一个 `/plugin` 列表里。
好处是**注册只需一次**：`source` 不带 `ref`，默认跟随本仓库默认分支，
所以之后插件怎么改、怎么发版，都不需要再动 zettabyte 那边。

## vesta-design-doc —— 技术方案

按团队模板写功能技术方案。初版只能**手动调用**：

```
/vesta-design-doc:write 根据 @prd/xxx_PRD.md 写一份技术方案，涉及 A 和 B 两个服务
```

不让它自动触发是为了 eval 阶段每次产出可控可复现 —— 原因和放开方式写在
[插件 README](plugins/vesta-design-doc/README.md) 里。

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
4. 想让它也出现在 zettabyte 的列表里，去那边的 `marketplace.json` 加一条
   `git-subdir` 记录（要提 PR，本团队没有该仓库的写权限）

更新已装插件见上面「更新与版本」。
