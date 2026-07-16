# 設定

プラグインが公開するすべての設定のリファレンスです。<shortcut>⌘,</shortcut>（macOS）または <shortcut>Ctrl+Alt+S</shortcut>（Windows/Linux）で **Settings** を開きます。

## Version Control → Azure DevOps

メインページです。上部には **accounts** パネル（追加 **+**、編集 ✏、削除 ✕、プロジェクトごとの既定）があります。[認証](Authentication-ja.md)を参照してください。

![Azure DevOps 設定ページの accounts パネル](accounts-panel.png){ width="700" border-effect="line" }

- **Sync interval (seconds)** - ツールウィンドウが Azure DevOps をポーリングする頻度です。**既定は 60**、範囲は **15–3600**。

### Polling & notifications

| 設定 | 既定 |
|---------|---------|
| **Notify when I'm asked to review a pull request** | オン |
| **Notify when someone @mentions me in a pull request** | オン |
| **Notify on replies in threads I participated in** | オン |
| **Notify when reviewer votes change on my PRs** | オン |
| **Offer Create PR after I push to an Azure DevOps remote** | オン |
| **Include my own pull requests and @mentions** | オフ |

これらが何を制御するかについては、[通知と注目](Notifications-and-Attention-ja.md)を参照してください。

### Pull request review

| 設定 | 既定 |
|---------|---------|
| **Mark files as viewed when their diff is opened** | オフ |
| **Show attention markers on pull-request rows** | オフ |
| **Show keyboard shortcut on comment buttons** | オン |

最後のトグルは、コンポーザーの **Comment** / **Reply** / **Save** ボタンのラベルのすぐ前に送信ショートカット（<shortcut>⌘↵</shortcut> / <shortcut>Ctrl+Enter</shortcut>）を表示します。ショートカットはどちらの状態でも機能します。これはヒントを表示するだけです。

> **Show unread markers** はここにはありません。設定のチェックボックスではなく、ツールウィンドウのトグル（ギアメニュー）です。ドラフトは設定ではなく、リストの**フィルター**です。
> {style="note"}

### Go to Pull Requests

| 設定 | 既定 |
|---------|---------|
| **Show in the Search Everywhere window** | オン |

**Go to Pull Requests** の開き方を制御します。オンの間、このアクションは Search Everywhere に **Pull Requests** タブを追加します（Files / Symbols / Actions の隣）。オフにすると、代わりにスタンドアロンのクイックピックダイアログが開きます。

## Version Control → Azure DevOps → AI Settings

オプションの AI ヘルパーを設定するサブページです。[AI 機能](AI-Features-ja.md)を参照してください。

![AI Settings ページ](ai-settings.png){ width="720" border-effect="line" }

- **General AI Settings → Enable AI assistance** - マスタースイッチです。**既定はオフ。** オフにするとすべての AI 機能が非表示になり、送信呼び出しは一切行われません。
- **AI Providers** - プロバイダーインスタンスごとに 1 行（**Provider / Model / Enabled**）。最初に有効になっている行が既定になります。**Add AI Provider** ダイアログから追加します（OpenAI、Claude、Gemini、Ollama、GitHub Copilot。HTTP-API または CLI モード）。
- **Per-Feature Provider** - **AI Summary**、**AI Review**、**Title + Description**、**Explain Code** を特定のインスタンスにルーティングするか、**Default** のままにします。
- **Configure Prompts** - 各機能のシステムプロンプトを編集します。
- **Advanced** - **Cache AI responses per commit SHA**（既定はオン）、**Max diff size**（既定は 200 KB、範囲は 10–2000）、**Clear AI Response Cache**。

## Appearance & Behavior → Notifications {id="notifications"}

プラグインは、ルーティング可能な（ポップアップ / ツールウィンドウ / ログのみ）2 つの通知グループを登録します。

| グループ | 用途 |
|-------|-----|
| **Azure DevOps Pull Requests** | レビュー依頼、@メンション、返信、投票の変更、プッシュの提案。 |
| **Azure DevOps AI** | AI サマリー / レビュー完了のバルーン。 |

## Keymap

<ui-path>Settings | Keymap</ui-path> を開いて **Azure DevOps** を検索すると、任意のアクションを再割り当てできます。アクション ID を含む完全な一覧は[キーボードショートカット](Keyboard-Shortcuts-ja.md)にあります。

## Per-project vs application-level

ほとんどの設定は**アプリケーションレベル**（すべてのプロジェクト）です。アカウント、通知の設定、AI プロバイダーなど。2 つは**プロジェクトごと**（プロジェクトのワークスペースに保存）です。**既定のアカウント**と **PR リストのフィルター**です。
