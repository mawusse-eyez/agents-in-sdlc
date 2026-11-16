---
title: "练习 5 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：自定义智能体][previous-lesson] |
|:--|

在智能体模式下，GitHub Copilot 会自主探索代码库、提出更改、编辑文件并运行命令。由于这些工作会在你的计算机上实时发生，VS Code 中的 Copilot Chat 会显示每次工具调用和文件编辑。你可以直接在聊天中审查差异、接受或撤销单项更改，也可以通过后续提示引导会话，扩展或调整工作范围。

在本练习中，你将：

- 实时监控无障碍智能体的工作。
- 审查并接受建议的文件编辑。
- 在会话进行期间引导智能体，要求它同时添加浅色模式切换开关。

## 场景

[练习 4][previous-lesson]中使用的无障碍自定义智能体正在实现高对比度模式。工作进行期间，设计团队又提出了浅色模式切换开关的需求，以便解决部分用户觉得默认主题过暗的问题。你将引导现有会话扩展工作，而不是从头开始新对话。

## 监控 Copilot 的进度

Copilot Chat 会显示智能体执行的每个步骤，包括探索的文件、运行的命令和提出的编辑。每项文件编辑都会在聊天中内嵌显示差异，并提供 **Keep** 和 **Undo** 控件。

1. 返回练习 4 中使用的 Copilot Chat 视图。
2. 智能体工作时，滚动聊天内容，查看每次工具调用。你会看到文件读取、文件编辑，以及它请求运行的终端命令。
3. 智能体提出文件编辑时，差异会内嵌显示：
   - 选择 **Keep** 接受更改。
   - 选择 **Undo** 撤销更改，让智能体重新尝试。
4. 也可以打开聊天顶部的 **Files changed** 指示器，查看该会话中智能体修改的所有文件。

> [!NOTE]
> 如果工具调用请求权限（例如运行终端命令），智能体会暂停并显示 **Allow** 提示。只批准你信任的命令。

5. 等待智能体完成高对比度模式。完成后应会显示更改摘要。

## 引导智能体添加浅色模式

高对比度模式实现后，在同一对话中添加浅色模式切换开关。继续当前会话可以保留之前的上下文，包括已修改的组件、样式方案和本地存储模式。

1. 在 Copilot Chat 输入框中发送以下后续提示：

    ```plaintext
    Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
    ```

2. 智能体会继续工作，探索已有更改并提出浅色模式更新。
3. 像审查高对比度更改一样审查每项新编辑，并使用 **Keep** 或 **Undo**。
4. 如果智能体的处理方向不符合预期，例如想重构切换 UI，可选择聊天输入框旁的 **Stop** 按钮停止任务，然后发送澄清提示。

> [!TIP]
> 引导进行中的会话通常比从头开始更快。可以用后续提示要求调整（例如“简化 CSS，改用 CSS 变量，避免重复选择器”）、纠正方向（例如“不要添加第三个开关，将浅色模式集成到现有设置面板”），或扩展范围（例如“为两个开关添加键盘快捷键”）。

## 审查工作集

提交之前，快速检查智能体修改的所有内容。

1. 在 VS Code 中打开 **Source Control** 视图。
2. 审查所有更改的文件。你应会看到 Astro 组件、样式和相关测试的更新。
3. 打开几个更改过的文件并检查差异。确认智能体遵循无障碍实践，例如无障碍富互联网应用程序（ARIA）属性、键盘导航、语义化超文本标记语言（HTML）和本地存储持久化。
4. 确认满意后，在 Source Control 面板中暂存并提交更改。下一课中会发布这些更改。

## 总结和后续步骤

你已使用 Copilot Chat 智能体模式监控并引导正在进行的会话：逐项审查文件编辑、接受或撤销更改，并使用后续提示扩展工作，同时保留上下文。

在本课中，你：

- 实时监控了智能体的工作。
- 接受或撤销了单项文件编辑。
- 使用后续提示引导了正在进行的会话。

接下来在[下一课][next-lesson]中发布无障碍功能 PR，并审查本实验中本地自定义智能体完成的更改。

## 资源

- [VS Code 中的 Copilot Chat][copilot-chat-vscode]
- [使用智能体模式][agent-mode]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代改进 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
