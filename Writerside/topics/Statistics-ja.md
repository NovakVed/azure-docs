# 統計情報

PR 履歴を KPI とチャートに変換する専用のエディタータブです。カスタムの Azure DevOps クエリも、IDE を離れる必要もありません。

![プルリクエスト統計ダッシュボード](statistics-dashboard.png){ width="720" border-effect="line" }

> **ライブポーリングではなく、キャッシュされたデータから計算されます。** 統計情報は、ツールウィンドウがすでに取得済みのデータを使用します。パネルを開くのは瞬時で、追加の API 呼び出しは発生しません。バックグラウンド同期で新しいデータが取り込まれると、数値が更新されます。
> {style="note"}

## 開く

ツールウィンドウのツールバーにある **Pull Request Statistics**（チャート）アイコンをクリックするか、*Find Action* → **Pull Request Statistics** を実行します。タブがエディター領域に開きます。**Refresh statistics** で再計算されます。

## KPI タイル

上部に並ぶ主要な数値の行です。

| KPI | 意味 |
|-----|---------|
| **Created** · **Merged** · **Abandoned** · **Open now** | ウィンドウ内の PR 数 |
| **Merge rate** | 解決済み PR のうちマージされた割合 |
| **Median merge (h)** | 作成から完了までの一般的な時間数 |
| **Approval rate** | レビュアーの投票のうち Approved（提案付きを含む）だった割合 |
| **First response (h)** | 作成者以外による最初のコメントまでの中央値の時間数 |

> 時間ベースの KPI では、平均ではなく**中央値**を使用します。1〜2 件の 1 週間がかりの遅延が、典型的な PR の数値をゆがめるべきではないからです。平均が表示される箇所には、その旨のラベルが付いています。
> {style="note"}

## チャート

チャートは 3 つのセクションにグループ化されています。

- **Workload** - *Top creators*、*Top reviewers*、*Top commenters*、*Reviewer × Author* のコラボレーション。
- **Process health** - *Vote distribution*、*Time to merge*、*PR status*、*Open PR aging*、*PR cycle time (days)*、*PRs merged per week*。
- **Where work goes** - *Target branches*、*Day-of-week activity*、*Daily activity*。

## フィルターとスコープ

固定ヘッダーですべてのメトリックを一度にスコープします。

- **Window** - 直近 7 日間、30 日間、90 日間、6 か月、1 年、または全期間。
- **Author**、**Reviewer**、**Target branch** - 特定の人物やブランチに絞り込みます。
- **Clear filters** - デフォルトにリセットします。

## 注意事項

> **ローカルビューのみ。** 統計情報は、あなたのアカウントが閲覧できる PR を対象とします。アクセス権のないリポジトリはカウントされません。
> {style="warning"}

これは Azure DevOps Analytics の代替ではなく、エディター内で得られる迅速なシグナルです。組織全体のレポートには、Azure DevOps の Analytics サービスを直接使用してください。
