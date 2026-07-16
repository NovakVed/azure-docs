# プルリクエスト

**Pull Requests** ツールウィンドウは、あなたの司令塔です。キューを閲覧し、フィルタリングと検索を行い、PR を開いて操作します（完了、取り消し、比較など）。

## ツールウィンドウを開く

ツールウィンドウは、開いているプロジェクトに Azure DevOps の Git リモートが 1 つ以上ある場合に、左サイドバーに表示されます。（Azure DevOps リモートがない場合は、煩雑さを避けるために非表示のままになります。）

- サイドバーの **Pull Requests** ストライプアイコンをクリックします。
- または <ui-path>View | Tool Windows | Pull Requests</ui-path> を使用します。
- または *Find Action*（<shortcut>⌘⇧A</shortcut> / <shortcut>Ctrl+Shift+A</shortcut>）を実行して **Pull Requests** と入力します。

![検索フィールド、フィルターチップ、および項目が並んだリストを備えた Pull Requests ツールウィンドウ](pr-tool-window.png){ width="720" border-effect="line" }

## プルリクエストを探す

### デフォルトビュー: 自分のもの

フィルターが有効になっていない状態では、リストには Azure DevOps Web の **Mine** タブに表示されるものとまったく同じ内容が表示されます。つまり、あなたが**作成した**、**あなたに割り当てられた**、または**あなたのチームのいずれかに割り当てられた**アクティブな PR です。これは最初に表示されるビューであり、*Clear filters* で戻ってくるビューです。

いずれかのチップ、プリセット、または検索を選ぶと、リストは全体のセットに切り替わります。それらをクリアすると、自分のものに戻ります。

> チームに割り当てられた PR には適切な[権限](Permissions-ja.md)が必要です。資格情報でチームメンバーシップを読み取れない場合、プラグインは一度だけ通知します。ビューの残りの部分は引き続き動作します。
> {style="note"}

### Quick Filters

チップ行の左にある**フィルターアイコン**をクリックすると、ワンクリックのプリセットが表示されます。アイコン上のバッジは、有効なフィルターの数を示します。

![プリセットが並んだ Quick Filters メニュー](quick-filters-menu.png){ width="380" border-effect="line" }

| プリセット | 表示内容 |
|--------|-------|
| **All pull requests** | すべて - デフォルトの「自分のもの」ビューからの脱出口 |
| **Open pull requests** | すべてのアクティブな PR |
| **Awaiting my review** | あなたがレビュアーであり、まだ投票していない PR |
| **Involving me** | あなたが作成した、レビューする、またはメンションされた PR |
| **Clear N filter(s)** | 有効なすべてのフィルターをリセット - デフォルトの「自分のもの」ビューに戻る |

### フィルターチップ

検索フィールドの下に、スクロール可能なチップの行があります。いずれかのチップをクリックしてリストを絞り込みます。

| チップ | オプション |
|------|---------|
| **State** | Active · Completed · Abandoned |
| **Author** | ユーザー全体を対象とした先行入力検索 |
| **Tags** | Azure DevOps PR ラベル（タグ） |
| **Assignee** | ユーザー全体を対象とした先行入力検索 |
| **Review** | Approved · Approved with suggestions · Waiting for author · Rejected · Awaiting my review |
| **Work Items** | リンクされた Azure Boards の作業項目 |
| **Draft** | ドラフトのみ · ドラフト以外のみ |
| **Sort** | Newest · Oldest · Most/Least commented · Recently/Least recently updated |

フィルターは、IDE の再起動をまたいで**プロジェクトごとに**保持されます。クリアするには、Quick Filters メニューの **Clear N filter(s)** を使用します。

> **検索** - チップの上にあるフィールドに入力すると、PR のタイトル、番号、作成者、およびブランチ名に一致します。<shortcut>⇧ Shift</shortcut> を 2 回押すと *Search Everywhere* が開き、そこには Azure DevOps の PR も表示されます。いずれかを選択すると直接開きます。
> {style="tip"}

### 特定の PR にジャンプする

どの PR が必要かすでにわかっている場合は、リストをスキップできます。**Go to Pull Requests…** は、キャッシュされたすべての PR を **id、タイトル、作成者、またはリポジトリ**であいまい検索し、そのタイムラインを直接開きます。検索を空にすると、キャッシュされたすべての PR が一覧表示されます（未読を先に、次に新しい順）。

- <shortcut>⌘⇧P</shortcut> / <shortcut>Ctrl+Shift+P</shortcut> を押します。
- または <ui-path>VCS | Go to Pull Requests…</ui-path> を使用します。
- または *Find Action*（<shortcut>⌘⇧A</shortcut> / <shortcut>Ctrl+Shift+A</shortcut>）を実行して **Go to Pull Requests** と入力します。

デフォルトでは、IDE の *Search Everywhere* ポップアップ内に、Files、Symbols、Actions の隣に **Pull Requests** タブを開きます。<shortcut>↵ Enter</shortcut> を押すと、ハイライトされた PR が開きます。

![Go to Pull Requests の結果: Search Everywhere 内の Pull Requests タブ](go-to-pr-popup.png){ width="560" border-effect="line" }

> 専用のダイアログのほうがよいですか？ [Settings](Settings-ja.md) で **Show in the Search Everywhere window** を**オフ**にすると、このアクションは代わりに独自のクイックピックポップアップを開きます。検索フィールドとその横にステータス**ファネル**があり、<shortcut>↵</shortcut> で開く / <shortcut>⎋</shortcut> で閉じるキーが使えます。
> {style="tip"}

## PR 行を読む

各行には、ひと目でわかるステータスが詰め込まれています。

![プルリクエスト行の構成](pr-row-anatomy.png){ width="640" border-effect="line" }

- **タイトルと `!` 番号**。関連する場合は**ステータスピル**が付きます: *Draft*、*Merged*、*Abandoned*、または *Has merge conflicts*。
- **レビュアーの投票アイコン** - 承認、提案付き承認、待機、または却下。
- スレッド数（およびそのうち未解決がいくつあるか）を示す**アンバー色のディスカッションバッジ**。
- **アテンションチップ** - *Review requested*、*Mentions you*、または *Replied* - PR があなたの注意を求めているときに表示されます。これらはデフォルトでオフです。オンにするには [Notifications &amp; Attention](Notifications-and-Attention-ja.md) を参照してください。

未読の PR には、新しいコミット*および*新しいコメント活動に反応する青い**未読マーカー**ドットが表示されることがあります。これはツールウィンドウの歯車 → **Show unread markers** で切り替えられます。

## PR を開いて操作する

PR を**クリック**すると、エディタタブに単一ペインの詳細ビューが開きます。下部のアクションバーは、あなたの役割に応じて変化します。

| あなたの役割… | 主なアクション |
|----------|-----------------|
| **Reviewer** | **Approve ▾**（分割ボタン: Approve with suggestions、Wait for author、Reject、Reset feedback） |
| **Author, needs review** | **Request review** |
| **Author, reviews in** | **Complete ▾**（Set auto-complete…、Mark as draft、Abandon） |
| **Not involved** | **Set myself as reviewer** |

どの状態でも、アクションセット全体を含む **⋮**（More）メニューが表示されます。

![PR アクションバーのオーバーフローメニュー](pr-overflow-menu.png){ width="440" border-effect="line" }

| アクション | 動作 |
|--------|--------------|
| **Share Pull Request…** | PR をメールで人に送る（レビュアーは追加されず、コメントも投稿されません） |
| **Submit Pending Comments (N)** | キューに入れたコメントをレビューとして投稿する（N > 0 のときのみ） |
| **Restart Merge** | 停止したマージを再キューする（コンフリクト / 失敗 / ポリシー却下） |
| **Change Target Branch…** | PR を別のターゲットブランチに向け直す |
| **Cherry-Pick…** | この PR のコミットを別のブランチにチェリーピックしたブランチを作成する |
| **Review Changes Since…** | 選択した更新以降に変更された内容に差分を再スコープする - [Code Review](Code-Review-ja.md#compare) を参照 |
| **Revert…** | *（マージ済みの PR）* この PR の変更を取り消すブランチを作成する |
| **Open on Web** · **Copy Link** | dev.azure.com の URL に移動 / コピーする |
| **Summarize Pull Request** · **Run AI Review** | [AI アシスト](AI-Features-ja.md) |

### プルリクエストを完了する

**Complete** をクリックすると、**Complete Pull Request** ダイアログが開きます。**Merge type** を選択します。ライブ図が、結果として得られる履歴の形状を示します。

![マージ戦略の図が付いた Complete Pull Request ダイアログ](complete-pr-dialog.png){ width="560" border-effect="line" }

- **Merge (no fast forward)** · **Squash commit** · **Rebase and fast-forward** · **Semi-linear merge**
- **完了後のオプション:** 関連する作業項目を完了する、ソースブランチを削除する、そして必要に応じてマージコミットメッセージをカスタマイズします。

> **ブランチポリシーは尊重されます。** 必須のレビュアーやステータスチェックが満たされていない場合、ダイアログはブロッカーを一覧表示します。バイパス権限を持っている場合にのみ、**Override branch policies and enable merge**（理由の入力が必須）が利用できます。
> {style="warning"}

行を右クリックすると、クイックアクションも使えます: **View Pull Request**、**View Pull Request in Browser**、**Copy Pull Request URL**、および **Refresh List**。

## プルリクエストを作成する

ツールウィンドウのツールバーで **+**（Create Pull Request）をクリックします。フォームには、ソースブランチ（現在のブランチ）とデフォルトのターゲットブランチが事前入力されます。

![Create Pull Request フォーム: Write/Preview の説明コンポーザーと、レビュアー、タグ、作業項目の行](create-pr-ai.png){ width="640" border-effect="line" }

**説明**は、PR コメントと同じコンポーザーを使用します。**Write | Preview** のタブストリップがあり、エディタの上に書式設定ツールバーがあります。`@`、`#`、または `!` を入力すると、人、作業項目、PR のインライン補完が表示されます。<shortcut>⌘↵</shortcut> / <shortcut>Ctrl+Enter</shortcut> を押すと作成します。

説明の下にあるメタデータブロックは、4 つのインライン行です。それぞれに編集用の鉛筆があり、表示されている場合はクリア用の **X** があります。

| 行 | 設定する内容 |
|-----|--------------|
| **Required reviewers** | レビューしなければならない人 |
| **Optional reviewers** | レビューに招待された人 |
| **Tags** | Azure DevOps PR ラベル - 既存のものを選ぶか、**+** を使ってまったく新しいタグを作成します |
| **Work items** | リンクされた Azure Boards の作業項目 |

プライマリボタンは分割ボタンです: **Create Pull Request**。ドロップダウンには **Create Draft Pull Request** があります。

> [AI を有効にする](AI-Features-ja.md)と、説明コンポーザーのツールバーに AI ボタン（ツールチップ **Generate title &amp; description with AI**）が追加され、ブランチのコミットからタイトルと説明を下書きします。AI プロバイダーがまだ設定されていない場合、クリックすると AI Settings を開くよう促されます。
> {style="tip"}

## 更新とバックグラウンド同期

Azure DevOps には Webhook がないため、プラグインはポーリングします。リストは自動的に更新されますが、オンデマンドで更新することもできます。

- ツールウィンドウにフォーカスがある状態で <shortcut>⌘R</shortcut> / <shortcut>Ctrl+R</shortcut> または <shortcut>F5</shortcut> を押します。
- または行を右クリック → **Refresh List**。

> ポーリングの間隔は [Settings](Settings-ja.md) の **Sync interval** です（デフォルトは 60 秒）。コールドスタート時には、最初の同期が実行される間、リストは**最後に判明したキャッシュ状態**を表示するため、スピナーを待つ代わりにすぐに操作できます。
> {style="note"}

## アカウントまたはリポジトリを切り替える

複数の組織やリポジトリにバインドされているプロジェクトの場合は、ツールウィンドウの歯車 → **Switch Account / Repository…** を使用します。現在のブランチの PR は、Git ブランチウィジェットとステータスバーにも表示されます - [Git Integration](Git-Integration-ja.md) を参照してください。
