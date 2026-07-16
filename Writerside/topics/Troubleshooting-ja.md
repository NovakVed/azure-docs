# トラブルシューティング

ユーザーが最もよく遭遇する問題への手早い解決策です。判断が必要な質問（「OAuth と PAT のどちらを使うべき？」「オンプレミスに対応している？」など）については、[FAQ](FAQ-ja.md) を参照してください。問題がここで扱われていない場合は、末尾の[バグの報告](#filing-a-bug)を参照してください。

## ツールウィンドウが表示されない

Azure DevOps の Git リモートが検出されない場合、Pull Requests ツールウィンドウは非表示になります。次を確認してください。

<procedure>
    <step>プロジェクトのルートで <code>git remote -v</code> を実行します。少なくとも 1 つのリモート URL に <code>dev.azure.com</code> または <code>visualstudio.com</code>（あるいは設定済みのセルフホストサーバー）が含まれている必要があります。</step>
    <step>バンドルされた <b>Git</b> プラグイン（<code>Git4Idea</code>）が <ui-path>Settings | Plugins | Installed</ui-path> で有効になっていることを確認します。</step>
    <step>IDE を再起動します。リモートのスキャンはプロジェクトを開いたときに実行されます。</step>
</procedure>

## サインイン後に「401 Unauthorized」と表示される

- PAT に必要なスコープが不足している可能性があります。[認証](Authentication-ja.md)を参照してください。最も簡単な解決策は **Full access** で再生成することです。
- PAT の有効期限が切れている可能性があります。トークンは作成時に設定した日付で失効します。
- 組織が PAT を無効化している可能性があります。その場合は OAuth を使用してください。

## 特定の操作で「403 Forbidden」と表示される

PAT は有効ですが、その操作に対する権限が Azure DevOps アカウントにありません（例: プルリクエストは読めるが投票できない、マージできないなど）。プロジェクトまたはリポジトリに対する必要な権限を付与してもらうよう、Azure DevOps 管理者に依頼してください。

## OAuth のブラウザーが IDE に戻ってこない

OAuth は**ローカルループバックリダイレクト**を介して完了します。ブラウザーは `http://127.0.0.1:<port>/azure-oauth/callback` に戻され、IDE の組み込み Web サーバーがこれを処理して *"Sign-in complete. You can close this tab."* を表示します。この往復が失敗する場合は次を確認してください。

- ファイアウォールやセキュリティツールが、IDE の組み込みサーバー（ポート範囲 **63342–63352**）への localhost 接続をブロックしている可能性があります。
- ポップアップのブロックや既定でないブラウザーがリダイレクトを妨げることがあります。意図したブラウザーが既定になっていることを確認してください。
- サインインウィンドウには **5 分**の制限があります。期限が切れた場合は最初からやり直してください。

回避策: OAuth の代わりに Personal Access Token を使用します。

## 同期後もプルリクエストに新しいコメントが表示されない

<procedure>
    <step><shortcut>⌘R</shortcut> / <shortcut>Ctrl+R</shortcut> / <shortcut>F5</shortcut> を押す（または右クリック → <b>Refresh List</b>）ことで、すぐに同期を強制します。Reload ツールバーボタンはありません。</step>
    <step><b>idea.log</b> に同期エラーがないか確認します（詳細については<a anchor="enabling-debug-logs">デバッグログを有効化</a>してください）。</step>
    <step>同期間隔は既定で 60 秒です。<a href="Settings-ja.md">Settings</a> で長く設定している場合は、遅延も長くなります。</step>
</procedure>

## インラインコメントが差分に表示されない

- プラグインは、**Code (Read)** 権限を持つプルリクエストにのみインラインスレッドを描画します。
- （プルリクエストではなく）ローカルの作業ツリーから差分を表示している場合、インラインスレッドは描画されません。ツールウィンドウからプルリクエストを開き、その変更ツリーとスレッドを読み込んでください。
- ローカルブランチがプルリクエストのヘッドから分岐している場合、エディター内レビューは自動的に無効になります。変更をプッシュするか、プルリクエストのヘッドを正確にチェックアウトしてください。

## Git のプッシュでパスワードを求められる

プラグインの HTTPS 資格情報プロバイダーは、**IDE 内**で実行される Git 操作に対してのみ機能します（IDE 内から起動したターミナルは「内部」とみなされます）。外部ターミナルの場合は、システムレベルの Git 資格情報ヘルパーを設定してください。

```bash
# macOS Keychain
git config --global credential.helper osxkeychain

# Windows
git config --global credential.helper manager

# Linux (libsecret)
git config --global credential.helper libsecret
```

## AI 機能が見つからない、またはエラーを返す

- <ui-path>Settings | Version Control | Azure DevOps | AI Settings</ui-path> を開き、**Enable AI assistance** がオンになっており、少なくとも 1 つのプロバイダーが構成され有効になっていることを確認します。
- プロバイダーの行で **Test connection** をクリックします。失敗する場合は、API キー、モデル名、エンドポイント URL を再確認してください。
- **Ollama** の場合は、デーモンがローカルで実行されており（`ollama serve`）、指定したモデルがプルされている（`ollama list`）ことを確認します。
- **CLI プロバイダー**（Claude Code、Codex、Copilot CLI）の場合は、バイナリが `PATH` 上にあり、サインイン済み（`claude /login` など）であることを確認します。
- プロバイダーのレート制限やクォータのエラーはプロバイダーから直接返されるもので、再試行されません。

## プラグインの競合

このプラグインは、IDE の `collaboration-tools` ツールキットをバンドルされた **GitHub** プラグインおよび **GitLab** プラグインと共有します。両方と共存します（独立したツールウィンドウ、独立した状態）。既知の相互作用点が 2 つあります。

- プロジェクトに Azure DevOps と GitHub の両方のリモートがある場合、両方のツールウィンドウが表示され、右クリックのコンテキストメニューにそれぞれの操作が現れることがあります。
- サードパーティのプラグインが AI 拡張ポイント（`intellij.vcs.azuredevops.aiSummaryExtension` など、[プライバシーとデータ](Privacy-and-Data-ja.md)を参照）をオーバーライドしている場合、その機能について組み込みの既定はバイパスされます。AI 機能が予期しない動作をする場合は、<ui-path>Settings | Plugins</ui-path> で、拡張ポイントにフックしている可能性のある他の Azure DevOps または AI プラグインを確認してください。

## ネットワークのタイムアウトまたは「request failed」

このプラグインは IntelliJ の HTTP プロキシ構成を使用します。専用のプロキシ設定はありません。企業ネットワークの制限で送信 HTTPS がブロックされる場合は次を確認してください。

- <ui-path>Settings | Appearance &amp; Behavior | System Settings | HTTP Proxy</ui-path> を確認します。プラグインはここで設定した内容に従います。
- AI ストリーミングリクエストの HTTP タイムアウトは **5 分**です。それより長いものはハングとして扱われ、通知として報告されます。
- Azure DevOps API 呼び出しの再試行動作は「フェイルファスト」です。一時的なエラーは再試行されないため、UI に重複した呼び出しが積み上がりません。60 秒ごとのバックグラウンド同期が、失敗したリクエストの続きを引き継ぎます。

## プラグインの更新で何かが壊れた

以前のバージョンにロールバックします。

<procedure>
    <step><ui-path>Settings | Plugins | Installed</ui-path> を開き、<b>Azure DevOps Pull Requests</b> を見つけます。</step>
    <step>歯車アイコンをクリック → <b>Manage Plugin Versions</b> を選択します。</step>
    <step>古いバージョンを選択してインストールします。</step>
    <step>IDE を再起動します。</step>
</procedure>

## デバッグログの有効化 {id="enabling-debug-logs"}

より詳細なトラブルシューティングのために、トレースログを有効にします。

<procedure>
    <step><ui-path>Help | Diagnostic Tools | Debug Log Settings…</ui-path> を開きます。</step>
    <step>次の行を追加します。
        <code-block lang="text">
#com.vednovak.azure
#com.vednovak.azure.sync
#com.vednovak.azure.api
        </code-block>
    </step>
    <step>問題を再現します。</step>
    <step><ui-path>Help | Show Log in Explorer/Finder</ui-path> を開いて <code>idea.log</code> を見つけます。</step>
</procedure>

ログは IDE のキャッシュディレクトリにあります。

<tabs>
    <tab title="macOS">
        <code>~/Library/Logs/JetBrains/&lt;IDE&gt;&lt;Version&gt;/idea.log</code>
    </tab>
    <tab title="Windows">
        <code>&#37;LOCALAPPDATA&#37;\JetBrains\&lt;IDE&gt;&lt;Version&gt;\log\idea.log</code>
    </tab>
    <tab title="Linux">
        <code>~/.cache/JetBrains/&lt;IDE&gt;&lt;Version&gt;/log/idea.log</code>
    </tab>
</tabs>

## バグの報告 {id="filing-a-bug"}

再現可能な問題を見つけた場合は次を行ってください。

<procedure>
    <step><ui-path>Help | Diagnostic Tools | Collect Logs and Diagnostic Data</ui-path> を実行します。</step>
    <step><a href="%repo_url%/issues/new">新しい GitHub issue</a> を開き、次を含めます。
        <ul>
            <li>IDE のバージョン（<b>About</b>）</li>
            <li>プラグインのバージョン</li>
            <li>OS とアーキテクチャ</li>
            <li>再現手順</li>
            <li>期待される動作と実際の動作</li>
            <li>整理した <code>idea.log</code> のスニペット（投稿前にトークンを削除してください）</li>
        </ul>
    </step>
</procedure>

> **公開 issue に PAT や OAuth リフレッシュトークンを絶対に貼り付けないでください**。ログは既定でトークンを秘匿してキャプチャしますが、送信前に必ず再確認してください。
> {style="warning"}
