# 专业书籍精读清单 Books Reading List（按书聚类 · 逐章排开）

BigCat 人工维护的计算机 / 软件经典书清单。**按书成簇、簇内按原书章节顺序排开**，一次把一本
书连着逐章读透。首本 DDIA，日后可在下面另起 `## 书名` 簇加新书（如 SICP、CSAPP、《TCP/IP
详解》、《数据库系统概念》……）。

> **选题 / 编号规则**
> - routine 每次从清单**顶部往下**挑第一个「slug 还没做过」的章（做没做看 `ls *-book*.html`，
>   去掉 `-bookN` 后缀按 slug 判断）。簇内顺序即优先级，从上往下逐章做即可。
> - 文件名 `book{N}` 的 **N 用写作顺序的下一个编号**（现有最大 N + 1），**与本清单的章号解耦**——
>   重排清单、插新书都不会打乱已发布文件（N 只递增）。
> - 这份清单**人工策划、routine 只读不改**（`publish.sh` 硬卡 TOPICS.md 改动）。清单全做完就发
>   PushNotification 请 BigCat 续单（加新书 / 新章）、本次不发布。
> - 要加书：在下面另起一个 `## 书名 · 作者 · 年份` 簇，簇内按原书章节顺序一行一章；别打散到别处。

> **当前优先级：先写 Alex Xu 两卷（Vol 1 → Vol 2），写完再往下走。**
> 2026-09-04 由 BigCat 指定，所以这两簇被提到清单最顶——routine 取的是「从顶往下第一个未做的 slug」，
> 之后往下面任何书簇里补章都不会插到 Xu 前面。Xu 写完后顺序自然回到 DDIA → CD → SRE → … 的原序列。

## System Design Interview Vol 1 — An Insider's Guide · Alex Xu · 2020
系统设计面试的通行底本。**与本仓其他书最大的不同：它是案例制不是概念制**——每章从需求澄清一路走到 API、数据模型、组件演进，示范的是「怎么把一道开放题做完」。精读时保留这条主线，别拆成概念清单。（跳过 Ch16「学习的延续」——收尾励志章、无实质内容。）
### Part I · 方法与基础（Ch1–3）
- **Ch1 从零到百万用户** — Scale From Zero To Millions Of Users — 单机怎么一步步长成分层集群：加缓存、加从库、加负载均衡、拆数据层，每一步解决的到底是哪个瓶颈（slug: `sdi1-ch01-scale-to-millions`）· xref: `sd:scalability-day1`, `sd:caching-day2`, `sd:sharding-day4`
- **Ch2 粗略估算** — Back-of-the-Envelope Estimation — 2 的幂、延迟数字、可用性九位数：怎么在白板上把 QPS / 存储 / 带宽算到量级正确（slug: `sdi1-ch02-back-of-envelope-estimation`）· xref: `sd:capacity-estimation-day26`, `sd:cost-capacity-engineering-day27`
- **Ch3 系统设计面试框架** — A Framework for System Design Interviews — 四步法：澄清需求 → 高层设计 → 深挖 → 收尾，以及面试官到底在评估什么（slug: `sdi1-ch03-interview-framework`）· xref: `sd:system-design-interview-day25`, `sd:capacity-estimation-day26`
### Part II · 系统案例（Ch4–15）
- **Ch4 设计限流器** — Design a Rate Limiter — 令牌桶 / 漏桶 / 滑动窗口各挡住什么，以及限流器该放在哪一层、分布式下的竞态怎么处理（slug: `sdi1-ch04-rate-limiter`）· xref: `sd:rate-limiting-day10`, `sd:api-design-day9`
- **Ch5 设计一致性哈希** — Design Consistent Hashing — 取模分片一加机器就全盘搬迁，一致性哈希用环 + 虚拟节点把搬迁量降到 1/N（slug: `sdi1-ch05-consistent-hashing`）· xref: `sd:sharding-day4`, `sd:replication-day5`
- **Ch6 设计键值存储** — Design a Key-Value Store — Dynamo 那一整套：quorum NWR、向量时钟、Merkle 树反熵、gossip 与 hinted handoff 怎么拼成一个无主存储（slug: `sdi1-ch06-key-value-store`）· xref: `sd:database-selection-day3`, `sd:consistency-day6`, `sd:storage-engine-day47`
- **Ch7 设计分布式唯一 ID** — Design a Unique ID Generator — 为什么自增主键在分布式下不成立，Snowflake 的时间戳 + 机器号 + 序列号怎么换来有序且无协调（slug: `sdi1-ch07-unique-id-generator`）· xref: `sd:unique-id-generation-day11`
- **Ch8 设计短网址服务** — Design a URL Shortener — 读多写少的极端形态：ID 编码成 base62、缓存命中率决定成本、301 与 302 的分析权衡（slug: `sdi1-ch08-url-shortener`）· xref: `sd:unique-id-generation-day11`, `sd:caching-day2`, `sd:rate-limiting-day10`
- **Ch9 设计网页爬虫** — Design a Web Crawler — URL frontier 的礼貌队列 + 优先级队列双层设计、robots.txt、内容去重与爬虫陷阱（slug: `sdi1-ch09-web-crawler`）· xref: `sd:search-system-day12`, `sd:message-queue-day8`, `sd:rate-limiting-day10`
- **Ch10 设计通知系统** — Design a Notification System — 可靠性全押在你控制不了的第三方通道（APNs / FCM / SMS）上：扇出、重试、去重与限流怎么设计（slug: `sdi1-ch10-notification-system`）· xref: `sd:message-queue-day8`, `sd:reliability-day23`, `sd:chat-system-day15`
- **Ch11 设计信息流** — Design a News Feed System — 写时扇出 vs 读时扇出，以及名人账号为什么必须走混合策略（slug: `sdi1-ch11-news-feed`）· xref: `sd:feed-system-day14`, `sd:caching-day2`
- **Ch12 设计聊天系统** — Design a Chat System — 长连接接入层、消息 ID 的有序性、已读回执与离线推送，1v1 与群聊的存储差别（slug: `sdi1-ch12-chat-system`）· xref: `sd:chat-system-day15`, `sd:realtime-systems-day34`
- **Ch13 设计搜索自动补全** — Design a Search Autocomplete System — Trie 怎么撑住每敲一个字母一次查询：前缀缓存、Top-k 预存、离线聚合与 trie 分片（slug: `sdi1-ch13-search-autocomplete`）· xref: `sd:search-system-day12`, `sd:caching-day2`, `sd:cdn-edge-day28`
- **Ch14 设计 YouTube** — Design YouTube — 转码流水线的 DAG 分解、分片上传、CDN 分层与冷热内容的成本取舍（slug: `sdi1-ch14-youtube`）· xref: `sd:video-streaming-day16`, `sd:cdn-edge-day28`, `sd:object-storage-day29`
- **Ch15 设计 Google Drive** — Design Google Drive — 文件同步这一层：块级切分与去重、增量同步、修订历史，以及多端离线后的冲突怎么收敛（slug: `sdi1-ch15-google-drive`）· xref: `sd:object-storage-day29`, `sd:collaborative-editing-day45`, `sd:consistency-day6`

## System Design Interview Vol 2 · Alex Xu & Sahn Lam · 2022
第二卷全部是案例，且比第一卷更深、更贴近真实工程——**造轮子的内部构造**（自己实现消息队列 / 对象存储）与**低延迟确定性系统**（交易所撮合）是它独有的两条线，本仓其他书都没有。
- **Ch1 设计附近服务** — Proximity Service — 把球面切成可索引的格子：geohash / 四叉树 / S2 各自的边界问题与半径查询（slug: `sdi2-ch01-proximity-service`）· xref: `sd:geo-system-day19`, `sd:sharding-day4`
- **Ch2 设计附近的好友** — Nearby Friends — 从静态兴趣点到高频移动的活人：位置流的发布订阅、Redis pub/sub 的扇出与陈旧位置的过期（slug: `sdi2-ch02-nearby-friends`）· xref: `sd:geo-system-day19`, `sd:chat-system-day15`, `sd:realtime-systems-day34`
- **Ch3 设计 Google Maps** — Google Maps — 地图瓦片的分级预渲染、路网图上的最短路与 contraction hierarchies、ETA 与实时导航重算（slug: `sdi2-ch03-google-maps`）· xref: `sd:geo-system-day19`, `sd:cdn-edge-day28`
- **Ch4 设计分布式消息队列** — Distributed Message Queue — 亲手造一个 Kafka：分段日志的磁盘布局、ISR 副本同步、消费者 rebalance 与元数据存哪（slug: `sdi2-ch04-distributed-message-queue`）· xref: `sd:message-queue-day8`, `sd:storage-engine-day47`, `sd:replication-day5`
- **Ch5 设计监控告警系统** — Metrics Monitoring and Alerting System — 时序数据的写入放大与降采样、拉 vs 推的采集模型、告警规则引擎与去重收敛（slug: `sdi2-ch05-metrics-monitoring`）· xref: `sd:observability-day21`, `sd:low-base-rate-alerting-day51`, `sd:data-processing-day20`
- **Ch6 设计广告点击聚合** — Ad Click Event Aggregation — 钱挂在聚合结果上时的流处理：点击去重、迟到数据回补、对账，以及大广告主的热点分片（slug: `sdi2-ch06-ad-click-aggregation`）· xref: `sd:data-processing-day20`, `sd:data-lakehouse-day38`, `sd:message-queue-day8`
- **Ch7 设计酒店预订系统** — Hotel Reservation System — 有限库存的并发争抢：超卖怎么防、悲观锁 vs 乐观版本号、临时占位与幂等下单（slug: `sdi2-ch07-hotel-reservation`）· xref: `sd:distributed-transactions-day7`, `sd:consistency-day6`, `sd:api-design-day9`
- **Ch8 设计分布式邮箱服务** — Distributed Email Service — 海量小对象的元数据难题：邮件正文与附件分离存储、按用户分区的收件箱索引与全文检索（slug: `sdi2-ch08-distributed-email`）· xref: `sd:object-storage-day29`, `sd:search-system-day12`, `sd:sharding-day4`
- **Ch9 设计对象存储** — S3-like Object Storage — 数据面与元数据面分离、纠删码怎么用 1.5 倍空间换 11 个 9、大对象分片上传与版本控制（slug: `sdi2-ch09-object-storage`）· xref: `sd:object-storage-day29`, `sd:replication-day5`, `sd:consistency-day6`
- **Ch10 设计实时排行榜** — Real-time Gaming Leaderboard — Redis sorted set 撑到多大就撑不住了：按分数分桶分片、查排名的近似解与精确解的代价差（slug: `sdi2-ch10-gaming-leaderboard`）· xref: `sd:database-selection-day3`, `sd:sharding-day4`, `sd:caching-day2`
- **Ch11 设计支付系统** — Payment System — 支付进出账的双向流、幂等键、与第三方 PSP 的对账，以及失败重试怎么不重复扣款（slug: `sdi2-ch11-payment-system`）· xref: `sd:payments-day17`, `sd:distributed-transactions-day7`, `sd:reliability-day23`
- **Ch12 设计数字钱包** — Digital Wallet — 从分布式事务一路推到事件溯源 + CQRS + Raft 复制状态机：让账本可重放、可审计、可恢复（slug: `sdi2-ch12-digital-wallet`）· xref: `sd:payments-day17`, `sd:consensus-coordination-day46`, `sd:distributed-transactions-day7`
- **Ch13 设计证券交易所** — Stock Exchange — 全书最反直觉的一章：订单簿 + 单线程确定性撮合 + 定序器，靠不分布式换微秒级与可重放（slug: `sdi2-ch13-stock-exchange`）· xref: `sd:realtime-systems-day34`, `sd:networking-fundamentals-day48`, `sd:observability-day21`

## DDIA — Designing Data-Intensive Applications · Martin Kleppmann · 2017

数据密集型应用设计。围绕**可靠、可扩展、可维护**三条主线，把「数据系统怎么选型、怎么权衡」讲
成一套通用心智——现代后端 / 分布式 / 数据库面试与架构决策的公认底本。三部分：基础 → 分布式数据
→ 派生数据。

### Part I. 数据系统的基石（Foundations of Data Systems）
- **Ch1 可靠、可扩展、可维护的应用** — Reliable, Scalable, and Maintainable Applications — 先立三把尺子（可靠/可扩展/可维护），教你用负载参数、响应时间百分位量化「系统好不好」（slug: `ddia-ch01-reliable-scalable-maintainable`）
- **Ch2 数据模型与查询语言** — Data Models and Query Languages — 关系 / 文档 / 图三种数据模型各擅长什么，以及声明式查询为何胜过命令式（slug: `ddia-ch02-data-models-query-languages`）
- **Ch3 存储与检索** — Storage and Retrieval — 数据库底层怎么存怎么找：日志结构 / LSM-tree vs B-tree，OLTP vs 列式 OLAP（slug: `ddia-ch03-storage-and-retrieval`）
- **Ch4 编码与演化** — Encoding and Evolution — 数据怎么序列化、schema 怎么在不停机的前提下前后兼容地演化（slug: `ddia-ch04-encoding-and-evolution`）

### Part II. 分布式数据（Distributed Data）
- **Ch5 复制** — Replication — 同一份数据放多台机器：单主 / 多主 / 无主，以及复制滞后带来的一致性坑（slug: `ddia-ch05-replication`）
- **Ch6 分区** — Partitioning — 一份数据太大切成片：按键范围还是按哈希，热点与再平衡怎么办（slug: `ddia-ch06-partitioning`）
- **Ch7 事务** — Transactions — ACID 到底保证了什么，隔离级别与并发异常（脏读 / 幻读 / 写偏斜）（slug: `ddia-ch07-transactions`）
- **Ch8 分布式系统的麻烦** — The Trouble with Distributed Systems — 部分失效、不可靠时钟、网络与进程停顿：为什么分布式这么难（slug: `ddia-ch08-trouble-with-distributed-systems`）
- **Ch9 一致性与共识** — Consistency and Consensus — 线性一致、全序广播与共识（Paxos/Raft 之魂），CAP 之后真正该知道的（slug: `ddia-ch09-consistency-and-consensus`）

### Part III. 派生数据（Derived Data）
- **Ch10 批处理** — Batch Processing — MapReduce 及其后：把海量数据当不可变输入、批量算出派生结果（slug: `ddia-ch10-batch-processing`）
- **Ch11 流处理** — Stream Processing — 把数据当**永不结束的事件流**实时处理，事件溯源与流表二象性（slug: `ddia-ch11-stream-processing`）
- **Ch12 数据系统的未来** — The Future of Data Systems — 把整本书拧成一条主张：以数据流 / unbundling 重新组织数据系统，兼顾正确性（slug: `ddia-ch12-future-of-data-systems`）

## Continuous Delivery — Reliable Software Releases through Build, Test, and Deployment Automation · Jez Humble & David Farley · 2010

持续交付的奠基之作。**核心主张：让软件随时可发布**——靠部署流水线（deployment pipeline）把构建、测试、发布全自动化，把「发布」从高风险事件变成平常事。

### Part I. 基础
- **Ch1 软件交付的难题** — The Problem of Delivering Software — 常见反模式（手工部署、发布日地狱），持续交付要解决什么（slug: `contdelivery-ch01-problem-of-delivering-software`）
- **Ch2 配置管理** — Configuration Management — 一切纳入版本控制：代码、配置、环境、依赖（slug: `contdelivery-ch02-configuration-management`）
- **Ch3 持续集成** — Continuous Integration — 频繁集成、保持主干随时可构建可测（slug: `contdelivery-ch03-continuous-integration`）
- **Ch4 测试策略** — Implementing a Testing Strategy — 测试象限与金字塔，自动化到什么程度（slug: `contdelivery-ch04-testing-strategy`）
### Part II. 部署流水线
- **Ch5 部署流水线剖析** — Anatomy of the Deployment Pipeline — 从提交到生产的自动化关卡设计（全书核心）（slug: `contdelivery-ch05-deployment-pipeline`）
- **Ch7 提交阶段** — The Commit Stage — 快速反馈：编译、单测、静态分析（slug: `contdelivery-ch07-commit-stage`）
- **Ch8 自动化验收测试** — Automated Acceptance Testing — 面向业务的端到端自动化测试（slug: `contdelivery-ch08-automated-acceptance-testing`）
- **Ch10 部署与发布** — Deploying and Releasing Applications — 蓝绿 / 金丝雀、回滚、发布与部署解耦（slug: `contdelivery-ch10-deploying-and-releasing`）
### Part III. 交付生态
- **Ch11 管理基础设施与环境** — Managing Infrastructure and Environments — 基础设施即代码的雏形，环境一致性（slug: `contdelivery-ch11-managing-infrastructure`）
- **Ch12 管理数据** — Managing Data — 数据库迁移与 schema 演化如何纳入流水线（slug: `contdelivery-ch12-managing-data`）
- **Ch13 组件与依赖** — Components and Dependencies — 依赖管理与组件化构建（slug: `contdelivery-ch13-components-and-dependencies`）

## SRE — Site Reliability Engineering: How Google Runs Production Systems · Google（Beyer/Jones/Petoff/Murphy 编）· 2016

Google 怎么用软件工程的方法跑生产系统。**核心是把「可靠性」变成可量化、可预算的工程目标**（SLO + error budget），而不是靠英雄主义救火——云上大规模服务的运维底本。（精读技术/原则核心章，略去纯管理与组织章。）

- **Ch1 引论** — Introduction — SRE 是什么：用软件工程手段做运维，与传统 ops 的根本区别（slug: `sre-ch01-introduction`）
- **Ch3 拥抱风险** — Embracing Risk — 100% 可靠既不现实也不划算，如何用错误预算（error budget）给可靠性定价（slug: `sre-ch03-embracing-risk`）
- **Ch4 服务质量目标** — Service Level Objectives — SLI / SLO / SLA 到底怎么定、怎么用来做决策（slug: `sre-ch04-service-level-objectives`）
- **Ch5 消除琐务** — Eliminating Toil — 什么是 toil、为什么要自动化掉、上限该设多少（slug: `sre-ch05-eliminating-toil`）
- **Ch6 监控分布式系统** — Monitoring Distributed Systems — 四个黄金信号（延迟/流量/错误/饱和度），告警基于症状还是原因（slug: `sre-ch06-monitoring-distributed-systems`）
- **Ch8 发布工程** — Release Engineering — 可复现、自动化、一致的构建与发布：Google 的 CI/CD 观（slug: `sre-ch08-release-engineering`）
- **Ch9 简单性** — Simplicity — 可靠性的敌人是复杂度，如何主动做减法（slug: `sre-ch09-simplicity`）
- **Ch12 有效排障** — Effective Troubleshooting — 系统化定位故障的方法论，而非拍脑袋猜（slug: `sre-ch12-effective-troubleshooting`）
- **Ch15 事后复盘文化** — Postmortem Culture — 无指责（blameless）复盘：从失败里学习、不追人（slug: `sre-ch15-postmortem-culture`）
- **Ch21 处理过载** — Handling Overload — 优雅降级、负载脱落（load shedding）、客户端节流（slug: `sre-ch21-handling-overload`）
- **Ch22 应对级联失效** — Addressing Cascading Failures — 一个组件拖垮全局的机理与防线（slug: `sre-ch22-addressing-cascading-failures`）
- **Ch23 管理关键状态** — Managing Critical State: Distributed Consensus — 用分布式共识做可靠的状态复制（slug: `sre-ch23-managing-critical-state`）
- **Ch25 数据处理管线** — Data Processing Pipelines — 批 / 流管线的可靠性设计（slug: `sre-ch25-data-processing-pipelines`）
- **Ch26 数据完整性** — Data Integrity — 「读到的就是写进的」：备份、恢复与静默损坏防护（slug: `sre-ch26-data-integrity`）

## Accelerate — The Science of Lean Software and DevOps · Nicole Forsgren, Jez Humble, Gene Kim · 2018

用**科学方法**证明：软件交付效能能被测量、且能预测组织绩效。DORA 四大指标（部署频率/变更前置时间/变更失败率/恢复时间）的出处。（精读 Part I 研究发现，略去 Part II 统计方法论与 Part III 案例。）

- **Ch1 加速** — Accelerate — 为什么交付效能是竞争力，研究怎么做的（slug: `accelerate-ch01-accelerate`）
- **Ch2 测量效能** — Measuring Performance — 四大关键指标怎么定义、为什么是这四个（slug: `accelerate-ch02-measuring-performance`）
- **Ch3 测量并改变文化** — Measuring and Changing Culture — Westrum 组织文化模型与它为何影响绩效（slug: `accelerate-ch03-measuring-culture`）
- **Ch4 技术实践** — Technical Practices — 持续交付的哪些实践真正驱动效能（slug: `accelerate-ch04-technical-practices`）
- **Ch5 架构** — Architecture — 松耦合架构与团队自治如何解放交付速度（slug: `accelerate-ch05-architecture`）
- **Ch6 把安全融入交付** — Integrating Infosec — 左移安全（shift-left），别让安全成为最后的瓶颈（slug: `accelerate-ch06-integrating-infosec`）
- **Ch9 让工作可持续** — Making Work Sustainable — 减少部署痛苦与倦怠（burnout）（slug: `accelerate-ch09-making-work-sustainable`）
- **Ch11 领导者与管理者** — Leaders and Managers — 变革型领导如何放大技术实践的效果（slug: `accelerate-ch11-leaders-and-managers`）

## Database Internals — A Deep Dive into How Distributed Data Systems Work · Alex Petrov · 2019

DDIA 的自然续集，往下钻一层：数据库**存储引擎**与**分布式系统**到底怎么实现。BigQuery / 列存 / 查询执行的底层机理都能在这里找到根。

### Part I. 存储引擎（Storage Engines）
- **Ch1 引论与概览** — Introduction and Overview — DBMS 架构、行存 vs 列存、内存 vs 磁盘（slug: `dbinternals-ch01-introduction-and-overview`）
- **Ch2 B-Tree 基础** — B-Tree Basics — 为什么磁盘数据库偏爱 B-Tree（slug: `dbinternals-ch02-btree-basics`）
- **Ch3 文件格式** — File Formats — 页、cell、slotted page：数据在磁盘上怎么摆（slug: `dbinternals-ch03-file-formats`）
- **Ch4 实现 B-Tree** — Implementing B-Trees — 分裂/合并、并发、页管理的工程细节（slug: `dbinternals-ch04-implementing-btrees`）
- **Ch5 事务处理与恢复** — Transaction Processing and Recovery — WAL、页缓存、ARIES 恢复（slug: `dbinternals-ch05-transaction-processing-and-recovery`）
- **Ch6 B-Tree 变体** — B-Tree Variants — Copy-on-Write、惰性 B-Tree、FD-Tree、Bw-Tree（slug: `dbinternals-ch06-btree-variants`）
- **Ch7 日志结构存储** — Log-Structured Storage — LSM-Tree：写优化存储怎么工作（BigTable/Cassandra 系）（slug: `dbinternals-ch07-log-structured-storage`）
### Part II. 分布式系统（Distributed Systems）
- **Ch8 引论与概览** — Introduction and Overview — 分布式系统的基本难题与抽象（slug: `dbinternals-ch08-distributed-introduction`）
- **Ch9 故障检测** — Failure Detection — 怎么判断一个节点挂了（心跳、φ-accrual）（slug: `dbinternals-ch09-failure-detection`）
- **Ch10 领导者选举** — Leader Election — 选主算法与脑裂防护（slug: `dbinternals-ch10-leader-election`）
- **Ch11 复制与一致性** — Replication and Consistency — 一致性模型谱系、quorum、CRDT（slug: `dbinternals-ch11-replication-and-consistency`）
- **Ch12 反熵与传播** — Anti-Entropy and Dissemination — gossip、Merkle 树、读修复（slug: `dbinternals-ch12-anti-entropy-and-dissemination`）
- **Ch13 分布式事务** — Distributed Transactions — 2PC/3PC、Percolator、Calvin（slug: `dbinternals-ch13-distributed-transactions`）
- **Ch14 共识** — Consensus — Paxos、Raft、Zab、拜占庭共识（slug: `dbinternals-ch14-consensus`）

## Chaos Engineering — System Resiliency in Practice · Casey Rosenthal & Nora Jones · 2020
混沌工程的正典，由创立这门学科的 Netflix 团队与同代实践者合写。**核心主张：可靠性不能靠「别出错」，只能靠主动制造故障去证伪你对系统的假设。** 前三章立原则，中间五章是 Slack / Google / 微软 / LinkedIn / Capital One 的一手实践，后半转向人的因素、投资回报与演进方向（持续验证、信息物理系统、安全混沌）。**全书 21 章全收，一章不跳。**
### Part I · 铺垫（Ch1–3）
- **Ch1 遭遇复杂系统** — Encountering Complex Systems — 复杂系统为什么不能靠拆开来理解：没有哪个工程师完整装得下它，故障来自组件之间而非组件本身（slug: `chaoseng-ch01-encountering-complex-systems`）· xref: `sd:chaos-engineering-day44`, `paper:no-silver-bullet-paper48`, `paper:tail-at-scale-paper27`
- **Ch2 在复杂系统里导航** — Navigating Complex Systems — 动态安全模型：经济、工作量、安全三条边界互相挤压，系统总在向失效边界漂移（slug: `chaoseng-ch02-navigating-complex-systems`）· xref: `sd:guardrails-before-scale-day41`, `sd:reliability-day23`, `paper:harvest-yield-paper56`
- **Ch3 原则总览** — Overview of Principles — 五条高级原则：建稳态假设、多样化真实事件、在生产跑、自动化持续跑、最小化爆炸半径（slug: `chaoseng-ch03-overview-of-principles`）· xref: `sd:chaos-engineering-day44`, `sd:chaos-correctness-oracle-day52`
### Part II · 原则的实战（Ch4–8）
- **Ch4 Slack 的灾难剧场** — Slack's Disasterpiece Theater — 给存量系统做混沌：先写设计文档、定预案、人在回路地演一场，而不是直接往生产扔猴子（slug: `chaoseng-ch04-slack-disasterpiece-theater`）· xref: `sd:chaos-engineering-day44`, `sd:deployment-release-day22`
- **Ch5 Google 灾难恢复演练 DiRT** — Google DiRT: Disaster Recovery Testing — 把演练做到公司规模：不只摇技术组件，也摇人员、流程、供应链——包括「关键工程师联系不上」（slug: `chaoseng-ch05-google-dirt`）· xref: `sd:chaos-engineering-day44`, `sd:reliability-day23`
- **Ch6 微软：实验的变化与优先级** — Microsoft Variation and Prioritization of Experiments — 故障空间是无穷的，所以真问题不是「怎么注入」而是「先注入哪个」——怎么排优先级（slug: `chaoseng-ch06-microsoft-variation-prioritization`）· xref: `sd:chaos-engineering-day44`, `sd:fat-tailed-risk-day53`
- **Ch7 LinkedIn：对真实用户负责** — LinkedIn Being Mindful of Members — 生产实验的伦理与工程：把爆炸半径限制到少数真人身上，并在伤害扩大前自动叫停（slug: `chaoseng-ch07-linkedin-mindful-of-members`）· xref: `sd:guardrails-before-scale-day41`, `sd:chaos-engineering-day44`
- **Ch8 Capital One：在强监管行业落地** — Capital One Adoption and Evolution of Chaos Engineering — 合规约束下怎么做混沌：从非生产环境起步、拿审计要的证据、再一步步走到生产（slug: `chaoseng-ch08-capital-one-adoption`）· xref: `sd:privacy-compliance-day43`, `sd:chaos-engineering-day44`
### Part III · 人的因素（Ch9–12）
- **Ch9 创造前瞻** — Creating Foresight — 从事后复盘转向事前想象：怎么在故障发生前把工程师心智模型里的盲区挖出来（slug: `chaoseng-ch09-creating-foresight`）· xref: `sd:observability-day21`, `sd:fail-obviously-day54`
- **Ch10 人性化的混沌** — Humanistic Chaos — 把混沌工程的方法搬到人类组织上：往团队、角色与流程里注入扰动，观察组织怎么恢复（slug: `chaoseng-ch10-humanistic-chaos`）· xref: `sd:guardrails-before-scale-day41`, `sd:fail-obviously-day54`
- **Ch11 人在回路** — People in the Loop — 什么时候该让人介入、什么时候人本身就是瓶颈：自动化与人类判断怎么分工（slug: `chaoseng-ch11-people-in-the-loop`）· xref: `sd:guardrails-before-scale-day41`, `sd:fail-obviously-day54`
- **Ch12 实验选择问题（及一个解法）** — The Experiment Selection Problem (and a Solution) — 从随机注入走向血缘驱动的故障注入（LDFI）：用数据依赖关系算出「该注入哪里」而不是靠猜（slug: `chaoseng-ch12-experiment-selection-problem`）· xref: `sd:chaos-correctness-oracle-day52`, `sd:chaos-engineering-day44`
### Part IV · 商业因素（Ch13–15）
- **Ch13 混沌工程的投资回报** — ROI of Chaos Engineering — 怎么向业务证明「什么都没发生」的价值——用 Kirkpatrick 模型把预防性工作变成可度量的东西（slug: `chaoseng-ch13-roi-of-chaos-engineering`）· xref: `sd:cost-capacity-engineering-day27`, `sd:fat-tailed-risk-day53`
- **Ch14 开放心态、开放科学与开放混沌** — Open Minds, Open Science, and Open Chaos — 混沌实验的结果为什么该像科学成果一样公开：可复现、可同行评议，以及围绕它的开源工具生态（slug: `chaoseng-ch14-open-minds-open-science`）· xref: `sd:chaos-engineering-day44`
- **Ch15 混沌成熟度模型** — Chaos Maturity Model — 用采用度 × 精细度两个维度定位团队现在在哪一格、下一步该补什么（slug: `chaoseng-ch15-chaos-maturity-model`）· xref: `sd:chaos-engineering-day44`
### Part V · 演进与结语（Ch16–21）
- **Ch16 持续验证** — Continuous Verification — 从 CI/CD 推到 CV：Netflix 的 ChAP 怎么自动选实验、自动分流、自动判定，把混沌变成流水线的一道关（slug: `chaoseng-ch16-continuous-verification`）· xref: `sd:chaos-correctness-oracle-day52`, `sd:deployment-release-day22`, `paper:tail-at-scale-paper27`
- **Ch17 走向信息物理系统** — Let's Get Cyber-Physical — 当故障会伤到人：FMEA、功能安全与软件那套「在生产里试」在物理世界的边界在哪（slug: `chaoseng-ch17-lets-get-cyber-physical`）· xref: `sd:iot-edge-day35`, `sd:fat-tailed-risk-day53`
- **Ch18 HOP 与混沌工程** — HOP Meets Chaos Engineering — 人与组织绩效的五条原则：出错是常态、责备无助于学习，以及这如何改变你设计实验的方式（slug: `chaoseng-ch18-hop-meets-chaos-engineering`）· xref: `sd:fail-obviously-day54`, `sd:guardrails-before-scale-day41`
- **Ch19 在数据库上做混沌** — Chaos Engineering on a Database — 分布式数据库怎么被系统性地摇：网络分区、时钟漂移、节点失联，以及故障下的一致性怎么验（slug: `chaoseng-ch19-chaos-engineering-on-a-database`）· xref: `sd:chaos-correctness-oracle-day52`, `paper:time-clocks-ordering-paper31`, `paper:raft-paper50`
- **Ch20 安全混沌工程** — The Case for Security Chaos Engineering — 把安全事件当成可注入的故障：验的是检测与响应管不管用，而不是再做一次渗透测试（slug: `chaoseng-ch20-security-chaos-engineering`）· xref: `sd:security-day24`, `sd:chaos-engineering-day44`
- **Ch21 结语** — Conclusion — 把全书拧成一条主张：在没人装得下整个系统的时代，经验主义地制造故障是唯一诚实的可靠性方法（slug: `chaoseng-ch21-conclusion`）· xref: `sd:chaos-engineering-day44`

## Fundamentals of Data Engineering — Plan and Build Robust Data Systems · Joe Reis & Matt Housley · 2022

现代、云优先的数据工程全景。**把上面几本串成一条完整的数据栈**：采集→存储→转换→服务，warehouse/lakehouse/批流全覆盖——数据工程师的第一本系统读物。

### Part I. 基础与构件
- **Ch1 何谓数据工程** — Data Engineering Described — 数据工程师到底做什么，与数据科学的边界（slug: `dataeng-ch01-data-engineering-described`）
- **Ch2 数据工程生命周期** — The Data Engineering Lifecycle — 采集/存储/转换/服务 + 底层横切关注点（slug: `dataeng-ch02-data-engineering-lifecycle`）
- **Ch3 设计好的数据架构** — Designing Good Data Architecture — 架构原则与权衡，lakehouse/warehouse 之争（slug: `dataeng-ch03-designing-good-data-architecture`）
- **Ch4 全生命周期选型** — Choosing Technologies Across the Lifecycle — 自建 vs 托管、开源 vs 云、成本（slug: `dataeng-ch04-choosing-technologies`）
### Part II. 生命周期详解
- **Ch5 源系统数据生成** — Data Generation in Source Systems — 数据从哪来：数据库、API、CDC（slug: `dataeng-ch05-data-generation`）
- **Ch6 存储** — Storage — 对象存储、列式格式、warehouse/lakehouse 存储层（slug: `dataeng-ch06-storage`）
- **Ch7 采集** — Ingestion — 批 vs 流采集、ETL vs ELT（slug: `dataeng-ch07-ingestion`）
- **Ch8 查询、建模与转换** — Queries, Modeling, and Transformation — SQL / 查询引擎、数据建模、dbt 式转换（slug: `dataeng-ch08-queries-modeling-transformation`）
- **Ch9 为分析与 ML 服务数据** — Serving Data for Analytics and ML — BI、分析、特征供给（slug: `dataeng-ch09-serving-data`）
### Part III. 安全与未来
- **Ch10 安全与隐私** — Security and Privacy — 数据工程师的安全责任（slug: `dataeng-ch10-security-and-privacy`）

## A Philosophy of Software Design · John Ousterhout · 2nd ed 2021

短小精深的**软件设计品味**课。一条主线：**复杂度是敌人**，而复杂度来自依赖与晦涩；对策是「深模块」——简单接口包住复杂实现。全书每章一个可直接上手的判据。（精读核心设计章。）

- **Ch1 引论：一切都是复杂度** — Introduction: It's All About Complexity — 软件设计的根本目标就是压住复杂度（slug: `aposd-ch01-its-all-about-complexity`）
- **Ch2 复杂度的本质** — The Nature of Complexity — 复杂度的三种症状：变更放大、认知负担、未知的未知（slug: `aposd-ch02-nature-of-complexity`）
- **Ch3 光能跑还不够** — Working Code Isn't Enough — 战术编程 vs 战略编程：为什么「先能跑」会复利式还债（slug: `aposd-ch03-working-code-isnt-enough`）
- **Ch4 模块要「深」** — Modules Should Be Deep — 全书最核心的比喻：接口要小、实现可以厚，浅模块是复杂度之源（slug: `aposd-ch04-modules-should-be-deep`）
- **Ch5 信息隐藏与泄漏** — Information Hiding and Leakage — 什么该藏、什么算泄漏，为什么「时序分解」是常见陷阱（slug: `aposd-ch05-information-hiding`）
- **Ch6 通用模块更深** — General-Purpose Modules are Deeper — 略微通用的接口反而更简单、更好用（slug: `aposd-ch06-general-purpose-modules`）
- **Ch7 不同层，不同抽象** — Different Layer, Different Abstraction — 直通方法（pass-through）与装饰器泛滥是层次设计失败的信号（slug: `aposd-ch07-different-layer-different-abstraction`）
- **Ch8 把复杂度向下沉** — Pull Complexity Downward — 宁可模块内部难写，也别让调用方难用（slug: `aposd-ch08-pull-complexity-downward`）
- **Ch9 合还是分** — Better Together or Better Apart? — 何时该合并、何时该拆分：判据不是行数（slug: `aposd-ch09-better-together-or-apart`）
- **Ch10 把错误定义掉** — Define Errors Out of Existence — 最反直觉的一招：让异常情况在语义上不存在，而不是到处 try/catch（slug: `aposd-ch10-define-errors-out-of-existence`）
- **Ch11 设计两次** — Design it Twice — 第一版方案几乎从不是最好的，逼自己出第二套（slug: `aposd-ch11-design-it-twice`）
- **Ch13 注释写「不明显」的东西** — Comments Should Describe Things That Aren't Obvious — 好注释补充代码说不出的信息，而非复述代码（slug: `aposd-ch13-comments-non-obvious`）
- **Ch14 命名** — Choosing Names — 名字是最小单位的抽象，含糊的名字预示设计有问题（slug: `aposd-ch14-choosing-names`）
- **Ch18 代码应当一目了然** — Code Should be Obvious — 「显而易见」是读者判定的，不是作者（slug: `aposd-ch18-code-should-be-obvious`）
- **Ch20 为性能而设计** — Designing for Performance — 简洁与快通常同向；何时才该为性能牺牲清晰（slug: `aposd-ch20-designing-for-performance`）

## Software Engineering at Google · Titus Winters, Tom Manshreck, Hyrum Wright · 2020

Google 二十年工程实践的公开总结。**核心命题：软件工程 = 编程 × 时间 × 规模**——代码要活很多年、被很多人改，一切实践（测试、评审、依赖、大规模变更）都是为这个命题服务。（精读技术与流程核心章，略去纯文化 / 管理章。）

### Part I. 论题
- **Ch1 何谓软件工程** — What Is Software Engineering? — 编程是写代码，工程是让代码在时间与规模下still 可维护；Hyrum 定律（slug: `swegoogle-ch01-what-is-software-engineering`）
### Part III. 流程
- **Ch8 风格指南与规则** — Style Guides and Rules — 规则为什么存在、怎么定、怎么自动执行（slug: `swegoogle-ch08-style-guides-and-rules`）
- **Ch9 代码评审** — Code Review — Google 的评审流程与它真正带来的收益（不只是找 bug）（slug: `swegoogle-ch09-code-review`）
- **Ch10 文档** — Documentation — 把文档当代码来维护（slug: `swegoogle-ch10-documentation`）
- **Ch11 测试总览** — Testing Overview — 为什么写测试、测试规模分类与收益模型（slug: `swegoogle-ch11-testing-overview`）
- **Ch12 单元测试** — Unit Testing — 可维护的单测：测行为不测实现（slug: `swegoogle-ch12-unit-testing`）
- **Ch13 测试替身** — Test Doubles — mock / stub / fake 的取舍与滥用代价（slug: `swegoogle-ch13-test-doubles`）
- **Ch14 更大范围的测试** — Larger Testing — 集成 / 端到端测试怎么做才不脆（slug: `swegoogle-ch14-larger-testing`）
- **Ch15 废弃** — Deprecation — 怎么体面地下线一个被广泛依赖的系统（slug: `swegoogle-ch15-deprecation`）
### Part IV. 工具
- **Ch16 版本控制与分支管理** — Version Control and Branch Management — 为什么 Google 选单体仓 + 主干开发（slug: `swegoogle-ch16-version-control`）
- **Ch18 构建系统与构建哲学** — Build Systems and Build Philosophy — 基于制品的构建、可复现与远端缓存（Bazel 之道）（slug: `swegoogle-ch18-build-systems`）
- **Ch20 静态分析** — Static Analysis — 让静态分析在开发流里真正被接受的条件（slug: `swegoogle-ch20-static-analysis`）
- **Ch21 依赖管理** — Dependency Management — 菱形依赖、语义化版本的局限、活在 HEAD（slug: `swegoogle-ch21-dependency-management`）
- **Ch22 大规模变更** — Large-Scale Changes — 怎么在几百万文件上安全地做一次全局改动（slug: `swegoogle-ch22-large-scale-changes`）
- **Ch23 持续集成** — Continuous Integration — CI 在超大规模下的形态与取舍（slug: `swegoogle-ch23-continuous-integration`）
- **Ch24 持续交付** — Continuous Delivery — 小步、频繁、可回滚：把发布做成非事件（slug: `swegoogle-ch24-continuous-delivery`）
- **Ch25 计算即服务** — Compute as a Service — 从 Borg 到托管计算：把机器当抽象资源（slug: `swegoogle-ch25-compute-as-a-service`）

## Fundamentals of Software Architecture · Mark Richards & Neal Ford · 2020

架构师的系统性入门。**核心：架构没有最佳实践，只有权衡**——先把「架构特征」（可扩展 / 可用 / 弹性…）定义清楚、可度量，再据此挑架构风格。（精读基础与架构风格核心章，略去纯职业软技能章。）

- **Ch1 引论** — Introduction — 架构到底是什么、架构师做什么，为什么没有标准定义（slug: `fosa-ch01-introduction`）
### Part I. 基础
- **Ch2 架构思维** — Architectural Thinking — 架构与设计的边界、广度胜过深度、权衡思维（slug: `fosa-ch02-architectural-thinking`）
- **Ch3 模块化** — Modularity — 内聚与耦合怎么量：连接度、抽象度、与主序列的距离（slug: `fosa-ch03-modularity`）
- **Ch4 架构特征定义** — Architecture Characteristics Defined — 「-ility」们到底指什么，隐式 vs 显式特征（slug: `fosa-ch04-architecture-characteristics-defined`）
- **Ch5 识别架构特征** — Identifying Architectural Characteristics — 从领域关切与需求里把关键特征挖出来（最多挑几个）（slug: `fosa-ch05-identifying-characteristics`）
- **Ch6 度量与治理架构特征** — Measuring and Governing Architecture Characteristics — 让特征可测量、用适应度函数持续守护（slug: `fosa-ch06-measuring-and-governing`）
- **Ch7 架构特征的作用域** — Scope of Architecture Characteristics — 架构量子：特征的边界不等于整个系统（slug: `fosa-ch07-scope-of-characteristics`）
- **Ch8 组件化思维** — Component-Based Thinking — 组件怎么划分、粒度多大、与领域怎么对齐（slug: `fosa-ch08-component-based-thinking`）
### Part II. 架构风格
- **Ch10 分层架构** — Layered Architecture Style — 最常见的单体分层：优点、隔离层与「污水池」反模式（slug: `fosa-ch10-layered-architecture`）
- **Ch11 管道架构** — Pipeline Architecture Style — 管道与过滤器：ETL 与数据处理的经典骨架（slug: `fosa-ch11-pipeline-architecture`）
- **Ch12 微内核架构** — Microkernel Architecture Style — 核心系统 + 插件：产品型软件的常用形态（slug: `fosa-ch12-microkernel-architecture`）
- **Ch13 基于服务的架构** — Service-Based Architecture Style — 粗粒度服务 + 共享库：微服务的务实折中（slug: `fosa-ch13-service-based-architecture`）
- **Ch14 事件驱动架构** — Event-Driven Architecture Style — 中介 vs 代理拓扑、异步的威力与代价（slug: `fosa-ch14-event-driven-architecture`）
- **Ch15 空间架构** — Space-Based Architecture Style — 用内存网格去掉数据库瓶颈，应对极端并发（slug: `fosa-ch15-space-based-architecture`）
- **Ch17 微服务架构** — Microservices Architecture — 边界上下文、粒度陷阱、数据隔离与通信（slug: `fosa-ch17-microservices-architecture`）
- **Ch18 如何选择架构风格** — Choosing the Appropriate Architecture Style — 按架构特征反推风格的决策路径（slug: `fosa-ch18-choosing-architecture-style`）
### Part III. 技术
- **Ch19 架构决策** — Architecture Decisions — ADR：把决策与理由固化下来，反模式「掩耳盗铃」（slug: `fosa-ch19-architecture-decisions`）
- **Ch20 分析架构风险** — Analyzing Architecture Risk — 风险矩阵、风险风暴与持续评估（slug: `fosa-ch20-analyzing-architecture-risk`）

<!-- 下一本书从这里另起：## 书名 · 作者 · 年份 —— routine 只读不改本文件 -->
