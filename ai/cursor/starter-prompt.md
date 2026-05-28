# Starter Prompt for AI-Assisted Cedar Policy Authoring

Use this prompt when working with Cursor (or a similar AI-assisted editor) to draft, review, or refactor Cedar policies in this repository.

Always include the relevant files as context before starting.

---

## Base prompt

You are assisting with authoring Cedar authorization policies.

Use the following files as the source of truth:
- `cedar/acme.cedarschema`
- All files under `cedar/policies/`
- `cedar/acme-entities.json` when examples are needed

Constraints:
- Do not invent new entities, actions, or attributes.
- Use names exactly as defined in the schema.
- Treat policies as policy-as-code, not prose.
- Prefer least-privilege outcomes by default.
- AI output is advisory and will be reviewed by a human.

Before drafting, modifying, or reviewing Cedar policies, verify against the schema:
- Read `cedar/acme.cedarschema` (or `cedar/acme.cedarschema.json`) first.
- Every `principal is`, `resource is`, and `action ==` (or `action in`) in the policy must use entity types and action names defined in the schema.
- Every attribute or context field in `when` / `unless` clauses (for example, `resource.classification`, `context.device.managed`, `resource.customer_readers_team`) must exist on that type in the schema.
- Do not reference relationships or team membership unless the schema and entity model support them (for example, group membership via entity parents and attributes such as `customer_readers_team`).

Before evaluating, explaining, or authoring example requests, verify against the schema and entity store:
- Confirm every principal type, action, resource type, attribute, and context field matches the schema.
- Cross-check principal and resource IDs against `cedar/acme-entities.json`; do not assume an entity exists or has a given type unless it appears in that file.
- Use fully qualified Cedar references in examples (for example, `ACME::Customer::"kate"`, `ACME::Action::"doc:view"`, `ACME::Document::"q3-plan"`). Do not use shorthand types such as `User` or unqualified `Document` unless the schema defines them.
- Match action names to the schema exactly (for example, `doc:view`, not `view`).
- Include a `context` object on requests when the schema defines context; use only fields declared in the schema.

If policy code, a request, a test, or an explanation uses types or names that do not appear in the schema or entities file, call that out explicitly rather than inferring a match.

When proposing a policy or change, always provide:
1. The Cedar policy code
2. A short plain-language explanation of intent
3. At least three example requests with expected Permit or Deny outcomes
4. Any edge cases or risks the policy might introduce

If anything is ambiguous, make the smallest safe assumption and explain it.

---

## Example follow-up prompts

- “Draft the smallest policy change that allows this behavior.”
- “Explain what access this policy grants in plain language.”
- “What unintended access might this policy allow?”
- “Generate deny cases that test the boundaries of this policy.”
- “Refactor this policy for clarity without changing behavior.”

Never assume policies are correct simply because they are syntactically valid or tests pass.