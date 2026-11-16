---
slug: ja-jp/real-world-development/cloud
title: "GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

**[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent)** を使うと、GitHub Copilot がクラウドで非同期に作業できます。GitHub 上で作業を割り当てると、cloud agent がバックグラウンドでリポジトリを調べ、変更を加え、プル リクエストを作成します。その間、別の作業を続けられます。

このワークショップでは、まず cloud agent が従うカスタム命令を追加し、GitHub issue を割り当てて実装を依頼します。カスタム エージェントをレビューして使い、agents ダッシュボードからセッションの進捗を確認して作業を調整します。最後に、作成されたプル リクエストをレビューし、結果を改善します。

## 演習

| 演習 | トピック | 説明 |
|----------|-------|-------------|
| [0. 前提条件][ex0] | セットアップ | リポジトリと Codespace を作成します |
| [1. カスタム命令][ex1] | コンテキスト | cloud agent が従うカスタム命令を追加します |
| [2. Cloud agent][ex2] | 非同期エージェント | GitHub issue を Copilot cloud agent に割り当てます |
| [3. カスタム エージェント][ex3] | 専門エージェント | カスタム エージェントを確認して使います |
| [4. エージェントの管理][ex4] | 監視 | エージェントのセッションを監視して調整します |
| [5. 反復と改善][ex5] | レビュー | プル リクエストをレビューし、Copilot の作業を改善して次の手順を選びます |

## 前提条件

このワークショップを始める前に、次のものを用意してください。

- [ ] **Copilot Student、Pro、Pro+、Business、Enterprise** のいずれかが有効な GitHub アカウント
- [ ] アカウントまたは組織で有効になっている Copilot cloud agent

> [!TIP]
> 有料プランを利用していない場合、認証済みの学生は [GitHub Education][student-plan] を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使うエージェント、Model Context Protocol (MCP)、コードレビュー、Copilot CLI の機能が含まれているため、すべてのハーネスを完了できます。

[student-plan]: https://github.com/education/students

> [!NOTE]
> Cloud agent は **Copilot Free を除く Copilot Student、Pro、Pro+、Business、Enterprise** で利用できます。Copilot Business または Enterprise の場合、管理者が組織で有効にする必要があります。

> [!NOTE]
> このハーネスでは MCP を扱いません。Copilot で MCP サーバーを使う方法については、[CLI ハーネス](../cli/)または [VS Code ハーネス](../vscode/)を参照してください。

## はじめる

**[演習 0: 前提条件から始める →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
