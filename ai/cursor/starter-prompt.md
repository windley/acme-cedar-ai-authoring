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