# vesta-design-doc —— Vesta 技术方案

一个 skill + 一份模板。让「写技术方案」这件事在团队里有统一的结构。

## 安装

```
/plugin marketplace add jupiter-eng/vesta-claude-plugins
/plugin install vesta-design-doc@vesta
```

建本地文件不需要令牌；建到飞书要先装好 `lark-*` skill 并完成 `lark-cli` 授权。

## 用起来

**只能手动调用**（原因见下面「调用方式」）：

```
/vesta-design-doc:create-template 在 docs/design/ 下建一份批量导入的技术方案
/vesta-design-doc:create-template 在飞书文件夹 https://xxx.feishu.cn/drive/folder/xxx 下建一份用量上报的技术方案
```

它**只建模板，不写正文**：

## 调用方式：故意设成手动

`skills/create-template/SKILL.md` 的 frontmatter 里有一行：

```yaml
disable-model-invocation: true
```

这是**有意选择**：让 Claude 不能自己决定触发，只有你显式打
`/vesta-design-doc:create-template` 才会跑。这样不会出现「随口提了句技术方案，
它自己在飞书建了一份文档」。

