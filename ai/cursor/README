# Using Cursor for AI-Assisted Cedar Policy Authoring

This directory demonstrates how AI-assisted development tools—such as Cursor—can be used to help **author, review, and refine Cedar authorization policies** safely. The goal is to improve the human workflow around policy-as-code without weakening deterministic policy evaluation or enforcement.

This material supports **Appendix B** of *Dynamic Authorization* and builds directly on the ACME Cedar schema and policies introduced in Appendix A.

## Scope and boundaries

The guidance in this directory is intentionally narrow.

AI tools may be used to:
- Draft policy candidates from natural-language intent
- Explain what existing policies do
- Suggest refactoring or normalization
- Generate example requests and test cases

AI tools must **not** be used to:
- Make authorization decisions at runtime
- Modify policies without human review
- Bypass testing, version control, or approval workflows
- Grant access or exceptions directly

Policies define authority. AI output is advisory.

## Repository context

This repository reuses the ACME Cedar artifacts without modification:

- `cedar/acme.cedarschema` is the source of truth for entities, actions, and attributes
- `cedar/policies/` contains the canonical policy files
- `cedar/acme-entities.json` provides example entities for evaluation and testing

When using Cursor, these files should always be included as context. The model should never invent new entities, actions, or attributes. Any proposed schema change must be called out explicitly and reviewed like any other architectural change.

## Recommended workflow

A safe AI-assisted policy authoring workflow looks like this:

1. A human expresses policy intent in natural language
2. The AI proposes a draft Cedar policy or modification
3. A human reviews the proposal for correctness, scope, and unintended access
4. Test cases are added or updated to reflect the intended behavior
5. Policies are committed and evaluated by the Cedar policy engine

At no point does the AI evaluate authorization requests or enforce access. Deterministic policy evaluation remains the responsibility of the policy engine.

## Human review is required

Human review is not a formality. Policies often fail in subtle ways, including:
- Over-broad permissions
- Missing constraints
- Incorrect assumptions about default behavior
- Unintended interactions between policies

AI-generated policy should be treated like code written by a junior engineer: useful, but never trusted without careful review. Review should focus on **semantic intent**, not just syntactic correctness or passing tests.

## Getting started with Cursor

When opening this repository in Cursor:

1. Include the following files as context:
   - `cedar/acme.cedarschema`
   - All files under `cedar/policies/`
   - Relevant examples or tests
2. Use the starter prompt in `starter-prompt.md` as the basis for AI interaction
3. Ask the model to:
   - Propose the smallest possible policy change
   - Explain what access the policy grants and denies
   - Identify potential edge cases or abuse scenarios

Do not allow Cursor to automatically apply changes without review.

## Supporting files

This directory includes two supporting files that define how AI assistance should be used:

- `starter-prompt.md`  
  A reusable base prompt for working with Cursor. Use this as the starting point for AI-assisted policy drafting, refactoring, and explanation.

- `authoring-guidelines.md`  
  A human review checklist and set of guardrails for accepting AI-assisted policy changes. These guidelines apply to every policy modification, regardless of whether it was drafted by a human or an AI tool.

Read both files before using Cursor with this repository.

## Tooling notes

Cedar does not require specific filenames, but some editor features assume conventions. This repository preserves the domain-specific naming used in Appendix A (for example, `acme.cedarschema`) to reinforce that schemas and policies are architectural artifacts, not tooling defaults.

## Relationship to the book

This directory exists to support hands-on exploration of AI-assisted policy authoring. It is not required to understand the core arguments of the book. Readers who prefer to focus on concepts can safely skip this material.

For a discussion of how authorization and AI interact at runtime, including data retrieval and LLM integration, see Chapter 17. For agentic systems and delegated authority, see Chapter 18.