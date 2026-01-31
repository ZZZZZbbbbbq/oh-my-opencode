# Oh My OpenCode 项目总结

## 🎯 项目核心定位

**Oh My OpenCode** 是一个强大的 OpenCode 插件，被称为"OpenCode 的 oh-my-zsh"。它实现了多模型 AI 代理编排系统，让 AI 编程助手像一个完整的开发团队一样工作。

**一句话概括**：一个电池全包（batteries-included）的 OpenCode 插件，提供多模型协同、并行后台代理和精心打造的 LSP/AST 工具。

## 📊 项目规模与技术栈

- **版本**: 3.0.0-beta.12
- **许可证**: SUL-1.0
- **包管理器**: Bun（独家使用）
- **开发语言**: TypeScript
- **构建方式**: ESM + 类型声明文件
- **测试框架**: Bun 原生测试（83个测试文件）
- **代码量级**: 
  - 主编排代理: 1383 行
  - 后台代理管理器: 1335 行
  - 总体架构: 31个生命周期钩子，20+个工具，10个专业化代理

## 🏗️ 核心架构

### 目录结构
```
oh-my-opencode/
├── src/
│   ├── agents/        # 10个AI代理（Sisyphus, oracle, librarian等）
│   ├── hooks/         # 31个生命周期钩子
│   ├── tools/         # 20+个工具（LSP, AST-Grep, 任务委派等）
│   ├── features/      # 后台代理、Claude Code兼容层
│   ├── shared/        # 50个跨模块工具函数
│   ├── cli/           # CLI安装器、健康检查工具
│   ├── mcp/           # 内置MCP服务器
│   └── config/        # Zod配置模式
├── packages/          # 7个平台特定的二进制文件
└── docs/              # 完整文档
```

## 🤖 核心代理系统

### 主力代理 - Sisyphus（西西弗斯）
- **模型**: Anthropic Claude Opus 4.5 High
- **定位**: 主编排代理，具有扩展思维能力
- **特点**: 像西西弗斯推石头一样，永不放弃直到任务完成
- **温度**: 0.1（代码生成极度精确）

### 专业化团队代理

| 代理名称 | 默认模型 | 专业领域 |
|---------|---------|---------|
| **Oracle（神谕）** | GPT-5.2 Medium | 只读咨询、高智商调试、架构设计 |
| **Librarian（图书管理员）** | GLM-4.7 Free | 多仓库分析、文档搜索、GitHub搜索 |
| **Explore（探索者）** | Grok Code | 快速代码库探索（上下文grep） |
| **Frontend UI/UX Engineer** | Gemini 3 Pro | 前端开发、UI/UX设计 |
| **Multimodal Looker** | Gemini 3 Flash | PDF/图像分析 |
| **Prometheus（普罗米修斯）** | Claude Opus 4.5 | 战略规划、面试模式 |
| **Metis（墨提斯）** | Claude Sonnet 4.5 | 计划前分析咨询 |
| **Momus（摩摩斯）** | Claude Sonnet 4.5 | 计划验证审查 |

## 🛠️ 核心功能特性

### 1. 多模型编排
- 根据任务类型自动选择最佳模型
- 并行运行多个代理，像真实开发团队一样协作
- 智能任务委派系统（delegate_task工具）

### 2. 强大的代码工具
- **LSP集成**: 完整的语言服务器协议支持
  - 代码重构（rename, extract）
  - 诊断信息获取
  - 符号跳转和定义查找
- **AST-Grep**: 基于抽象语法树的代码搜索和重构
- **会话工具**: 列表、读取、搜索和分析会话历史

### 3. 生产力增强功能
- **Ralph Loop**: 自动循环执行直到任务完成
- **Todo强制执行器**: 强制代理完成TODO列表
- **注释检查器**: 防止AI添加过多注释，保持代码简洁
- **Think模式**: 深度思考模式
- **Ultrawork关键词**: 只需输入"ultrawork"或"ulw"即可启动所有功能

### 4. Claude Code完全兼容
- 命令（Commands）
- 技能（Skills）
- 代理（Agents）
- MCP服务器
- 钩子系统（PreToolUse, PostToolUse, UserPromptSubmit, Stop）

### 5. 内置MCP服务器
- **websearch**: 基于Exa的网络搜索
- **context7**: 官方文档搜索
- **grep_app**: GitHub代码搜索

### 6. 内置技能（Skills）
- **playwright**: 浏览器自动化
- **git-master**: 原子化Git提交
- **frontend-ui-ux**: 前端开发增强

### 7. 后台代理系统
- 并行运行多个代理任务
- 智能通知批处理
- 任务生命周期管理
- 每个provider/model的并发限制配置

## 🎨 独特设计理念

### "永不放弃"哲学
项目以希腊神话中的西西弗斯命名，象征着AI代理会像西西弗斯推石头一样，永不放弃直到完成任务。这通过以下机制实现：
1. Todo强制执行器 - 强制继续未完成的任务
2. Ralph Loop - 自动循环直到成功
3. 后台代理系统 - 并行处理，提高效率

### 代码质量理念
- **温度控制**: 代码生成代理温度≤0.3，确保精确性
- **注释检查**: 自动清理过多注释，让AI生成的代码与人类代码无异
- **TDD强制**: 强制测试驱动开发（RED-GREEN-REFACTOR）

### 开发者体验优先
- "让AI帮你安装" - 把安装文档链接给AI，让它自己完成
- "Ultrawork关键词" - 一个词启动全部功能
- "电池全包" - 开箱即用，无需配置

## 📈 使用场景与效果

### 用户评价摘录
- "它让我取消了Cursor订阅。开源社区正在发生令人难以置信的事情。"
- "如果Claude Code 7天完成3个月的工作，Sisyphus 1小时就能完成。"
- "一天内用Oh My Opencode清理了8000个eslint警告"
- "一夜之间将45k行的Tauri应用转换为SaaS网页应用"

### 典型工作流程
1. Sisyphus派发后台任务给快速、便宜的模型并行探索代码库
2. 使用LSP进行确定性、安全的重构操作
3. 需要UI调整时，直接委派给Gemini 3 Pro前端专家
4. 遇到困难时，召唤GPT 5.2进行高智商战略支援
5. 处理复杂开源框架时，生成子代理实时消化源代码和文档
6. 代理被TODO列表约束，未完成则强制继续"推石头"

## 🔧 技术特色

### 配置系统
- **Zod验证**: 类型安全的配置模式
- **JSONC支持**: 支持注释和尾随逗号
- **多级配置**: 项目级（`.opencode/`）和用户级（`~/.config/opencode/`）
- **CLI doctor**: 配置验证和健康检查

### 三层MCP架构
1. **内置MCP**: websearch, context7, grep_app
2. **Claude Code兼容**: 支持`.mcp.json`文件和`${VAR}`变量扩展
3. **技能嵌入**: YAML前置配置的技能内嵌MCP服务器

### 持续集成/部署
- **GitHub Actions工作流**: 
  - `ci.yml`: 并行测试/类型检查 → 构建 → 自动提交模式 → 滚动`next`草稿发布
  - `publish.yml`: 手动workflow_dispatch → 版本提升 → 变更日志 → 8包OIDC npm发布
- **禁止本地发布**: 版本管理完全由CI控制

## 📚 文档与国际化

- **多语言README**: 英语、日语、简体中文、韩语
- **完整文档**:
  - 安装指南
  - 功能文档
  - 配置文档
  - CLI指南
  - Ultrawork宣言
  - 编排指南
  - 分类技能指南

## 🚀 快速开始

### 安装方式
**推荐**: 将以下内容粘贴给AI助手（Claude Code, AmpCode, Cursor等）：
```
Install and configure oh-my-opencode by following the instructions here:
https://raw.githubusercontent.com/code-yeongyu/oh-my-opencode/refs/heads/master/docs/guide/installation.md
```

### 魔法关键词
只需在提示词中包含 `ultrawork` 或 `ulw`，所有功能将自动启动：
- 并行代理
- 后台任务
- 深度探索
- 执行直到完成

## ⚠️ 重要注意事项

### Claude OAuth访问通知
- Anthropic于2026年1月限制了第三方OAuth访问
- 项目不包含任何自定义OAuth实现
- 技术上可以使用，但需注意ToS影响

### 兼容性要求
- OpenCode版本 >= 1.0.150
- 使用Bun作为包管理器（不支持npm/yarn）

## 💡 项目哲学

作者在个人开发中使用了价值$24,000的LLM tokens，试用了所有可用工具，最终选择了OpenCode。

**核心理念**:
- "如果OpenCode是Debian/Arch，Oh My OpenCode就是Ubuntu"
- "不要为选择代理框架而痛苦，我会做研究、借鉴最佳实践并在这里发布更新"
- "99%的项目是用OpenCode构建的，我只是测试功能"

## 📊 项目统计

- **GitHub Stars**: 持续增长中
- **npm下载量**: 持续增长中
- **贡献者**: 活跃的开源社区
- **使用公司**: Google、Microsoft、Indent等

## 🎯 项目定位总结

Oh My OpenCode不仅仅是一个插件，它是：
1. **框架**：提供完整的多模型AI代理编排系统
2. **工具集**：包含LSP、AST-Grep、会话管理等专业工具
3. **最佳实践**：集成作者$24,000实验的经验教训
4. **生态系统**：Claude Code完全兼容，支持社区扩展
5. **生产力倍增器**：通过智能编排让AI像团队一样工作

**适用人群**：
- 想要最大化AI编程助手效能的开发者
- 需要多模型协同的复杂项目
- 追求极致生产力的个人/团队
- OpenCode的深度用户

**核心价值**：
让AI代理不再是单打独斗的工具，而是成为一个完整的、专业化的、永不放弃的开发团队。
