# Prompt Optimizer For Engineer

## Project Plan (v1.0) — 2026-02-10

### 🎯 **Vision**
Create an AI-powered tool that optimizes engineering prompts while strictly adhering to *no-mode-switching* inputs and *confidence-aware* context management.

---

### 🗓️ **Phases & Timeline**

| Phase | Duration | Deliverables | Confidence |
|-------|----------|--------------|------------|
| **1. Architecture** | 3 days | - Unified input schema<br>- Context memory handler | high |
| **2. Core Development** | 7 days | - Vision Analyzer<br>- UI Decomposer<br>- Spec Architect | assumed |
| **3. Validation** | 2 days | - Schema Validator<br>- UX Gap Analyzer | moderate |
| **4. Deployment** | 1 day | - Auto-commit + Vercel integration | high |

---

### ⚙️ **Technical Implementation**

#### **Context Management**
- Memory files: `/memory/` with automatic rotation
- Project state snapshots in `project_doc/` (e.g., `step-001-Architecture.md`)

#### **Input Handling Workflow**
```mermaid
graph TD
    A[Single Input Card] -->|Image| B(Vision Analyzer)
    A -->|Text| C(Conceptual Parser)
    B --> D{Confidence > 90%?}
    C --> E{Mark as "assumed"}
    D -->|Yes| F[UI Decomposer]
    E --> F
    F --> G[System Spec Architect]
```

#### **AI Contract Requirements**
- ✅ No input mode references in UI
- ✅ All outputs include confidence levels:
  ```json
  {"element": "Search Button", "confidence": "high"}
  ```
- ✅ Image always overrides text (e.g., if screenshot shows 5 icons but text says 4)

---

### 📌 **Immediate Next Steps**
1. Implement Vision Analyzer (priority: high)
2. Validate schema structure against [input handling rules](https://github.com/alamakmak/Prompt-Optimizer-For-Engineer/blob/main/ai-dev-tool/SKILL.md#input-handling-workflow)
3. Set up Vercel deployment pipeline

> ⚠️ **Note**: This plan evolves automatically via the `ai-dev-tool` as new inputs arrive. Current confidence level: 95% (derived from init.json + SKILL.md constraints).