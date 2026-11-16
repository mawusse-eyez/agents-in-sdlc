---
slug: ja-jp/real-world-development/cli
title: "GitHub Copilot CLI"
description: "Copilot CLI のモード、カスタマイズ、MCP ツール、プル リクエストの自動化を学びながら、Tailspin Toys に 2 つの変更を加え、検証して公開します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

**[GitHub Copilot CLI][about-copilot-cli]** を使うと、ターミナルで GitHub Copilot をエージェント型コーディング アシスタントとして利用できます。コードベースを調べ、コードを生成し、コマンドを実行し、外部ツールに接続できます。すべてコマンド ラインから行えるため、グラフィカル エディターに切り替えずに作業を続けられます。

このワークショップでは、Tailspin Toys で一連の作業を進めます。

1. GitHub Codespaces でプロジェクトを準備し、Copilot CLI をインストールして、プロジェクトを確認します。
2. 星評価の変更を加え、ブラウザーで確認して、最初のプル リクエスト (PR) を手動でマージします。
3. フィルタリング issue から始め、Plan モードで方針を決め、Autopilot モードで実装し、Interactive モードでレビューします。
4. リポジトリの命令を更新し、フィルタリング作業に適用します。
5. 既存の `quality-checks` スキルをカスタマイズし、プロジェクトのチェックを実行します。
6. Playwright Model Context Protocol (MCP) サーバーを追加し、ブラウザーでフィルタリングを確認します。
7. 品質保証 (QA) 用のカスタム エージェントを作成して使い、要件、テスト範囲、検証の証拠を確認します。
8. フィルタリングの変更全体をレビューし、Agent Merge でフィルタリング PR を処理します。
9. コンテキスト、モデル、共有、任意の cloud agent への委任に使う便利なスラッシュ コマンドを確認します。

このワークショップでは、星評価の PR と、命令の更新、スキルの更新、QA プロファイル、テストを含むフィルタリングの PR の、合計 2 つを作成します。フィルタリングと品質確認の作業では、会話とブランチを 1 つにまとめ、各ツールを学びながら作業を積み重ねます。

## レッスン

| レッスン | トピック | 説明 |
| ------ | ----------- | ----------- |
| [0. 前提条件][ex0] | セットアップ | リポジトリと Codespace を作成します |
| [1. Copilot CLI のインストール][ex1] | インストール | Copilot CLI をインストールして認証し、使い始めます |
| [2. 星評価を追加する: 小さな改善][ex2] | 最初の変更 | 既存の評価と評価がない場合の状態を表示し、最初の PR をマージします |
| [3. エージェント モード: Plan と Autopilot][ex3] | エージェント モード | issue に基づいて機能を計画し、Autopilot で作成して、Interactive モードでレビューします |
| [4. カスタム命令で Copilot を導く][ex4] | コンテキスト | 既存の命令を確認して更新し、フィルタリングに適用します |
| [5. quality-checks スキルをカスタマイズして使う][ex5] | 繰り返し実行するチェック | 既存のスキルを確認し、レポート形式を変更して実行します |
| [6. Playwright MCP で機能を検証する][ex6] | ブラウザーでの確認 | CLI で MCP を構成し、フィルタリングの動作を確認します |
| [7. QA エージェントを作成して使う][ex7] | 要件とテスト範囲 | 専門エージェントを作成して選択し、最終確認の証拠を集めます |
| [8. 機能の PR を作成してマージする][ex8] | レビューとマージ | 変更全体をレビューし、PR を作成して Agent Merge を使います |
| [9. GitHub Copilot CLI のスラッシュ コマンド][ex9] | CLI 機能 | コンテキスト、モデル、共有、cloud agent への任意の委任を確認します |
| [10. まとめと次のステップ][ex10] | まとめ | ワークフロー、再利用できるカスタマイズ、参考資料を振り返ります |
| [オプション: Foundry を組み込む][foundry] | ホスト型エージェント | モデルを準備し、カタログに基づくエージェントをデプロイして Web サイトに接続します |

## 前提条件

このワークショップを始める前に、次のものを用意してください。

- [ ] **Copilot Student、Pro、Pro+、Business、Enterprise** のいずれかが有効な GitHub アカウント
- [ ] リポジトリと Codespace を作成する権限
- [ ] ターミナルまたはコマンド ライン操作の基本的な知識

> [!TIP]
> 有料プランを利用していない場合、認証済みの学生は [GitHub Education][student-plan] を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使うエージェント、MCP、コードレビュー、Copilot CLI の機能が含まれています。

[student-plan]: https://github.com/education/students

> [!NOTE]
> Copilot Business または Copilot Enterprise を使う場合は、管理者が Copilot CLI を有効にしていることを確認してください。

## はじめる

**[前提条件から始める][ex0]**

[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-cli/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-cli-power-tools/
[ex10]: 10-review/
[foundry]: 8-foundry-agent/
