# Paper Reading Lab

在一篇论文的专属原始会话中持续阅读 AI 的高质量逐句分析，学习如何根据已有信息作出有依据的判断。

AI 负责把对象、线索、必要前提和推导连接层层讲透，使后一层自然承接前一层；用户只需持续阅读、反复看或按需追问，以潜移默化地提高分析能力为目标。本仓库不提供训练、测验或评分，也不保留可选训练流程。简化的是操作机制，不是分析深度；不把清楚易懂直接当作能力提升的证明。

## 怎么用

从[待读论文清单](https://github.com/liqiangcc/paper-reading-lab/issues/28)选题，或按标签查看[论文入口](https://github.com/liqiangcc/paper-reading-lab/issues?q=is%3Aissue%20label%3Atype%3Apaper)、[阅读清单](https://github.com/liqiangcc/paper-reading-lab/issues?q=is%3Aissue%20label%3Atype%3Areading-list)、[维护任务](https://github.com/liqiangcc/paper-reading-lab/issues?q=is%3Aissue%20label%3Atype%3Atask)。一篇论文使用一个专属阅读会话，仓库维护另开会话。

```text
首次：开始逐句阅读这篇论文，使用本会话作为专属阅读会话。
之后始终在该会话：下一句。
追问：这句的中间理由再讲清楚，不读取下一句。
```

日常只有一条路径：

```text
承接本会话前文 → 读取当前原文 → 讲清分析 → 等待下一句
```

“停止”表示本句结束，不是要求换新会话。暂停后回到原会话继续；Issue 只记录必要进度和问题，不能替代原会话。不提供跨会话恢复、交接重建或持久化模型快照。同一会话也可能压缩，关键前文不可用时明确缺口并停止依赖它推论，不声称上下文永不丢失。

## 规则放在哪里

- [AGENTS.md](AGENTS.md)：Agent 入口和必要边界。
- [逐句分析协议](docs/learning/source-first-sentence-reading.md)：唯一的日常分析质量标准。
- [Reading Skill](.agents/skills/source-first-reading/SKILL.md)：读取、解释和保存的操作步骤。
- [会话与进度](docs/learning/reading-sessions.md)：原会话边界和最小进度记录，不提供恢复。
- [文档导航](docs/README.md)：工具细节、工程维护和历史证据按需查阅。

reading-mcp 提供真实原文与精确定位；GitHub 保存规则和进度。AI 分析不替代原文，不使用未揭示后文，不擅自切换论文版本。

本仓库维护分析规则和必要原文约束：Source binding 固定论文版本及 provider 身份，范围、位置、未完成动作和理解过程在阅读会话内保留，Paper Issue 只提供论文入口与进度参考。原文解析和单元 identity 由 reading-mcp 负责；不另建解析器、句子索引、聊天数据库、恢复系统或知识导出流水线。一次分析结束不表示论文永久学完。

## 验证边界

CI 检查仓库文件和链接，不证明分析正确或用户已经掌握。分析质量在真实阅读中检查：是否误读、是否跳步、依据是否清楚、是否有多余负担；发现具体问题就修正，不另设常规测试流水线。

现行分析契约为 `source-first-analysis/v2`。旧训练式规则已从当前文件树删除；原 commit 与历史 Issue 证据保留供追溯，不再调度。已有阅读采用新契约时记录一次切换，Source、范围和位置不变。
