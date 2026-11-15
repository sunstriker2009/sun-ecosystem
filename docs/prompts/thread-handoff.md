# Thread continuation prompt

Use this prompt in the old thread to prepare a handoff for a fresh thread in the same project. It creates a continuation brief; it does not manually compact or delete the original conversation.

## How to use

1. Copy the prompt below into the old thread.
2. Check the resulting brief for missing decisions, links, blockers, and paused work.
3. Paste the brief into a new thread in the same project.
4. Verify current repository, PR, workflow, and automation state before continuing. A handoff records prior authorization; it does not grant new permissions or resume paused work.

## Copyable prompt

```text
Prepare a self-contained continuation brief so I can continue this work in a fresh thread within the same project.

Preserve:
- The goal, scope, and current milestone.
- Approved decisions, constraints, preferences, and superseded decisions that must not be revived.
- Completed work, work in progress, blockers, and unresolved questions.
- Relevant repositories, branches, PR numbers, workflow names, file paths, and artifact links or IDs.
- The latest known validation results, clearly distinguishing verified facts from assumptions or stale information.
- Existing authorization, review requirements, and automation status, including anything paused.
- The next concrete action and a short ordered list of subsequent steps.

Remove repetition, abandoned approaches, lengthy logs, and conversational filler. Retain details needed to avoid repeating work or making incorrect decisions. Do not invent missing information or treat planned work as completed.

Use only information available to you and flag any important gaps. Do not perform development, change external systems, or resume paused work.

Return one copyable brief beginning:
“Continue from this handoff. Verify current external state before making changes.”

Aim for 800–1,200 words, using fewer if sufficient. End with the immediate next action.
```

## Keeping handoffs

Keep this reusable prompt in SUN Ecosystem. Save project-specific handoffs alongside that project's documentation when useful, rather than collecting implementation status here. Date saved handoffs so later readers can identify stale state. Omit credentials, tokens, and other secrets.
