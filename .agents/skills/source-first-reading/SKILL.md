---
name: source-first-reading
description: 基于 reading-mcp 原文开始或恢复逐句分析，支持下一句、追问和回看；负责原文分析与必要阅读状态，不用于仓库修改。
---

# Source-First Reading

遵循 [AGENTS](../../../AGENTS.md)。本文件只定义操作，分析质量由阅读状态绑定的协议定义。

## 开始或恢复

有目标 Paper Issue 时先读其正文；尚无明确 Issue 时先查找该论文已有入口，避免重复创建。检查是否已有阅读历史；已有状态时按[恢复规则](../../../docs/workflows/issue-driven-workflow.md#恢复与并发)取得当前记录，核对身份、范围、已揭示位置、未完成动作及前文模型。旧指针或状态丢失不能视作首次阅读，默认不加载全部评论。

确认首次启动时：复用已有 Primary Issue，尚无则在用户已决定开始该论文后创建；核对论文版本与来源，用 `open_document` 获取身份、`get_document_structure` 的无正文结构确定用户授权范围及起点。版本或范围不明时只询问缺失选择，不读取正文探路；候选清单本身不授予阅读范围。完成下述版本加载后，保存初始状态（已揭示位置与待完成单元均为 none、前文模型为空）并核对 Issue 指针，首单元从该范围的结构起点读取，不编造 anchor。

两条路径都在任何正文调用前完成[规则版本加载](../../../docs/learning/reading-sessions.md#规则版本加载)。新状态须带固定契约 commit；已有绑定不可因仓库更新静默切换。

同一会话已核验的规则和状态直接继续使用；不用每句重读仓库、探测所有工具或新开 Session。能力检查并入实际需要的工具调用。

## 下一句

1. 先检查[未完成单元](../../../docs/learning/reading-sessions.md#已揭示与已完成)：若存在，恢复同一目标的回读或分析，本次不枚举新单元。否则确认下一单元可被工具限制在当前授权范围内；不能确认时先停。
2. 无待完成单元时调用 `get_text_units`，使用绑定 document、允许 owner/section 和已完成单元的精确 anchor；首次无 anchor 时从已确认的结构起点读取。默认 `requested_kind=sentence`、`coverage_policy=preserve_source`、`direction=forward`、`max_items=1`。
3. 按[返回结果处理](../../../docs/integrations/reading-mcp.md#返回结果处理)检查枚举结果；取得单元后立即记录实际暴露与待完成动作，再用其 `TextLocator` 调用 `read_document(document_id, target_locator)`，不同时加 `section_id`。核对 identity、范围、完整性；不擅自过滤后再读取第二个。
4. 同一目标完整回读后，执行开始时已加载的固定版本分析协议。完成分析输出后更新模型、清除待完成动作；不能仅凭工具成功标记分析完成。
5. 本次输出结束，等待用户继续。若本次是失败恢复，完成后也不顺带推进下一单元。

## 追问与回看

只解释已有内容，按需要精确回读已授权 locator；不推进新正文。当前图表/公式确有需要时才使用 locator 绑定的原始视觉，不能借整页看后文。细节见 [Source Adapter](../../../docs/integrations/reading-mcp.md)。

## 保存与异常

自然边界、暂停、交接、范围变化或故障时写一份完整、简短的阅读状态并回读；不把逐句输出逐条写成 START/RESULT/HANDOFF。

失败时保留[未完成动作](../../../docs/learning/reading-sessions.md#已揭示与已完成)，重试界限见[返回结果处理](../../../docs/integrations/reading-mcp.md#返回结果处理)。身份或范围不确定时停止，不能换成最像的文本。未持久化进度可能丢失；无法确认分析已完成时先恢复同一单元，不猜测跳过。

原文正确性不受简化流程影响；阻塞原因未变不重复写同样记录。只在实际需要交接时换会话，不为了保持风格而定期重测。
