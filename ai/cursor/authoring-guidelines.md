# Human Review Guidelines for AI-Assisted Policy Authoring

These guidelines apply to any Cedar policy authored or modified with AI assistance. They exist to ensure that human intent, accountability, and deterministic evaluation remain central to authorization decisions.

AI output is never authoritative.

---

## Core principles

- Policies define authority and must be reviewed with care.
- AI assists with drafting and explanation; it does not decide access.
- Deterministic evaluation by the policy engine is the only source of truth.
- Human reviewers are accountable for policy outcomes.

---

## Required review checks

Before accepting any AI-assisted policy change, confirm that:

### 1. Intent is preserved
- The policy matches the stated business intent.
- No additional permissions are granted implicitly.
- Defaults and fall-through behavior are understood.

### 2. Scope is constrained
- Access is limited to the minimum required set of principals, actions, and resources.
- Conditions are explicit, not implied.
- Broad grants are intentional and justified.

### 3. Schema usage is correct
- All entities, actions, and attributes exist in `acme.cedarschema`.
- No attributes are assumed or inferred.
- Any schema change is proposed separately and reviewed explicitly.

### 4. Policy interactions are considered
- The policy does not unintentionally override or combine with existing policies.
- Forbid and Permit semantics are well understood.
- Ordering and evaluation effects are considered.

### 5. Tests reflect intent
- New or modified policies include:
  - At least one Permit case
  - At least one Deny case
  - At least one edge or boundary case
- Tests verify *semantic* behavior, not just syntax.

---

## Common failure modes to watch for

AI-generated policies often fail in subtle ways, including:
- Overly broad conditions (“any authenticated user”)
- Missing contextual constraints
- Incorrect assumptions about ownership or relationships
- Silent privilege escalation through policy composition

Treat AI output like code written by a junior engineer: helpful, but requiring careful review.

---

## What AI must never do

- Approve or deny access at runtime
- Modify policies without human review
- Deploy changes automatically
- Grant exceptions or emergency access

Authorization decisions must remain deterministic, auditable, and externalized.

---

## Final reminder

Passing tests is necessary, but not sufficient. Always review policies for meaning, not just correctness.

If you are unsure whether a policy is safe, assume it is not.