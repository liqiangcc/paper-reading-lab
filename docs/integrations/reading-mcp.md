# reading-mcp 集成

本文件是按需查阅的工具边界，不是每句阅读的额外前置流程。正式执行步骤只在 [Reading Skill](../../.agents/skills/source-first-reading/SKILL.md) 定义。

## 身份

保留 `paper_id / revision_id` 与 provider 的 `document_id / content_hash / normalized_document_hash / segmentation_version` 绑定。provider document id 不能替代论文版本，旧 hash/locator 不能静默套用新 normalization。

使用原阅读会话保有的身份；只在需要打开来源或身份核验时调用相应工具，不在每一句枚举所有工具或单独做健康探针。实际成功调用才是可用性证据。精确回读用于当前单元和原会话内回看，不提供跨会话上下文重建。

## 范围与读取

named-section 边界优先取不含正文的结构层级或绑定当前 identity 的预验证边界。不能为了确定停止点搜索尚未揭示正文；边界不明先停。

顺序阅读默认 `get_text_units(requested_kind=sentence, direction=forward, coverage_policy=preserve_source, max_items=1)`，使用当前 document、允许的 owner/section 和精确 anchor。

对返回单元调用 `read_document(document_id, target_locator)`，不要同时传 `section_id`。核对 resolved identity、范围、完整性与截断状态；不能因显示句号编号相同就视作一致。

一个 canonical unit 可以包含多个表面句子，也可能是 fragment/paragraph/heading/caption。保留实际 kind 和顺序，不自造新 identity；结构单元也消耗当前一次读取，除非已有 scope 明确允许进一步过滤。

## 返回结果处理

枚举的 `complete / section_complete` 描述流与章节状态，不能直接当作某条正文已完整回读的证据；`max_items=1` 也不保证必有一条结果。

`get_text_units.complete=true` 表示本次遍历已到达指定方向的 section 边界，包括从 anchor 开始的续读。`section_complete` 只对从 section 边界开始、覆盖完整的遍历成立；anchor 及其 cursor 续页即使到达节末也会返回 `section_complete=false`。`coverage` 统计整个声明流的源内容表示情况，不证明本会话已经读过 anchor 或其前文。

对默认 forward / preserve_source 读取，在身份、owner/section、kind、policy 与请求一致的前提下，使用以下信号确认节末，不要求 `section_complete=true`：

```text
complete == true
next_cursor == null
stream.direction == forward
stream.end_index == stream.total_items
coverage.source_complete == true
coverage.unsupported_gaps == 0
```

这仅确认流的前向边界。声称整节已读完还需原阅读会话中同一 identity 下的连续阅读记录，且 anchor 和所有已返回单元的回读、分析均已完成；记录缺失不得从 Issue 重建。切换下一 section 仍须 scope 授权，不用读取下一 section 正文探测边界。backward 的 `complete=true / start_index=0` 只确认节首；`eligible_only` 耗尽也不证明完整源覆盖。空结果本身不能证明结束。

| 结果 | 动作 |
| --- | --- |
| 返回一个单元 | 核对身份及范围，记录已暴露单元与待完成动作，再精确回读。同一响应即使报告 complete 或 section_complete，也先完成这个单元的分析；完成后等待用户，不自动跨节。 |
| 无单元且满足上述节末信号（包括 section_complete=false 的 anchor 续读） | 确认当前 section 流已枚举到末尾，不因 section_complete=false 重试或阻塞。结合本会话连续阅读记录判断整节是否读完，不宣称整篇读完。下一 section 仍检查授权，且本次不自动跨节读取。 |
| 无单元且未确认结束，或 coverage 有缺口 | 保留锚点及不完整事实，不把空结果解释为结束，不切 section 或用搜索补文；待原因明确后在原会话重试。 |
| 返回多于一个单元或越界内容 | 记录全部实际暴露范围并停止；不挑一条后声称 exactly-one 或无污染。 |
| 精确回读截断 / complete=false | 保留同一 target locator，下一动作仍是补全该目标；不能使用枚举 next_cursor 推进新单元。 |

截断时可按当前工具契约，在同一 document、身份和 target 内增大 `max_chars` 重读，或使用明确绑定该目标的 read cursor 连续补全；每块核对范围、顺序和覆盖，完整后才分析。无有效 continuation、连续两次无覆盖进展或同一故障重复时，保存待完成动作并停止重试。identity mismatch / stale 立即停止，不适用自动重试。回读成功但输出中断时按[未完成单元规则](../learning/reading-sessions.md#已揭示与已完成)恢复分析。

## 异常

`STALE_LOCATOR / STALE_CURSOR / identity mismatch` 停止精确续作；不拿旧文本做 fuzzy search。原文缺失不使用模型记忆、旧 Issue 解释或 Web 替代。

枚举已经返回文字后，即使精确回读失败，也要保留实际暴露范围；不谎称零揭示。工具或写入失败时记录能确认的事实，原会话重试不猜测跳过单元。

`search_document` 不得用于获取未来正文、帮助预测或模糊恢复；它不是默认顺序阅读工具。需要外部/跨版本调查时先单独获授权。

## 原始视觉

当前允许内容确需图、表、公式或布局核对时，使用 locator 绑定的原始 source view。区分原始视觉观察、提取文字与 AI 解释，不用 OCR/重绘冒充原页。

优先使用可限制到当前目标的视图；若工具只能暴露带未读内容的整页且无法满足当前边界，先说明限制，不先取整页再声称“没有用后文”。意外暴露必须记录；不能假装忘记。

调用 source view 前，必须从工具契约或已核验能力确定返回范围能被限制到当前已授权、已揭示内容；仅传入精确 locator 不证明返回的是裁剪视图。范围未知时不调用；纯文字单元继续使用精确文字回读，确需视觉而无法限制范围时保留阻塞。不得先获取整页再裁剪，因为获取时后文已经进入上下文。

工具调用成功、locator 精确匹配、未提前暴露后文是三个独立结论。污染记录需随后续状态保留，精确回读成功不将其清除。这是 Agent 调用前约束；本仓库没有拦截外部 MCP 请求的运行时，离线 CI 不证明该约束已执行。

本仓库不重新实现 parser 或句子索引，也不固定 live Tool 数量。保留不影响当前阅读的已知限制，不能把一个样本成功宣称成全文正确。
