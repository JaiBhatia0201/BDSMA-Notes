# BDSMA Syllabus Inventory and Topic Coverage Map

**Subject:** Big Data and Social Media Analytics (BDSMA)  
**Official College Course (Authoritative Syllabus):** **Vivekanand Education Society's Institute of Technology (VESIT)**, Dept. of Computer Engineering (Autonomous Institute affiliated to University of Mumbai) — **Final Year B.E. (Computer Engineering) Batch 2023–2027 (2026 'NEP & Autonomy' Scheme)**, **Course Code `26CMPC71`: Big Data and Social Media Analytics** (3 Theory hrs + 2 Practical hrs/week; Theory End-Sem 60 + Mid-Term 20 + CA 20; Lab Term Work 25 + **Practical & Oral [`PR & OR`] 25 Marks**).  
**Legacy Context in Slide Decks:** Slide 2–6 of `ch 01 A` still show screenshots of the older MU `CSC702: Big Data Analytics` syllabus, while the actual taught syllabus across Modules 1–6 matches **`26CMPC71`**.  
**Primary Professor / Compiler Credit Observed:** Dr. Rohini Temkar (credited across Modules 1, 2, 4, 5, and 6; select screenshots in Module 1A/Module 2 NoSQL show VESIT / Abha Tewari context).  
**Last Inventory Update:** 2026-11-19 (Updated with Official `26CMPC71` Syllabus PDF)

---

## 0. Official `26CMPC71` Syllabus Alignment & Lab Viva (`PR & OR`) Map

Source: `Final year B. E. (Computer Engineering) (Sem-VII & VIII) Batch  [2023-2027] (2026 ‘NEP & Autonomy’ Scheme).pdf` (pp. 10–18 in original booklet; PDF pages 1–9).  
**Prerequisites listed in official syllabus:** Graph Theory, Data Mining, Python/R programming.  
**Total Theory Hours:** 39 hours across 6 modules (`CO1`–`CO6`).

| Official Module | CO & Hrs | Official Syllabus Topics (`26CMPC71`) | Primary Slide Deck(s) | Official Syllabus Items Missing or Weak in Slides (Must Cover in Notes) |
|---|---|---|---|---|
| **1. Introduction to Big Data and Hadoop** | `CO1` (04 hrs) | **1.1** Intro to Big Data (characteristics, types), Traditional vs. Big Data business approach, Concept of Hadoop, Core Hadoop Components, Hadoop Ecosystem.<br>**1.2** Distributed File Systems: Physical Organization of Compute Nodes, Large Scale File-System Organization. | `ch 01 A Introduction to Big Data.pptx.pdf`, `Module_ 01 B Introduction_to_Hadoop.pptx.pdf`, plus `Module _02 Hadoop...` Slides 3–9 (DFS Physical/Large-Scale Org) | `1.2` DFS Physical Organization & Large-Scale File-System Organization live primarily in `Module _02` Slides 3–9 and `Module_ 01 B` Slides 52–60, 84–91; we will integrate both cleanly in Module 1! |
| **2. Hadoop HDFS, MapReduce and NoSQL** | `CO2` (08 hrs) | **2.1 MapReduce:** Map Tasks, Grouping by Key, Reduce Tasks, **Combiners**, Details of MapReduce Execution, **Coping With Node Failures**.<br>**2.2 Algorithms Using MapReduce:** Matrix-Vector Multiplication, Relational-Algebra Operations, Selections, Projections, Union, Intersection, Difference.<br>**2.3 NoSQL Data Architecture Patterns:** Key-value, Graph, Column family (Bigtable), Document, Variations of NoSQL patterns, NoSQL Case Study. | `Module _02 Hadoop HDFS and Mapreduce.pptx.pdf`, `Mod 2_NoSQL.pptx.pdf` | **Combiners** and **Coping With Node Failures** are explicitly required by `2.1` but missing from slides! Also slides cover Natural Join, Grouping & Aggregation, and 2-step Matrix Multiplication (plus 1-step in MU Qs) — keep all of these and add Combiners & Node Failures. |
| **3. Mining Data Streams** | `CO3` (07 hrs) | **3.1 Stream Data Model:** DSMS, Stream Sources, Stream Queries, Issues in Stream Processing.<br>**3.2** **Sampling Data techniques in a Stream**, Filtering Streams: **Bloom Filter with Analysis**, Counting Distinct Elements, Count Distinct Problem, Flajolet-Martin, DGIM. | `BDA_Mod 3 Mining Data Streams.pptx.pdf` | **Reservoir Sampling** (varying/fixed-size stream sampling), **Bloom Filter mathematical FPR analysis**, and **Cost of Exact Counts proof** ($\Omega(N)$) are missing in slides; Decaying Windows is covered in slides & retained. |
| **4. Social Network Structure, Measures & Visualization** | `CO4` (08 hrs) | **4.1** Core Characteristics of SM, Types of SM, **Social media landscape**, **Need for SMA**, **SMA in small & large organizations**, Seven Layers of SMA, Types of SMA, SMA Cycle, Challenges.<br>**4.2** Basics of Social Network Structure (Nodes, Edges & Tie), Measures (Degree Distribution, Density, Connectivity, Centralization, Tie Strength & Trust), Visualization (Layout, Visualizing features, Scale Issues).<br>**4.3** Social Media Network Analytics, Types of Networks, Tools, Clustering of Social network graphs, Direct discovery of communities, Clique Percolation Algorithm. | `Mod4 Social Network Structure...pdf` (actually 4.1), `Mod4B.pptx.pdf` (4.2), `Mod4d.pdf` + `Mod4C.pdf` (4.3) | **Social Media Landscape**, **Need for SMA**, and **SMA in small & large organizations** are explicitly in `4.1` (and Slide 33 TOC) but omitted from slides! Also **Dyads/Triads**, **Structural Holes**, **Diameter**, and **Louvain method** (from Lab Exp 10) need clear explanations. |
| **5. Social Media Text, Action & Hyperlink Analytics** | `CO5` (06 hrs) | **5.1 Text Analytics:** Types of SM Text, Purpose, Steps, Tools.<br>**5.2 Action Analytics:** What is Actions Analytics, Common SM Actions, Tools.<br>**5.3 Hyperlink Analytics:** Types of Hyperlinks, Types of Hyperlink Analytics, Hyperlink Analytics Tools, Social Media Analytics Tools. | `ch 03 A Text Analytics.pptx.pdf`, `ch 03 B Action Analytics.pptx.pdf`, `ch 03 C Hyperlink Analytics.pptx.pdf` | All 3 textbook case studies (`Flyertalk`/`Online Customer Opinions`, `Cover-More Group`, `Viral YouTube Videos`) are empty stubs; **Co-linking vs. Co-citation** and **Inter- vs. Intra-linking** need disambiguation. |
| **6. Social Media Location, Search Engine Analytics and Applications** | `CO6` (06 hrs) | **6.1 Location Analytics:** Sources, Categories, Privacy Concerns, Tools.<br>**6.2 Search Engine Analytics:** Types of Search Engines, Search Engine Analytics, Tools, **PageRank algorithm**, **Big data and social media analytics applications**. | `ch 04 A Location Analytics.pptx.pdf`, `ch 04 B Search Engine Analytics.pptx.pdf`, `ch 04 -Page Rank n HITS.pptx.pdf` | **Teleportation/Taxation formula** for PageRank is missing; **Big Data & Social Media Analytics Applications** (explicit in `6.2`) needs a dedicated synthesis; **HITS** (in PPT filename, though not in `6.2` text) will be included as a concise bonus section; **Local vs. Global Search Engines** & **Owl Bus** stub need filling. |

### Official Lab Experiments Mapped for Practical & Oral (`PR & OR`, 25 Marks) Viva

Since the course includes a **25-mark Practical & Oral (`PR & OR`)** component, each module's notes will also link relevant lab concepts:
- **Exp 1 (`CO1` $\to$ Mod 1):** Hadoop HDFS Practical (HDFS CLI: `put`/`copyFromLocal`, `get`/`copyToLocal`, `rm`, `mv`, `ls`, `cat`; installing & navigating HDFS).
- **Exp 2 (`CO1, CO2` $\to$ Mod 2):** NoSQL Setup & Operations (`MongoDB` / `Cassandra` / `HBase` / `Hypertable` CRUD across key-value, column-family, document stores).
- **Exp 3 (`CO2` $\to$ Mod 2):** Hadoop MapReduce Programming (WordCount, Matrix multiplication, Aggregates, Joins, Sorting, Searching).
- **Exp 4 (`CO2` $\to$ Mod 2):** HIVE Database & Descriptive Analytics (HiveQL queries, group-by, aggregations).
- **Exp 5 (`CO3` $\to$ Mod 3):** Data Stream Algorithms (implementing DGIM, Bloom Filter, or Flajolet–Martin).
- **Exp 6 (`CO3` $\to$ Mod 3):** Apache Spark — Iterative Algorithms & Frequent Itemset Mining.
- **Exp 7 (`CO4, CO5` $\to$ Mod 4 & 5):** Study of Social Media Platforms & Tools (FB Insights, GA, Netlytic, Brand24; page/post/member engagement metrics).
- **Exp 8 (`CO5` $\to$ Mod 5):** Content-Based Social Media Analytics Model (topic, issue, trend, sentiment/opinion analysis).
- **Exp 9 (`CO4, CO6` $\to$ Mod 4 & 6):** Structure-Based Social Media Analytics Model (community detection, influencer analysis).
- **Exp 10 (`CO4, CO6` $\to$ Mod 4):** Community Detection / Clustering Algorithm (Clique Percolation, **Louvain method**).
- **Exp 11* Microproject (`CO1–CO6` $\to$ Mod 6 Applications):** Streaming pipeline (Kafka/Flume + Hive/PySpark), Recommendation System, or SpatioTemporal Data Analytics.

*(Note: The official syllabus also lists **Self-Learning Topics (`Content Beyond Syllabus`, 60 hrs)** covering PySpark RDDs/DataFrames/Spark Streaming, Twitter Sentiment with TextBlob/VADER, Kafka + Flume real-time streaming, Google Analytics Academy, NPTEL Big Data/SNA courses, and `mpi4py`.)*

---

## 1. File Inventory & Readability Status

All **15 PDF files** across `module_1` through `module_6` (**1,395 total slides/pages**) were opened and visually inspected (page screenshots + OCR text layer). **Zero files were unreadable or truncated.**

| Module | File Path (relative to `BDSMA/`) | Pages | Readability | Title Shown Inside Deck | Compiler / Author Credit |
|---|---|---:|---|---|---|
| Module 1 | `module_1/ch 01 A Introduction to Big Data.pptx.pdf` | 136 | Readable (136/136) | `BIG DATA ANALYTICS` / `Module 1: Introduction to Big Data and Hadoop` | `compiled by Dr. Rohini Temkar` |
| Module 1 | `module_1/Module_ 01 B Introduction_to_Hadoop.pptx.pdf` | 93 | Readable (93/93) | `Chapter 1: Introduction to Hadoop` | `compiled by Dr. Rohini Temkar` (p. 40–41, 83) |
| Module 2 | `module_2/Module _02 Hadoop HDFS and Mapreduce.pptx.pdf` | 184 | Readable (184/184) | `CHAPTER 2: HADOOP HDFS & MAPREDUCE` | `Compiled by Dr. Rohini Temkar` (p. 4) |
| Module 2 | `module_2/Mod 2_NoSQL.pptx.pdf` | 214 | Readable (214/214) | `MODULE 2: NOSQL` *(p. 2 says `Module 3- Contents`)* | `Compile by Dr. Rohini Temkar` (p. 1) |
| Module 3 | `module_3/BDA_Mod 3 Mining Data Streams.pptx.pdf` | 135 | Readable (135/135) | `Big Data Analytics — Module 3: Mining data Streams` | None printed *(cites MMDS / Datar et al.)* |
| Module 4 | `module_4/Mod4 Social Network Structure, Measures & Visualization.pdf` | 193 | Readable (193/193) | `Module 4: Social Media Analytics: An Overview` (`Chapter 1`) | `Compiled by Dr. Rohini Temkar` |
| Module 4 | `module_4/Mod4B.pptx.pdf` | 175 | Readable (175/175) | `Chapter 2: Social Media Analytics: An Overview` *(actual content: Social Network Structure, Measures & Visualization)* | `Compiled By Dr. Rohini Temkar` |
| Module 4 | `module_4/Mod4C.pdf` | 45 | Readable (45/45) | `Module 4: Social Network Structure, Measures & Visualization` *(actual content: Clustering & Clique Percolation Method)* | None printed |
| Module 4 | `module_4/Mod4d.pdf` | 29 | Readable (29/29) | `CHAPTER 2: SOCIAL NETWORK STRUCTURE, MEASURES AND VISUALIZATION — SUBTOPIC: SOCIAL MEDIA NETWORK ANALYTICS` | `Compiled By Dr. Rohini Temkar` |
| Module 5 | `module_5/ch 03 A Text Analytics.pptx.pdf` | 30 | Readable (30/30) | `CHAPTER 3: SOCIAL MEDIA TEXT ANALYTICS` | `Compiled by Dr. Rohini Temkar` |
| Module 5 | `module_5/ch 03 B Action Analytics.pptx.pdf` | 24 | Readable (24/24) | `CHAPTER 5: SOCIAL MEDIA ACTIONS ANALYTICS` | `Compiled by Dr. Rohini Temkar` |
| Module 5 | `module_5/ch 03 C Hyperlink Analytics.pptx.pdf` | 36 | Readable (36/36) | `Module 5: Social Media Text, Action & Hyperlink Analytics` | `Compiled By Dr. Rohini Temkar` |
| Module 6 | `module_6/ch 04 A Location Analytics.pptx.pdf` | 38 | Readable (38/38) | `CHAPTER 4: Social Media Location Analytics` | `Compiled By Dr. Rohini Temkar` |
| Module 6 | `module_6/ch 04 B Search Engine Analytics.pptx.pdf` | 37 | Readable (37/37) | `CHAPTER 9: Search Engines Analytics` | `Compiled by Dr. Rohini Temkar` |
| Module 6 | `module_6/ch 04 -Page Rank n HITS.pptx.pdf` | 26 | Readable (26/26) | `Module 5: Social Media Location, Search Engine Analytics and Applications — 1) Page Rank Algorithm` | `Compiled By Dr. Rohini Temkar` |
| **Total** | **15 files** | **1,395** | **15/15 Readable** | — | — |

### Output Notes Status Tracker

| Deliverable | Path | Status |
|---|---|---|
| Syllabus & Topic Map | `VIVA_NOTES/00_SYLLABUS_AND_TOPIC_MAP.md` | `[x]` Created (Phase A) |
| External Source Register | `VIVA_NOTES/SOURCE_REGISTER.md` | `[x]` Created (Phase A) |
| Module 1 Notes | `VIVA_NOTES/Module_1_Notes.md` | `[x]` Covered & Verified |
| Module 2 Notes | `VIVA_NOTES/Module_2_Notes.md` | `[x]` Covered & Verified |
| Module 3 Notes | `VIVA_NOTES/Module_3_Notes.md` | `[x]` Covered & Verified |
| Module 4 Notes | `VIVA_NOTES/Module_4_Notes.md` | `[x]` Covered & Verified |
| Module 5 Notes | `VIVA_NOTES/Module_5_Notes.md` | `[x]` Covered & Verified |
| Module 6 Notes | `VIVA_NOTES/Module_6_Notes.md` | `[x]` Covered & Verified |
| Final Viva Question Bank | `VIVA_NOTES/Final_Viva_Question_Bank.md` | `[x]` Covered & Verified |
| Quick Revision Notes | `VIVA_NOTES/QUICK_REVISION_NOTES.md` | `[x]` Covered & Verified |

**Status Legend:** `[ ]` Not Started | `[~]` Partially Covered | `[x]` Covered & Verified

---

## 2. Cross-Module Structural Findings & Major Gaps

1. **Filename vs. Content Mismatches:**
   - `module_4/Mod4 Social Network Structure, Measures & Visualization.pdf` actually teaches **Social Media Analytics: An Overview** (Chapter 1, including the 7 Layers and SMA Cycle) — zero network graph metrics appear in it.
   - `module_4/Mod4B.pptx.pdf` carries a leftover title *"Chapter 2: Social Media Analytics: An Overview"* on Slide 1, while actually teaching **Social Network Structure, Measures & Visualization**.
   - `module_6/ch 04 -Page Rank n HITS.pptx.pdf` is titled `Page Rank n HITS`, yet **HITS (Hyperlink-Induced Topic Search / Hubs & Authorities) is completely absent** from all 26 slides.
2. **Repeated / Duplicated Slides Across Decks:**
   - `Mod4 Social Network Structure...pdf` Slides **136–193** repeat Slides **77–134** verbatim (and Slides 80–82 appear three times).
   - Several decks contain duplicate slides from animation exports or duplicated question slides (`Mod4C` pp. 14–28; `Mod 2_NoSQL` pp. 161–162 & 213–214; `Module _02 Hadoop` pp. 158/161, 177/179, 182/184; `BDA_Mod 3` p. 88/97; `Mod4B` pp. 66/70, 99/100; `ch 04 -Page Rank n HITS` pp. 22/24/25).
3. **Topics Listed in Contents/Filenames but Omitted in Slides:**
   - **Module 2 (Hadoop/MapReduce):** Combiners, Coping with Node Failures, One-Step Matrix Multiplication (listed in TOC & university questions), Hadoop Limitations (partially covered in Module 1B).
   - **Module 3 (Streams):** Reservoir Sampling / Varying the Sample Size (listed in TOC & Slide 37), Cost of Exact Counts proof, Bloom filter false-positive probability formula/derivation, Concept Drift/Evolution, Heavy Hitters & Frequent Itemsets (only named on Slide 25).
   - **Module 4 (Network Analytics):** Dyads & Triads details (`Mod4B` Slide 31 stub), Structural Holes & Diameter (`Mod4d` Slides 17–18 list only), worked answers to `Mod4B` & `Mod4C` unsolved exercises.
   - **Modules 5 & 6 (Case Studies & Tools):** All 6 textbook case studies (`Tapping into Online Customer Opinions`, `Cover-More Group`, `Hyperlinks and Viral YouTube Videos`, `The Underground Campaign that Scored Big`, `Do Social Media Networks Reflect Social Culture?`, `the "Owl Bus"`) are empty 3-bullet placeholders (`The Problem / The Solutions / The Results`). `ch 04 B` lists `Local vs. Global Search Engines` without definitions; `ch 04 -Page Rank n HITS` omits the **Teleportation/Taxation formula** and **HITS**.

---

## 3. Detailed Module-Wise Topic Map

### Module 1: Introduction to Big Data and Hadoop
**Files:** `module_1/ch 01 A Introduction to Big Data.pptx.pdf` (136 pp.), `module_1/Module_ 01 B Introduction_to_Hadoop.pptx.pdf` (93 pp.)

#### Part 1A — Introduction to Big Data (`ch 01 A Introduction to Big Data.pptx.pdf`)
- `[x]` **1A.1 Course Syllabus & Big Data Ecosystem Overview** (pp. 1–13)
  - *Terms/Tools:* CSC702 syllabus, Apache Hadoop, HDFS, YARN, MapReduce, Apache Kafka, Spark (Spark SQL, Spark Streaming, GraphX, MLlib), Hive, Pig, Mahout, ZooKeeper, Storm, Solr/Lucene, Flume, Sqoop, HBase, Cassandra, MongoDB `mapReduce`.
- `[x]` **1A.2 Why Big Data & Global Data Growth Statistics** (pp. 14–20, 40–43, 60–61)
  - *Data/Claims verified:* `>80%` unstructured data; `70%` user-generated; `2.5 quintillion bytes/day` (IBM ~2012) vs. `402.74 million TB/day` (~2024 IDC/Statista); `180+ ZB` by 2025 chart; "Data Never Sleeps"; "181 million years to download"; Single View of the Customer diagram (p. 41); Peter Sondergaard & Chris Lynch quotes.
- `[x]` **1A.3 Formal Definitions & Data Size Scale** (pp. 58–59, 62–64, 70–83)
  - *Definitions:* Gartner 3Vs definition, Oracle definition, IBM definition, McKinsey definition (p. 111).
  - *Scale Perspective & Units:* Bit, Nibble, Byte, KB, MB, GB, TB ("Terrabyte" typo), PB, EB, ZB, YB, plus informal `Brontobyte` ($10^{27}$) & `Geopbyte` ($10^{30}$) — **verified SI 2022 (`ronna`, `quetta`) and binary ($1024$) vs decimal ($1000$) units**.
- `[x]` **1A.4 Characteristics of Big Data (3Vs, 4Vs, 5Vs, Dimensions, 10Vs)** (pp. 21–22, 81–97, 107)
  - *Dimensions:* Volume, Velocity, Variety ("Varity" typo p. 84), Veracity, Value, plus Valence, Validity, Variability, Volatility, Vulnerability, Visualization (10Vs construction-context chart p. 97).
  - *Model shift:* Old Model (few producers, many consumers) vs. New Model (all produce and consume, p. 89).
- `[x]` **1A.5 Sources & Types of Big Data** (pp. 65–69, 98–106)
  - *Sources:* Text, Image, Audio, Video; IoT, Social Media, Web, Machine Logs, DBs, Cloud, Documents, Archives, ERP, Financial, Mobile Apps.
  - *Types:* Big Data vs. Small Data table (p. 99); Structured vs. Unstructured vs. Semi-Structured Data (XML example p. 105; ~20% vs ~80% Gartner split p. 100); Data $\to$ Explore $\to$ Knowledge $\to$ Value (p. 106).
- `[x]` **1A.6 Traditional vs. Big Data Business Approach & Data Science Technologies** (pp. 47–50, 98, 108–120)
  - *Concepts:* Traditional BI (Exadata, Teradata, structured repeatable analysis) vs. Big Data Approach (MPP, shared-nothing, scale-out, iterative/exploratory); Complexity vs. Business Value curve (p. 98); Accelerating Time-to-Value chart (p. 109).
  - *5 Data Science Technologies:* Traditional BI, Data Modeling, Statistical Application, Predictive Analysis, Data Mining ("Think & Answer" class scenarios p. 117 solved); Analytics pipeline (Storage $\to$ Formatting/Cleaning $\to$ Understanding $\to$ Access/Integration $\to$ Analysis $\to$ Visualization, p. 120).
- `[x]` **1A.7 Case Studies & Use Cases of Big Data Solutions** (pp. 26–39, 44–57, 121–136)
  - *Case Studies:* Netflix (recommendations = ~80% activity, \$1B+ annual retention savings verified via Gomez-Uribe & Hunt 2015, thumbnail personalization via Contextual Bandits, 2023 subscriber snapshot), Delivery/Routing Ops (p. 34), IMDb Movie Reviews sentiment & 1–10 ratings (pp. 44–57), NYT/Log Files Trend Detection & Ad Segmentation (p. 122), Car Insurance pricing via CRM + Social Sentiment (pp. 123–124), British Telecom Alarms Explorer Server (~25,000 devices, RCA, 15-min fault prediction, anomaly detection, p. 125).
  - *Challenges & Tools:* 8 challenges (Capture, Curation, Storage, Search, Sharing, Transfer, Analysis, Visualization, pp. 58, 127–128); Hadoop, MapReduce, HDFS, Hive, Pig overview (pp. 23–25, 129–133); Big Data timeline & landscape (pp. 134–135).

#### Part 1B — Introduction to Hadoop (`Module_ 01 B Introduction_to_Hadoop.pptx.pdf`)
- `[x]` **1B.1 Distributed Systems Motivation, History & Core Philosophy** (pp. 1–21)
  - *Concepts:* Processor-bound traditional systems vs. scale-out distributed systems; challenges (programming complexity, finite bandwidth, partial failures); Doug Cutting & Michael Cafarella (2005 Nutch, Yahoo, 2006 Apache); Google origins (GFS 2003 $\to$ HDFS, MapReduce 2004 $\to$ MapReduce, Bigtable 2006 $\to$ HBase).
  - *Assumptions & Principles:* Hardware will fail; batch/high-throughput over low latency; GB–TB files; write-once-read-many; **"Moving Computation is Cheaper than Moving Data"**; Scalable, Cost-effective (commodity hardware), Flexible (schema-less), Fault-tolerant.
  - *Whiteboard Diagrams:* 8-node cluster (p. 3), Hadoop core stack (p. 4), Hadoop mind map (p. 5), Data processing flow (p. 6), Ecosystem layers (p. 7/14), Pipeline sketch (p. 8).
- `[x]` **1B.2 Hadoop Ecosystem & Processing Stages** (pp. 22–51)
  - *4 Stages:* 1. Ingest (`Sqoop`, `Flume`, `Kafka`) $\to$ 2. Store (`HDFS`, `HBase`) $\to$ 3. Process (`MapReduce`, `Spark`, `Pig`, `Hive`) $\to$ 4. Analyze/Explore (`Impala`, `Search`, `Mahout`) + `Oozie`, `ZooKeeper`, `Hue`.
  - *Ecosystem Components:* MapReduce Word Count trace (pp. 25–29), JobTracker/TaskTracker overview (pp. 30–32), HDFS NameNode/DataNode (p. 34), HBase (pp. 35–36), Apache Pig & Pig Latin script (pp. 38–39), Apache Hive & HQL + **Hive vs. Pig table** (pp. 40–41), Mahout (CF, Clustering, Classification, Frequent itemset mining — typo `"missing"` fixed, pp. 42–43), Apache Spark ("100x faster" in-memory qualified, p. 44), Sqoop (p. 45, Attic 2021 noted), Flume (Source-Channel-Sink, pp. 46–48, 2023 termination noted), Hue (p. 49), Oozie Workflow vs. Coordinator (p. 50), ZooKeeper (p. 51).
- `[x]` **1B.3 Physical Cluster Architecture, HDFS & Hadoop 1.x Daemons** (pp. 52–73)
  - *Terminology:* Cluster, Node, Daemon; HDFS layered over Native OS FS (`ext3/ext4/xfs`) and Disk; 3 components (Storage, Processing, Resource Management).
  - *HDFS Storage & Retrieval:* 128 MB blocks (64 MB in 1.x), default 3x replication, metadata block mapping, client read/write flow (pp. 56–60).
  - *Hadoop 1.x Daemons:* Master (`NameNode` — `FsImage` & `EditLog`; `Secondary NameNode` — 1-hr checkpointing clarified vs backup/HA; `JobTracker`) and Slaves (`DataNode` — 3-sec heartbeat; `TaskTracker`).
  - *Hadoop 1.x Limitations:* Single NameNode SPOF, MapReduce-only, MapReduce handles resource management, batch-only (no real-time/streaming), ~4,000 node limit (p. 73).
- `[x]` **1B.4 Hadoop 2.x / 3.x & YARN Architecture** (pp. 74–83)
  - *YARN Components:* `ResourceManager` (`Scheduler` + `ApplicationsManager`), `NodeManager` (per-node slave, auxiliary shuffle service), `ApplicationMaster` (1 per app), `Container` (RAM/CPU/disk unit).
  - *Hadoop 1 vs. Hadoop 2 Table* (p. 83) — clarified Active/Standby NameNodes vs Secondary NameNode, plus Hadoop 3.x updates (Erasure Coding, >2 NameNodes).
- `[x]` **1B.5 Rack Awareness & Exam Questions** (pp. 84–93)
  - *Rack Awareness:* Rack (40–50 nodes/switch); NameNode tracks Rack IDs; Replication factor 3 placement rule (clarified Slide 89 vs official `HdfsDesign.html` 1-local + 2-remote-rack policy); 300 MB = `A(128)+B(128)+C(44)` 3-rack diagram (p. 90).
  - *University & Important Questions:* MU Comp-SH16 & IT-FH16 + 6 study questions (pp. 92–93).
- `[x]` **1B.6 Distributed File Systems: Physical Organization & Large-Scale File-System Organization** (`26CMPC71` Topic 1.2 — cross-referenced from `module_2/Module _02 Hadoop HDFS and Mapreduce.pptx.pdf` pp. 3–9 + `Module_ 01 B` pp. 52–60, 84–91 + Lab Exp 1 HDFS CLI)
  - *Concepts:* 2-level cluster switch/rack topology, commodity compute nodes & MTTF failure math, 1 Gbps network bottleneck (10 TB $\approx$ 1 day), chunk servers (`64/128 MB`, 2x–3x rack-aware replication, NameNode metadata), *"Bring computation to the data"*, and HDFS practical CLI commands (`hdfs dfs -put/-get/-ls/-rm/-mv/-cat` for `PR & OR` viva).

---

### Module 2: Hadoop HDFS, MapReduce Algorithms, and NoSQL
**Files:** `module_2/Module _02 Hadoop HDFS and Mapreduce.pptx.pdf` (184 pp.), `module_2/Mod 2_NoSQL.pptx.pdf` (214 pp.)

#### Part 2A — HDFS, MapReduce Execution & Algorithms (`Module _02 Hadoop HDFS and Mapreduce.pptx.pdf`)
- `[x]` **2A.1 Cluster Architecture, Bottlenecks & DFS Foundations** (pp. 1–9)
  - *Concepts:* 2-level switch/rack topology (1,000 nodes/rack), MTTF failure math (1000 days/server $\to$ 1 failure/day per 1000 servers), 1 Gbps network bottleneck (10 TB $\approx$ 1 day), DFS chunk servers (`64/128 MB`, 2x–3x replication, compute on chunk servers), NameNode.
- `[x]` **2A.2 MapReduce Programming Model, Data Flow, Combiners, Fault Tolerance & Java Implementation** (`26CMPC71` Topic 2.1; pp. 10–36)
  - *Concepts:* Formal signatures `Map(k,v) -> <k',v'>*`, `Reduce(k',<v'>*) -> <k',v''>*` (**verify value-order claim**); WordCount pseudocode & `"The doctor ate an apple..."` trace (**flag case-folding mismatch**); Master coordination & task counts (`M` vs `R`); DFS vs local FS intermediate storage.
  - *Required by `26CMPC71` Topic 2.1 (Omitted in Slides):* **Combiners** (mini-reducer / local aggregation optimization & associativity/commutativity condition) and **Coping With Node Failures** (Master failure, Map worker failure, Reduce worker failure, speculative execution / stragglers).
  - *Java Code & CLI:* `MyMapper`, `MyReducer`, `WordCount` Driver, `javac`/`jar`/`hadoop jar` commands (**fix syntax/brace/deprecated `new Job()` errors**).
- `[x]` **2A.3 Relational-Algebra Operations by MapReduce** (pp. 37–96)
  - `[x]` Selection $\sigma_C(R)$ (pp. 39–48) — *note $\delta$ vs $\sigma$ typo on p. 44*
  - `[x]` Projection $\pi_S(R)$ (pp. 49–60) — *note p. 50 cutoff & p. 59 diagram typo*
  - `[x]` Union $R \cup S$ (pp. 61–67)
  - `[x]` Intersection $R \cap S$ (pp. 68–71) — *note set vs multiset assumption & p. 70 `(t, NULL)` conflict*
  - `[x]` Difference $R - S$ (pp. 72–78)
  - `[x]` Natural Join $R \bowtie S$ (pp. 79–87) — *note equijoin vs natural join on `Employee`/`Assigned Departments`*
  - `[x]` Grouping & Aggregation $\gamma_X(R)$ (pp. 88–96) — *note SQL equivalence & `sum(C)` trace*
- `[x]` **2A.4 Matrix-Vector & Two-Step Matrix Multiplication by MapReduce** (pp. 97–134)
  - *Formulas:* $(Av)_i = \sum_{j=1}^n a_{ij}v_j$; $(AB)_{ik} = \sum_{j=1}^n a_{ij}b_{jk}$; sparse matrix CSV input format `(M, i, j, m_ij)`.
  - *Algorithms:* 1-step Matrix-Vector MR + worked $3\times 2$ example (`[16, 4, 7]`); 2-step Matrix-Matrix MR (`Map1/Reduce1` join on $J$, `Map2/Reduce2` sum on `(i,k)`) + worked $2\times 3 \times 3\times 2$ example (**correct $m_{23}n_{32}=6$ typo printed as `10` on pp. 129, 132**).
  - *Syllabus Gap:* **1-Step Matrix Multiplication**, **Combiners**, and **Coping with Node Failures** (listed in Slide 2 TOC & Slide 181 MU Question) are missing from the deck — add clear beginner-friendly coverage for viva!
- `[x]` **2A.5 Hadoop Ecosystem Deep Dive & Cloudera VM Lab Context** (pp. 135–184)
  - *Tools:* HDFS, Flume (`flume.conf` TwitterSource, MemChannel, HDFS sink — **note legacy channel/Twitter notes**), Sqoop (`import`, `export`, `list-databases` typo on p. 155, export arrow diagram error p. 152), Hive (HiveQL, **note Tez/Spark vs MR**), Pig (Pig Latin vs Hive table), Oozie, HBase (vs RDBMS table), Hue, Mahout (vs Spark), ZooKeeper.
  - *University Questions (p. 181):* MU FH-2016 COMP/IT & SH-2016 COMP; Cloudera QuickStart VM 5.13.0 Sqoop/MySQL/Hue photos (pp. 182–184).

#### Part 2B — NoSQL Databases & Big Data Solutions (`Mod 2_NoSQL.pptx.pdf`)
- `[x]` **2B.1 Database Fundamentals, SQL/RDBMS Pressures & ACID** (pp. 1–20)
  - *Types:* Centralized, Distributed (Homogeneous/Heterogeneous), Cloud (DBaaS: DynamoDB, Cosmos DB, Cloud SQL), Object-Oriented (`ObjectDB`), Hierarchical (`IMS`, `RDM`), Network (`TurboIMAGE`), Personal/Operational/Enterprise, Relational (Tuple, Attribute, Relation).
  - *RDBMS Pressures & ACID:* Atomicity, Consistency (banking transfer example p. 19 — **clarify invariant wording p. 18**), Isolation (concurrent schedule example p. 20), Durability.
- `[x]` **2B.2 NoSQL Introduction, History, Scale-Up vs. Scale-Out & Business Drivers** (pp. 21–45)
  - *Concepts:* Carlo Strozzi (1998), 2000–2009 timeline (Neo4j, Bigtable, CouchDB, Dynamo, Cassandra); RDBMS vs NoSQL comparison table (**fix p. 25 col 7 typo & p. 15/21 "homogeneous" confusion**); Scale-Up (vertical) vs Scale-Out (horizontal).
  - *4 Business Drivers:* Volume, Velocity, Variability (sparse columns / `ALTER TABLE` downtime), Agility (ORM impedance mismatch).
- `[x]` **2B.3 CAP Theorem & BASE Properties** (pp. 29–41)
  - *CAP Theorem:* Consistency, Availability (**fix p. 37 "success or failure" definition**), Partition Tolerance; CA vs CP vs AP classification (`RDBMS`, `MongoDB`/`HBase`/`Bigtable`, `Cassandra` + **tunable consistency note**).
  - *BASE:* Basically Available, Soft State, Eventually Consistent; Strong (ACID) vs Weak (BASE) consistency.
- `[x]` **2B.4 Four NoSQL Architectural Patterns** (pp. 46–167)
  - `[x]` **Key-Value Stores** (pp. 52–75): `put/get/delete/execute`, hash table pointers, relational-to-KV conversion (`Student`, `Employee`), Session Store & Shopping Cart architectures, **Snapchat/Snap Inc. & Amazon DynamoDB** + Zoom/Disney+ cases, `Redis`, `Riak`, `Memcached`, `Oracle NoSQL`.
  - `[x]` **Column-Family / Wide-Column Stores** (pp. 76–95): Row vs Column storage (**clarify relational columnar e.g. Vertica vs wide-column NoSQL e.g. Bigtable/HBase/Cassandra**), Keyspace $\to$ Column Family $\to$ Row Key $\to$ `(Name, Value, Timestamp)`, **Google Bigtable** Webtable case (`com.cnn.www`), **HBase** architecture (`HMaster`, `ZooKeeper`, `RegionServer`, `HDFS`), **Spotify** (Cassandra) & **Facebook** (HBase) cases.
  - `[x]` **Document-Oriented Stores** (pp. 96–115): JSON/BSON/XML documents, schema-on-read, `Artists/Albums/Genre` relational-to-document conversion (**fix p. 99/102 invalid JSON**), MongoDB model (`Database -> Collection -> Document`), embedding vs linking, `CouchDB`, `Couchbase`, `MongoDB`.
  - `[x]` **Graph Databases & Neo4j/Cypher** (pp. 116–167): Nodes, typed directed relationships, properties; index-free adjacency / multi-hop traversal; *Student–Course* 3-way comparison (Relational vs Document vs Graph, pp. 124–127); Fraud detection & Recommendation engines; **Neo4j Workspace Northwind walkthrough** & **Cypher (`twitter.cyp`)** (**clarify deprecated `ON ... ASSERT` vs Neo4j 5 `FOR ... REQUIRE`**).
- `[x]` **2B.5 Selecting Stores, Distributed Architectures & Distribution Models** (pp. 168–214)
  - *Store Selection:* Decision criteria for KV, Document, Column-Family, Graph (pp. 169–173).
  - *Shared Computing Architectures (`[DEWI92]`):* Shared RAM (graph traversals), Shared Disk (**fix p. 178 private vs shared memory contradiction**), Shared Nothing / MPP.
  - *Distribution Models:* Aggregate-oriented DBs; **Sharding** (Horizontal vs Vertical shards, shard keys); **Replication** (Master-Slave vs Peer-to-Peer, **clarify HBase vs Cassandra architecture**).
  - *Quizzes & University Questions:* 14 Q&A pairs (pp. 185–212, **flag p. 201 XPath/JSON mix-up**) + MU 2016–2019 questions (pp. 213–214, **note wrong header on p. 214**).

---

### Module 3: Mining Data Streams
**File:** `module_3/BDA_Mod 3 Mining Data Streams.pptx.pdf` (135 pp.)

- `[x]` **3.1 Data Stream Model, Challenges & DSMS Architecture** (pp. 1–27)
  - *Characteristics:* Real-time, continuous, unbounded, non-controllable arrival order, volatile (3Vs: Volume, Velocity, Volatility), Concept Drift & Concept Evolution. *(Flag swapped labels on p. 5 images.)*
  - *DSMS Architecture:* Generic model (Standing vs Ad-Hoc queries, Limited Working Storage, Archival Storage); Abstract DSMS (Input Stream Monitor/Regulator, Working/Summary/Metadata Storage, Query Repository, Query Processor); 6 query requirements (non-blocking, single-pass, etc.).
  - *Stream Queries & Applications:* One-time vs Continuous, Predefined vs Ad-Hoc; Network traffic/DoS, Financial stocks, Transaction logs/fraud, Sensor networks.
- `[x]` **3.2 Approximate Query Answering, Sliding Windows, Batching & Sampling** (pp. 28–40)
  - *Techniques:* Sliding Windows ($N$ elements), Batch Processing (bursty streams), Synopsis/Sketch/Histogram/Wavelet, Sampling.
  - *Sampling Fixed Proportion:* Search `(user, query, time)` biased-naive vs user-key hash sampling; hash bucket rule $a/b$ (**clarify 0-indexed `< a` vs `<= a`**).
  - *Syllabus Gap:* **Problem 2 — Fixed-Size Reservoir Sampling** (listed on Slides 2 & 37) is missing from slides — add full algorithm + proof intuition for viva!
- `[x]` **3.3 Filtering Streams — Bloom Filter** (pp. 41–60)
  - *Mechanics:* Bit array of size $n$, $k$ hash functions, $m$ elements in set $S$; $O(k)$ insert & query; **zero false negatives**, possible false positives.
  - *Formula & Examples:* Optimal $k = \frac{n}{m}\ln 2$ (**add missing FPR formula $p \approx (1 - e^{-km/n})^k$**); Wikipedia example (`n=18, k=3`), handwritten example (`m=5`, $h_1=x \bmod 5$, $h_2=(2x+3)\bmod 5$, inserts `9, 11`, queries `15, 16`); unsolved exercise (`K=8`, `x mod 8`, `(x+4) mod 8`); real-world applications (HBase HFiles, Bitly malicious URLs).
- `[x]` **3.4 Counting Ones in a Sliding Window — DGIM Algorithm** (pp. 61–103)
  - *Window & Rules:* Last $N$ bits; buckets store `(end timestamp, size = 2^j)`; 6 rules (1 or 2 buckets per power of 2, right boundary starts with `1`, non-decreasing sizes leftwards, expire when `end_time <= current_time - N`).
  - *Operations & Complexity:* Update/cascade merge on bit `1`; Query algorithm (sum all enclosed buckets + **1/2** of oldest overlapping bucket $\implies \le 50\%$ error); **$O(\log^2 N)$ space** (**clarify exponents vs sizes on p. 101**).
  - *Worked Examples & Corrections:* MMDS cascade (pp. 88–92), `N=24` examples (pp. 93–95, 98–103), unsolved `k=14` exercise (p. 100); **flag & correct p. 84 DGIM query error (added full `4` instead of `4/2`) & p. 93–95 inconsistent timestamps**.
  - *Syllabus Gap:* Add brief explanation of **Cost of Exact Counts** ($\Omega(N)$ bits lower bound) from Slide 2 TOC.
- `[x]` **3.5 Decaying Windows (Most Common / Trending Elements)** (pp. 104–114)
  - *Formula & Algorithm:* $\sum_{i=0}^{t-1} a_{t-i}(1-c)^i$ ($c \sim 10^{-6}$–$10^{-9}$); per-element score update $S \leftarrow S(1-c) + a_t$; spam/spike dampening.
  - *Worked Example Correction (pp. 112–113):* `fifa, ipl, fifa, ipl, ipl, ipl, fifa` (`c=0.1`) — **document and correct the $0.9$ initial-step error on `fifa` and the silent switch from $c=0.1$ to $c=0.01$ on `ipl`**.
- `[x]` **3.6 Counting Distinct Elements — Flajolet–Martin (FM) Algorithm** (pp. 115–135)
  - *Concept & Estimate:* Hash to bit-string of $\ge \log_2 n$ bits, count trailing zeros $r(x)$, track $R = \max r(x)$, estimate $m = 2^R$; $O(n)$ time, $O(\log m)$ memory.
  - *Worked Examples & Corrections:* `S={1,3,2,1,2,3,4,3,1}`, $h(x)=(3x+1)\bmod 5$ (**correct row 5/6 swaps & `mod 2` typo on pp. 122–124, 128**); solve Exercise 1 (p. 127).
  - *Combining Estimates Contradiction:* **Resolve Slide 130 (median of group means — standard MMDS) vs. Slide 133 (mean of group medians)**, and clarify Quiz p. 134 (`00..0` tail pattern caveat).

---

### Module 4: Social Media Analytics Overview & Social Network Structure, Measures, Visualization, and Clustering
**Files (Recommended Pedagogical Order):**
1. `module_4/Mod4 Social Network Structure, Measures & Visualization.pdf` (193 pp. — *actually Chapter 1: Social Media Analytics: An Overview*)
2. `module_4/Mod4B.pptx.pdf` (175 pp. — *Social Network Structure, Measures & Visualization*)
3. `module_4/Mod4d.pdf` (29 pp. — *Social Media Network Analytics & Clustering Coefficient*)
4. `module_4/Mod4C.pdf` (45 pp. — *Clustering of Social-Network Graphs & Clique Percolation Method*)

#### Part 4A — Social Media Analytics Overview (`Mod4 Social Network Structure, Measures & Visualization.pdf`)
- `[x]` **4A.1 Global Social Media Facts & Usage Trends (2024 DataReportal / GWI)** (pp. 1–9)
  - *Stats:* 7.99B / 5.22B SM identities (Oct 2024), active user index (YouTube 100, WhatsApp 85.7, Facebook 83.2, Instagram 71.4), audience overlap matrix, usage motivations, addiction facts.
- `[x]` **4A.2 Scope of Social Media Analytics & Metrics** (pp. 10–32)
  - *6 Metric Categories & Formulas:* Engagement Rate $= (\text{Engagements}/\text{Followers})\times 100$, Virality Rate $= (\text{Shares}/\text{Impressions})\times 100$, Follower Growth Rate, Conversion Rate, CTR, CPC, ROI, CSAT, Video completion rate.
  - *Analyses & Tools:* Audience (Demographics, Psychographics, Behavioral, Sentiment), Network, Content, Competitor, Evolution (pre-2000s $\to$ Web 2.0 $\to$ 2022–now), Tools (`Scrapy`, `Gephi`, `NLTK`, `NodeXL`, `Hootsuite`, `Brand24`, etc.).
- `[x]` **4A.3 Foundations: Web 1.0/2.0/3.0, Characteristics, Types, Landscape & Need for SMA** (`26CMPC71` Topic 4.1; pp. 33–64)
  - *Web Evolution:* Web 1.0 (static) $\to$ Web 2.0 (UGC, two-way) $\to$ Web 3.0 (Semantic Web, RDF).
  - *8 Social Media Categories:* SNS, Content Communities, Blogs, Microblogs (Twitter terms — **update 140-char limit**), Wikis/Collaborative Projects, Folksonomies/Tagging, Virtual Worlds, Mobile Apps.
  - *Required by `26CMPC71` Topic 4.1 (Omitted in Slides):* **Social Media Landscape**, **Need for Social Media Analytics (SMA)**, and **SMA in Small & Large Organizations**.
- `[x]` **4A.4 Applications, SMA vs. Traditional BA, Seven Layers & Types of Analytics** (pp. 65–113)
  - *10 Applications* (pp. 65–74) & Metrics Mapping Table (pp. 75–76).
  - *SMA Definition (Art & Science)* & **SMA vs. Traditional BA** (13-row + 6-row comparison tables, pp. 82, 98).
  - *Seven Layers of SMA:* Text, Networks, Actions, Apps/Mobile, Hyperlinks, Location, Search Engines (pp. 86–94).
  - *4 Analytics Types:* Descriptive $\to$ Diagnostic $\to$ Predictive ($\text{Sales}=5.6+1.2\cdot\text{AdExp}+0.5\cdot\text{Discount}$) $\to$ Prescriptive (Ice Cream, Coffee Shop, Coca-Cola `#ShareACoke`, Maruti Baleno vs Google Trends `"balleno"` examples, pp. 99–113).
- `[x]` **4A.5 Social Media Analytics Cycle, Challenges & Tools** (pp. 114–135; *pp. 136–193 duplicate pp. 77–134*)
  - *6-Step Cycle:* Identification $\to$ Extraction $\to$ Cleaning $\to$ Analyzing $\to$ Visualization $\to$ Interpretation (around Business Objectives).
  - *Challenges:* Volume/Velocity, Diversity, Unstructuredness; *Layer-wise Tools Table* (**note retired tools: Google Fusion Tables, Google+, Wikispaces, Socialbakers**); Review Questions (p. 134).

#### Part 4B — Social Network Structure, Measures & Visualization (`Mod4B.pptx.pdf`)
- `[x]` **4B.1 Graph Basics & Representations** (pp. 1–29)
  - *Concepts:* Actors/Nodes ($V$), Ties/Edges ($E$), Relationship types (Kinship, Cognitive, Affective, Interaction, Affiliation), Directed (arc) vs Undirected, Weighted (*Apollo 13* example).
  - *Representations:* Adjacency Matrix (sociomatrix, sparse), Adjacency List, Edge List (**fix p. 26 `4->3` vs `3|4` mismatch**), XML `<Person>`, Neighborhood $N(v)$ & Degree $d_i^{in}, d_i^{out}$.
- `[x]` **4B.2 Subnetworks, Paths, Connectedness, Bridges & Hubs** (pp. 30–57)
  - *Subnetworks:* Singleton, Dyad/Triad (**add brief definitions missing from slides**), Cliques ($k$-clique), Egocentric Networks (ego, alters, 1.0, 1.5, 2.0, without ego).
  - *Paths & Structure:* Path length, Geodesic / Shortest Path, Strongly vs Weakly Connected digraphs, Connected Components, Bridge, Hub; **2 Multi-part Exercises (pp. 56–57)** (provide worked walkthroughs!).
- `[x]` **4B.3 Network Measures: Degree Distribution, Density & Local Clustering** (pp. 58–76)
  - *Formulas:* Degree sequence $\pi(d)$, Degree distribution $p_d = n_d/n$, Directed density $\frac{e}{n(n-1)}$, Undirected density $\frac{e}{n(n-1)/2}$, Local clustering coefficient via 1.5-ego alter density (**flag p. 58/59 Fig 3.1 vs 2.7 `F` degree diff & p. 61 Fig 3.2 count mismatch**).
- `[x]` **4B.4 Node Centrality Measures** (pp. 77–112)
  - `[x]` Degree Centrality (plus peripheral hub limitation & quality vs quantity)
  - `[x]` Closeness Centrality — **reconcile average distance (lower=central, pp. 83–86) vs normalized reciprocal $CC(i) = \frac{N-1}{\sum d(i,j)}$ (higher=central, p. 87)**
  - `[x]` Betweenness Centrality — $BC(v) = \sum_{u \neq v \neq w} \frac{\sigma_{uw}(v)}{\sigma_{uw}}$ (**fix p. 89 subscript typo**; verify Bowtie, 6-node, and 8-node examples)
  - `[x]` Eigenvector Centrality — $Ax = \lambda x$, 4-step Power Iteration, worked 4-node & 5-node examples, NetworkX `nx.eigenvector_centrality(G)`.
- `[x]` **4B.5 Connectivity/Cohesion & Network Centralization** (pp. 113–128)
  - *Connectivity:* Minimum vertex cut (1 vs 2 examples).
  - *Centralization Formulas:* $NC_D$ (star/ring & 9-node examples), $NC_C$ (6-node star), $NC_B$; worked exercises (pp. 127–128).
- `[x]` **4B.6 Tie Strength & Trust** (pp. 129–155)
  - *Tie Strength:* Granovetter (1973/1974) **Strength of Weak Ties**, 4 dimensions (Time, Emotional Intensity, Intimacy, Reciprocal Services), social media measurement proxies.
  - *Trust:* McKnight et al. (1998) 4 types, Asymmetry & Context/Time, Johnson-George & Swap (1982) 4 facets, Network-based & Similarity-based trust inference.
- `[x]` **4B.7 Network Visualization & Scale Issues** (pp. 156–175)
  - *Principles:* Dunne & Shneiderman (2009) 4 readability guidelines, pre-attentive processing; Layouts (Random, Circular, Grid, **Force Atlas**, **Harel-Koren Fast Multiscale**, Cluster-boxed); Feature mapping (color, size, width); Hairball scale issue & Graph Simplification.

#### Part 4C — Social Media Network Analytics (`Mod4d.pdf`)
- `[x]` **4C.1 Social Media Network Analytics Concepts, Network Types & Clustering Coefficient** (pp. 1–29)
  - *Purpose:* 5 goals (structure, influential nodes, important links, cohesive subgroups, **multiplexity**).
  - *Taxonomies:* Existence (Implicit vs Explicit), Direction, Mode (One-mode, Two-mode/Bipartite, Multimode), Weights; 12 SM network types (Co-authorship, Co-commenter, Co-like, Geo Co-existence, etc.).
  - *Metrics:* Lists node/network properties (**note Structural Holes & Diameter are unlisted elsewhere — define them!**); **Local Clustering Coefficient formula** $CC(v) = \frac{2N_v}{K_v(K_v-1)}$ + worked $1/6$ example & Global $CC(G) = \text{avg } CC(v)$ (p. 19).
  - *Tools:* NodeXL (Excel screenshot p. 26), UCINET/Netdraw, Pajek, NetMiner, Flocker, Reach, Mentionmapp (**note X/Twitter API & CodePlex legacy status**).

#### Part 4D — Clustering of Social-Network Graphs & Clique Percolation Method (`Mod4C.pdf`)
- `[x]` **4D.1 Clustering of Social-Network Graphs & Community Concepts** (pp. 1–9)
  - *Concepts:* Community definition (dense intra-links, sparse inter-links), standard clustering, labeled similarity (co-authorship graph), binary edge distance $d(x,y) \in \{0,1\}$ (**note non-metric $d(x,y)=0$ when $x\neq y$**), **Disjoint vs. Overlapping communities**.
- `[x]` **4D.2 Clique Percolation Method (CPM) Algorithm & Worked Examples** (pp. 10–45)
  - *Definitions:* Clique, $k$-clique, Adjacent $k$-cliques (sharing $k-1$ nodes), $k$-clique community (connected component in clique graph $G_c$).
  - *Worked Examples & MU Exams:* 6-node $k=3$ intro, 8-node clique computation (p. 29), 9-node $k=3$ worked example (**flag & fix duplicated `{5,7,8}` / missing `{6,7,8}` typo on pp. 34–35**), 10-node $k=3$ (p. 37), Protein network (p. 38), unsolved `A–G` example (p. 39), **MU COMP May 2016** (pp. 40–42, temporary link `C–H`), **MU IT May 2016** (pp. 43–45 — **flag missing `2–5` & `6–4` edges in original question scan vs solution diagram!**).

---

### Module 5: Social Media Text, Action, and Hyperlink Analytics
**Files:** `module_5/ch 03 A Text Analytics.pptx.pdf` (30 pp.), `module_5/ch 03 B Action Analytics.pptx.pdf` (24 pp.), `module_5/ch 03 C Hyperlink Analytics.pptx.pdf` (36 pp.)

#### Part 5A — Text Analytics (`ch 03 A Text Analytics.pptx.pdf`)
- `[x]` **5A.1 Text Analytics Foundations & Types of Social Media Text** (pp. 1–10)
  - *Definition:* Extracting hidden business insights from textual UGC (~80% organizational data, roots in DM + NLP; `Flyertalk.com`).
  - *Static Text* (long, infrequent updates: wikis, blogs, docs, corporate reports, emails, transcripts) vs. *Dynamic Text* (short, real-time, opinionated: Tweets [**update 140-char limit $\to$ 280 / 25,000**], Comments, Forum Discussions, Private Conversations, Reviews).
- `[x]` **5A.2 Four Purposes of Text Analytics** (pp. 11–17)
  - **Sentiment Analysis** (pos/neg/neutral, Semantria logarithmic scoring), **Intention Mining** (`buy, sell, recommend, quit, desire, wish`), **Trends Mining** (predictive analytics via ML/DM/SNA), **Concept Mining** (extract/classify/cluster/rank ideas from static text).
- `[x]` **5A.3 Four Steps in Text Analytics** (pp. 18–25)
  - 1. *Identification & Searching* $\to$ 2. *Text Parsing & Filtering* (`NLP` — fix `"NPL"` typo p. 20; POS tagging, NER, stop-word removal, stemming, spell-check) $\to$ 3. *Text Transformation* (LSA, Vector Space Models / binary/TF representation) $\to$ 4. *Text Mining* (Association rules, Clustering [**fix `"natural"` $\to$ `"neutral"` typo p. 24**], Classification, Predictive & Sentiment analysis).
- `[x]` **5A.4 Tools & Semantria Tutorial** (pp. 26–30)
  - *Tools:* Discovertext, Lexalytics (**note 2021 InMoment acquisition**), Tweet Archivist, Twitonomy, Netlytic, LIWC, Voyant; Semantria for Excel + TripAdvisor dataset (**note legacy Excel add-in vs cloud API**; Case Study stub on p. 28).

#### Part 5B — Action Analytics (`ch 03 B Action Analytics.pptx.pdf`)
- `[x]` **5B.1 Actions Analytics Foundations & Business Value** (pp. 1–4)
  - *Concepts:* Symbolic reactions ("cash cow" / social expressions) measuring popularity & influence; boosts revenue, brand value, loyalty.
- `[x]` **5B.2 Fourteen Common Social Media Actions & Web Metrics** (pp. 5–20)
  - Like, Dislike, Share, Visitors/Visits(Sessions)/Revisits (**Unique Visitor, Average Bounce Rate, Session Duration**), View & Page Views, Clicks & **Clickstream Analysis**, Tagging, Mentions, Hovering, Check-in, Pinning, Embeds, Endorsement (`LinkedIn`), Uploading & Downloading.
- `[x]` **5B.3 Tools, Case Study Stub & Hootsuite** (pp. 21–24)
  - *Tools:* Hootsuite (legacy pricing screenshot p. 23), Lithium (now Khoros), Google Analytics, Facebook Insights, Klout (**shut down 2018**), SocialMediaMineR, Tweetreach, Kred, Hashtagify, Twtrland (now Klear), Tweetstats; Cover-More Group case study stub (p. 22); Review questions (p. 24).

#### Part 5C — Hyperlink Analytics (`ch 03 C Hyperlink Analytics.pptx.pdf`)
- `[x]` **5C.1 Hyperlinks Foundations & Types** (pp. 1–10)
  - *Types:* **In-links** (incoming backlinks; quantity + quality), **Out-links**, **Co-links** (**clarify Co-linking / Bibliographic Coupling vs. Co-citation ambiguity on Fig 1 p. 5 & p. 9**); Inter-linking vs. Intra-linking (**clarify p. 14 internal linking terminology**); core assumption (link count & quality = importance).
- `[x]` **5C.2 Three Types of Hyperlink Analytics** (pp. 11–25)
  - 1. *Hyperlink Environment Analysis* (link structure, SEO, competitor analysis, internal linking, spam link detection — **note "disavow" vs "denied" p. 16**, e-commerce scenario).
  - 2. *Link Impact Analysis* (URL web citations, referring domain authority, unlinked mentions, referral traffic).
  - 3. *Social Media Hyperlink Analysis* (links embedded in tweets/posts; source analysis, engagement, virality, sentiment, fake news, influencers; **Khan et al. 2014 Korean vs. US government Twitter out-link study**, Fig 2).
- `[x]` **5C.3 Tools, VOSON Tutorial & Review Questions** (pp. 26–36)
  - *Tools:* Google Search Console, GA, Ahrefs, SEMrush, Moz Link Explorer (**note Open Site Explorer retired**), Majestic, Screaming Frog, BuzzSumo, CognitiveSEO, Ubersuggest, SEO SpyGlass, OpenLinkProfiler, Webometrics Analyst, VOSON (`LinLog`, `Indegree*`, ccTLD screenshot p. 35), Link Diagnosis, Advanced Link Manager, Backlink Watch; YouTube viral links stub (p. 34); Review questions (p. 36).

---

### Module 6: Social Media Location Analytics, Search Engine Analytics, PageRank & HITS
**Files:** `module_6/ch 04 A Location Analytics.pptx.pdf` (38 pp.), `module_6/ch 04 B Search Engine Analytics.pptx.pdf` (37 pp.), `module_6/ch 04 -Page Rank n HITS.pptx.pdf` (26 pp.)

#### Part 6A — Location Analytics (`ch 04 A Location Analytics.pptx.pdf`)
- `[x]` **6A.1 Location Analytics Foundations & Data Sources** (pp. 1–5)
  - *Definition:* Spatial / geo-analytics (mapping, visualizing, mining locations of people, data, resources).
  - *Sources:* Postal Address, Lat/Long, GPS, IP Geolocation, Geotagged Posts/Media, Check-ins (Facebook Places, Swarm), User Profile info, Crowdsourced/3rd-party data.
- `[x]` **6A.2 Business Data-Driven Location Analytics** (pp. 6–16)
  - *Applications:* (1) **Powerful Intelligence** (overcoming static maps via Clustering, Heat Mapping, Data Aggregation, Color-Coded Mapping); (2) **Geo-Enrichment** (`Hecht 2013`: demographics, spending, lifestyle, foot traffic); (3) **Collaboration & Sharing**.
- `[x]` **6A.3 Social Media Data-Driven Location Analytics & Privacy** (pp. 17–28)
  - *7 Uses:* Recommendations (`Tinder` — fix `"Tender"` typo p. 19), Customer Segmentation (`Tweepsmap`/`Fedica`), Location-based Ads, Info Requests, Alerts, Search & Rescue (`Agos`), Navigation (`Google Maps`).
  - *Privacy Concerns & Questions:* Collection/retention/use/disclosure; fundamental rights (freedom of movement, freedom from being observed); 6 legal/ethical privacy questions (pp. 27–28).
- `[x]` **6A.4 Tools, Fusion Tables Tutorial & Review** (pp. 29–38)
  - *Tools:* Google Fusion Tables (**shut down Dec 3, 2019** — add modern alternatives like Kepler.gl/Looker Studio/QGIS!), Agos, Tweepsmap (`fedica.com`), Trendsmap, Followerwonk, Esri GIS; "Owl Bus" case study stub (p. 35); Victoria Police Stations KML screenshot (p. 36); Review questions (p. 37).

#### Part 6B — Search Engine Analytics (`ch 04 B Search Engine Analytics.pptx.pdf`)
- `[x]` **6B.1 Search Engine Types, Architecture & Working** (pp. 1–12)
  - *3 Types:* **Crawler-Based** (`Google`, `Bing`: 1. Web Crawling/spiders/cache/`robots.txt`, 2. Indexing, 3. Searching/NLP query rewriting & optimization; `Live Google Example` architecture diagram p. 9), **Directories** (`Yahoo Directory`, `DMOZ`, `LookSmart` — **note historical/retired status**), **Metasearch Engines** (`Metacrawler`, `Mamma`, `Dogpile`).
  - *Scope Gap:* Local vs. Global Search Engines listed on p. 12 & Review Q3 p. 37 without definitions — define & contrast cleanly!
- `[x]` **6B.2 Search Engine Optimization (SEO) & Ranking Signals** (pp. 13–26)
  - *SEO & SERP:* Organic vs non-organic results; 4 ranking factors (Keywords, Page Content, Backlinks/PageRank, User Info/personalization); Moz backlink graphic; PageRank qualitative example (Fig 1 `Page B` vs `Page D`, p. 19) & 11-node percentage network (p. 20).
  - *Domain Analysis Screenshots (`checkpagerank.net`, pp. 21–26):* `facebook.com`, `dominos.co.in`, `frcrit.ac.in`/`fcrit.ac.in`, `ultimatix.net`, `vesit.ves.ac.in` (2023) — **clarify Toolbar PageRank 0–10 retirement (2016) & Alexa Rank retirement (May 2022) vs modern Moz DA/PA & Majestic Trust/Citation Flow**.
- `[x]` **6B.3 Search Trend Analytics, Operators & Tools** (pp. 27–37)
  - *Trend Questions & Tools:* Google Trends, Canopy, Google Alerts, Icerocket/Social Mention/TweetBeep (**note legacy status**); Table 1 research query syntax (**clarify `+` as OR in Google Trends vs AND/modern search syntax**, p. 35); Google Trends UI screenshot (p. 36); Review questions (p. 37).

#### Part 6C — PageRank & HITS Algorithms (`ch 04 -Page Rank n HITS.pptx.pdf`)
- `[x]` **6C.1 Idealized PageRank Formulation & Power Iteration** (pp. 1–12, 19–26)
  - *Formulation:* Random surfer uniform start $V_0 = [1/n,\dots,1/n]^T$, column-stochastic transition matrix $M$ ($m_{ij}=1/k$), update $v = Mv$, $M^t v_0$.
  - *Worked Examples:* 3-node (`Yahoo, Amazon, Microsoft` $\to [2/5, 2/5, 1/5]^T$); 5-node `Ex 2` (**explain L1 `[0.20, 0.20, 0.15, 0.15, 0.30]` vs L2 `[0.4313, ...]` normalization discrepancy on p. 12**); 4-node `A` matrix (`p. 19–21`); Flow-style PageRank exercises (`pp. 22–26`: `B=14`, `B=12`, `A=14`).
- `[x]` **6C.2 Dead Ends, Spider Traps & Teleportation (Taxation)** (pp. 13–18)
  - *Problems:* Dead Ends (no outlinks, PageRank leaks to 0) & Spider Traps (absorbing SCC/self-loop traps all rank).
  - *Worked Correction:* **Flag & correct `Dead end: Ex 3` (pp. 15–16)** where spider trap numbers `[0,0,1]` were pasted onto a dead-end matrix (true limit is `[0,0,0]`); verify `Ex: Dead end` (p. 17) & `Ex: Spider Trap` (p. 18).
  - *Critical Missing Math:* **Add damped PageRank / Teleportation (Taxation) equation** $v' = \beta M v + (1-\beta)\frac{e}{n}$ (mentioned in prose on p. 14, formula omitted!).
- `[x]` **6C.3 HITS Algorithm (Hubs and Authorities)** *(Supplementary — in PPT filename `ch 04 -Page Rank n HITS.pptx.pdf`, not in `26CMPC71` `6.2` text)*
  - *Gap Fill Needed:* Include complete beginner-friendly derivation, Hub ($h$) & Authority ($a$) mutually recursive equations ($a = L^T h$, $h = L a$), normalization, worked numerical matrix example, and **PageRank vs. HITS comparison** for the viva.
- `[x]` **6C.4 Big Data & Social Media Analytics Applications (Synthesis + Microproject Context)** (`26CMPC71` Topic 6.2 & Lab Exp 11*)
  - *Required by `26CMPC71` Topic 6.2:* End-to-end real-world applications across domains (streaming pipelines with Kafka/Flume/PySpark, recommender systems, spatio-temporal analytics, healthcare, finance, telecom, crisis response).

---

## 4. Proposed Order for Preparing Detailed Notes (Updated for `26CMPC71`)

1. **`Module_1_Notes.md` (`CO1`, 04 hrs):** Establishes zero-prerequisite Big Data foundations (`1.1`) and Distributed File Systems / Hadoop / HDFS / YARN / Ecosystem (`1.1` + `1.2`, integrating DFS physical/large-scale organization from `Module _02` Slides 3–9 + Lab Exp 1 HDFS commands).
2. **`Module_2_Notes.md` (`CO2`, 08 hrs):** Covers MapReduce execution, **Combiners**, **Coping with Node Failures** (`2.1`), Matrix-Vector & Relational Algebra algorithms plus 2-Step Matrix Multiplication (`2.2`), and NoSQL Architecture Patterns + Case Studies + Distribution Models (`2.3` + Lab Exp 2, 3, 4).
3. **`Module_3_Notes.md` (`CO3`, 07 hrs):** Covers Stream Data Model & DSMS (`3.1`), **Stream Sampling + Reservoir Sampling**, **Bloom Filters + FPR Analysis**, DGIM (`O(log^2 N)` & exact-count cost), Decaying Windows, and Flajolet–Martin (`3.2` + Lab Exp 5 & 6 Spark context).
4. **`Module_4_Notes.md` (`CO4`, 08 hrs):** Structured exactly along `26CMPC71` `4.1 -> 4.2 -> 4.3`:
   - `4.1`: SMA Overview, Core Characteristics, Landscape, **Need for SMA**, **SMA in Small & Large Orgs**, Seven Layers, Types of Analytics, SMA Cycle, Challenges (`Mod4 Social Network Structure...pdf`).
   - `4.2`: Social Network Structure, Graph Measures, Centralities, Centralization, Tie Strength, Trust, Visualization (`Mod4B.pptx.pdf`).
   - `4.3`: SM Network Analytics, Types of Networks, Tools, Clustering & **Clique Percolation Method (CPM)** + **Louvain Method** (`Mod4d.pdf` & `Mod4C.pdf` + Lab Exp 9 & 10).
5. **`Module_5_Notes.md` (`CO5`, 06 hrs):** Covers Text (`5.1`), Action (`5.2`), and Hyperlink (`5.3`) Analytics (+ Lab Exp 7 & 8).
6. **`Module_6_Notes.md` (`CO6`, 06 hrs):** Covers Location (`6.1`) and Search Engine Analytics, PageRank + Teleportation, **Big Data & Social Media Analytics Applications** (`6.2`), plus concise HITS bonus coverage (+ Lab Exp 11* Microproject context).
7. **Final Synthesis (`Final_Viva_Question_Bank.md` & `QUICK_REVISION_NOTES.md`):** Compiled after all 6 modules are verified complete, including both Theory End-Sem / Oral and `PR & OR` Lab Viva questions.
