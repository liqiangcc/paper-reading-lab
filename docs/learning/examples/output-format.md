# 输出版式示范（虚构）

这是[分析协议](../source-first-sentence-reading.md#从学习目标出发每句是一份判断的完整示范)中“从学习目标出发”一节的呈现参照：主线“读准 → 接上 → 推出 → 守住”、接入图、零摩擦写法和一行停点。全部材料是自包含的虚构设定，不是任何论文的原文或已揭示前文，不能用来补任何 Paper 的事实。示范不规定固定标题、字数或图数；实际输出按当前单元的作用取舍。

## 已给出的虚构前文

以下五个单元视为本会话已揭示、已分析：

- ¶1 s1：Readers at the city library place holds on books that are currently checked out.（读者可以预约当前已借出的书。）
- ¶1 s2：Today, a librarian checks returned books against a printed hold list once every evening.（目前，馆员每天晚上对照纸质预约单核对一次归还的书。）
- ¶1 s3：Readers report that held books often sit on the return cart for a full day before they are notified.（读者反映，被预约的书常在还书车上放一整天才通知到人。）
- ¶2 s1：We built Shelf, a system that matches each returned book against open holds at the moment it is scanned.（我们构建了 Shelf：每本书归还扫描时，立即与未完成的预约匹配。）
- ¶2 s2：In a two-week trial at one branch, the median time from return to notification fell from 19 hours to 4 minutes.（在一个分馆为期两周的试运行中，从归还到通知的中位时间从 19 小时降到 4 分钟。）

## 示例一：过渡单元

**虚构 · ¶2 · s3**

> The rest of this note describes the matching rule and its limits.

本文其余部分说明匹配规则及其局限。

导览句，预告后文分两部分：规则和局限。

`虚构 · ¶2 · s3 · sentence · exact-read complete`

## 示例二：普通单元

**虚构 · ¶3 · s1**

> However, matching at scan time tends to fail for books whose barcodes are damaged.

然而，对于条码受损的书，扫描时匹配往往会失败。

本句给出 Shelf 的第一条局限。

“扫描时匹配”就是 ¶2 s1 中归还扫描那一刻与预约比对的做法。本句说，条码受损的书在这一步往往失败；“往往”指多数情况，不是全部。

上一单元预告了“规则和局限”，本句是局限的第一条，挂在 Shelf 的新机制之下：

```text
Shelf：归还扫描时立即匹配预约
├─ 效果：中位通知时间 19 小时 → 4 分钟（一个分馆试运行两周）
└─ 局限一：条码受损的书，扫描匹配往往失败   ← 本句
       └─ 失败之后怎么办：？
```

“However”容易让人以为本句否定了试运行的效果。其实两者可以同时成立：¶2 s2 报告的是中位数，中位数只由排在中间的那本书决定；只要条码受损的书是少数，它们匹配失败不会改变中位数。

但“少数”正是这个结论成立的条件，原文尚未给出受损书的比例。如果受损的书超过一半，中位数就会受到影响，两句之间才会真正冲突。失败之后怎样处理，原文也尚未给出。

整体指标与局部失败看似矛盾时，先问这个指标对少数情况是否敏感。

`虚构 · ¶3 · s1 · sentence · exact-read complete`

## 示例三：关键单元

**虚构 · ¶3 · s2**

> Because a damaged barcode is re-scanned by hand at the evening check, those books still reach readers within a day, so Shelf never makes notification slower than the old process.

由于条码受损的书会在晚间核对时由人工重新扫描，这些书仍能在一天内通知到读者，因此 Shelf 绝不会使通知比旧流程更慢。

本句回答了上一句留下的问题，并由此得出一个全称结论：Shelf 不会比旧流程更慢。

本句分两步：先说受损的书在晚间核对时人工重扫、一天内通知；再由此得出“绝不会更慢”。“绝不”是全称，覆盖所有归还的书。

它填上了上一句留下的空位：

```text
局限一：条码受损的书，扫描匹配往往失败（¶3 s1）
└─ 失败之后：晚间核对时人工重扫，一天内通知   ← 本句
```

全称结论要逐类检查。归还的书分两类：扫描匹配成功的，按 ¶2 s1 当场通知，比旧流程快；匹配失败的，按本句晚间重扫、一天内通知，与 ¶1 s2 的旧流程（每晚核对一次）相同。两类都不慢于旧流程，由此可知，“绝不会更慢”在这两类上成立。¶3 s1 说受损的书“往往”失败，匹配成功的那部分归入第一类，结论不受影响。

这一步还依赖一个本句没有写出的前提：上线 Shelf 后，晚间核对仍然保留。如果晚间核对被取消，失败的书就没有补救路径，结论不再成立。原文尚未说明晚间核对是否保留。

到这里，前面分散的几个节点接成了一条完整论证：

```text
问题      被预约的书常放一整天才通知（¶1 s3，读者反映）
旧流程    每晚核对一次（¶1 s2）
新机制    扫描时立即匹配（¶2 s1）
效果      中位通知 19 小时 → 4 分钟（¶2 s2，一个分馆两周）
局限      条码受损往往匹配失败（¶3 s1）
补救      晚间人工重扫，一天内通知（本句）
结论      不会比旧流程更慢；前提是晚间核对仍保留
```

遇到“绝不”“总是”一类结论，先把对象分类逐一检查，再找推理中没有写出的前提。

`虚构 · ¶3 · s2 · sentence · exact-read complete`

## 对照时看什么

- 没有一个栏目标题或括号标签；主线体现在段落顺序里：先读准，再接上，然后推出，最后守住。
- 每段只走一步，段首接住上一段；术语在使用前已经解释。
- 确定程度靠固定说法表达：“本句说”“由此可知”“如果……就……”“原文尚未给出”。
- 接入图只承载关系，用“← 本句”标新增，用“？”标空位；示例二留下的“？”在示例三被填上。
- 示例二的“往往”在示例三中仍按“往往”处理，没有升级为“一定”。
- 篇幅由单元作用决定：过渡单元一行说明，关键单元最后重建整条论证链。

实际阅读中的停点必须使用工具返回的真实 locator，并按协议写出 Section / Page、paragraph、sentence、normalized_range、effective_kind、degradation 与 exact re-read 状态；不照抄示范中的虚构位置。
