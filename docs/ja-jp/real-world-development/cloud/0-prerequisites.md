---
title: "演習 0: 前提条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Copilot cloud agent の演習を始める前に、必要なものを準備します。Tailspin Toys リポジトリのコピーを作成し、[Codespace][codespaces] を起動します。Codespace では、命令ファイルの編集と cloud agent が作成した変更のレビューを行います。

## ワークショップ用リポジトリを設定する

コードの作業に使うリポジトリを作成するため、[テンプレート][template-repository]から自分用のリポジトリを作成します。新しいリポジトリには演習に必要なファイルが含まれます。

1. ブラウザーで [Tailspin Toys のテンプレート][tailspin-template]を開きます。
2. リポジトリのページで **Use this template** を選択し、次に **Create a new repository** を選択して、自分用のコピーを作成します。

   ![Use this template ボタン](../../../_images/ex0-use-template.png)

3. GitHub または Microsoft が主催するイベントでワークショップに参加している場合は、メンターの案内に従います。それ以外の場合は、GitHub Copilot を利用できる組織に新しいリポジトリを作成します。

   ![リポジトリ テンプレートの設定を入力](../../../_images/ex0-repository-settings.png)

4. 作成したリポジトリのパス (**organization-or-user-name/repository-name**) を控えておきます。演習中にこの値を参照します。

## Codespace を作成する

次に、演習で使う Codespace を作成します。

[GitHub Codespaces][codespaces] は、ブラウザーから直接コードを作成、実行、デバッグできるクラウド開発環境です。複数のプログラミング言語、拡張機能、ツールに対応した IDE を利用できます。

1. 作成したリポジトリを開きます。
2. 緑色の **Code** ボタンを選択します。

   ![Code ボタンを選択](../../../_images/ex0-code-button.png)

3. **Codespaces** タブを選択し、**+** ボタンを選択して新しい Codespace を作成します。

   ![新しい Codespace を作成](../../../_images/ex0-create-codespace.png)

Codespace の作成には数分かかりますが、必要なサービスを手動でインストールするよりも早く準備できます。作成を待つ間に、次に紹介する GitHub Copilot の機能を確認してもかまいません。

> [!CAUTION]
> 今後の演習で Codespace に戻ります。ひとまず、ブラウザーのタブで開いたままにしてください。

> [!NOTE]
> このワークショップは Codespace またはローカルの [開発コンテナー][dev-containers]内で実行するように構成されています。どちらも必要な前提条件がインストール済みの環境を提供します。ローカルで実行する場合は、クローンしたリポジトリを VS Code で開き、プロンプトが表示されたら **Reopen in Container** を選択してください。Codespace と同じ開発コンテナーが構築されます。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## まとめ

ワークショップ用リポジトリのコピーを作成し、Copilot cloud agent と作業するための Codespace の作成を開始しました。

## 次のステップ

次は、cloud agent が従うカスタム命令を追加します。[演習 1 - カスタム命令][next-lesson]に進んでください。

## リソース

- [GitHub Codespaces の概要][codespaces]
- [テンプレートからリポジトリを作成する][template-repository]
- [Codespaces を使い始める][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
