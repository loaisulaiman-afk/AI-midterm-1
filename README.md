# Academic Transfer Planner — Documentation

> **Course:** Introduction to Artificial Intelligence  
> **University:** Ilia State University — School of Technology  
> **Current Program:** Computer Science (Bachelor's, 240 ECTS)  
> **Source:** [ISU School of Technology](https://iliauni.edu.ge/en/iliauni/AcademicDepartments/bte/programebi-276/schooloftechnology3/bachelorsprograms)

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [How to Use](#2-how-to-use)
3. [Course List](#3-course-list)
4. [Equivalency Algorithm](#4-equivalency-algorithm)
5. [Improvement Plan — Automatic Syllabus Comparison](#5-improvement-plan--automatic-syllabus-comparison)

---

## 1. Project Overview

The **Academic Transfer Planner** is a single-file web application (`index.html`) built for a Computer Science student at Ilia State University's School of Technology. It helps plan a potential transfer to one of the other three Bachelor's programs in the same school.

**About the ISU Computer Science program:**

The CS Bachelor's program was developed in 2020 in collaboration with the Steinbuch Computing Center of the Karlsruhe Institute of Technology (KIT) and 20 major companies including Bank of Georgia and Deutsche Post DHL Group. The program is 240 ECTS (8 semesters) and covers:

- Basics of Computer Science
- Algorithms and modern programming technologies
- System and network programming
- Data analysis and visualization
- Machine learning and artificial intelligence
- Cybersecurity and ethics
- Database systems
- Human-computer interaction
- Computer graphics and bioinformatics

**Technologies used:**

| Technology | Purpose |
|------------|---------|
| HTML5 | Page structure |
| CSS3 (embedded) | Styling, layout, animations |
| Vanilla JavaScript (embedded) | Data, logic, DOM rendering |

Everything is in a **single `.html` file** — no external files, no frameworks.

---

## 2. How to Use

1. Open `index.html` in any modern browser
2. The full course table loads automatically on the left
3. Review your statistics on the right panel
4. Choose a target program from the dropdown:
   - Computer Engineering
   - Civil Engineering
   - Electrical and Electronics Engineering
5. Click **Transfer →**
6. The equivalency table appears below

---

## 3. Course List

The courses reflect the structure of the ISU Computer Science Bachelor's program (General Module 60 ECTS + Major 180 ECTS = 240 ECTS total).

| # | Course | Semester | Passed |
|---|--------|----------|--------|
| 1 | English Language I | 1 | Yes |
| 2 | Calculus I | 1 | Yes |
| 3 | Introduction to Programming | 1 | Yes |
| 4 | Discrete Mathematics | 1 | Yes |
| 5 | English Language II | 2 | Yes |
| 6 | Calculus II | 2 | Yes |
| 7 | Linear Algebra | 2 | Yes |
| 8 | Object-Oriented Programming | 2 | Yes |
| 9 | Data Structures | 3 | Yes |
| 10 | Statistics and Probability | 3 | Yes |
| 11 | Algorithms | 4 | No |
| 12 | Computer Organization and Architecture | 4 | No |
| 13 | Database Systems | 5 | No |
| 14 | Operating Systems | 5 | No |
| 15 | Introduction to Artificial Intelligence | 5 | No (in progress) |
| 16 | Computer Networks *(additional)* | — | Yes |
| 17 | Software Engineering *(additional)* | — | Yes |
| 18 | Human-Computer Interaction *(additional)* | — | Yes |
| 19 | Cybersecurity Fundamentals *(additional)* | — | Yes |
| 20 | Machine Learning *(additional)* | — | Yes |

---

## 4. Equivalency Algorithm

### Overview

The algorithm uses a **rule-based lookup table** defined as a JavaScript object. Each top-level key is a target program. Each inner key maps a CS course to its equivalent in that program, or `"N/A"` if none exists.

### Step-by-Step Logic
### Rules Applied

**Tier 1 — Direct Match**  
Courses confirmed by ISU programme descriptions to appear in both programs:

| CS Course | CE | Civil | EEE |
|-----------|:--:|:-----:|:---:|
| English Language I & II | ✓ | ✓ | ✓ |
| Calculus I & II | ✓ | ✓ | ✓ |
| Linear Algebra | ✓ | ✓ | ✓ |
| Statistics and Probability | ✓ | ✓ | ✓ |

**Tier 2 — Similar Match**  
Same subject, different name in target program:

| CS Course | Target | Equivalent | Reason |
|-----------|--------|-----------|--------|
| Introduction to Programming | EEE | Programming for Engineers | Same content, engineering framing |
| Data Structures | CE | Data Structures and Algorithms | Same content, merged with algorithms |
| Computer Networks | CE | Computer Networks and Communication Protocols | ISU CE explicitly lists this area |
| Computer Networks | EEE | Telecommunications and Networks | Same core topic, EEE framing |

**Tier 3 — No Equivalent (N/A)**  
CS-specific courses not offered in target programs:

- `Human-Computer Interaction` → N/A in all (CS-specific area per ISU)
- `Cybersecurity Fundamentals` → N/A in all (listed only under CS)
- `Machine Learning` → N/A in all (CS/AI specialization)
- `Discrete Mathematics` → N/A in Civil and EEE
- `Object-Oriented Programming` → N/A in Civil and EEE
- `Software Engineering` → N/A in Civil and EEE

### Full Equivalency Table

| CS Course | Computer Engineering | Civil Engineering | EEE |
|-----------|---------------------|------------------|-----|
| English Language I | English Language I | English Language I | English Language I |
| English Language II | English Language II | English Language II | English Language II |
| Calculus I | Calculus I | Calculus I | Calculus I |
| Calculus II | Calculus II | Calculus II | Calculus II |
| Linear Algebra | Linear Algebra | Linear Algebra | Linear Algebra |
| Introduction to Programming | Introduction to Programming | N/A | Programming for Engineers |
| Discrete Mathematics | Discrete Mathematics | N/A | N/A |
| Object-Oriented Programming | Object-Oriented Programming | N/A | N/A |
| Data Structures | Data Structures and Algorithms | N/A | N/A |
| Statistics and Probability | Probability Theory and Statistics | Engineering Statistics | Probability Theory and Statistics |
| Computer Networks | Computer Networks and Communication Protocols | N/A | Telecommunications and Networks |
| Software Engineering | Software Engineering | N/A | N/A |
| Human-Computer Interaction | N/A | N/A | N/A |
| Cybersecurity Fundamentals | N/A | N/A | N/A |
| Machine Learning | N/A | N/A | N/A |

---

## 5. Improvement Plan — Automatic Syllabus Comparison

### Motivation

The current system requires manually reviewing each course pair and hard-coding the result. This has three critical weaknesses:

- It does not scale — updating 100+ courses across 4 programs takes significant human effort
- It is subjective — two reviewers may disagree on equivalency
- It cannot detect partial equivalency — a course covering 60% of another is treated the same as 0%

An AI-powered system solves all three by reading actual syllabi and computing similarity automatically.

---

### Proposed Architecture
---

### Step-by-Step Algorithm

#### Step 1 — Syllabus Ingestion

Parse each ISU curriculum file to extract structured data:

```json
{
  "program": "Computer Science",
  "course_name": "Introduction to Programming",
  "ects": 6,
  "semester": 1,
  "topics": ["variables", "control flow", "functions", "recursion", "basic OOP"],
  "learning_outcomes": [
    "write and debug basic programs",
    "understand data types and structures",
    "apply algorithmic thinking to simple problems"
  ]
}
```

**Tools:** `PyMuPDF` for PDFs, `openpyxl` for Excel files, `spaCy` for NLP cleaning.

#### Step 2 — Text Embedding

Convert each course into a vector using a sentence embedding model:

```python
from sentence_transformers import SentenceTransformer

model = SentenceTransformer("paraphrase-multilingual-MiniLM-L12-v2")

course_text = "variables control flow functions recursion OOP " \
              "write basic programs debug code understand data types"

vector = model.encode(course_text)
```

> A multilingual model is used because ISU syllabi may contain Georgian text.

#### Step 3 — Similarity Scoring

```python
from sklearn.metrics.pairwise import cosine_similarity

def score(vec_a, vec_b, topics_a, topics_b, ects_a, ects_b):
    semantic  = cosine_similarity([vec_a], [vec_b])[0][0]
    keywords  = len(set(topics_a) & set(topics_b)) / max(len(set(topics_a) | set(topics_b)), 1)
    ects_diff = abs(ects_a - ects_b)
    proximity = 1.0 if ects_diff == 0 else max(0, 1 - ects_diff / 12)
    return round(0.6 * semantic + 0.3 * keywords + 0.1 * proximity, 4)
```

- `score >= 0.80` → **EQUIVALENT** (automatic)
- `score 0.55–0.79` → sent to LLM for validation
- `score < 0.55` → **N/A** (automatic)

#### Step 4 — LLM Validation
#### Step 5 — Output

| CS Course | Target Equivalent | Score | Verdict | Reason |
|-----------|-----------------|-------|---------|--------|
| Calculus I | Calculus I | 0.99 | EQUIVALENT | Identical content and ECTS |
| Intro to Programming | Programming for Engineers | 0.83 | EQUIVALENT | Same core concepts |
| Data Structures | Data Structures and Algorithms | 0.76 | EQUIVALENT (LLM) | Overlapping topics confirmed |
| Machine Learning | N/A | 0.21 | NOT_EQUIVALENT | No ML content in target program |

---

### Why AI Is Essential

| Step | Without AI | With AI |
|------|-----------|---------|
| Syllabus reading | Human reads every document | NLP parser extracts structured data automatically |
| Course comparison | Subjective human judgment | Embedding model computes objective similarity |
| Borderline cases | Inconsistent decisions | LLM provides reasoned verdict with confidence |
| Scaling | Weeks of manual work | Minutes of computation |
| Multilingual support | Requires bilingual expert | Multilingual model handles Georgian + English |

---

### Challenges and Mitigations

| Challenge | Mitigation |
|-----------|-----------|
| ISU syllabus files restricted | Request from programme coordinators |
| Georgian + English mixed content | Use multilingual embedding model |
| LLM hallucination | Require structured JSON output; human review for PARTIAL |
| ECTS mismatch | Apply credit proximity penalty; flag large differences |
| Partial equivalency | Introduce PARTIAL verdict — advisor makes final call |

---

*End of documentation.*
