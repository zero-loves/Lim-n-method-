---
name: limon-method
description: >
  Activate this skill whenever the user uploads or pastes exam question papers and wants structured exam preparation. 
  The skill runs in two phases: a pre-trigger phase where Claude answers all questions immediately upon receiving papers, 
  and a post-trigger phase activated by the codeword "Limón" where Claude performs pattern analysis, generates notes, 
  and produces 4 practice sets with answer keys. Use this skill for ANY subject, ANY exam board — it is a general-purpose 
  exam prep pipeline. Trigger on: uploaded past papers, pasted question papers, requests for exam prep, study notes from 
  past papers, or practice question generation. Do not wait for the user to say "Limón" to begin Phase 1.
---

# Limón Method V2

A two-phase exam preparation pipeline for any subject, any exam board.

---

## Phase 1 — Pre-Trigger (Runs immediately on question paper input)

As soon as the user pastes or uploads question papers, **do not wait for "Limón."** Begin Phase 1 immediately.

### What to do:
1. **Read all question papers in full.** Identify every question including sub-questions.
2. **Answer every single question.** Cover all of them — no skipping, no summarizing groups.
3. Present answers clearly, labeled by paper → section → question number (e.g., Paper 1 → Section B → Q3a).
4. Keep answers accurate, complete, and at the level appropriate for the exam.

### Format:
- Group by paper if multiple papers are given
- Use consistent numbering that mirrors the original paper
- Don't editorialize — just answer

---

## Phase 2 — Post-Trigger (Activated when user says "Limón")

When the user says **"Limón"**, switch into Phase 2. Execute all four steps below in order.

---

### Step 1 — Pattern Analysis

Analyze ALL question papers provided. Extract and report:

- **High-frequency topics** — what concepts appear most often across papers
- **Question type patterns** — MCQ, short answer, essay, calculation, diagram-based, etc.
- **Wording patterns** — recurring command words (explain, describe, evaluate, calculate, compare, state, suggest)
- **Mark distribution** — which topics carry the most marks across papers
- **Topics that always appear vs topics that rotate**
- **Any notable gaps** — topics in the syllabus that rarely or never appear

Present this as a clean, scannable analysis. This is the foundation for the notes and practice sets.

---

### Step 2 — Delivery Format Choice

Ask the user:

> "Do you want your notes delivered as **TXT files** (downloadable, works with NotebookLM) or **in the messages** (inline)?"

Wait for their answer before proceeding.

---

### Step 3 — Notes Generation

Generate detailed, simple notes based on:
- The high-frequency topics from Pattern Analysis
- Any source material the user provides (uploaded notes, textbook content, etc.)
- The question paper content itself if no external sources are given

#### Notes must be:
- **Detailed** — cover the concept fully, don't assume prior knowledge
- **Simple** — plain language, no unnecessary jargon unless the exam requires it
- **Structured for dual processing** — readable by a human AND processable by NotebookLM or similar AI tools

#### Structure for NotebookLM + human compatibility:
```
# [Topic Name]

## Key Concepts
[Clear definitions and explanations]

## How It Works / How It Applies
[Mechanism, process, or application]

## Common Exam Angles
[How examiners typically ask about this topic based on pattern analysis]

## Key Terms
[Glossary of essential vocabulary]

## Watch Out For
[Common mistakes or tricky phrasing]
```

Use this structure for every major topic. If delivering as TXT files, create one file per topic cluster. If inline, use headers to separate cleanly.

---

### Step 4 — 4 Practice Sets

Generate **4 full practice sets** following the school repetition model.

#### The school repetition rule:
Schools repeat questions across years — same concepts, same structure, slightly different phrasing or numbers. Sets should work the same way:

- **Set 1** — Closest to original papers. Questions use familiar phrasing, same command words, same structure. High overlap with actual past paper patterns.
- **Set 2** — Same topics, slightly varied phrasing. Some command words swapped (e.g., "describe" → "explain"). Context examples changed.
- **Set 3** — Same topics, more varied scenarios. The underlying concept tested is identical but the surface presentation shifts.
- **Set 4** — Most varied surface presentation while still testing the same core patterns. A student who can answer Set 4 can handle any paper.

**Difficulty does not increase across sets.** The exam standard stays constant. Only surface variation increases.

#### Each set must include:
- A clean question paper (numbered, organized by section if applicable)
- A **separate answer key** for that set — clearly labeled, not mixed into the question paper
- Mark allocations mirroring the original papers

#### Format:
```
--- SET [N] — QUESTION PAPER ---
[Questions here]

--- SET [N] — ANSWER KEY ---
[Answers here]
```

Keep all 4 sets separated. Do not bundle them together. Do not reference other sets within a set.

---

## General Rules

- **Subject agnostic** — this pipeline works for sciences, humanities, mathematics, languages, social studies, anything
- **No calibration table** — answer depth follows the mark allocation on the actual paper, not a fixed formula
- **Organization is non-negotiable** — messy output defeats the purpose; use headers, clear labels, consistent numbering at all times
- **NotebookLM compatibility** — when generating TXT files, avoid heavy markdown formatting (no nested bullets more than 2 levels deep, use plain headers, avoid tables in favor of structured prose where possible)
- **Don't summarize what you're about to do** — just do it

---

## Quick Reference

| Trigger | Action |
|---|---|
| User pastes/uploads question papers | Begin Phase 1 immediately — answer all questions |
| User says "Limón" | Begin Phase 2 — pattern analysis → delivery choice → notes → 4 practice sets |
