# キーボードショートカット

プラグインが使用するすべてのショートカットを一箇所にまとめました。種類は 2 つあります。

- **IDE アクション** - IDE に登録され、メニューに表示され、<ui-path>Settings | Keymap</ui-path> で**再割り当て可能**です。それぞれに **Action ID** があります（ほとんどは `AzureDevOps` に一致し、ツールウィンドウのものはウィンドウ名に一致します）。
- **ビュー内キー** - 特定のビュー（コメントコンポーザー、プルリクエストのタイムライン、パイプラインの実行エディター）に組み込まれており、そのビューにフォーカスがある間のみ有効です。Keymap には含まれず、再割り当てできません。

> macOS では、<shortcut>⌘</shortcut> は Command、<shortcut>⌃</shortcut> は **Control** です。ほとんどのアクションは ⌘ を使いますが、一部は ⌃ を使います。Windows / Linux では <shortcut>Ctrl</shortcut> を使います。
> {style="note"}

## ツールウィンドウ

どこからでもプラグインのツールウィンドウを開く（またはフォーカスする）ことができます。これらは IDE 標準の **Activate tool window** アクションなので、<ui-path>Settings | Keymap</ui-path> で再割り当てできます（ウィンドウ名で検索してください）。

| アクション | macOS | Windows / Linux | Action ID |
|--------|-------|------------------|-----------|
| **Pull Requests** ツールウィンドウ | <shortcut>⌘⇧Y</shortcut> | <shortcut>Ctrl+Shift+Y</shortcut> | `ActivatePullRequestsWindowToolWindow` |
| **Pipelines** ツールウィンドウ | <shortcut>⌘⇧W</shortcut> | *最初の空き - ツールチップを参照* | `ActivatePipelinesWindowToolWindow` |

> **Pipelines** のショートカットは、パイプライン統合が有効な場合（<ui-path>Settings | Version Control | Azure DevOps</ui-path> → **Enable Pipelines integration**）にのみ機能します。有効でなければ開くツールウィンドウがありません。
> {style="note"}

> **macOS** では既定値は <shortcut>⌘⇧W</shortcut> です。これは 2025.2 と 2026.1 の両方で空いている数少ない ⌘⇧ の組み合わせの一つです（最新の IntelliJ はそのほとんどを占有しています。⌘⇧J は Database console、⌘⇧O は Go to File、⌘⇧K は Push、など）。**Windows / Linux** ではプラグインが代わりに最初の空きの組み合わせを選ぶため、異なることがあります。**Pipelines のストライプアイコンにカーソルを合わせると実際のキーが表示されます**。既定値を別の用途で使っている場合は、<ui-path>Settings | Keymap</ui-path> で Pipelines を再割り当てしてください（**Pipelines** で検索）。ショートカットは IDE 起動時にシードされるため、プラグインをインストール／更新した後は **IDE を完全に再起動する** 必要があります（プラグインのその場での再読み込みではシードされません）。また、再割り当ても同様に、再起動後にのみアイコンに表示されます。
> {style="tip"}

## エディター内（review-in-editor）

| アクション | macOS | Windows / Linux | Action ID |
|--------|-------|------------------|-----------|
| **Add Review Comment** | <shortcut>⌃⇧M</shortcut> | <shortcut>Ctrl+Shift+M</shortcut> | `AzureDevOps.PullRequest.AddCommentAtCursor` |
| **Copy Link to Code** | <shortcut>⌘⇧L</shortcut> | <shortcut>Ctrl+Shift+L</shortcut> | `AzureDevOps.PullRequest.CopyCodeLink` |

開いているプルリクエスト内のファイルの変更された行にキャレットがある場合にのみ発動します。[エディターでレビュー](Review-in-Editor-ja.md)を参照してください。

## 差分ビューアー内

| アクション | macOS | Windows / Linux | Action ID |
|--------|-------|------------------|-----------|
| **Mark File as Viewed** | <shortcut>⌘⇧S</shortcut> | <shortcut>Ctrl+Shift+S</shortcut> | `AzureDevOps.PullRequest.MarkFileAsViewed` |
| **Add Review Comment** | <shortcut>⌃⇧M</shortcut> | <shortcut>Ctrl+Shift+M</shortcut> | `AzureDevOps.PullRequest.AddCommentAtCursor` |
| **Copy Link to Code** | <shortcut>⌘⇧L</shortcut> | <shortcut>Ctrl+Shift+L</shortcut> | `AzureDevOps.PullRequest.CopyCodeLink` |
| 次 / 前の変更範囲 | <shortcut>F7</shortcut> / <shortcut>⇧F7</shortcut> | <shortcut>F7</shortcut> / <shortcut>Shift+F7</shortcut> | *IntelliJ 組み込みの差分* |

## コメントコンポーザー内

これらはコメント、返信、またはプルリクエスト説明のエディターにフォーカスがある間に機能します。コンポーザーに組み込まれており（Keymap にはありません）、修飾キーを除けばすべてのプラットフォームで同一です。

| アクション | macOS | Windows / Linux |
|--------|-------|------------------|
| **Bold** | <shortcut>⌘B</shortcut> | <shortcut>Ctrl+B</shortcut> |
| **Italic** | <shortcut>⌘I</shortcut> | <shortcut>Ctrl+I</shortcut> |
| **Inline code** | <shortcut>⌘E</shortcut> | <shortcut>Ctrl+E</shortcut> |
| **Insert link** | <shortcut>⌘K</shortcut> | <shortcut>Ctrl+K</shortcut> |
| **Mention user**（`@`） | <shortcut>⇧⌘M</shortcut> | <shortcut>Ctrl+Shift+M</shortcut> |
| **Bulleted list** | <shortcut>⇧⌘8</shortcut> | <shortcut>Ctrl+Shift+8</shortcut> |
| **Numbered list** | <shortcut>⇧⌘7</shortcut> | <shortcut>Ctrl+Shift+7</shortcut> |
| **Task list** | <shortcut>⇧⌘9</shortcut> | <shortcut>Ctrl+Shift+9</shortcut> |
| **Paste image** | <shortcut>⌘V</shortcut> | <shortcut>Ctrl+V</shortcut> |
| **Submit**（Comment / Reply / Save） | <shortcut>⌘↵</shortcut> | <shortcut>Ctrl+Enter</shortcut> |
| **Cancel / close editor** | <shortcut>⎋</shortcut> | <shortcut>Esc</shortcut> |

> よく似た 2 つのショートカットですが、役割は異なります。**Mention user**（<shortcut>⇧⌘M</shortcut>）はコンポーザー内に `@mention` を*挿入*し、**Add Review Comment**（<shortcut>⌃⇧M</shortcut>）はエディターまたは差分のキャレット位置で新しいコメントを*開始*します。
> {style="note"}

## プルリクエストの一覧、タイムライン、詳細ビュー内

| アクション | ショートカット | Action ID |
|--------|----------|-----------|
| **Refresh List** | <shortcut>⌘R</shortcut> / <shortcut>Ctrl+R</shortcut> / <shortcut>F5</shortcut> | `AzureDevOps.PullRequest.List.Reload` |
| **Refresh Timeline** | <shortcut>F5</shortcut> | `AzureDevOps.PullRequest.Timeline.Update` |
| **Refresh Pull Request** | <shortcut>F5</shortcut> | `AzureDevOps.PullRequest.Details.Reload` |
| **View Pull Request** | <shortcut>↵ Enter</shortcut> / ダブルクリック *（一覧内）* | `AzureDevOps.PullRequest.Show` |
| **View Pull Request in Browser** | *既定なし* | `AzureDevOps.PullRequest.Open.Link` |
| **Copy Pull Request URL** | *既定なし* | `AzureDevOps.PullRequest.Copy.Link` |
| **Show in Tool Window** | *既定なし* | `AzureDevOps.Pull.Request.Show.In.Toolwindow` |

> Pull Requests ツールウィンドウには Reload ボタンがありません。更新はキーボードのみ（または右クリック → **Refresh List**）です。
> {style="note"}

## プルリクエストのタイムライン内

これらのキーは **View Timeline** エディターを操作し、そのエディターにフォーカスがある間に発動します。コンポーザーのキーと同様に組み込みで（Keymap にはありません）。いつでも <shortcut>?</shortcut> を押すと同じ一覧が表示されます。

| アクション | ショートカット |
|--------|----------|
| **次の未解決スレッド** | <shortcut>F8</shortcut> / <shortcut>J</shortcut> |
| **前の未解決スレッド** | <shortcut>⇧F8</shortcut> / <shortcut>K</shortcut> |
| フォーカス中のスレッドを **解決 / 再オープン** | <shortcut>R</shortcut> |
| フォーカス中のスレッドに **返信** | <shortcut>A</shortcut> |
| **新しいコメントを開始** | <shortcut>C</shortcut> |
| 解決済みスレッドを **折りたたむ / 表示** | <shortcut>H</shortcut> |
| **AI レビューコメントを表示** | <shortcut>I</shortcut> |
| **タイムライン内を検索** | <shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> |
| **この一覧を表示** | <shortcut>?</shortcut> |

> **AI レビューコメントを表示**（<shortcut>I</shortcut>）は、最初の AI 提案の位置で差分にジャンプします。AI レビューコメントは差分のインレイとして表示され、インレイ自身の矢印で残りを順に移動できます。事前に AI レビューが実行されている必要があります。[AI 機能](AI-Features-ja.md)を参照してください。
> {style="tip"}

## パイプラインの実行エディター内

実行の概要（**Pipelines** ツールウィンドウから開きます）には独自のキーがあり、<shortcut>?</shortcut> またはステージグラフのツールバーの **?** ボタンでいつでも表示できます。組み込みで、Keymap にはありません。パイプライン統合が有効である必要があります。

| アクション | ショートカット |
|--------|----------|
| **ログを表示 / ステージグラフに戻る** | <shortcut>L</shortcut> |
| **前 / 次のタブ** | <shortcut>[</shortcut> / <shortcut>]</shortcut> |
| ステージグラフを **拡大 / 縮小 / フィット** | <shortcut>=</shortcut> / <shortcut>-</shortcut> / <shortcut>0</shortcut> |
| **この実行をブラウザーで開く** | <shortcut>B</shortcut> |
| **テストを絞り込む**（Tests タブ） | <shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> |
| **この一覧を表示** | <shortcut>?</shortcut> |

> ジョブの **logs** 内では、<shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> は代わりにログ検索バーを開きます（すべてのステップを横断して検索）。
> {style="note"}

## ブランチウィジェット / VCS メニュー

| アクション | ショートカット | Action ID |
|--------|----------|-----------|
| **Open Current Branch PR** | *既定なし* | `AzureDevOps.OpenCurrentBranchPr` |
| **Update Pull Request Branch** | *既定なし* | `AzureDevOps.Pull.Request.Branch.Update` |
| **Review in Editor** | *既定なし* | `AzureDevOps.Pull.Request.Review.In.Editor.Toggle` |
| **Go to Pull Requests…** | <shortcut>⌘⇧P</shortcut> / <shortcut>Ctrl+Shift+P</shortcut> | `AzureDevOps.PullRequest.GoTo` |

> **Shift** を 2 回（<shortcut>⇧⇧</shortcut>）押すと IDE の *Search Everywhere* が開き、そこで Azure DevOps のプルリクエストが専用の **Pull Requests** タブに表示されます。これは **Go to Pull Requests…** が既定で開くのと同じタブです。[プルリクエスト](Pull-Requests-ja.md#jump-to-a-specific-pr)を参照してください。
> {style="tip"}

## AI アクション

| アクション | ショートカット | Action ID |
|--------|----------|-----------|
| **Summarize Pull Request** | *既定なし* | `AzureDevOps.PullRequest.AI.Summarize` |
| **Run AI Review** | *既定なし* | `AzureDevOps.PullRequest.AI.Review` |
| **Explain This File** | *既定なし* | `AzureDevOps.PullRequest.AI.Explain` |
| **Generate Commit Message with AI** | *既定なし* | `AzureDevOps.AI.GenerateCommitMessage` |

これらには AI プロバイダーの設定が必要です。[AI 機能](AI-Features-ja.md)を参照してください。

## 再割り当ての方法 {id="rebind"}

上記のうち **IDE アクション**（Action ID があるもの）のみが再割り当てできます。**ビュー内キー**（コメントコンポーザー、プルリクエストのタイムライン、パイプラインの実行エディター）は固定です。

<procedure title="ショートカットを割り当てる">
    <step><ui-path>Settings | Keymap</ui-path> を開きます。</step>
    <step>検索ボックスに <code>AzureDevOps</code> と入力してプラグインのアクションに絞り込みます（表示名だけでなく action ID にも一致します）。</step>
    <step>アクションをダブルクリック → <b>Add Keyboard Shortcut</b>。</step>
    <step>組み合わせを押します。競合する場合は IntelliJ が警告し、競合を削除するよう提案します。</step>
    <step><b>OK</b> をクリックします。</step>
</procedure>

> 2 つの **ツールウィンドウ** のショートカットも IDE アクションですが、その ID（`ActivatePullRequestsWindowToolWindow` / `ActivatePipelinesWindowToolWindow`）には `AzureDevOps` が含まれていません。**Pull Requests** または **Pipelines** で検索して見つけ、再割り当てしてください。
> {style="note"}

> バグを報告する際は **action ID** の列を使用してください。表示名がバージョンによって異なる場合があっても、IDE のバージョンを越えて正確なアクションを特定できます。
> {style="tip"}
