# ディスカッションとコメント

IDE を離れることなく、プルリクエストで本格的な会話ができます。markdown エディター、@メンション、作業項目やプルリクエストへの参照、変更の提案、画像の添付、AI による文法調整、スレッドの解決に対応しています。

## スレッドが表示される場所

同じスレッドが 3 か所に表示されます。

- **差分内のインライン** - 参照している行にアンカーされます。[コードレビュー](Code-Review-ja.md)を参照してください。
- **タイムライン** - すべてのスレッドとプルリクエストのイベントを時系列で表示します。プルリクエストの詳細ビューにある **View Timeline** リンクから開きます。(**Find in timeline** で検索できます。)
- **エディター内** - プルリクエストのブランチがチェックアウトされているときに、通常のエディターに重ねて表示されます。[エディターでのレビュー](Review-in-Editor-ja.md)を参照してください。

## コメントエディター

タイムライン、差分インレイ、インライン編集、そして Create-PR の説明欄まで、すべてのコメントエディターは 1 つの GitHub スタイルのコンポーザーを共有しています。左上に **Write | Preview** のタブストリップがあり、書式設定ツールバーは同じ上部ストリップに沿ってタブの右隣に右詰めで配置され、**Polish grammar &amp; spelling with AI** が区切り線の後ろの右端に固定されています。控えめな **Add files** リンクが下段の、送信ボタンの左側にあります。

![Write | Preview タブと上部の書式設定ツールバーストリップ、送信ボタンの隣の下段にある Add files リンクを備えたコメントコンポーザー](comment-toolbar.png){ width="640" border-effect="line" }

| グループ | ボタン |
|-------|---------|
| **References** | Mention user (`@`)、Reference work item (`#`)、Reference pull request (`!`) |
| **Formatting** | Heading、Bold、Italic、Inline code、Link |
| **Lists** | Bulleted、Numbered、Task list |
| **AI** | **Polish grammar &amp; spelling with AI** |

差分／エディターのインレイでは **Insert code suggestion** も使えます。キーボード: <shortcut>⌘B</shortcut> 太字、<shortcut>⌘I</shortcut> 斜体、<shortcut>⌘E</shortcut> インラインコード、<shortcut>⌘K</shortcut> リンク、<shortcut>⌘↵</shortcut> 送信 (または <shortcut>Ctrl</shortcut> 相当のキー)。

**Preview** をクリックすると、エディターが markdown のレンダリングビューに切り替わります。これは投稿済みのコメントで使われるレンダリングと同じなので、プレビューした内容が投稿される内容と一致します。Preview を表示している間は書式設定ツールバーが隠れます。**Write** をクリックすると編集に戻ります。空の下書きは *Nothing to preview* としてプレビューされます。

> **Polish grammar &amp; spelling with AI** は、下書き (または選択範囲) をその場で 1 回の取り消し可能な編集として書き換えます。[AI プロバイダーの設定](AI-Features-ja.md)が必要です。AI がオフのときは、このボタンは表示されません。
> {style="tip"}

## @メンション

**Mention user** をクリックするか `@` を入力すると、組織内のメンバーのオートコンプリートが開きます。矢印キーと <shortcut>Enter</shortcut> で 1 人を選びます。メンションされたユーザーには Azure DevOps の通知が届きます。

既存の `@mention` をクリックすると、そのユーザーのアバターと名前を表示する小さな **author card** が開きます。メールアドレスが分かっている場合 (プルリクエストの作成者またはレビュアー) は、このカードで **Copy email** と **Send email** が利用できます。

> @メンションのオートコンプリートには **Identity (Read)** スコープ (PAT) または **Full access** (OAuth) が必要です。[認証](Authentication-ja.md)を参照してください。
> {style="note"}

## 画像と添付ファイル

画像を添付する方法は 3 つあります。

- **Add files** - 下段 (送信ボタンの左側) の **Add files** リンクをクリックして、ディスクから画像ファイルを選びます。
- クリップボードから画像を **貼り付け** ます (<shortcut>⌘V</shortcut> / <shortcut>Ctrl+V</shortcut>)。
- 画像ファイルをエディターに **ドラッグ &amp; ドロップ** します。

サポートされる形式は `png`、`jpg`、`jpeg`、`gif`、`webp`、`bmp`、`svg` です。アップロードごとに *Uploading…* プレースホルダーが表示され、その後インラインの markdown 画像になります。投稿済みの画像を右クリックすると **Copy Image Link** または **Download Image…** が利用できます。

## 変更の提案

変更を説明する代わりに具体的な変更を提案するには、**suggestion** を使います。差分／エディターのインレイで **Insert code suggestion** をクリックする (コメント対象の行があらかじめ入力されます) か、```` ```suggestion ```` ブロックを入力します。

![Apply Locally アクションを備えた変更の提案](suggestion-block.png){ width="560" border-effect="line" }

スレッドには **Suggested change** カードが表示され、**Apply Locally** (および 1 ステップで適用してコミットする **Commit…**) が使えます。Apply は、プルリクエストのブランチがチェックアウトされるまで、また解決済みのスレッドでは無効になっています。

## 返信、解決、スレッドの管理

- **Reply** - フォローアップを追加します。Azure DevOps のスレッドはフラットなので、返信はスレッドの末尾に追加されます。
- **Resolve / Reopen** - 完了したスレッドを閉じたり、再度開いたりします。解決済みのスレッドは目立たなくなり、差分フィルターが *Show only unresolved* に設定されているときは非表示になります。
- **👍 Thumbs up** - コメント本文の下にあるリアクション行の「いいね」ボタンです (レビュースレッドでは **Reply** / **Resolve** と共有されます)。「いいね」が 1 件以上つくとカウントが表示され、自分が「いいね」するとゴールドになります。ツールチップは **Thumbs up** と **Remove thumbs up** の間で切り替わります。
- **More actions (⋯)** - コメントヘッダーのオーバーフローメニューです。どのコメントでも **Copy link**、**Copy Markdown**、**Quote reply** (コメントを `>` ブロック引用としてこのスレッドの返信エディターに挿入します) に加えて **Hide** (本文をその場で折りたたむローカル専用の操作で、再構築や再起動をまたいで維持されます) が使えます。自分のコメントではさらに **Edit** と **Delete** が使えます。

### スレッドのステータス

解決済み／未解決に加えて、スレッドはステータスチップを持ちます。これ (**Change status**) をクリックすると、次の間で切り替えられます。

| ステータス | 意味 |
|--------|---------|
| **Active** | 新しいスレッド (チップは表示されません)。 |
| **Pending** | 作成者による変更を待っています。 |
| **Resolved** | 変更が適用されました。 |
| **Won't fix** | 認識されていますが、変更は行われません。 |
| **Closed** | ディスカッションは完了し、アクションはありません。 |

## タイムラインイベント

タイムラインには、コメントに加えてシステムイベントも表示されます。投票の変更、レビュアーの追加／削除、作業項目のリンク／リンク解除、完了したステータスチェック、そして強制プッシュ (コミットを比較するリンク付き) です。
