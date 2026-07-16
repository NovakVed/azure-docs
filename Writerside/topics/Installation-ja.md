# インストール

ビルド %min_ide_build% 以降で動作する任意の JetBrains IDE に %product% をインストールできます。

> **要点** - <ui-path>Settings | Plugins | Marketplace</ui-path> で **Azure DevOps Pull Requests** を検索し、**Install** をクリックして再起動します。その後、Azure DevOps リモートを持つプロジェクトを開いて[サインイン](Authentication-ja.md)します。
> {style="tip"}

## サポート対象の IDE

このプラグインは IntelliJ Platform を対象としており、その上に構築された任意の IDE で動作します。

- IntelliJ IDEA (Ultimate &amp; Community)
- JetBrains Rider
- PyCharm (Professional &amp; Community)
- WebStorm、PhpStorm、GoLand、RubyMine、CLion、DataGrip、RustRover
- Android Studio (動作する場合がありますが、正式にはサポートされていません)

### 最小ビルド

このプラグインは、当時導入されたプラットフォーム API を使用するため、IDE ビルド `%min_ide_build%.*` 以降 - すべての JetBrains IDE の **%min_ide_version%** リリース - を必要とします。

> **バージョンの確認:** IDE メニューから **About** を開き、`%min_ide_build%` で始まるビルド番号を探します。それより低い場合は、まず **Help → Check for Updates** を実行してください。
> {style="note"}

## Marketplace からインストールする

<procedure title="プラグインをインストールする">
    <step><ui-path>Settings | Plugins | Marketplace</ui-path> を開きます (macOS では <shortcut>⌘,</shortcut>、Windows/Linux では <shortcut>Ctrl+Alt+S</shortcut>)。</step>
    <step><b>Azure DevOps Pull Requests</b> を検索します。</step>
    <step><b>Install</b> をクリックします。</step>
    <step>プロンプトが表示されたら IDE を再起動します。</step>
</procedure>

![JetBrains Marketplace からのインストール](marketplace-install.png){ width="700" border-effect="line" }

### 正しく動作したか確認する

Azure DevOps の Git リモートを持つプロジェクトを開き、次を確認します。

- 左側のツールウィンドウバーに **Pull Requests** のストライプアイコンが表示される。
- <ui-path>Settings | Version Control | Azure DevOps</ui-path> が存在する。

> **ツールウィンドウが表示されない場合は?** プロジェクトに **Azure DevOps リモートがない** 場合は非表示になります。`git remote -v` を実行し、URL に `dev.azure.com` または `visualstudio.com` が含まれることを確認してください。[トラブルシューティング](Troubleshooting-ja.md)を参照してください。
> {style="note"}

## ディスクからインストールする

プレリリースの `.zip` ビルドの場合:

<procedure title="ディスクからインストールする">
    <step><ui-path>Settings | Plugins</ui-path> を開きます。</step>
    <step>歯車アイコン → <b>Install Plugin from Disk…</b> をクリックします。</step>
    <step><code>.zip</code> を選択して再起動します。</step>
</procedure>

## システム要件

| コンポーネント | 最小要件 | 備考 |
|-----------|---------|-------|
| IDE ビルド | %min_ide_build%.* | JetBrains %min_ide_version% 以降 |
| JDK | 21 | IDE にバンドル |
| Git | 2.20+ | ブランチ検出と HTTPS 認証の受け渡し |
| OS | macOS / Windows / Linux | IDE がサポートする任意のプラットフォーム |
| ネットワーク | Azure DevOps への HTTPS | `dev.azure.com` またはセルフホストサーバー |

> **プロキシの背後にある場合は?** このプラグインは IDE 自身の HTTP プロキシを使用します。<ui-path>Settings | Appearance &amp; Behavior | System Settings | HTTP Proxy</ui-path> で一度設定すれば、Azure DevOps と (HTTP) AI 呼び出しの両方がそれを継承します。CLI ベースの AI プロバイダーは外部バイナリであり、これを経由しません。
> {style="note"}

## 必須のバンドルプラグイン

このプラグインは、IDE にバンドルされている 2 つのプラグイン (どこでもデフォルトで有効) に**依存**しています。いずれかが無効になっていると、プラグインは読み込まれません。<ui-path>Settings | Plugins | Installed</ui-path> で再度有効にしてください。

- **Git** (`Git4Idea`) - ブランチ検出と HTTPS 資格情報。
- **Markdown** - コメントと説明のエディターを支えます。

## 更新とアンインストール

更新は <ui-path>Settings | Plugins | Installed</ui-path> に表示されます。更新が提供されたら **Update** をクリックし、新しいバージョンが完全に読み込まれるように **IDE を再起動**してください。アンインストールするには、歯車アイコン → **Uninstall** を使用します。保存されている資格情報もキーチェーンから削除されます。

> **インストールまたは更新後は再起動してください。** このプラグインはいくつかのスタートアップフック (例: ツールウィンドウのアクティベーションショートカット) を登録するため、その場でホットリロードされません。IDE を完全に再起動することで、すべてが正しく接続されます。
> {style="note"}

> **次のステップ:** 1 分間のツアーには[クイックスタート](Quick-Start-ja.md)、サインインには[認証](Authentication-ja.md)を参照してください。要約と AI レビューを有効にするには、[AI 機能](AI-Features-ja.md)を参照してください。
> {style="tip"}
