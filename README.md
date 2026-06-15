# LLM Prompt Evaluation and Failure Analysis

A systematic analysis of ambiguity, assumptions, and evaluation instability in large language models.

## Overview

This project presents a curated evaluation suite of 10 prompt scenarios designed to surface common failure modes in large language models (LLMs). Each prompt is analyzed for issues such as:

- Ambiguity handling
- Implicit assumption injection
- Temporal inconsistency
- Subjective scoring instability

Each scenario includes the observed model output, a classified failure type, a failure analysis, the expected correct behavior, and (where applicable) a corrected prompt with improved model output.

## Tools Used

- **ChatGPT (GPT-5.2)** — primary model used to evaluate prompt response behavior, failure modes, and consistency issues.
- **Notion** — used to structure documents and present prompt evaluations and findings.
- **Wispr Flow** — used for voice dictation to capture prompt ideas and evaluation notes during analysis.

## Evaluation Methodology

Each prompt was evaluated by analyzing the model's response for one dominant failure mode that most affected output quality. The evaluation focuses on how the model handles:

- Ambiguity
- Implicit assumptions
- Instruction adherence
- Contextual consistency

For every prompt, the observed error is documented, the failure type is classified, and a corrected prompt or expected response is provided to demonstrate mitigation. This project prioritizes clear failure identification and practical prompt refinement over exhaustive scoring.

## Prompt Scenarios

| # | Scenario | Failure Type | Summary |
|---|----------|--------------|---------|
| 1 | Apple Review | Lexical Ambiguity | Model assumed "Apple" referred only to the tech company, ignoring the fruit interpretation. |
| 2 | Stranger Things Summary | Factual Incompleteness & Hallucination | Model omitted the latest season and fabricated speculative details about an unannounced/unverified future season. |
| 3 | Resume Review Feedback | Non-Deterministic Evaluation / Calibration Error | Model gave inconsistent scores and judgments across multiple runs due to lack of a fixed rubric. |
| 4 | Common Sense Review | None | Model demonstrated appropriate common-sense reasoning; no failure observed. |
| 5 | Instruction-Following (Pros/Cons) | Instruction-Following / Formatting Error | Model failed to format five distinct bullet points as instructed, despite correct content. |
| 6 | Email Generation Feedback | Contextual / Role Assumption Error | Model assumed an incorrect sender-recipient hierarchy when roles were unspecified. |
| 7 | Comparison Parameters Review | Under-Specified Comparison | Model gave a definitive "better device" verdict without clarifying comparison criteria. |
| 8 | Image Generation (Blue Car) | None | Model followed user intent correctly; no failure observed. |
| 9 | Image Generation (Dog Frame) | Subject Assumption Error | Model completed the task without asking for unspecified subject characteristics (the dog). |
| 10 | Pronoun (Un)Ambiguity | Overconfident Disambiguation / Hallucinated Assumption | Model resolved an inherently ambiguous pronoun reference with unwarranted confidence. |

## Meta Analysis and Cross-Prompt Observations

This evaluation reveals several recurring behavioral patterns in LLMs when responding to underspecified, ambiguous, or constraint-heavy prompts. Rather than isolated failures, the observed issues cluster into a small set of dominant failure modes that consistently impact output quality.

### Most Common Failure Types

1. **Implicit Assumption Injection** — the most frequent failure, where the model generates output based on assumptions rather than requesting clarification. Seen in role assumptions, subjective comparisons, and pronoun resolution tasks.
2. **Overconfident Disambiguation** — the model produces a single definitive answer despite insufficient information, particularly with ambiguity-sensitive terms.
3. **Instruction-Following / Formatting Errors** — occur when prompts are logically valid but contain complex or layered formatting instructions.

### Clarification vs. Completion

The analysis highlights a critical distinction:

- **Clarification is preferred** when ambiguity directly affects factual correctness or task intent.
- **Clarification is optional** when the task can be reasonably completed without it. In these cases, the model may complete the task first and offer refinement afterward.

### Implications for Prompt Design and Evaluation

These findings suggest that high-quality prompt evaluation should prioritize ambiguity detection, assumption suppression, and explicit uncertainty handling over surface-level correctness. Prompt refinements that explicitly constrain scope, define roles, or enforce evaluation rubrics significantly improve response stability, reliability, and contextual accuracy. Overall, the results reinforce that prompt design should be treated as an iterative control mechanism rather than a one-shot instruction.

## Repository Structure

```
.
├── README.md
└── LLM_Prompt_Evaluation_and_Failure_Analysis.md   # Full evaluation document with prompts, observed/improved outputs, and links
```
