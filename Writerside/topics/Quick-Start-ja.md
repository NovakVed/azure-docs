# クイックスタート

ゼロから最初のプルリクエストのレビューまで、およそ1分で完了します。このページでは、プラグインを既に[インストール](Installation-ja.md)していることを前提としています。

## 1. Azure DevOps でホストされているプロジェクトを開く

Azure DevOps のリポジトリを通常どおりクローンします:

```bash
git clone https://dev.azure.com/your-org/your-project/_git/your-repo
cd your-repo
```

そのフォルダーを IDE で開きます。プラグインは起動時に Git リモートをスキャンし、`dev.azure.com` または `*.visualstudio.com` のリモートを検出すると有効化され、**Pull Requests** ツールウィンドウを表示します。

> **ツールウィンドウが表示されない場合** プラグインは Azure DevOps のリモートが検出されないときは自身を非表示にします。`git remote -v` を実行して、リモート URL に `dev.azure.com` が含まれていることを確認してください。
> {style="note"}

## 2. サインインする

左サイドバーから Pull Requests ツールウィンドウを開きます。そのサインイン画面には2つの選択肢があります:

- **Log In with Token…**（トークンでログイン） Azure DevOps のユーザー設定から取得した個人用アクセス トークンを貼り付けます。最も速い方法であり、オンプレミスの Azure DevOps Server では唯一の選択肢です。
- **Log In via Microsoft…**（Microsoft 経由でログイン） Microsoft Entra ID を介したブラウザーベースの OAuth サインインです（クラウドの `dev.azure.com` のみ）。最初にダイアログで **Full access** と **Standard access** のどちらを付与するかを尋ねられます。

![Full access（推奨）と Standard access を示す、Sign in with Microsoft の権限選択画面](oauth-scope-dialog.png){ width="520" border-effect="line" }

トークンを選択する場合、プラグインには次のスコープが必要です: **Code (Read &amp; write + Status), User Profile (Read), Identity (Read), Work Items (Read), Security (Manage)**。ログイン ダイアログにこれらが一覧表示され、その **Generate…** ボタンを押すと、組織のトークン ページがブラウザーで開きます。

> サインインの完全なフロー、スコープ、Full と Standard のティア選択については、[認証](Authentication-ja.md)を参照してください。
> {style="note"}

## 3. プルリクエストを閲覧する

サインインすると、ツールウィンドウにリポジトリのプルリクエストが一覧表示されます。

![検索フィールド、フィルターチップ、および入力済みのリストを備えた Pull Requests ツールウィンドウ](pr-tool-window.png){ width="720" border-effect="line" }

リストを絞り込むには:

- **Quick Filters**（クイックフィルター） チップ行の左にあるフィルターアイコンをクリックすると、ワンクリックのプリセットが使えます: **Open pull requests**、**Awaiting my review**、**Involving me**。
- **フィルターチップ** **State**（Active / Completed / Abandoned）、**Author**、**Tags**、**Assignee**、**Review**（自分の投票状態）、**Work Items**、**Draft**。
- **Sort**（並べ替え） 最後のチップ: Newest、Oldest、Most/Least commented、または Recently/Least recently updated。
- **Search**（検索） チップの上のフィールドに入力すると、PR のタイトルと説明に一致します。

任意の PR を**クリック**すると、エディタータブでその詳細ビューが開きます。

> **PR が表示されない場合** よくある原因: (1) お使いのアカウントがこのリポジトリにアクセスできない — まず Azure DevOps の Web UI で開いてください。(2) プロジェクトが複数の組織を指している — ツールウィンドウの歯車アイコン → **Switch Account / Repository…** で切り替えてください。(3) 実際にアクティブな PR が存在しない — **State** チップを **Completed** に設定して、接続が機能していることを確認してください。
> {style="note"}

## 4. コードをレビューする

詳細ビューは**単一のペイン**で、サブタブはありません。上から下へ: `!` 番号付きのタイトルと **View Timeline** リンク、ソース → ターゲットのブランチ、各レビュアーの投票を含むステータスチェック、変更されたファイルのツリー、そしてアクションバー。

![単一ペインの詳細ビューで開かれたプルリクエスト](pr-detail.png){ width="720" border-effect="line" }

- **差分を読む** 変更ツリー内の任意のファイルをクリックすると差分が開きます。行のガター（余白）をクリックするとコメントできます。
- **ディスカッションを読む** **View Timeline** をクリックすると、コメントの全タイムラインが専用のタブで開きます。
- **投票する** アクションバーの **Approve** ボタンは分割ボタンです。そのドロップダウンには **Approve with suggestions**、**Wait for author**、**Reject**、**Reset feedback** が含まれます。

![投票オプションを展開した Approve 分割ボタン](vote-approve-dropdown.png){ width="380" border-effect="line" }

> **エディターを離れずにレビューする:** PR のブランチをチェックアウトすると、プラグインが通常のエディター上にそのコメントを直接オーバーレイ表示します。[エディター内レビュー](Review-in-Editor-ja.md)を参照してください。
> {style="tip"}

## 5. プルリクエストを作成する

ツールウィンドウのツールバーから **+**（Create Pull Request）をクリックします。フォームには、ソースブランチ（現在のブランチ）とデフォルトのターゲットブランチが事前入力されます。タイトル、説明、レビュアーを追加してから作成します。

![AI が生成したタイトルと説明を使ったプルリクエストの作成](create-pr-ai.png){ width="640" border-effect="line" }

> **AI によるタイトルと説明の支援:** [AI プロバイダーを構成](AI-Features-ja.md)しておくと、フォームのタイトルと説明フィールドに **Generate** アクションが追加され、ブランチの差分から両方を下書きします。
> {style="tip"}

## 次に見るべきページ

- [プルリクエスト](Pull-Requests-ja.md) フィルタリング、検索、アクションバー、オーバーフローメニュー（Complete、Revert、Compare）。
- [コードレビュー](Code-Review-ja.md) インライン差分、提案、投票、ファイル閲覧状態の追跡。
- [通知とアテンション](Notifications-and-Attention-ja.md) PR が自分のレビューを必要とするときや @メンションされたときに通知を受け取ります。
- [AI 機能](AI-Features-ja.md) 要約、AI レビュー、文法の校正。
