# 输出版式示范（虚构）

这是[分析协议](../source-first-sentence-reading.md#从学习目标出发让推理一步步可跟随)中“从学习目标出发”一节的呈现参照：标题行、开头（位置与上一句的关系）、“原文短语：洞见”的小标题、ASCII 树或流程图、就地写出的边界、必要时的“现在回头看”、这一句真正新增的核心信息、分组的 Known / Unknown、一个问题，以及结尾的停止语和停点。全部材料是自包含的虚构设定，不是任何论文的原文或已揭示前文，不能用来补任何 Paper 的事实。示范不规定固定节数、字数或图数；实际输出按当前单元的分量取舍。

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

上一单元刚刚预告，后文要讲“规则和局限”。现在作者马上给出第一条局限：

```text
Shelf：归还扫描时立即匹配预约
   ↓ However
条码受损的书：扫描匹配往往失败
```

⸻

**1. However 不是在否定试运行结果，而是在缩小它的适用范围**

最容易产生的误读是：

```text
❌ 扫描匹配会失败 → ¶2 s2 的“19 小时降到 4 分钟”不可信
```

但 ¶2 s2 报告的是中位数：

```text
中位数只由排在中间的那本书决定
   ↓
条码受损的书如果是少数，它们失败不会改变中位数
   ↓
✓ 两句可以同时成立：整体中位数大幅下降，少数受损的书仍会失败
```

这里要就地守住：“受损的书是少数”是两句能同时成立的条件，原文没有给出比例。如果受损的书超过一半，两句才真正冲突。

⸻

**2. tends to：是“往往失败”，不是“一定失败”**

```text
tends to fail
   ↓
多数受损的书匹配失败，少数仍可能成功
```

后面的推理要一直按“往往”处理。

⸻

**这一句真正新增的**

```text
Shelf 的机制有了第一条边界：依赖条码可读
```

**当前 Known / Unknown**

```text
Known
  旧流程：每晚核对一次                        ¶1 s2
  新机制：归还扫描时立即匹配                  ¶2 s1
  效果：中位通知时间 19 小时 → 4 分钟          ¶2 s2（一个分馆，两周）
  局限一：条码受损的书，扫描匹配往往失败      ¶3 s1  ← 本句

Unknown
  条码受损的书占多少？（决定两句是否冲突）    ← 本句新出现
  匹配失败的书之后怎么处理？                  ← 本句新出现
```

**现在最值得继续追的问题：** 匹配失败的书，最后还能不能通知到读者？

`虚构 · ¶3 · s1 · sentence · exact-read complete`

## 示例三：关键单元

**虚构 · ¶3 · s2**

> Because a damaged barcode is re-scanned by hand at the evening check, those books still reach readers within a day, so Shelf never makes notification slower than the old process.

由于条码受损的书会在晚间核对时由人工重新扫描，这些书仍能在一天内通知到读者，因此 Shelf 绝不会使通知比旧流程更慢。

上一句刚刚留下一个问题：匹配失败的书怎么办？现在作者马上回答，并由此推出一个更强的结论：

```text
条码受损 → 晚间核对时人工重扫 → 一天内通知
   ↓ so
Shelf 绝不会比旧流程更慢
```

⸻

**1. Because … so：从“一天内通知”到“绝不会更慢”，中间还缺一个前提**

```text
受损的书在晚间核对时重扫
   ↓
一天内通知，与 ¶1 s2 的旧流程（每晚核对一次）一样
   ↓ 隐含前提：上线 Shelf 后，晚间核对仍然保留
最坏情况不慢于旧流程
```

原文没有说晚间核对是否保留。如果它被取消，受损的书就没有补救路径，结论不再成立。

⸻

**2. never：全称结论要逐类检查**

```text
❌ 只看受损的书，就断定“绝不会更慢”

✓ 把所有归还的书分成两类，逐类检查：
   扫描匹配成功 → 当场通知（¶2 s1）    → 比旧流程快
   扫描匹配失败 → 晚间重扫（本句）      → 与旧流程相同
   ↓
两类都不慢 → “绝不会更慢”在这两类上成立
```

¶3 s1 说的是受损的书“往往”失败；匹配成功的受损书归入第一类，结论不受影响。

⸻

**3. 现在回头看 Shelf 的效果，理解要升级**

之前（¶2 s2）我们理解为：

```text
Shelf 让通知变快了（中位数）
```

现在升级为：

```text
多数书：通知大幅变快
少数受损的书：与旧流程相同
任何书：都不比旧流程慢（前提是晚间核对仍保留）
```

⸻

**4. 整条论证到这里闭合**

```text
问题     被预约的书常放一整天才通知       ¶1 s3（读者反映）
旧流程   每晚核对一次                     ¶1 s2
新机制   扫描时立即匹配                   ¶2 s1
效果     中位通知 19 小时 → 4 分钟         ¶2 s2（一个分馆，两周）
局限     条码受损往往匹配失败             ¶3 s1
补救     晚间人工重扫，一天内通知         ¶3 s2
结论     不会比旧流程更慢                 ¶3 s2（前提：晚间核对保留）
```

⸻

**这一句真正新增的**

```text
Shelf 的承诺从“通常更快”扩展为“不会更慢”
   ↓
但这个承诺依赖一个原文没写出的前提：晚间核对仍保留
```

遇到“绝不”“总是”这类全称结论，先分类逐一检查，再找推理中没写出的前提。

**当前 Known / Unknown**

```text
Known
  （前四条同上一句）
  补救：受损的书晚间人工重扫，一天内通知      ¶3 s2  ← 本句
  结论：Shelf 不会比旧流程更慢                ¶3 s2  ← 本句

  ✓ 本句解决：匹配失败的书怎么处理（¶3 s1 留下）

Unknown
  晚间核对在 Shelf 上线后是否保留？（结论依赖它）   ← 本句新出现
  条码受损的书占多少？                              （¶3 s1 留下，仍未解决）
```

**现在最值得继续追的问题：** 晚间核对在 Shelf 上线后是否保留？

`虚构 · ¶3 · s2 · sentence · exact-read complete`

## 对照时看什么

- 开头说明这一句的位置，以及它接上了上一句的什么。
- 小标题是“原文短语：洞见”，读者不读正文也能看出抓住了哪个词。
- 图只画本节新增的关系，每张图后一句话说明它表达了什么。
- 边界写在它起作用的那一步：“原文只说……，没有说……”。
- 理解有修正时，用“现在回头看……”写出旧理解、新理解和差别。
- 同一判断只说一次；评价性形容词不用。
- 结尾先给“这一句真正新增的核心信息”，再列 Known / Unknown，最后只留一个问题，并写“到这里停止，不读取下一条正文”。

实际阅读中的停点必须使用工具返回的真实 locator，并按协议写出 Section / Page、paragraph、sentence、normalized_range、effective_kind、degradation 与 exact re-read 状态；不照抄示范中的虚构位置。
