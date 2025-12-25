# My Claude Agent Skills

A collection of custom skills for Claude AI agents that enhance development workflows and automate complex tasks.

## Skills

### 1. Codex-Claude Engineering Loop

**Directory:** `codex-claude-loop/`

A dual-AI engineering loop that orchestrates Claude Code and Codex to work together for optimal code quality.

#### How It Works

```
Plan (Claude) → Validate Plan (Codex) → Feedback →
Implement (Claude) → Review Code (Codex) →
Fix Issues (Claude) → Re-validate (Codex) → Repeat until perfect
```

#### Key Features

- **Claude Code**: Handles architecture, planning, and code implementation
- **Codex**: Provides validation, code review, and quality assurance
- **Continuous Review**: Each AI reviews the other's work
- **Context Handoff**: Maintains context between AI systems

#### Workflow Phases

1. **Planning**: Claude creates a detailed implementation plan
2. **Plan Validation**: Codex reviews the plan for issues
3. **Feedback Loop**: Iterative refinement based on Codex feedback
4. **Execution**: Claude implements the validated plan
5. **Cross-Review**: Codex reviews the implementation
6. **Iterative Improvement**: Continue until quality standards are met

---

### 2. Figma to Jetpack Compose

**Directory:** `figma-to-compose/`

Automatically converts Figma designs to Android Jetpack Compose UI code using MCP (Model Context Protocol) tools.

#### Key Features

- **Design System Extraction**: Extracts colors, typography, spacing, and radius from Figma variables
- **Auto Icon Pipeline**: Automatically detects icons and converts them to Android VectorDrawable XML
- **Material3 Support**: Generates idiomatic Jetpack Compose code with Material3 theming
- **Visual Validation**: Uses screenshots for layout verification

#### Tools Used

**Figma Desktop MCP:**
- `get_design_context` - Get layout/component context
- `get_screenshot` - Capture design screenshots
- `get_variable_defs` - Extract design tokens
- `get_metadata` - Get node information
- `create_design_system_rules` - Generate mapping rules
- `get_figjam` - Get FigJam content

**Android MCP Toolkit:**
- `convert-svg-to-android-drawable` - Convert SVG to VectorDrawable XML
- `read-adb-logcat` - Debug crash logs
- `get-pid-by-package` - Get process ID by package name
- `get-current-activity` - Get current activity information
- `fetch-crash-stacktrace` - Get crash information
- `check-anr-state` - Detect ANR issues
- `clear-logcat-buffer` - Clear logcat buffer
- `estimate-text-length-difference` - Estimate text length differences

#### Output Structure

```
ui/
├── screen/
│   ├── <ScreenName>Screen.kt
│   └── <ScreenName>Components.kt
└── theme/
    ├── Color.kt
    ├── Type.kt
    └── Dimens.kt
res/
└── drawable/
    └── ic_<name>.xml
```

## Usage

These skills are designed to be used with Claude AI agents. Each skill contains a `SKILL.md` file with detailed instructions on how the agent should behave when the skill is activated.

### Example Triggers

**Codex-Claude Loop:**
- Tasks requiring high-quality code with validation
- Complex implementations needing review cycles

**Figma to Compose:**
- "Implement this screen from Figma using Jetpack Compose: `<figma link>`"
- "Build this component set (Button variants) from Figma"
- "Create UI from Figma and auto-generate VectorDrawables for icons"

## License

This project is open source. Feel free to use and modify these skills for your own Claude agents.
