---
title: "第 6 课 - 使用 Playwright MCP 验证功能"
description: "在 Copilot CLI 中检查或配置 Playwright MCP，并使用它在浏览器中体验筛选功能。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

正如前面所说，编写代码不只是写代码。我们还要处理数据、外部服务，并让 Copilot 使用更多自动化工具。这正是 MCP 服务器的作用。MCP 服务器让 Copilot 能够使用 CLI 内置功能以外的工具和服务。

在本课中，你将：

- 了解模型上下文协议（MCP）以及 Copilot CLI 如何使用它。
- 在尚未配置时添加 Playwright MCP 服务器。
- 让智能体操作浏览器并体验筛选功能。

## 场景

单元测试和端到端测试很重要，但要验证 UI 更新，还需要实际与 UI 交互。你希望 Copilot 能像用户一样使用正在开发的网站，从而自动验证更改是否符合预期。

## 什么是模型上下文协议（MCP）？

[模型上下文协议（MCP）][mcp-blog-post]让 AI 智能体能够与外部工具和服务通信。使用 MCP 后，AI 智能体可以实时访问最新信息，并代表你执行操作。

智能体通过 MCP 服务器访问这些工具和资源。MCP 服务器充当 AI 智能体与外部工具、服务之间的桥梁。每个 MCP 服务器都提供一组智能体可以访问的工具和资源。

常见的 MCP 服务器包括：

- **[GitHub MCP Server][github-mcp]**：提供用于管理 GitHub 存储库、议题和拉取请求的 API。
- **[Playwright MCP Server][playwright-mcp-server]**：使用 Playwright 提供浏览器自动化功能。

还有许多其他 MCP 服务器。GitHub 提供了 [MCP 注册表][mcp-registry]，帮助发现并参与生态系统。

> [!CAUTION]
> 请像对待项目的其他依赖项一样对待 MCP 服务器。使用前先检查源代码、验证发布者，并考虑安全影响。

## 添加 Playwright MCP 服务器

如果 Copilot CLI 尚未配置 Playwright MCP 服务器，请将它添加进来，让 Copilot 能像用户一样操作网站。

> [!NOTE]
> 如果 Copilot CLI 已配置 Playwright MCP，请跳过这些设置步骤，继续下一部分。

1. 返回 Codespace。
2. 在 Copilot CLI 中输入以下命令，打开添加 MCP 服务器的对话框：

   ```plaintext
   /mcp add
   ```

3. 名称输入 `playwright`，然后按 <kbd>Tab</kbd>。
4. 按 <kbd>Enter</kbd> 确认服务器类型为 **STDIO**，然后按 <kbd>Tab</kbd>。
5. 在 **Command** 对话框中粘贴以下命令：

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. 按 <kbd>Control</kbd>+<kbd>S</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>S</kbd>（Windows/Linux）保存新的 MCP 服务器。
7. 按 <kbd>Esc</kbd> 退出 MCP 对话框。

## 让 Copilot 使用 Playwright 体验功能

之前你已手动确认功能符合预期。现在使用 Copilot 中的 Playwright MCP 服务器完成同样的操作。

1. 使用以下提示，让 Copilot 通过 Playwright MCP 服务器验证功能：

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> 通常 Copilot 会自动找到 MCP 服务器，不一定需要明确要求它使用该服务器。不过，指出应使用的工具有助于保持结果一致，也能节省一些 token。

2. 观察 Copilot 如何列出它在浏览器中执行的操作，以确认功能是否正常。
3. 阅读报告，确保一切符合预期。

Copilot 会启动服务器，使用 Playwright 与网站交互，停止服务器，然后提供报告。

## 总结和后续步骤

恭喜！你已使用 Playwright MCP 服务器，通过 Copilot CLI 在真实浏览器中体验功能。回顾一下，你：

- 了解了模型上下文协议（MCP）以及 Copilot CLI 如何使用它。
- 在尚未配置时添加了 Playwright MCP 服务器。
- 让智能体操作浏览器并体验了筛选功能。

接下来，你将[创建 QA 自定义智能体][next-lesson]，把技能和浏览器工具结合起来，供专门的角色使用。

## 资源

- [MCP 是什么，为什么大家都在讨论它？][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [向 Copilot CLI 添加 MCP 服务器][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
