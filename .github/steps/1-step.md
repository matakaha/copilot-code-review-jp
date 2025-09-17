## Step 1: VS Code でレビューを依頼する

マージントン高校には課外活動専用ウェブサイトがあります。ここ数か月で多くの機能が追加され、教職員や生徒の間で利用がますます広がっています。

現在、さまざまな教師が新機能の開発を手伝いたいと思っています。これはありがたいことですが、あなたの時間とパワーには限界があり、変更点をレビューする時間がなければ、アプリケーション開発が混乱するのではないかと懸念しています。あなたの "レビュー" 対応力を向上させるため、**GitHub Copilot code review** を導入しましょう！

Copilotによる自動コードレビューを導入する前に、VS Codeでローカルレビューを試すのが合理的です。これにより、Copilotの理解を深めレビュー基準を構築し、協力してくれる教師たちが貢献を開始した際に、一貫したフィードバックを確実に受け取れるようになります。

### 📖 理論：GitHub Copilot ローカルコードレビュー

GitHub CopilotはVS Code内で直接コードをレビューし、コミット前の変更に対して即座にフィードバックを提供します。プルリクエストのフィードバックに似たコメントを追加することさえ可能です！このローカルレビュー機能により、開発者はバージョン管理に到達する前に問題を発見でき、最初からコード品質を向上させられます。そして、恥ずかしいタイプミスも発見できるかもしれません！ 😅

**主な機能:**

- コミットされていない変更の **ローカル解析**
- **コードの品質とスタイル** に関する推奨事項
- 一般的なセキュリティ脆弱性の **検出**
- **パフォーマンス最適化** の提案

この即時フィードバックにより、開発プロセスの早い段階で問題を特定・修正できるため、プルリクエストに到達する前にコードの堅牢性を高めることができます。

## ⌨️ Activity: 課外活動サイトについて知ろう

開発とレビューを始める前に、現在の課外活動サイトについて理解を深めましょう。

1. 以下のボタンを右クリックして、新しいタブで **Create Codespace** ページを開きます。デフォルトの設定を使用してください

   [![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/{{full_repo_name}}?quickstart=1)

1. 環境準備が始まりますのでしばらくお待ちください。必要なすべてのサービスなどが自動的にインストールされます

1. **GitHub Copilot** および **Python** 拡張機能がインストールされ、有効化されていることを確認してください

   <img width="300" alt="copilot extension for VS Code" src="https://github.com/user-attachments/assets/ef1ef984-17fc-4b20-a9a6-65a866def468" /><br/>
   <img width="300" alt="python extension for VS Code" src="https://github.com/user-attachments/assets/3040c0f5-1658-47e2-a439-20504a384f77" />

1. アプリケーションを実行してみてください。左サイドバーで**実行とデバッグ**タブを選択し、**デバッグの開始**アイコンを押してください

   <img width="300" alt="run and debug" src="https://github.com/user-attachments/assets/50b27f2a-5eab-4827-9343-ab5bce62357e" />

   Python Debuggerを求められる場合もあります。その際はインストールしてください。

   <img width="300" alt="Python Debugger extension for VS Code" src="https://github.com/user-attachments/assets/0dc3a323-7649-4040-ae68-0533e194159a" />

   <details>
   <summary>🤷 Having trouble?</summary><br/>

   **実行とデバッグ** 領域が空の場合、VS Codeを再読み込みしてみてください：コマンドパレット（`Ctrl`+`Shift`+`P`）を開き、`Developer: Reload Window`を検索してください

   <img width="300" alt="empty run and debug panel" src="https://github.com/user-attachments/assets/0dbf1407-3a97-401a-a630-f462697082d6" />

   </details>

1. **ポート** タブを使用してウェブページのアドレスを見つけ、それを開き、動作していることを確認してください

   <img width="350" alt="ports tab" src="https://github.com/user-attachments/assets/8d24d6b5-202d-4109-8174-2f0d1e4d8d44" />

   ![Screenshot of Mergington High School WebApp](https://github.com/user-attachments/assets/5e1e7c1e-1b0e-4378-a5af-a266763e6544)

### ⌨️ Activity: Copilot にレビューを依頼する

教師が`お知らせ`を行うためのシンプルなバナー機能を追加し、その後Copilotにフィードバックを求めましょう。

1. VS Codeで次の名前の新しいブランチを作成します

   ```txt
   add-announcement-banner
   ```
   画面下部、`main`と記載のある部分をクリックすると画面上部にメニューが提示されます。`＋新しいブランチの作成`を選択し、`add-announcement-banner`と入力しEnterを押下します。
   
   <img width="400" alt="VS Code" src="https://github.com/user-attachments/assets/ea12fecd-db48-46ae-b761-1be73b26c7ed" />
   
   画面下部、`main`が`add-announcement-banner`になっていれば成功です。
   
   <img width="400" alt="VS Code" src="https://github.com/user-attachments/assets/8f1ccdf8-c560-44df-9e44-4555e24610c6" />


1. `src/static/index.html` ファイルを開きます。`<body>` タグのすぐ後に以下の内容を追加します

   ```html
   <div class="announcement-banner">
     📢 活動登録は今月末まで受け付けています。お早めに！
   </div>
   ```

1. `src/static/styles.css` ファイルを開きます。末尾に以下の内容を追加します
   ```css
   .announcement-banner {
     background-color: #4caf50;
     color: white;
     text-align: center;
     padding: 15px;
     font-weight: bold;
   }
   ```

1. (optional) 変更を確認するには、実行中のアプリを再読み込みしてください

   <img width="400" alt="screenshot of site with announcement banner" src="https://github.com/user-attachments/assets/39de7fe0-58f2-4eba-a163-d3037b2b3b06"/>

1. VS Code でソース管理パネルを開き、すべての変更が保存されてることを確認してください

1. ソース管理タブの **変更** セクションにカーソルを合わせると、さまざまなアイコンが表示されます。**Code Review**ボタンをクリックし、Copilotがコメントを追加するまでしばらくお待ちください

   <img width="300" alt="screenshot of site with announcement banner" src="https://github.com/user-attachments/assets/6c52d550-d67b-4af9-99dd-e181695a4933"/>

   > 💡 **TIP:** 利用可能なレビューレベルは3つ提示されることがあります：`未ステージングの変更`、`ステージング済みの変更`、`未コミットの変更`

1. **コメント**パネルを展開すると、Copilotからのレビューフィードバックの一覧が表示されます

   <img width="300" alt="screenshot of problems control panel with comments from Copilot" src="https://github.com/user-attachments/assets/64c5efb6-9071-4511-b2a2-2dc85c9e929b"/>

1. Copilot のフィードバックに対応するには、**適用(適用して次へ移動)** または **破棄(破棄して次へ移動)** ボタンを使用してください

   <img width="300" alt="screenshot of inline comment with buttons to address feedback" src="https://github.com/user-attachments/assets/aef73097-acaf-4f5b-a52f-52a142bb413f"/>

1. `add-announcement-banner` ブランチに、お知らせ関連の変更をコミットしてプッシュしてください。（コミットメッセージの生成ボタン（キラキラアイコン）をクリックし、Copilotにコミットメッセージを生成してもらいましょう）

1. 変更をプッシュしたら、モナが作業を確認し、フィードバックを提供し、次のレッスンを共有するまでしばらくお待ちください

<details>
<summary>Having trouble? 🤷</summary><br/>

- Copilot Review in VS Code only considers uncommitted changes. Don't commit before asking for the review.
- If Copilot doesn't provide review feedback, make sure to click the correct review button for the grouping (unstaged, staged, uncommitted).
- If Copilot doesn't see your changes, make sure to save the files first.

</details>
