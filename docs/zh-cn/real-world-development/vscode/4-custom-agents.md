---
title: "练习 4 - 自定义智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## 什么是自定义智能体？

GitHub Copilot 中的[自定义智能体][custom-agents-concept]是针对开发工作流中特定任务或领域定制的人工智能（AI）助手。你可以在存储库的 `.github/agents` 文件夹中使用 Markdown 文件定义智能体，为其提供专门的指令、最佳实践、编码模式和领域知识。团队可以创建可复用的智能体，例如依据《Web 内容无障碍指南》（[WCAG][wcag]）执行合规审查的无障碍智能体、遵循安全编码实践的安全智能体，或维护一致测试模式的测试智能体。

自定义智能体也可以全局定义在 `~/.copilot/agents` 中。每个文件都包含 YAML frontmatter，至少包含 `name` 和 `description`，后面是用于定义智能体行为、专长和指令的 Markdown 提示。

### 自定义智能体与智能体技能

自定义智能体与[智能体技能][agent-skills-concept]的用途有些重叠。最简单的区分方式是：**自定义智能体是工作者，技能是工具**。自定义智能体拥有自己的上下文窗口，并可以协调技能甚至其他智能体。本实验中的无障碍智能体会根据无障碍指南审查并更新网站，也可以调用拉取请求工作流或运行测试等技能。

> [!NOTE]
> 编写自定义智能体没有唯一的正确方式。通过测试和迭代，找到适合工作环境和场景的方案。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## 场景

Tailspin Toys 致力于让所有用户都能使用其众筹平台，无论用户的视觉能力或偏好如何。近期反馈指出，当前暗色主题的文字和背景对比度不足，导致难以阅读。设计团队因此要求添加可由用户开启或关闭的高对比度模式。你将使用自定义智能体快速实现此功能。

在本练习中，你将：

- 查看现有的无障碍自定义智能体。
- 在 Copilot Chat 中使用该智能体实现高对比度模式。

## 查看无障碍自定义智能体

项目已为无障碍工作创建了自定义智能体。先查看它如何引导 Copilot。

返回 Codespace，打开终端，并从 `main` 创建无障碍功能分支（筛选 PR 将与本分支分开）：

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. 打开 `.github/agents/accessibility.md`。
2. 查看包含 `name` 和 `description` 字段的 YAML frontmatter。

> [!CAUTION]
> 自定义智能体必须包含 `name` 和 `description` frontmatter。

3. 浏览文件后续部分，了解无障碍网站代码生成的核心职责、最佳实践、HTML/CSS/JavaScript 示例，以及常见问题。

## 在 Copilot Chat 中使用自定义智能体

VS Code 会在 Copilot Chat 视图底部的智能体下拉菜单中显示 `.github/agents` 中定义的自定义智能体。选择智能体后，聊天会使用该智能体的指令和工具。

> [!TIP]
> **打开 Copilot Chat**
>
> 开始练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始全新对话。模式和模型的选择因练习而异；每个步骤会在相关处说明。

1. 如果 Chat 视图的智能体下拉菜单尚未选中 **Agent**，请先选择它。

   ![Chat 视图中智能体选择器的截图。](../../../_images/shared-chat-mode-selector.png)

2. 选择 Chat 视图底部的智能体下拉菜单。它会显示当前智能体，默认是 **default**。
3. 从可用智能体列表中选择 **Accessibility agent**。
4. 向无障碍智能体发送以下提示：

    ```plaintext
    Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
    ```

5. Copilot Chat 会探索代码库、提出更改并修改项目文件。每项编辑都会在聊天中显示文件路径和差异，供你审查。
6. 随着编辑发生，**Files changed** 指示器会更新，显示智能体已修改的文件。

> [!NOTE]
> 这可能需要几分钟。Copilot 会修改 Astro 组件、CSS 和相关测试等现有文件。

下一练习中，你将审查并引导这项正在进行的工作。

## 总结和后续步骤

本课介绍了 GitHub Copilot 中的[自定义智能体][custom-agents]，它们是针对特定任务和领域定制的 AI 助手。你可以将团队的专业知识和标准整理成可复用的智能体，引导 Copilot 更有效地完成工作。

本练习介绍了以下内容：

- 如何定义自定义智能体。
- 如何在 Copilot Chat 智能体模式中使用自定义智能体。

接下来[监控并引导智能体的工作][next-lesson]，审查实时更改，并在同一会话中添加浅色模式切换开关。

## 资源

- [关于自定义智能体][custom-agents]
- [在 IDE 中创建自定义智能体][creating-custom-agents-ide]
- [VS Code 中的自定义智能体][custom-agents-vscode]
- [自定义智能体配置][custom-agents-config]
- [Awesome Copilot 中的自定义智能体][awesome-copilot-agents]

---

| [← 上一课：使用 Playwright MCP 服务器测试功能][previous-lesson] | [下一课：监控和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
