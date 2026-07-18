# 通知と注目

このプラグインは *あなた* を必要とするプルリクエスト（あなたのレビュー待ちのもの、または誰かがあなたを @メンションしたもの）を監視し、**バルーン**、**ツールウィンドウのバッジ**、**行のチップ** という 3 つの方法で表示します。すでにポーリングしているデータを利用するため、追加のネットワーク呼び出しは発生しません。

## 通知バルーン

あなたの対応が必要なことが発生すると、右下にワンクリックで操作できるバルーンが表示されます。

![あなたの対応が必要な PR の通知バルーン](attention-balloon.png){ width="420" border-effect="line" }

次のような場合に通知を受け取ることができます。

- あなたが **レビューを依頼された** PR。
- あなたを **@メンションした** コメント。
- あなたが参加したスレッドへの **返信**。
- あなたが作成した PR での **レビュアーの投票の変更**。
- ブランチをプッシュした直後に **PR を作成する** チャンス。

単一のイベントは、その PR を直接開きます。レビュー依頼や投票の変更では **Open pull request**、メンションや返信では **View comment**（該当するコメントの位置に移動します）。複数のイベントが同時に発生した場合は 1 つのバルーンにまとめられ（*「N 件のプルリクエストがあなたのレビューを必要としています」*）、その **Show pull requests** アクションでツールウィンドウが開きます。バルーンは、あなたが操作するか、しばらくすると自動的に消えます。クリアするためのボタンはありません。

## ツールウィンドウのバッジ

**Pull Requests** のストライプアイコンには、あなたのレビュー待ちのものがある間はバッジのドットが表示されるため、ウィンドウを開かなくても気づくことができます。（ドットは、ストライプボタンが選択されているときも見やすいように色を変えます。）

## 行の注目チップ

**注目チップ** をオンにすると、その PR がなぜあなたを必要としているのかを、リスト内で直接確認できます。

![プルリクエストの行に表示される注目チップ](attention-row-chips.png){ width="640" border-effect="line" }

| チップ | 意味 |
|------|---------|
| **Review requested** | あなたはまだ投票していないレビュアーです。 |
| **Mentions you** | コメントがあなたを @メンションしています。 |
| **Replied** | あなたが参加したスレッドに新しいアクティビティがあります。 |

チップは **デフォルトではオフ** です。[Settings](Settings-ja.md) の **Show attention markers on pull-request rows** でオンにできます。チップにマウスカーソルを合わせると、*「このプルリクエストがあなたの注目を必要としている理由」* のツールチップが表示されます。

> **未読マーカー** は別のものです。青いドットは新しいコミット *または* 新しいコメントアクティビティがある PR を示し、その PR を開いた瞬間にクリアされます。ツールウィンドウの歯車アイコン → **Show unread markers** から切り替えられます。
> {style="note"}

## 通知される内容を調整する

<ui-path>Settings | Version Control | Azure DevOps</ui-path> → **Polling &amp; notifications** を開きます。

| 設定 | デフォルト |
|---------|---------|
| **Notify when I'm asked to review a pull request** | オン |
| **Notify when someone @mentions me in a pull request** | オン |
| **Notify on replies in threads I participated in** | オン |
| **Notify when reviewer votes change on my PRs** | オン |
| **Offer Create PR after I push to an Azure DevOps remote** | オン |

プラグインの通知グループ（ポップアップ / ツールウィンドウ / ログのみ）は、<ui-path>Settings | Appearance &amp; Behavior | Notifications</ui-path> で振り分けることもできます。[Settings](Settings-ja.md#notifications) を参照してください。
