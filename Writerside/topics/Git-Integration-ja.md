# Git 連携

このプラグインは IDE にバンドルされている Git プラグインと連携し、Azure DevOps のリモートを検出して、現在のブランチをその PR と対応付け、HTTPS 認証情報を引き渡すことで `git fetch` と `git push` をそのまま動作させます。

## リポジトリの検出

プロジェクトを開くと、プラグインはすべての Git リモートを走査して次のパターンを探します。

- `https://dev.azure.com/<org>/<project>/_git/<repo>`
- `https://<org>.visualstudio.com/<project>/_git/<repo>`（レガシー）
- `git@ssh.dev.azure.com:v3/<org>/<project>/<repo>`（SSH）
- アカウントに登録されたセルフホストの Azure DevOps Server の URL

いずれかのリモートが一致すると、**Pull Requests** ツールウィンドウが表示され、バックグラウンド同期が始まります。一致しない場合、プラグインは邪魔になりません。

## 現在のブランチ → PR

プラグインはチェックアウトされたブランチを監視し、（ソースブランチ名によって）対応するオープンな PR に解決します。見つかると、2 つのウィジェットが点灯します。

### メインツールバーのブランチウィジェット

**main toolbar** の Git ブランチウィジェットに Azure DevOps バッジ `!1234 on feature/login` が付きます。クリックするとその PR の操作が表示されます。

![メインツールバーのブランチウィジェットのポップアップ](branch-widget-popup.png){ width="440" border-effect="line" }

- **Show in Tool Window** - PR の詳細ビューを開きます。
- **Update Pull Request Branch** - ローカルブランチが PR のヘッドから分岐している場合に表示されます（*Update Project* を実行します）。
- **Review in Editor** - エディター内レビューのオーバーレイを切り替えます。[エディターでレビュー](Review-in-Editor-ja.md)を参照してください。

### ステータスバーのウィジェット

**status bar** にある別のウィジェットは `ADO PR !1234` を表示します。クリックするとその PR がツールウィンドウで開きます。（ステータスバーのウィジェットチューザーで表示・非表示を切り替えられます。名前は *Azure DevOps PR (current branch)* です。）

ブランチを切り替えると両方のウィジェットが更新され、新しいブランチに PR がない場合は消えます。

## HTTPS 認証

Git が Azure DevOps リモートに対して HTTPS 認証情報を必要とすると、プラグインは保存されたトークンを自動的に供給します。

<procedure title="HTTPS 認証の引き渡しの仕組み">
    <step>IDE 内から（Update Project、Git ツールウィンドウ、または組み込みターミナルで）<code>git fetch</code> または <code>git push</code> を実行します。</step>
    <step>Git が IDE に認証情報を要求します。</step>
    <step>プラグインがリモートをサインイン済みのアカウントと照合し、そのトークンを供給します。</step>
    <step>Git が処理を進めます - パスワードの入力は求められません。</step>
</procedure>

同じ URL に複数のサインイン済みアカウントが一致する場合は、プロジェクトの**デフォルトアカウント**が使用されます（[設定](Settings-ja.md)を参照）。

> IDE の外部の**システムシェル**から実行された Git コマンドは、このプロバイダーを認識しません。主に外部ターミナルで作業する場合は、システム全体の Git 認証情報ヘルパーを設定してください - [トラブルシューティング](Troubleshooting-ja.md#git-push-asks-for-a-password)を参照してください。
> {style="note"}

## Push → PR の作成

まだ PR のないブランチをプッシュした後、プラグインはバルーンで **Create a pull request** を提案できます - ツールバーよりも速い経路です。[設定](Settings-ja.md)の **Offer Create PR after I push to an Azure DevOps remote** で切り替えられます。その他の Git 由来の通知（レビュー依頼、投票の変更、返信）は[通知と注目](Notifications-and-Attention-ja.md)で扱っています。

## 複数リポジトリとセルフホスト

- 1 つのプロジェクト内の**複数のリポジトリ**はそれぞれ独立して検出されます。ツールウィンドウの **Switch Account / Repository…** を使って 1 つに絞り込みます。
- **Azure DevOps Server（オンプレミス）**はクラウド製品とまったく同じように動作します - サインイン時にサーバー URL を追加し、そのサーバーで生成したトークンを使用します。
