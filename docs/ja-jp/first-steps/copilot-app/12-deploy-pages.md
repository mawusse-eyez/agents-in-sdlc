---
title: "レッスン 12 - GitHub Pages でサイトをデプロイする"
description: "GitHub Copilot app を使って Pages ワークフローを設定し、プル リクエストをレビューして、公開された Space Quiz を確認します。"
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

GitHub Pages を使って Space Quiz を公開しましょう。Copilot はワークフローの準備とデプロイの案内を行いますが、変更をレビューし、サイトが公開されたことを確認するのは開発者の役割です。

このレッスンでは、次のことを行います。

- Copilot に GitHub Pages のデプロイ設定を依頼します。
- マージする前に、ワークフローとプル リクエストをレビューします。
- デプロイの進行を確認し、公開されたサイトを検証します。

## シナリオ

Space Quiz はすでに GitHub リポジトリにありますが、ほかの人が簡単に試せるようにする必要があります。単一ファイルのサイトを GitHub Pages で公開すれば、サーバーやランタイム依存関係を追加せずに、公開 URL から利用できるようになります。

## Copilot にデプロイの準備を依頼する

> [!WARNING]
> プル リクエストの作成によって、コードがコミットおよびプッシュされることがあります。プロンプトを送る前に、承認設定と送信先リポジトリを確認してください。**すべて承認**が有効な場合、別途確認を求められないことがあります。

`space-quiz` の Copilot app セッションで、次のプロンプトを送信します。

```plaintext
Prepare a GitHub Pages deployment for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages after changes reach the default branch. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and report its link and any required Pages settings or permissions. Do not merge, enable auto-merge, change Pages settings, or deploy. Stop and wait for my review.
```

## ワークフローとプル リクエストをレビューする

1. リポジトリに README がまだない場合に限り、README が追加されていることを確認します。
2. ワークフローのビルド手順とデプロイ手順、トリガー、権限を含め、プル リクエストの変更をレビューします。
3. ワークフローが、マージ前のプル リクエストではなく既定のブランチからデプロイすることを確認します。
4. 必要な修正を依頼し、更新された差分をレビューします。マージを承認する前に、必須のプル リクエスト チェックが成功するまで待ちます。

## マージとデプロイを承認する

> [!WARNING]
> 次のプロンプトを送ると、レビュー済みプル リクエストのマージ、リポジトリの Pages 設定の変更、サイトの公開をエージェントに許可します。レビューを完了し、リポジトリとプル リクエストを確認してから送信してください。承認設定によっては、これらの操作が追加の確認なしに実行されることがあります。

`<PR_NUMBER>` をレビューしたプル リクエストの番号に置き換えてから、次のプロンプトを別途送信します。

```plaintext
I have reviewed pull request <PR_NUMBER> in this repository and authorize its merge and deployment. Enable GitHub Pages using GitHub Actions, merge that pull request only after required checks pass, and monitor the deployment until it succeeds. Report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
```

![3 段階の図: マージ済みの space-quiz プル リクエスト、Build website・Upload artifact・Deploy to Pages の各ステップが成功した GitHub Actions の Deploy website 実行、yourname.github.io/space-quiz/ で公開された Space Quiz。](../../../_images/first-steps-app-pages-deploy.svg)

## デプロイを確認する

1. GitHub Actions のデプロイ実行が成功するまで確認します。
2. 報告された URL を開き、Space Quiz が読み込まれることを確認します。

エージェントが Pages の有効化やプル リクエストのマージを実行できない場合は、案内された手順に従います。デプロイが成功し、公開サイトが読み込まれるまでは完了と見なさないでください。

## まとめと次のステップ

Space Quiz が公開され、エージェントの報告だけに頼らずデプロイを確認できました。[レッスン 13: レビューと次のステップ][next-lesson]に進みます。

[next-lesson]: ../13-review/
