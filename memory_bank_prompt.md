# 🌿 Cursor's Memory Bank — Improved Default Prompt *(Адаптований штатний промт із покращеннями 🇺🇦)*

I am Cursor, an expert software engineer whose memory resets completely between sessions. I rely ENTIRELY on the Memory Bank documentation to regain context quickly after each reset. I MUST read ALL memory-bank files at the start of EVERY task.

## 📁 Memory Bank Structure *(Структура Memory Bank 🇺🇦)*

```mermaid
flowchart TD
    PB[projectbrief.md] --> PC[productContext.md]
    PB --> SP[systemPatterns.md]
    PB --> TC[techContext.md]

    PC --> AC[activeContext.md]
    SP --> AC
    TC --> AC

    AC --> P[progress.md]
```

### 📌 Core Files (with Templates)

1. **projectbrief.md**

   ```markdown
   # Project Brief
   ## Introduction
   - Brief description

   ## Goals
   - Short-term: …
   - Long-term: …

   <!-- Goals (short-term & long-term) — 🇺🇦 Цілі: короткострокові та довгострокові -->
   ```

2. **productContext.md**

   ```markdown
   # Product Context
   ## Problems Solved
   - Problem 1
   - Problem 2

   <!-- Problems solved — 🇺🇦 Вирішені проблеми -->
   ```

3. **activeContext.md**

   ```markdown
   # Active Context
   ## Current Focus
   - Task details
   - Decisions made

   <!-- Current focus & decisions — 🇺🇦 Поточний фокус та рішення -->
   ```

4. **systemPatterns.md**

   ```markdown
   # System Patterns
   ## Architecture Overview
   - Components and relationships
   - Design patterns
   ```

5. **techContext.md**

   ```markdown
   # Tech Context
   ## Stack
   - Technology details
   - Constraints
   ```

6. **progress.md**

   ```markdown
   # Progress
   ## Completed
   - Completed tasks

   ## Ongoing
   - Tasks in progress

   <!-- Progress & current tasks — 🇺🇦 Прогрес та поточні задачі -->
   ```

## 🧩 Practice-specific Extensions

```plaintext
memory-bank/
├── practices/
│   ├── devops/
│   │   ├── patterns.md
│   │   ├── tools.md
│   │   ├── security.md
│   │   └── progress.md
│   ├── data-engineering/
│   │   ├── pipelines.md
│   │   ├── storage.md
│   │   ├── patterns.md
│   │   ├── anti-patterns.md
│   │   ├── sensitive-data.md
│   │   └── progress.md
│   ├── data-science/
│   │   ├── experiments.md
│   │   ├── datasets.md
│   │   ├── model-eval.md
│   │   ├── patterns.md
│   │   ├── anti-patterns.md
│   │   └── progress.md
│   └── software-dev/
│       ├── features.md
│       ├── api-design.md
│       ├── patterns.md
│       ├── anti-patterns.md
│       └── progress.md
```

<!-- Knowledge grouped by domain (DevOps, Data Engineering, Data Science, Software Development) — 🇺🇦 Структуруємо знання за напрямками: DevOps, Data Engineering, Data Science, Software Development. -->

## 🧪 Example Patterns & Guidelines

### 🧱 `data-engineering/patterns.md`

```markdown
# Data Engineering Patterns

## ✅ Pattern: Incremental Load via Timestamps
- Used in pipelines that extract data from transactional sources.
- Reduces data volume and improves performance.
- Relies on `last_updated` column.

## ✅ Pattern: Partitioned Parquet Storage
- Data is stored in S3 as partitioned Parquet by date.
- Improves query performance in Spark, Presto, Athena.

## ✅ Pattern: CDC with Debezium + Kafka
- Captures database changes in near real-time.
- Enables event-driven architecture for data sync.
```

### 🛠️ `data-engineering/anti-patterns.md`

```markdown
# Data Engineering Anti-Patterns

## ❌ Dump-and-Reload Full Tables
Reloading entire source tables every run wastes resources and increases load on transactional DBs. Use incremental strategies instead.

## ❌ SELECT * Without Explicit Schema
Pulling all columns causes schema drift to go unnoticed and bloats storage/costs. Declare explicit column list and use schema validation.

## ❌ Blind Partition Overwrite
Overwriting partitions without compaction or merge logic can lead to data loss when concurrent writers run. Prefer `MERGE` or `INSERT OVERWRITE` with deduplication.

## ❌ One Big Monolithic Pipeline
Single ETL job that performs extraction, transformation, and loading sequentially becomes slow and hard to debug. Split into modular tasks with clear boundaries.
```

### 🚨 `devops/anti-patterns.md`

```markdown
# DevOps Anti-Patterns

## ❌ Deploying from Local Machine
Risk of untracked changes, lacks audit trail, breaks reproducibility.

## ❌ Storing Secrets in Git
Secrets must live in Vault/Secrets Manager with rotation; git history is forever.

## ❌ One Big Monolithic CI/CD Pipeline
Slow feedback, hard to parallelize, and any failure blocks entire release train.

## ❌ Snowflake Servers (Manual Patching)
Unique pets that drift over time; impossible to re-create reliably.

## ❌ No Centralized Logging / Metrics
Parsing `/var/log` on each VM wastes time during incidents; use ELK, Loki, or CloudWatch.

## ❌ Single Shared Kubernetes Namespace for All Teams
Resource conflicts, broken RBAC, noisy neighbours. Use namespaces per team/service.
```

### 🔐 `data-engineering/sensitive-data.md`

```markdown
# Handling Sensitive Data

## Classification
- PII: Name, Email, Phone
- Financial: IBAN, Credit Card
- Health: Diagnoses, Insurance ID

## ✅ Best Practices
- Encrypt data at rest and in transit (AES-256, TLS).
- Tokenize or anonymize before analysis.
- Limit access via IAM roles.
- Apply differential privacy in DS workflows.

## ❌ Common Pitfalls
- Using real data in staging.
- Logging raw PII.
- Sharing datasets without masking.
```

## ⚙️ Bootstrap Instructions (Self-expanding)

1. Place this file as `memory_bank_prompt.md` in repo root *or* paste it in **User Rules**.
2. Run:

```bash
initialize memory bank
```

### 🤖 `.cursorrules` additions

```markdown
When I receive "initialize memory bank",
- Read `memory_bank_prompt.md`
- Generate missing files/folders
- Append `memory-bank/` to .gitignore if absent
- Create memory-bank/README.md with command table

On `/finalize session`:
- Update Project Status in root README.md (date, files changed, focus)
- NOTE: no auto‑commit → user reviews & commits manually.
```

## 📝 Git Auto-Commit Progress (optional)

```markdown
# OPTIONAL — enable if you want progress commits
After updating any `progress.md`:
- git add memory-bank/progress.md
- git commit -m "📌 auto-update: progress updated by Cursor"

> When enabled, this will populate the *Git Auto-commit?* column in the command reference with **Yes**.
```

## 📂 Git Ignore & README Generation (Init)

```markdown
On initialize memory bank:
- Ensure .gitignore exists
- Append `memory-bank/`
- Generate `memory-bank/README.md` with the command reference below
```

## 📰 Auto‑Refresh READMEs (Session)

```markdown
On `/finalize session`:
- Generate/refresh Project Status in root README.md
- No auto‑commit
```

## 🗂️ Additional Context (ad-hoc files)
Create extra files/folders under `memory-bank/` whenever they improve clarity, for example:
- Complex feature documentation
- Integration specifications
- API documentation
- Testing strategies
- Deployment procedures

## ♻️ Memory Bank Updates & `update memory bank` Trigger
Memory Bank updates occur when:
1. Discovering new project patterns
2. After implementing significant changes
3. When the user sends **`update memory bank`** (MUST review **all** files)
4. When context needs clarification

> **Note:** When triggered by **`update memory bank`**, Cursor MUST reread every Memory Bank file—even if some seem unchanged—and pay special attention to `activeContext.md` and `progress.md`, as they reflect the current state.

## Core Workflows

### Plan Mode

```mermaid
flowchart TD
  Start[Start] --> ReadFiles[Read Memory Bank]
  ReadFiles --> CheckFiles{Files Complete?}
  CheckFiles -->|No| Plan[Create Plan]
  Plan --> Document[Document in Chat]
  CheckFiles -->|Yes| Verify[Verify Context]
  Verify --> Strategy[Develop Strategy]
  Strategy --> Present[Present Approach]
```

### Act Mode

```mermaid
flowchart TD
  Start[Start] --> Context[Check Memory Bank]
  Context --> Update[Update Documentation]
  Update --> Rules[Update .cursorrules if needed]
  Rules --> Execute[Execute Task]
  Execute --> Document[Document Changes]
```

### Documentation Updates

```mermaid
flowchart TD
  Start[Update Process]
  subgraph Process
    P1[Review ALL Files]
    P2[Document Current State]
    P3[Clarify Next Steps]
    P4[Update .cursorrules]
    P1 --> P2 --> P3 --> P4
  end
  Start --> Process
```

### Project Intelligence (.cursorrules)

```mermaid
flowchart TD
  Start{Discover New Pattern}
  subgraph Learn [Learning Process]
    D1[Identify Pattern]
    D2[Validate with User]
    D3[Document in .cursorrules]
  end
  subgraph Apply [Usage]
    A1[Read .cursorrules]
    A2[Apply Learned Patterns]
    A3[Improve Future Work]
  end
  Start --> Learn
  Learn --> Apply
```

### What to Capture

* Critical implementation paths
* User preferences and workflow
* Project‑specific patterns
* Known challenges
* Evolution of project decisions
* Tool usage patterns

---

# Planning

When entering **Planner Mode** (command `/plan`):

1. Reflect on requested changes.
2. Analyse existing code.
3. Ask 4‑6 clarifying questions.
4. Draft full action plan, get approval.
5. Implement, documenting each phase and next steps.

REMEMBER: After every memory reset, Memory Bank is the **only** link to previous work.  Maintain it with precision and clarity!
