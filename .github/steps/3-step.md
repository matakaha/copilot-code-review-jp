## Step 3: レビューのカスタマイズ

学校のコーディング規約は、課外活動ウェブサイト維持管理に欠かすことはできません。教師たちが作成するサイトのデザインやコーティングパターンがバラバラなことに気付いたとします。協力してくれる教師たちのプログラミングに関するバックグラウンドや優先事項は様々であることを念頭に、Copilotのレビュー動作をカスタマイズして、学校としてのプログラミング基準に沿うようにカスタマイズしましょう。

### 📖 Theory: リポジトリのカスタム指示

リポジトリのカスタム指示により、プロジェクトの標準や好みをCopilotに伝達できます。指示ファイルを作成することで、Copilotの提案がチーム方針に対し一貫性を保持し、特定の要件に集中するよう保証できます。プロジェクトを分析させ、[指示を生成](https://code.visualstudio.com/docs/copilot/customization/custom-instructions#_generate-an-instructions-file-for-your-workspace)させることも可能です！

**指示(Instruction)の種類 :**

- **リポジトリ全体に対する指示**: リポジトリ内のすべてのコードに適用されます。 例: `.github/copilot-instructions.md`
- **パス固有の指示**: 特定のファイルに適用し、コードベースの異なる部分に対して焦点を絞った規約を作成します。 例: `.github/instructions/NAME.instructions.md`.

説明文は自然言語で記述され、Markdown形式で書かれ、通常以下のような内容を含みます:

- セキュリティ要件とチェックリスト
- 標準的なコーディングと規約
- パフォーマンス最適化の優先順位
- チーム固有の設定とスタイルのガイド
- 言語固有のレビュー基準

パス固有の指示ファイルには、特定のファイルやディレクトリを対象とするファイル[glob patterns](https://code.visualstudio.com/docs/editor/glob-patterns)を含む[YAML front matter](https://docs.github.com/en/contributing/writing-for-github-docs/using-yaml-frontmatter)が含まれます。 例:

```yaml
---
applyTo: "tests/**/**,docs/*.md"
---
# テスト ガイドライン ...
```

```yaml
---
applyTo: "docs/*.md,README.md"
---
# ドキュメント ガイドライン ...
```

> [!TIP]
> リポジトリの[カスタム指示(custom instructions)](https://docs.github.com/en/copilot/how-tos/custom-instructions/adding-repository-custom-instructions-for-github-copilot)は、VS Code上のコードレビューとプルリクエストのコードレビューの両方で機能するため、開発ワークフロー全体で一貫性を確保します。

### ⌨️ Activity: リポジトリ全体に対する指示を追加する

カスタム指示(custom instructions)を追加して、Copilotが行うレビューの考慮事項をカスタマイズしましょう。

1. VS Codeで、`add-announcement-banner` ブランチにいることを確認してください

1. リポジトリの一般的なガイドラインに関するファイルを作成する

   ファイルのパスと名前:

   ```txt
   .github/copilot-instructions.md
   ```

   コンテンツ:

   ```markdown
   ## セキュリティ

   - 入力へのサニタイズ処理を検証する
   - ユーザーデータを危険にさらす可能性のあるリスクを検索する
   - 設定とコンテンツは、ハードコードされた内容ではなくデータベースから読み込むことを推奨します。どうしても必要な場合は、環境変数またはコミットされていない設定ファイルから読み込んでください。

   ## コードの品質

   - 一貫した命名規則を使用する
   - 重複するコードを減らすように努める
   - 最適化よりも保守性と可読性を優先する
   - メソッドが頻繁に使用される場合は、パフォーマンス向上のために最適化を試みる
   - サイレント障害(silent failures)を失くし、明示的なエラー処理をするように努める
   ```

### ⌨️ Activity: 焦点を絞った指示を追加する

フロントエンドおよびバックエンド向けに、Copilotのレビューに関する具体的な考慮事項を作成しましょう。

1. フロントエンド用のガイドラインを記述するファイルを作成する

   > ❗️ **Important**: ファイル固有の指示は必ず `.github/instructions/` フォルダに配置し、`.github/` フォルダには配置しないでください

   ファイルのパスと名前:

   ```txt
   .github/instructions/frontend.instructions.md
   ```

   コンテンツ:

   ```markdown
   ---
   applyTo: "*.html,*.css,*.js"
   ---

   ## フロントエンド ガイドライン

   - accessibility attributes(alt text, aria labels)とcolor schemeを使用する
   - モバイルデバイスにおける互換性確保を目的として、レスポンシブデザインを使用する
   - HTML構造とsemantic elementを検証する
   ```

1. バックエンド用のガイドラインを記述するファイルを作成する

   ファイルのパスと名前:

   ```txt
   .github/instructions/backend.instructions.md
   ```

   コンテンツ:

   ```markdown
   ---
   applyTo: "backend/**/*,*.py"
   ---

   ## バックエンド ガイドライン

   - すべてのAPIエンドポイントは`routers`フォルダ内に定義する
   - `database.py`ファイルからサンプルデータベースの内容を読み込む
   - エラー処理はサーバー側でのみログ記録する。フロントエンドへ伝播させない
   - すべてのAPIがドキュメントで説明されていることを確認する
   - バックエンドの変更がフロントエンド（`src/static/**`）に反映されていることを確認する。可能であれば、互換性を損なう変更が見つかった場合、開発者にその旨を伝える
   ```

1. 指示(Instraction)を記載したすべてのファイルをCommitしPushする

> [!TIP]
> VS Codeには、指示を管理するのに役立つ組み込みコマンドがあります。コマンドパレット(`Ctrl`+`Shift`+`P`)を開き、`instructions` を検索してみてください。

### ⌨️ Activity: 再レビューを依頼する

新しい指示を定義したことで、Copilotはプロジェクトにとって何が重要かをより理解できるようになりました。それでは、再度レビューを依頼しましょう。

1. VS Codeで、指示が実際にコミットされ、リポジトリにプッシュされていることを確認する

1. ブラウザで、先ほど作成したプルリクエストに戻る

1. 右上の**Reviewers**メニューと、**Copilot**の横にある**Re-request review**ボタンを探してください。クリックすると、Copilotがプルリクエストにコメントを追加するまでしばらく待ちます

   <img width="300" alt="screenshot of re-review button" src="https://github.com/user-attachments/assets/c45aa8de-278d-46e7-bfe2-2dc6b574e11e"/>

   > 🪧 **Note:** 新しいコミットをプッシュした後、すぐに操作すると、ボタンが表示されるまで少し待つ必要があります。しばらく待っても表示が変更されない場合は、ページを更新してください。

1. Copilotのフィードバックが前回のレビューコメントとは異なることを注視してください

1. レビューをリクエストしたら、モナがあなたの作業を確認し、フィードバックを提供し、次のレッスンを共有するまでしばらくお待ちください

<details>
<summary>Having trouble? 🤷</summary><br/>

- If you forgot to add a custom instruction (or made a typo), try fixing the mistake and asking Copilot for another review. This will inform Mona to check your work again.

</details>
