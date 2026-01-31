# Oh My OpenCode Project Summary

## 🎯 Core Position

**Oh My OpenCode** is a powerful OpenCode plugin, dubbed "oh-my-zsh for OpenCode". It implements a multi-model AI agent orchestration system that makes AI coding assistants work like a complete development team.

**One-liner**: A batteries-included OpenCode plugin providing multi-model orchestration, parallel background agents, and crafted LSP/AST tools.

## 📊 Project Scale & Tech Stack

- **Version**: 3.0.0-beta.12
- **License**: SUL-1.0
- **Package Manager**: Bun (exclusive)
- **Language**: TypeScript
- **Build**: ESM + type declarations
- **Testing**: Bun native tests (83 test files)
- **Code Scale**: 
  - Main orchestrator agent: 1383 lines
  - Background agent manager: 1335 lines
  - Overall: 31 lifecycle hooks, 20+ tools, 10 specialized agents

## 🏗️ Core Architecture

### Directory Structure
```
oh-my-opencode/
├── src/
│   ├── agents/        # 10 AI agents (Sisyphus, oracle, librarian, etc.)
│   ├── hooks/         # 31 lifecycle hooks
│   ├── tools/         # 20+ tools (LSP, AST-Grep, task delegation, etc.)
│   ├── features/      # Background agents, Claude Code compat layer
│   ├── shared/        # 50 cross-cutting utilities
│   ├── cli/           # CLI installer, health checks
│   ├── mcp/           # Built-in MCP servers
│   └── config/        # Zod configuration schema
├── packages/          # 7 platform-specific binaries
└── docs/              # Complete documentation
```

## 🤖 Core Agent System

### Main Agent - Sisyphus
- **Model**: Anthropic Claude Opus 4.5 High
- **Role**: Main orchestrator with extended thinking capabilities
- **Philosophy**: Like Sisyphus rolling the boulder, never gives up until task completion
- **Temperature**: 0.1 (extremely precise code generation)

### Specialized Team Agents

| Agent Name | Default Model | Specialization |
|-----------|---------------|----------------|
| **Oracle** | GPT-5.2 Medium | Read-only consultation, high-IQ debugging, architecture design |
| **Librarian** | GLM-4.7 Free | Multi-repo analysis, docs search, GitHub search |
| **Explore** | Grok Code | Fast codebase exploration (contextual grep) |
| **Frontend UI/UX Engineer** | Gemini 3 Pro | Frontend development, UI/UX design |
| **Multimodal Looker** | Gemini 3 Flash | PDF/image analysis |
| **Prometheus** | Claude Opus 4.5 | Strategic planning, interview mode |
| **Metis** | Claude Sonnet 4.5 | Pre-planning analysis |
| **Momus** | Claude Sonnet 4.5 | Plan validation review |

## 🛠️ Core Features

### 1. Multi-Model Orchestration
- Automatically selects best model for task type
- Runs multiple agents in parallel like a real dev team
- Intelligent task delegation system (delegate_task tool)

### 2. Powerful Code Tools
- **LSP Integration**: Full Language Server Protocol support
  - Code refactoring (rename, extract)
  - Diagnostics retrieval
  - Symbol navigation and definition lookup
- **AST-Grep**: Abstract Syntax Tree-based code search and refactoring
- **Session Tools**: List, read, search, and analyze session history

### 3. Productivity Enhancements
- **Ralph Loop**: Auto-loop until task completion
- **Todo Enforcer**: Forces agent to complete TODO lists
- **Comment Checker**: Prevents excessive AI comments, keeps code clean
- **Think Mode**: Deep thinking mode
- **Ultrawork Keyword**: Just type "ultrawork" or "ulw" to activate all features

### 4. Full Claude Code Compatibility
- Commands
- Skills
- Agents
- MCP servers
- Hook system (PreToolUse, PostToolUse, UserPromptSubmit, Stop)

### 5. Built-in MCP Servers
- **websearch**: Exa-based web search
- **context7**: Official documentation search
- **grep_app**: GitHub code search

### 6. Built-in Skills
- **playwright**: Browser automation
- **git-master**: Atomic git commits
- **frontend-ui-ux**: Frontend development enhancement

### 7. Background Agent System
- Run multiple agent tasks in parallel
- Intelligent notification batching
- Task lifecycle management
- Concurrency limits per provider/model

## 🎨 Unique Design Philosophy

### "Never Give Up" Philosophy
Named after Greek mythology's Sisyphus, symbolizing that AI agents will never give up until task completion. Achieved through:
1. Todo Enforcer - Forces continuation of incomplete tasks
2. Ralph Loop - Auto-loops until success
3. Background agent system - Parallel processing for efficiency

### Code Quality Philosophy
- **Temperature Control**: Code generation agents ≤0.3 for precision
- **Comment Checking**: Auto-cleans excessive comments to make AI code indistinguishable from human code
- **TDD Enforcement**: Mandatory Test-Driven Development (RED-GREEN-REFACTOR)

### Developer Experience First
- "Let AI install it" - Give installation doc link to AI, let it handle setup
- "Ultrawork keyword" - One word activates all features
- "Batteries included" - Works out of the box, no config needed

## 📈 Use Cases & Impact

### User Testimonials Excerpts
- "It made me cancel my Cursor subscription. Unbelievable things are happening in the open source community."
- "If Claude Code does in 7 days what a human does in 3 months, Sisyphus does it in 1 hour."
- "Knocked out 8000 eslint warnings with Oh My Opencode, just in a day"
- "Converted a 45k line Tauri app into a SaaS web app overnight"

### Typical Workflow
1. Sisyphus dispatches background tasks to fast, cheap models to explore codebase in parallel
2. Uses LSP for deterministic, safe refactoring operations
3. Delegates frontend tasks directly to Gemini 3 Pro when UI adjustments needed
4. Summons GPT 5.2 for high-IQ strategic support when stuck
5. Spawns subagents to digest source code and docs in real-time for complex frameworks
6. Agent is bound by TODO list; forced to continue "bouldering" if incomplete

## 🔧 Technical Highlights

### Configuration System
- **Zod validation**: Type-safe configuration schema
- **JSONC support**: Comments and trailing commas supported
- **Multi-level config**: Project-level (`.opencode/`) and user-level (`~/.config/opencode/`)
- **CLI doctor**: Configuration validation and health checks

### Three-Tier MCP Architecture
1. **Built-in MCPs**: websearch, context7, grep_app
2. **Claude Code compatible**: Supports `.mcp.json` files with `${VAR}` expansion
3. **Skill-embedded**: MCP servers embedded in skills via YAML frontmatter

### CI/CD
- **GitHub Actions workflows**: 
  - `ci.yml`: Parallel test/typecheck → build → auto-commit schema → rolling `next` draft release
  - `publish.yml`: Manual workflow_dispatch → version bump → changelog → 8-package OIDC npm publish
- **No local publishing**: Version management fully controlled by CI

## 📚 Documentation & i18n

- **Multi-language READMEs**: English, Japanese, Simplified Chinese, Korean
- **Complete docs**:
  - Installation guide
  - Features documentation
  - Configuration documentation
  - CLI guide
  - Ultrawork manifesto
  - Orchestration guide
  - Category skill guide

## 🚀 Quick Start

### Installation
**Recommended**: Paste this to your AI assistant (Claude Code, AmpCode, Cursor, etc.):
```
Install and configure oh-my-opencode by following the instructions here:
https://raw.githubusercontent.com/code-yeongyu/oh-my-opencode/refs/heads/master/docs/guide/installation.md
```

### Magic Keywords
Just include `ultrawork` or `ulw` in your prompt, and all features activate automatically:
- Parallel agents
- Background tasks
- Deep exploration
- Execution until completion

## ⚠️ Important Notes

### Claude OAuth Access Notice
- Anthropic restricted third-party OAuth access as of January 2026
- Project contains no custom OAuth implementations
- Technically usable but be aware of ToS implications

### Compatibility Requirements
- OpenCode version >= 1.0.150
- Use Bun as package manager (npm/yarn not supported)

## 💡 Project Philosophy

Author spent $24,000 worth of LLM tokens in personal development, tried every available tool, and chose OpenCode.

**Core Principles**:
- "If OpenCode is Debian/Arch, Oh My OpenCode is Ubuntu"
- "Don't agonize over agent harness choices, I'll do the research and ship updates here"
- "99% of the project was built using OpenCode, I just test functionality"

## 📊 Project Statistics

- **GitHub Stars**: Growing continuously
- **npm Downloads**: Growing continuously
- **Contributors**: Active open-source community
- **Used by**: Google, Microsoft, Indent, and more

## 🎯 Project Positioning Summary

Oh My OpenCode is more than just a plugin, it's:
1. **Framework**: Complete multi-model AI agent orchestration system
2. **Toolset**: Professional tools including LSP, AST-Grep, session management
3. **Best Practices**: Integrates lessons from author's $24,000 experiments
4. **Ecosystem**: Full Claude Code compatibility, supports community extensions
5. **Productivity Multiplier**: Makes AI work like a team through intelligent orchestration

**Target Audience**:
- Developers wanting to maximize AI coding assistant effectiveness
- Complex projects requiring multi-model collaboration
- Individuals/teams pursuing extreme productivity
- Power users of OpenCode

**Core Value**:
Transform AI agents from solo tools into a complete, specialized, never-give-up development team.
