# 코드 리뷰

IntelliJ의 기본 diff(변경 내용) 뷰어로 풀 리퀘스트를 리뷰합니다. 변경 내용을 읽고, 인라인 댓글과 제안을 남기고, 투표하고, 확인한 파일을 추적합니다.

## 상세 보기

PR을 열면 닫을 수 있는 에디터 탭이 생성됩니다. 하위 탭이 없는 **단일 창**입니다. 위에서 아래로: 제목과 `!`-번호에 딸린 **View Timeline** 링크, 소스 → 대상 브랜치, 상태 체크(CI, 충돌, 필수 리뷰어와 그들의 투표), **변경된 파일 트리**, 그리고 액션 바 순서입니다.

![단일 창 상세 보기에 열린 풀 리퀘스트](pr-detail.png){ width="720" border-effect="line" }

- **변경된 파일**은 트리에 있습니다. 파일을 클릭하면 diff가 열립니다.
- **Discussion**은 **View Timeline** 링크를 통해 자체 탭에서 열립니다. [토론 및 댓글](Discussions-and-Comments-ko.md)을 참조하세요.
- **투표와 액션**은 액션 바와 오버플로 메뉴에 있습니다. [풀 리퀘스트](Pull-Requests-ko.md#open-and-act-on-a-pr)를 참조하세요.

## diff 읽기

파일을 클릭하면 PR당 하나의 탭에서 diff가 열립니다. 다른 파일을 클릭하면 같은 자리에서 교체되므로, <shortcut>F7</shortcut> / <shortcut>⇧F7</shortcut>로 PR 전체의 모든 변경 범위를 하나씩 넘어갈 수 있습니다. diff 탭에는 **Refresh**, **Submit review**, **Previous / Next Comment**가 있는 **Review:** 도구 모음이 함께 표시됩니다.

| 이동 | macOS | Windows / Linux |
|----------|-------|------------------|
| 다음 / 이전 변경 범위 | <shortcut>F7</shortcut> / <shortcut>⇧F7</shortcut> | <shortcut>F7</shortcut> / <shortcut>Shift+F7</shortcut> |
| 다음 / 이전 댓글 | *Review: 도구 모음* | *Review: 도구 모음* |

### 스레드 표시 또는 숨기기

diff의 여백(gutter) 설정에서 **Review Discussions** 메뉴는 어떤 인라인 스레드를 렌더링할지 제어합니다: **Show all discussions**, **Show only unresolved**, 또는 **Don't show**.

## 한 줄에 댓글 달기

<procedure title="인라인 댓글 추가하기">
    <step>변경된 줄의 여백에 마우스를 올리면 <b>+</b>가 나타납니다. 이를 클릭하세요(또는 줄 번호를 가로질러 드래그하면 범위를 지정할 수 있습니다). 캐럿 위치에서 <shortcut>⌃⇧M</shortcut> / <shortcut>Ctrl+Shift+M</shortcut>을 눌러도 됩니다.</step>
    <step>댓글을 입력하세요. 편집기(composer)는 PR 토론과 동일한 GitHub 스타일 UI를 사용합니다. 상단에 서식 도구 모음이 있는 <b>Write</b> / <b>Preview</b> 탭 스트립과 @멘션, 이미지 붙여넣기를 지원합니다. 편집기 전체에 대한 내용은 <a href="Discussions-and-Comments-ko.md">토론 및 댓글</a>을 참조하세요.</step>
    <step>분할 제출 버튼으로 게시하세요. 기본 액션은 <b>Start Review</b>로, 댓글을 보류 중인 리뷰의 일부로 대기열에 넣습니다. 드롭다운에는 <b>Add Single Comment</b>(즉시 게시)와 <b>Suggest change</b>(선택 영역을 작성자가 적용할 수 있는 제안된 변경으로 감싸기)가 있습니다.</step>
</procedure>

![diff 뷰어에 열린 인라인 댓글](diff-comment.png){ width="720" border-effect="line" }

> **보류 중인 리뷰.** 대기열에 넣은 댓글은 투표와 함께 제출할 때까지 초안 상태로 유지됩니다(**Submit (N)** 버튼에 개수가 표시됨). 이는 GitHub 사용자에게 익숙한 리뷰 흐름과 동일합니다. **Review:** 도구 모음이나 오버플로 메뉴의 **Submit Pending Comments**에서 제출하세요.
> {style="note"}

### 코드 링크 복사

diff 뷰어에서(또는 에디터에서 리뷰 중일 때 일반 에디터에서) 줄을 마우스 오른쪽 버튼으로 클릭하고 **Copy Link to Code**를 선택하면 해당 코드(파일, 줄, 열 범위)에 대한 Azure DevOps 웹 딥링크가 복사됩니다. 이는 웹 UI의 **Copy link**가 생성하는 것과 동일한 링크입니다. 텍스트를 선택한 상태에서는 항목이 **Copy Link to Selected Code**로 표시되어 정확한 문자 범위를 링크하고, 선택하지 않은 상태에서는 캐럿 위치의 줄 전체 링크를 복사합니다. 단축키는 <shortcut>⌘⇧L</shortcut> / <shortcut>Ctrl+Shift+L</shortcut>입니다.

> 이 액션은 Azure PR 리뷰 화면(diff 뷰어 또는 에디터 리뷰 화면) 안에서만 나타납니다. 일반 에디터에서는 숨겨진 상태로 유지됩니다.
> {style="note"}

## 투표

액션 바의 **Approve** 버튼은 분할 버튼입니다. 드롭다운에는 **Approve with suggestions**, **Wait for author**, **Reject**, **Reset feedback**가 있습니다.

![Approve 분할 버튼의 투표 옵션](vote-approve-dropdown.png){ width="380" border-effect="line" }

병합 전략을 포함한 PR 완료 또는 취소는 [풀 리퀘스트](Pull-Requests-ko.md#complete-a-pull-request)에서 다룹니다.

## 확인한 파일 추적

대규모 PR의 경우 진행하면서 각 파일을 **viewed**로 표시하세요. 확인한 파일은 변경 트리에서 흐리게 표시됩니다.

- <shortcut>⌘⇧S</shortcut> / <shortcut>Ctrl+Shift+S</shortcut>를 누르거나, 마우스 오른쪽 버튼 클릭 → **Mark File as Viewed**를 선택하세요.
- 여러 파일을 선택한 상태에서 마우스 오른쪽 버튼을 클릭하면 **Mark All as Viewed**를 사용할 수 있습니다.

![변경 트리의 Mark File as Viewed](mark-file-viewed.png){ width="560" border-effect="line" }

> 파일을 열 때 자동으로 viewed로 표시되게 하고 싶으신가요? [설정](Settings-ko.md)에서 **Mark files as viewed when their diff is opened**를 켜세요(GitHub과 동일하게 기본값은 꺼짐).
> {style="tip"}

## 업데이트 이후 변경된 내용만 리뷰 {id="compare"}

작성자가 새 커밋을 푸시하면 PR 전체를 다시 읽을 필요가 없습니다. 오버플로 **⋮** 메뉴에서 **Review Changes Since…**를 선택하고 업데이트를 고르면, 변경 트리가 해당 diff만으로 다시 범위가 좁혀집니다. 그 사이에 병합된 대상 브랜치 커밋은 걸러집니다.

![변경 트리 위의 반복(iteration) 범위 배너](compare-updates-banner.png){ width="700" border-effect="line" }

트리 위에 *"Reviewing only what changed since update N"* 배너가 표시됩니다. **Show all changes**를 클릭하면 전체 PR로 돌아갑니다. (이 액션은 PR에 업데이트가 두 개 이상 있을 때 나타납니다.)

## 에디터에서 리뷰하기

PR의 소스 브랜치가 체크아웃되어 있으면, diff 탭 없이 일반 에디터에서 변경된 줄에 바로 댓글을 달 수 있습니다. [에디터에서 리뷰](Review-in-Editor-ko.md)를 참조하세요.
