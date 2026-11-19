# Final Viva Question Bank — BDSMA (`26CMPC71`)

> [!NOTE]
> **Practice Disclaimer:** These are **likely practice questions and model viva answers** compiled systematically from the official VESIT `26CMPC71` syllabus (Theory Modules 1–6 + Lab Experiments `1–11*`), Dr. Rohini Temkar's lecture decks (`module_1`–`module_6`), past Mumbai University (`MU`) exam questions embedded in the slides, and verified primary documentation. They are **not** claimed to be exact leaked examiner questions—use them to test active recall and handle examiner follow-ups naturally.

**Legend:**
- **`[HIGH PRIORITY]`** = Core pillar tested repeatedly in university theory/orals, slide review lists, or `25`-mark Practical & Oral (`PR & OR`) exams.
- **Categories per Module:** Basic Definition · Conceptual · How/Why · Difference-Between · Application/Scenario · Formula/Numerical · Challenging Follow-Up (including *Slide-Trap Clarifications*).

---

## Quick Jump Index

- [Module 1: Introduction to Big Data & Hadoop (`CO1`)](#module-1-introduction-to-big-data--hadoop-co1) (`Q1`–`Q14`)
- [Module 2: MapReduce, MapReduce Algorithms & NoSQL (`CO2`)](#module-2-mapreduce-mapreduce-algorithms--nosql-co2) (`Q15`–`Q34`)
- [Module 3: Mining Data Streams (`CO3`)](#module-3-mining-data-streams-co3) (`Q35`–`Q50`)
- [Module 4: Social Media Analytics, Network Measures & Community Clustering (`CO4`)](#module-4-social-media-analytics-network-measures--community-clustering-co4) (`Q51`–`Q68`)
- [Module 5: Social Media Text, Action & Hyperlink Analytics (`CO5`)](#module-5-social-media-text-action--hyperlink-analytics-co5) (`Q69`–`Q84`)
- [Module 6: Location Analytics, Search Engine Analytics, PageRank, HITS & Applications (`CO6`)](#module-6-location-analytics-search-engine-analytics-pagerank-hits--applications-co6) (`Q85`–`Q100`)
- [Practical & Oral (`PR & OR` — 25 Marks) Lab & Microproject Questions (`Exp 1–11*`)](#practical--oral-pr--or-lab--microproject-questions-exp-111) (`L1`–`L14`)

---

## Module 1: Introduction to Big Data & Hadoop (`CO1`)

*Supports `Module_1_Notes.md` (`26CMPC71` `1.1`, `1.2`, and Lab Exp 1).*

### Basic Definition Questions

**Q1. `[HIGH PRIORITY]` What is Big Data, and what are its 5 Vs?**  
**Answer:** Big Data refers to datasets whose massive size, arrival speed, and structural variety exceed the capture, storage, search, and processing capacity of traditional single-machine databases (RDBMS) within useful time and reasonable cost. The **5 Vs** are:
1. **Volume:** Huge scale of data (terabytes to exabytes/zettabytes).
2. **Velocity:** High speed at which data arrives and requires processing (real-time streams, clicks, IoT).
3. **Variety:** Diverse formats—structured tables, semi-structured JSON/XML, and unstructured video/text/audio.
4. **Veracity:** Uncertainty, noise, typos, duplicates, or unreliability in raw data.
5. **Value:** Turning raw processed patterns into real business profit, safety, or better decisions.

**Q2. What is Hadoop? Name its core components.**  
**Answer:** Apache Hadoop is an open-source framework (started by Doug Cutting and Michael Cafarella in 2005–2006, inspired by Google's GFS and MapReduce papers) for reliable, scalable distributed storage and batch processing across clusters of commodity hardware. Its core components are:
1. **HDFS (Hadoop Distributed File System):** Distributed storage layer.
2. **YARN (Yet Another Resource Negotiator, Hadoop 2.x+):** Cluster resource management and job scheduling layer.
3. **MapReduce:** Distributed parallel batch processing engine.
4. **Hadoop Common:** Shared Java utilities, libraries, and filesystem abstractions.

**Q3. Expand WORM, SPOF, QJM, and MPP in the context of Module 1.**  
**Answer:**
- **WORM:** *Write-Once-Read-Many* — HDFS files are written once (or appended) and read repeatedly without arbitrary in-place random edits.
- **SPOF:** *Single Point of Failure* — A single node (like the lone NameNode in Hadoop 1.x) whose failure brings down the entire cluster.
- **QJM:** *Quorum Journal Manager* — Majority-quorum set of JournalNodes synchronizing `EditLog` edits between Active and Standby NameNodes in Hadoop 2.x/3.x HA.
- **MPP:** *Massively Parallel Processing* — Shared-nothing cluster computing where independent nodes run queries in parallel on local storage.

### Conceptual & How/Why Questions

**Q4. `[HIGH PRIORITY]` Why does Hadoop say "Moving computation is cheaper than moving data"?**  
**Answer:** Over a standard `1 Gbps` network link, copying `10 TB` of raw data from storage nodes to a central compute node takes roughly **1 day** ($\approx 22$–$24\text{ hours}$). Instead, Hadoop sends the compiled MapReduce program (only a few kilobytes of code) to the DataNodes already storing the local `128 MB` HDFS blocks so all servers read their local disks in parallel.

**Q5. `[HIGH PRIORITY]` How does HDFS store and read/write a large file?**  
**Answer:**
- **Storage:** Files are split into large chunks (`128 MB` default in Hadoop 2.x/3.x; `64 MB` in 1.x) and replicated (`RF = 3` by default) across DataNodes. The **NameNode** keeps only namespace/block-location metadata in RAM (backed by `FsImage` + `EditLog`).
- **Write Pipeline:** Client asks NameNode for block locations $\to$ NameNode returns 3 DataNodes (`DN1, DN2, DN3`) $\to$ Client streams packets to `DN1`, which pipelines to `DN2`, which forwards to `DN3`; acknowledgments flow back before the NameNode commits.
- **Read Flow:** Client queries NameNode for block locations sorted by network proximity $\to$ Client reads blocks **directly from the nearest DataNode** in parallel without passing bulk data through the NameNode.

**Q6. How does Rack Awareness place 3 replicas of a block, and why?**  
**Answer:** Under Hadoop's default Replica Placement Policy (`HdfsDesign.html`), if the writer runs inside the cluster:
- **Replica 1:** Local node (or random node in local rack if outside cluster) — fast local/intra-rack write.
- **Replica 2:** A DataNode on a **different remote rack** — protects against an entire Top-of-Rack switch or rack power failure.
- **Replica 3:** A **different DataNode on that same remote rack** — keeps rack-fault tolerance while avoiding sending data across the slow core switch twice during writes.  
*(Clarifies slide phrasing suggesting 3 separate racks: default policy uses 2 distinct racks, not 3!)*

**Q7. Why are HDFS blocks `128 MB` instead of `4 KB` like a typical OS filesystem?**  
**Answer:**
1. **Minimizes disk seek overhead:** A `128 MB` block transfers continuously for ~1 second once the disk head seeks (~10 ms), keeping seek cost `< 1%` of transfer time.
2. **Protects NameNode RAM:** Since the NameNode stores metadata for *every* block in RAM, `128 MB` blocks mean ~32,000x fewer metadata entries than `4 KB` OS blocks!

### Difference-Between Questions

**Q8. `[HIGH PRIORITY]` Compare Structured, Semi-Structured, and Unstructured Big Data.**  
**Answer:**
| Feature | Structured | Semi-Structured | Unstructured |
|---|---|---|---|
| **Schema** | Rigid pre-defined tabular schema | Self-describing tags/keys (flexible schema) | No predefined data model |
| **Approx. Share** | Smallest portion (~10–20% alongside semi) | Growing logs/exchange formats | ~80% of enterprise/social data |
| **Examples** | Banking SQL tables, ERP rows | JSON tweets, XML docs, server logs | YouTube videos, images, free-text reviews, audio |

**Q9. `[HIGH PRIORITY]` Compare Traditional BI / Data Warehousing vs. the Big Data Approach.**  
**Answer:**
- **Traditional BI:** Structured internal data, central scale-up DB/EDW (Teradata, Exadata), strict schema-on-write, repeatable predefined KPI reports, slow to ingest messy social feeds.
- **Big Data Approach:** Structured + semi + unstructured internal/external data, scale-out shared-nothing commodity clusters (Hadoop/Spark/NoSQL), flexible schema-on-read, exploratory/predictive/streaming ML, agile time-to-value.

**Q10. `[HIGH PRIORITY]` Compare Hadoop 1.x vs. Hadoop 2.x (YARN) vs. Hadoop 3.x.**  
**Answer:**
| Dimension | Hadoop 1.x | Hadoop 2.x | Hadoop 3.x |
|---|---|---|---|
| **Resource Management** | Coupled inside `JobTracker` (MR only) | Decoupled via **YARN** (`RM`, `NM`, `AM`, `Container`) | Enhanced YARN (timelines, GPU/FPGA, federation) |
| **NameNode HA** | Single NameNode (**SPOF**); ~4,000 node cap | Active/Standby NameNodes via **QJM** (>10,000 nodes) | Multiple (`>2`) Standby NameNodes |
| **Storage Efficiency** | 3x Replication (`200%` overhead) | 3x Replication (`200%` overhead) | Adds **Reed-Solomon Erasure Coding** (`~50%` overhead!) |
| **Processing Paradigms** | MapReduce batch only | MapReduce, Spark, Tez, Storm, Graph on one cluster | Multi-engine cloud/containerized workloads |

**Q11. Compare Apache Hive vs. Apache Pig, and Apache MapReduce vs. Apache Spark.**  
**Answer:**
- **Hive vs. Pig:** **Hive** provides declarative SQL-like **HiveQL** best for BI analysts querying structured warehouse tables (now usually backed by Tez/Spark rather than MR). **Pig** uses procedural **Pig Latin** dataflow scripts best for programmers writing multi-step ETL over messy/semi-structured data.
- **MapReduce vs. Spark:** **MapReduce** writes intermediate results between Map and Reduce to **disk/HDFS**, making multi-pass iterative ML slow. **Apache Spark** executes a **DAG** of transformations using in-memory **RDDs/DataFrames**, cutting disk I/O dramatically (up to ~100x faster on iterative workloads that fit in memory, ~10x on disk).

### Application, Numerical & Challenging Follow-Up Questions

**Q12. (Application) How does Netflix use Big Data to save over \$1 billion/year, and how does British Telecom use Alarms Explorer?**  
**Answer:** Per Gomez-Uribe & Hunt (2015, *ACM TMIS*), **~80%** of hours streamed on Netflix are driven by personalized recommender models (and ~20% by search), cutting subscriber churn to save over **\$1 billion/year**, alongside **Contextual Bandits** for artwork/thumbnail personalization. **British Telecom (BT)** monitors ~25,000 devices via Alarms Explorer for Root-Cause Analysis (RCA), 15-minute ahead fault prediction, and real-time anomaly detection.

**Q13. `[HIGH PRIORITY]` (Numerical) A `300 MB` file (and a `1 GB = 1024 MB` file) are stored in HDFS with `128 MB` block size and Replication Factor `3`. Calculate blocks, block sizes, and total storage consumed.**  
**Answer:**
- **`300 MB` file:** $\lceil 300 / 128 \rceil = \mathbf{3\text{ blocks}}$ of sizes `128 MB`, `128 MB`, and `44 MB` (HDFS does not pad the final partial block!). With `RF = 3`, total replicas $= 3 \times 3 = \mathbf{9\text{ block replicas}}$, using $300 \times 3 = \mathbf{900\text{ MB}}$ total cluster disk.
- **`1 GB (1024 MB)` file:** $1024 / 128 = \mathbf{8\text{ blocks}}$ of `128 MB` each $\implies 8 \times 3 = \mathbf{24\text{ replicas}} = \mathbf{3\text{ GB}}$ total cluster storage.

**Q14. `[HIGH PRIORITY]` (Challenging Follow-Up / Slide Trap) Is the Secondary NameNode a hot standby backup if the primary NameNode crashes? What about "brontobytes" and `2.5 quintillion bytes/day`?**  
**Answer:**
1. **Secondary NameNode:** **No!** It is a **checkpointing helper**, not a hot failover backup. Every ~1 hour (or edit threshold), it merges `FsImage` + `EditLog` into a fresh `FsImage` so the NameNode restarts fast—if the NameNode dies abruptly, recent uncheckpointed edits can still be lost unless **Hadoop 2.x/3.x HA (Active + Standby NameNode + QJM)** is used (in HA, running Secondary NameNode is an error).
2. **Slide Units & Stats:** `"Brontobyte"` ($10^{27}$) and `"Geopbyte"` ($10^{30}$) are informal terms; the official SI prefixes adopted by BIPM in **Nov 2022** are **`ronna` ($10^{27}$)** and **`quetta` ($10^{30}$)**. Similarly, `2.5 EB/day` was IBM's ~2012 figure, whereas recent ~2024 IDC/Statista estimates cite ~`402.74 million TB/day` (~`402.74 EB/day`).

---

## Module 2: MapReduce, MapReduce Algorithms & NoSQL (`CO2`)

*Supports `Module_2_Notes.md` (`26CMPC71` `2.1`, `2.2`, `2.3`, and Lab Exps 2, 3, 4).*

### Basic Definition & Conceptual Questions

**Q15. `[HIGH PRIORITY]` Define the MapReduce programming model (`Map`, `Shuffle & Sort`, `Reduce`).**  
**Answer:** MapReduce processes massive datasets in three stages:
1. **`Map(k, v) -> <k', v'>*`:** Runs independently per input record on data-local nodes and emits zero or more intermediate key-value pairs.
2. **Shuffle & Sort (Group by Key):** Framework automatically partitions intermediate outputs across `R` reducers, transfers them over the network, and sorts/groups all values sharing each unique key `k'` into `(k', [v'1, v'2, ...])`.
3. **`Reduce(k', <v'>*) -> <k', v''>*`:** Runs once per unique intermediate key `k'` to aggregate or filter its value list and writes final output files (`part-r-00000`, etc.) to HDFS.

**Q16. `[HIGH PRIORITY]` What is a Combiner in MapReduce? When is it safe vs. unsafe to use one?**  
**Answer:** A **Combiner** is an optional **mini-reducer** executed locally on each Mapper node's output *before* network transfer across the Shuffle phase, drastically shrinking network I/O.  
- **Safe when:** The aggregation function is **associative and commutative**—such as `SUM`, `MAX`, `MIN`, or WordCount `COUNT` (e.g., collapsing 1,000 `(the, 1)` emissions on one machine into `(the, 1000)`).
- **Unsafe when:** Calculating **`AVERAGE`** directly! Because $\text{avg}(\text{avg}(10), \text{avg}(20, 30, 40)) = \text{avg}(10, 30) = 20 \neq 25$ (wrong weighting). **Fix:** Have the Combiner emit `(partial_sum, partial_count)` pairs and divide only inside the final Reducer!

**Q17. What are the 4 Business Drivers of NoSQL, and what does NoSQL stand for?**  
**Answer:** **NoSQL** (*"Not Only SQL"*, coined historically by Carlo Strozzi in 1998 for a non-SQL relational tool and popularized in 2009 by Johan Oskarsson/Eric Evans for distributed non-relational stores) is driven by:
1. **Volume:** Massive terabyte/petabyte data outgrowing single-machine scale-up hardware.
2. **Velocity:** Millions of concurrent reads/writes/sec demanding sub-millisecond ingestion.
3. **Variability:** Semi-structured/sparse attributes changing rapidly without `ALTER TABLE` downtime.
4. **Agility:** Eliminating the **Object-Relational Mapping (ORM) impedance mismatch** between app objects/JSON and rigid multi-table joins.

**Q18. `[HIGH PRIORITY]` State Brewer's CAP Theorem and Abadi's PACELC Theorem.**  
**Answer:**
- **CAP Theorem (Eric Brewer):** Any distributed data store can simultaneously guarantee at most two of three properties during a **Network Partition (`P`)** — **Consistency (`C`)** (every read receives the most recent write or error) and **Availability (`A`)** (every request to a non-failing node receives a non-error response). Since network partitions (`P`) are unavoidable in distributed clusters, real systems choose between **`CP`** (`HBase`, `Bigtable`, strict-majority `MongoDB`) and **`AP`** (default `Cassandra`, `Dynamo`-style eventual stores).
- **PACELC Theorem (Daniel Abadi, 2012):** Extends CAP: *If there is a **P**artition, trade off **A**vailability vs. **C**onsistency; **E**lse (normal operation with no partition), trade off **L**atency vs. **C**onsistency* (explaining why systems like Cassandra/DynamoDB also tune consistency during healthy operation).

**Q19. What does BASE stand for in NoSQL?**  
**Answer:** **BASE** (Dan Pritchett, 2008) stands for:
- **Basically Available:** System guarantees availability responses even during partial failures (though possibly stale).
- **Soft State:** Data/replicas may change over time even without new user input (during background anti-entropy/sync).
- **Eventually Consistent:** Once writes stop, all replicas converge to the same value after propagation delay.

### How/Why & Architecture Questions

**Q20. `[HIGH PRIORITY]` How does MapReduce cope with node failures (Map worker, Reduce worker, Master) and slow stragglers?**  
**Answer:** (Omitted from slides, required by `26CMPC71` `2.1`):
1. **Map worker fails:** The Master/ApplicationMaster marks **all** map tasks assigned to that machine—**even completed ones!**—as idle and reschedules them on another healthy node. *Why even completed maps?* Because intermediate map outputs live on the failed worker's **local disk**, so reducers can no longer fetch them! Downstream running reducers are notified of the new location.
2. **Reduce worker fails:** Only **in-progress** reduce tasks on that machine are restarted elsewhere; **completed** reduce tasks are *not* rerun because their final outputs are safely replicated inside global **HDFS**!
3. **Master / ApplicationMaster fails:** Periodically checkpoints state (`Hadoop 1.x` single JobTracker failed the job unless restarted from checkpoint; `Hadoop 2.x/3.x` **YARN** restarts a new `ApplicationMaster` container automatically via `ResourceManager`).
4. **Stragglers:** Solved via **Speculative Execution**—near job completion, the Master launches duplicate backup copies of slow trailing tasks; whichever copy finishes first wins and the duplicate is killed.

**Q21. Explain how MapReduce performs Natural Join ($R \bowtie S$) and Difference ($R - S$). Why are table tags needed?**  
**Answer:** Both need **table tags** so the Reducer knows which relation each tuple came from (since Mapper outputs share one intermediate stream):
- **Natural Join $R(A,B) \bowtie S(B,C)$:** Map emits key = join attribute `b`, value = `(R, a)` for $R$ and `(S, c)` for $S$. For each key `b`, Reduce builds the Cartesian product of all `a` values tagged `'R'` with all `c` values tagged `'S'` (if either list is empty, emits nothing).
- **Set Difference $R - S$:** Map emits key = full tuple `t`, value = `'R'` or `'S'`. Reduce emits `t` **only if** the value list contains `'R'` and does **NOT** contain `'S'`.

**Q22. Explain Master-Slave vs. Peer-to-Peer replication, and Horizontal vs. Vertical Sharding.**  
**Answer:**
- **Sharding:** Splitting data across multiple nodes so no single server holds everything. **Horizontal Sharding (most common):** different rows assigned to different servers via a **shard key** (hash/consistent hashing or range). **Vertical Sharding:** separating subsets of columns (e.g., frequently accessed profile fields vs. rare large blobs) onto separate servers.
- **Master-Slave Replication:** One primary/master node accepts writes and propagates updates asynchronously/synchronously to read replicas (`MongoDB` Primary-Secondary, `MySQL` replicas; `HBase` assigns single RegionServer authority per key range backed by HDFS 3x replication).
- **Peer-to-Peer Replication:** Every node in a ring can accept both reads and writes with no single point of failure (`Apache Cassandra`, `Dynamo`), handling conflicts via timestamps or quorum rules ($R + W > N$).

### Difference-Between Questions

**Q23. `[HIGH PRIORITY]` Compare 1-Step vs. 2-Step Matrix-Matrix Multiplication in MapReduce.**  
**Answer:**
| Aspect | 2-Step Matrix Multiplication (In Slides) | 1-Step Matrix Multiplication (Gap Fill / MU Q) |
|---|---|---|
| **MR Jobs Required** | **2 sequential jobs** (`Map1/Reduce1` joins on $j$; `Map2/Reduce2` sums on `(i, k)`) | **1 single job** (Reducers grouped directly on `(i, k)`) |
| **Network Shuffle Cost** | Lower per-element replication; requires reading/writing intermediate `(i, k)` pairs to HDFS between phases | **High replication:** Every $m_{ij}$ replicated $p$ times (to all columns $k$); every $n_{jk}$ replicated $r$ times (to all rows $i$) |
| **When Best** | Very large sparse/dense matrices where `(i,k)` replication blows up memory/network | Small-to-moderate dimensions where saving a full HDFS disk round-trip beats replication overhead |

**Q24. `[HIGH PRIORITY]` Compare Apache Flume vs. Apache Sqoop (including current Apache status).**  
**Answer:**
- **Sqoop:** Bulk **bidirectional batch transfer** between **RDBMS** (`MySQL`, `Oracle`) and Hadoop (`HDFS`/`Hive`/`HBase`) using JDBC/MapReduce (`sqoop import`, `sqoop export`). *Retired to **Apache Attic in June/July 2021**.*
- **Flume:** Reliable **streaming log/event ingestion** (`Source -> Channel -> Sink`, e.g., Memory/File/Kafka/JDBC channels into HDFS) for continuous unstructured logs/feeds. *Standalone Flume PMC retired **March 2024**, moving maintenance under **Apache Logging Services** (latest `1.11.0`).*

**Q25. `[HIGH PRIORITY]` Distinguish between Relational Columnar DBs (`Vertica`) and Wide-Column NoSQL (`HBase`, `Cassandra`, `Bigtable`).**  
**Answer:** True **Columnar RDBMS** (`Vertica`, `Parquet` analytics warehouses) store every single SQL column contiguously on disk for fast **OLAP** aggregations (`AVG`, `SUM`) across millions of rows. **Wide-Column NoSQL** (`Bigtable`, `HBase`, `Cassandra`) actually store a distributed **multi-level map** (`RowKey -> ColumnFamily:Qualifier -> Timestamp -> Value`) organized physically by sorted RowKey blocks (`SSTable`/`HFile`), letting each row add dynamic columns without fixed schemas and serving fast random key/range **OLTP/operational** lookups.

**Q26. `[HIGH PRIORITY]` Compare the 4 NoSQL Data Architecture Patterns (KV, Wide-Column, Document, Graph) with Real Case Studies.**  
**Answer:**
| Pattern | Data Model | Core Advantage | Best Use Cases | Verified Real Case / Tool |
|---|---|---|---|---|
| **Key-Value** | Opaque `key -> value` hash/map | Ultra-fast $O(1)$ lookup, massive scale | Shopping carts, sessions, caching | **Snap Inc. / Amazon DynamoDB**, **Redis**, Zoom |
| **Wide-Column** | Sparse `(RowKey, CF, Col, TS)` | High write throughput, dynamic sparse columns, petabyte scale | Time-series logs, telemetry, messaging | **Google Bigtable**, **Facebook/HBase**, **Spotify/Cassandra** |
| **Document** | Nested JSON / BSON / XML docs | Schema flexibility, matches OOP objects (`no ORM mismatch`) | Product catalogs, CMS, user profiles | **MongoDB**, **CouchDB**, Couchbase |
| **Graph** | Nodes + typed directed Edges + properties | **Index-free adjacency** ($O(1)$ per hop, no costly SQL joins!) | Fraud rings, social recommendations, shortest paths | **Neo4j** (Northwind / Twitter Cypher) |

**Q27. Compare ACID (RDBMS) vs. BASE (NoSQL), and Shared RAM vs. Shared Disk vs. Shared Nothing (`[DEWI92]`).**  
**Answer:**
- **ACID vs. BASE:** ACID enforces strict **Atomicity, Consistency (invariant preservation), Isolation, Durability** via locking/transactions; BASE prioritizes **availability and partition tolerance** via eventual convergence.
- **`[DEWI92]` Architectures:** **Shared RAM** (all CPUs share global memory + disks — fast for in-memory graph traversals, limited hardware scale); **Shared Disk** (each node has *private RAM* but shares a SAN/storage array — disk bus contention); **Shared Nothing / MPP** (each node has private CPU, RAM, and disk, communicating only via network — standard Hadoop/Spark/NoSQL scale-out architecture).

### Application, Formula/Numerical & Challenging Follow-Up Questions

**Q28. (Scenario — Store Selection) Which NoSQL pattern would you pick for: (a) a multiplayer game's live session token cache, (b) an e-commerce catalog where laptops and t-shirts have totally different attributes, (c) detecting circular money-laundering rings across 5 hops, and (d) Spotify's high-write playlist/metadata infrastructure?**  
**Answer:** (a) **Key-Value (`Redis`/`DynamoDB`)**, (b) **Document (`MongoDB`)**, (c) **Graph (`Neo4j`)** (constant multi-hop traversal via index-free adjacency), (d) **Wide-Column (`Apache Cassandra`)** (peer-to-peer multi-DC high write availability).

**Q29. `[HIGH PRIORITY]` (Formula / Numerical) Given $M_{2\times 3} = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix}$ and $N_{3\times 2} = \begin{bmatrix} 1 & 2 \\ 3 & 4 \\ 5 & 1 \end{bmatrix}$, show how 2-step MapReduce computes `(AB)_{2,2}` and flag the slide typo.**  
**Answer:**
- **Step 1 (`Map1/Reduce1`, join on `j = 1,2,3`):** Pair row 2 of $M$ (`4, 5, 6`) with col 2 of $N$ (`2, 4, 1`), producing `(i=2, k=2)` terms: $m_{21}n_{12} = 4\times 2 = 8$, $m_{22}n_{22} = 5\times 4 = 20$, and **$m_{23}n_{32} = 6\times 1 = 6$**.
- **Step 2 (`Map2/Reduce2`, sum by key `(2, 2)`):** $8 + 20 + 6 = \mathbf{34}$! *(Note: Slide 129 & 132 misprint `m_23*n_32` as `10` [adding to 38], while Slide 134 shows `28` when omitting the last pair—true sum is **`34`**!)*

**Q30. (Numerical — Cassandra Quorum) If a Cassandra cluster uses Replication Factor $N = 3$, what values of Read consistency $R$ and Write consistency $W$ guarantee strong consistency?**  
**Answer:** Any combination satisfying **$R + W > N$** (so read and write replica sets must overlap on at least one up-to-date node)—typically **`QUORUM` read ($R=2$) + `QUORUM` write ($W=2$)** since $2 + 2 = 4 > 3$, or `ALL` + `ONE` ($3+1>3$).

**Q31. `[HIGH PRIORITY]` (Challenging Follow-Up / Slide Trap) Does MapReduce `reduce(k', Iterable<v'>)` receive values sorted in `v'` order? Why does Java's WordCount on Slides 32–35 fail to compile?**  
**Answer:**
- **Sort Trap:** Slide 17 claims values are *"processed in $v'$ order"*. **False!** Standard Hadoop sorts strictly by intermediate **key `k'`**, not value `v'`. Sorting values requires **Secondary Sort** (composite key + custom `Partitioner` + custom `GroupingComparator`).
- **Java Code Bugs (`pp. 32–35`):** Missing `StringTokenizer` import, stray closing `)`, illegal `private`/`static` modifiers inside `map()`, missing closing braces, and deprecated `new Job(conf)` instead of **`Job.getInstance(conf, "WordCount")`**.

**Q32. (Challenging Follow-Up / Slide Trap) Spot the bug in Slide 155's `sqoop list databases --table emp` and Slide 157's Neo4j `CREATE CONSTRAINT ON ... ASSERT ...`!**  
**Answer:**
1. **`sqoop list-databases`:** Requires a **hyphen** (`list-databases`, not `list databases`) and takes **no `--table` argument** because it lists all databases on the server!
2. **Neo4j Cypher (`p. 157` vs `p. 159`):** Slide 157 prints Neo4j 4.x `ON (u:User) ASSERT u.name IS UNIQUE` syntax, which fails on the Slide 159 **Neo4j 5.3.0** server—Neo4j 5 requires **`CREATE CONSTRAINT FOR (u:User) REQUIRE u.name IS UNIQUE;`**.

**Q33. (Challenging Follow-Up / Slide Trap) Why is Slide 37's CAP definition of Availability (*"success or failure response"*) dangerous in a viva?**  
**Answer:** CAP **Availability** strictly requires every request to a non-failing node to receive a **non-error** response (not an HTTP 500 failure/timeout), *without* guaranteeing it contains the latest write! Returning an error satisfies Consistency/Abort, *not* CAP Availability.

**Q34. (Challenging Follow-Up) Why is `COUNT(*)` or `MIN`/`MAX` inside Hive sometimes fast, whereas `ORDER BY` bottlenecks a huge cluster?**  
**Answer:** `ORDER BY` in Hive forces a **total global sort through `1` single Reducer**, creating a severe bottleneck on big data. Using **`SORT BY`** instead sorts independently inside each of `R` parallel reducers!

---

## Module 3: Mining Data Streams (`CO3`)

*Supports `Module_3_Notes.md` (`26CMPC71` `3.1`, `3.2`, and Lab Exps 5 & 6).*

### Basic Definition & Conceptual Questions

**Q35. `[HIGH PRIORITY]` What is a Data Stream, and what are the 3Vs of Data Stream Mining?**  
**Answer:** A **data stream** is an unbounded, continuous, rapidly arriving sequence of elements (`IP packets`, stock trades, sensor pings, clickstreams) whose arrival rate and order cannot be controlled by the system. Unlike Big Data at rest, Stream Mining's **3Vs** (Slide 6) are:
1. **Volume:** Unbounded total records accumulating indefinitely.
2. **Velocity:** High real-time arrival rates requiring single-pass RAM processing.
3. **Volatility:** Constantly shifting data distributions over time!

**Q36. `[HIGH PRIORITY]` Distinguish between Concept Drift and Concept Evolution (from Stream Volatility).**  
**Answer:**
- **Concept Drift:** The statistical mapping $P(X, Y)$ between input features $X$ and *existing* labels $Y$ shifts over time (e.g., normal Diwali Rs. 50k spending vs off-season fraud trigger, or spammers changing trigger words). Can be sudden, gradual, incremental, or recurring.
- **Concept Evolution:** **Entirely new target classes** emerge dynamically in the stream that never existed during initial training (e.g., a brand-new zero-day malware family or a novel event category like `"COVID-19"`). Requires novel-class detection rather than forced old classification.

**Q37. What is a Blocking Operator, and what is Load Shedding in a DSMS?**  
**Answer:**
- **Blocking Operator:** A query operator that cannot emit any output until it has consumed the *entire* input (e.g., full `SORT` or `MAX` over an unbounded stream)—impossible on infinite streams unless restricted to finite **sliding/tumbling windows**.
- **Load Shedding:** Deliberately dropping selected incoming stream tuples during sudden traffic bursts so working RAM doesn't overflow and latency stays bounded.

### How/Why & Architecture Questions

**Q38. Draw/explain the Abstract DSMS Architecture. What role does the Input Stream Monitor/Regulator play?**  
**Answer:** Incoming heterogeneous streams pass through the **Input Stream Monitor / Regulator** (which timestamps tuples, parses formats, buffers bursts, and performs load shedding if overwhelmed) into the **Query Processor**. Unlike a DBMS pulling from disk, the Query Processor executes **Continuous/Standing Queries** registered in the **Query Repository** in **one pass** using bounded **Working/Summary Storage** (windows, sketches, Bloom filters), referencing **Metadata Storage** and optionally dumping cold raw records to **Archival Storage**.

**Q39. `[HIGH PRIORITY]` In the search stream `(user, query, time)`, why does random 10% sampling fail for estimating "what fraction of users issued repeat queries?", and how does Key-Hash Sampling fix it?**  
**Answer:**
- **Why naive sampling fails:** Picking 10% of raw search tuples splits a single user's queries arbitrarily! For instance, if a user searched `"hadoop"` 3 times, naive 10% sampling has roughly `~27%` chance of keeping 1 copy (falsely making them look like a *one-time* searcher!) and misses multiple repeats almost completely ($0.1^2$).
- **Key-Hash Sampling Fix:** Hash **only the `user` ID** deterministically into `b = 10` buckets (`0..9`), and keep **every** search tuple where `hash(user) < 1` (bucket `0`). Now 10% of *users* are sampled along with **100% of each sampled user's search history**, keeping group-by-user ratios completely unbiased! *(Fix for Slide 40: use `< a` on `0`-indexed buckets `0..b-1`, or `<= a` only if `1`-indexed!)*

**Q40. `[HIGH PRIORITY]` Explain Reservoir Sampling (Vitter's Algorithm R) and give the intuition for its $s/k$ inclusion probability proof.** *(Syllabus Gap Fill!)*  
**Answer:** When stream length $n$ is unknown beforehand and we want a uniform fixed-size sample of $s$ items:
1. Store the first $s$ arriving items directly in reservoir array $R[1..s]$.
2. For each subsequent $k$-th item ($k > s$): generate a uniform random integer $j \in \{1, \dots, k\}$. If $j \le s$, overwrite $R[j]$ with the $k$-th item; otherwise discard it.
- **Proof Intuition (Induction):** After step $k$, the new item sits in $R$ with probability $s/k$. Any earlier item already in $R$ (with prior prob $\frac{s}{k-1}$) survives step $k$ if it is *not* picked to be overwritten, which happens with prob $1 - \frac{1}{k} = \frac{k-1}{k}$. Thus $\frac{s}{k-1} \cdot \frac{k-1}{k} = \frac{s}{k}$—every item seen so far has **exact equal probability $s/k$**!

**Q41. `[HIGH PRIORITY]` Explain Bloom Filters: operations, why False Negatives are impossible, and why deletions break standard Bloom filters.**  
**Answer:**
- **Structure:** An $n$-bit array initialized to all `0`s plus $k$ independent hash functions $h_1, \dots, h_k \to \{0, \dots, n-1\}$.
- **Insert $x$:** Compute all $k$ indices and set `bits[h_i(x)] = 1`.
- **Query $y$:** Return `True` (*probably in set*) iff **all $k$ bits `bits[h_i(y)] == 1`**; if *any* single bit is `0`, return `False` (*definitely NOT in set*).
- **Zero False Negatives:** Inserting $x$ unconditionally sets all its $k$ bits to `1`, and bits are never reset to `0`, so a true member can never encounter a `0` bit later. Collisions among other inserted keys *can*, however, turn on all $k$ bits of a non-member, causing **False Positives**.
- **Deletion Fix:** Zeroing a bit during deletion would accidentally corrupt overlapping bits belonging to *other* keys! Standard solution: replace each 1-bit slot with a multi-bit **Counting Bloom Filter** (increment on insert, decrement on delete).

**Q42. `[HIGH PRIORITY]` Prove via the Pigeonhole Principle why exact counting of `1`s in a sliding window of length $N$ requires $\Omega(N)$ bits — and explain how DGIM achieves $O(\log^2 N)$ space with $\le 50\%$ error.** *(Syllabus Gap Fill!)*  
**Answer:**
- **Exact Lower Bound ($\Omega(N)$):** Consider two distinct $N$-bit strings differing at least at some position $p$. If the stream subsequently receives $p-1$ zeros, position $p$ becomes the *exact* outgoing bit leaving the window! To always update exact counts for all future steps without miscounting, the summary must distinguish all $2^N$ possible $N$-bit window histories—by the Pigeonhole Principle, that requires at least **$\log_2(2^N) = N = \Omega(N)$ bits**.
- **DGIM Breakthrough ($O(\log^2 N)$ space, $\le 50\%$ error):** Instead of tracking exact positions, DGIM groups `1`s into **exponentially sized buckets** `(end_timestamp, size = 2^j)` following 6 strict rules (sizes non-decreasing leftwards, **1 or 2 buckets** per power of 2 up to $\le \log_2 N$, right edge starts on `1`, expire when `end_ts <= t - N`).
  - *Space:* At most $\log_2 N$ distinct sizes $\times$ max 2 buckets/size $\times$ $O(\log_2 N)$ bits per timestamp $= \mathbf{O(\log^2 N)\text{ bits}}$!
  - *Query Error ($\le 50\%$):* Sum all fully enclosed buckets + **$\frac{1}{2}$** of the oldest partially overlapping bucket of size $2^j$. Since the true count inside that overlapping bucket lies in $[1, 2^j]$ and enclosed smaller buckets sum to at least $2^j - 1$, worst-case error is **strictly $< 50\%$**!

**Q43. `[HIGH PRIORITY]` Explain the Flajolet–Martin (FM) algorithm and why we combine multiple hash estimates using Median of Group Means rather than pure Mean or pure Median.**  
**Answer:**
- **FM Idea:** Hash each stream item $x$ uniformly into a binary string of length $\ge \log_2 n$ bits, count **trailing zeros** $r(x)$ from the LSB (probability a random string ends in $\ge R$ zeros is $2^{-R}$), keep $R = \max r(x)$, and estimate distinct count as **$m \approx 2^R$** using only **$O(\log m)$ bits**!
- **Combining Hashes (`Slide 130 vs. 133` Resolution):**
  - *Why pure Mean fails:* A single outlier lucky hash with many trailing zeros doubles/quadruples $2^R$ and **skews the average high** (unbounded upward bias).
  - *Why pure Median fails:* Every single estimate $2^R$ is always an exact **power of 2** (`1, 2, 4, 8, ...`), so the median of powers of 2 can never smoothly approximate numbers in between (e.g., `5` or `12`).
  - **Standard Solution (`MMDS` / Slide 130):** Group independent hashes into small groups of size $O(\log m)$, take the **mean within each group** (smoothing off power-of-2 steps), and take the **median across group means** (eliminating rare high outliers!). *(Warn examiner politely that Slide 133 reverses this textually as "mean of medians", whereas standard MMDS/Slide 130 is **median of means**!)*

### Difference-Between Questions

**Q44. `[HIGH PRIORITY]` Compare DBMS vs. DSMS across at least 6 dimensions.**  
**Answer:**
| Dimension | Traditional DBMS | Data Stream Management System (DSMS) |
|---|---|---|
| **Data Model** | Persistent finite relations on disk | Transient infinite continuous streams in RAM |
| **Access / Passes** | Arbitrary multi-pass random access | **Single-pass** sequential processing |
| **Arrival Control** | System-controlled (pull on demand) | **Source-controlled** (uncontrolled, push, bursty) |
| **Queries** | Ad-hoc **One-Time** SQL queries | **Continuous / Standing** queries |
| **Operations Allowed** | Blocking ops (`SORT`, global `COUNT`) allowed | Non-blocking operators only (or finite windows) |
| **Output & Accuracy** | Exact complete answer once | Approximate/sketch incremental updates in low latency |

**Q45. Compare Sliding Window (`DGIM`) vs. Exponentially Decaying Window for trend detection.**  
**Answer:** A fixed **Sliding Window** gives full weight `1` to items up to age $N$ and abruptly drops to `0` at $N+1$ (requiring $O(N)$ storage if tracking arbitrary item IDs). An **Exponentially Decaying Window** weights age-$i$ arrivals by $(1-c)^i$ ($c \sim 10^{-6}\text{–}10^{-9}$) via $O(1)$ per-step update $S \leftarrow S(1-c) + a_t$, smoothly fading older items, capping total active elements at $\approx 2/c$, and preventing sudden boundary drops or bursty spam spikes!

### Formula, Numerical & Challenging Follow-Up Questions

**Q46. `[HIGH PRIORITY]` (Formula + Numerical — Bloom Filter) State the False Positive Rate formula and optimal $k$ for a Bloom Filter. Then solve Slide 59 (`K = 8`, `H1 = x mod 8`, `H2 = (x+4) mod 8`): insert `10, 15`, then query `10` and `13`.**  
**Answer:**
- **Formulas:** After inserting $m$ keys into $n$ bits with $k$ hashes, fraction of remaining `0` bits $\approx e^{-km/n}$, fraction of `1` bits $\approx 1 - e^{-km/n}$, so:
  $$\text{FPR } p \approx \left(1 - e^{-km/n}\right)^k \qquad\text{and}\qquad k_{\text{opt}} = \frac{n}{m}\ln 2 \approx 0.693\,\frac{n}{m}$$
- **Slide 59 Trace (`bits[0..7]` initially `00000000`):**
  - Insert `10`: $H_1(10)=2$, $H_2(10)=6 \implies$ set bits **`2, 6`**.
  - Insert `15`: $H_1(15)=7$, $H_2(15)=3 \implies$ set bits **`3, 7`**. Bit array: `[0,0,1,1,0,0,1,1]` (bits `{2,3,6,7}` = `1`).
  - Query `10`: bits `2` (`1`) and `6` (`1`) $\implies$ **Probably Present** (True Positive).
  - Query `13`: $H_1(13)=5$ (`0`), $H_2(13)=1$ (`0`) $\implies$ **Definitely Not Present**!

**Q47. `[HIGH PRIORITY]` (Numerical — DGIM Slide 100 & Slide 84 Correction) For Slide 100's 24-bit window (`N = 24`, left = `t=1` to right = `t=24`): `1 0 1 0 1 1 0 0 0 1 0 1 1 1 0 1 1 0 0 1 0 1 1 0`, estimate the number of `1`s in the last `k = 14` bits before and after feeding `1 0 1 0 1 0 1 1`, and explain the error on Slide 84.**  
**Answer:**
- **Rule to Query Last `k` Bits:** Sum all buckets whose `end_timestamp > t - k`, taking **$\frac{1}{2}$** of the **oldest overlapping bucket**'s size. Always merge 3 identical consecutive sizes by combining the **older two** into $2^{j+1}$ at the newer of the two's end-timestamp.
- **Slide 100 (`t = 24`, `k = 14`, query `t >= 11`):** Buckets (`[end_ts, size]`): `[6, 4], [14, 4], [17, 2], [22, 2], [23, 1]`. Skipping `[6, 4]` (`end_ts < 11`), oldest overlapping is `[14, 4]` $\implies \frac{4}{2} + 2 + 2 + 1 = \mathbf{7}$ (exact `8`, `12.5%` error).
- **After Feeding `10101011` (`t = 32`, `k = 14`, query `t >= 19`):** Updated buckets: `[14, 8], [22, 4], [25, 2], [29, 2], [31, 1], [32, 1]` $\implies \frac{4}{2} + 2 + 2 + 1 + 1 = \mathbf{8}$ (exact `8`!).
- **Slide 84 Error:** On buckets `[4, 2, 2, 1]` where the `4`-bucket only partially overlapped `k`, Slide 84 wrongly added the full oldest bucket (`4 + 2 + 2 + 1 = 9`). Taking half gives $\frac{4}{2} + 2 + 2 + 1 = \mathbf{7}$ (`22.2% <= 50%` error).

**Q48. `[HIGH PRIORITY]` (Challenging Follow-Up / Slide Trap — Decaying Windows Slides 112–113) What is wrong in the professor's `fifa` vs. `ipl` Decaying Windows trace ($c=0.1$) for `fifa, ipl, fifa, ipl, ipl, ipl, fifa`?**  
**Answer:** Two hidden calculation errors exist on Slides 112–113:
1. On step 1 (`t=1`, `fifa`), `fifa` started empty ($S=0$) and received $+1$, so $S_{\text{fifa}}(1) = 0(0.9) + 1 = \mathbf{1.0}$, **not `0.9`**! Continuing consistently with $c=0.1$: `1.0 -> 0.9 -> 1.81 -> 1.629 -> 1.4661 -> 1.31949 ->` **`2.187541`** (slides got `2.135` because of the step-1 `0.9` mistake).
2. On `ipl`, the slide used $c=0.1$ (`0.9`) through step 3, then silently switched to **`0.99` ($c=0.01$)** from step 4 onward to reach `3.7264`! With consistent **$c=0.1$**, `ipl` finishes at **`3.02949`**—and `ipl` appears **4 times** vs `fifa` **3 times** (contrary to the slide's *"both occurred equal no. of times"* note!).

**Q49. (Challenging Follow-Up / Slide Trap — Flajolet–Martin `pp. 122–128`) Spot the bugs in the slide's FM trace for `S = {1,3,2,1,2,3,4,3,1}` with $h(x)=(3x+1)\bmod 5$.**  
**Answer:** First, `x=2`: $3(2)+1 = 7 \bmod 5 = \mathbf{2}$ (`0010`, $r=1$ trailing zero), and `x=3`: $3(3)+1 = 10 \bmod 5 = \mathbf{0}$ (`0000`). The slide swapped $h(2)$ and $h(3)$ in rows 5–6, misprinted `mod 2` instead of `mod 5`, and wrote `r=2` for `0010` instead of `r=1`! Also note the `0000` edge case: in pure theory $0000$ has `4` trailing zeros (`log2 n` width), though implementations either use $R$ capped cleanly or map zero hash carefully.

**Q50. (Numerical — FM Exercise p. 127) Compute $m = 2^R$ for `S = {1,2,3,4,5,6,7,8}` (`5`-bit hashes mod 32) using (a) `h(x) = (2x+1) mod 32` and (b) `h(x) = (3x+7) mod 32`.**  
**Answer:**
- **(a) `2x + 1`:** Always **odd** (LSB is always `1`!), so every element has $r = 0$ trailing zeros $\implies R = 0 \implies m = 2^0 = \mathbf{1}$ (shows why even-multiplier + odd-constant hash fails!).
- **(b) `3x + 7`:** At $x=3$, $3(3)+7 = 16 = 10000_2 \implies r(3) = 4$ trailing zeros (others $<4$), so $R = 4 \implies m = 2^4 = \mathbf{16}$!

---

## Module 4: Social Media Analytics, Network Measures & Community Clustering (`CO4`)

*Supports `Module_4_Notes.md` (`26CMPC71` `4.1`, `4.2`, `4.3`, and Lab Exps 7, 9, 10).*

### Basic Definition & Conceptual Questions

**Q51. `[HIGH PRIORITY]` Define Social Media Analytics (SMA), and explain the difference between Reach and Impressions.**  
**Answer:** **SMA** is the art and science of collecting, cleaning, analyzing, and interpreting structured and unstructured data generated by users on social platforms to support business decisions.
- **Impressions:** Total number of times a post is displayed on users' screens (one person scrolling past it 3 times $= 3$ impressions).
- **Reach:** Number of **unique users** who saw the post at least once (that same user $= 1$ Reach). Hence **$\text{Impressions} \ge \text{Reach}$** always!

**Q52. `[HIGH PRIORITY]` What is the Social Media Landscape, Need for SMA, and how does SMA differ between Small & Large Organizations?** *(Syllabus `4.1` Gap Fill!)*  
**Answer:**
- **Landscape:** Multi-platform ecosystem spanning SNS (Facebook, LinkedIn), Media/Video (YouTube, Instagram, TikTok), Microblogs (X/Threads), Messaging (WhatsApp, Telegram), Wikis/Forums (Reddit, Wikipedia)—where `5.22B` user identities overlap heavily (`<1.5%` single-platform exclusive!).
- **Need for SMA:** Real-time brand monitoring/crisis control, listening to unfiltered Voice of the Customer, competitor benchmarking, campaign ROI measurement, and influencer identification.
- **Small vs. Large Organizations:**
  - *Small businesses / startups:* Focus on hyper-local awareness, low-cost/free native dashboards (Meta Business Suite, Google Analytics, Hootsuite free/starter, TextBlob/VADER), quick customer replies, and community loyalty.
  - *Large enterprises:* Integrate cross-platform paid APIs and enterprise suites (Khoros, Brand24, custom Kafka/Spark + CRM/ERP pipelines), track multi-region crisis triggers, legal/PR compliance, and omnichannel churn/revenue attribution.

**Q53. `[HIGH PRIORITY]` List and explain Gohar F. Khan's Seven Layers of Social Media Analytics.**  
**Answer:**
1. **Text:** Sentiment, intent, concepts, and trends inside posts/comments/reviews.
2. **Networks:** Structural ties, influencers, communities, and information flow between actors.
3. **Actions:** Discrete interactions—likes, shares, views, clicks, check-ins, pins.
4. **Hyperlinks:** In-links, out-links, and co-links revealing traffic sources and authority.
5. **Location:** Spatial mapping (`GPS`, `IP`, geotags, check-ins) of users and events.
6. **Search Engines:** Query trends, SERP rank, organic/paid visibility, and PageRank.
7. **Apps / Mobile:** Usage, downloads, ratings, retention, and mobile app analytics.

**Q54. Define: Dyad, Triad, Structural Hole (Burt 1992), Multiplexity, and Network Diameter.** *(Syllabus Gaps in `Mod4B`/`Mod4d`!)*  
**Answer:**
- **Dyad:** A subgraph of **2 nodes** (plus any ties between them: empty, asymmetric, or mutual).
- **Triad:** A subgraph of **3 nodes** (open V-shape vs closed triangle—important for triadic closure and clustering).
- **Structural Hole (Ronald Burt, 1992):** An absence/gap of direct edges between two densely connected clusters; a bridging actor spanning that hole gains **brokerage control** over non-redundant information flow.
- **Multiplexity:** Simultaneous presence of **multiple types of relationships** (e.g., co-worker + friend + retweeted-by) connecting the same actors.
- **Network Diameter:** The **longest geodesic (shortest path)** between any pair of nodes in a connected network (measuring worst-case separation across the graph).

### How/Why & Visualization Questions

**Q55. Explain the 6-Step SMA Cycle and why "Cleaning" is so important (use the Maruti Baleno example).**  
**Answer:** The 6 steps circling **Business Objectives** are: **1. Identification $\to$ 2. Extraction $\to$ 3. Cleaning $\to$ 4. Analyzing $\to$ 5. Visualization $\to$ 6. Interpretation**. Cleaning strips bots, spam, duplicates, emojis/noise, and spelling variants—as shown in the Maruti Baleno slide where Google Trends revealed high search volume for the common **typo `"balleno"`** that raw exact-keyword extraction would miss!

**Q56. `[HIGH PRIORITY]` Compare the 4 Node Centralities (Degree, Closeness, Betweenness, Eigenvector) + when each fails.**  
**Answer:**
| Measure | Measures | Finds | Classic Failure Case |
|---|---|---|---|
| **Degree** | Direct neighbor count | Popular active hubs | Peripheral cluster hub (`Fig 3.3`) with many local friends but poor global reach |
| **Closeness** | Speed/shortest distance to *all* nodes | Fast information broadcasters | Disconnected components (infinite distances unless using harmonic closeness) |
| **Betweenness** | Fraction of shortest paths passing through node | **Bridges / gatekeepers / brokers** (`Bowtie` center) | Expensive $O(VE)$ on massive graphs; `0` for interior nodes of dense cliques |
| **Eigenvector** | Importance weighted by **neighbors' importance** ($Ax = \lambda x$) | Prestigious VIPs connected to other VIPs | Collapses to `0` on non-strongly-connected directed DAGs/tails (fixed by PageRank) |

**Q57. Explain Granovetter's "Strength of Weak Ties" and how Social Network Trust models work.**  
**Answer:**
- **Granovetter (1973/1974):** Counterintuitively, **weak ties** (acquaintances) bring far more new job leads and novel opportunities than close friends (**strong ties**) because close friends move in the **same tight cluster** with redundant information, whereas weak ties act as **local bridges** into distant circles! Four dimensions of tie strength: **Time, Emotional Intensity, Intimacy (mutual confiding), and Reciprocal Services**.
- **Trust:** Context-dependent and asymmetric (`A` trusts `B` doesn't guarantee `B` trusts `A`, nor does trusting a friend with secrets imply trusting them to drive carefully). Measured via McKnight's 4 organizational trust types, Johnson-George & Swap's 4 facets, and inferred across networks via shortest paths, similarity, and friend endorsement.

**Q58. How do Dunne & Shneiderman (2009) improve network graphs, and how do we tame "hairball" graphs?**  
**Answer:** Four readability guidelines: **1.** Every node is visible (`no overlap`), **2.** Every edge is visible (`no hidden edge crossings`), **3.** Edge length variation is minimized, **4.** Edge crossings are minimized—leveraging **pre-attentive visual processing** (color, size, shape, width) and layouts like **Force Atlas** or **Harel-Koren Fast Multiscale**. To prevent massive unreadable **hairballs**, apply **filtering/thresholding**, **egocentric sampling**, **community clustering/motifs (collapse supernodes)**, and interactive pan/zoom.

### Difference-Between Questions

**Q59. `[HIGH PRIORITY]` Compare Social Media Analytics (SMA) vs. Traditional Business Analytics (BA).**  
**Answer:** Traditional BA analyzes **structured, internal, historical, schema-fixed** enterprise data (`ERP`, sales ledgers) owned by the company using SQL/OLAP dashboards. SMA analyzes **unstructured, real-time, external, public/semi-public** User-Generated Content across evolving third-party APIs (tweets, graphs, actions, hyperlinks) using NLP, SNA, and stream mining to gauge public sentiment, influence, and virality.

**Q60. `[HIGH PRIORITY]` Compare Adjacency Matrix vs. Adjacency List vs. Edge List for Social Networks.**  
**Answer:** Social media graphs are **very sparse** (e.g., 1 million users have far fewer than $10^{12}$ possible pairs). An **Adjacency Matrix** wastes $O(n^2)$ memory storing zeros (though convenient for $Ax=\lambda x$ math). **Edge Lists** (`[(u, v), ...]`) and **Adjacency Lists** (`u -> [neighbors]`) store only existing ties in **$O(n + m)$ space**, scaling easily to massive social graphs!

**Q61. `[HIGH PRIORITY]` Distinguish Node Centrality vs. Network Centralization, and 1.0 vs. 1.5 vs. 2.0 Egocentric Networks.**  
**Answer:**
- **Centrality vs. Centralization:** **Node Centrality** scores one *individual node* (`who is central?`). **Network Centralization** ($NC \in [0, 1]$) measures how *unequally* centrality is concentrated around one star node across the *entire network* (**Star graph** $= \mathbf{1.0}$ max centralization; **Ring/Regular graph** $= \mathbf{0.0}$ zero centralization).
- **Ego Networks:** **1.0-Ego** = Ego + Alters + only Ego–Alter edges. **1.5-Ego** = adds Alter–Alter edges among those alters (used directly to compute Local Clustering Coefficient!). **2.0-Ego** = adds friends-of-friends (`2 hops` from Ego).

**Q62. `[HIGH PRIORITY]` Compare Clique Percolation Method (CPM) vs. Louvain Method (`Lab Exp 10`).**  
**Answer:**
- **CPM (`Mod4C`, Palla et al. 2005):** Finds **overlapping communities** (a node can belong to multiple groups, just like belonging to both a *College* and *Cricket* friend circle!) by extracting all $k$-cliques and merging those sharing **$k-1$ nodes** via components in clique graph $G_c$. Leaves peripheral non-clique degree-1 nodes unassigned and can be slow on dense graphs.
- **Louvain Method (`Lab Exp 10`, Blondel et al. 2008):** Finds **disjoint hierarchical partitions** quickly ($O(m)$ empirically) by greedily maximizing **Modularity $Q$** (intra-community edges minus random expectation) across two phases (local node moves $\to$ aggregate communities into supernodes). Assigns **every** node to a community.

### Application, Formula/Numerical & Challenging Follow-Up Questions

**Q63. `[HIGH PRIORITY]` (Numerical) Compute Engagement Rate (`250` engagements, `5,000` followers), Virality Rate (`50` shares, `2,000` impressions), and predictive sales ($\text{Sales} = 5.6 + 1.2\cdot\text{AdExp} + 0.5\cdot\text{Discount}$ for `AdExp=10, Discount=4`).**  
**Answer:**
- **Engagement Rate:** $(250 / 5000) \times 100 = \mathbf{5.0\%}$.
- **Virality Rate:** $(50 / 2000) \times 100 = \mathbf{2.5\%}$.
- **Predictive Analytics Regression:** $5.6 + 1.2(10) + 0.5(4) = 5.6 + 12 + 2 = \mathbf{19.6}$.

**Q64. `[HIGH PRIORITY]` (Formula / Numerical) Write the Local Clustering Coefficient formula and calculate it for a vertex `v` of degree $K_v = 4$ whose neighbors share $N_v = 1$ edge between themselves (`Mod4d` p. 19). Also compute Network Density for an undirected graph with $n=5$ nodes and $e=4$ edges.**  
**Answer:**
- **Local Clustering Coefficient:**
  $$CC(v) = \frac{2 N_v}{K_v(K_v - 1)} = \frac{2(1)}{4 \times 3} = \frac{2}{12} = \mathbf{\frac{1}{6} \approx 0.167}$$
- **Undirected Density:**
  $$D = \frac{e}{n(n-1)/2} = \frac{4}{5 \times 4 / 2} = \frac{4}{10} = \mathbf{0.40}$$

**Q65. (Numerical — CPM `MU COMP May 2016`) In a 9-node graph with 3-cliques `{1,2,3}, {2,3,4}, {3,4,5}` and `{5,7,8}, {6,7,8}` (`k=3`), find the $k$-clique communities. What changes if a temporary edge `C–H` creates `{C,G,H}` adjacent to `{G,H,I}` (`MU COMP May 2016`)?**  
**Answer:**
- **9-node (`k=3`, fixing Slide 34–35 duplicated `{5,7,8}` / missing `{6,7,8}` typo):** `{1,2,3}` shares `{2,3}` (2 nodes = $k-1$) with `{2,3,4}`, which shares `{3,4}` with `{3,4,5}` $\implies$ **Community 1 = `{1, 2, 3, 4, 5}`**. `{5,7,8}` shares `{7,8}` with `{6,7,8}` $\implies$ **Community 2 = `{5, 6, 7, 8}`**. Node **`5` overlaps** both communities (`node 9` is unclustered)!
- **`MU COMP May 2016`:** Adding temporary link `C–H` completes triangle `{C,G,H}`, which shares edge `G–H` with `{G,H,I}`, merging them into `{C,G,H,I}` (and bridging further if overlapping cliques exist).

**Q66. `[HIGH PRIORITY]` (Challenging Follow-Up / Slide Trap) Why does Closeness Centrality on `Mod4B` Slides 83–86 say *lower* numbers are more central, while Slide 87 says *higher* numbers are more central?**  
**Answer:** Slides 83–86 measure **Average Shortest-Path Distance** $\frac{\sum d(i,j)}{N-1}$ (farness—smaller average hop distance = closer to everyone = *more* central!), whereas Slide 87 defines **Normalized Closeness Centrality (Freeman 1979)** as its **reciprocal**:
$$CC(i) = \frac{N - 1}{\sum_{j \neq i} d(i, j)}$$
Taking the reciprocal flips the direction so values lie in $(0, 1]$ and **higher = more central**! *(Also watch Slide 89's typo writing $BC(v)$ denominator/subscript incorrectly—the standard formula is $\sum_{u \neq v \neq w} \frac{\sigma_{uw}(v)}{\sigma_{uw}}$.)*

**Q67. (Challenging Follow-Up / Slide Trap) Explain why `d(x,y) = 0` when `x != y` in `Mod4C` Slide 8 makes binary edge distance a "non-metric" similarity measure, and name the missing edges in the `MU IT May 2016` scan.**  
**Answer:** A mathematical **metric** requires $d(x, y) = 0 \iff x = y$ and the Triangle Inequality. Because `Mod4C` sets $d(x, y) = 0$ for *distinct* connected friends ($x \neq y$), it violates the identity of indiscernibles (and triangle inequality if $x-y$ and $y-z$ exist without $x-z$), making it a dissimilarity heuristic rather than a metric. In `Mod4C` p. 43 (`MU IT May 2016`), the cropped scan omits edges **`2–5` and `6–4`** which appear in the p. 44–45 solution!

**Q68. (Challenging Follow-Up / Tool Status) Which tools listed in Module 4's decks (`Mod4` / `Mod4d`) have shut down or changed names?**  
**Answer:**
- **Google+:** Shut down consumer accounts in **April 2019**.
- **Google Fusion Tables:** Shut down **December 3, 2019**.
- **Wikispaces:** Shut down **2018–Jan 2019**.
- **Socialbakers:** Rebranded to **Emplifi** (2021).
- **CodePlex (`NodeXL` legacy host):** Retired; NodeXL is now maintained by the **Social Media Research (SMR) Foundation** (`nodexlgraphgallery.org`). Also **`7layersanalytics.com`** in slides is no longer actively maintained by the author (`Gohar F. Khan 2015` book ISBN `978-1507823200`).

---

## Module 5: Social Media Text, Action & Hyperlink Analytics (`CO5`)

*Supports `Module_5_Notes.md` (`26CMPC71` `5.1`, `5.2`, `5.3`, and Lab Exps 7 & 8).*

### Basic Definition & Conceptual Questions

**Q69. `[HIGH PRIORITY]` Define Social Media Text Analytics, and compare Static Text vs. Dynamic Text.**  
**Answer:** **Social Media Text Analytics (Text Mining)** combines **NLP** and **Data Mining/ML** to extract structured insights from messy textual User-Generated Content (`~80%` of organizational data, e.g., `Flyertalk.com` forum complaints).
- **Static Text:** Longer, structured/formal, infrequently modified (`wikis`, blogs, corporate reports, emails, transcripts)—used heavily in **Concept Mining**.
- **Dynamic Text:** Short, rapid, real-time, opinionated (`Tweets`, comments, live forum discussions, private chats, customer reviews)—used heavily in **Sentiment & Trends Mining**.

**Q70. `[HIGH PRIORITY]` What are the 4 Purposes of Social Media Text Analytics (`ch 03 A` Fig. 1)?**  
**Answer:**
1. **Sentiment Analysis (Opinion Mining):** Detects positive, negative, or neutral polarity toward brands/products (e.g., Semantria logarithmic scoring).
2. **Intention Mining:** Extracts **future action intent** via intent verbs (`buy`, `purchase`, `sell`, `recommend`, `quit`, `desire`, `wish`)—e.g., catching churn risk before a user cancels!
3. **Trends Mining:** Predicts emerging market/viral shifts across time using ML/DM/SNA.
4. **Concept Mining:** Extracts, classifies, clusters, and ranks core concepts from **static documents** (academic abstracts, transcripts, policies).

**Q71. `[HIGH PRIORITY]` Define Social Media Actions Analytics (`ch 03 B` p. 24). Why are actions called the "cash cow" of social media?**  
**Answer:** **Actions Analytics** measures, analyzes, and interprets discrete symbolic user interactions with social media content (the **14 common actions:** Like, Dislike, Share, Visit/Revisit, View/Page View, Click/Clickstream, Tagging, Mentions, Hovering, Check-in, Pinning, Embeds, LinkedIn Endorsement, Uploading/Downloading). They are called the **"cash cow"** because every click, share, or visit directly translates into measurable popularity, ad revenue, website referral traffic, conversion funnels, and brand loyalty!

**Q72. What is Clickstream Analysis, Hovering, Pinning, and Embedding?**  
**Answer:**
- **Clickstream Analysis:** Tracking the exact ordered sequence of pages and links a user clicks through a site (`Home -> Search -> Filter -> Cart -> Checkout Dropoff`) to fix UX bottlenecks.
- **Hovering:** Pausing the mouse pointer (or dwell time) over an element without clicking—revealing visual attention/hesitation heatmaps.
- **Pinning:** Bookmarking/saving visual items to curated boards (`Pinterest`, pinned posts) signaling high future purchase intent.
- **Embedding:** Inserting hosted social media widgets/videos/posts onto external blogs or sites using HTML snippets (`iframe`/script), extending reach while tracking playback back to the host.

### How/Why & Difference-Between Questions

**Q73. `[HIGH PRIORITY]` Walk through the 4 Steps of the Text Analytics Pipeline (`ch 03 A` Fig. 2) and distinguish Stemming vs. Lemmatization.**  
**Answer:** *(Slide 18 PDF omitted inner circle labels; full 4 stages are:)*
1. **Identification & Searching:** Define business scope and scrape relevant text sources.
2. **Text Parsing & Filtering (NLP — *note `"NPL"` typo on Slide 20!*):** Tokenize text, fix spelling, remove **stop words** (`is, the, an` — *caveat: never blindly remove `"not"`/`"never"` in sentiment analysis!*), **POS tagging**, **Named Entity Recognition (NER)**, and normalize word stems.
   - **Stemming (`PorterStemmer`):** Crude heuristic suffix stripping (fast, can create non-words like `"studies" -> "studi"`).
   - **Lemmatization (`WordNetLemmatizer`):** Dictionary + POS-aware morphological reduction returning real valid root lemmas (`"better" -> "good"`, `"studies" -> "study"`).
3. **Text Transformation:** Convert clean text into numeric matrices using **Bag-of-Words / Vector Space Model (VSM)**, **TF-IDF**, co-occurrence, or **Latent Semantic Analysis (LSA via Truncated SVD)** to compress sparse dimensions into latent topics.
4. **Text Mining:** Run Association Rules, Clustering (*note `"natural"` $\to$ **`"neutral"`** typo on Slide 24!*), Classification, Prediction, and Sentiment scoring.

**Q74. `[HIGH PRIORITY]` Disambiguate Co-Citation vs. Bibliographic Coupling, AND Intra-Linking vs. Inter-Linking (`ch 03 C`).**  
**Answer:** *(Critical Slide Disambiguations!)*
1. **Co-Citation vs. Bibliographic Coupling (`Fig. 1 p. 5 & p. 9`):**
   - **Co-Citation / Co-Inlinking (`Small, 1973`):** One page $A$ links **to both** $B$ and $C$ ($A \to B$ and $A \to C$). Signals $B$ and $C$ are seen as similar topics/competitors.
   - **Bibliographic Coupling / Co-Outlinking (`Kessler, 1963`):** Two pages $B$ and $C$ both link **to the same common target** $A$ ($B \to A$ and $C \to A$). Signals $B$ and $C$ share overlapping focus/sources.
2. **Intra-Linking vs. Inter-Linking (`p. 2 & p. 14`):**
   - **Intra-Linking (Internal Linking):** Hyperlinks connecting pages **within the same website/domain** (helps navigation & crawl depth).
   - **Inter-Linking (External Linking):** Hyperlinks connecting **different websites/domains** (builds backlink authority and referral traffic). *(Note: Slide 14 loosely writes `"internal linking"` inside a confused header—state both clear definitions in the viva!)*

**Q75. `[HIGH PRIORITY]` Compare the 3 Types of Hyperlink Analytics (`ch 03 C` pp. 11–25). Summarize Khan, Yoon, & Park (2014).**  
**Answer:**
1. **Hyperlink Environment Analysis:** Audits a website's own and competitors' link topology, internal structure, SEO health, and toxic spam backlinks (using Google Search Console's **`.txt` Disavow Tool** — *not `"denied"` as Slide 16 writes!*).
2. **Link Impact Analysis:** Measures backlink quantity, referring domain authority, unlinked brand mentions, and inbound referral traffic hitting target URLs.
3. **Social Media Hyperlink Analysis:** Analyzes URLs shared *inside* tweets/posts (tracking sources, engagement, virality, fake news domains, influencers).
- **Khan, Yoon, & Park (2014) Finding (*Asian J. Comm.*):** Analyzed Korean vs. U.S. government agency Twitter out-links and found Korean government tweets clustered tightly around **centralized national/official hubs**, whereas U.S. agency tweets showed a more **decentralized, diverse external network**.

**Q76. What do `LinLog`, `ccTLD`, and `Indegree*` mean in the VOSON hyperlink diagram (`ch 03 C` p. 35)?**  
**Answer:**
- **`LinLog`:** Force-directed graph layout (**Noack's LinLog energy model**) that clusters tightly interlinked websites together cleanly.
- **`ccTLD`:** *Country Code Top-Level Domain* (`.uk`, `.in`, `.kr`) used to color/group nodes by country.
- **`Indegree*`:** Scaling node visual size proportional to its **in-degree** (how many external sites link *into* that node—higher in-links = larger bubble).

### Application, Formula/Numerical & Challenging Follow-Up Questions

**Q77. `[HIGH PRIORITY]` (Formula / Numerical — Bounce Rate & Session Duration) Define Unique Visitors, Visits (Sessions), and Revisits. Compute Bounce Rate under BOTH Universal Analytics (UA) and GA4 if out of `1,000` sessions: `400` leave immediately after 1 pageview (`<10s`, no event), `350` stay >`10s` on 1 page without clicking, and `250` browse 2+ pages.**  
**Answer:**
- **Terms:** **Unique Visitors** = deduplicated individuals in a period; **Visits (Sessions)** = distinct active browsing windows (`default 30 min inactivity timeout`); **Revisits** = repeat sessions by returning visitors.
- **Universal Analytics (UA) Bounce Rate:** Counts *all* single-page sessions (`400 + 350 = 750`) as bounces: $\frac{750}{1000} = \mathbf{75\%}$.
- **GA4 (Current Standard) Bounce Rate:** $\text{Engaged Sessions} = 350\text{ (>10s)} + 250\text{ (2+ views)} = 600 \implies \text{Engagement Rate} = 60\% \implies \text{GA4 Bounce Rate} = 100\% - 60\% = \mathbf{40\%}$!
- **Average Session Duration:** $\frac{\sum \text{Session Durations}}{\text{Total Sessions}}$ (traditionally calculated between first hit and last engagement hit).

**Q78. (Scenario — E-commerce Link Audit, `ch 03 C` p. 17) An online store gets `50%` of backlinks from product reviews/blogs, `20%` from forums/social media, `10%` from partner sites, and `20%` low-quality spam directories. What action should the SEO team take?**  
**Answer:** Run **Hyperlink Environment + Link Impact Analysis**: cultivate the high-value `50%` review/blog and `10%` partner links (converting unlinked mentions), inspect the `20%` social/forum links for traffic, and strip or submit a **Google Search Console Disavow `.txt` file** for toxic spam backlinks that could harm domain trust.

**Q79. (Verified Case Studies — `ch 03 B` p. 22 & `ch 03 C` p. 34) Summarize Cover-More Group (Action Analytics) and Khan & Vong (2014) YouTube Virality.**  
**Answer:**
- **Cover-More Group (Travel Insurance):** Used a **Hootsuite Command Center** to monitor customer inquiries/tweets and traveler disruptions in real time across regions, converting reactive support into faster claim response and proactive travel advisories.
- **Khan & Vong (2014, *Internet Research*):** Empirically studied viral YouTube videos across external social vs internal YouTube links/actions, confirming that **external network capital / sharing actions** alongside video view/engagement dynamics drive cross-platform virality—not view counts alone.

**Q80. `[HIGH PRIORITY]` (Lab Exp 8 — TextBlob vs. VADER) Compare TextBlob and VADER. What are VADER's `compound` score cutoffs?**  
**Answer:**
- **TextBlob:** General-purpose lexicon (`polarity` $\in [-1.0, +1.0]$, `subjectivity` $\in [0.0, 1.0]$); struggles with emojis, slang, ALL-CAPS emphasis, and exclamation marks.
- **VADER (Hutto & Gilbert, ICWSM 2014):** Specifically tuned for **social media text**—understands slang (`"sux"`), emojis (`😊`), booster words (`"extremely"`), punctuation (`"!!!"`), capitalization (`"GREAT"`), and negations (`"not bad"`). Returns `{neg, neu, pos, compound}` where standard thresholds classify:
  - **Positive:** $\text{compound} \ge +0.05$
  - **Negative:** $\text{compound} \le -0.05$
  - **Neutral:** $-0.05 < \text{compound} < +0.05$

**Q81. `[HIGH PRIORITY]` (Challenging Follow-Up / Slide Updates) What is X's (Twitter's) current character limit vs. Slide 7, and which tools in Module 5 (`ch 03 A/B/C`) are retired or renamed?**  
**Answer:**
- **X (Twitter) Limit:** Slides cite historical **`140`** chars; raised to **`280`** chars for standard posts in Nov 2017 and up to **`25,000`** chars for **X Premium** subscribers (`docs.x.com`; `t.co` URLs count `23` chars).
- **Tool Updates:** **Klout** (shut down May 25, 2018); **Open Site Explorer** (retired May 2018 $\to$ replaced by **Moz Link Explorer**); **Lithium** $\to$ **Khoros**; **Twtrland** $\to$ **Klear (Meltwater)**; **Facebook Insights** $\to$ **Meta Business Suite**; **Lexalytics/Semantria** (acquired by **InMoment** in Sept 2021; cloud API rather than legacy Excel add-in); **Hootsuite** legacy `Free/$8.99 Pro` slide screenshot replaced by current paid per-seat plans + short free trial.

**Q82. (Challenging Follow-Up / Slide Typos) What typos appear on `ch 03 A` pp. 20 & 24 and `ch 03 C` p. 16?**  
**Answer:** Slide 20 prints **`"NPL"`** instead of **`NLP`** (*Natural Language Processing*); Slide 24 prints **`"natural"`** instead of **`"neutral"`** sentiment; Slide 16 says `"denied"` spam links instead of Google's official **`disavow`** links tool!

**Q83. (Formula — TF-IDF Intuition) Why does Text Transformation (`Step 3`) prefer TF-IDF over raw word frequency?**  
**Answer:** Raw Bag-of-Words lets ultra-common corpus words (`"product"`, `"said"`, `"post"`) dominate similarity vectors. **TF-IDF** multiplies local **Term Frequency (`TF`)** by **Inverse Document Frequency (`IDF` = $\log(N / df)$)**, boosting rare words that distinguish a specific tweet or document while down-weighting generic filler terms.

**Q84. (Challenging Follow-Up) Why can simply deleting standard NLTK stop-words hurt Sentiment Analysis (`ch 03 A` / Exp 8)?**  
**Answer:** Default stop-word lists contain **negation words** (`not`, `no`, `never`, `nor`, `isn't`). Stripping `"not"` turns `"The phone is not good"` into `"phone good"`—flipping true negative sentiment into a completely wrong positive prediction! Always exclude negations when building sentiment pipelines.

---

## Module 6: Location Analytics, Search Engine Analytics, PageRank, HITS & Applications (`CO6`)

*Supports `Module_6_Notes.md` (`26CMPC71` `6.1`, `6.2`, and Lab Exps 9, 10, `11*`).*

### Basic Definition & Conceptual Questions

**Q85. `[HIGH PRIORITY]` What is Location Analytics, and what are its 4 general + 6 social media data sources?**  
**Answer:** **Location Analytics** (spatial / geo-analytics) maps, visualizes, and mines geographic locations of people, transactions, and resources.
- **4 General Sources:** Postal/ZIP address (converted via *geocoding*), Latitude/Longitude, GPS, IP geolocation.
- **6 Social Media Sources:** Device GPS pings, Geotagged posts/media (incl. EXIF), IP address geolocation, Check-ins (Facebook Places, Swarm), User profile location bios, Crowdsourced/third-party SDK mobility feeds.

**Q86. `[HIGH PRIORITY]` Differentiate Business Data-Driven vs. Social Media Data-Driven Location Analytics, and explain Geo-Enrichment (`Hecht 2013`).**  
**Answer:**
- **Business Data-Driven:** Analyzes internal structured records (POS billing, CDRs, delivery logs) via **4 Powerful Intelligence techniques** (**Clustering**, **Heat Mapping**, **Data Aggregation**, **Color-Coded Mapping**), **Geo-Enrichment**, and **Collaboration/Sharing**—overcoming static pinpoint clutter.
- **Social Media Data-Driven:** Analyzes public/mobile user traces across **7 uses**: Recommendations (**Tinder** — *note `"Tender"` typo p. 19!*), Customer Segmentation (`Fedica`/Tweepsmap), Location-based Ads, Info Requests, Emergency Alerts, Search & Rescue (`Project Agos`), and Navigation (`Google Maps`).
- **Geo-Enrichment (`Hecht 2013`):** Layering demographic, income/spending, lifestyle, and foot-traffic attributes onto raw geographic coordinates to explain *who* lives or visits there.

**Q87. What privacy rights are threatened by Location Analytics, and how can systems mitigate them?**  
**Answer:** Slides highlight two core rights: **Freedom of Movement** (moving unmonitored without chilling effects) and **Freedom from Being Observed** (privacy in daily routines), plus 6 ethical/legal questions across *Collection, Retention, Use, and Disclosure*. Mitigations include explicit opt-in consent, **spatial cloaking / *k*-anonymity** (reporting regional cells instead of raw user coordinates), data minimization, retention limits, and regulatory compliance (GDPR / India DPDP Act).

### How/Why & Architecture Questions

**Q88. `[HIGH PRIORITY]` Explain the 3 steps of a Crawler-Based Search Engine and clarify what `robots.txt` actually does.**  
**Answer:**
1. **Web Crawling:** Automated bots (`Googlebot`) fetch pages across hyperlinks, store snapshots in cache, and read **`robots.txt`** rules.
   - *Official Clarification (`Google Search Central`):* `robots.txt` manages **crawler traffic** (`allow/disallow` fetching); it does **NOT guarantee de-indexing**—if another site links to a disallowed URL, Google can still list its URL snippet unless blocked via **`noindex` meta tag / HTTP header**!
2. **Indexing:** Parses text/tags/links into massive **inverted indexes** (`word -> sorted posting list of doc IDs`) with PageRank/authority weights.
3. **Searching & Query Optimization:** Tokenizes queries, applies **NLP** spell correction, synonyms, personalization, ranks via **PageRank** + relevance + content signals, and renders the **SERP** (Organic vs. Paid PPC results).

**Q89. `[HIGH PRIORITY]` Explain the Seoul "Owl Bus" (`ch 04 A` p. 35 stub) case study in full.**  
**Answer:** Facing high late-night taxi congestion and expensive midnight cab rides (`midnight–5 AM`), the **Seoul Metropolitan Government** partnered with **KT Corporation** to mine **3 billion anonymized mobile call-detail/location records** paired with customer billing postcodes plus **5 million T-Money taxi pick-up/drop-off trips** aggregated into **1,250 1-km city grid cells** (preserving individual privacy!). Optimizing across origin-destination corridors produced **9 dedicated `Owl Bus` (`N-Bus`) night routes**, carrying ~7,900 passengers/night, cutting ~2.3M car trips/year and 500 metric tons of emissions while delivering ~14.1B KRW in public benefit.

**Q90. `[HIGH PRIORITY]` Why do we need Teleportation / Taxation ($\beta \approx 0.85$) in PageRank? Write the formula.**  
**Answer:** Idealized PageRank $\mathbf{r} = M\mathbf{r}$ breaks under two real web link pathologies:
1. **Dead Ends (Dangling Nodes):** Pages with zero outlinks (`0` column in $M$) leak probability mass every step until all scores collapse toward **`[0, 0, ..., 0]^T`**!
2. **Spider Traps:** Groups of pages (or self-loops like node `m -> m`) whose edges never exit the group absorb **100% of total PageRank** (`[0, ..., 1, ...]^T`).
- **Teleportation / Taxation Fix (`MMDS Ch. 5`):** With probability $\beta$ (typically `0.85`), the random surfer follows a random outgoing link; with probability $(1 - \beta)$ (`0.15` "tax"), they **teleport** uniformly to *any* page on the web:
  $$\mathbf{r}' = \beta M \mathbf{r} + (1 - \beta)\frac{\mathbf{e}}{n}$$
  *(And dead-end columns are treated as either teleporting uniformly to all $n$ nodes or normalizing total rank each step!)*

### Difference-Between Questions

**Q91. `[HIGH PRIORITY]` Compare Crawler-Based Engines vs. Directories vs. Metasearch Engines, AND Local vs. Global Search Engines.**  
**Answer:**
- **Crawler-Based (`Google`, `Bing`):** Automatically crawl & build giant indexes; handle massive long-tail real-time queries. **Directories (`Yahoo Directory` [closed 2014], `DMOZ` [closed 2017], `LookSmart`):** Manually curated by human editors; smaller and slow to update. **Metasearch (`Dogpile`, `Metacrawler`, `Mamma`):** Keep no giant independent web index; forward user queries to multiple search engines simultaneously and deduplicate/rank combined results.
- **Local vs. Global Search (`ch 04 B` p. 12 / Q3 gap fill):** **Local Search** scopes results to a **single website/enterprise intranet** (`Elasticsearch`/site search) *or* a **geographic radius** (`Google Maps "cafe near Chembur"`). **Global Search** indexes and ranks the **entire public World Wide Web** globally (`Google.com`, `Bing.com`).

**Q92. `[HIGH PRIORITY]` Compare PageRank vs. HITS (Hubs and Authorities — Bonus Section).**  
**Answer:**
| Dimension | PageRank | HITS (Kleinberg, 1999) |
|---|---|---|
| **Query Dependence** | **Query-independent** (computed offline globally) | **Query-dependent** (computed dynamically per query's Root + Base Set) |
| **Scores per Page** | **1 score** ($r_i$) | **2 scores**: **Authority ($a_i$)** & **Hub ($h_i$)** |
| **Equations** | $\mathbf{r}' = \beta M \mathbf{r} + (1-\beta)\frac{\mathbf{e}}{n}$ (column-stochastic $M$) | $\mathbf{a} = L^T \mathbf{h}$, $\mathbf{h} = L \mathbf{a}$ + L2 normalize (`binary L`) |
| **Main Risks** | Dead ends, Spider traps, link farms | **Topic drift** in expanded Base Set; tightly knit community bias |

### Formula, Numerical & Challenging Follow-Up Questions

**Q93. `[HIGH PRIORITY]` (Numerical — PageRank 3-Node) Given `Yahoo -> {Yahoo, Amazon}`, `Amazon -> {Yahoo, Microsoft}`, `Microsoft -> {Amazon}` (`m -> a`), write the transition matrix $M$ (`y, a, m`), compute $\mathbf{v}_1$ from $\mathbf{v}_0 = [1/3, 1/3, 1/3]^T$, and state the stationary limit.**  
**Answer:**
- Transition columns: $y \to (1/2, 1/2, 0)^T$, $a \to (1/2, 0, 1/2)^T$, $m \to (0, 1, 0)^T$:
  $$M = \begin{bmatrix} 1/2 & 1/2 & 0 \\ 1/2 & 0 & 1 \\ 0 & 1/2 & 0 \end{bmatrix}$$
- **Iteration 1:** $\mathbf{v}_1 = M \mathbf{v}_0 = [\frac{1}{6}+\frac{1}{6},\; \frac{1}{6}+\frac{1}{3},\; \frac{1}{6}]^T = \mathbf{[1/3,\; 1/2,\; 1/6]^T}$.
- **Limit ($\mathbf{v}_\infty$):** Converges to **$[2/5,\; 2/5,\; 1/5]^T = [0.4,\; 0.4,\; 0.2]^T$**.

**Q94. `[HIGH PRIORITY]` (Numerical — PageRank Flow Puzzle) If `PR(A) = 12` (`A` links to `B` and `D`), `PR(C) = 10` (`C` links only to `D`), and `D` links to `B` and `E`, find `PR(B)`.**  
**Answer:** `A` splits `12` evenly $\to$ `6` to `B` and `6` to `D`. `C` sends all `10` to `D`. Thus `D` receives $6 + 10 = 16$, and splits evenly $\to$ `8` to `B` and `8` to `E`. Total **`PR(B)` $= 6 + 8 = \mathbf{14}$**!

**Q95. (Numerical — Bonus HITS) For a 3-node link matrix $L = \begin{bmatrix} 0 & 1 & 1 \\ 0 & 0 & 1 \\ 0 & 0 & 0 \end{bmatrix}$ (`1->2,3`; `2->3`), compute 1 step of HITS from $\mathbf{h}_0 = [1, 1, 1]^T$.**  
**Answer:**
- Authority update $\mathbf{a}_1 = L^T \mathbf{h}_0 = [0, 1, 2]^T$ (L2-normalized: $[0, \frac{1}{\sqrt{5}}, \frac{2}{\sqrt{5}}]^T \approx [0, 0.447, 0.894]^T$ — node `3` is top Authority!).
- Hub update $\mathbf{h}_1 = L \mathbf{a}_1 = [3, 2, 0]^T$ (L2-normalized: $[\frac{3}{\sqrt{13}}, \frac{2}{\sqrt{13}}, 0]^T \approx [0.832, 0.555, 0]^T$ — node `1` is top Hub!).

**Q96. `[HIGH PRIORITY]` (Challenging Follow-Up / Slide Trap — `Dead end: Ex 3` & `Ex 2` L1/L2) Spot the errors on `ch 04 -Page Rank n HITS` Slides 12 and 15–16!**  
**Answer:**
1. **Slide 12 (`Ex 2`, 5 nodes):** Slide 12 prints `[0.4313, 0.4313, 0.3235, 0.3235, 0.6470]`, which looks unfamiliar next to standard probability PageRank `[0.20, 0.20, 0.15, 0.15, 0.30]`. *Why?* Both represent the **exact same `[4, 4, 3, 3, 6]` ratio**—Slide 12 just normalized the eigenvector to **L2 unit length ($\|\mathbf{v}\|_2 = 1$)** rather than probability **L1 sum ($\sum v_i = 1$)**!
2. **Slides 15–16 (`Dead end: Ex 3`):** Node `m` is a dead end (out-degree 0), yet Slide 16 accidentally pasted the Spider Trap iteration values ending in **`[0, 0, 1]^T`**! In the true dead-end matrix, probability leaks out every step (`[1/3, 1/6, 1/6] -> [1/4, 1/6, 1/12] -> ...`) and converges to **`[0, 0, 0]^T`** (shown correctly on Slide 17!).

**Q97. `[HIGH PRIORITY]` (Challenging Follow-Up / Syntax Trap) In `ch 04 B` Table 1 (`p. 35`), what does `+` mean in `social + analytics`, and what breaks in `social – analytics`?**  
**Answer:** Inside **Google Trends**, `+` acts as boolean **OR** (`social + analytics` searches for *either* term—whereas Google deprecated `+` in standard web search back in 2011!). Meanwhile, **`-` (exclude)** must have **NO space** after the hyphen (`social -analytics`, not `social – analytics` with a space or en-dash, or Trends treats it incorrectly!).

**Q98. `[HIGH PRIORITY]` (Challenging Follow-Up / Retired Metrics) Why does the 2023 `vesit.ves.ac.in` screenshot (`ch 04 B` p. 26) show `Alexa Rank: N/A`, and why shouldn't SEO teams target "Google PageRank 4/10" anymore?**  
**Answer:** Amazon shut down **`alexa.com` on May 1, 2022** (leaving 2023 lookups as `N/A`), and Google permanently removed its public **0–10 Toolbar PageRank score in 2016** (even though Google still uses internal link-authority PageRank signals behind the scenes). Today, teams inspect **Moz Domain Authority (`DA`) / Page Authority (`PA`)** and **Majestic Trust Flow / Citation Flow**.

**Q99. (Tool Migration) Since Google Fusion Tables (`ch 04 A` pp. 29–36) shut down on December 3, 2019, what modern tools replace it?**  
**Answer:** **QGIS** (open-source desktop GIS supporting KML/CSV joins like the Victoria Police tutorial), **Kepler.gl** (WebGL massive-scale spatiotemporal heatmaps/hex-bins), **Looker Studio + Google Maps Platform** (cloud BI geo-dashboards), and **Esri ArcGIS**.

**Q100. (Cross-Module Integration — `26CMPC71` Topic 6.2) How do all 6 modules fit together inside a real-time Big Data & Social Media Analytics application?**  
**Answer:** Continuous social/location streams (**Mod 3/6**) flow through **Kafka/Flume** (**Mod 2**) into distributed storage (**HDFS** **Mod 1** & **MongoDB/Cassandra/HBase** **Mod 2**), where **Spark Streaming** filters duplicates via **Bloom Filters/FM** (**Mod 3**), scores text via **VADER/TF-IDF** (**Mod 5**), counts clicks/actions (**Mod 5**), extracts communities/influencers via **Louvain/CPM/Centralities** (**Mod 4**) and **PageRank** (**Mod 6**), and serves geographic heatmaps (**Mod 6**) to business dashboards!

---

## Practical & Oral (`PR & OR` — 25 Marks) Lab & Microproject Questions (`Exp 1–11*`)

**L1. (`Exp 1` — HDFS CLI) Compare `hdfs dfs -put` vs `-copyFromLocal`, `-get` vs `-copyToLocal`, and give commands to inspect, move, and delete a file in HDFS.**  
**Answer:** Practically identical today (`-copyFromLocal` / `-copyToLocal` strictly require a local source/destination path, while `-put` / `-get` are slightly broader aliases). Key commands: `hdfs dfs -ls /dir`, `hdfs dfs -cat /dir/file`, `hdfs dfs -mv /src /dst`, `hdfs dfs -rm -r /path` (note `-skipTrash` bypasses Trash).

**L2. (`Exp 2` — NoSQL Setup & CRUD) How do MongoDB (`Document`), HBase (`Wide-Column`), and Cassandra (`Wide-Column`) store data differently when you run basic CRUD commands?**  
**Answer:** **MongoDB** stores BSON documents inside Collections (`db.users.insertOne()`, `find()`) using Primary-Secondary replica sets and optional shard keys. **HBase** (`put 'table','row1','cf:col','val'`, `get`, `scan`) stores sorted HFiles on **HDFS** managed by `HMaster` + `RegionServers` + `ZooKeeper` (strong single-row consistency). **Cassandra** uses SQL-like **CQL** (`CREATE TABLE ... PRIMARY KEY ((partition_key), clustering_col)`) over a masterless peer-to-peer ring with tunable consistency (`ONE`/`QUORUM`/`ALL`).

**L3. (`Exp 3` — MapReduce Programming) In your WordCount `.jar` job output directory on HDFS, what are `_SUCCESS` and `part-r-00000`? Why do custom Hadoop keys implement `WritableComparable`?**  
**Answer:** **`_SUCCESS`** is an empty 0-byte marker created only if the entire job finished cleanly; **`part-r-00000`** contains the output of Reducer `0` (if `numReduceTasks=0`, mappers write `part-m-00000`). Custom value types implement **`Writable`** (compact binary serialization for network/disk), while **keys** must implement **`WritableComparable`** so Hadoop can both serialize *and compare/sort* them during Shuffle & Sort!

**L4. (`Exp 4` — HiveQL) Compare a Managed (`Internal`) vs. External Hive table, and `PARTITIONED BY` vs. `CLUSTERED BY` (Bucketing).**  
**Answer:** Dropping a **Managed** table deletes *both* metastore schema AND HDFS files; dropping an **`EXTERNAL`** table removes *only* metadata, leaving underlying HDFS files safe! **Partitioning** splits low-cardinality columns (`year`, `state`) into separate HDFS subdirectories for fast directory pruning; **Bucketing (`CLUSTERED BY`)** hashes high-cardinality columns (`user_id`) into a fixed number of bucket files within each partition for balanced distribution and map-side bucketed joins.

**L5. (`Exp 5` — Stream Algorithms) In your Bloom Filter / DGIM / FM Python lab program, how do you verify your algorithm works without storing the whole raw stream in a giant list?**  
**Answer:** Maintain only the bounded state object—an $n$-bit integer/boolean array (Bloom Filter), a deque of at most $\le 2\log_2 N$ bucket tuples `(end_ts, size)` (DGIM), or an integer `max_zeros` variable across independent hashes (FM)—feeding stream elements one-by-one from a generator/iterator and comparing the final approximate output against an independent ground-truth checker *only* during testing validation!

**L6. (`Exp 6` — Apache Spark) Explain what `rdd.cache()` / `persist()` does, compare Narrow vs. Wide Transformations, and explain why MLlib uses Parallel FP-Growth instead of Apriori.**  
**Answer:** **`cache()`** (`MEMORY_ONLY` default) keeps computed RDD partitions in executor RAM across iterations instead of recomputing from HDFS every pass. **Narrow transformations** (`map`, `filter`) compute each output partition from *1* input partition with zero network shuffle; **Wide transformations** (`groupByKey`, `reduceByKey`, `join`) trigger an expensive cross-node **shuffle**! MLlib uses **Parallel FP-Growth** because it discovers frequent itemsets in ~2 scans using a compact prefix **FP-Tree**, avoiding Apriori's exponential candidate generation and repeated full dataset scans.

**L7. (`Exp 7` — SM Tools & Metrics) Which metrics would you extract first for a brand audit in Netlytic / Meta Business Suite / GA4, and how has "Bounce Rate" changed in GA4?**  
**Answer:** Extract Reach vs. Impressions, Engagement Rate (`Likes+Comments+Shares / Reach` or `Followers`), Virality/Share Rate, CTR, and sentiment/conversion rate. In **GA4**, Bounce Rate is now **`100% - Engagement Rate`** (so a user reading one long blog post for `2 minutes` without clicking a second page is an *Engaged Session*, not a bounce!).

**L8. (`Exp 8` — Sentiment Model) Write the exact logic distinguishing a TextBlob vs. VADER social-media classifier on tweets like `"OMG best concert EVERR!! 😍🔥"`.**  
**Answer:** In **TextBlob**, stripped punctuation/emojis yield moderate positive polarity (`blob.sentiment.polarity`) but ignore capitalization and emoji emphasis. In **VADER** (`SentimentIntensityAnalyzer().polarity_scores(text)`), ALL-CAPS `"EVERR"`, `"!!"`, and positive emojis boost intensity, emitting `compound` closer to `+1` (`>= 0.05 -> Positive`, `<= -0.05 -> Negative`, else `Neutral`).

**L9. (`Exp 9` — Structure-Based SMA) Given a Twitter retweet/reply graph in NetworkX, which metric finds: (a) most viral broadcaster (`reach speed`), (b) cross-circle bridge (`broker`), and (c) VIP endorsed by VIPs?**  
**Answer:** (a) High **Closeness Centrality** / high **Out-Degree**; (b) High **Betweenness Centrality** (or spanning **Structural Holes**); (c) High **Eigenvector Centrality** / **PageRank** (`nx.pagerank(G)`).

**L10. (`Exp 10` — Community Detection) When would your lab implementation use `nx.community.louvain_communities(G)` vs. `nx.community.k_clique_communities(G, k=3)`?**  
**Answer:** Use **Louvain** when you want every single node cleanly partitioned into non-overlapping communities quickly by maximizing Modularity $Q$ on large graphs; use **CPM (`k_clique_communities`)** when real users legitimately belong to **multiple overlapping groups** simultaneously and dense triangle cores matter more than assigning stray degree-1 nodes.

**L11. (`Exp 11*` — Microproject Architecture) Defend a Microproject pipeline (`e.g., Live Twitter/News Sentiment + Geo/Trending Dashboard`). How do you prevent data loss, handle duplicates, and compute sliding metrics?**  
**Answer:** Use **Apache Kafka** (replicated partitioned durable buffer) feeding **Spark Structured Streaming** with **checkpointing** for fault recovery; use **Bloom Filters / deduplication keys** or stateful watermarks for late/duplicate events; run **VADER/TextBlob** + **Decaying Windows** for live topic scores; sink aggregates to **MongoDB/Cassandra/Hive** and visualize via **Kepler.gl / Plotly** without calling deprecated Fusion Tables or Alexa APIs!

**L12. (`PR & OR` Cross-Check) What is the difference between `reduceByKey` and `groupByKey` in Spark?**  
**Answer:** `groupByKey` shuffles *all* raw `(key, value)` records across the network before aggregating (high network/memory pressure, risking OOM!). **`reduceByKey`** performs **local map-side combining** on each partition *first* (just like a Hadoop Combiner!) before shuffling much smaller partial totals.

**L13. (`PR & OR` Cross-Check) In Hadoop MapReduce vs. Spark, why might Spark STILL take time if an action fails?**  
**Answer:** Although Spark recovers lost partitions via **RDD Lineage (DAG recomputation)** rather than replicating every intermediate step across nodes like HDFS, if a wide-shuffle ancestor fails without checkpointing (`checkpoint()`), Spark may recompute a long dependency chain from upstream input splits.

**L14. (`PR & OR` Cross-Check) If an examiner asks *"Which part of our college syllabus PDF was missing from the lecture slides, and how did you verify it?"*, give 3 sharp examples!**  
**Answer:**
1. **Module 2 (`2.1`):** *Combiners* and *Coping With Node Failures* (verified via `hadoop.apache.org` & Dean & Ghemawat 2004).
2. **Module 3 (`3.2`):** *Reservoir Sampling (Algorithm R)*, *Bloom Filter FPR derivation*, and *Cost of Exact Counts ($\Omega(N)$)* (verified via `mmds.org` & NIST).
3. **Module 4 (`4.1`–`4.3`) & Module 6 (`6.2`):** *Social Media Landscape, Need for SMA, Small vs. Large Orgs, Structural Holes, Diameter, PageRank Teleportation formula, Local vs. Global Search, Big Data Applications & Louvain (`Exp 10`)* (verified via Burt 1992, MMDS Ch. 5, NetworkX docs, Blondel et al. 2008).
