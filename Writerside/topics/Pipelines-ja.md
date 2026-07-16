# パイプライン

Azure Pipelines を IDE から離れることなく参照、実行、レビューできます。専用の **Pipelines** ツールウィンドウには、インタラクティブなステージグラフ、適応型の実行タブ、ライブジョブログ、IDE 内での承認、実行完了通知が備わっています。

> パイプライン統合は**デフォルトで有効**です。[設定](Settings-ja.md)にある単一のマスタースイッチで制御します。ツールウィンドウ、実行通知、ストライプバッジ、IDE 内のパイプラインチェックはすべてこれに連動します。オフにすると、これらはまとめて表示されなくなります。
> {style="note"}

## パイプラインの設定

パイプラインは初期状態で有効になっています。そのマスタースイッチと関連オプションは、<ui-path>Settings | Version Control | Azure DevOps</ui-path> の **Pipelines** グループにあります。

| 設定 | 機能 |
|---------|--------------|
| **Enable Pipelines integration** | Pipelines ツールウィンドウを表示し、プルリクエストのパイプラインチェックを IDE 内で開きます。オフにすると、ツールウィンドウのアイコンが非表示になり、パイプライン通知やバッジは発生せず、パイプラインチェックは代わりにブラウザーで開きます。 |
| **Notify when a pipeline run of mine finishes** | 自分がトリガーした実行が終了状態に達したときにバルーンを表示します。統合がオンのときのみ有効になります。 |
| **Badge the Pipelines tool-window icon when my runs finish** | 自分の実行が完了したときに、Pipelines ストライプアイコンに色付きのドットを追加します（失敗は赤、部分成功は黄、成功は青）。ウィンドウを開くまで表示されます。統合がオンのときのみ有効になります。 |

> **Pipelines** ストライプアイコンは、プロジェクトに **Azure DevOps リモート**が存在し、*かつ*統合スイッチがオンになっている場合にのみ表示されます。アイコンは左側の **Pull Requests** の下に固定され、Pull Requests ウィンドウと同じサインイン済みアカウントおよびリポジトリを共有します。
> {style="note"}

<shortcut>⌘⇧W</shortcut> / <shortcut>Ctrl+Shift+W</shortcut> でウィンドウを開く（またはフォーカスする）ことができます。Windows / Linux では、プラグインが代わりに最初に空いている組み合わせを選びます。**実際のキーを確認するには、ストライプアイコンにカーソルを合わせてください**。このショートカットは IDE 起動時にシードされるため、プラグインをインストールまたは更新した後は、**IDE を完全に再起動する**必要があります。[キーボードショートカット](Keyboard-Shortcuts-ja.md)を参照してください。

## Pipelines ツールウィンドウ

ウィンドウは **Pipelines** リストタブで開きます。そのタイトルアクション（右上）は **Run Pipeline…**（パイプライン実行をトリガー）と **Refresh**（パイプライン実行を再読み込み）で、歯車メニューには **Switch Account / Repository…** が追加されています。

![実行ナビゲーションバーと定義リストが表示された Pipelines ツールウィンドウ](pipelines-tool-window.png){ width="720" border-effect="line" }

### 実行をナビゲートする

上部には検索バーがあり、Pull Requests ウィンドウと同じ構成です。

- 名前、ブランチ、ビルド番号、実行をリクエストした人と一致する**フリーテキスト検索フィールド**。
- 3 つのスコープ（**Recent**、**All**、**Runs**）を持つ **View** チップ（デフォルトは **Recent**）。
- 直近の実行結果でフィルタリングする **Status** チップ: **Succeeded**、**Partially succeeded**、**Failed**、**Running**、**Canceled**。
- **Quick filters** というタイトルの **Filter** クイックメニュー（ライブインジケーターバッジ付き）: **All pipelines**、**Recently run**、**All runs**、**Failed only**、そしていずれかが有効なときには **Clear filters**。

各 **View** スコープでは異なる本文が表示されます。

| スコープ | 表示内容 | 実行を開く |
|-------|-------|------------|
| **Recent** | パイプライン**定義**のフラットなリスト。各項目には最新実行のステータスアイコンと `folder · last run <relative>` のサブタイトルが付きます。 | ダブルクリック / <shortcut>↵ Enter</shortcut> で最新の実行を開きます。右クリック → **Run Pipeline…**。 |
| **All** | 折りたたみ可能な**フォルダーツリー**（`\Team\SubTeam`）としてのパイプライン定義。子孫の数が表示されます。 | リーフをダブルクリック / <shortcut>↵ Enter</shortcut> すると最新の実行が開きます。フォルダーの場合は展開が切り替わります。リーフを右クリック → **Run Pipeline…**。 |
| **Runs** | 最近の**実行**のフラットでスクロール可能なリスト。 | ダブルクリック / <shortcut>↵ Enter</shortcut> で実行を開きます。 |

### 実行のジョブを追跡する

実行を開くと、閉じることのできる `#<n>` タブが追加されます。これは純粋なナビゲーターで、ログはありません。そのヘッダーは実行ステータスのグリフに加えて、パイプライン名と、ブラウザーで実行を開くクリック可能な `#<run number>` です。その下には**ジョブレール**があります。**Summary** リンク、**All jobs** の見出し、そして**折りたたみ可能なステージヘッダーの下にグループ化された**ジョブが並びます。

**Summary** をクリックすると実行概要エディターが開き、**ジョブ**をクリックするとそのジョブのステップログでエディターが開き、**ステージヘッダー**をクリックするとそれが折りたたまれます。<shortcut>↵ Enter</shortcut> はクリックと同じ動作をします。

### ストライプバッジ

**自分がトリガーした**実行が完了し、かつウィンドウをまだ開いていない場合、Pipelines ストライプアイコンに色付きのドットが付きます。**失敗は赤、部分成功は黄、成功は青**です。ウィンドウを開くかフォーカスした瞬間にクリアされ、アカウントや組織の切り替え時に消去されます。[設定](Settings-ja.md)の **Badge the Pipelines tool-window icon when my runs finish** で制御します。[通知と注目](Notifications-and-Attention-ja.md)を参照してください。

## 実行の概要を開く

**Summary**（またはジョブ）をクリックすると、実行ラベル（例: `#20260101.1`）をタイトルとするメインエディタータブとして**実行概要**が開きます。同じ実行を再度開くと、既存のタブがフォーカスされます。

![パイプライン実行の概要: ヘッダー、タブ、インタラクティブなステージグラフ](pipeline-run-overview.png){ width="720" border-effect="line" }

ヘッダーには実行ステータスアイコン、パイプライン名と実行番号、そして淡色のメタ行（`status • branch • requestedFor • duration`）が表示されます。右揃えのアクションは **Cancel**（実行中）、**Re-run**（終了状態のとき、同じソースブランチで再キュー）、そして **Open in Browser** リンクです。ステージがあなたの承認を待っている場合は、ヘッダーの直下に**承認ゲート**バンドが表示されます。[IDE 内での承認](#approvals)を参照してください。

### インタラクティブなステージグラフ

**Summary** タブは **Stages** の見出しと、ズーム・パン可能なステージカードの DAG で開きます。サーバーが `dependsOn` を省略している場合、グラフはジョブカードまたは順次チェーンにフォールバックし、切断されたフローは別々の垂直バンドに配置されます。

![フォーカスされたステージがそのフローをたどっているステージグラフ](pipeline-stage-graph.png){ width="700" border-effect="line" }

- ズームツールバー（右上）には **Zoom out**、**Zoom in**、**Fit to view**、そして **Keyboard shortcuts**（`?` のチートシートを開く）があります。
- どこでも**ドラッグ**するとパンできます。**ホイール**はカーソルを中心にズームします（フィットは 1.0× を超えてズームしません）。
- ステージにカーソルを合わせるかクリックすると、そのフローが強調されます。**Depends on** のエッジは青、**Runs after** のエッジは緑、その他は薄暗く表示され、キャプションカードと凡例がオーバーレイとして表示されます。
- 各カードの**シェブロン**を展開すると、そのジョブと **Rerun stage** ボタンが一覧表示されます。
- ジョブ（またはステージ）をクリックすると、エディターがそのジョブのステップログに移動します。

> <shortcut>=</shortcut> / <shortcut>-</shortcut> / <shortcut>0</shortcut> でグラフをズームイン、ズームアウト、フィットさせ、<shortcut>?</shortcut> で **Pipeline run shortcuts** のチートシートを表示できます。
> {style="tip"}

## 実行タブ

3 つのタブが常に表示されます。**Summary**、**Environments**、**Code coverage** です。さらに 2 つのタブは、**終了した実行がそのデータを公開した場合にのみ**、Azure Web の順序で Summary の直後に挿入されます。**Tests**（実行がテストを報告した場合）と **Extensions**（拡張機能のサマリーを公開した場合）です。

| タブ | 表示内容 |
|-----|---------------|
| **Summary** | ステージグラフに加えて、実行にリポジトリリソースがある場合は **Repositories** カード（列は **Resource Name, Repository, Branch/Tag, Version, Related**）。 |
| **Tests** | ドーナツサマリーと関連するテストケース（後述）。 |
| **Extensions** | 拡張機能が公開した Markdown サマリー（例: SonarQube の品質ゲート）を角丸のカードとして表示。 |
| **Environments** | **Environment, Last stage, Result, Finished** のテーブル。 |
| **Code coverage** | メトリックごとの行。各行にはドーナツ（緑は 80% 以上、黄は 50% 以上、赤はそれ未満）と `X / Y covered` の数値が付きます。 |

終了した実行にアーティファクトがある場合、下部の **Artifacts:** ストリップが各アーティファクトへのリンクを表示します（ブラウザーでダウンロード URL を開きます）。オフライン中に読み込めないセクションはその旨を表示し、再接続時に読み込まれます。

### Tests タブ

![Tests タブ: 結果のドーナツ、統計ブロック、フィルタリング可能な結果テーブル](pipeline-tests-tab.png){ width="720" border-effect="line" }

**ドーナツ**（緑は **Passed**、赤は **Failed**、灰色は **Others**）が統計ブロックの横に表示されます。統計ブロックは **Total tests**、**Pass percentage**、**Run duration**、**Tests not reported** です。その下の **Test results** カードにはフィルターバーがあります。

- 検索ボックス（**Filter by test or run name**）。Tests タブが表示されている間、<shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> でフォーカスし、<shortcut>Esc</shortcut> でクリアします。
- ファセットチップ: **Test file** と **Owner**（それぞれ 2 つ以上の異なる値がある場合にのみ表示）、および **Outcome** チップ。Outcome のバケットは **Failed, Aborted, Passed, Not Impacted, Others** で、デフォルトのフィルターは **Failed + Aborted** です。

テーブルの列はデータに応じて変化し（**Test**、**Owner**（ある場合）、**Duration**（ある場合）、**Outcome**）、300 行が上限です。フィルターですべてが非表示になった場合、**Show all tests** リンクですべてのフィルターがクリアされます。

## ジョブログを表示する

ジョブ（ジョブレールまたはステージカードから）をクリックすると、**GitHub Actions スタイルの折りたたみ可能なステップセクション**が開きます。各ヘッダーはシェブロン、ステータスアイコン、ステップ名、所要時間で構成され、展開すると、エディターフォントでレンダリングされた番号付きの色分けされたログが表示されます（`##[error]` は赤、`##[warning]` は黄、`##[section]` は太字、`##[command]` は青）。失敗したステップは自動的に展開され、実行がライブ中の場合はログがその場でストリーミングされます。

![色分けされた出力を持つジョブの折りたたみ可能なステップログ](pipeline-job-logs.png){ width="720" border-effect="line" }

ログの上の細いヘッダーバーには、**← Summary** の戻りリンク（ツールチップ「Back to the run overview (L)」）があり、続いてジョブのステータスアイコン、名前、メタが表示されます。

> **ログを検索する:** ジョブのログ内で <shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> を押すと、IDE の検索バー（一致件数のカウンターと Case / Words / Regex トグル付き）が開きます。<shortcut>↵ Enter</shortcut> と <shortcut>⇧↵</shortcut> で一致箇所を移動し（折りたたまれたステップを展開して各ヒットをビューにスクロールします）、<shortcut>Esc</shortcut> でバーを非表示にします。
> {style="tip"}

## IDE 内での承認 {id="approvals"}

ステージが、あなたに割り当てられた手動承認でゲートされている場合、実行ヘッダーの下に承認バンドが表示されます。**保留中のゲートごとに 1 つのコールアウトカード**が、Complete-PR の「blocked by」バナーと同じ赤色に色付けされたクロムで表示されます。

![コメントフィールドと Approve / Reject ボタンを持つ承認ゲートカード](pipeline-approval-gate.png){ width="640" border-effect="line" }

各カードには **Approval needed — &lt;Stage&gt;**、`N of M approved · in sequence · waiting since <time>` のメタ行、チェックの指示、そして状態（**Approved**、**Rejected**、**Reassigned**、**Pending**）を示す承認者ごとの行が表示されます。アクション行にはオプションのコメントフィールド（**Add an optional comment…**）と、右揃えの **Reject** および **Approve** ボタンがあり、**Approve** がプライマリスロットに配置されます。

> 実行のリクエスト者が自分の実行を承認することを許可されていない場合、ボタンは説明文と **Review in browser** リンクに置き換えられます。権限やオフラインの問題は、静かに失敗するのではなく、カード上にインラインで表示されます。
> {style="note"}

## パイプラインを実行する

ツールウィンドウのタイトルアクション、または定義の右クリックメニューから **Run Pipeline…** を選択すると、**Run Pipeline** ダイアログが開きます（その OK ボタンには **Run** と表示されます）。

![Run Pipeline ダイアログ: パイプラインとブランチのピッカー、パラメーター、変数](pipeline-run-dialog.png){ width="560" border-effect="line" }

- **Pipeline** および **Branch** のピッカー（検索可能なコンボボックス）。パイプラインの行には名前とフォルダーのサブタイトルが表示されます。ブランチの行には短いブランチ名に加えて、カスタム ref（例: `main` や `refs/tags/v1.0`）用の **Enter a branch or ref…** エスケープが表示されます。ブランチが列挙されるのは Azure Repos のパイプラインのみです。
- **Parameters** セクションは、YAML で宣言された `parameters:` を型付きフォームとしてレンダリングします。`values:` にはドロップダウン、ブール値にはチェックボックス、オブジェクトには等幅の YAML エリア、それ以外にはテキストフィールドが使われます。必須パラメーターには `*` が付きます。
- **Variables** セクションは、キュー時に設定可能な定義変数を公開します（シークレットは保存された値を保持するため空欄のままにします）。
- 2 つのチェックボックス: **Enable system diagnostics**（`system.debug=true` を追加）と **Preview only (render final YAML, don't queue)**。

実際の実行はリストを更新し、新しい実行の詳細を開きます。**Preview only** の場合は、代わりに読み取り専用の **Pipeline Preview — final YAML** ダイアログが開きます。

## 実行完了通知

**自分がトリガーした**実行が終了状態に達すると、`<pipeline> <run#> <verb>`（succeeded / partially succeeded / failed / was canceled）というタイトルのバルーンが表示されます。本文にはブランチが表示され、**Open run** アクションで IDE 内に実行の詳細が開きます。実行と結果ごとに重複が排除され、マスタースイッチと **Notify when a pipeline run of mine finishes** の両方によって制御されます。[通知と注目](Notifications-and-Attention-ja.md)を参照してください。

![Open run アクションを持つ実行完了通知バルーン](pipeline-notification.png){ width="420" border-effect="line" }

## PR のパイプラインチェックを IDE で開く

統合がオンの状態でプルリクエストのパイプライン CI チェックの **Details…** をクリックすると、その実行が **IDE 内で**開き、該当するジョブのログに直接ジャンプします。URL でジョブが指定されていればディープリンクされたジョブへ、そうでなければ最初に失敗または実行中のジョブへ移動します。進行中のチェックには Pipelines の青い「waiting」ディスクが描画されます。マスタースイッチがオフの場合、パイプラインチェックは他のステータスと同様にブラウザーで開きます。

## キーボードショートカット

実行概要には独自のビュー内キーがあり、フォーカスされている間に有効になります。<shortcut>?</shortcut>（またはステージグラフツールバーの **?** ボタン）を押すと同じ一覧が表示されます。これらは Keymap には含まれておらず、再割り当てはできません。

| アクション | ショートカット |
|--------|----------|
| ステージグラフへの**ログの表示 / 戻る** | <shortcut>L</shortcut> |
| **前 / 次のタブ** | <shortcut>[</shortcut> / <shortcut>]</shortcut> |
| ステージグラフの**ズームイン / アウト / フィット** | <shortcut>=</shortcut> / <shortcut>-</shortcut> / <shortcut>0</shortcut> |
| **この実行をブラウザーで開く** | <shortcut>B</shortcut> |
| **テストをフィルタリング**（Tests タブ） | <shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> |
| **この一覧を表示** | <shortcut>?</shortcut> |

> ジョブの**ログ**内では、<shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> は代わりにログ検索バーを開きます。プラグインのショートカットの完全なリファレンスは[キーボードショートカット](Keyboard-Shortcuts-ja.md)にあります。
> {style="note"}

> **次のステップ:** [通知と注目](Notifications-and-Attention-ja.md)で何を発生させるかを調整するか、[設定](Settings-ja.md)ですべてのプラグイン設定を確認してください。
> {style="tip"}
