---
name: how-i-ai-generate-a-living-html-design-system-with-ai-9d7d4002
description: Extract implemented UI tokens and components from code repositories into a portable HTML design system file to serve as human-readable documentation and visual context for future AI coding tasks.
---

# Living HTML Design System Generator

This skill extracts design tokens and component implementations from existing repositories and compiles them into a standalone, rendered `design_system.html` file. The resulting artifact serves as an interactive reference for human review and as visual context for subsequent agent-driven UI implementation.

Adapted from the *How I AI* episode with Anthropic engineer Thariq Shihipar demonstrating how portable HTML design systems provide compressed, inspectable visual context for models and humans without complex documentation build chains.

> *Note: This skill captures demonstrated workflows and suggested adaptations from the episode; it has not been independently execution-tested.*

---

## Workflow Overview

Instead of maintaining separate design docs or raw JSON token files that must be translated mentally, this process extracts the live design language directly from repository code (e.g., CSS, component files, or framework configs) into an executable HTML artifact:

1. **Extract implemented design DNA:** Scan repositories for tokens and core components, annotating their source files.
2. **Resolve inconsistencies:** Pause if marketing, application, or library repositories conflict on styles or typography.
3. **Compile `design_system.html`:** Render palettes, typography ladders, spacing grids, and component states in a self-contained HTML file.
4. **Add playground controls (optional):** Enable interactive adjustment of debated properties like spacing, radii, or density.
5. **Feed artifact into future prompts:** Pass `design_system.html` as explicit context to enforce consistency across new feature builds.

---

## Inputs and Prerequisites

- **Target Repositories:** Paths or links to one or more codebases containing the user interface (e.g., product apps, marketing sites, shared component libraries).
- **Source Access:** Use the current assistant with repository inspection tools or uploaded CSS, component files, and configuration. [Claude](https://claude.ai) and [GitHub Copilot](https://github.com/features/copilot) are examples from the tooling context, not required clients.
- **Browser:** Any local web browser to open and review the rendered `.html` file without a local web server.

---

## Step-by-Step Instructions

### Step 1: Extract Design Tokens and Components

Run an extraction prompt against the target codebases. The agent must cite the file path for each finding and halt on conflicting implementations rather than arbitrarily picking one.

**Extraction Prompt:**
```text
Analyze these repositories and extract the implemented design system. Identify colors, typography, spacing, radii, breakpoints, and core components. Cite the source file for each finding. If the repositories conflict, list the conflict and ask which source should win.

[Repository paths or links]
```

**Review Gate:**
Before proceeding, review any listed conflicts (for example, if marketing typography overrides app typography). Provide explicit authority rules defining which repository governs which layer.

### Step 2: Generate the Standalone `design_system.html`

Once the extraction analysis is verified, instruct the agent to build the self-contained HTML file.

**Generation Prompt:**
```text
Create a self-contained design_system.html from the approved analysis. Render the color, typography, spacing, radius, and breakpoint tokens. Show the core components in their common sizes and states, including hover, focus, disabled, loading, and error where applicable. Add the relevant source file path beside each section.
```

Ensure the output file satisfies these defaults:
- **Self-Contained:** Inline styles and lightweight scripts; requires no build tools or bundler to open.
- **Rendered Tokens:** Visible color swatches with labels, live typography specimens, spacing boxes, and border radius chips.
- **Non-Ideal States:** Component galleries rendering hover, focus, disabled, loading, and error states alongside defaults.
- **Source Paths:** Visible file annotations (e.g., `src/components/Button.tsx`) next to each element for code traceability.

### Step 3: Add Component Playground Controls

To help cross-functional stakeholders explore variations without touching source code, request interactive playground controls for common styling debates.

**Playground Prompt:**
```text
Add a component playground to design_system.html. Let me change spacing, radius, density, and supported variants with simple controls. Start from the real token values, show the current values, and include a reset button for every example.
```

### Step 4: Use as Context for Downstream Development

Save and, where authorized, commit `design_system.html` using available repository tools. If file writes are unavailable, return the complete HTML for saving; visual verification remains pending until it is opened in a browser. When prompting an agent to design or code a new feature, provide this file as visual and structural context.

**Context Prompt:**
```text
Use design_system.html as the visual and implementation reference for this feature. Reuse its tokens and component patterns. If the requested design conflicts with the file, identify the conflict before generating code.
```

---

## Failure Modes & Recovery

- **Conflicting Tokens Between Repositories:** If the model silently averages or picks random values when multi-repo differences exist, instruct it to create a explicit conflict table before generating HTML. Specify which codebase is authoritative (e.g., app repo for UI widgets, marketing repo for editorial type).
- **Ideal-State Bias:** If the generated artifact displays only static, pristine components, explicitly request interactive states (`hover`, `focus`, `disabled`, `error`, `loading`) and responsive variants.
- **Style Drift During Downstream Generation:** If generated code uses arbitrary values instead of tokens, pass both `design_system.html` and the specific production component files into the prompt, directing the model to report any off-token design choice.

---

## References and Source Links

- [Workflow: Generate a Living HTML Design System with AI for UI Consistency](https://www.chatprd.ai/how-i-ai/workflows/generate-a-living-html-design-system-with-ai-for-ui-consistency)
- [Article: Claude Code Anthropic - Thariq Shihipar on Replacing Markdown with HTML](https://www.chatprd.ai/how-i-ai/claude-code-anthropic-thariq-shihipar-on-replacing-markdown-with-html)
- [YouTube Clip: Thariq Demonstrating Living HTML Design System (25:10)](https://www.youtube.com/watch?v=Qrpm7E80wQ0&t=1510s)
- [YouTube: Full Episode](https://www.youtube.com/watch?v=Qrpm7E80wQ0)
- [Spotify: How I AI Podcast Episode](https://open.spotify.com/episode/6Wtk2CxwbHUwYGAe9HWgYT?si=Q9G6nIpsQQ-U25nNAwN8Mw)
- [Apple Podcasts: How I AI Podcast Episode](https://podcasts.apple.com/us/podcast/html-is-the-new-markdown-how-anthropic-engineers-are/id1809663079?i=1000768383813)
- [Claude](https://claude.ai)
- [GitHub Copilot](https://github.com/features/copilot)