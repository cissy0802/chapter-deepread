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
