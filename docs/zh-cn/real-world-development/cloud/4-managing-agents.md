---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前两项练习中，你让 Copilot cloud agent 承担了三项不同任务，用于改进用户体验和添加功能。cloud agent 会异步自主工作，但监控任务进展仍然很重要。

你可以使用多种工具管理分配给 cloud agent 的任务，包括 GitHub.com 上的[智能体页面][agents-page]。在这个 mission control 中，你可以查看所有拥有未关闭拉取请求（PR）的智能体任务，检查已执行的操作，也可以引导正在进行的会话。

在本课中，你将：

- 查看智能体页面并监控 cloud agent 任务。
- 引导正在进行的会话，要求添加其他功能。

## 场景

将高对比度模式任务分配给智能体后，团队意识到也可以同时添加浅色模式。网站样式和切换功能正在更新，正好适合纳入这项功能。你将引导智能体，让它同时添加浅色模式和高对比度模式。

## 查看 Copilot cloud agent 任务

查看分配给 Copilot cloud agent 的任务状态。

1. 打开 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 查看主区域和左侧区域中的任务列表。列表中应包含你分配给 Copilot 的任务，例如：
   - 更新代码文档。
   - 生成用于修改游戏的 API。
   - 为网站添加高对比度模式。
3. 选择一个正在运行的任务，查看 Copilot 已执行的操作，例如：
   - 从存储库检出代码。
   - 为 Copilot 创建工作环境。
   - 设置 MCP 服务器。
   - 执行完成分配任务的各种操作。

> [!NOTE]
> 具体显示的步骤因 Copilot 的工作状态和所采用的方法而异。

4. 查看右侧显示的 PR 面板，以便监控 PR 和更改的文件。

## 引导 cloud agent

查看当前任务后，要求 Copilot 在实现高对比度模式时也添加浅色模式切换开关。

1. 选择与添加高对比度模式相关的会话。具体标题取决于 Copilot 使用的名称和当前工作状态。

    ![mission control 中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 观察会话几分钟，直到设置完成并开始执行任务。出现类似下方的消息时，表示已开始工作。
3. 在 **Steer active session while Copilot is working** 对话框中输入以下提示：

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![智能体页面上的 cloud agent 任务及突出显示的 Steer active session while Copilot is working 对话框](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示。
5. 留意 Copilot 如何确认提示并将其纳入工作流程。

## 等待 Copilot 完成

和之前一样，Copilot 会继续处理更新后的任务。收到消息后，它会先完成当前步骤，再将新请求纳入工作流程。

这可能需要几分钟。等待时可以回顾到目前为止的学习和探索内容。

## 总结和后续步骤

本课介绍了 Copilot 智能体页面，这是监控和引导 GitHub Copilot cloud agent 任务的中心位置。你可以在这里跟踪进行中和已完成的任务、审查工作，也可以在任务执行期间调整范围或补充指导。

本练习介绍了以下内容：

- 使用 mission control 和智能体页面监控 cloud agent 任务。
- 引导正在进行的会话，要求添加其他功能。

Copilot 正在完成无障碍功能。接下来[迭代改进 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代改进 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
