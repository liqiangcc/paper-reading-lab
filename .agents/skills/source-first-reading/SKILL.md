---
name: source-first-reading
description: 在一篇论文的原始专属会话中基于 reading-mcp 持续逐句分析，支持开始、下一句、追问和回看；不提供跨会话恢复，不用于仓库修改。
---

# Source-First Reading

遵循 [AGENTS](../../../AGENTS.md)。本文件定义读取操作，分析质量由[分析协议](../../../docs/learning/source-first-sentence-reading.md)负责。

## 开始与同会话继续

先区分首次开始与原会话继续。已有阅读但当前不是原阅读会话，或必要上下文不可用时，按[会话边界](../../../docs/learning/reading-sessions.md#一篇论文一个原始会话)停止续读；不从 Issue、历史评论或日志恢复。维护会话不承担论文续读。

首次开始：用户确定论文后查找已有 Paper Issue，必要时创建入口，不重复建论文 Issue。核对版本和来源，用 open_document 取得身份、get_document_structure 的无正文结构确定授权范围及起点。版本或范围不明时询问缺失信息，不读正文探路；已有历史停点不自动成为新起点。按[版本加载规则](../../../docs/learning/reading-sessions.md#规则版本加载)加载协议及示范，然后从已确认的结构起点读取。

原会话继续：使用本会话的身份、范围、精确位置、前文与已加载规则；不每句读取 Issue 或重新加载仓库，不要求用户重复风格提示。

## 下一句

1. 先检查[未完成单元](../../../docs/learning/reading-sessions.md#已揭示与已完成)：如有，只补完同一目标。否则确认下一单元能被工具限制在已授权范围内；不能确认时停止。
2. 调用 get_text_units，使用绑定 document、允许的 section 与已完成单元的精确 anchor；首次从已确认的结构起点读取。默认 requested_kind=sentence、coverage_policy=preserve_source、direction=forward、max_items=1。
3. 按[返回结果处理](../../../docs/integrations/reading-mcp.md#返回结果处理)核对身份和范围，立即记录实际暴露与待完成动作。用返回 TextLocator 调用 read_document(document_id, target_locator)，不同时加 section_id；核对完整性，不擅自过滤后再取第二个单元。
4. 完整回读后，按本会话已加载的分析协议连接相关已读前文、解释当前单元。输出分析后才清除待完成动作；工具成功不等于分析完成。
5. 展示可靠停点并结束，等待用户；同会话重试完成后也不顺带推进下一单元。

## 追问、回看与记录

追问与回看只解释本会话已有内容，必要时精确回读已授权 locator，不推进后文；它不是用来重建另一会话上下文的入口。视觉读取遵守 [Source Adapter](../../../docs/integrations/reading-mcp.md) 的范围约束。

按[进度记录规则](../../../docs/learning/reading-sessions.md#何时保存)在需要时保存必要进度和问题，不生成恢复包或逐句日志。故障重试保留当前目标、身份和范围，重试上限见 Source Adapter；stale/mismatch 或关键上下文缺失时停止，不模糊补文，不要求新开试次。
