---
name: sync-coding-style
description: >-
  Update or check the coding-style skill against Franklin Yu's Wikipedia coding
  style page. Distill executable rules and preserve locally maintained agent
  guidance. Use for synchronization, not ordinary coding tasks.
---

# Sync coding style

Maintain `coding-style` as a concise execution-oriented version of the human
style guide. The wiki owns the style rules and their rationale; local agent
guidance has a separate, explicitly maintained source.

## Read the source and target

- Read the existing target and its applicable instructions. The default target
  is `~/.agents/skills/coding-style/SKILL.md`; honor a user-specified target.
  Resolve symlinks and check whether a dotfile manager owns the file before
  choosing which source to edit.
- Use the target's `upstream-url`, defaulting to
  [Franklin Yu's Coding styles](https://en.wikipedia.org/wiki/User:Franklin_Yu/Coding_styles).
  Retrieve the complete current revision, including its revision ID and edit
  date. Use a specific revision instead when the user requests one.
- Prefer wikitext or another complete representation that retains examples,
  links, and section structure. Search snippets alone are insufficient. If the
  full source cannot be retrieved, report the limitation without marking the
  target synchronized.
- Inspect existing local guidance before rewriting. When its origin is unclear,
  compare with the recorded upstream revision to distinguish source rules from
  local additions.

## Distill without changing policy

- Preserve every current rule, its strength, applicability, exceptions, numeric
  limits, overrides, and fallback order. Preserve language and shell-dialect
  distinctions. Recommendations remain recommendations.
- Put the decision first. Keep concise rationale and examples when they clarify
  a boundary or help apply the rule to an unlisted case. Do not optimize for a
  fixed word count at the expense of meaning.
- Leave historical narrative, extended debate, and supporting opinions in the
  upstream page. Link to the pinned revision and relevant sections for optional
  background. Do not require reading that background for ordinary coding work.
- Keep references to adopted standards and essential technical details. A
  citation offered as background does not become an additional instruction.
  Distinguish other authors' positions from the user's final decision.
- Retain the source language and useful organization. Reuse existing distilled
  wording when the underlying rule has not changed. Flag ambiguity that could
  change behavior instead of silently choosing a new policy.

## Preserve agent guidance

Keep locally maintained agent guidance separate from wiki-derived rules, using
its existing section or referenced file. Preserve its contents and links during
synchronization. If local additions are mixed into the old text, identify and
retain them explicitly; surface uncertain cases for review.

Do not generate new guardrails from the wiki's rationale or silently migrate
instructions from `AGENTS.md` or other agent configuration. Add or revise local
guidance when the user requests that change, and identify it as a local edit.
When there is no local supplement, no empty section is needed. Surface conflicts
with upstream rules rather than silently overwriting either source.

## Check and deliver

- Compare the result with the complete source for omitted rules and changed
  conditions. Check that local guidance is preserved, frontmatter is valid,
  and any local reference links resolve. Use an available skill validator.
- Maintain the existing provenance fields: `upstream-title`, `upstream-url`,
  `upstream-revision`, `upstream-revision-url`, `upstream-edited-on`, and
  `synced-on`. Record the revision actually read and the synchronization date;
  preserve unrelated metadata and skill discovery settings.
- Follow the requested mode: produce a separate candidate for a draft or review
  request; update the intended target for a synchronization request. The wiki
  remains source material for this workflow.
- Present the source revision, output location, validation results, and a diff
  against the existing target. Distinguish upstream rule changes, editorial
  condensation, and requested local edits. Call out unresolved semantic changes
  so the user can review them directly.
