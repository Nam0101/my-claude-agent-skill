---
name: ai-pair-programming
description: Orchestrates a dual-AI engineering loop where a Primary AI plans and implements, while a Review AI validates and reviews, with continuous feedback for optimal code quality. Supports custom AI pairing (Claude, Codex, Gemini, etc.)
---

# AI Pair Programming Skill

## Overview
A flexible pair programming workflow that allows you to combine any two AI assistants for collaborative development. Configure your preferred AI pair based on their strengths.

## AI Configuration

Before using this skill, configure your AI pair by setting the following roles:

| Role | Description | Examples |
|------|-------------|----------|
| **Primary AI** | Handles architecture, planning, and code implementation | Claude, Gemini, GPT-4 |
| **Review AI** | Validates plans and reviews code for quality assurance | Codex, Claude, Gemini |

### Example Configurations

| Configuration | Primary AI | Review AI | Use Case |
|---------------|------------|-----------|----------|
| Claude + Codex | Claude | Codex | Strong planning + Fast validation |
| Claude + Gemini | Claude | Gemini | Multi-model perspective |
| Gemini + Claude | Gemini | Claude | Leverage Gemini's context + Claude's review |
| GPT-4 + Codex | GPT-4 | Codex | GPT planning + Codex validation |

### Setting Up Your AI Pair

Replace `{{PRIMARY_AI}}` and `{{REVIEW_AI}}` placeholders throughout this skill with your chosen AI names.

**Example:**
- `{{PRIMARY_AI}}` → `Claude`
- `{{REVIEW_AI}}` → `Codex`

For command-line tools, replace `{{REVIEW_AI_CLI}}` with the appropriate CLI command:
- Codex: `codex exec --sandbox read-only`
- Claude: `claude --print`
- Gemini: `gemini`
- Other: Use your AI's CLI tool

> **Note:** CLI commands are examples. Please verify the correct CLI syntax for your specific AI tools and their current versions.

## Core Workflow Philosophy
This skill implements a balanced engineering loop:
- **{{PRIMARY_AI}}**: Architecture, planning, and execution
- **{{REVIEW_AI}}**: Validation and code review
- **Continuous Review**: Each AI reviews the other's work
- **Context Handoff**: Always continue with whoever last cleaned up

> **Note:** Model + reasoning settings are assumed to be handled by each AI's existing config. Commands below use generic placeholders.

## Phase 1: Planning with {{PRIMARY_AI}}
1. Start by creating a detailed plan for the task
2. Break down the implementation into clear steps
3. Document assumptions and potential issues
4. Output the plan in a structured format

## Phase 2: Plan Validation with {{REVIEW_AI}}
1. Send the plan to {{REVIEW_AI}} for validation:
```bash
echo "Review this implementation plan and identify any issues:
[{{PRIMARY_AI}}'s plan here]

Check for:
- Logic errors
- Missing edge cases
- Architecture flaws
- Security concerns" | {{REVIEW_AI_CLI}}
```
2. Capture {{REVIEW_AI}}'s feedback

## Phase 3: Feedback Loop
If {{REVIEW_AI}} finds issues:
1. Summarize {{REVIEW_AI}}'s concerns to the user
2. Refine the plan based on feedback
3. Ask user (via `AskUserQuestion`): "Should I revise the plan and re-validate, or proceed with fixes?"
4. Repeat Phase 2 if needed

## Phase 4: Execution
Once the plan is validated:
1. {{PRIMARY_AI}} implements the code using available tools (Edit, Write, Read, etc.)
2. Break down implementation into manageable steps
3. Execute each step carefully with proper error handling
4. Document what was implemented

## Phase 5: Cross-Review After Changes
After every change:
1. Send {{PRIMARY_AI}}'s implementation to {{REVIEW_AI}} for review:
   - Bug detection
   - Performance issues
   - Best practices validation
   - Security vulnerabilities
2. {{PRIMARY_AI}} analyzes {{REVIEW_AI}}'s feedback and decides:
   - Apply fixes immediately if issues are critical
   - Discuss with user if architectural changes needed
   - Document decisions made

## Phase 6: Iterative Improvement
1. After {{REVIEW_AI}} review, {{PRIMARY_AI}} applies necessary fixes
2. For significant changes, send back to {{REVIEW_AI}} for re-validation
3. Continue the loop until code quality standards are met
4. For AI tools that support session continuation, use the resume flag:
```bash
echo "Review the updated implementation" | {{REVIEW_AI_CLI}} --resume
```
**Note:** Session resumption support varies by AI tool. For tools without resume support, start a new session with full context.

## Recovery When Issues Are Found
When {{REVIEW_AI}} identifies problems:
1. {{PRIMARY_AI}} analyzes the root cause
2. Implements fixes using available tools
3. Sends updated code back to {{REVIEW_AI}} for verification
4. Repeats until validation passes

When implementation errors occur:
1. {{PRIMARY_AI}} reviews the error/issue
2. Adjusts implementation strategy
3. Re-validates with {{REVIEW_AI}} before proceeding

## Best Practices
- **Always validate plans** before execution
- **Never skip cross-review** after changes
- **Maintain clear handoff** between AIs
- **Document who did what** for context
- **Use resume** to preserve session state (check your AI tool's documentation for support)

## Command Reference
| Phase | Command Pattern | Purpose |
|------:|------------------|---------|
| Validate plan | `echo "plan" \| {{REVIEW_AI_CLI}}` | Check logic before coding |
| Implement | {{PRIMARY_AI}} uses Edit/Write/Read tools | {{PRIMARY_AI}} implements the validated plan |
| Review code | `echo "review changes" \| {{REVIEW_AI_CLI}}` | {{REVIEW_AI}} validates {{PRIMARY_AI}}'s implementation |
| Continue review | `echo "next step" \| {{REVIEW_AI_CLI}} --resume` | Continue validation session (if supported) |
| Apply fixes | {{PRIMARY_AI}} uses Edit/Write tools | {{PRIMARY_AI}} fixes issues found by {{REVIEW_AI}} |
| Re-validate | `echo "verify fixes" \| {{REVIEW_AI_CLI}}` | {{REVIEW_AI}} re-checks after fixes |

> **Note:** The `--resume` flag is supported by some AI tools (e.g., Codex). For tools without resume support, start a new session with the necessary context.

## Error Handling
1. Stop on non-zero exit codes from {{REVIEW_AI}}
2. Summarize {{REVIEW_AI}} feedback and ask for direction via `AskUserQuestion`
3. Before implementing changes, confirm approach with user if:
   - Significant architectural changes needed
   - Multiple files will be affected
   - Breaking changes are required
4. When {{REVIEW_AI}} warnings appear, {{PRIMARY_AI}} evaluates severity and decides next steps

## The Perfect Loop
```
Plan ({{PRIMARY_AI}}) → Validate Plan ({{REVIEW_AI}}) → Feedback →
Implement ({{PRIMARY_AI}}) → Review Code ({{REVIEW_AI}}) →
Fix Issues ({{PRIMARY_AI}}) → Re-validate ({{REVIEW_AI}}) → Repeat until perfect
```

This creates a self-correcting, high-quality engineering system where:
- **{{PRIMARY_AI}}** handles all code implementation and modifications
- **{{REVIEW_AI}}** provides validation, review, and quality assurance

---

## Quick Start Examples

### Example 1: Claude + Codex (Original Configuration)
```
PRIMARY_AI = Claude
REVIEW_AI = Codex
REVIEW_AI_CLI = codex exec --sandbox read-only
```

### Example 2: Claude + Gemini
```
PRIMARY_AI = Claude
REVIEW_AI = Gemini
REVIEW_AI_CLI = gemini
```

### Example 3: Gemini + Claude
```
PRIMARY_AI = Gemini
REVIEW_AI = Claude
REVIEW_AI_CLI = claude --print
```
