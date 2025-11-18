# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

Claude Code plugin containing slash commands and skills. Install via `claude plugin marketplace add glittercowboy/taches-cc-resources`.

## Architecture

### Plugin Structure

```
.claude-plugin/
  plugin.json            # Plugin manifest
commands/
  *.md                   # Slash commands
skills/
  {skill-name}/
    SKILL.md             # Main skill file
    references/*.md      # Progressive disclosure content
    README.md            # User documentation
docs/
  *.md                   # Category documentation
```

### Slash Command Pattern

Location: `commands/*.md`

YAML frontmatter format:
```yaml
---
description: Brief description for command list
argument-hint: [what user provides]
allowed-tools: [tool restrictions if any]
---
```

Body uses pure XML structure with semantic tags: `<objective>`, `<process>`, `<success_criteria>`.

### Skill Pattern

Location: `skills/{skill-name}/`

Structure:
```
skills/{skill-name}/
  SKILL.md             # Main skill file
  references/*.md      # Progressive disclosure content
  README.md            # User documentation
```

SKILL.md format:
```yaml
---
name: skill-name-here        # Matches directory, verb-noun convention
description: What it does AND when to use it (third person, triggers)
---
```

Required XML tags in body: `<objective>`, `<quick_start>`, `<success_criteria>`

Conditional tags: `<context>`, `<workflow>`, `<advanced_features>`, `<validation>`, `<examples>`, `<anti_patterns>`, `<reference_guides>`

### Wrapper Command Pattern

Lightweight commands that just route to skills:

```yaml
---
description: Brief description
allowed-tools: Skill(skill-name)
argument-hint: [argument description]
---
```

Body contains: `<objective>`, `<process>`, `<success_criteria>` - routing only, expertise lives in skill.

## Canonical Reference Files

For skill authoring best practices, the authoritative content lives in:
- `skills/create-agent-skills/references/`
  - `core-principles.md` - XML structure, conciseness, degrees of freedom
  - `skill-structure.md` - Naming, YAML, progressive disclosure
  - `workflows-and-validation.md` - Complex workflows, feedback loops
  - `common-patterns.md` - Templates, examples, anti-patterns
  - `api-security.md` - Credential handling

## Writing Style

- Direct, no preamble
- Problem/Solution format with concrete scenarios
- Example Workflow sections with actual dialogue
- No philosophy sections or meta-commentary
- Video links at bottom of each README

## Key Relationships

- `create-meta-prompts` skill is the evolution of the `/create-prompt` command
- Both are kept for users who prefer simpler command-only approach vs full skill
