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

<!-- 下一本书从这里另起：## 书名 · 作者 · 年份 —— routine 只读不改本文件 -->
