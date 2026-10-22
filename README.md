# Vesta Claude Code 插件

| 插件 | 干什么 |
|---|---|
| [`vesta-design-doc`](plugins/vesta-design-doc/README.md) | 写技术方案：起草、审阅、精简。带骨架、表述规范、自检清单 |

## 安装

```
/plugin marketplace add jupiter-eng/vesta-claude-plugins
/plugin install vesta-design-doc@vesta
```

`/plugin` 只在**终端的 Claude Code CLI** 可用。桌面版用输入框旁的 **`+` → Plugins → Add plugin**。

## 用起来

装好直接说话，不用记命令：

```
写一份用量上报的技术方案          → 起草：按骨架建文档
这份方案帮我看看，哪里要优化       → 审阅：分 P0/P1/P2 输出，每条指到具体位置
太啰嗦了，帮我精简一下            → 精简：先砍重复，再把长论述转成表
```

细节与模板见[插件 README](plugins/vesta-design-doc/README.md)。

## 更新

装过的人**不会自动收到**改动——Claude Code 的自动更新默认关闭，`marketplace.json` 里也没有字段能替用户打开。让他们跑：

```
/plugin marketplace update vesta
```

⚠ **本仓库刻意不写 `version`。** Claude Code 只在版本字符串变化时才下发新副本——钉死 `"version": "0.1.0"` 再不停 push，用户 update 了也拿不到新代码。省掉它，用户就跟随本仓库的 commit。

所以 `claude plugin validate` 会报一条 `No version specified` 警告，**这是预期的**，别为了消警告加回去。

## 加新插件

1. `plugins/<name>/` 下放 `.claude-plugin/plugin.json` 和组件目录
2. 根 `.claude-plugin/marketplace.json` 的 `plugins` 数组加一项
3. `claude plugin validate .` 过了再提

---

`README.md` · v1.0 · 10/2026
