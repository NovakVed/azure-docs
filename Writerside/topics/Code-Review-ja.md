# コードレビュー

IntelliJ ネイティブの差分ビューアーでプルリクエストをレビューします。変更内容を読み、インラインコメントや提案を残し、投票し、確認済みのファイルを追跡できます。

## 詳細ビュー

プルリクエストを開くと、閉じることのできるエディタータブが作成されます。これは**単一のペイン**で、サブタブはありません。上から下へ、タイトルと `!` 番号（**View Timeline** リンク付き）、source → target のブランチ、ステータスチェック（CI、コンフリクト、必須レビュアーとその投票）、**changed-files ツリー**、そしてアクションバーが並びます。

![単一ペインの詳細ビューで開いたプルリクエスト](pr-detail.png){ width="720" border-effect="line" }

- **変更されたファイル**はツリーに表示されます。クリックすると差分が開きます。
- **ディスカッション**は **View Timeline** リンクから専用のタブで開きます。[ディスカッションとコメント](Discussions-and-Comments-ja.md)を参照してください。
- **投票とアクション**はアクションバーとそのオーバーフローメニューにあります。[プルリクエスト](Pull-Requests-ja.md#open-and-act-on-a-pr)を参照してください。

## 差分を読む

ファイルをクリックすると、プルリクエストごとに 1 つのタブで差分が開きます。別のファイルをクリックするとその場で差し替わるため、<shortcut>F7</shortcut> / <shortcut>⇧F7</shortcut> でプルリクエスト全体のすべての変更範囲を順に移動できます。差分タブには **Review:** ツールバーがあり、**Refresh**、**Submit review**、**Previous / Next Comment** が含まれます。

| 移動 | macOS | Windows / Linux |
|----------|-------|------------------|
| 次 / 前の変更範囲 | <shortcut>F7</shortcut> / <shortcut>⇧F7</shortcut> | <shortcut>F7</shortcut> / <shortcut>Shift+F7</shortcut> |
| 次 / 前のコメント | *Review: ツールバー* | *Review: ツールバー* |

### スレッドの表示 / 非表示

差分のガター設定にある **Review Discussions** メニューで、どのインラインスレッドを表示するかを制御します。**Show all discussions**、**Show only unresolved**、または **Don't show** から選べます。

## 行にコメントする

<procedure title="インラインコメントを追加する">
    <step>変更された行のガターにマウスを合わせると <b>+</b> が表示されます。これをクリックします（または行番号をドラッグして範囲を指定します）。キャレット位置で <shortcut>⌃⇧M</shortcut> / <shortcut>Ctrl+Shift+M</shortcut> を押すこともできます。</step>
    <step>コメントを入力します。コンポーザーはプルリクエストのディスカッションと同じ GitHub スタイルの外観で、上部に整形ツールバーを備えた <b>Write</b> / <b>Preview</b> のタブストリップ、さらに @メンションと画像の貼り付けに対応しています。エディターの詳細は<a href="Discussions-and-Comments-ja.md">ディスカッションとコメント</a>を参照してください。</step>
    <step>分割された送信ボタンから投稿します。主アクションは <b>Start Review</b> で、コメントを保留中のレビューの一部としてキューに追加します。そのドロップダウンには <b>Add Single Comment</b>（すぐに投稿）と <b>Suggest change</b>（選択範囲を作成者が適用できる変更提案としてラップ）があります。</step>
</procedure>

![差分ビューアーで開いたインラインコメント](diff-comment.png){ width="720" border-effect="line" }

> **保留中のレビュー。** キューに追加したコメントは、投票と一緒に送信するまでドラフトのまま残ります（**Submit (N)** ボタンにカウントされます）。これは GitHub ユーザーが期待するのと同じレビューフローです。**Review:** ツールバー、またはオーバーフローメニューの **Submit Pending Comments** から送信します。
> {style="note"}

### コードへのリンクをコピーする

差分ビューアーで行を右クリックし（またはエディター内でレビュー中に）、**Copy Link to Code** を選ぶと、そのコード（ファイル、行、列範囲）への Azure DevOps Web のディープリンクをコピーできます。これは Web UI の **Copy link** が生成するのと同じリンクです。テキストを選択している場合、項目は **Copy Link to Selected Code** となり、正確な文字範囲をリンクします。選択がない場合は、キャレット位置の行全体へのリンクをコピーします。ショートカットは <shortcut>⌘⇧L</shortcut> / <shortcut>Ctrl+Shift+L</shortcut> です。

> このアクションは Azure のプルリクエストレビュー画面（差分ビューアーまたはエディター内レビュー画面）の内部でのみ表示され、通常のエディターでは表示されません。
> {style="note"}

## 投票する

アクションバーの **Approve** ボタンは分割ボタンです。そのドロップダウンには **Approve with suggestions**、**Wait for author**、**Reject**、**Reset feedback** があります。

![Approve 分割ボタンの投票オプション](vote-approve-dropdown.png){ width="380" border-effect="line" }

マージ戦略を含む、プルリクエストの完了または破棄については、[プルリクエスト](Pull-Requests-ja.md#complete-a-pull-request)で説明しています。

## ファイルを確認済みとして追跡する

大きなプルリクエストでは、進めながら各ファイルを **viewed**（確認済み）としてマークしましょう。確認済みのファイルは変更ツリー内で薄く表示されます。

- <shortcut>⌘⇧S</shortcut> / <shortcut>Ctrl+Shift+S</shortcut> を押すか、右クリック → **Mark File as Viewed** を選びます。
- 複数のファイルを選択して右クリックすると **Mark All as Viewed** ができます。

![変更ツリーでの Mark File as Viewed](mark-file-viewed.png){ width="560" border-effect="line" }

> ファイルを開いたときに自動で確認済みにしたい場合は、[設定](Settings-ja.md)で **Mark files as viewed when their diff is opened** をオンにしてください（GitHub に合わせてデフォルトはオフです）。
> {style="tip"}

## 更新以降に変更された部分のみをレビューする {id="compare"}

作成者が新しいコミットをプッシュしても、プルリクエスト全体を読み直す必要はありません。オーバーフロー **⋮** メニューから **Review Changes Since…** を選び、更新を選択すると、変更ツリーがその差分だけに絞り込まれます。その間にマージされた target ブランチのコミットは除外されます。

![変更ツリー上部のイテレーションスコープバナー](compare-updates-banner.png){ width="700" border-effect="line" }

*「Reviewing only what changed since update N」* というバナーがツリーの上に表示されます。**Show all changes** をクリックすると、プルリクエスト全体に戻ります。（このアクションは、プルリクエストに少なくとも 2 つの更新があると表示されます。）

## 代わりにエディターでレビューする

プルリクエストの source ブランチがチェックアウトされている場合、差分タブを使わずに通常のエディターで変更行に直接コメントできます。[エディターでレビューする](Review-in-Editor-ja.md)を参照してください。
