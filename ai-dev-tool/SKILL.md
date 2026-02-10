---
name: ai-dev-tool
description: AI-powered development workflow with unified input handling and context management
---
# AI Dev Tool

A robust development tool that implements **no-mode-switching** input handling and context-aware progress tracking.

## Setup
1. Create required directories:
   ```bash
   mkdir -p /root/.openclaw/workspace/{project_doc,memory}
   ```
2. Create environment files:
   ```bash
   echo "# API Keys\nOPENAI_API_KEY=" > /root/.openclaw/workspace/.env.example
   cp /root/.openclaw/workspace/.env.example /root/.openclaw/workspace/.env
   ```
3. Create gitignore:
   ```bash
   echo "node_modules/\n.env\n*.log\nmemory/" > /root/.openclaw/workspace/.gitignore
   ```

## Core Components

### 🧠 Context Memory Handler
```bash
# Automatically manages context window limits
exec openclaw ai-dev-tool memory save --id my-project --step "UI Design"
exec openclaw ai-dev-tool memory load --id my-project
```

### 🖼️ Image Processing
```bash
# Auto-detects image input mode (no user selection)
exec openclaw ai-dev-tool process --image /path/to/screenshot.png --text "Optimize layout"
```

### 📝 Project Documentation
- All updates automatically logged in `project_doc/`
- Structured with timestamps and confidence levels
- Example: `project_doc/2026-02-10/step-001-UI-Analysis.md`

## Input Handling Workflow

### For Image + Text Input:
1. Vision Analyzer extracts UI elements
2. Confidence levels attached to all entities
3. Decomposer creates schema without UI assumptions
4. Final output: `project_doc/<timestamp>/schema.json`

### For Text-only Input:
1. Conceptual UI Parser generates assumed specifications
2. All elements marked with `{confidence: "assumed"}`
3. System Spec Architect validates against patterns

### Critical Rules Enforced:
- ⛔ No input mode selection UI
- ✅ Single unified input card
- 📊 Confidence levels for all extracted elements
- 🔒 Image always takes priority over text

## First Run
```bash
exec openclaw ai-dev-tool init --name "My-Project"
exec openclaw ai-dev-tool process \
  --image /root/.openclaw/workspace/samples/design.png \
  --text "Convert to responsive layout"
```

## Maintenance
- Auto-commit to GitHub every 15 minutes:
  ```bash
  openclaw cron add --job 'save' \
    --schedule '{"kind":"every","everyMs":900000}' \
    --payload '{"kind":"systemEvent","text":"exec openclaw ai-dev-tool memory save --id current"}'
  ```
- Verifiable project state at all times