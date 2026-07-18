# 通知与关注

该插件会监视需要*你*处理的拉取请求——那些等待你审查的，或者有人 @提及你的——并通过三种方式呈现它们：**气泡通知**、**工具窗口徽标**以及**行内标签**。它使用的是已经轮询到的数据，因此不会产生额外的网络调用。

## 通知气泡

当有事项需要你关注时，屏幕右下角会出现一个带有一键操作的气泡：

![一个提示某个 PR 需要你处理的通知气泡](attention-balloon.png){ width="420" border-effect="line" }

你可以收到以下事项的通知：

- 一个**请你审查**的 PR。
- 一条**@提及你**的评论。
- 你参与过的话题中的一条**回复**。
- 你所创建的 PR 上的**审查者投票变更**。
- 在你推送分支后立即出现的**创建 PR** 的机会。

单个事件会直接打开对应的 PR——审查请求或投票变更时为 **Open pull request**，提及或回复时为 **View comment**（会精确定位到该条评论）。多个事件同时出现时会合并为一个气泡（*"N pull requests need your review"*），其 **Show pull requests** 操作会打开工具窗口。气泡会在你采取操作后或过一会儿自行消失——无需点击任何按钮来清除它们。

## 工具窗口徽标

只要有事项等待你审查，**Pull Requests** 边栏图标就会显示一个徽标圆点，这样即使不打开窗口你也能注意到。（当边栏按钮被选中时，圆点会重新着色以保持可见。）

## 行内关注标签

打开**关注标签**即可直接在列表中看到某个 PR *为何*需要你处理：

![拉取请求行上的关注标签](attention-row-chips.png){ width="640" border-effect="line" }

| 标签 | 含义 |
|------|---------|
| **Review requested** | 你是尚未投票的审查者。 |
| **Mentions you** | 一条评论 @提及了你。 |
| **Replied** | 你参与过的话题中有新的活动。 |

标签**默认关闭**。在 [设置](Settings-zh.md)中通过 **Show attention markers on pull-request rows** 将其打开。将鼠标悬停在标签上可看到 *"Why this pull request wants your attention"* 提示。

> **未读标记**是独立的：一个蓝色圆点标记有新提交*或*有新评论活动的 PR，并在你打开该 PR 的那一刻清除。可从工具窗口的齿轮图标 → **Show unread markers** 切换它。
> {style="note"}

## 调整你收到的通知内容

打开 <ui-path>Settings | Version Control | Azure DevOps</ui-path> → **Polling &amp; notifications**：

| 设置 | 默认值 |
|---------|---------|
| **Notify when I'm asked to review a pull request** | 开 |
| **Notify when someone @mentions me in a pull request** | 开 |
| **Notify on replies in threads I participated in** | 开 |
| **Notify when reviewer votes change on my PRs** | 开 |
| **Offer Create PR after I push to an Azure DevOps remote** | 开 |

你也可以在 <ui-path>Settings | Appearance &amp; Behavior | Notifications</ui-path> 中路由该插件的通知组（弹窗 / 工具窗口 / 仅日志）——参见 [设置](Settings-zh.md#notifications)。
