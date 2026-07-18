# 풀 리퀘스트

**Pull Requests** 도구 창은 여러분의 명령 센터입니다. 대기열을 탐색하고, 필터링 및 검색하고, PR을 열고, 그에 대해 작업할 수 있습니다 - 완료, 되돌리기, 비교 등.

## 도구 창 열기

도구 창은 열린 프로젝트에 Azure DevOps Git 원격이 하나 이상 있을 때마다 왼쪽 사이드바에 나타납니다. (Azure DevOps 원격이 없나요? 어수선함을 줄이기 위해 숨겨진 상태로 유지됩니다.)

- 사이드바에서 **Pull Requests** 스트라이프 아이콘을 클릭합니다.
- 또는 <ui-path>View | Tool Windows | Pull Requests</ui-path>를 사용합니다.
- 또는 *Find Action*(<shortcut>⌘⇧A</shortcut> / <shortcut>Ctrl+Shift+A</shortcut>)을 실행하고 **Pull Requests**를 입력합니다.

![검색 필드, 필터 칩, 그리고 항목이 채워진 목록이 있는 Pull Requests 도구 창](pr-tool-window.png){ width="720" border-effect="line" }

## 풀 리퀘스트 찾기

### 기본 보기: 나의 것

활성 필터가 없으면 목록에는 Azure DevOps 웹의 **Mine** 탭이 보여주는 것과 정확히 동일한 내용이 표시됩니다 - 여러분이 **생성**했거나, **여러분에게 할당**되었거나, **여러분의 팀 중 하나에 할당**된 활성 PR들. 이것은 여러분이 처음 도착하는 보기이며, *Clear filters*가 여러분을 되돌려 보내는 보기입니다.

칩, 프리셋 또는 검색을 선택하면 목록이 전체 집합으로 전환됩니다. 이들을 지우면 다시 나의 것으로 돌아옵니다.

> 팀에 할당된 PR에는 올바른 [권한](Permissions-ko.md)이 필요합니다. 여러분의 자격 증명이 팀 멤버십을 읽을 수 없는 경우, 플러그인이 한 번 알려줍니다 - 보기의 나머지 부분은 계속 작동합니다.
> {style="note"}

### Quick Filters

칩 행의 왼쪽에 있는 **필터 아이콘**을 클릭하면 원클릭 프리셋을 사용할 수 있습니다. 아이콘의 배지는 활성 필터가 몇 개인지 보여줍니다.

![프리셋이 있는 Quick Filters 메뉴](quick-filters-menu.png){ width="380" border-effect="line" }

| 프리셋 | 표시 내용 |
|--------|-----------|
| **All pull requests** | 모든 것 - 기본 "나의 것" 보기에서 벗어나기 |
| **Open pull requests** | 모든 활성 PR |
| **Awaiting my review** | 여러분이 아직 투표하지 않은 리뷰어로 지정된 PR |
| **Involving me** | 여러분이 작성했거나, 리뷰하거나, 언급된 PR |
| **Clear N filter(s)** | 모든 활성 필터를 재설정 - 기본 "나의 것" 보기로 복귀 |

### 필터 칩

검색 필드 아래에 스크롤 가능한 칩 행이 있습니다. 아무 칩이나 클릭하여 목록을 세분화하세요:

| 칩 | 옵션 |
|------|------|
| **State** | Active · Completed · Abandoned |
| **Author** | 사용자 전체에 대한 타이핑 즉시 검색 |
| **Tags** | Azure DevOps PR 레이블(태그) |
| **Assignee** | 사용자 전체에 대한 타이핑 즉시 검색 |
| **Review** | Approved · Approved with suggestions · Waiting for author · Rejected · Awaiting my review |
| **Work Items** | 연결된 Azure Boards 작업 항목 |
| **Draft** | 초안만 · 초안이 아닌 것만 |
| **Sort** | Newest · Oldest · Most/Least commented · Recently/Least recently updated |

필터는 IDE를 다시 시작해도 **프로젝트별로** 유지됩니다. 이를 지우려면 Quick Filters 메뉴의 **Clear N filter(s)**를 사용하세요.

> **검색** - 칩 위의 필드에 입력하여 PR 제목, 번호, 작성자 및 브랜치 이름을 일치시킵니다. <shortcut>⇧ Shift</shortcut>를 두 번 눌러 *Search Everywhere*를 여세요. 여기에 Azure DevOps PR도 나타나며 - 하나를 선택하면 바로 열립니다.
> {style="tip"}

### 특정 PR로 이동 {id="jump-to-a-specific-pr"}

원하는 PR을 이미 알고 있을 때는 목록을 건너뛰세요. **Go to Pull Requests…**는 캐시된 모든 PR을 **id, 제목, 작성자 또는 리포지토리**로 퍼지 검색하여 해당 타임라인에서 바로 엽니다. 빈 검색은 캐시된 모든 PR을 나열합니다(읽지 않은 것 먼저, 그다음 최신순).

- <shortcut>⌘⇧P</shortcut> / <shortcut>Ctrl+Shift+P</shortcut>를 누릅니다.
- 또는 <ui-path>VCS | Go to Pull Requests…</ui-path>를 사용합니다.
- 또는 *Find Action*(<shortcut>⌘⇧A</shortcut> / <shortcut>Ctrl+Shift+A</shortcut>)을 실행하고 **Go to Pull Requests**를 입력합니다.

기본적으로 IDE의 *Search Everywhere* 팝업에서 Files, Symbols, Actions 옆에 **Pull Requests** 탭을 엽니다. <shortcut>↵ Enter</shortcut>를 눌러 강조 표시된 PR을 여세요.

![Go to Pull Requests 결과: Search Everywhere의 Pull Requests 탭](go-to-pr-popup.png){ width="560" border-effect="line" }

> 전용 대화 상자를 선호하시나요? [Settings](Settings-ko.md)에서 **Show in the Search Everywhere window**를 **끄면** 이 작업이 대신 자체 빠른 선택 팝업을 엽니다 - 옆에 상태 **깔때기(funnel)**가 있는 검색 필드와 <shortcut>↵</shortcut> 열기 / <shortcut>⎋</shortcut> 닫기 키를 갖춘 팝업입니다.
> {style="tip"}

## PR 행 읽기 {id="read-a-pr-row"}

각 행에는 상태가 한눈에 보이도록 담겨 있습니다:

![풀 리퀘스트 행의 구조](pr-row-anatomy.png){ width="640" border-effect="line" }

- **제목과 `!`-번호**, 그리고 관련이 있을 때 **상태 알약(pill)**: *Draft*, *Merged*, *Abandoned* 또는 *Has merge conflicts*.
- **리뷰어 투표 아이콘** - approved, approved-with-suggestions, waiting 또는 rejected.
- **스레드 수(그리고 아직 미해결인 개수)를 표시하는 호박색 토론 배지**.
- **주의 칩(Attention chips)** - *Review requested*, *Mentions you* 또는 *Replied* - PR이 여러분의 주의를 원할 때 표시됩니다. 이들은 기본적으로 꺼져 있습니다. 켜는 방법은 [Notifications &amp; Attention](Notifications-and-Attention-ko.md)을 참조하세요.

읽지 않은 PR에는 새 커밋 *및* 새 댓글 활동에 반응하는 파란색 **읽지 않음 표시** 점이 나타날 수 있습니다. 도구 창의 톱니바퀴 → **Show unread markers**에서 토글하세요.

## PR 열기 및 작업 {id="open-and-act-on-a-pr"}

PR을 **클릭**하면 에디터 탭에서 단일 창 상세 보기가 열립니다. 하단의 작업 표시줄은 여러분의 역할에 맞게 조정됩니다:

| 여러분의 역할… | 기본 작업 |
|----------------|-----------|
| **리뷰어** | **Approve ▾**(분할 버튼: Approve with suggestions, Wait for author, Reject, Reset feedback) |
| **작성자, 리뷰 필요** | **Request review** |
| **작성자, 리뷰 완료됨** | **Complete ▾**(Set auto-complete…, Mark as draft, Abandon) |
| **관여하지 않음** | **Set myself as reviewer** |

모든 상태에서는 전체 작업 세트를 갖춘 **⋮**(More) 메뉴도 표시됩니다:

![PR 작업 표시줄 오버플로 메뉴](pr-overflow-menu.png){ width="440" border-effect="line" }

| 작업 | 하는 일 |
|------|---------|
| **Share Pull Request…** | PR을 사람들에게 이메일로 보냅니다(리뷰어 추가 없음, 댓글 게시 없음) |
| **Submit Pending Comments (N)** | 대기시켜 둔 댓글을 리뷰로 게시합니다(N > 0일 때만) |
| **Restart Merge** | 멈춘 병합을 다시 대기열에 넣습니다(충돌 / 실패 / 정책 거부) |
| **Change Target Branch…** | PR을 다른 대상 브랜치로 다시 지정합니다 |
| **Cherry-Pick…** | 이 PR의 커밋을 다른 브랜치에 체리픽한 브랜치를 만듭니다 |
| **Review Changes Since…** | diff(변경 내용)를 선택한 업데이트 이후 변경된 내용으로 다시 범위 지정합니다 - [Code Review](Code-Review-ko.md#compare) 참조 |
| **Revert…** | *(병합된 PR)* 이 PR의 변경 내용을 되돌리는 브랜치를 만듭니다 |
| **Open on Web** · **Copy Link** | dev.azure.com URL로 이동 / 복사합니다 |
| **Summarize Pull Request** · **Run AI Review** | [AI 지원](AI-Features-ko.md) |

### 풀 리퀘스트 완료 {id="complete-a-pull-request"}

**Complete**를 클릭하면 **Complete Pull Request** 대화 상자가 열립니다. **Merge type**을 선택하세요 - 실시간 다이어그램이 결과적으로 만들어지는 히스토리 형태를 보여줍니다:

![병합 전략 다이어그램이 있는 Complete Pull Request 대화 상자](complete-pr-dialog.png){ width="560" border-effect="line" }

- **Merge (no fast forward)** · **Squash commit** · **Rebase and fast-forward** · **Semi-linear merge**
- **완료 후 옵션:** 연결된 작업 항목 완료, 소스 브랜치 삭제, 그리고 선택적으로 병합 커밋 메시지 사용자 지정.

> **브랜치 정책이 준수됩니다.** 필수 리뷰어 또는 상태 검사가 충족되지 않으면 대화 상자에 차단 요소가 나열됩니다. 우회 권한을 보유한 경우에만 **Override branch policies and enable merge**(필수 사유 포함)를 사용할 수 있습니다.
> {style="warning"}

행을 마우스 오른쪽 버튼으로 클릭하면 빠른 작업도 가능합니다: **View Pull Request**, **View Pull Request in Browser**, **Copy Pull Request URL**, 그리고 **Refresh List**.

## 풀 리퀘스트 만들기

도구 창 툴바에서 **+**(Create Pull Request)를 클릭합니다. 양식은 소스 브랜치(현재 브랜치)와 기본 대상 브랜치를 미리 채웁니다.

![Create Pull Request 양식: Write/Preview 설명 작성기와 리뷰어, 태그, 작업 항목 행](create-pr-ai.png){ width="640" border-effect="line" }

**설명**은 PR 댓글과 동일한 작성기를 사용합니다: **Write | Preview** 탭 스트립과 에디터 위의 서식 도구 모음. `@`, `#` 또는 `!`를 입력하면 사람, 작업 항목, PR을 인라인 자동 완성할 수 있습니다. <shortcut>⌘↵</shortcut> / <shortcut>Ctrl+Enter</shortcut>를 눌러 만드세요.

설명 아래의 메타데이터 블록은 네 개의 인라인 행입니다 - 각 행에는 편집용 연필이 있고, 표시된 곳에는 지우기용 **X**가 있습니다:

| 행 | 설정하는 내용 |
|-----|---------------|
| **Required reviewers** | 반드시 리뷰해야 하는 사람들 |
| **Optional reviewers** | 리뷰하도록 초대된 사람들 |
| **Tags** | Azure DevOps PR 레이블 - 기존 항목을 선택하거나 **+**를 사용하여 완전히 새로운 태그를 만듭니다 |
| **Work items** | 연결된 Azure Boards 작업 항목 |

기본 버튼은 분할 버튼입니다: **Create Pull Request**, 그리고 드롭다운에 **Create Draft Pull Request**.

> [AI가 활성화](AI-Features-ko.md)되면 설명 작성기 도구 모음에 여러분 브랜치의 커밋에서 제목과 설명 초안을 작성해 주는 AI 버튼(툴팁 **Generate title &amp; description with AI**)이 추가됩니다. 아직 AI 공급자가 설정되지 않은 경우, 클릭하면 AI Settings를 열도록 제안합니다.
> {style="tip"}

## 새로 고침 및 백그라운드 동기화

Azure DevOps에는 웹훅이 없으므로 플러그인이 폴링합니다. 목록은 자체적으로 업데이트되지만, 필요에 따라 새로 고칠 수 있습니다:

- 도구 창에 포커스가 있는 동안 <shortcut>⌘R</shortcut> / <shortcut>Ctrl+R</shortcut> 또는 <shortcut>F5</shortcut>를 누릅니다.
- 또는 행을 마우스 오른쪽 버튼으로 클릭 → **Refresh List**.

> 폴링 주기는 [Settings](Settings-ko.md)의 **Sync interval**입니다(기본값 60초). 콜드 스타트 시에는 첫 동기화가 실행되는 동안 목록에 **마지막으로 알려진 캐시 상태**가 표시되므로, 스피너를 기다리는 대신 즉시 작업할 수 있습니다.
> {style="note"}

## 계정 또는 리포지토리 전환

여러 조직 또는 리포지토리에 바인딩된 프로젝트의 경우, 도구 창의 톱니바퀴 → **Switch Account / Repository…**를 사용하세요. 현재 브랜치의 PR은 Git 브랜치 위젯과 상태 표시줄에도 표시됩니다 - [Git Integration](Git-Integration-ko.md)을 참조하세요.
