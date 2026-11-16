---
title: "练习 1 - 自定义指令（VS Code）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：智能体模式 →][next-lesson]

使用生成式 AI 时，上下文至关重要。如果任务必须以特定方式完成，或 Copilot 需要了解背景信息，就要确保它能访问这些上下文。[指令文件][instruction-files]是向 Copilot 提供代码生成指导的重要方式。

在本练习中，你将：

- 了解项目上下文、编码指南和文档规范如何通过存储库自定义指令及按路径限定范围的指令文件传递给 Copilot。
- 使用当前指令生成筛选功能的第一个数据切片（发行商辅助函数）。
- 向 `.github/copilot-instructions.md` 添加新的全局存储库规范。
- 再次运行相同提示，观察生成的代码如何遵循新规范。
- 提交指令更新和筛选切片到 `main`，供下一练习使用。

> [!CAUTION]
> 生成的代码可能不完全遵循你设置的规范。Copilot 的结果并非确定性输出。本练习要观察的是更新指令前后行为的总体变化，而不是要求输出逐字一致。

## 指令文件

### 场景

Tailspin Toys 有一套开发实践指南和要求，包括：

- 数据层必须始终有单元测试。
- UI 应采用暗色模式并具有现代感。
- 应使用 TSDoc 文档注释为代码添加文档。
- 每个文件开头都应有一段注释，说明文件的用途。

通过指令文件，你可以确保 Copilot 按照这些实践执行任务。

### 自定义指令

自定义指令可向 Copilot 提供上下文和偏好，帮助它理解你的编码风格和要求。你可以为整个存储库或特定文件类型创建指令。

指令文件有两种：

- `.github/copilot-instructions.md`：每个存储库只有一个此类文件，Copilot 会在处理该存储库的**每个**请求时读取它。文件中应包含技术栈、项目概况、最佳实践等项目级信息。
- `.github/instructions/*.instructions.md`：为特定任务或文件类型创建此类文件，例如为 TypeScript、Astro、UI 组件或单元测试提供指导。

> [!NOTE]
> 在 IDE 中，指令文件仅用于 Copilot Chat 的代码生成，不用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot cloud agent 在生成代码时都会使用存储库级指令文件以及带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> Copilot 还[支持其他标准的指令文件][custom-instructions-support]，包括 AGENTS.md 和 CLAUDE.md。

为指令文件提供清晰、简洁的自然语言说明，并附上代码示例。将项目级指导放入 `copilot-instructions.md`，将文件类型或任务专用指导放入 `*.instructions.md`。不同项目的做法会有所不同，可通过试验找到合适方案。

> [!TIP]
> 示例项目中有适用于多种任务的指令文件，例如 [UI 更新][ui-instructions]和 [Astro][astro-instructions]。Copilot 也可以帮助生成指令文件，不同工作环境的入口各不相同，例如 VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`。还可以查看 [awesome-copilot][awesome-copilot] 中的模板和示例。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 查看项目中的自定义指令文件

先查看存储库附带的指令文件，了解现有指导。

1. 打开 `.github/copilot-instructions.md`。
2. 查看项目简介以及 **Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等部分。留意 **Code standards** 下的 **GitHub Actions Workflows** 指引。
3. 打开 `.github/instructions` 文件夹并浏览其中的文件。你会看到适用于 Astro 文件、Drizzle 数据层、测试等内容的指令。
4. 打开 `.github/instructions/unit-tests.instructions.md`。留意顶部的 `applyTo` 字段；它使用相对于存储库根目录的 glob 来确定指令适用的文件，例如符合 `**/*.test.ts` 的 TypeScript 测试文件。
5. 查看此项目针对单元测试的具体指令。
6. 打开 `.github/instructions/drizzle.instructions.md` 并滚动到底部，查看它指向其他指令文件（如 `unit-tests.instructions.md`）和项目现有文件的链接。路径相对于指令文件本身。

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分介绍了项目编码标准，但尚未要求添加代码文档。接下来会加入 TSDoc 文档注释和文件级注释头规范。

## 为更改创建分支

为本次更改创建一个分支。

1. 返回上一练习使用的 Codespace。
2. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开终端。
3. 创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions
   ```

## 更新指令前先使用 Copilot Chat

> [!TIP]
> **打开 Copilot Chat**
>
> 开始练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始全新对话。模式和模型的选择因练习而异；每个步骤会在相关处说明。

先使用当前指令文件发送提示，之后更新指令并再次发送相同提示，以便观察差异。

1. 关闭之前练习留下的编辑器标签页，让 Copilot 只获取所需上下文。
2. 打开 `src/lib/publishers.ts`，让 Copilot 知道辅助函数应放在哪里。
3. 在 Chat 视图的智能体下拉菜单中选择 **Agent**，以便 Copilot 修改文件。

   ![Chat 视图中智能体选择器的截图。](../../../_images/shared-chat-mode-selector.png)

4. 发送以下提示：

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot 会探索项目并应用代码更改，通常会同时修改辅助函数文件和测试。
6. 留意生成的辅助函数是带类型的函数，它将 `db` 客户端作为第一个参数，并返回带类型的发行商数组。这来自 `.github/instructions/drizzle.instructions.md` 中适用于 `src/lib/*.ts` 的数据层规范。
7. 留意生成的代码**缺少** TSDoc 文档注释和文件级注释头。

> [!CAUTION]
> Copilot 的结果具有概率性，因此即使没有相关指令，也可能生成文档注释。这并不影响本练习的目标：观察更新指令后的一致性变化。

## 添加新的存储库规范

`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。现在添加编码规范，以改善代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements** 部分，该部分应位于第 27 行附近。注意其中记录了项目编码标准，但尚无代码文档规则。
3. 在现有规范下方添加以下 Markdown 内容，要求 Copilot 添加文件注释头和 TSDoc 文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 指令文件可以放在存储库级别（`.github/copilot-instructions.md`），为整个项目提供指导；也可以使用 `*.instructions.md` 为特定语言、文件类型或任务提供指导。存储库级文件适合放置添加文档注释等项目级规范。

## 再次运行提示并观察变化

1. 返回 Copilot Chat 并选择 **New Chat**，清除上下文。
2. 再次打开 `src/lib/publishers.ts`，让 Copilot 聚焦正确文件。
3. 发送与之前相同的提示：

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 留意文件现在是否以类似以下注释块开头：

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. 留意生成的函数现在是否包含类似以下 TSDoc 注释：

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

你已引导 Copilot 遵循新的项目规范，并将其应用到后续练习会用到的实际代码中。

## 提交指令并推送分支

指令文件与存储库中的其他文件一样，使用相同的源代码管理方式。现在提交并推送分支。

1. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开终端。
2. 运行以下命令，确认指令和辅助函数更改已保存：

   ```bash
   git status
   ```

3. 暂存并提交指令更新，以及 Copilot 为辅助函数基础所做的所有更改：

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # 如果 git status 显示其他配套更改（例如测试），也要添加这些文件。
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. 推送分支：

   ```bash
   git push -u origin custom-instructions
   ```

## 创建并合并拉取请求

分支推送后，创建拉取请求并将其关联到待办事项中的文档规范议题。Copilot 可以通过已连接到项目的 GitHub 工具查找议题、创建关联 PR 并合并。

1. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开终端。
2. 在 Codespace 中打开 Copilot Chat，并确认智能体选择器中选中 **Agent**。
3. 按 <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd>（Windows/Linux）打开 Copilot Chat 视图；要求 Copilot 查找与更新指令文件相关的议题，并从当前分支创建 PR，说明指令更新和新的发行商辅助函数基础：

   ```
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot 会查找议题并创建 PR。
5. Copilot 请求代表你执行 GitHub 操作时，检查命令并酌情选择 **Allow**。
6. PR 创建后，使用以下提示要求 Copilot 合并 PR 并将分支切回 main：

   ```
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. Copilot 请求代表你执行 GitHub 操作和 shell 命令时，检查命令并酌情选择 **Allow**。

你已在 GitHub Copilot 的帮助下创建并合并拉取请求。

## 总结和后续步骤

你了解了 Copilot 如何读取项目指令，并在 VS Code 中使用 Copilot Chat：

- 发送代码生成提示，观察现有指令下 Copilot 的输出。
- 向 `.github/copilot-instructions.md` 添加新的存储库级规范。
- 再次发送相同提示，观察代码如何遵循新规范。
- 将指令更新和辅助函数基础提交到 `main`，供下一练习使用。

接下来，在[智能体模式][next-lesson]中运用这些指令，让 Copilot 跨多个文件实现新功能。

## 资源

- [用于自定义 GitHub Copilot 的指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更好的 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [GitHub Copilot 个人自定义指令][personal-instructions]
- [Awesome Copilot：指令文件及其他资源汇总][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
