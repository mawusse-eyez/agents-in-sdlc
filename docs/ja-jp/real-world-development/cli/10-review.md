---
title: "レッスン 10 - まとめと次のステップ"
description: "Copilot CLI のワークフロー、2 つのプル リクエスト、再利用できるカスタマイズ、参考資料を振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Tailspin Toys の一連のワークフローで GitHub Copilot CLI を使いました。次のことを行いました。

- Codespace を準備し、Copilot CLI をインストールしてプロジェクトを確認し、用意されているフィルタリング issue を見つけました。
- 星評価を追加し、転送されたブラウザーで結果を確認して、最初のプル リクエスト (PR) を手動でマージしました。
- フィルタリング issue から始め、Plan モードで方針を決め、Autopilot モードで実装し、Interactive モードでレビューしました。
- カスタム命令でエージェントを案内し、既存の `quality-checks` スキルをカスタマイズして、単体テスト、lint、型チェックを実行しました。
- Playwright Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーでフィルタリングを確認しました。
- 品質保証 (QA) 用のカスタム エージェントを作成して選択し、要件、テスト範囲、スキルの結果、ブラウザーでの検証結果を評価しました。
- フィルタリングの変更全体をレビューし、フィルタリング PR に対して Agent Merge を承認しました。
- コンテキスト、モデル、共有、任意の cloud agent への委任に使うスラッシュ コマンドを確認しました。

## 作成したもの

このワークショップには、更新済みの `main` からそれぞれ別のブランチを作成する、2 つの PR の節目があります。

1. **星評価:** ゲーム カードに既存の `starRating` と、評価がない場合の状態を明示して表示します。
2. **フィルタリングと品質ワークフロー:** フィルタリングを実装し、命令を更新して機能に適用し、`quality-checks` のレポートをカスタマイズして QA プロファイルを作成し、関連するテストを追加します。

フィルタリングの計画から PR の作成まで、同じ会話とブランチを使いました。ワークショップを簡潔にするため、これらの作業を 1 つの PR にまとめました。

## さまざまな方法で検証する

自動テスト、自分で行うブラウザー確認、MCP 経由で Copilot が行うブラウザー調査を使ってコードを確認しました。`quality-checks` スキルは単体テスト、lint、型チェックを実行し、設定した形式で結果を報告しました。QA エージェントは、PR の前にそれらの結果と要件およびテスト範囲のレビューをまとめました。

追加したテストは、実際の不足を補うものである必要があります。QA の実行で新しいテストが不要と判断される場合もあります。マージを承認する前にコードと検証結果を確認し、変更後は関係する検証結果を更新してください。

## ベスト プラクティス

Copilot に与えるコンテキストやツールは、作業の結果に影響します。このワークショップでは、命令を更新し、スキルをカスタマイズし、QA プロファイルを作成し、MCP サーバーを構成しました。これらのカスタマイズは会話をまたいで再利用し、チームのニーズに合わせて調整できます。命令は標準を定め、スキルは繰り返し実行するタスクを説明し、カスタム エージェントは専門的な役割を定義し、MCP サーバーは外部ツールに接続します。エージェントの要約だけでなく、実際の変更とツールの結果を確認してください。

タスクに合った**モードとモデル**を選びます。**Plan** は実装前に方針を検討するとき、**Interactive** は小さな変更で作業に関わり続けたいとき、**Autopilot** は範囲が明確なタスクに適しています。定型的な編集には高速なモデルを、複雑な作業にはより高性能なモデルを選びます。

インフラストラクチャと同じように、コンテキストも重要です。何を、なぜ、どのように作るのかを明確に伝えることで、結果は大きく変わります。

## さらに試す

基本的なワークフローを終えました。Copilot CLI の機能をさらに確認するには、次を試してください。

- `/review` でコードレビュー エージェントに変更を分析してもらいます。
- `/rubber-duck` で問題を整理し、別の視点を得ます。
- `/fleet` で独立したサブタスクを並行して調整します。
- `/worktree` で別のタスクを分離します。
- `/delegate` で Copilot cloud agent にタスクを委任します。

## 次のステップ

ツールの使い方を上達させるには、使い続けることが一番です。製品コード、趣味のコード、いつか作ろうと思っていた小さなアプリなどで活用してください。チームと学んだことを共有し、互いの経験から学びましょう。必要に応じてドキュメントも確認してください。

ターミナルから Tailspin Toys を拡張する場合は、オプションの[Foundry Backer Concierge シリーズ][foundry]に進みます。別の環境と比較するには、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、または [Copilot cloud agent ワークショップ][cloud]を確認してください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI のコマンド リファレンス][cli-reference]
- [Copilot CLI をカスタマイズする][customize-cli]
- [Copilot CLI でプル リクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
