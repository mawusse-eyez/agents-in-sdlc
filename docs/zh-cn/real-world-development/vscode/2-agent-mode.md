---
title: "练习 2 - 使用 Copilot 智能体模式添加功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

即使是简单的应用更新，通常也涉及多个文件，还需要运行测试。开发者往往需要定位相关文件、修改代码、运行测试、调试，并不断检查是否遗漏了文件。Copilot 智能体模式可以在 IDE 中更自主地处理这类工作：探索项目、执行必要更改、运行测试并修复发现的问题。现在使用智能体模式为网站添加新功能。

> [!NOTE]
> 智能体模式和 cloud agent 名称相似，但适用于不同场景。智能体模式在集成开发环境（IDE）中执行任务，可快速反馈并随时交互；cloud agent 则像团队成员一样异步工作，通过议题和拉取请求与你协作。

在本练习中，你将了解如何：

- 让 Copilot 智能体模式探索项目、识别相关文件并协调更改。
- 使用 Copilot 智能体模式跨用户界面（UI）和数据层实现新功能。
- 在将更改合并到代码库之前，审查 Copilot 生成的更改和测试。

## 场景

游戏列表不断扩大，你希望允许用户按类别和发行商筛选。上一练习已添加发行商辅助函数，现在将使用 Copilot 智能体模式完成剩余的数据层、UI 和测试工作。

## 运行 Tailspin Toys 网站

修改代码前，先探索网站，了解当前功能。

Tailspin Toys 是一个开发者主题棋盘游戏众筹平台，可列出游戏并显示游戏详情。该网站是一个单体 Astro 应用，会在构建时将页面渲染为静态超文本标记语言（HTML）。页面在 frontmatter 中通过 Drizzle ORM 直接查询本地 SQLite 数据库；没有独立后端应用程序编程接口（API）或客户端 UI 框架。可复用的数据访问辅助函数位于 `src/lib/`，交互功能通过使用标准文档对象模型（DOM）API 的小型 Astro `<script>` 实现。

### 启动网站

使用 `npm run dev` 任务启动 Astro 开发服务器。

1. 返回上一练习使用的 Codespace。你应已回到 `main` 分支。
2. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开终端。
3. 更新 `main` 并创建筛选功能分支：

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 启动网站：

   ```bash
   npm run dev
   ```

   Astro 开发服务器就绪后，会显示类似以下内容：

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

5. 如果弹出提示，询问是否要为 `http://localhost:4321` 打开浏览器，请选择 **x** 关闭。
6. 按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），然后在终端中选择 Astro 服务器地址 `http://localhost:4321`，打开网站。

> [!NOTE]
> 在 Codespace 中选择终端的 localhost 链接时，会自动跳转到 `https://<your-codespace-name>-4321.app.github.dev/`。这是连接到 Codespace 中 Web 服务器的私有隧道。

### 浏览网站

网站启动后，可以浏览其功能：

- **主页**：显示棋盘游戏列表，包括标题、图片和描述。
- **游戏详情页**：选择游戏后会打开详情页，显示标题、描述、发行商和类别等信息。

## 使用 Copilot 探索待办事项

> [!TIP]
> **打开 Copilot Chat**
>
> 开始练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始全新对话。模式和模型的选择因练习而异；每个步骤会在相关处说明。

网站的初始实现已可运行，但还可以添加新功能。先查看从模板创建项目时自动生成的待办议题，并让 GitHub Copilot 帮助查看。

1. 在 Chat 视图的智能体下拉菜单中选择 **Agent**。Agent 智能体可以自主规划并修改多个文件、运行终端命令和调用工具。

   ![Chat 视图中智能体选择器的截图。](../../../_images/shared-chat-mode-selector.png)

2. 从可用模型列表中选择 **Claude Sonnet 4.5**。

> [!CAUTION]
> 本研讨会作者并未偏好某个模型。编写研讨会时使用了 Claude Sonnet 4.5，因此将其列入说明，以便建议结果尽可能一致。不过，大型语言模型（LLM）的输出具有概率性，实际建议可能不同。这是正常现象。

> [!NOTE]
> Copilot 可能会使用不同的 MCP 命令，但仍应能完成任务。

3. 向 Copilot 发送以下提示，查看 GitHub 存储库中的待办事项：

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. 选择 **Continue**，允许运行列出所有议题的命令。
5. 查看生成的议题列表。

留意 Copilot 如何根据它判断的用户价值对议题进行排序。

## 查看指令文件

生成代码前，先查看将用于向 Copilot 提供上下文的指令文件。本练习将使用 [UI 指令文件](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)，其中介绍了如何为网站添加功能。

1. 在 Codespace 中打开 `.github/instructions/ui.instructions.md`。
2. 查看整体指导，包括：
   - 架构概述。
   - 组件设计、可测试性和无障碍原则。
   - 指向 Astro、Tailwind CSS 和 Drizzle 等特定文件指令的链接。

> [!TIP]
> 指令文件可以引用其他指令文件和项目文件。路径相对于指令文件本身，便于复用内容、拆分复杂指导，并提供示例和模板。

## 实现筛选功能

完成筛选至少需要对应用程序进行三项更改：

- 在数据层（`src/lib/`）添加或完善剩余筛选逻辑。
- 为筛选行为添加或更新测试。
- 更新游戏列表页，添加筛选 UI。

Copilot 智能体模式可以完成这些工作并运行测试。

1. 继续当前 Copilot 对话，或选择 **New Chat** 开始新对话。
2. 选择 **Add Context**、**Instructions**，然后选择 **ui** 指令文件。

   ![选择 UI 指令文件的示例截图](../../../_images/ex3-select-instructions-file.png)

3. 确认 Chat 视图的智能体下拉菜单中仍选中 **Agent**。

   ![Chat 视图中智能体选择器的截图。](../../../_images/shared-chat-mode-selector.png)

4. 确认仍选择 **Claude Sonnet 4.5** 模型。
5. 使用以下提示，请 Copilot 根据待办议题实现功能：

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. 观察 Copilot 如何探索项目并查找相关数据层辅助函数、UI 和测试，然后修改文件并运行测试。

   ![Copilot 探索项目文件的截图](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot 会探索项目、修改文件并运行测试。根据任务和代码库的复杂度，这可能需要几分钟。过程中编辑器可能会出现 **Keep** 和 **Undo** 按钮。Copilot 完成后，每项更改都会提供 **Keep** 或 **Undo**，无需在工作过程中立即选择。

7. Copilot 提示运行测试时，选择 **Continue**。

   ![Copilot Chat 面板中要求确认运行测试的对话框](../../../_images/ex3-agent-mode-run-tests.png)

8. 过程中可能会暂停，或暂时出现测试失败。这是正常的。Copilot 会在生成代码和运行测试之间迭代，直至完成任务且不再发现错误。

   ![Copilot 智能体模式完整会话的截图](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 检查生成的代码是否存在潜在问题。

> [!CAUTION]
> 始终需要审查 Copilot 或其他 AI 工具生成的代码。

10. 返回正在运行网站的浏览器，体验新功能。
11. 确认功能正常并审查代码后，在 Copilot Chat 窗口中选择 **Keep**。

## 总结和后续步骤

本练习介绍了如何使用 GitHub Copilot 智能体模式为 Tailspin Toys 网站添加功能。你了解了如何：

- 使用智能体模式跨 UI 和数据层实现新功能。
- 让智能体模式探索项目、识别相关文件并协调更改。
- 在合并到代码库之前审查 Copilot 生成的更改和测试。

接下来使用 [Playwright MCP 服务器测试功能][next-lesson]，并为其创建拉取请求。

### 可选探索练习 – 实现分页

游戏列表增长后需要支持分页。使用本练习中学到的技能，提示 Copilot 更新网站并实现分页：

- 遵循现有最佳实践，包括使用现有指令文件。
- 确定分页方式，例如是否允许用户选择每页大小，或使用固定值。
- 编写提示时提供 Copilot 完成实现所需的指导。
- 根据需要与 GitHub Copilot 迭代，要求修改并补充上下文。这是正常工作方式。

## 资源

- [Copilot 的 ask、edit 和 agent 模式：功能及适用场景][choose-mode]
- [VS Code 中的智能体模式][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
