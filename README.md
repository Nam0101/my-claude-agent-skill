# My Claude Agent Skills

A collection of custom skills for Claude Code Agent to enhance AI-assisted development workflows.

## Overview

This repository contains reusable skills that extend Claude's capabilities for specific development tasks. Each skill provides structured workflows and best practices for common engineering scenarios.

## Skills

### 1. Codex-Claude Engineering Loop

**Location:** [`codex-claude-loop/SKILL.md`](codex-claude-loop/SKILL.md)

A dual-AI engineering workflow that combines Claude Code's planning and implementation capabilities with Codex's validation and review strengths.

**Key Features:**
- **Balanced AI collaboration**: Claude handles architecture, planning, and execution while Codex provides validation and code review
- **Continuous feedback loop**: Each AI reviews the other's work for optimal code quality
- **Structured phases**: Planning → Validation → Execution → Cross-Review → Iterative Improvement

**Workflow:**
```
Plan (Claude) → Validate Plan (Codex) → Feedback →
Implement (Claude) → Review Code (Codex) →
Fix Issues (Claude) → Re-validate (Codex) → Repeat until perfect
```

---

### 2. Figma to Jetpack Compose

**Location:** [`figma-to-compose/SKILL.md`](figma-to-compose/SKILL.md)

Automates the generation of Android Jetpack Compose UI code from Figma designs using MCP (Model Context Protocol) tools.

**Key Features:**
- **Automatic UI generation**: Converts Figma frames/components to idiomatic Jetpack Compose code (Material3)
- **Design token extraction**: Extracts colors, typography, spacing, and radius from Figma variables
- **Icon pipeline**: Automatically detects icon/vector nodes and converts them to Android VectorDrawable XML
- **Debug helpers**: Includes crash/ANR debugging utilities using ADB

**Required MCP Tools:**
- **Figma Desktop MCP**: `get_metadata`, `get_variable_defs`, `create_design_system_rules`, `get_design_context`, `get_screenshot`
- **Android MCP Toolkit**: `convert-svg-to-android-drawable`, `read-adb-logcat`, `fetch-crash-stacktrace`, `check-anr-state`

**Output Deliverables:**
- Screen composables with previews
- Reusable component files
- Theme files (Color.kt, Type.kt, Dimens.kt)
- VectorDrawable XML icons

## Usage

These skills are designed to be used with Claude Code Agent. To use a skill:

1. Reference the skill in your Claude Code configuration or conversation
2. Provide the required inputs as specified in each skill's documentation
3. Follow the structured workflow phases

## Contributing

Feel free to submit issues or pull requests to improve existing skills or add new ones.

## License

This project is available for personal and educational use.
