# Big Data and Social Media Analytics (`26CMPC71`) — Study & Viva Preparation Repository

**Institution / Program:** Vivekanand Education Society's Institute of Technology (VESIT), Dept. of Computer Engineering — Final Year B.E. (Batch 2023–2027, 2026 'NEP & Autonomy' Scheme, Sem VII)  
**Course Code:** `26CMPC71` — *Big Data and Social Media Analytics* (`06` Modules / `39` Theory Hours + `10` Lab Experiments + Microproject; Theory + `25`-mark Practical & Oral [`PR & OR`])  
**Slide Decks Included:** `15` lecture PDFs (`1,395` total slides) across `module_1/`–`module_6/` (primarily compiled by Dr. Rohini Temkar)

---

## Quick Navigation: Viva Study Materials ([`VIVA_NOTES/`](./VIVA_NOTES/))

Start with [`VIVA_NOTES/`](./VIVA_NOTES/), which contains beginner-friendly, syllabus-grounded notes verified against both the professor's slides, official `26CMPC71` curriculum, and authoritative external documentation:

| Order | File | Purpose |
|---:|---|---|
| 1 | [`VIVA_NOTES/00_SYLLABUS_AND_TOPIC_MAP.md`](./VIVA_NOTES/00_SYLLABUS_AND_TOPIC_MAP.md) | Official `26CMPC71` module/CO/lab mapping (`Exp 1–11*`), `15`-PDF inventory, and complete topic checklist |
| 2 | [`VIVA_NOTES/Module_1_Notes.md`](./VIVA_NOTES/Module_1_Notes.md) | **Module 1 (`CO1`, `04` hrs):** Introduction to Big Data, Hadoop Core Components, HDFS, YARN, & DFS Physical/Large-Scale Organization (+ `Exp 1` HDFS CLI) |
| 3 | [`VIVA_NOTES/Module_2_Notes.md`](./VIVA_NOTES/Module_2_Notes.md) | **Module 2 (`CO2`, `08` hrs):** MapReduce, Combiners, Node Failure Recovery, Relational Algebra, 1/2-Step Matrix Multiplication, Hadoop Ecosystem & NoSQL Patterns (+ `Exps 2–4`) |
| 4 | [`VIVA_NOTES/Module_3_Notes.md`](./VIVA_NOTES/Module_3_Notes.md) | **Module 3 (`CO3`, `07` hrs):** Mining Data Streams — DSMS, Sampling (incl. Reservoir Sampling), Bloom Filters + FPR, $\Omega(N)$ & DGIM, Decaying Windows, Flajolet–Martin (+ `Exps 5–6`) |
| 5 | [`VIVA_NOTES/Module_4_Notes.md`](./VIVA_NOTES/Module_4_Notes.md) | **Module 4 (`CO4`, `08` hrs):** SMA Overview (`4.1`), Social Network Structure, Measures & Visualization (`4.2`), Network Analytics, CPM & Louvain Clustering (`4.3`, `Exps 7, 9, 10`) |
| 6 | [`VIVA_NOTES/Module_5_Notes.md`](./VIVA_NOTES/Module_5_Notes.md) | **Module 5 (`CO5`, `06` hrs):** Text Analytics (`TextBlob`/`VADER`), Action Analytics (GA4 vs UA), & Hyperlink Analytics (`Co-citation` vs `Bibliographic Coupling`, VOSON) (+ `Exps 7–8`) |
| 7 | [`VIVA_NOTES/Module_6_Notes.md`](./VIVA_NOTES/Module_6_Notes.md) | **Module 6 (`CO6`, `06` hrs):** Location Analytics ("Owl Bus"), Search Engine Analytics, PageRank + Teleportation, Bonus HITS, & End-to-End Applications (+ `Exps 9, 10, 11*`) |
| 8 | [`VIVA_NOTES/Final_Viva_Question_Bank.md`](./VIVA_NOTES/Final_Viva_Question_Bank.md) | `114` categorized practice Q&As (`Q1`–`Q100` across Modules 1–6 + `L1`–`L14` for `PR & OR` Lab & Microproject) |
| 9 | [`VIVA_NOTES/QUICK_REVISION_NOTES.md`](./VIVA_NOTES/QUICK_REVISION_NOTES.md) | Pre-viva cram sheet: 1-line definitions, formulas, acronyms, key differences, Mermaid flows, 30-second spoken answers & top slide-trap fixes |
| 10 | [`VIVA_NOTES/SOURCE_REGISTER.md`](./VIVA_NOTES/SOURCE_REGISTER.md) | Official syllabus textbooks and verified external reference URLs (`S01`–`S72`) |

---

## Repository Structure

```text
BDSMA/
├── README.md
├── Final year B. E. (Computer Engineering) (Sem-VII & VIII) Batch  [2023-2027] (2026 ‘NEP & Autonomy’ Scheme).pdf
├── MASTER_ANTIGRAVITY_PROMPT.md
├── VIVA_NOTES/                         # Complete beginner-friendly viva notes & revision suite
├── module_1/                           # 2 PDFs (ch 01 A, Module_ 01 B)
├── module_2/                           # 2 PDFs (Module _02 Hadoop/MapReduce, Mod 2_NoSQL)
├── module_3/                           # 1 PDF  (BDA_Mod 3 Mining Data Streams)
├── module_4/                           # 4 PDFs (Mod4 [actually Topic 4.1], Mod4B, Mod4d, Mod4C)
├── module_5/                           # 3 PDFs (ch 03 A Text, ch 03 B Action, ch 03 C Hyperlink)
└── module_6/                           # 3 PDFs (ch 04 A Location, ch 04 B Search Engine, ch 04 -Page Rank n HITS)
```

---

## Key Features of the Study Notes

- **Syllabus-Complete (`26CMPC71`):** Fills official syllabus topics absent from the slides (e.g., *Combiners*, *Coping With Node Failures*, *Reservoir Sampling*, *Bloom Filter FPR derivation*, *Cost of Exact Counts $\Omega(N)$*, *SMA Landscape / Small vs. Large Organizations*, *Structural Holes*, *Diameter*, *Local vs. Global Search*, *PageRank Teleportation*, *Louvain Method*, and *HITS*).
- **Slide Traps Verified & Corrected:** Clearly distinguishes exact slide printouts from verified corrections (such as DGIM Slide 84, Decaying Windows `fifa`/`ipl`, Matrix $m_{23}n_{32}=6$, Dead End Ex 3, Closeness Centrality conventions, Co-citation vs. Bibliographic Coupling, GA4 Bounce Rate, and retired tools like Google Fusion Tables, Alexa Rank, Toolbar PageRank, and Klout).
- **Spoken Viva Ready:** Includes 30–60 second oral explanations, numerical walkthroughs, practical examples, examiner follow-ups, and Lab `PR & OR` prep without altering any original slide PDFs.

---

## Recommended Study Order

1. **Full Learning Pass:** Read `Module_1_Notes.md` through `Module_6_Notes.md` sequentially.
2. **Active Recall Drill:** Practice answering [Final_Viva_Question_Bank.md](./VIVA_NOTES/Final_Viva_Question_Bank.md) out loud (`[HIGH PRIORITY]` items + `L1`–`L14` lab questions).
3. **Final Pre-Viva Scan:** Review [QUICK_REVISION_NOTES.md](./VIVA_NOTES/QUICK_REVISION_NOTES.md) right before entering the exam/viva room.
