# 输出版式示范（虚构）

这是[分析协议](../source-first-sentence-reading.md#从学习目标出发让分析方法可见)中“从学习目标出发”一节的呈现参照，示范三档输出、编号点展开顺序、依据类型、问题账本、本句分析动作和一行停点。全部材料是自包含的虚构设定，不是任何论文的原文或已揭示前文，不能用来补任何 Paper 的事实。示范不规定固定标题、字数或图数；实际输出按当前单元的作用取舍。

## 已给出的虚构前文

以下五个单元视为本会话已揭示、已分析：

- ¶1 s1：Readers at the city library place holds on books that are currently checked out.（读者可以预约当前已借出的书。）
- ¶1 s2：Today, a librarian checks returned books against a printed hold list once every evening.（目前，馆员每天晚上对照纸质预约单核对一次归还的书。）
- ¶1 s3：Readers report that held books often sit on the return cart for a full day before they are notified.（读者反映，被预约的书常在还书车上放一整天才通知到人。）
- ¶2 s1：We built Shelf, a system that matches each returned book against open holds at the moment it is scanned.（我们构建了 Shelf：每本书归还扫描时，立即与未完成的预约匹配。）
- ¶2 s2：In a two-week trial at one branch, the median time from return to notification fell from 19 hours to 4 minutes.（在一个分馆为期两周的试运行中，从归还到通知的中位时间从 19 小时降到 4 分钟。）

## 示例一：过渡档

**虚构 · ¶2 · s3**

> The rest of this note describes the matching rule and its limits.

本文其余部分说明匹配规则及其局限。

过渡句，预告后文的两部分：规则和局限。本身没有论证。

`虚构 · ¶2 · s3 · sentence · exact-read complete`

## 示例二：普通档

**虚构 · ¶3 · s1**

> However, matching at scan time tends to fail for books whose barcodes are damaged.

然而，对于条码受损的书，扫描时匹配往往会失败。

**一句总判断：** 上一单元预告了“局限”，这一句给出第一条：扫描时匹配依赖条码可读。

**1. 线索 “However” → 这句话否定了 ¶2 s2 的试运行结果吗？**

- 依据：¶2 s2（中位通知时间从 19 小时降到 4 分钟）说的是中位数；本句说的是条码受损的书。
- 结论〔推论〕：中位数只反映排在中间的那本书。只要条码受损的书是少数，它们匹配失败不会改变中位数。两句能同时成立，条件是受损的书不超过一半；原文没有给出比例，这个条件目前待检验。

```text
¶2 s2   全部归还的书 → 中位通知时间 4 分钟    〔实验：一个分馆，两周〕
¶3 s1   其中条码受损的书 → 扫描匹配往往失败   〔主张〕
        两者同时成立的条件：受损的书是少数    〔推论，比例未给出〕
```

**2. 线索 “tends to” → 失败有多确定？**

- 依据：“tends to”表示倾向。
- 结论：说的是“往往失败”，不是“一定失败”。后面的推理不能把它当成“受损的书都匹配不上”。

**问题账本**

- 新开：匹配失败的书之后怎么处理？
- 待检验：〔推论〕条码受损的书只占少数。

**本句分析动作：用统计量的含义化解冲突。** 一个整体指标和一个局部失败看似矛盾时，先问这个指标对少数情况是否敏感（中位数不敏感，平均值敏感〔背景〕），再判断两者是否真的冲突。

`虚构 · ¶3 · s1 · sentence · exact-read complete`

## 示例三：关键档

**虚构 · ¶3 · s2**

> Because a damaged barcode is re-scanned by hand at the evening check, those books still reach readers within a day, so Shelf never makes notification slower than the old process.

由于条码受损的书会在晚间核对时由人工重新扫描，这些书仍能在一天内通知到读者，因此 Shelf 绝不会使通知比旧流程更慢。

**一句总判断：** 这一句回答了上一句留下的问题（匹配失败的书怎么办），并把它与旧流程接起来，得出一个全称结论：Shelf 不会比旧流程更慢。前面分散的几个节点在这里闭合。

**1. 线索 “Because … so” → 从“一天内通知”到“绝不会更慢”，中间缺什么？**

先只看本句自身的推理：

```text
条码受损 → 晚间核对时人工重扫 → 一天内通知
                                    │ 隐含前提：上线 Shelf 后，晚间核对仍然保留
                                    ▼
                    最坏情况与旧流程相同 → “绝不会更慢”
```

- 依据：¶1 s2（旧流程是每晚核对一次）。原文没有说上线 Shelf 后晚间核对是否还在。
- 结论〔推论〕：结论成立需要一个原文没写出的前提：晚间核对在 Shelf 上线后仍然保留。若晚间核对被取消，受损的书就没有补救路径，“绝不会更慢”不再成立。

**2. 线索 “never” → 全称结论覆盖所有书，要逐类检查**

- 依据：¶2 s1（扫描时立即匹配）；本句（失败的书晚间人工重扫）。
- 结论：分两类看。扫描匹配成功的书比晚间核对快；扫描匹配失败的书与旧流程相同。两类都不比旧流程慢，全称结论才成立。

¶3 s1 说受损的书“往往”匹配失败，本句处理的正是失败的那部分；匹配成功的受损书归入第一类，结论不受影响。限定词“往往”在这里仍按原强度处理。

**3. 最后把整条链连起来**

```text
问题     ¶1 s3  被预约的书常放一整天才通知        〔经验：读者反映〕
旧流程   ¶1 s2  每晚对照纸质预约单核对一次
新机制   ¶2 s1  归还扫描时立即匹配
效果     ¶2 s2  中位通知时间 19 小时 → 4 分钟      〔实验：一个分馆，两周〕
局限     ¶3 s1  条码受损的书往往匹配失败          〔主张〕
补救     ¶3 s2  晚间人工重扫，一天内通知
结论     ¶3 s2  不会比旧流程更慢                  〔主张，依赖隐含前提〕
```

每一行建立在上一行之上：先有问题和旧流程，再有新机制和效果，然后是局限和补救，最后得出结论。

**问题账本**

- 本句回答：¶3 s1 留下的“匹配失败的书怎么处理”。
- 新开：晚间核对在 Shelf 上线后是否保留（结论依赖它）。
- 仍待检验：〔推论〕条码受损的书只占少数（¶3 s1）。

**本句分析动作：检查全称结论的成立条件。** 遇到“绝不”“总是”一类结论，先把对象分成几类逐一检查，再找出推理中没写出的前提；前提不成立，结论就不成立。

`虚构 · ¶3 · s2 · sentence · exact-read complete`

## 对照时看什么

- 三个示例长度不同，由单元作用决定：过渡档三行，关键档完整展开。
- 每个编号点都从原文线索开始，先问后答；读者能看出结论由哪个词触发、依据是哪条前文。
- 引用前文时都带短语，读者不需要回翻。
- 示例二的“tends to”在示例三中仍按“往往”处理，没有升级为“一定”。
- 依据类型只标在需要区分的地方，不逐行铺满。
- 问题账本让示例二留下的问题在示例三得到回答，并把新的前提缺口交给后文。

实际阅读中的停点必须使用工具返回的真实 locator，并按协议写出 Section / Page、paragraph、sentence、normalized_range、effective_kind、degradation 与 exact re-read 状态；不照抄示范中的虚构位置。
