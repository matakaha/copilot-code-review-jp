## Step 2: Pull Request Review を依頼する

さて、VS CodeでのCopilotのローカルレビュー機能を動作確認し、アクティビティサイトの改善変更を加えたので、プルリクエストの作成、メインブランチにマージする前に提案した変更に対するCopilotのフィードバックを得る段階です。他の教師が行うのと同様の手順です。プルリクエストプロセスにおける変更のレビュー方法をCopilotがどのように行うのか確認してみましょう。

### 📖 理論: Pull Request Code Reviews

GitHub Copilotはコードを分析し、即座に適用可能な実用的な提案を含むインテリジェントなフィードバックを提供します。各コードレビューはリクエスト元から1つの[プレミアムリクエストユニット（PRU:Premium Request Unit）](https://docs.github.com/en/copilot/concepts/billing/copilot-requests)を消費します。

> [!IMPORTANT]
> [Code review利用時の責任の所在](https://docs.github.com/en/copilot/responsible-use/code-review) - Copilotは多くの一般的なセキュリティ上の懸念事項に精通するよう訓練されています。しかし、専用のセキュリティツール、ガイドライン、標準に代わるものではありません。適切なツールを適切に使用してください。

**主な機能:**

- **自動分析**: コードの品質、セキュリティ、パフォーマンスの問題をレビューする
- **実施可能な提案**: コードの変更を伴う提案と共に具体的な推奨事項を提供する
- **インテグレーション**: GitHub上の一般的なプルリクエストワークフローとシームレスに統合されており、通常のピアコードレビューと同様に動作する
- **ノンブロッキング**: マージのブロックをすることもなく、マージ時に必要なコメント数にもカウントされないレビューコメントを提供する
- **カスタム可能**: チームの基準に沿うように指示内容をカスタムできる
- **セキュア**: GitHubが提供するセキュアなインフラ上で動作する

詳細については、[GitHub Copilot コードレビューのドキュメント](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/request-a-code-review)を参照してください。

### ⌨️ Activity: レビュー依頼

1. 必要に応じて、ブラウザで別のタブを開き、この演習リポジトリに移動してください。

1. 新しいプルリクエストを開始します。以下の詳細を入力し、**Create pull request**ボタンをクリックしてください。

   - **compare:** `add-announcement-banner`
   - **target:** `main`
   - **title:** `お知らせバナーを追加する`

1. 右側の詳細エリアで **Reviewers** メニューを探します。 **settings icon** をクリックして利用可能なレビュー担当者のリストを表示し **Copilot** を選択します。

   <img width="300" alt="screenshot of reviewers menu" src="https://github.com/user-attachments/assets/0f9f2e86-51b7-4542-82a1-afb6a22ab3ca"/>

1. Copilotが変更内容をレビューし、コメントを追記するまで待ちます。会話のログが追記されることに注視します。

   <img width="300" alt="new log entry - requested review from copilot" src="https://github.com/user-attachments/assets/3e522bda-e68e-4469-93f4-a7ad103cca97"/>

   <img width="500" alt="new log entry - copilot's PR summary" src="https://github.com/user-attachments/assets/0a870950-560e-4df8-80d5-2b93f1be99ab"/>

1. レビューをリクエストしたら、モナがあなたの作業を確認し、フィードバックを提供し、次のレッスンを共有するまでしばらくお待ちください。

<details>
<summary>Having trouble? 🤷</summary><br/>

- If Copilot doesn't appear in the reviewers list, ensure your repository has Copilot enabled
- If Copilot doesn't appear in the reviewers list, check your subscription plan. It is not available for free tier.
- Sometimes reviews take a minute or two to complete.

</details>
