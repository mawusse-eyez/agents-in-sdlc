---
title: "第 8 课 - 创建并合并功能 PR"
description: "一起审查筛选功能、指令、技能更新、QA 配置文件和测试，然后创建 PR 并使用 Agent Merge。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

筛选功能实现、指令更新、技能更新、质量保证（QA）配置文件和测试都保存在同一个分支中。现在可以一起审查这些内容并创建拉取请求。你已手动合并星级评分拉取请求（PR）；这次将使用 **Agent Merge** 管理合并流程。

> [!NOTE]
> 通常，我们会将功能、指令更新、技能更新和 QA 智能体拆分到几个独立的 PR 中。为简化本研讨会的流程，你在同一个对话和分支中完成了筛选及质量工作，并将所有更改放在这个 PR 中。

在本课中，你将：

- 了解 Agent Merge 以及它如何自动处理合并生命周期。
- 检查完整的功能更改和验证证据。
- 创建筛选功能 PR。
- 仅在审查后启用 Agent Merge，并确认 PR 已合并。

## 场景

在筛选工作流中，你使用 Copilot 规划、实现并验证了功能。现在 Tailspin Toys 希望自动处理剩余的 PR 工作，同时由开发者掌控合并授权。

## 了解 Agent Merge

**Agent Merge** 会自动处理合并拉取请求所需的后续工作。启用后，Copilot 会解决阻止 PR 合并的问题，例如修复失败的持续集成（CI）检查、回复审查意见，以及在需要时变基；之后，如果存储库允许，还会启用 GitHub 自动合并。

到目前为止，你都是自行选择 **Merge pull request**。Agent Merge 可以代为处理这项工作。启用 Agent Merge 前，请先审查更改并确认可以合并。

## 使用 Agent Merge 管理 PR

代码都已完成，现在一起审查并创建 PR，然后让 Agent Merge 处理剩余流程。

1. 返回 Codespace。
2. 输入 `/agent` 打开智能体对话框。
3. 从选项列表中选择 **Default**，然后按 <kbd>Enter</kbd>。
4. 使用命令 `/pr create` 创建新的 PR。
5. 使用 `/pr agentmerge` 启用 Agent Merge。
6. Copilot 会监控 PR 的持续集成流程。所有检查成功后，它将执行合并。
7. 确认 Copilot 显示了类似“PR #14 was squash-merged successfully.”的消息。

> [!IMPORTANT]
> Agent Merge 不会绕过必需的审批、分支保护、合并队列、存储库设置或权限要求。如果流程受阻，请查看报告的原因，并在存储库允许时手动完成审查后的合并。

## 总结和后续步骤

你已将代码生成、测试和验证以及拉取请求处理等多个开发步骤自动化。在本课中，你：

- 了解了 Agent Merge 以及它如何自动处理合并生命周期。
- 检查了完整的功能更改和验证证据。
- 创建了筛选功能 PR。
- 仅在审查后启用了 Agent Merge，并确认 PR 已合并。

接下来，你将[探索更多实用的 Copilot CLI 斜杠命令][next-lesson]，管理上下文和模型、共享会话，并选择性地委派给云智能体。

## 资源

- [使用 Copilot CLI 管理拉取请求][manage-prs]
- [Copilot CLI 命令参考][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
