# Oh My OpenCode 项目部署与使用总结

> 针对 @newtype-01/newtype-profile 的问题总结

## 快速总结

**Oh My OpenCode** 是一个强大的 OpenCode 插件，通过多智能体协作实现高效开发。

### 如何部署

#### 最简单的方式（强烈推荐）
将以下内容复制给 AI 智能体（Claude Code、Cursor 等）：
```
安装并配置 oh-my-opencode，请按照以下说明操作：
https://raw.githubusercontent.com/code-yeongyu/oh-my-opencode/refs/heads/master/docs/guide/installation.md
```

让 AI 帮你完成安装！

#### 手动安装
```bash
# 1. 确保已安装 OpenCode (>= 1.0.150)
opencode --version

# 2. 运行安装器
bunx oh-my-opencode install

# 3. 按照提示配置订阅（Claude/OpenAI/Gemini/GitHub Copilot等）

# 4. 完成认证
opencode auth login
```

### 如何使用

#### 方式 1: 快速模式（日常使用）
在提示中加入 `ultrawork` 或 `ulw` 关键词：
```
ulw 为我的 Next.js 应用添加身份认证
ulw 修复所有 ESLint 警告
ulw 实现支付功能
```

智能体会自动探索代码、查询文档、实现功能、验证结果，直到完成！

#### 方式 2: 精确模式（复杂任务）
1. 按 **Tab** 键进入 Prometheus（规划器）模式
2. 描述你的需求 - Prometheus 会面试你了解详细需求
3. 确认生成的工作计划
4. 运行 `/start-work` - Orchestrator 执行计划

适用于：多天项目、重大重构、关键生产变更

### 核心特性

- 🤖 **多智能体协作**: Sisyphus（主力）、Oracle（调试）、Librarian（文档）、Explore（探索）
- ⚡ **并行执行**: 同时运行多个智能体，像真实团队
- 🔧 **完整工具链**: LSP、AST-Grep、会话管理
- 📚 **内置搜索**: 网络搜索、官方文档、GitHub 代码搜索

### 系统要求

- **OpenCode**: >= 1.0.150
- **订阅**: 至少选择一个
  - Claude Pro/Max（强烈推荐 - 最佳体验）
  - OpenAI/ChatGPT Plus
  - Google AI (Gemini)
  - GitHub Copilot
  - OpenCode Zen
  - Z.ai Coding Plan

### 实际案例

```
# 案例 1: 功能开发
ulw 实现用户注册和登录功能，包括邮箱验证

# 案例 2: Bug 修复
ulw 修复用户登录后会话丢失的问题

# 案例 3: 代码重构
按 Tab → "将整个 API 层从 REST 迁移到 GraphQL" → 确认计划 → /start-work

# 案例 4: 批量修复
ulw 清理所有 ESLint 警告并优化代码
```

### 常见问题

**Q: 没有 Claude 订阅可以用吗？**  
A: 可以，但建议使用 Claude Opus 4.5 以获得最佳体验。也可使用 GitHub Copilot、OpenCode Zen 等。

**Q: 如何查看进度？**  
A: Prometheus 模式下查看 `.sisyphus/plans/` 目录，或使用 `/status` 命令。

**Q: 支持多项目吗？**  
A: 支持！配置分用户级（`~/.config/opencode/`）和项目级（`.opencode/`）。

### 完整文档

- 📚 **中文完整指南**: [docs/部署与使用指南.md](docs/部署与使用指南.md)
- 📚 **English Guide**: [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md)
- 📖 **安装指南**: [docs/guide/installation.md](docs/guide/installation.md)
- 📖 **功能文档**: [docs/features.md](docs/features.md)
- 📖 **配置文档**: [docs/configurations.md](docs/configurations.md)

### 最佳实践

1. ✅ 简单任务用 `ulw`
2. ✅ 复杂项目用 Prometheus 模式（Tab 键）
3. ✅ 使用 Claude Opus 4.5 获得最佳体验
4. ✅ 保持默认配置，开箱即用
5. ✅ 充分利用并行能力

### 社区支持

- **Discord**: https://discord.gg/PUwSMR9XNk
- **GitHub Issues**: https://github.com/code-yeongyu/oh-my-opencode/issues
- **文档**: https://github.com/code-yeongyu/oh-my-opencode/tree/master/docs

---

## 总结

Oh My OpenCode 让你的 AI 编程助手变成一个完整的开发团队：

- **部署**: 运行 `bunx oh-my-opencode install`，配置订阅，完成认证
- **使用**: 
  - 日常任务：加 `ulw` 关键词
  - 复杂项目：按 Tab 进入 Prometheus 模式
- **结果**: 多智能体并行工作，自动完成任务，直到成功

立即开始：
```bash
bunx oh-my-opencode install
```

🚀 让你的生产力翻倍！
