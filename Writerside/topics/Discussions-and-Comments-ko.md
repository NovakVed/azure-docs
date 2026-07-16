# 토론 및 댓글

IDE를 벗어나지 않고 풀 리퀘스트에서 완전한 대화를 나눠 보세요. 마크다운 편집기, @멘션, 작업 항목 및 PR 참조, 제안 편집, 이미지 첨부, AI 문법 다듬기, 스레드 해결 기능을 제공합니다.

## 스레드가 표시되는 위치

동일한 스레드가 세 곳에 표시됩니다.

- **diff(변경 내용) 내 인라인** - 참조하는 줄에 고정됩니다. [코드 리뷰](Code-Review-ko.md)를 참조하세요.
- **타임라인** - 모든 스레드와 PR 이벤트를 시간순으로 보여 줍니다. PR 세부 정보 보기의 **View Timeline** 링크에서 엽니다. (**Find in timeline**으로 검색할 수 있습니다.)
- **편집기 내** - PR의 브랜치를 체크아웃하면 평소 편집기 위에 겹쳐서 표시됩니다. [편집기에서 리뷰](Review-in-Editor-ko.md)를 참조하세요.

## 댓글 편집기

모든 댓글 편집기 - 타임라인, diff 인레이, 인라인 편집, Create-PR 설명 - 는 하나의 GitHub 스타일 작성기를 공유합니다. **Write | Preview** 탭 스트립이 왼쪽 상단에 있고, 서식 도구 모음은 같은 상단 스트립을 따라 탭 옆 오른쪽 끝에 붙어 있으며, **Polish grammar &amp; spelling with AI**가 구분선 뒤 맨 오른쪽에 고정되어 있습니다. 흐리게 표시된 **Add files** 링크는 제출 버튼 왼쪽의 맨 아래 행에 있습니다.

![Write | Preview 탭과 상단 서식 도구 모음 스트립, 그리고 제출 버튼 옆 맨 아래 행의 Add files 링크가 있는 댓글 작성기](comment-toolbar.png){ width="640" border-effect="line" }

| 그룹 | 버튼 |
|-------|---------|
| **References** | Mention user (`@`), Reference work item (`#`), Reference pull request (`!`) |
| **Formatting** | Heading, Bold, Italic, Inline code, Link |
| **Lists** | Bulleted, Numbered, Task list |
| **AI** | **Polish grammar &amp; spelling with AI** |

diff/편집기 인레이에서는 **Insert code suggestion**도 사용할 수 있습니다. 키보드: <shortcut>⌘B</shortcut> 굵게, <shortcut>⌘I</shortcut> 기울임, <shortcut>⌘E</shortcut> 인라인 코드, <shortcut>⌘K</shortcut> 링크, <shortcut>⌘↵</shortcut> 제출 (또는 <shortcut>Ctrl</shortcut> 조합).

**Preview**를 클릭하면 편집기가 마크다운의 렌더링된 보기로 바뀝니다 - 게시된 댓글에 사용되는 것과 동일한 렌더링이므로 미리 보는 내용이 게시될 내용과 일치합니다. Preview가 표시되는 동안에는 서식 도구 모음이 숨겨집니다. 편집으로 돌아가려면 **Write**를 클릭하세요. 비어 있는 초안은 *Nothing to preview*로 미리 표시됩니다.

> **Polish grammar &amp; spelling with AI**는 초안(또는 선택 영역)을 하나의 실행 취소 가능한 편집으로 제자리에서 다시 씁니다. [AI 공급자 구성](AI-Features-ko.md)이 필요하며, AI가 꺼져 있으면 버튼이 숨겨집니다.
> {style="tip"}

## @멘션

**Mention user**를 클릭하거나 `@`를 입력하면 조직 내 사람들의 자동 완성이 열립니다. 화살표 키와 <shortcut>Enter</shortcut>로 한 명을 선택하세요. 멘션된 사용자는 Azure DevOps 알림을 받습니다.

기존 `@mention`을 클릭하면 해당 사람의 아바타와 이름이 담긴 작은 **author card**가 열립니다. 이메일을 알 수 있는 경우(PR 작성자 또는 리뷰어), 카드에서 **Copy email**과 **Send email**을 제공합니다.

> @멘션 자동 완성에는 **Identity (Read)** 범위(PAT) 또는 **Full access**(OAuth)가 필요합니다. [인증](Authentication-ko.md)을 참조하세요.
> {style="note"}

## 이미지 및 첨부 파일

이미지를 첨부하는 세 가지 방법:

- **Add files** - 맨 아래 행(제출 버튼 왼쪽)의 **Add files** 링크를 클릭하여 디스크에서 이미지 파일을 선택합니다.
- 클립보드에서 이미지 **붙여넣기**(<shortcut>⌘V</shortcut> / <shortcut>Ctrl+V</shortcut>).
- 이미지 파일을 편집기로 **끌어서 놓기**.

지원되는 형식은 `png`, `jpg`, `jpeg`, `gif`, `webp`, `bmp`, `svg`입니다. 각 업로드는 *Uploading…* 자리 표시자를 표시한 다음 인라인 마크다운 이미지가 됩니다. 게시된 이미지를 마우스 오른쪽 버튼으로 클릭하면 **Copy Image Link** 또는 **Download Image…**를 사용할 수 있습니다.

## 제안 편집

변경 사항을 설명하는 대신 구체적인 변경을 제안하려면 **suggestion**을 사용하세요. diff/편집기 인레이에서 **Insert code suggestion**을 클릭하거나(댓글이 달린 줄을 미리 채웁니다) ```` ```suggestion ```` 블록을 입력하세요.

![Apply Locally 작업이 있는 제안된 변경](suggestion-block.png){ width="560" border-effect="line" }

스레드는 **Apply Locally**(그리고 한 단계로 적용하고 커밋하는 **Commit…**)가 있는 **Suggested change** 카드를 렌더링합니다. Apply는 PR 브랜치가 체크아웃되기 전과 해결된 스레드에서는 비활성화됩니다.

## 답글, 해결 및 스레드 관리

- **Reply** - 후속 내용을 추가합니다. Azure DevOps 스레드는 플랫 구조이므로 답글이 스레드 끝에 추가됩니다.
- **Resolve / Reopen** - 완료되면 스레드를 닫거나 다시 엽니다. 해결된 스레드는 강조가 약화되며, diff 필터가 *Show only unresolved*로 설정되면 숨겨집니다.
- **👍 Thumbs up** - 댓글 본문 아래 반응 행에 있는 좋아요 버튼입니다(리뷰 스레드에서는 **Reply** / **Resolve**와 공유). 좋아요가 하나 이상 있으면 개수를 표시하고, 좋아요를 누르면 금색으로 바뀝니다. 툴팁은 **Thumbs up**과 **Remove thumbs up** 사이를 전환합니다.
- **More actions (⋯)** - 댓글 헤더의 오버플로 메뉴입니다. 모든 댓글에서: **Copy link**, **Copy Markdown**, **Quote reply**(댓글을 이 스레드의 답글 편집기에 `>` 블록 인용으로 삽입)와 **Hide** - 본문을 제자리에서 접고 다시 빌드나 재시작 후에도 유지되는 로컬 전용 접기 기능입니다. 자신의 댓글에서는 **Edit**와 **Delete**도 사용할 수 있습니다.

### 스레드 상태

해결/미해결 외에도 스레드에는 상태 칩이 있습니다. 이를 클릭하여(**Change status**) 다음 사이를 전환합니다.

| 상태 | 의미 |
|--------|---------|
| **Active** | 새 스레드(칩이 표시되지 않음). |
| **Pending** | 작성자의 변경을 기다리는 중. |
| **Resolved** | 변경이 적용됨. |
| **Won't fix** | 확인했지만 변경을 반영하지 않음. |
| **Closed** | 토론 완료, 조치 없음. |

## 타임라인 이벤트

타임라인은 댓글과 함께 시스템 이벤트도 표시합니다. 투표 변경, 리뷰어 추가/제거, 작업 항목 연결/연결 해제, 완료된 상태 검사, 강제 푸시(커밋 비교 링크 포함) 등입니다.
