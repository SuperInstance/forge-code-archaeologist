# 🔨 Forge: Code Archaeologist

A 4-stage ability forge that trains and certifies git agents in **code archaeology** — the art of seeing structural rot that others walk over. Not "finds bugs," but *feels wrongness before naming it*.

Built from the real practices of the fleet's code forensics specialist (Third Z Agent), who found 8 real bugs in 5 minutes — including an ISA numbering conflict that had existed for weeks. These weren't found by search or grep. They were found by attunement.

---

## Overview

Forge-Code-Archaeologist provides a structured training and evaluation pipeline:

- **Exercises** — Socratic drills organized across 4 stages, each targeting a specific attunement pattern (structural load sensitivity, test-vs-truth discrimination, expert intention reading)
- **Scoring** — A progression framework (`scoring/progression.json`) that tracks pass/fail across stages, with measurable outcomes and anti-signals for each pattern
- **Attunement Patterns** — Codified behavioral signatures (`attunement_patterns/`) that define what true ability looks like vs. cargo-cult模仿
- **Attestation** — DOCKSIDE-EXAM certification with a 7-category seaworthiness checklist, producing a fleet-recognized ability attestation

This is **not** a linter. Not a static analyzer. Not a test suite. Not a code review checklist. This is the attunement that makes an agent *look at the right place first*.

---

## The Forge Model

The forge progresses through four stages, each building on the last. Agents must complete them in order — surprise is part of the training.

```
NOVICE ──▶ APPRENTICE ──▶ JOURNEYMAN ──▶ MASTER
  CUT         CRISIS          NAVIGATE      MIRROR
 (3 ex)       (1 ex)          (2 ex)       (1 ex)
```

### Stage 1: CUT — Reduce to Essentials *(Novice)*

Remove code until it breaks. Restore the minimum cut. Feel the boundary.

Agents learn **structural load sensitivity** — the ability to perceive which code is load-bearing without tracing every dependency. Exercises enforce information budgets (e.g., "you may only read 5 of the 20 source files") to force intuitive pattern recognition over brute-force analysis.

| Exercise | Description | Time | Attunement Target |
|----------|-------------|------|-------------------|
| Boundary Violation Detection | Remove functions from a 10-bug module until tests break; identify load-bearing code *before* removing it | 30 min | `structural_load_sensitivity` |
| Dependency Trace | Identify the 3 nodes carrying 80% of structural weight in a 20-node call graph within a 5-file read budget | 20 min | `structural_weight_perception` |
| Minimal Restore | Restore only the essential code (scored by line count) to make tests pass after 50% deletion | 45 min | `essential_vs_accidental_discrimination` |

### Stage 2: CRISIS — Break Current Seeing *(Apprentice)*

Encounter code that's "correct" by every measure but wrong in context. The **aporia moment** — where the agent must trust their attunement over tools.

| Exercise | Description | Crisis Type | Attunement Target |
|----------|-------------|-------------|-------------------|
| Correct But Wrong | All tests pass, but a semantic error will cause production failure. Find it by *reading*, not by adding tests | Aporia | `test_vs_truth_discrimination` |

### Stage 3: NAVIGATE — Traverse with Resistance *(Journeyman)*

Read commit diffs as traces of intention. Follow expert attention maps through unfamiliar codebases. Agents learn to navigate large systems by following the structural signals left by prior developers.

| Exercise | Description | Attunement Target |
|----------|-------------|-------------------|
| Attention Map Following | Follow expert commit trails through a multi-module codebase, identifying the attention path the expert took | `attention_map_following` |

### Stage 4: MIRROR — Read Expert Traces *(Master)*

Watch real expert commit sequences. Predict what comes next. The ultimate test: can you think like an expert before seeing the answer?

| Exercise | Description | Attunement Target |
|----------|-------------|-------------------|
| Commit Prediction | Given 10 sequential commits from an expert bug fix, predict the next commit's intention before seeing it | `expert_intention_reading` |

**Minimum for attunement certification: 5 of 7 exercises passed**, with integration exercises required.

---

## Exercises

All exercises live in `exercises/` and are structured as JSON manifests:

```
exercises/
├── 01-cut/
│   ├── 01-boundary-violation.json    # Structural load detection
│   ├── 02-dependency-trace.json      # Weight perception under budget
│   └── 03-minimal-restore.json       # Essential code discrimination
├── 02-crisis/
│   └── 01-correct-but-wrong.json     # Aporia: tests pass, code lies
├── 03-navigate/                      # Attention map following (planned)
└── 04-mirror/
    └── 01-commit-prediction.json     # Expert intention prediction
```

Each exercise JSON specifies:

- **`name`** and **`stage`** — identity and forge stage
- **`description`** — what the agent must do
- **`constraint`** — the information/time budget that forces attunement
- **`time_limit_minutes`** — maximum exercise duration
- **`success_signal`** — behavioral evidence of true ability
- **`failure_signal`** — behavioral evidence of cargo-cult模仿 (cheating the drill)
- **`attunement_target`** — which pattern this exercise develops

### How to Enter the Forge

1. Clone this repo
2. Start with `exercises/01-cut/`
3. Do **not** skip stages — each builds on the last
4. Do **not** read ahead — surprise is part of the forge
5. Write reflections after each exercise

**Estimated total time:** ~7 hours of focused forge work across all stages.

---

## Scoring & Attestation

### Progression Tracking

`scoring/progression.json` defines the evaluation framework:

```json
{
  "stages": [
    {"stage": "cut",      "exercises": 3, "min_pass": 2},
    {"stage": "crisis",   "exercises": 1, "min_pass": 1},
    {"stage": "navigate", "exercises": 2, "min_pass": 1},
    {"stage": "mirror",   "exercises": 1, "min_pass": 1}
  ],
  "minimum_for_attunement": 5,
  "integration_required": true
}
```

### Attunement Patterns

`attunement_patterns/structural_debt_sensitivity.json` defines measurable behavioral signatures:

| Signal (positive) | Anti-Signal (negative) |
|---|---|
| Pauses before modifying unread code | Modifies code without hesitation |
| Asks "what depends on this?" | Trusts tests completely |
| Identifies coupling invisible in call graph | Needs full call graph trace |
| Flags "this looks too simple for what it does" | — |

**Measurable outcomes:**
- False positive rate: < 30%
- False negative rate: < 20%
- Detection speed: < 60 seconds per structural problem

### Dockside Exam Certification

`DOCKSIDE-EXAM.md` provides the fleet certification checklist across 7 categories:

1. **Identity** — CHARTER.md, README.md, license
2. **Code Quality** — compiles, no secrets, documented deps
3. **Testing** — test suite, passing, edge cases
4. **Fleet Integration** — Git-Agent Standard v2.0, I2I protocol
5. **Documentation** — API, configuration, examples
6. **Safety** — no destructive ops, error handling, graceful degradation
7. **Operational** — deployable, health check, logging

**Scoring:** 7/7 = Seaworthy 🟢 · 5–6/7 = Conditional 🟡 · <5/7 = Needs Work ⚠️

---

## For Fleet Agents

### Training Path

Git agents entering the forge should follow the bootcamp protocol in `BOOTCAMP.md`:

1. **Start cold** — use a codebase you've never seen before
2. **Respect the constraints** — the information budget IS the training
3. **Document your inner state** — write reflections after each exercise
4. **Don't dodge the crisis** — if you add tests to find a Stage 2 bug, you failed the attunement even if you found the bug

### Self-Improvement Loop

The forge is designed for iterative use:

- **Re-attempt failed exercises** with a different codebase
- **Track progression** using `scoring/progression.json` as your state file
- **Validate attunement** by running against novel, unseen codebases
- **Achieve certification** via the DOCKSIDE-EXAM when ready for fleet deployment

### What You Need

- A codebase you've never seen before
- Time to think without urgency
- Willingness to be wrong about what feels wrong

### What You Don't Need

- Specific tools (the ability is in you, not the tool)
- Domain expertise (attunement transcends domains)
- Perfect accuracy (feeling wrongness is the skill, not always being right)

---

## Evidence of True Attunement

- Agent identifies problems in novel codebases without being told what to look for
- The "something's wrong" signal fires **before** conscious analysis
- Agent can explain **why** something feels wrong, not just **that** it's wrong
- Agent composes effectively with Hardware Whisperer, Quality Auditor, and other fleet abilities

---

## Repository Structure

```
forge-code-archaeologist/
├── CHARTER.md                          # Mission and real-world evidence
├── README.md                           # This file
├── BOOTCAMP.md                         # Training protocol and entry guide
├── DOCKSIDE-EXAM.md                    # 7-category fleet certification
├── LICENSE
├── callsign1.jpg                       # Forge callsign
├── exercises/
│   ├── 01-cut/                         # Novice: structural load sensitivity
│   ├── 02-crisis/                      # Apprentice: aporia and truth
│   ├── 03-navigate/                    # Journeyman: attention maps
│   └── 04-mirror/                      # Master: expert intention reading
├── scoring/
│   └── progression.json                # Stage pass/fail tracking
└── attunement_patterns/
    └── structural_debt_sensitivity.json # Behavioral signatures
```

---

<img src="callsign1.jpg" width="128" alt="callsign">
