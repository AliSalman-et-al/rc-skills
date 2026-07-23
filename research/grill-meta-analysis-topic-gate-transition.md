# Prompt-engineering the early viability transition

Research date: 2026-07-23

Scope: `skills/protocol-design/grill-meta-analysis-topic/SKILL.md`, specifically the transition from a rough topic formulation to the published-landscape audit. Sources are limited to first-party Anthropic and OpenAI guidance and the Cochrane Handbook. Context7 was queried first for current Claude Code documentation and resolved `/anthropics/claude-code`.

## Executive recommendation

Turn Gate 1 from an open-ended interview phase into a small transition contract. Define a minimum observable condition for “searchable,” prescribe the action that must happen immediately when it is met, and name the only condition under which another Gate 1 question is allowed. Then represent unresolved choices as state carried into the Gate 2–4 loop.

The current revision points in the right direction, but phrases such as “enough,” “rough,” and “reasonable alternatives” still leave the model to decide whether one more clarifying question would be helpful. The strongest fix is an explicit default:

> **Default to the audit.** Gate 1 exists only to create a provisional search seed, not to finish the review specification. As soon as the population or condition, intervention or exposure, and outcome domain are identifiable—and the comparator is either known or can be represented as `any`, `usual care`, `no exposure`, or explicit alternatives—Gate 1 is complete. In the same turn: (1) state the provisional question, (2) label unresolved elements in the decision backlog, and (3) begin Gate 2. Do not ask another Gate 1 question unless no meaningful broad search can be constructed.

This is an inference from the sources rather than wording prescribed by them. Anthropic recommends clear sequential steps, conditional workflows, explicit feedback loops, and instructions whose specificity matches the fragility of the operation; OpenAI likewise recommends that each workflow step map to a concrete action and that incomplete-input edge cases be expressed as conditional branches ([Anthropic Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices), [Anthropic prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices), [OpenAI, *A practical guide to building agents*](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)).

## Recommended structure

### 1. Put the transition rule before the Gate 1 interview instructions

The skill’s main behavioral correction should be prominent and stated once. Anthropic advises concise skills, consistent terminology, clear steps, and avoiding repeated instructions; current OpenAI model guidance similarly recommends stating each instruction once and validating leaner prompts on representative tasks ([Anthropic Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices), [OpenAI model prompting guidance](https://developers.openai.com/api/docs/guides/latest-model#prompting-best-practices)).

Suggested wording:

```markdown
## Operating rule — audit early

Gate 1 is a search-seed phase, not a full protocol interview. Default to Gate 2.
Once the minimum search seed below exists, begin the landscape audit in the same
turn. Carry uncertainty forward; do not resolve it merely to make the PICO look
complete.
```

This is preferable to intensifiers such as “CRITICAL” or repeated “MUST” statements. Anthropic’s current model guidance warns that aggressive anti-undertriggering language can cause overtriggering and recommends targeted instructions instead ([Anthropic prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices#tool-use)).

### 2. Make “searchable” a checkable predicate

Replace the subjective threshold with a compact rule:

```markdown
The minimum search seed is:

- a named population, condition, or clinical context;
- a named intervention or exposure;
- an intended outcome domain; and
- a comparator that is stated, safely broadened, or listed as alternatives.

The seed is searchable when at least one broad database query can be run without
inventing a clinical concept. Missing setting, exclusions, exact outcome measure,
time point, effect measure, study design, and contribution do not block Gate 2.
```

For evidence discovery, do not require every PICO element to appear in the first query. The Cochrane Handbook says it may be undesirable to search every aspect of the clinical question because comparator and outcome concepts may be absent or poorly indexed; general-database searches commonly emphasize population, intervention, and study design. Cochrane also notes that equal precision across all PICO components is unnecessary ([Cochrane Handbook, Chapter 4 §4.4.2](https://training.cochrane.org/handbook/current/chapter-04#section-4-4-2), [Cochrane Handbook, Chapter 2 §2.3](https://training.cochrane.org/handbook/current/chapter-02#section-2-3)).

### 3. Specify the transition as actions, not permission

“Advance to Gate 2” can still be interpreted as ending the turn after announcing the transition. Make the handoff observable:

```markdown
When the predicate becomes true:

1. Show the one-sentence provisional question and compact PICO/PECO/PICOS.
2. Mark each uncertain element as `[open]` in the decision backlog.
3. Run the first broad Gate 2 search immediately in the same turn.
4. Let the audit determine which open decisions require the next user question.
```

The phrase “in the same turn” is important because it distinguishes an actual tool/action transition from a conversational promise. This follows first-party guidance to define a specific action or output for every step and to be explicit when proactive action is desired ([OpenAI, *A practical guide to building agents*](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/#configuring-instructions), [Anthropic prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices#tool-usage)).

### 4. Narrow the Gate 1 self-loop

Add one explicit exception:

```markdown
Ask another Gate 1 question only if the missing answer prevents any meaningful
broad search—for example, neither the condition/population nor the intervention/
exposure is identifiable. Ask the single question with the highest search impact.
Do not ask for confirmation of the provisional formulation.
```

This conditional branch handles genuinely unusable inputs without allowing “helpful” polishing to become the default. Anthropic presents conditional workflows as the pattern for guiding model decisions, while OpenAI advises anticipating incomplete inputs with explicit alternative branches ([Anthropic Skill authoring best practices, “Conditional workflow pattern”](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices#conditional-workflow-pattern), [OpenAI, *A practical guide to building agents*](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/#configuring-instructions)).

### 5. Make Gates 3–4 the refinement loop

The backlog should have a defined consumer, not merely be recorded:

```markdown
At Gate 3, use the audit to rank open decisions by whether they change overlap,
clinical meaning, or analytical feasibility. At Gate 4, ask one question about
the highest-impact open decision, recommend a pivot grounded in the audit, update
the provisional question, and repeat only the affected Gate 2 checks. Continue
until the topic is viable, viable after a defensible modification, or abandoned.
```

Also broaden Gate 4’s entry condition from only “already covered or not feasible” to any verdict with an unresolved decision that could materially change viability. This makes the desired loop explicit: **seed → audit → verdict → evidence-led re-grill → targeted re-audit**. Anthropic recommends feedback loops for quality-critical work and checkable progress through multi-step workflows ([Anthropic Skill authoring best practices, “Workflows and feedback loops”](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices#workflows-and-feedback-loops)).

## Minimal examples to add

Examples are useful only if testing shows the transition still fails. Anthropic calls examples a reliable steering mechanism but also recommends concise skills and evaluation-driven iteration, so start with one boundary pair rather than several ([Anthropic prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices#use-examples-effectively), [Anthropic Skill authoring best practices, “Build evaluations first”](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices#build-evaluations-first)).

```markdown
Searchable: “GLP-1 agonists for weight loss in adolescents; probably versus
placebo/usual care; weight change is the main outcome.” → State the provisional
PICO, backlog exact age/comparator/time point, and start Gate 2 now.

Not searchable: “I want to do a meta-analysis in cardiology.” → Ask one Gate 1
question that identifies the condition or intervention/exposure.
```

## Evaluation rubric

Test at least these cases across the models the plugin supports:

| Scenario | Passing behavior |
| --- | --- |
| Complete PICO | Starts Gate 2 in the same turn; asks no Gate 1 question |
| Rough PICO with uncertain comparator/time point | Broadens or lists alternatives, records backlog, starts Gate 2 |
| Population + intervention/exposure but vague outcome | Uses an outcome domain or broad discovery search, starts Gate 2 |
| Topic area only | Asks exactly one high-impact Gate 1 question |
| Audit finds a recent close review | Gives Gate 3 verdict, asks one evidence-led Gate 4 pivot question |
| Audit finds sparse/incompatible primary studies | Re-grills toward a defensible modification or stopping decision |

The primary metric should be **whether the first search begins on the first turn in which the minimum seed is present**, not whether the agent verbally says it is moving to Gate 2. Secondary metrics are unnecessary pre-audit questions, invented PICO details, backlog preservation, and whether a pivot triggers only the affected re-search. Anthropic recommends defining success criteria before prompt tuning, creating representative evaluations, and iterating from observed failures rather than assumptions ([Anthropic prompt-engineering overview](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview), [Anthropic Skill authoring best practices, “Evaluation and iteration”](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices#evaluation-and-iteration)).

## Tradeoffs

- A lower Gate 1 threshold increases false starts and broader result sets. That is intentional: Gate 2 is being used as information gathering, and Cochrane cautions against overconstraining searches with every PICO element.
- “Same turn” may create a slower first response because it includes a real search. It is the clearest behavioral test of eagerness and avoids an extra confirmation turn.
- A strict transition predicate reduces conversational discretion. Preserve discretion inside Gate 2 search design and Gate 4 pivots, where context genuinely matters; keep the fragile state transition low-freedom.
- Adding examples costs context. Add them only if the rule-plus-evaluation change does not reliably correct behavior.

## Bottom line

The best prompt-engineering change is not stronger exhortation. It is a deterministic handoff: define the minimum search seed, make the default transition immediate and observable, allow only one narrow blocking exception, and explicitly consume the unresolved-decision backlog in an evidence-led Gate 3–4 loop.
