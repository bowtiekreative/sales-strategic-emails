---
name: knowledge-bank-builder
description: >
  Build interconnected knowledge banks from multiple sources — methodologies,
  philosophies, frameworks — organized as Hermes-compatible skills with
  scenario maps, people maps, tension maps, and decision trees.
toolsets:
  - file
  - terminal
  - web
  - search
---

# Knowledge Bank Builder 🧠

**Create Hermes-compatible skill repos that function as interconnected knowledge graphs.**

This is a **meta-skill** — a skill for building skills. Use it when you need to encode a domain of expertise (sales methodologies, leadership frameworks, design systems, negotiation tactics, etc.) into a repository of loadable Hermes skills that an AI agent can navigate, combine, and apply.

---

## 📋 When to Use This Skill

### TRIGGER CONDITIONS — Load this when:

- Someone asks: *"Create a repo of skills about [domain]"*
- You're asked to synthesize 3+ related sources/methodologies/thinkers
- The goal is an **agent-usable knowledge base**, not just a reference doc
- The user wants interconnected, cross-referenced skills (a "brain," not a "list")
- You're building a skill collection that needs a decision tree / scenario map

### DO NOT load this when:

- Building a single isolated skill (use `hermes-agent-skill-authoring` instead)
- The sources have no meaningful connections or overlap
- It's a simple FAQ or documentation dump (overkill)

---

## 🏗️ The 5-Phase Workflow

### Phase 1: PREPARE — Gather & Define

```
Input:  Domain name + list of sources/methodologies/thinkers
Output: Source inventory + metadata table
```

1. **Name the domain** — make it specific and searchable (e.g., "Sales Strategy" not "Business")
2. **Inventory every source** — list each methodology, thinker, or framework the user named
3. **For each source**, identify at minimum:
   - Core thesis (one sentence)
   - Key principles / frameworks (3-7)
   - Best use case (what scenario does this dominate?)
   - Worst use case (when does this fail?)
   - Signature techniques (tactics, phrases, scripts)
4. **Set up the repo**:
   ```bash
   git init <repo-name>
   mkdir -p skills/
   ```

### Phase 2: EXTRACT — Build Each Skill

```
Input:  Source inventory
Output: N x SKILL.md files (one per source)
```

For each source, write a `SKILL.md` in `skills/<kebab-name>/SKILL.md` with:

**Frontmatter:**
```yaml
---
name: chris-voss-negotiation
description: "FBI hostage negotiation — tactical empathy, mirroring, labeling"
toolsets:
  - file
  - terminal
---
```

**Body structure (every skill MUST have):**

| Section | Purpose | Required? |
|---------|---------|-----------|
| **Core Thesis** | One-sentence elevator pitch | ✅ |
| **Principles** | 3-7 actionable principles with explanations | ✅ |
| **Frameworks** | Step-by-step mental models (e.g., Ackerman model, 7 Steps) | ✅ |
| **Email/Response Templates** | Real templates the agent can use immediately | ✅ |
| **Pitfalls** | "What NOT to do" — table with Why and How-to-Fix | ✅ |
| **Trigger Conditions** | When to / when NOT to use this skill | ✅ |
| **Combination Notes** | Which other skills this plays well with | ✅ |

**File structure:**
```
skills/
├── chris-voss-negotiation/
│   └── SKILL.md
├── art-of-war/
│   └── SKILL.md
├── spin-selling/
│   └── SKILL.md
```

### Phase 3: MAP — Build the Connection Layer

```
Input:  All SKILL.md files
Output: Scenario map + people map + tension map
```

This is what transforms a **list** into a **brain**. Three maps:

#### A. Scenario Map (Situation → Method)
Build a table where rows are scenarios and columns are:
- **Primary Skill** — the best single method
- **Secondary Skill** — what complements it
- **Why** — one-sentence rationale

Cover every phase of your domain:
```
| Scenario | Primary | Secondary | Why |
|----------|---------|-----------|-----|
| Objection: price | Voss | Yin Yang | Mirror + flip |
```

Use the decision pattern:
```
For each scenario, ask:
- Which method owns this situation? (Primary)
- Which method covers the blind spots? (Secondary)
- Why does this pair work?
```

#### B. People Map (Method → Method connections)
Build a relationship graph. For each pair of methods, determine:

| Connection Type | Meaning |
|-----------------|---------|
| **Parent→Child** | One directly influenced/created the other |
| **Soul Brothers** | Same energy, different packaging |
| **Siblings** | Same tree, different branch |
| **Rivals** | Same arena, different approach |
| **Opposites** | Fundamentally incompatible philosophy |
| **Best Friends** | Cover each other's weaknesses perfectly |
| **Frenemies** | Would argue but both win |
| **Teacher→Student** | One is derived from the other |
| **Incompatible** | Never combine — they cancel out |
| **Meta-Parent** | One orchestrates all the others |

Render as an ASCII graph showing connections, then a relationship table.

#### C. Tension Map (Anti-Patterns)
Identify pairs that should NEVER be combined, with specific reasons:
```
| Don't Use A | With B | Why It Breaks |
|-------------|--------|---------------|
| Aggressive close | Long-game patience | Contradictory signals |
```

Also build an axis map showing methods on spectrums:
```
AGGRESSIVE ←──────────────────────────→ PATIENT
    Belfort · Cardone         Vee · Voss · Best Block

LOGICAL ←──────────────────────────────→ PSYCHOLOGICAL
    SPIN · Xerox · Solutions   Voss · Robbins · Yin Yang
```

### Phase 4: SYNTHESIZE — The Decision Tree + Meta-Pattern

```
Input:  All maps
Output: Decision tree + meta-pattern
```

#### The Decision Tree
A single flow from `START HERE` that an agent can traverse:

```
START HERE
│
├─ Is this a COLD OUTREACH?
│   ├─ B2B → SPIN
│   └─ Content-first → Vee
│
├─ Is this an OBJECTION?
│   ├─ Price → Voss + Yin Yang
│   └─ Competitor → Best Block + Art of War
│
└─ ...
```

Each branch ends in a **skill name** the agent can load.

**Design principles for the tree:**
- Each question is a **present-tense scenario** ("Am I facing...")
- Each answer is a **skill** (not an abstract category)
- Terminal nodes are **always skill names** — never "depends"
- If a branch needs sub-reasoning, make sub-branches

#### The Meta-Pattern
Reduce the entire knowledge bank to 2-3 core questions that span all methods:

```
All 12 methods reduce to:
1. Who are they? (their needs, fears, position)
2. Where am I? (my strengths, weaknesses, leverage)
3. How do I move forward? (the next inch)
```

And one-sentence theses for each skill:
```
| Skill | One-Sentence Thesis |
|-------|---------------------|
| Voss  | "No is the start"   |
```

### Phase 5: PACKAGE — The README as Knowledge Brain

```
Input:  All maps + tree + meta-pattern
Output: README.md that is itself a decision engine
```

**The README must be structured so an agent can read it and immediately navigate:**

1. **Scenario Map** — the primary navigation table
2. **People Map** — ASCII graph + relationship matrix
3. **Tension Map** — what breaks, what's incompatible
4. **Decision Tree** — the full flow
5. **One-Liner Reference** — quick theses
6. **Meta-Pattern** — the 3 core questions
7. **Skills Directory** — simple list of what exists

Then commit and push:
```bash
git add -A && git commit -m "🧠 Initial knowledge bank with N skills + maps"
git push
```

---

## 📁 Repo Structure (canonical)

```
<repo-name>/
├── README.md          ← The knowledge brain (maps, tree, meta-pattern)
├── SYNTHESIS.md       ← Deep synthesis document (optional - for large domains)
└── skills/
    ├── <method-a>/
    │   └── SKILL.md
    ├── <method-b>/
    │   └── SKILL.md
    └── ...
```

---

## 🧠 Principles

### 1. More connections beats more content
A repo with 12 interconnected skills is **more valuable** than 50 isolated ones. Every connection you draw adds combinatorial intelligence.

### 2. The README is the engine
Don't hide the maps in a separate file. The README must be the thing an agent reads to navigate. It should be self-contained.

### 3. Every skill has an anti-skill
For every method, know when it **fails**. Capture this in the tension map. This prevents agents from applying the wrong tool.

### 4. The decision tree is the agent's interface
An agent doesn't think "which methodology is best?" — it thinks "what scenario am I in?" Design the tree around the agent's perspective.

### 5. One-liners are the API
Each skill's one-sentence thesis is how an agent decides whether to load it. Make them sharp and memorable.

### 6. Pitfalls are the validator
Every skill must have a pitfalls section. This is where agents learn what not to do — often more important than what to do.

---

## ⚠️ Pitfalls

| Mistake | Why It's Bad | Fix |
|---------|-------------|-----|
| **Listing without connecting** | Just a file dump — not a knowledge brain | Always build the three maps (scenario, people, tension) |
| **Vague decision tree** | "It depends" at leaf nodes | Every terminal must be a skill name |
| **No anti-patterns** | Agent combines incompatible methods | Always build the tension map |
| **Over-abstracting** | "Sales strategies" when you mean "SPIN's Implication questions" | Be concrete — use skill names and technique names |
| **Skipping the meta-pattern** | 12 disconnected tools with no unifying insight | Always reduce to 2-3 core questions |
| **Forgetting file structure** | Skills dumped in root | Each skill gets its own directory with SKILL.md |
| **No trigger conditions per skill** | Agent doesn't know when to use each one | Every SKILL.md needs When to Use / When NOT to Use |

---

## 🔗 Combining with Other Skills

| Skill | Why |
|-------|-----|
| **hermes-agent-skill-authoring** | Use for single-skill creation. Use this skill when building 3+ interconnected skills. |
| **plan** | Use for complex knowledge banks (8+ sources). Draft a plan first. |
| **spike** | Use to validate a single technique or method before building the full SKILL.md |

---

## ✅ Verification Checklist

Before calling a knowledge bank complete:

- [ ] Every source has a `skills/<name>/SKILL.md` with all required sections
- [ ] README has a **Scenario Map** covering ALL major domain scenarios
- [ ] README has a **People Map** with connection types for every pair
- [ ] README has a **Tension Map** with at least 3 anti-patterns
- [ ] README has a **Decision Tree** from START to skill names
- [ ] README has **One-Liner Theses** for every skill
- [ ] README has a **Meta-Pattern** (2-3 core questions)
- [ ] README references skills by name (loadable)
- [ ] All frontmatter is valid YAML
- [ ] Each skill has ✅ trigger conditions
- [ ] Each skill has ⚠️ pitfalls
- [ ] git initialised and pushed to GitHub
