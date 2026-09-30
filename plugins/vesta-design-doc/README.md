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

| 目标 | 做法 |
|---|---|
| 本地 markdown | 复制模板文件到指定目录，已存在不覆盖 |
| 飞书 | 用 `lark-*` skill 建文档 |
| 其他平台 | 用该平台的 skill / 连接器；没有就复制到本地并告诉你 |

没说放哪，它会问一句。

## 调用方式：故意设成手动

`skills/create-template/SKILL.md` 的 frontmatter 里有一行：

```yaml
disable-model-invocation: true
```

这是**有意选择**：让 Claude 不能自己决定触发，只有你显式打
`/vesta-design-doc:create-template` 才会跑。这样不会出现「随口提了句技术方案，
它自己在飞书建了一份文档」。

三种可见性的区别：

| frontmatter | 你能调 | Claude 能自动调 | description 占上下文 |
|---|---|---|---|
| 默认（不写这行） | 能 | 能 | 常驻 |
| **`disable-model-invocation: true`**（当前） | 能 | 不能 | **不加载** |
| `user-invocable: false` | 不能 | 能 | 常驻 |

附带好处是第三列：description 不进上下文，挂着零成本。

**想放开自动触发**：删掉那一行即可，description 已经写好了，不用再改。

## 模板

`templates/vesta-design-doc-template.md`，七节 + 评审 TODO：

1. **背景** —— 需求背景、本次范围（**包含 / 不包含都要写**）
2. **相关链接**
3. **技术方案**
   - 3.1 **现状能力盘点** —— PRD 需求逐条映射到现有接口
   - 3.2 **总体设计** —— 静态结构：架构图 · 职责边界 · 数据流
   - 3.3 **方案选型** —— 岔路口决策
   - 3.4 **详细设计** —— 按功能路径分节：做什么 · 配图 · 新引入的东西（含接口详情 · 数据变更）· 异常处理
   - 3.5 **关键机制设计** —— 跨路径的公共契约
   - 3.6 **关键技术缺口** —— 开发前要拍板的
4. **接口与数据变更一览** —— 两张表，详情在 3.4，这里不重抄
5. **改动影响** —— 兼容性 + 上线清单
6. **测试验收** —— 含回归范围
7. **排期** —— 阶段表 + 关键节点

**评审 TODO** —— 需要在评审会上拍板的问题，每条带 owner

模板是从团队一份已评审通过的方案里提炼的，不是通用模板。每节该写什么、
什么算写够了，都写在模板自己的注释里 —— 改模板直接改那个文件就行。
