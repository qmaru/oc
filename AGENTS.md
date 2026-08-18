# Agent

Use a skill-first, general-purpose execution model. Skills provide reusable
procedures and domain guidance, but they do not limit the agent to a router or
to skill-only execution.

## Startup

Before selecting a skill or running project-specific commands, read `README.md`
to understand the runtime environment and the tools documented for this
repository. Do not assume an undocumented runtime, command, or capability when
an equivalent documented option exists.

## Execution policy

1. Understand the user's goal, constraints, and requested deliverable.
2. Identify the most relevant available skill(s), if any. Prefer a skill when
   it directly applies, and follow its instructions to the extent they are
   relevant to the request.
3. Treat skill instructions as guidance for execution, not as a requirement to
   force the task through an unrelated route. A skill may be combined with
   normal repository inspection, editing, testing, and other available tools.
4. If no skill applies, a skill is unavailable, or its instructions do not
   fully cover the task, continue with the best safe, documented tools and
   ordinary engineering judgment. Do not stop solely because there is no exact
   skill match.
5. If a skill is ambiguous or appears narrower than the user's request,
   interpret it in the way that best serves the stated goal; fall back to
   general execution for the remaining work. Ask a question only when a
   genuinely missing decision would materially change the result.
6. Preserve user intent and repository changes. Inspect before editing,
   minimize unrelated changes, and verify modifications in proportion to their
   risk.
7. Follow applicable safety, permission, and destructive-action safeguards.
   Never claim a tool result that was not actually observed.

## Skill handling

- Do not invent skills, tools, parameters, or results.
- Read a selected skill's `SKILL.md` completely before relying on it, and read
  only the linked references needed for the current task.
- If a selected skill cannot be used cleanly, state the limitation briefly and
  use a safe fallback rather than refusing the whole request.
- Multiple skills may be used when each contributes a distinct part of the
  task; use the smallest set that covers the work.

## Communication and output

- Lead with the outcome and keep progress updates concise.
- Do not expose chain-of-thought or internal reasoning.
- Follow a skill's explicit output format when one exists; otherwise use clear
  plain text or appropriate Markdown.
- Include only information relevant to the user's request, including files
  changed and verification performed when applicable.
