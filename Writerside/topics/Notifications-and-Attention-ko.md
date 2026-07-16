# 알림 및 주목

이 플러그인은 *여러분*을 필요로 하는 풀 리퀘스트, 즉 여러분의 리뷰를 기다리고 있거나 누군가 여러분을 @멘션한 풀 리퀘스트를 감시하여 세 가지 방식으로 표시합니다. **풍선 알림**, **도구 창 배지**, 그리고 **행 칩**입니다. 이미 폴링하는 데이터를 사용하므로 추가 네트워크 호출이 발생하지 않습니다.

## 풍선 알림

무언가 여러분의 주목을 필요로 할 때, 원클릭 동작이 포함된 풍선이 우측 하단에 나타납니다.

![여러분을 필요로 하는 PR에 대한 알림 풍선](attention-balloon.png){ width="420" border-effect="line" }

다음에 대해 알림을 받을 수 있습니다.

- 여러분이 **리뷰를 요청받은** PR.
- 여러분을 **@멘션한** 댓글.
- 여러분이 참여한 스레드의 **답글**.
- 여러분이 작성한 PR의 **리뷰어 투표 변경**.
- 브랜치를 푸시한 직후 **PR을 생성**할 수 있는 기회.

단일 이벤트는 곧바로 PR로 이동합니다. 리뷰 요청이나 투표 변경의 경우 **Open pull request**, 멘션이나 답글의 경우 **View comment**(정확한 댓글 위치로 이동)입니다. 여러 개가 동시에 발생하면 하나의 풍선(*"N pull requests need your review"*)으로 합쳐지며, 이 풍선의 **Show pull requests** 동작이 도구 창을 엽니다. 풍선은 여러분이 동작을 취하거나 잠시 후 스스로 사라지므로, 지우기 위해 클릭할 버튼이 따로 없습니다.

## 도구 창 배지

**Pull Requests** 스트라이프 아이콘은 무언가 여러분의 리뷰를 기다리고 있는 동안 배지 점을 표시하여, 창을 열지 않아도 알아챌 수 있게 합니다. (스트라이프 버튼이 선택된 상태에서도 잘 보이도록 점의 색이 바뀝니다.)

## 행에 표시되는 주목 칩

**주목 칩**을 켜면 PR이 *왜* 여러분을 필요로 하는지 목록에서 바로 확인할 수 있습니다.

![풀 리퀘스트 행에 표시된 주목 칩](attention-row-chips.png){ width="640" border-effect="line" }

| 칩 | 의미 |
|------|---------|
| **Review requested** | 여러분은 아직 투표하지 않은 리뷰어입니다. |
| **Mentions you** | 댓글이 여러분을 @멘션합니다. |
| **Replied** | 여러분이 참여한 스레드에 새로운 활동이 있습니다. |

칩은 **기본적으로 꺼져** 있습니다. [Settings](Settings-ko.md)에서 **Show attention markers on pull-request rows**로 켤 수 있습니다. 칩 위에 마우스를 올리면 *"Why this pull request wants your attention"* 툴팁이 표시됩니다.

> **읽지 않음 표시**는 별개입니다. 파란 점은 새 커밋 *또는* 새 댓글 활동이 있는 PR을 표시하며, PR을 여는 순간 사라집니다. 도구 창 톱니바퀴 → **Show unread markers**에서 전환할 수 있습니다.
> {style="note"}

## 알림 받을 항목 조정

<ui-path>Settings | Version Control | Azure DevOps</ui-path> → **Polling &amp; notifications**를 엽니다.

| 설정 | 기본값 |
|---------|---------|
| **Notify when I'm asked to review a pull request** | 켜짐 |
| **Notify when someone @mentions me in a pull request** | 켜짐 |
| **Notify on replies in threads I participated in** | 켜짐 |
| **Notify when reviewer votes change on my PRs** | 켜짐 |
| **Offer Create PR after I push to an Azure DevOps remote** | 켜짐 |
| **Include my own pull requests and @mentions** | 꺼짐 |

> **혼자 테스트 중이신가요?** **Include my own pull requests and @mentions**를 켜면 여러분 자신의 활동에서 발생하는 주목 신호를 확인할 수 있습니다. 리포지토리에 여러분 혼자만 있을 때 유용합니다.
> {style="tip"}

<ui-path>Settings | Appearance &amp; Behavior | Notifications</ui-path>에서 플러그인의 알림 그룹(팝업 / 도구 창 / 로그 전용)을 라우팅할 수도 있습니다. [Settings](Settings-ko.md#notifications)를 참조하세요.
