# Oh My OpenCode - Deployment and Usage Guide

> Complete guide for deploying and using Oh My OpenCode

## Table of Contents

- [Project Overview](#project-overview)
- [System Requirements](#system-requirements)
- [Quick Start](#quick-start)
- [Detailed Deployment Steps](#detailed-deployment-steps)
- [Usage Guide](#usage-guide)
- [FAQ](#faq)
- [Advanced Configuration](#advanced-configuration)

---

## Project Overview

**Oh My OpenCode** is a powerful OpenCode plugin that provides multi-model agent orchestration, parallel background task execution, LSP/AST tool integration, and enterprise-grade features.

### Core Features

- 🤖 **Multi-Agent Collaboration**: Sisyphus (main orchestrator), Oracle (architecture/debugging), Librarian (doc search), Explore (codebase exploration)
- ⚡ **Parallel Task Execution**: Run multiple agents simultaneously like a real dev team
- 🔧 **Complete Toolchain**: LSP support, AST-Grep, session management
- 🎯 **Claude Code Compatible**: Full hook system, commands, and skills support
- 📚 **Built-in MCPs**: Web search (Exa), official docs (Context7), GitHub search (Grep.app)

---

## System Requirements

### Required

- **OpenCode**: >= 1.0.150
- **Operating System**: macOS (ARM64/x64), Linux (x64/ARM64/Alpine), Windows (x64)
- **Package Manager**: Bun or npm/npx (Bun recommended)

### Subscription Requirements (Choose at least one)

Select at least one of the following subscription services:

1. **Claude Pro/Max** (Highly recommended - Best experience for Sisyphus agent)
2. **OpenAI/ChatGPT Plus** (Oracle agent uses GPT-5.2)
3. **Google AI** (Gemini 3 Pro - Frontend UI/UX agent)
4. **GitHub Copilot** (Fallback option)
5. **OpenCode Zen** (Access to opencode/ models)
6. **Z.ai Coding Plan** (GLM-4.7 models - Librarian agent)

**⚠️ Important**: Sisyphus agent strongly recommends Opus 4.5 model. Using other models may result in significantly degraded experience.

---

## Quick Start

### Fastest Installation (Recommended)

Copy and paste this into your LLM agent (Claude Code, AmpCode, Cursor, etc.):

```
Install and configure oh-my-opencode by following the instructions here:
https://raw.githubusercontent.com/code-yeongyu/oh-my-opencode/refs/heads/master/docs/guide/installation.md
```

Let the AI agent handle the installation for you - **Humans make mistakes, agents don't**.

### Manual Installation (Not Recommended)

If you insist on manual installation:

```bash
# Run the interactive installer
bunx oh-my-opencode install
# Or use npm
npx oh-my-opencode install
```

Follow the prompts to configure your subscriptions and authentication.

---

## Detailed Deployment Steps

### Step 1: Check OpenCode Installation

```bash
# Check if OpenCode is installed
opencode --version

# Should show 1.0.150 or higher
```

If not installed, visit [OpenCode Official Docs](https://opencode.ai/docs) for installation.

### Step 2: Determine Your Subscription Configuration

Choose installation options based on your subscriptions:

| Subscription Service | Installation Flag | Models Used |
|---------------------|------------------|-------------|
| Claude Pro/Max | `--claude=yes` or `--claude=max20` | Opus 4.5 (Sisyphus) |
| OpenAI/ChatGPT Plus | `--openai=yes` | GPT-5.2 (Oracle) |
| Google AI | `--gemini=yes` | Gemini 3 Pro (Frontend agent) |
| GitHub Copilot | `--copilot=yes` | Multi-model proxy access |
| OpenCode Zen | `--opencode-zen=yes` | opencode/ models |
| Z.ai Coding Plan | `--zai-coding-plan=yes` | GLM-4.7 (Librarian) |

### Step 3: Run the Installer

Run the appropriate command based on your subscriptions:

#### Example 1: All Native Subscriptions
```bash
bunx oh-my-opencode install --no-tui \
  --claude=max20 \
  --openai=yes \
  --gemini=yes \
  --copilot=no
```

#### Example 2: Claude Only
```bash
bunx oh-my-opencode install --no-tui \
  --claude=yes \
  --gemini=no \
  --copilot=no
```

#### Example 3: GitHub Copilot Only
```bash
bunx oh-my-opencode install --no-tui \
  --claude=no \
  --gemini=no \
  --copilot=yes
```

#### Example 4: OpenCode Zen
```bash
bunx oh-my-opencode install --no-tui \
  --claude=no \
  --gemini=no \
  --copilot=no \
  --opencode-zen=yes
```

The installer will automatically:
- Register the plugin in `opencode.json`
- Configure agent models based on subscription flags
- Show required authentication steps

### Step 4: Configure Authentication

Complete the following authentication steps based on your subscriptions:

#### 4.1 Anthropic (Claude) Authentication

```bash
opencode auth login
# Select Provider: Anthropic
# Select Login method: Claude Pro/Max
# Complete OAuth flow in browser
```

#### 4.2 Google Gemini Authentication

First, add the opencode-antigravity-auth plugin to your config:

Edit `~/.config/opencode/opencode.json`:
```json
{
  "plugin": [
    "oh-my-opencode",
    "opencode-antigravity-auth@1.2.8"
  ]
}
```

Then authenticate:
```bash
opencode auth login
# Select Provider: Google
# Select Login method: OAuth with Google (Antigravity)
# Complete sign-in in browser
```

**Multi-Account Load Balancing**: The plugin supports up to 10 Google accounts. When one account hits rate limits, it automatically switches to the next available account.

#### 4.3 GitHub Copilot Authentication

```bash
opencode auth login
# Select Provider: GitHub
# Authenticate via OAuth
```

### Step 5: Verify Installation

```bash
# Check OpenCode version
opencode --version

# Verify plugin is loaded
cat ~/.config/opencode/opencode.json | grep oh-my-opencode
# Should see "oh-my-opencode" in the plugin array

# Use health check tool (optional)
bunx oh-my-opencode doctor
```

---

## Usage Guide

### Basic Usage

Oh My OpenCode provides two main working modes:

### Mode 1: Ultrawork Mode (Quick Work)

**Use Cases**: Quick development, daily tasks, simple feature implementation

Simply include the **`ultrawork`** or **`ulw`** keyword in your prompt:

```
ulw add authentication to my Next.js app
```

The agent will automatically:
1. Explore your codebase to understand existing patterns
2. Research best practices via specialized agents
3. Implement the feature following your conventions
4. Verify with diagnostics and tests
5. Keep working until complete

**Example Prompts**:
```
ulw fix all ESLint warnings
ulw implement user registration and login
ulw optimize database query performance
ulw write unit tests covering the auth module
```

### Mode 2: Prometheus Mode (Precise Work)

**Use Cases**: Complex tasks, multi-day projects, critical production changes, work requiring detailed planning

Press **Tab** to switch to Prometheus (Planner) mode.

**Workflow**:

1. **Prometheus Interviews You**
   - Acts as your personal consultant, asking clarifying questions
   - Simultaneously researches your codebase to understand your needs
   
2. **Generate Work Plan**
   - Creates detailed work plan based on interview
   - Includes tasks, acceptance criteria, and guardrails
   - Optionally reviewed by Momus (plan reviewer) for high-accuracy validation
   
3. **Run `/start-work`**
   - Orchestrator-Sisyphus takes over execution
   - Distributes tasks to specialized sub-agents
   - Verifies each task completion independently
   - Accumulates learnings across tasks
   - Tracks progress across sessions (resume anytime)

**Correct Workflow**:
```
1. Press Tab → Enter Prometheus mode
2. Describe work → Prometheus interviews you
3. Confirm plan → Review .sisyphus/plans/*.md
4. Run /start-work → Orchestrator executes
```

**⚠️ Important**: Do NOT use `atlas` without `/start-work`. The orchestrator is designed to execute work plans created by Prometheus.

### Common Commands

```bash
# View all available commands
opencode help

# Run health check
bunx oh-my-opencode doctor

# View configuration
cat ~/.config/opencode/oh-my-opencode.json

# View project-level configuration
cat .opencode/oh-my-opencode.json
```

### Using Specialized Agents

The project includes multiple specialized agents, each with specific purposes:

| Agent | Default Model | Purpose |
|-------|--------------|---------|
| **Sisyphus** | Claude Opus 4.5 High | Main orchestrator with extended thinking |
| **Oracle** | GPT-5.2 Medium | Read-only consultation, high-IQ debugging |
| **Librarian** | GLM-4.7 Free | Multi-repo analysis, docs, GitHub search |
| **Explore** | Grok Code | Fast codebase exploration (contextual grep) |
| **Multimodal Looker** | Gemini 3 Flash | PDF/image analysis |
| **Prometheus** | Claude Opus 4.5 | Strategic planning, interview mode |

### Real-World Use Cases

#### Case 1: Feature Development
```
ulw implement payment feature
- Integrate Stripe API
- Add payment pages
- Handle success/failure callbacks
- Add tests
```

#### Case 2: Bug Fixing
```
ulw fix issue where user session is lost after login
```

#### Case 3: Code Refactoring
```
Press Tab to enter Prometheus mode
"I need to refactor the entire API layer, migrate from REST to GraphQL"
(Prometheus will interview you to understand detailed requirements)
After confirming the plan, run /start-work
```

#### Case 4: Code Review
```
ulw review the recent PR and provide improvement suggestions
```

---

## FAQ

### Q1: Can I use this without a Claude subscription?

**Answer**: Yes, but Sisyphus agent may not achieve optimal experience. You can:
- Use GitHub Copilot as a fallback
- Use OpenCode Zen models
- Use Z.ai Coding Plan

However, Claude Opus 4.5 is strongly recommended for the best experience.

### Q2: How do I switch the model used by an agent?

**Answer**: Edit the config file `~/.config/opencode/oh-my-opencode.json`:

```json
{
  "agents": {
    "sisyphus": {
      "model": "anthropic/claude-opus-4-5-high"
    },
    "oracle": {
      "model": "openai/gpt-5.2-medium"
    }
  }
}
```

### Q3: How do I disable an agent or feature?

**Answer**: Disable specific hooks in the config file:

```json
{
  "disabled_hooks": [
    "todo-enforcer",
    "comment-checker"
  ]
}
```

**⚠️ Warning**: Unless explicitly needed, don't change the default configuration. The plugin works best out of the box.

### Q4: Does it support multiple projects?

**Answer**: Yes! Configuration is two-tiered:
- **User-level**: `~/.config/opencode/oh-my-opencode.json` (global settings)
- **Project-level**: `.opencode/oh-my-opencode.json` (project-specific settings)

Project-level config overrides user-level config.

### Q5: How do I view agent work progress?

**Answer**: 
- In Prometheus mode, check the `.sisyphus/plans/` directory
- Use the `/status` command to view current status
- Background tasks show notifications in the terminal

### Q6: How do I debug issues?

**Answer**: 
1. Run health check: `bunx oh-my-opencode doctor`
2. Check logs: OpenCode shows detailed logs in the terminal
3. Verify config: Ensure JSON syntax is correct (JSONC comments supported)
4. Check [GitHub Issues](https://github.com/code-yeongyu/oh-my-opencode/issues)

### Q7: How do I uninstall?

**Answer**: 

```bash
# 1. Remove plugin from config
jq '.plugin = [.plugin[] | select(. != "oh-my-opencode")]' \
    ~/.config/opencode/opencode.json > /tmp/oc.json && \
    mv /tmp/oc.json ~/.config/opencode/opencode.json

# 2. Delete config files (optional)
rm -f ~/.config/opencode/oh-my-opencode.json
rm -f .opencode/oh-my-opencode.json

# 3. Verify
opencode --version
```

---

## Advanced Configuration

### Background Task Concurrency Control

Control concurrency limits per provider/model:

```json
{
  "background_task": {
    "concurrency": {
      "anthropic": 3,
      "openai": 2,
      "google": 2
    }
  }
}
```

### Category Task Delegation

Configure domain-specific task delegation:

```json
{
  "categories": {
    "visual": {
      "agent": "multimodal-looker",
      "triggers": ["ui", "design", "frontend", "css"]
    },
    "business-logic": {
      "agent": "oracle",
      "triggers": ["architecture", "algorithm", "optimization"]
    }
  }
}
```

### Custom LSP Configuration

```json
{
  "lsp": {
    "enabled": true,
    "languages": ["typescript", "javascript", "python", "go"]
  }
}
```

### Built-in Skills Configuration

```json
{
  "builtin_skills": {
    "playwright": { "enabled": true },
    "git-master": { 
      "enabled": true,
      "atomic_commits": true
    }
  }
}
```

### MCP Server Configuration

```json
{
  "mcps": {
    "websearch": { "enabled": true },
    "context7": { "enabled": true },
    "grep_app": { "enabled": true }
  }
}
```

---

## Best Practices

### 1. Use the Right Mode

- **Simple tasks**: Use `ulw` keyword
- **Complex tasks**: Use Prometheus mode (Tab key)
- **Code exploration**: Let Explore agent handle it
- **Architecture decisions**: Consult Oracle agent

### 2. Leverage Parallel Capabilities

Oh My OpenCode can run multiple agents simultaneously. When you include `ultrawork` in your prompt, the system automatically:
- Explores codebase in parallel
- Queries documentation in parallel
- Executes independent tasks in parallel

### 3. Keep Configuration Minimal

Unless you have specific needs, use the default configuration. The plugin is carefully tuned and works best out of the box.

### 4. Utilize Session Persistence

Work plans from Prometheus mode are saved in the `.sisyphus/plans/` directory. You can:
- Interrupt work at any time
- Resume later using `/start-work`
- Maintain progress across different sessions

### 5. Monitor Costs

Different models have different costs. Choose the right agent based on task complexity:
- Simple exploration: Explore (Grok Code - fast and cheap)
- Documentation queries: Librarian (GLM-4.7 - free)
- Complex tasks: Sisyphus (Opus 4.5 - most powerful but expensive)

---

## Performance Optimization Tips

1. **Context Management**: Let agents handle context management, don't worry about token limits
2. **Parallel Execution**: When using `ulw`, the system automatically parallelizes tasks
3. **Incremental Work**: In Prometheus mode, tasks are broken down into manageable chunks
4. **Cache Utilization**: Explore and Librarian cache query results

---

## Community & Support

- **Discord**: [Join Community](https://discord.gg/PUwSMR9XNk)
- **GitHub**: [Submit Issues](https://github.com/code-yeongyu/oh-my-opencode/issues)
- **Documentation**: [Full Docs](https://github.com/code-yeongyu/oh-my-opencode/tree/master/docs)
- **Contributing**: [CONTRIBUTING.md](https://github.com/code-yeongyu/oh-my-opencode/blob/master/CONTRIBUTING.md)

---

## Summary

Oh My OpenCode is a powerful OpenCode plugin that dramatically improves development efficiency through multi-agent collaboration and parallel task execution.

**Key Takeaways**:
- ✅ Use `ulw` keyword for quick tasks
- ✅ Use Prometheus mode for complex projects
- ✅ Claude Opus 4.5 model highly recommended
- ✅ Keep default configuration for best experience
- ✅ Leverage specialized agents for their respective strengths

Get started:
```bash
bunx oh-my-opencode install
```

Happy coding! 🚀

---

*Special thanks to [@junhoyeo](https://github.com/junhoyeo) for the amazing hero image.*
