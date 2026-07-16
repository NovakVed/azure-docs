# AI機能

任意のAIヘルパー: PRの要約、差分全体のレビュー、コードの説明、コミットメッセージ、PRのタイトル/説明の下書き、文法の校正。**プロバイダーは自分で用意** - OpenAI、Claude、Gemini、Ollama、GitHub Copilot - し、各機能を好きな場所にルーティングできます。

> ここに記載されているものはすべて**オンにするまではオフ**です。プロバイダーに何が送信されるかの詳細については、[プライバシーとデータ](Privacy-and-Data-ja.md)を参照してください。
> {style="note"}

## プラグインがAIでできること

| 機能 | 内容 | 場所 |
|---------|--------------|-------|
| **Summarize Pull Request** | 説明に貼り付けられる差分の要約を下書きします。 | タイムラインカード / オーバーフローメニュー |
| **Run AI Review** | 差分をたどってインラインのレビューコメントを提案します。 | 差分ツールバー / 変更ツリーメニュー / オーバーフロー |
| **Explain This File** | ファイルまたは選択範囲のわかりやすい説明をストリーミングします。 | 差分内で右クリック |
| **Generate Commit Message with AI** | ステージされた変更からコミットメッセージを下書きします。 | Commitツールウィンドウ |
| **Title + Description** | ブランチの差分からCreate-PRフォームを事前入力します。 | Create Pull Requestフォーム |
| **Polish grammar &amp; spelling with AI** | 任意のコメントや説明をその場で整えます。 | すべてのコメントエディター |

![PRタイムライン上のAI要約カード](ai-summary-card.png){ width="700" border-effect="line" }

> **Run AI Review** は差分内にインラインの提案を表示します。それぞれに **Add to review** - AIのテキストをその行の新規コメントエディターに入れ、編集して下書きとしてキューに入れられます - または **Discard**（提案を非表示にする）が用意されています。**保留中のコメントを送信するまで、Azure DevOpsには何も投稿されません。** 実行に失敗すると、ワンクリックの **Open AI Settings** へのジャンプ付きのバルーンが表示されます。
> {style="tip"}

### 要約を調整する

**AI summary** カードの右上隅にある **Summary settings** の歯車アイコンを開くと、要約の生成方法を制御するポップアップが開きます:

| コントロール | オプション |
|---------|---------|
| **Generate automatically on open** | チェックボックス - 既定ではオフ。オンにすると、PRを開くとすぐにカードが要約を下書きします。 |
| **Verbosity** | スライダー: **Brief** · **Neutral** · **Verbose**。 |
| **Formality tone** | スライダー: **Informal** · **Neutral** · **Formal**。 |
| **Personality** | 自由入力 - 任意のペルソナ。例: 「少し皮肉屋のプリンシパルエンジニア」。 |
| **Customization prompt** | 自由入力 - 既定を使う場合は空欄のままにします。これはAI Settingsの **Configure Prompts → Pull Request summary** と同じオーバーライドなので、どちらの画面での編集も同期されます。 |

Saveボタンはありません - コントロールを編集してポップアップを閉じると適用されます。

![AI要約カードの歯車から開くSummary settingsポップアップ](ai-summary-settings-popup.png){ width="520" border-effect="line" }

## プロバイダーを設定する

<ui-path>Settings | Version Control | Azure DevOps | AI Settings</ui-path> を開き、**Enable AI assistance**（マスタースイッチ）をオンにします。次に **AI Providers** テーブルでプロバイダーを追加します。

![AI Settingsページ: プロバイダーと機能ごとのルーティング](ai-settings.png){ width="720" border-effect="line" }

各行は1つのプロバイダーインスタンスで、**Provider**、**Model**、**Enabled** の各列があります。最初の有効な行が既定になります。**Add AI Provider** ダイアログでは5つのファミリーを選べます:

| ファミリー | 備考 |
|--------|-------|
| **OpenAI** | GPTモデル。OpenAI互換のベースURL（Azure OpenAI、vLLMなど）で動作します。 |
| **Claude** | Anthropic Claudeモデル。 |
| **Gemini** | Google Geminiモデル。 |
| **Ollama** | ローカルモデル - 無料、キー不要。 |
| **GitHub Copilot** | Copilotサブスクリプションを使用します（CLIのみ）。 |

> Add/Editダイアログの **Model** ドロップダウンは自動的に候補を読み込みます: 内蔵の推奨リストを即座に表示し、続いてプロバイダーへのライブクエリ（例: OpenAIとClaudeの `/v1/models`）で更新するため、新しく出荷されたモデルもプラグインの更新なしで表示されます。ライブリストは約30分間キャッシュされます。ダイアログを開くたび、およびファミリーやモードを変更するたびに更新されるため、手動の更新ボタンはありません。ディスカバリーには保存済みのキーが必要です - キーが入力されるまで、ドロップダウンは推奨リストにフォールバックします。フィールドは編集可能なままなので、いつでもモデルIDを手入力できます。
> {style="note"}

ほとんどのファミリーは2つの **モード** のいずれかで動作します:

- **HTTP API (use an API key)** - キーを貼り付けます。任意で **API URL** を設定してカスタムエンドポイントを指定できます。キーはIDEキーチェーン（PasswordSafe）に保存されます。
- **CLI (use the local command-line tool)** - キー不要。ローカルバイナリが自身の認証を処理します。最も手間がかかりませんが、CLIベンダーの利用規約を受け入れることになります。

保存する前に、ダイアログ内の **Test Connection** でプロバイダーが動作することを確認してください。

## 機能をプロバイダーにルーティングする

**Per-Feature Provider** パネルは各機能を特定のインスタンスに固定します - 安価な機能を小さいモデルに、重いレビューを賢いモデルに送るのに便利です:

```
AI Summary          → [Default ▾]
AI Review           → [Default ▾]
Title + Description → [Default ▾]   (also used by Generate Commit Message)
Explain Code        → [Default ▾]
```

行を **Default** のままにすると、最初の有効なプロバイダーが使われます。**同じファミリーを複数回**追加でき（例: OpenAIの行を2つ、安価なモデルと賢いモデル）、それぞれ独立してルーティングできます。

### Configure Prompts

**Configure Prompts** パネルでは、各機能の背後にあるシステムプロンプトを編集できます。プロンプトを編集すると、その機能のキャッシュされた応答が無効化されます。

## キャッシュ、コスト、制限

AIの応答は **PRごと + コミットSHAごと** にキャッシュされます（トグル: **Cache AI responses per commit SHA**、既定でオン）。キャッシュヒットはAPI呼び出しなしで即座に返され、新しいコミットや編集されたプロンプトはそれを無効化します。**Advanced** の **Clear AI Response Cache** で強制的に更新できます。

使用したトークンについては、プロバイダーの請求を自分で支払います。使用量を抑えるには:

- 安価な機能（コミットメッセージ、タイトル）を機能ごとのルーティングで小さいモデルに送る。
- **Advanced** の **Max diff size** を下げて、送信前に大きな差分を切り詰める。
- キャッシュをオンにしておき、PRを再度開いても再課金されないようにする。

> プロバイダーのクォータや使用量制限のエラーはプロバイダーからそのまま返されます - プラグインはそれらを分類し、黙って失敗するのではなく明確で実行可能な文言を表示します。プラグイン独自のレート制限やリトライは追加しません。
> {style="note"}

## すべてをローカルに保つ、またはオフにする

- **ローカル推論:** すべての機能を `localhost` 上の **Ollama** インスタンスにルーティングします - コードがマシンから出ることはありません。
- **完全にオフ:** **Enable AI assistance** のチェックを外します。すべてのAIのUIがメニューやツールバーから消え、プラグインは外部へのAI呼び出しを一切行いません。
