# CLAUDE.md — 专业书籍精读 · chapter-deepread

这是云端 routine 的执行说明。你是引擎本身（Opus），**自主完成、不等任何人确认**。当前工作目录已挂载本仓库。

定位：每次挑**一本书里的一章**（计算机 / 软件领域的经典好书，首本 = DDIA），把这一章的核心思想、关键权衡与影响提炼出来、讲透。目标是：**读完这一页，约等于读懂了这一章——它要解决什么问题、核心概念是什么、几个关键设计怎么权衡、落到真实系统里是什么、为什么重要——读者不必再逐页啃原书。** 一本大书之所以「读不进去」，往往是每章信息密度高、又厚；你的活就是把**这一章真正该记住的那几个概念与权衡**拎出来、讲到读者真正 get、能对着面试或架构决策复述。**不是摘要、不是读书笔记、不是导读，是提纯。**

## 0. 选题 / 编号
- **从 `TOPICS.md` 顶部往下**挑第一个「slug 还没做过」的章（清单按书成簇、簇内按原书章节顺序排开，从上往下逐章做即可）。做没做看文件系统：`ls *-book*.html`，去掉 `-bookN` 后缀按 slug 判断。
- 文件名 `book{N}` 的 **N 用写作顺序的下一个编号**（现有最大 N + 1），**与 TOPICS 的章号解耦**——别用章号当 N（第 5 章不一定是 book5）。
- **绝不自我生成清单**：`TOPICS.md` 由 BigCat 人工维护，routine **只读不改**（`publish.sh` 硬卡 TOPICS.md 改动）。清单全做完就 **PushNotification** 请 BigCat 续单（加新书 / 新章）、本次不发布。
- `slug` 用 TOPICS 里给的英文短横线名（形如 `ddia-ch05-replication`），写成 `{slug}-book{N}.html`。

## 1. 写一篇单章「专业书籍精读」（核心）
写两个文件：中文 `{slug}-book{N}.html`、英文 `{slug}-book{N}.en.html`。

**每页两种模式，顶部一个 `.modebar` 药丸切换（默认落在科普版，localStorage 记住选择；见样例第 1 章的 CSS + 页尾内联切换脚本，localStorage key = `bookread-mode`）：**
- **科普版（`.mode-pop`）**：给零基础读者的**纯类比、零数学、零公式**短版（~600–900 字，5–6 节）。**深度按四层阶梯控制：① 现象（旧世界的痛）→ ② 点子（这章的核心想法）→ ③ 机制直觉（它「怎么」做到——用生活比喻讲，如 复制=「把同一份文件抄给几个人保管」、LSM=「先记流水账、事后再整理归档」、p99=「一百个人排队里第 99 慢的那个」）→ ④ 机制精确（记号 / 结构细节 / 具体协议）。科普版必须讲到 ③、绝不进 ④**（连 `O(n²)`、`w+r>n` 这类记号都不出现，只说人话）。每个概念要过「饭桌复述测试」：非技术读者听完能转述给第三人；锚不到生活经验的内容属于 ④，挪去精读版。保留**恰好一句**诚实的代价 / 局限或权衡，防营销腔，但别展开。结构参照样例第 1 章：这章讲什么（用读者熟悉的东西作锚，如「你打开淘宝、背后那套数据库」）→ 打个比方 / 先说个怪事 → 旧世界为什么难 → 核心机制直觉 → 带来了什么 / 该怎么选 → 一句话记住。末尾放 `.switch-hint` 链到精读版。这是默认视图。
- **精读版（`.mode-deep`，`hidden`）**：下面这**八节**深读，**分量压在第 4、5 节**。Glossary 小节放在精读版里。

两种模式都用 `<h2>` 分节（同样的蓝紫标题风）。八节：

1. **一句话** — 这一章的核心命题、要在读者脑里建立什么认知。
2. **坐标（一两句）** — 这章在书里的位置：属于哪一 Part、上承哪章 / 下启哪章、对应现实里哪类系统或问题。别展开、别堆客套。
3. **这章要解决什么** — 这章围绕的核心问题 / 旧世界的痛，为什么值得单独一章。讲清「不解决会怎样」。
4. **核心内容，讲透（主体）** — 把这章真正关键的**几个概念 / 机制 / 模式**拎出来，每个：**是什么 + 直觉 / 类比 + 机制（白话）+ 为什么这样设计 / 权衡在哪**。让没读过原书的人也能复述、能用。用 `<h3>` 分子节。
5. **关键权衡与选型** — 这一章的灵魂常常是 trade-off：**什么场景该选什么**。给具体系统 / 场景作锚（如 单主 vs 多主 vs 无主复制、LSM-tree vs B-tree、按范围分片 vs 按哈希分片、不同隔离级别挡住哪些异常）。诚实写每种选择的代价。
6. **为什么重要 / 落到真实系统** — 这套思想在架构决策、面试、真实系统里怎么用、对应了谁（点名真实数据库 / 中间件 / 论文，如 PostgreSQL、Cassandra、Kafka、Spanner）。
7. **易错点与争议** — 常见误解、书里点到的局限、原书写作时的时代局限、后续发展或有力的反方观点。不吹捧。
8. **要点收尾** — 把整章最该记住的揉成 6–10 条要点（问题、核心概念、机制、关键权衡、真实系统、易错点都点到）。

**不写「谁该读 / 怎么读原书 / 读完读什么」。**

## 2. 写作要求（重点）
- **篇幅：中文 3000–4500 字，宁精炼勿注水。** 一章覆盖面比单篇论文广，略放宽，但讲透了就收、别为凑字重复。
- **面向零基础读者（硬规则）**：假设读者**没有该领域基础**。每篇紧接「一句话」之后放一个**独立的 Glossary 小节**（用正式 `<h2>`——中文页 `<h2>Glossary · 术语表</h2>`、英文页 `<h2>Glossary</h2>`，与其它小节并排，别嵌在一句话里；下面接 `.glossary` 虚线框裹一个 `<ul>`，见样例第 1 章），把读这一章**必须先懂、但不是这章重点**的前置概念（如 副本 / replica、分区 / 分片、事务、索引、B-tree、日志 log、吞吐 / 延迟、哈希……该章会用到的前置词）**每个用一句大白话讲清**。宁可多花两三行讲基础，也别让新手卡在一个没解释的名词上。正文里其余术语继续随名即释。
- **数学 / 记号从简、白话讲原理（硬规则）**：**不容易理解的推导或形式化定义可以省略**，但必须**用大白话把原理 / 直觉讲清楚**。需要时用行内 `<code>` 给出关键记号或式子（如 `w + r > n`、`p99`、`O(log n)`）并紧跟一句白话解释它在说什么，**不追求完整证明**。判据：读者能不能不看记号就明白「这在说什么、为什么」。
- **配图是硬要求**：凡涉及**架构、数据流、机制的空间结构 / 时序**（如复制拓扑、分区与再平衡、LSM-tree 合并、B-tree 结构、写路径、共识 / 主从切换时序、事务隔离下的读写交错、批 / 流处理管线、响应时间分布），**必须配示意图**。默认用**内联 SVG 自绘**（自包含、跟随本页配色、不依赖外链、可离线）——参照样例第 1 章里的 `<figure><svg>…</svg><figcaption>…</figcaption></figure>` 写法（`viewBox` 自适应、箭头用 `<marker>`、盒子 `<rect rx>`、高亮节点用强调蓝描边）。每张图配一句中文 / 英文 `figcaption` 说明。只有当存在**权威且授权明确**的现成图（如 Wikimedia Commons）时才用外链图，否则一律自绘。英文页的图用英文标注。
- **写作参考姊妹站 `cissy0802/system-design`（硬规则）**：动笔前先读它 1–2 篇同主题正文（如 `replication-day5` / `sharding-day4` / `consistency-day6`）校准手感。把它写得好的地方搬进来——**在 chapter-deepread 的八节骨架内用，别照搬它自己的章节结构**（它的「问题场景→高层架构→关键技术点→面试问题」是它的骨架，我们仍用八节 + 双模式）。要学的写法：
  - **用具体场景 + 真实数字锚定**：讲一个机制别停在抽象定义，落到一个真实系统 / 设计场景，给**具体数字**（QPS、读写比、P99 延迟、容量、RPO/RTO 之类）——尤其 §3「这章要解决什么」、§5「关键权衡与选型」、§6「落到真实系统」。system-design 开篇就摆一个带 SLA 约束的场景，我们至少要有这种「拿真实系统当锚」的密度。
  - **反直觉的一句话钩子**：小标题 / §1 一句话 / 小节起手用「你以为 X，其实 Y」式的重构（如它的「复制——你以为是为了读扩展，其实是为了那一次故障」「一致性你以为是 0 或 1，其实是渐变光谱」）。一句话点破，比平铺直叙好记。
  - **权衡用表格**：§5 里「什么场景选什么」尽量落成一张对比表（`<table>`，跟随本页蓝紫配色），每种选择诚实标出代价，而不是只用段落讲。
  - **面试 / 复述导向**：§7「易错点与争议」、§8「要点」往「能对着面试或架构评审复述」使劲——点名真实系统的具体坑、常见误解、反直觉结论。
  - **诚实给具体数字**：宁可给一个保守但具体的量级，也别泛泛说「很快 / 很大」。（仍守 §2 的「严禁编造」：数字拿不准就讲保守、忠于原书。）
- **有公开实证就引大厂的原话（硬规则）**：若书里的某个设计 / 权衡，被知名公司用**公开可查的文字**证明有效或无效（工程博客、公开演讲、论文、事后复盘 postmortem），就把**该公司自己的主张**引进来，注明出处（公司 + 场合 / 年份），作为「落到真实系统」的实证——正反都要（谁验证了它、谁踩坑放弃了它）。例：Amazon 在 Dynamo 论文（SOSP 2007）主张按 <code>p99.9</code> 而非平均定 SLA；Google 的《The Tail at Scale》（CACM 2013）量化尾延迟放大并提出对冲请求；Netflix 用 Chaos Monkey（2011 起）在生产注入故障。**只引真实、公开、可核实的原话，绝不杜撰、绝不替公司发言**；拿不准出处就别写、或只说「业界普遍」。可用样例第 1 章的 `.ev`「大厂实证」框承载（§6「落到真实系统」里最合适）。出处尽量附**可点链接**（`.src` 里 `<a target="_blank" rel="noopener">`），优先官方 / 权威原始来源（工程博客原文、论文官方页 / 作者主页 PDF、会议录像页），**链接放上去前务必先验证可达、且确实指向该来源**，拿不准就只留文字出处、别放死链或臆测的 URL。
- **版式向 system-design / cs-papers 姊妹站看齐**：无衬线字体（`-apple-system` / SF Pro / Noto Sans SC）、渐变标题、等宽字体（mono）做小标签与元信息、玻璃拟态卡片——**直接复用样例第 1 章的内联 `<style>` 块**。
- **配色是本站专属的蓝 / 紫**（blue `#5b9df9` → violet `#9b6cf5` 渐变，冷暗底 `#0f1216`，强调字 `#8fbaff`）——**别改成琥珀**（那是 cs-papers 论文站的）、**别改成青绿**（system-design 站的）。复用样例第 1 章的 style。
- **localStorage key 用 `bookread-mode`**（不是 `cspapers-mode`）——所有姊妹站同源 `cissy0802.github.io`、共享 localStorage，key 必须独立，否则模式选择会跟论文站互相覆盖。
- **真实准确、严禁编造**：不杜撰系统名 / 数字 / 协议细节 / 书中并未有的论断；把机制和权衡讲对——这是技术站的生命线。拿不准就讲保守。批评 / 局限诚实写。**忠于原书**：概念、结论、例子要与 DDIA 原章一致，不把别处的观点安到书里。
- **中英双语，两版都地道**：split 模式，`{slug}-book{N}.html` + `.en.html` 各自独立成页、langbar 互链。**英文页除 langbar 的「中文 →」外不得出现汉字**（含 SVG 里的标注）。
- **中文页术语首次出现补英文**：`中文术语（English）`，如 复制（replication）、分区（partitioning）、线性一致性（linearizability）。缩写 / 英文名（LSM-tree、ACID、CAP、MVCC、Raft）照原样。
- **术语随名即释（硬规则）**：引入任何概念 / 机制 / 缩写，必须当场一句话说清它**是什么、在做什么**。判据：没读过原书的工程师读完这句能不能复述？不能就补或删。别 name-drop。
- **重点加粗**，克制。

## 2.5 交叉引用姊妹站（硬规则 · 全仓适用）

两个姊妹站和本仓高度互补——本仓按**书**走，它们分别按**主题**和按**论文**走。一章里讲到的机制或引到的论文，只要那边有一篇专门讲透，就把读者送过去。

- **system-design**（`https://hub.cissychen.com/system-design/`）— 54 篇主题制长文，对应**机制 / 概念**。
- **cs-papers-deepread**（`https://hub.cissychen.com/cs-papers-deepread/`）— 58 篇论文精读，对应**原书引用的论文**。书里点名一篇论文而那边正好有精读，是最该链的情形。

**什么时候链**：读者读到这个概念会想「我要再深一层」，而那篇正好接得住——才链。**同主题 ≠ 该链**，泛泛相关一律不链。宁缺勿滥。

**数量与位置**
- 每章 **最多 3 条**；同一篇 system-design 页面在一章里只出现一次。
- 放在**讲到该概念的那个小节末尾**（§4 的某个 `<h3>` 子节、§5 关键权衡、§6 落到真实系统），不要堆在页尾。
- **只放在精读版（`.mode-deep`）里。科普版（`.mode-pop`）不放**——那是给零基础读者的短版，外链是干扰。

**URL**
- 中文页：`https://hub.cissychen.com/{仓名}/{文件名}`
- 英文页：同名的 `.en.html`（两个姊妹站每篇都有），如 `…/system-design/rate-limiting-day10.en.html`
- 一律 `target="_blank" rel="noopener"`。**别写 `system-design-bidaily`**——那是旧仓名，现在 404。（`cissy0802.github.io/{仓名}/` 也通，但统一用 `hub.cissychen.com`。）

**HTML 形态（关乎 TTS，最硬的一条）**

必须用 `<aside class="xref">`，内部**只能有纯文本和行内标签**（`<a>` / `<strong>` / `<span>`）：

```html
<aside class="xref"><a href="https://hub.cissychen.com/system-design/rate-limiting-day10.html" target="_blank" rel="noopener">System Design · Day 10 Rate Limiting</a> — 令牌桶 vs 漏桶、滑动窗口的边界误差，以及分布式限流下的时钟与竞态</aside>
```

**绝不能用 `<div>` 包，内部绝不能出现 `<p>` / `<div>` / `<li>`。** 这三个标签在 `bake-tts.py` 的 `NARRATION_TAGS` 里，会被当成正文朗读 → 所在 `<h2>` 段的 hash 变化 → CI 重烘一条新 mp3、旧的变成 R2 孤儿（等周日的 prune job 清）。`aside` 不在 `NARRATION_TAGS` 里，其中的行内标签也收不到，所以完全隐形。

实测（`ddia-ch01`，19 段，`python3 bake-tts.py <file> --dry-run`）：

| 写法 | 结果 |
| --- | --- |
| `<aside class="xref">` + 纯文本 + `<a>` | 19/19 `skipped_existing`，零重烘 ✅ |
| `<aside>` 内含 `<strong>` / `<span>` | 19/19 `skipped_existing`，零重烘 ✅ |
| `<aside>` 内含 `<p>` | 该段重烘 ❌ |
| `<div class="xref">` | 该段重烘 ❌ |

**CSS**（加在复用的内联 `<style>` 末尾；英文页把 `content` 换成 `"Sister site"`）：

```css
.xref{background:rgba(91,157,249,0.06);border-left:3px solid #5b9df9;border-radius:8px;padding:11px 15px;margin:16px 0;font-size:0.93rem;color:#b9c2cf;display:block}
.xref::before{content:"姊妹站延伸";display:block;font-family:"SF Mono",Menlo,monospace;font-size:0.78rem;color:#5b9df9;letter-spacing:0.5px;font-weight:700;margin-bottom:5px}
.xref a{color:#8fbaff;font-weight:600;text-decoration:none;border-bottom:1px solid rgba(143,186,255,0.35)}
.xref a:hover{border-bottom-color:#8fbaff}
```

标签文字走 CSS `::before`，不进 DOM——所以它既不被朗读、也不进站内搜索索引。

**回填旧页**：只补 xref、不动正文的批量提交，走 `MSG="Backfill xref links [skip bake]" ./publish.sh`——`[skip bake]` 让 bake 工作流整个跳过（`publish.sh` 的 `MSG` 可被环境变量覆盖）。即使忘了带，只要守住上面的 `<aside>` 规则也不会产生任何新 mp3。

**TOPICS.md 里已给出对应关系的章**（行尾 `· xref: …`）直接照用——前缀 `sd:` 指 system-design 页面、`paper:` 指 cs-papers-deepread 页面，值就是不带扩展名的文件名（如 `sd:chaos-engineering-day44` → `https://hub.cissychen.com/system-design/chaos-engineering-day44.html`）。没给 xref 的章自己按下面两张表匹配。routine 的工作目录里**没有**这两个仓，**只能用表里的文件名，一个字都不要臆造**——写错就是死链。

### system-design 页面对照表（54 篇）

| 页 | 文件名 | 主题 |
| --- | --- | --- |
| Day 1 | `scalability-day1.html` | Scalability 基础 — 从单机到千万 QPS |
| Day 2 | `caching-day2.html` | 缓存 — 从浏览器到 DB 的多层穿透艺术 |
| Day 3 | `database-selection-day3.html` | 数据库选型 — 不是『SQL 还是 NoSQL』那么简单 |
| Day 4 | `sharding-day4.html` | 数据库分片 — 单机的尽头是分片，分片的尽头是后悔 |
| Day 5 | `replication-day5.html` | 复制 (Replication) — 你以为复制是为了读扩展，其实是为了那一次故障 |
| Day 6 | `consistency-day6.html` | 一致性 (Consistency) — 它不是一个开关，是一整条光谱 |
| Day 7 | `distributed-transactions-day7.html` | 分布式事务 — 别做，做了也尽量做小 |
| Day 8 | `message-queue-day8.html` | 消息队列 — 异步是解耦的代价，也是它的全部价值 |
| Day 9 | `api-design-day9.html` | API 设计 — 契约一旦公开，破坏它的代价由所有调用方承担 |
| Day 10 | `rate-limiting-day10.html` | Rate Limiting — 不只是「每秒 100 次」 |
| Day 11 | `unique-id-generation-day11.html` | 唯一 ID 生成 — 时间、随机与索引的三角博弈 |
| Day 12 | `search-system-day12.html` | 搜索系统 — 从倒排索引到语义检索 |
| Day 13 | `recommendation-system-day13.html` | 推荐系统 — 从十亿候选到二十条的漏斗 |
| Day 14 | `feed-system-day14.html` | Feed 系统 — 1 亿 DAU 关注流的 fanout 艺术 |
| Day 15 | `chat-system-day15.html` | 聊天系统 — 10 亿用户、5000 万并发长连接的实时递交 |
| Day 16 | `video-streaming-day16.html` | 视频流系统 — 2 亿 DAU 的点播，起播 2 秒、卡顿率 0.5% 以下 |
| Day 17 | `payments-day17.html` | 支付系统 — 钱不能多也不能少的工程 |
| Day 18 | `subscription-billing-day18.html` | 订阅与计费 — 把"按时间和用量收钱"做成可对账的引擎 |
| Day 19 | `geo-system-day19.html` | 地理系统 — 把球面切成格子，再在格子里找最近的人 |
| Day 20 | `data-processing-day20.html` | 计算作业系统 — 批处理与流处理的统一战争 |
| Day 21 | `observability-day21.html` | 可观测性 — 当系统挂了，你能问出『为什么』吗 |
| Day 22 | `deployment-release-day22.html` | 上线与发布 — 每天部署上百次、坏版本 5 分钟自动滚回 |
| Day 23 | `reliability-day23.html` | 可靠性 — 一个下游抖动，不让它拖垮整条链路 |
| Day 24 | `security-day24.html` | 安全基础 — 你是谁、你能做什么、密钥放哪 |
| Day 25 | `system-design-interview-day25.html` | 系统设计面试 — 45 分钟把开放题做成一场架构对话 |
| Day 26 | `capacity-estimation-day26.html` | 容量估算 — 用一张草稿纸把『这个设计扛不扛得住』算出来 |
| Day 27 | `cost-capacity-engineering-day27.html` | 成本与容量工程 — 在不破 SLO 的前提下把单位成本压下来 |
| Day 28 | `cdn-edge-day28.html` | CDN 与 Edge — 把计算和缓存推到离用户 50 公里处 |
| Day 29 | `object-storage-day29.html` | 文件存储 — 用 1.5x 空间换 11 个 9 的持久性 |
| Day 30 | `authorization-day30.html` | 权限与账号系统 — 一次 check 背后的图遍历、隔离与不可抵赖 |
| Day 31 | `hybrid-search-day31.html` | 混合检索与重排序 — BM25 与向量的多阶段拼接 |
| Day 32 | `llm-serving-day32.html` | LLM 服务架构 — 把 GPU 喂饱，把延迟压住 |
| Day 33 | `ai-product-backend-day33.html` | AI 产品后端 — RAG、Agent loop 服务化与人机协同 |
| Day 34 | `realtime-systems-day34.html` | 实时系统 — 在 100ms 内让世界保持一致 |
| Day 35 | `iot-edge-day35.html` | 物联网与边缘 — 千万设备每 10 秒一次心跳的吞吐工程 |
| Day 36 | `blockchain-day36.html` | 区块链与分布式账本 — 在无信任节点间复制一份谁也改不了的状态机 |
| Day 37 | `multi-tenant-saas-day37.html` | 多租户 SaaS 架构 — 一套系统服务一万个互不信任的租户 |
| Day 38 | `data-lakehouse-day38.html` | 数据湖与湖仓 — 在对象存储上长出一个数据库 |
| Day 39 | `workflow-engine-day39.html` | 工作流引擎 — 让崩溃后还能接着跑的长流程 |
| Day 40 | `feature-platform-day40.html` | 特征平台与 ML 基础设施 — 训练与推理共用一份特征的工程学 |
| Day 41 | `guardrails-before-scale-day41.html` | 当故障快于人类反应 — 自动护栏、爆炸半径与变更安全 |
| Day 42 | `globalization-multiregion-day42.html` | 全球化与多区域 — 光速是最后的约束 |
| Day 43 | `privacy-compliance-day43.html` | 隐私与合规架构 — 当「删除」不再是 DELETE |
| Day 44 | `chaos-engineering-day44.html` | 混沌工程 — 在生产里科学地制造故障 |
| Day 45 | `collaborative-editing-day45.html` | 协作编辑系统 — 让上百人同时敲一个文档还能收敛 |
| Day 46 | `consensus-coordination-day46.html` | 分布式共识与协调 — 让 5 台机器对「一件事」达成一致 |
| Day 47 | `storage-engine-day47.html` | 数据库内部与存储引擎 — 一次读写在盘上到底发生了什么 |
| Day 48 | `networking-fundamentals-day48.html` | 网络基础 — 一次请求在网线上到底走了几个来回 |
| Day 49 | `container-orchestration-day49.html` | 容器与编排 — 声明式控制平面如何让机器自愈 |
| Day 50 | `code-review-signal-detection-day50.html` | 把 Code Review 当信号检测系统 — 误报预算决定工具生死 |
| Day 51 | `low-base-rate-alerting-day51.html` | 低底率下的告警系统 — 报告级误报如何淹没真报 |
| Day 52 | `chaos-correctness-oracle-day52.html` | 给混沌工程装一个正确性 oracle — 故障下「还活着」不等于「答对了」 |
| Day 53 | `fat-tailed-risk-day53.html` | 项目风险要按肥尾管理 — 别盯均值，盯尾部 |
| Day 54 | `fail-obviously-day54.html` | Fail Obviously — 给 AI 工作流做失效可见性设计 |


### cs-papers-deepread 论文对照表（58 篇）

| 文件名 | 论文 |
| --- | --- |
| `attention-is-all-you-need-paper1.html` | Attention Is All You Need（Transformer） |
| `deep-residual-learning-paper2.html` | Deep Residual Learning（ResNet） |
| `alexnet-paper3.html` | AlexNet — 用深度卷积网络认图 |
| `word2vec-paper4.html` | Word2Vec（词向量） |
| `vision-transformer-paper5.html` | An Image is Worth 16×16 Words（ViT） |
| `clip-paper6.html` | CLIP：用自然语言当老师教机器看图 |
| `lstm-paper7.html` | Long Short-Term Memory（LSTM） |
| `seq2seq-paper8.html` | Sequence to Sequence Learning（Seq2Seq） |
| `bahdanau-attention-paper9.html` | Jointly Learning to Align and Translate（Bahdanau 注意力） |
| `bert-paper10.html` | BERT：双向预训练 + 微调 |
| `gpt-3-paper11.html` | GPT-3（Language Models are Few-Shot Learners） |
| `scaling-laws-paper12.html` | Scaling Laws（神经语言模型的缩放律） |
| `emergent-abilities-paper13.html` | Emergent Abilities（大模型的涌现能力） |
| `instructgpt-rlhf-paper14.html` | InstructGPT：用人类反馈训练模型「听话」（RLHF） |
| `constitutional-ai-paper15.html` | Constitutional AI（宪法 AI） |
| `generative-adversarial-networks-paper16.html` | Generative Adversarial Networks（GAN） |
| `google-file-system-paper17.html` | The Google File System（GFS） |
| `map-reduce-paper18.html` | MapReduce：把「大规模并行」缩成两个函数 |
| `bigtable-paper19.html` | Bigtable：一张能长到 PB 级的稀疏大表 |
| `chubby-paper20.html` | The Chubby Lock Service（Chubby 锁服务） |
| `percolator-paper21.html` | Percolator — 大规模增量处理 |
| `pregel-paper22.html` | Pregel — 像顶点一样思考 |
| `dremel-paper23.html` | Dremel：秒级交互式查询万亿行 |
| `spanner-paper24.html` | Spanner — Google 的全球分布式数据库 |
| `f1-distributed-sql-paper25.html` | F1：能扩展的分布式 SQL 数据库 |
| `dapper-paper26.html` | Dapper：大规模分布式系统追踪 |
| `tail-at-scale-paper27.html` | The Tail at Scale：大规模系统的尾延迟 |
| `ddpm-paper28.html` | Denoising Diffusion Probabilistic Models（DDPM） |
| `batch-normalization-paper29.html` | Batch Normalization（批归一化） |
| `dropout-paper30.html` | Dropout（随机失活） |
| `time-clocks-ordering-paper31.html` | Time, Clocks, and the Ordering of Events（逻辑时钟） |
| `relational-model-paper32.html` | A Relational Model of Data（关系模型） |
| `unix-time-sharing-paper33.html` | The UNIX Time-Sharing System（UNIX） |
| `new-directions-in-cryptography-paper34.html` | New Directions in Cryptography（公钥密码学） |
| `as-we-may-think-paper35.html` | As We May Think（诚如所思） |
| `mathematical-theory-of-communication-paper36.html` | A Mathematical Theory of Communication（通信的数学理论） |
| `goto-considered-harmful-paper37.html` | Go To Statement Considered Harmful（GOTO 有害论） |
| `byzantine-generals-paper38.html` | The Byzantine Generals Problem（拜占庭将军问题） |
| `end-to-end-arguments-paper39.html` | End-to-End Arguments in System Design（端到端论证） |
| `rsa-paper40.html` | RSA 公钥密码体制 |
| `anatomy-of-a-search-engine-paper41.html` | The Anatomy of a Search Engine（PageRank / 谷歌雏形） |
| `on-computable-numbers-paper42.html` | On Computable Numbers（图灵机 / 可计算性） |
| `decomposing-systems-into-modules-paper43.html` | 如何把系统拆成模块 · 信息隐藏 |
| `paxos-made-simple-paper44.html` | Paxos Made Simple |
| `congestion-avoidance-and-control-paper45.html` | Congestion Avoidance and Control（TCP 拥塞控制） |
| `bitcoin-paper46.html` | Bitcoin（比特币白皮书） |
| `computing-machinery-and-intelligence-paper47.html` | Computing Machinery and Intelligence（图灵测试） |
| `no-silver-bullet-paper48.html` | No Silver Bullet（没有银弹） |
| `adam-optimizer-paper49.html` | Adam：随机优化的默认解 |
| `raft-paper50.html` | Raft：为「读得懂」而生的共识算法 |
| `reflections-on-trusting-trust-paper51.html` | Reflections on Trusting Trust（信任的信任） |
| `complexity-of-theorem-proving-paper52.html` | The Complexity of Theorem-Proving Procedures（NP 完全性） |
| `dqn-atari-paper53.html` | Playing Atari with Deep Reinforcement Learning（DQN） |
| `dynamo-paper54.html` | Dynamo：亚马逊的高可用键值存储 |
| `alphago-paper55.html` | AlphaGo：深度网络 + 树搜索攻克围棋 |
| `harvest-yield-paper56.html` | Harvest、Yield 与可扩展容错系统 |
| `chord-paper57.html` | Chord（分布式哈希表 / DHT） |
| `kafka-paper58.html` | Kafka：为日志处理而生的分布式消息系统 |

## 3. 文件约定 / 发布
- 文件名 `{slug}-book{N}.html` + `{slug}-book{N}.en.html`，放仓库根目录。
- 发布前更新 `index.html`（把对应灰色占位行原地转链接，见下）+ `index.en.html`（同步转 `.en` 链接）。
- **index 条目的 `.title` 是「简介」不是「摘要」——一句话、一个钩子，只点出这一章那一两个核心想法 / 权衡，`Ch 标题 — 一个 clause` 到句号即止（对标样例第 1 章「Ch1 可靠·可扩展·可维护 — 先立三把尺子，用负载参数和响应时间百分位把『系统好不好』量化成可谈的东西」的分量，中文 ≤ 约 50 字、英文一行）。别把整章的问题、机制、权衡、影响全塞进 index——那些留给正文八节。宁短勿长。
- **不要**手动在内容页里加 `comments.js` / `search.js` / `index-button.js` / `i18n-tts.js` / `lightbox.js`（GitHub Action 自动注入，含右上角中英切换药丸 + TTS 朗读 + 图片/内联 SVG 点开放大）；也别硬写 `← Hub`。（index 页可硬写这些脚本，与姊妹站一致。）**图只管照常写 `<figure><svg>…</svg><figcaption>`，注入的 `lightbox.js` 会自动让每张图可点开、滚轮缩放、拖拽平移——不用你加任何 class 或 onclick。**
- **TTS 由 CI 自动烘焙（Azure → R2），你不用管**：`.github/workflows/bake-tts.yml` 在每次 push 到 `main` 且改动 `*.html` 时运行 `bake-tts.py`，按 `<h2>` 分段、对每段可朗读文本取 sha1 当 hash，生成 mp3 传到 R2 并把 `data-tts=<hash>` 写回 HTML（bot 提交，带 `[skip bake]` 防循环）。**你自己别手写 `data-tts`、别建 `audio/` 目录、别手跑 bake-tts。** 段内可朗读文本一字不变则 hash 不变、直接跳过——这条性质是下面 §2.5 交叉引用能「零重烘」回填的基础。
- 用 `./publish.sh` 发布：自动 add/commit/push 到 `main`，并校验体量、index 引用、div 平衡、重复编号、TOPICS 未被改、无硬写四脚本等。
- git：`user.name=BigCat` / `user.email=chengchen0802@gmail.com`。

## 4. 完成后
调用 **PushNotification**（`status:"proactive"`，一行 < 200 字、无 markdown），例如：
`专业书籍精读已更新：DDIA 第 5 章「复制」· 单主/多主/无主怎么选、复制滞后的坑 · cissy0802.github.io/chapter-deepread`

## index 维护：roadmap-first（写某章时把灰色占位转成链接，勿 append 重复）

本仓 index.html / index.en.html 采用「路线图先出」：清单里还没写的章已作为灰色占位行 `<div class="entry todo">…</div>`（无 href、不可点、todo 类）预先列出，顺序随 `TOPICS.md`。写某一章时：按 slug 在两个 index 里找到该章的灰色占位行，**原地**改成 `<a class="entry" href="{本期文件名}">`（去掉 `todo` 类、加 href，内部结构不变），绝不要在末尾另 append 一行（否则重复）。只有该章清单里没有对应灰色占位行时才 append。

**index 按书 → Part 分组显示**：两个 index 的 `.list` 里，条目按书成簇、簇内按 Part 分小组，每本书前一行 `<div class="group">书名<span class="tag">— 作者 · 年份</span></div>`，每个 Part 前一行 `<div class="group sub">Part 名</div>` 小标题。**原地转链接天然保持分组**（灰行本就在对的组里），不用动 group 标题。`<!-- entries -->` 标记在首本书 Part I 组内（已发布章之后）——仅当某章在 index 里找不到灰色占位行时才 fallback append 到该标记前，且要 append 进它所属的书 / Part 组，别破坏分组。新增一本书时，中英两版同步加 `.group`（书名）+ 若干 `.group.sub`（Part）标题。

**书架折叠**：两个 index 底部各有一段内联 `<script>`（+ head 里 `.book-toggle` 的 `<style>`）——点书名 `.group` 可折叠/展开该书章节，选择记在 localStorage。它在运行时自动接管所有 `.list > .group:not(.sub)`，所以你**照常加 `.group`/`.group.sub`/`.entry` 即可，新书自动可折叠**；只是别删掉这段 `<script>`/`<style>`。

**两个 index 页尾各有一段内联「书架折叠」`<style>`/`<script>`**（点书名 `.group` 折叠该书章节、`localStorage` 记选择）——**别删、别改**。它在运行时自动接管所有 `.list>.group:not(.sub)` 书名行，所以你照常加 `.group`/`.group.sub`/`.entry` 即可，新书自动获得折叠，无需为它加任何 class 或 onclick。

**TOPICS 顺序 = 写作优先级；index 分组顺序 = 展示顺序。** routine **永远从 `TOPICS.md` 顶部往下取第一个未做 slug** 来决定下一章写什么——只认 TOPICS。index 只是「书架 + 路线图」展示。

### 每次运行先「对齐」灰色占位（清单增长时自动补灰行）

每次运行开头，先扫 `TOPICS.md` 章节清单：凡是 **slug 没有对应页**（`ls *-book*.html` 去 `-bookN` 后缀比对）**且** index 里没有对应灰色行的章，按清单顺序补一条灰色占位行 `<div class="entry todo">…</div>`（无 href、`todo` 类）。`index.en.html` 用章的真实英文标题 + 简述（勿泄漏中文），`index.html` 用清单中文裁成本仓 zh 风格。**两个 index 都要补。** 新增整本书时，同步补该书的 `.group` + `.group.sub` 标题行。

这样 BigCat 往清单里加的新书 / 新章，下次运行就会自动作为灰色条目出现；等真正写它时再按 slug **原地**转成链接（勿另 append）。

## 新页面必带共享脚本（免触发 inject-comments 机器人提交）

生成任何 `*.html`（含 `.en.html`）时，在 `</body>` 前直接写入这 4 行，勿遗漏：

```html
<script src="https://hub.cissychen.com/comments.js" defer></script>
<script src="https://hub.cissychen.com/search.js" defer></script>
<script src="https://hub.cissychen.com/index-button.js" defer></script>
<script src="https://hub.cissychen.com/i18n-tts.js" defer></script>
```

这样 CI 的 inject-comments 不会再对新页面追加自动提交。
