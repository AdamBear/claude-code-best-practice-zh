# Code Review 与 Test Time Compute：来自 Boris Cherny 的技巧

这是 Boris Cherny（[@bcherny](https://x.com/bcherny)），Claude Code 的创造者，于 2026 年 3 月 10 日分享的洞见摘要。

<table width="100%">
<tr>
<td><a href="../">← 返回 Claude Code Best Practice</a></td>
<td align="right"><img src="../!/claude-jumping.svg" alt="Claude" width="60" /></td>
</tr>
</table>

---

## 1/ 介绍 Code Review

Claude Code 的新功能：**Code Review**。一组代理会对每个 PR 进行深度审查。

- 这个功能最初是为 Anthropic 自己的团队打造的：今年每位工程师的代码产出提高了 **200%**，而审查已经成为主要瓶颈
- Boris 已经用了几周，发现它能抓到很多他原本不会注意到的真实 bug
- 当一个 PR 打开时，Claude 会派出一组代理去集中“猎杀” bug

<a href="https://x.com/bcherny/status/2031089411820228645"><img src="assets/boris-10-mar-26/0.png" alt="Boris Cherny 宣布 Code Review" width="50%" /></a>

---

## 2/ Test Time Compute 与多个上下文窗口

粗略地说，你往一个编程问题上投入的 token 越多，结果通常就越好。Boris 把这叫作 **test time compute**。

- 使用**彼此独立的上下文窗口**，结果会更进一步提升。这正是子代理发挥作用的原因，也是为什么一个代理会引入 bug，而另一个代理即使用的是完全相同的模型，也可能把 bug 找出来
- 这和工程团队很像：如果 Boris 自己写出了一个 bug，那么同事来审查代码时，往往比他本人更容易发现问题
- 从极限来看，代理最终也许会写出完美、无 bug 的代码；但在那之前，**多个彼此不相关的上下文窗口**仍然是一种很好的策略

<a href="https://x.com/bcherny/status/2031151689219321886"><img src="assets/boris-10-mar-26/1.png" alt="Boris Cherny 谈 test time compute" width="50%" /></a>

---

## 来源

- [Boris Cherny (@bcherny) on X — March 10, 2026](https://x.com/bcherny)
