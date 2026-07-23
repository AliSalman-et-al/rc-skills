---
name: grill-meta-analysis-topic
description: Validate a proposed meta-analysis topic against the published evidence.
disable-model-invocation: true
---

# Validate a Meta-Analysis Topic

Run an evidence-led viability loop: **seed → audit → verdict → re-grill → targeted re-audit**. Use the model-invoked `grilling` skill for the interview and the model-invoked `pubmed` skill for reproducible biomedical searches.

## Operating rule — audit early

Gate 1 creates a provisional search seed; it does not finish the review specification. Default to Gate 2 as soon as the minimum seed exists. Carry uncertainty forward so the published landscape determines which decisions deserve further grilling.

## Gate 1 — Reach a searchable baseline

The minimum search seed has:

- an identifiable population, condition, or clinical context;
- the focal intervention, exposure, test, prognostic factor, or other synthesis target;
- an intended outcome domain or quantity to estimate; and
- enough information to run at least one broad search without inventing a clinical concept.

A missing comparator does not block the audit when it can be represented as any comparator, usual care, no exposure, or explicit alternatives. Exact setting, exclusions, outcome measure, time point, effect measure, study design, and contribution also remain open when a broad search is possible.

When the minimum seed exists, act in the same turn:

1. State the provisional one-sentence question and compact PICO/PECO/PICOS.
2. Mark every unresolved element as `[open]` in a decision backlog.
3. Begin the first broad Gate 2 search.
4. Let the audit determine the next question.

Ask another Gate 1 question only when a missing answer prevents any meaningful broad search. Ask the single question with the greatest effect on searchability, give your recommended answer with a short methodological rationale, and wait for the user's judgment. Retrieve factual answers instead of asking the user for them.

Maintain the provisional question, working title, PICO/PECO/PICOS, and decision backlog throughout the loop. Search reasonable alternatives for open elements. When an answer or audit finding changes one element, revisit every dependent choice.

## Gate 2 — Audit the published landscape

Search broadly enough to falsify novelty, not merely support it.

### Find prior syntheses

Run reproducible PubMed searches for exact and adjacent systematic reviews and meta-analyses. Vary terminology, MeSH terms, acronyms, spelling, intervention or exposure class, population breadth, outcomes, and review type. Inspect reference lists and related articles to find reviews missed by the first query.

Search the wider web for:

- Cochrane reviews and protocols;
- PROSPERO, OSF, and other relevant registrations;
- journal sites, DOI records, preprints, conference material, and specialty-society publications;
- non-PubMed-indexed reviews and recent online-first publications.

Record every exact query, source, search date, result count when available, and link. Separate published reviews from protocols, registrations, and ongoing work.

For each serious overlap candidate, extract:

- last search date and publication date;
- review question and eligibility criteria;
- included studies and sample size;
- outcomes, subgroups, effect measures, and synthesis methods;
- conclusions, limitations, and author-stated research gaps.

Appraise whether each close review deserves to constrain the proposed topic. Use ROBIS to judge risk of bias and AMSTAR 2 when its scope fits the review. Examine protocol or registration concordance, search coverage and recency, duplicate screening and extraction, excluded-study handling, risk-of-bias methods, synthesis choices, publication-bias assessment, conflicts, and certainty of evidence. Report domain judgments rather than converting the tools into a single score.

Call a review **high quality** only when the structured appraisal supports that judgment. A close but unreliable review may create a replication or methods-improvement opportunity rather than making the topic non-viable.

### Test analytical feasibility

Locate the likely primary studies and determine whether enough independent, sufficiently comparable data exist. Check outcome definitions, time points, effect measures, duplicate cohorts, extractable data, clinical and methodological heterogeneity, and whether one study would dominate the synthesis.

The audit is complete only when exact duplicates, adjacent reviews, registered or ongoing reviews, close-review quality, and primary-study feasibility have all been checked.

## Gate 3 — Give an overlap verdict

Classify the baseline topic:

- **Viable:** no close synthesis exists, a defensible contribution remains, and the primary evidence can support it.
- **Viable if modified:** overlap exists, but a clinically or methodologically justified distinction can be tested.
- **Not currently viable:** a recent high-quality review answers essentially the same question, or the primary evidence cannot support the proposed synthesis.

Show an overlap matrix comparing the proposed topic with the closest reviews across population, intervention/exposure, comparator, outcomes, study designs, search date, and synthesis method. Cite the strongest evidence for the verdict and label inference explicitly.

Novelty alone is insufficient. A viable topic must also be clinically meaningful, methodologically coherent, and feasible with the available evidence.

Before moving on, rank `[open]` decisions by whether they could change overlap, clinical meaning, or analytical feasibility. Carry material open decisions into Gate 4 even when the provisional verdict is viable.

## Gate 4 — Re-grill material open decisions and pivots

Ask one question about the highest-impact open decision. Give a recommended resolution or pivot grounded in the audit, then wait for the user's choice. If no open decision could materially change the verdict, retain the current formulation.

Consider only distinctions with a defensible rationale, such as:

- a materially different population, setting, comparator, outcome, or follow-up period;
- evidence published after the prior review's search date;
- a neglected subgroup that can be defined without arbitrary slicing;
- a different eligible design or estimand;
- dose-response, diagnostic, prognostic, network, individual-participant-data, cumulative, or living synthesis when the data and question justify it;
- resolving a documented methodological weakness in prior reviews.

After each accepted change, rewrite the question and repeat only the affected Gate 2 checks. Treat a pivot as viable only after research shows that it is distinct and feasible. Continue the **verdict → re-grill → targeted re-audit** loop until the user confirms a formulation supported by the audit, or accepts that no defensible version is currently available.

## Deliver the viability brief

Return:

1. final working title and one-sentence question;
2. compact PICO/PECO/PICOS and review type;
3. verdict with confidence and rationale;
4. closest published and registered overlaps with citations, links, and structured quality judgments;
5. exact search log and cutoff date;
6. primary-study feasibility, anticipated heterogeneity, and major risks;
7. the defensible contribution or the reason to stop.

Leave protocol drafting for a separate request.
