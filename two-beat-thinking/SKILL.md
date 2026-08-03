---
name: two-beat-thinking
description: "Use when the user wants to turn messy or unstructured thoughts into a decision and a concrete next action. Trigger on requests for ideation with structure, brainstorming that must end in an action, weighing options, sorting priorities, untangling worries or emotions, pre-meeting prep, project kickoff planning, or explicit mentions of 'Two-Beat Thinking', 'two-beat thinking', '두 박자 사고법', 'Stage 1 / Stage 2', 'brain dump', 'thought sprint', 'dump and distill', or '사고 정리'."
---

# Two-Beat Thinking

A structured reasoning skill that converts unfiltered thoughts into a validated decision and an immediately startable action. Time-boxes are removed; only the logical structure is enforced.

## Core Contract (Non-Negotiable)

Every invocation of this skill MUST produce, in order:

1. **Gate** — classify the topic (Section 1). Never skip.
2. **Frame** — one-sentence outcome statement (Section 2).
3. **Dump** — divergent thought expansion (Section 3).
4. **Distill** — grouped, filtered, prioritized synthesis (Section 4).
5. **Decide** — 1-2 actions in strict format (Section 5).
6. **Reflect** — validation signals + next checkpoint (Section 6).

If any step is omitted, the skill has failed. "Dump" without "Decide" is brainstorming, not this skill.

---

## 1. Gate — Topic Classification (Runs First, Always)

Before any expansion, silently classify the user's topic into exactly one preset. Do NOT ask the user; infer from the request. State the chosen preset at the top of the output as `Preset: <name>`.

| Preset | Trigger Signals (any language) | Frame Bias | Depth |
|---|---|---|---|
| `morning-plan` | "today", "priorities", "what first", "우선순위", "오늘" | Now / Next / Later | Light |
| `pre-meeting` | "before meeting", "prep", "회의 전", "미팅 전" | Goal / Question / Ask | Light |
| `emotion-sort` | "anxious", "stuck", "frustrated", "답답", "불안", "화", "고민" | Fact vs Emotion, Controllable vs Not | Full |
| `decision` | "choose", "A vs B", "should I", "결정", "선택" | Options × Criteria matrix | Full |
| `kickoff` | "new project", "start", "킥오프", "시작하려고" | Risk / Assumption / First step | Full |
| `end-of-day` | "wrap up", "review", "마감", "정리하고" | Done / Pending / Carry-over | Light |
| `default` | none of the above match | Problem / Options / Action | scales with complexity below |

If `default`, additionally run this 4-check to pick depth:

1. Are there 2+ stakeholders with different needs?
2. Are there 3+ meaningful options or trade-offs?
3. Is the cost of a wrong decision high (time, money, trust, relationships, health)?
4. Does the topic carry emotional load?

Depth mapping: `0-1 yes → Light`, `2-4 yes → Full`. Any "yes" on check 4 forces at least Full and activates the Fact-vs-Emotion split in Distill.

---

## 2. Frame — One-Sentence Outcome

Output exactly one sentence answering: **"After this sprint, what must be different?"**

Rules:
- Must contain a change verb (decide, choose, start, stop, clarify, prioritize, unblock).
- Must be observable (a reader can tell if it happened).
- Never a question. Never a wish. Never a feeling.

Bad: "정리하고 싶다" / "I want to feel better"
Good: "Choose one of the three vendor options by end of this session" / "3개 벤더 옵션 중 1개를 이 세션 안에서 결정한다"

---

## 3. Dump — Divergent Expansion

Rules:
- 8-15 bullets for Light, 15-25 for Full.
- No filtering, no ordering, no deduplication yet.
- Each bullet MUST be concrete (name a person, artifact, number, event) or explicitly labeled `[feeling]`, `[assumption]`, `[unknown]`.
- Cover at minimum these angles when relevant: user/stakeholder, product/artifact, risk, blocker, opportunity, emotion, unknown.

Anti-pattern: vague bullets like "improve UX", "think more", "be careful". Reject and rewrite.

---

## 4. Distill — Convergent Synthesis

Apply three passes in order:

1. **Group** — cluster the dump into 3-5 named themes.
2. **Cut** — mark every item as `[now]`, `[later]`, or `[drop]`. No item may remain untagged.
3. **Rank** — order the `[now]` items by leverage (impact ÷ effort).

Frame overlays (apply based on Preset):
- `emotion-sort` or check-4 triggered → add a **Fact / Emotion** split, then a **Controllable / Not-controllable** split.
- `decision` → build an **Options × Criteria** table with a score per cell and a total row.
- `kickoff` → produce a **Risk / Assumption / Unknown** table.

---

## 5. Decide — Action (Strict Format)

Output 1-2 actions. Never zero. Never more than two.

Each action MUST follow this schema:

```
Action:      <verb> <object>
First step:  <the very first sub-action, small enough to start without further planning>
Rationale:   <why this beats alternatives, in one line>
Assumption:  <the single load-bearing assumption>
Risk:        <what breaks it, in one line>
Validation:  <the observable signal that proves it worked>
```

Enforcement rules:
- `Action` must start with an imperative verb (Draft, Send, Call, Choose, Delete, Publish, Ask, Measure). Reject "consider", "explore", "think about", "look into".
- `First step` must be executable with no further inputs. If it needs an input, the missing input IS the first step.
- If the sprint genuinely has no viable action, the action becomes `Schedule a follow-up sprint with <specific missing input>`. Never "do nothing" silently.

---

## 6. Reflect — Validation and Next Checkpoint

Close every sprint with:

- **Success check** — the concrete observation that proves the action worked (metric, artifact, event).
- **Failure check** — the concrete observation that proves it did not.
- **Next sprint trigger** — the event that should launch the follow-up sprint (e.g., "after sending the draft", "if no reply by Thursday", "when the vendor quote arrives").

This closes the loop and prevents the sprint from degrading into one-shot brainstorming.

---

## Output Template (Copy Exactly, Fill In)

```md
Preset: <preset-name> (Depth: Light | Full)

Frame
<one sentence>

Dump
- ...
- ...

Distill
Themes
- Theme A: [now/later/drop] items...
- Theme B: ...
(overlay tables here if the preset requires)

Ranked Now-items
1. ...
2. ...

Decide
Action 1:
  Action:      ...
  First step:  ...
  Rationale:   ...
  Assumption:  ...
  Risk:        ...
  Validation:  ...

(Action 2 only if warranted)

Reflect
- Success check: ...
- Failure check: ...
- Next sprint trigger: ...
```

---

## Style Requirements

- Reply in the user's language. If the user mixes languages, mirror the dominant one; section headers stay in that language.
- Direct, implementation-level phrasing. No motivational filler ("You've got this", "Great question").
- Assumptions must be labeled as assumptions. Never present a guess as a fact.
- When evidence is missing, write `[assumption]` inline rather than hedging with "maybe" or "perhaps".

---

## Failure Conditions (Skill Has Failed If)

- Gate step is skipped or the chosen preset is not stated.
- Frame is a question, a feeling, or missing.
- Dump contains vague non-concrete bullets that were not rejected.
- Distill does not tag every item as now/later/drop.
- Decide produces zero actions, or produces an action starting with "consider/explore/think about".
- Any Decide field (First step, Rationale, Assumption, Risk, Validation) is missing or empty.
- Reflect section is omitted.
- Skill is used as generic brainstorming without producing an action.
