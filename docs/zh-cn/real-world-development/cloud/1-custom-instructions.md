---
title: "练习 1 - 自定义指令（Cloud agent）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：Copilot cloud agent →][next-lesson]

使用生成式 AI 时，上下文至关重要。如果任务必须以特定方式完成，或者 Copilot 需要了解背景信息，就要确保它能访问这些上下文。[指令文件][instruction-files]用于提供此类指导，让 Copilot 不仅了解你希望它做什么，也了解你希望它如何完成。

在本练习中，你将：

- 了解项目上下文、编码指南和文档规范如何通过存储库自定义指令及按路径限定范围的指令文件传递给 Copilot。
- 向 `.github/copilot-instructions.md` 添加新的全局存储库规范。

> [!NOTE]
> 与 VS Code 和 CLI 工作环境不同，这里不会通过前后提示进行对比。Copilot cloud agent 会异步处理 GitHub 议题，因此较难实时并排展示指令的影响。稍后审查 cloud agent 创建的拉取请求时，你会看到指令文件的作用。

## 指令文件

### 场景

Tailspin Toys 有一套开发实践指南和要求，包括：

- 数据层必须始终有单元测试。
- UI 应采用暗色模式并具有现代感。
- 应使用 TSDoc 文档注释为代码添加文档。
- 每个文件开头都应有一段注释，说明文件的用途。

通过指令文件，你可以确保 Copilot 按照这些实践执行任务。

### 自定义指令

自定义指令可向 Copilot 提供上下文和偏好，帮助它理解你的编码风格和要求。你可以通过指令引导 Copilot，使它给出更符合需求的建议和代码片段。你可以为整个存储库创建指令，也可以为特定类型的文件创建指令。

指令文件有两种：

- `.github/copilot-instructions.md`：每个存储库只有一个此类文件，Copilot 会在处理该存储库的**每个**请求时读取它。文件中应包含适用于大多数聊天或 CLI 请求的项目级信息，例如所用技术栈、项目概况、最佳实践和全局指导。
- `.github/instructions/*.instructions.md`：为特定任务或文件类型创建此类文件。你可以为 TypeScript、Astro 等语言提供指导，也可以为创建 UI 组件或单元测试等任务提供指导。

> [!NOTE]
> 在 IDE 中，指令文件仅用于 Copilot Chat 的代码生成，不用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot cloud agent 在生成代码时都会使用存储库级指令文件以及带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> Copilot 还[支持其他标准的指令文件][custom-instructions-support]，包括 AGENTS.md 和 CLAUDE.md。

### 管理指令文件的最佳实践

完整讨论如何创建指令文件超出了本研讨会的范围。示例项目展示了一种有代表性的做法，概要如下：

- 将 `copilot-instructions.md` 中的内容限定为项目级指导，例如项目说明、结构和全局编码标准。
- 使用 `*.instructions.md` 为文件类型（单元测试、Astro 组件、数据层）或特定任务提供指导。
- 使用自然语言，保持说明清晰，并提供代码示例说明推荐和不推荐的写法。

创建指令文件没有唯一方法，就像使用 AI 也没有唯一方式一样。你可以通过实验，逐步找到适合项目的做法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应该有一组完善的指令文件。查看本项目中的文件时，你会发现其中包含多种任务的指令，例如 [UI 更新][ui-instructions]和 [Astro][astro-instructions]。
>
> Copilot 也可以帮助生成指令文件。不同工作环境的入口不同，例如 VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`。相应工作环境的课程会在需要时说明具体操作。
>
> 需要模板或起点？请查看 [awesome-copilot][awesome-copilot]，其中汇集了指令文件、自定义智能体和其他资源。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 查看项目中的自定义指令文件

花些时间查看本存储库附带的指令文件：一个核心 `copilot-instructions.md` 文件，以及一组用于不同任务的 `*.instructions.md` 文件。可在编辑器或 GitHub 网页界面中打开这些文件。

1. 打开 `.github/copilot-instructions.md`。
2. 查看项目简介以及 **Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等部分。留意 **Code standards** 下的 **GitHub Actions Workflows** 指引。这些内容适用于你与 Copilot 的各种交互。
3. 打开 `.github/instructions` 文件夹并浏览其中的文件。你会看到适用于 Astro 文件、Drizzle 数据层、测试等内容的指令。
4. 打开 `.github/instructions/unit-tests.instructions.md`。留意顶部的 `applyTo` 字段，它使用相对于存储库根目录的 glob 来确定指令适用的文件。此处会匹配 TypeScript 测试文件，例如符合 `**/*.test.ts` 的文件。
5. 查看此项目针对单元测试的具体指令。
6. 最后，打开 `.github/instructions/drizzle.instructions.md` 并滚动到底部。留意它指向其他指令文件（如 `unit-tests.instructions.md`）和项目现有文件的链接。这样可以将较大的指令集拆分成更小、可复用的文件，并为 Copilot 提供示例。（其中的路径相对于指令文件，而不是存储库根目录。）

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分介绍了项目编码标准，但尚未要求添加代码文档。接下来会加入 TSDoc 文档注释和文件级注释头的规范。

## 添加新的存储库规范

接下来要编辑一次：添加项目级规则，要求在代码中使用 TSDoc 文档注释和文件级注释头。后续练习中，cloud agent 处理议题时会使用这些规范。

编辑之前，先创建一个分支。（cloud agent 会从议题目标分支读取指令，但仍建议单独提交这些更改。）

1. 在 Codespace 终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。现在添加编码规范，以改善代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements** 部分，该部分应位于第 27 行附近。注意其中记录了项目编码标准，但尚无代码文档规则，这正是生成的辅助函数没有文档注释的原因。
3. 在现有规范下方添加以下 Markdown 内容，要求 Copilot 添加文件注释头和 TSDoc 文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 如上一课所述，指令文件可以放在存储库级别（`.github/copilot-instructions.md`），为整个项目提供指导；也可以使用 `*.instructions.md` 为特定语言、文件类型或任务提供指导。存储库级文件适合放置添加文档注释等项目级规范。

## 提交、推送并合并指令更新

cloud agent 会读取议题目标分支中的指令。在下一练习中将议题分配给 Copilot 时，它会从 `main` 分支创建新分支。因此，必须先将指令更改合并到 `main`，cloud agent 才能使用它们。

1. 暂存并提交更改：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上创建从 `custom-instructions-cloud` 到 `main` 的拉取请求并合并。这样，cloud agent 在下一练习中处理分配给它的议题时就会读取这些指令。

> [!TIP]
> 如果希望在本研讨会中直接使用 `main`，可以跳过分支步骤并直接提交到 `main`。此处创建分支是为了模拟真实项目中的处理方式。

## 总结和后续步骤

你已了解 Copilot 如何读取本项目的指令文件，并向 `.github/copilot-instructions.md` 添加了新的存储库级规范。接下来可以在 cloud agent 生成的拉取请求中观察该规范的作用。

下一步，将[第一个议题分配给 Copilot cloud agent][next-lesson]。

## 资源

- [用于自定义 GitHub Copilot 的指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更好的 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot：指令文件及其他资源汇总][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
