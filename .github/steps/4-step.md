## Step 4: レビューの自動化

カスタマイズされたレビューはうまく機能しているようですが、問題があります。手動でレビュー依頼を行っている以上、技術的には必須ではないのです。何名もの教師が活動ウェブサイトに貢献している状況では、手動でCopilotにレビューを依頼するのは明らかに持続可能な方法ではありません。特に作業者のプログラミング経験に関するレベルが様々であるため、すべてのプルリクエストが自動的にCopilotのフィードバックを受け取るようにしたいところです。すべての変更に対してCopilotレビューを必須とするリポジトリルールセットを設定しましょう。

### 📖 理論: レビュー自動化を実施するルールセット

リポジトリルールセットを使用すると、すべてのプルリクエストに対して自動コードレビューを強制適用でき、開発者が手動でレビューを依頼したりドキュメントに従うことを忘れたりすることなく、一貫した品質チェックを保証します。

Each code review consumes one [Premium Request Unit (PRU)](https://docs.github.com/en/copilot/concepts/billing/copilot-requests) from the author of the pull request.プルリクエストの作成者から、各コードレビューごとに1つの[プレミアムリクエストユニット（PRU:Premium Request Unit）](https://docs.github.com/en/copilot/concepts/billing/copilot-requests)が消費されます。

**強制するためのオプション :**

- **Repository-level**: 特定リポジトリにおける全てのプルリクエストに適用する
- **Branch-specific**: フィルターと命名パターンで特定のブランチをターゲットとする
- **Organization-level**: 複数リポジトリにルールセットを適用する

**主なメリット :**

- 全ての貢献において一貫したコード品質を保つ
- 手動介入なしで自動的に適用できる
- ブランチ保護の必要性に基づいた設定が可能
- 既存のGitHubワークフロー権限との統合

詳細については、[リポジトリルールセットのドキュメント](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets)を参照してください。

### ⌨️ Activity: リポジトリルールセットの作成

1. 上部ナビゲーションで、**Settings**タブを選択する

1. 左側のナビゲーションで、**Rules**を展開し、**Rulesets**を選択する

1. **New ruleset**ボタンをクリックし、**New branch ruleset**オプションを選択する

1. 次のように、ルールセット名とステータスを設定する :

   - **Ruleset Name**: `Require Copilot Reviews`
   - **Enforcement Status**: `Active`

1. **Target branches**で、`main`ブランチに対する保護を追加します

   1. **Add target** をクリック、**Include default branch**を選択
   1. **Add target** をクリック、**Include by pattern**を選択
   1. `main`と入力し、**Add inclusion pattern**ボタンをクリック

   <img width="300" alt="screenshot of target branches" src="https://github.com/user-attachments/assets/217f205c-7a61-4ffa-a0a6-7e76ff8d7906"/>

1. **Rules**で、以下のオプションを有効にする :

   - **Require a pull request before merging(マージ前にプルリクエストを要求する)**: ☑️
   - **Require conversation resolution before merging(マージ前にConversationの解決を要求する)**: ☑️
   - **Automatically request Copilot code review(Copilotの自動コードレビューをリクエストする)**: ☑️

1. 画面下部までスクロールし、**Create**ボタンをクリックする

1. 開いているプルリクエストに戻る

1. マージボタンが無効になっていることに注意してください

   <img width="300" alt="screenshot of disabled merge button" src="https://github.com/user-attachments/assets/28e4cb05-f09d-423d-8c77-8f0ec61c73ad"/>

1. コパイロットからの現在および過去のフィードバックをすべて解決するには、**Resolve conversation(会話の解決)**をクリックします(今は実装する必要はありません)

1. プルリクエストをマージする

   > 🪧 **Note**: If the **Merge pull request** button doesn't activate, check for unresolved conversations in the outdated comments.**Merge pull request**ボタンが有効化されない場合は、古いコメント内の未解決の会話がないか確認してください。

1. プルリクエストがマージされたら、Monaが作業を確認し、フィードバックを提供し、最終レビューを行うまでしばらくお待ちください。素晴らしい！これで完了です！ 🎉

### ⌨️ Activity: (optional) 自動レビューのテスト

まだ終わらせたくない？ハードコードされたお知らせのバナーが気になる？私たちも同じです！

では、修正しますか 🧑‍🚀🚀

> [!NOTE]
> 新しいお知らせ機能を修正する必要はありません。自動レビューをテストしたいだけなら、簡単な変更を加えて新しいプルリクエストを開始するだけで十分です。

1. VS Codeで`main` ブランチに戻り、マージされた変更をプルし、`add-announcement-banner` ブランチを削除する

1. `main` ブランチから、以下の名前で新しいブランチを作成する

   ```txt
   enable-editing-announcements
   ```

1. チャットパネルを開き、**Agent mode**になっていることを確認します。以下のプロンプトを使用して、Copilotに新しいアナウンス機能のアップグレードを依頼します

   > 💡 **Tip**: The premium models (that use PRUs) are typically more robust and will require less, or no, followup prompts for refinement.プレミアムモデル（PRUを使用するもの）は一般的に強固であり(要するに賢い)、精緻化のためのフォローアッププロンプトが少なくて済むか、あるいは全く必要としません。

   > ![Static Badge](https://img.shields.io/badge/-Prompt-text?style=social&logo=github%20copilot)
   >
   > ```prompt
   > お知らせ機能はハードコードすべきではありません。
   >
   > - アナウンス情報をデータベースから取得するようにする
   > - ヘッダーにダイアログウィンドウを開くボタンを追加する。また既存のお知らせをすべて一覧表示し、追加・変更・削除の操作を行えるようにする
   > - サインインしたユーザーのみが、お知らせの管理にアクセスできるようにする
   > - お知らせの表示には有効期限を付ける。開始日の入力は任意入力とする
   > - データベースに初期値として、例となるお知らせメッセージを追加する
   > - 単体テストの実装はしない
   > - Make it pretty with a good UI/UX experience.ユーザーにとって優れたUI/UX体験になるよう、美しく仕上げる
   > ```

1. (optional) 変更内容を確認するためにアプリケーションを実行し、さらなる改善のためにCopilotにフォローアップのプロンプトを提供する

1. (optional) 変更内容をコミットする前に、VS Code上でローカルのレビューを実施する

1. 変更をコミットしプッシュする

1. 次のような内容で新しいプルリクエストを作成する

   - **compare:** `enable-editing-announcements`
   - **target:** `main`
   - **title:** `お知らせの編集を有効にする`

1. Copilotが自動的にレビュー担当者に追加されたことにご留意し、フィードバックを待つ

1. (optional) Copilotから提示されたコメントに対処する

1. プルリクエストをマージする

1. よくできました！これで終了となります 🎉
