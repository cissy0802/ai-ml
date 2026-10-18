# 本仓自治规则（内容层：自停 · 自愈 · 英文泄漏自查）

TOPICS.md 是本仓选题的**唯一真相源**。以下三条每次运行都适用；trigger 的启用/停用由外部 `verify-routine-caps` 守卫按 N_pub vs N_top 统一管，**你不要去改 trigger**。

## 1. 自停（写完 TOPICS 就不再生成）
运行开头先算：
- `N_pub` = 已发布页最高编号：`ls *-day*.html`（或本仓命名 week/issue/book/topic）去 `.en.html`、去前导零取最大。
- `N_top` = TOPICS.md 最大编号：`grep '^[-*#]* *(Day|Week|Issue|Book|Topic) *[0-9]+'` 取最大。

**若 N_pub ≥ N_top（TOPICS 已全部写完）**：本次**不生成任何页面、不修改 TOPICS.md、绝不自己发明新主题**；直接结束（至多发一条『本站已写完 TOPICS 路线图，补充新主题后自动续写』的通知，且仅在你判断这是刚写完的当次时发，不要每次都发）。**这条优先级高于本仓 routine prompt 里任何"超表就自造新主题"的旧措辞。** 新主题只由 BigCat 手动或 deep-research 反哺加进 TOPICS.md；加了之后守卫会自动重开、routine 自然续写。

## 2. 自愈（保持 TOPICS ⊇ 已发布）
**只在越界时动手**：若本期 Day/编号按 TOPICS 计划写、TOPICS 里本就有这行 → 不动。只有当你发布的编号是 **TOPICS.md 里没有的**（用户手动指定主题、或 deep-research 反哺内容，当时漏记进 TOPICS）时：
1. 用本期页面标题/副标题，在 TOPICS.md **末尾 append** 一行 `- Day N: <主题> — <要点>`（前缀 Day/Week/Issue/Book/Topic 随本仓约定，先 `grep` 看已有行照抄）。
2. 与本期内容改动**一并 commit / push 到 main**。
3. **只 append，绝不修改已有行。** 否则越界页占了 `dayN`、TOPICS 缺行，日后往 TOPICS 补的 Day N 新主题会撞车永远写不出。

## 3. 英文页中文泄漏自查
生成 `*.en.html` 后、publish 前，对它 grep 这些指纹（命中=模板槽把中文漏进了英文页）：
`class="en">[一-鿿]` / `class="name-en">[一-鿿]` / `class="name-zh">[一-鿿]` / `class="cn">[一-鿿]` / `Reflections — [一-鿿]` / `class="lang-tag">ZH`
命中就修掉（删中文节点或译成英文）再 publish。**正常情况不算泄漏**：经文/古典原典+英译、孙子兵法原文+英译、term(中文) 括注、代码/分词演示、语言切换标签『中文』、主题本身是中文的页。

## 新页面必带共享脚本（免触发 inject-comments 机器人提交）

生成任何 `*.html`（含 `.en.html`）时，在 `</body>` 前直接写入这 4 行，勿遗漏：

```html
<script src="https://hub.cissychen.com/comments.js" defer></script>
<script src="https://hub.cissychen.com/search.js" defer></script>
<script src="https://hub.cissychen.com/index-button.js" defer></script>
<script src="https://hub.cissychen.com/i18n-tts.js" defer></script>
```

这样 CI 的 inject-comments 不会再对新页面追加自动提交。

## 4. 文末两节：越界 · 十条要点（2026-10-17 起）

页面结构（云端 routine prompt 里的写作规范照旧）之外，**2026-10-17 起每期中英两页都加下面两节**，与 routine prompt 有冲突时以本节为准。位置：**最后一个概念 card 之后、「深入资源」card 之前**（顺序：概念 card… → 越界 → 十条要点 → 深入资源 → 深入思考）。两节都照本仓收尾节的样式包成 `<div class="card">` + `<h2>`。

1. **越界 · 跨学科的联想**（2026-10-17 起，必写，3–5 条）：写本期某个 AI/ML 想法和另一个领域的什么东西是同一个结构，一两句说清像在哪、不像在哪。**每条约 60–90 字**，只有展开的那 1 条可到约 120 字。优先挂读者的深度兴趣：意识、佛学、量子力学、神经科学、东西方哲学、心理学、生物进化、复杂性科学、分布式系统；旁支领导力、投资、商业。**别挂回 AI/ML 本身**（另一种模型、另一篇 ML 论文都不算越界）。提到的具体研究、人物、年份必须真实准确，拿不准就换一条。
   - **不与节内内容重复**：每个概念 card 里的「一句话类比」是讲解用的工程类比，「深入思考」里也常有跨领域的问答；越界框收拢成 3–5 条，**不复述这两处已经写过的类比**，要换一个领域或换一层结构。
   - 本期引用的论文/作者自己点名借用的东西（如论文作者自己借用的类比）属于正文；**我们自己联想到的只进越界**，读者要分得清哪些是原文说的、哪些是我们加的。
   ```html
   <div class="card" style="border-left-color:#a48cff">
   <h2>越界 · 跨学科的联想<span class="en">Crossovers</span></h2>
   <div class="crossx"><ul>
   <li><b>学科 · 概念/人物</b>：像在哪、不像在哪，一两句。</li>
   </ul></div>
   </div>
   ```
   英文页 h2 写 `Crossovers`（不带 span）。
2. **十条要点**（2026-10-17 起，必写，**正好 10 条**）：读者拿它直接记笔记。每条一句完整的话，约 20–45 字，**单独抄出去也能看懂**：写出概念名、方法名，不用「它」「这个指标」这类要靠上下文的代词。**人名不必每条都当主语开头**：全组里主角（论文作者、机构）的名字出现两三次就够，其余各条直接写观点、机制或事实。覆盖各概念 card 最值得记的定义、机制和误区，可含越界里的一两条；顺序跟正文走。**只总结正文已经写过的东西**，不加新信息，不放引语。注意它和每个 card 末尾的 `.takeaway`（单数，单节小结）是两回事：类名是 `takeaways`，别混用。
   ```html
   <div class="card">
   <h2>十条要点<span class="en">Ten takeaways</span></h2>
   <ol class="takeaways">
   <li>…</li>
   </ol>
   </div>
   ```
   英文页 h2 写 `Ten takeaways`（不带 span）。
3. **CSS**：上一期页面的 `<style>` 里若还没有下面这段，照抄上期样式后**把它追加到 `<style>` 末尾、`@media` 之前**（中英两页都要）：
   ```css
   .crossx ul{list-style:none;margin:6px 0 0;padding:0}
   .crossx li{margin:12px 0;padding-left:14px;border-left:2px solid rgba(123,97,255,0.45);color:#cfd3df;font-size:0.95rem}
   .crossx b{color:#a48cff}
   .takeaways{counter-reset:tk;list-style:none;margin:6px 0 0;padding:0;border:1px solid rgba(0,212,255,0.28);border-radius:12px;background:rgba(0,212,255,0.04)}
   .takeaways li{counter-increment:tk;position:relative;margin:0;padding:11px 18px 11px 52px;border-top:1px solid rgba(0,212,255,0.12);font-size:0.93rem;line-height:1.75;color:#cfd3df}
   .takeaways li:first-child{border-top:none}
   .takeaways li::before{content:counter(tk,decimal-leading-zero);position:absolute;left:18px;top:12px;font-family:"SF Mono",Menlo,monospace;font-size:0.78rem;color:#00d4ff}
   ```
4. **篇幅**：越界约 400 字、十条要点约 350 字。`.maxchars`（中文页汉字上限）已为这两节从 5000 上调到 5750（2026-10-17）；概念 card 的篇幅不跟着涨。
5. **闸门**：`publish.sh` 对从未提交过的新页（中英都查）卡：`<ol class="takeaways">` 正好 10 个 `<li>`，`<div class="crossx">` 3–5 个 `<li>`。不过就补齐/删减再 publish。
