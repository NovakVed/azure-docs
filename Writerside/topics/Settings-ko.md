# 설정

플러그인이 제공하는 모든 설정에 대한 참조입니다. <shortcut>⌘,</shortcut>(macOS) 또는 <shortcut>Ctrl+Alt+S</shortcut>(Windows/Linux)로 **Settings**를 엽니다.

## Version Control → Azure DevOps

기본 페이지입니다. 상단에는 **accounts** 패널(추가 **+**, 편집 ✏, 제거 ✕, 프로젝트별 기본값)이 있습니다 - [인증](Authentication-ko.md)을 참조하세요.

![Azure DevOps 설정 페이지의 계정 패널](accounts-panel.png){ width="700" border-effect="line" }

- **Sync interval (seconds)** - 도구 창이 Azure DevOps를 폴링하는 주기입니다. **기본값 60**, 범위 **15–3600**.

### Polling & notifications

| 설정 | 기본값 |
|---------|---------|
| **Notify when I'm asked to review a pull request** | On |
| **Notify when someone @mentions me in a pull request** | On |
| **Notify on replies in threads I participated in** | On |
| **Notify when reviewer votes change on my PRs** | On |
| **Offer Create PR after I push to an Azure DevOps remote** | On |

이 설정들이 무엇을 제어하는지는 [알림 및 주의](Notifications-and-Attention-ko.md)를 참조하세요.

### Pull request review

| 설정 | 기본값 |
|---------|---------|
| **Mark files as viewed when their diff is opened** | Off |
| **Show attention markers on pull-request rows** | Off |
| **Show keyboard shortcut on comment buttons** | On |

마지막 토글은 컴포저의 **Comment** / **Reply** / **Save** 버튼 레이블 바로 앞에 제출 단축키(<shortcut>⌘↵</shortcut> / <shortcut>Ctrl+Enter</shortcut>)를 표시합니다. 단축키는 어느 쪽이든 작동하며 - 이 설정은 힌트 표시 여부만 제어합니다.

> **Show unread markers**는 여기에 없습니다 - 이것은 설정 체크박스가 아니라 도구 창 토글(기어 메뉴)입니다. 초안(Drafts)은 설정이 아니라 목록 **필터**입니다.
> {style="note"}

### Go to Pull Requests

| 설정 | 기본값 |
|---------|---------|
| **Show in the Search Everywhere window** | On |

**Go to Pull Requests**가 열리는 방식을 제어합니다. 켜져 있으면 이 액션이 Search Everywhere에 **Pull Requests** 탭을 추가합니다(Files / Symbols / Actions 옆). 체크를 해제하면 대신 독립형 빠른 선택 대화 상자가 열립니다.

## Version Control → Azure DevOps → AI Settings

선택적 AI 도우미를 구성하는 하위 페이지입니다 - [AI 기능](AI-Features-ko.md)을 참조하세요.

![AI Settings 페이지](ai-settings.png){ width="720" border-effect="line" }

- **General AI Settings → Enable AI assistance** - 마스터 스위치입니다. **기본값 off.** 꺼져 있으면 모든 AI 요소가 숨겨지고 외부로 나가는 호출이 전혀 발생하지 않습니다.
- **AI Providers** - 공급자 인스턴스마다 한 행씩 표시됩니다(**Provider / Model / Enabled**). 활성화된 첫 번째 행이 기본값입니다. **Add AI Provider** 대화 상자를 통해 추가합니다(OpenAI, Claude, Gemini, Ollama, GitHub Copilot; HTTP-API 또는 CLI 모드).
- **Per-Feature Provider** - **AI Summary**, **AI Review**, **Title + Description**, **Explain Code**를 특정 인스턴스로 라우팅하거나 **Default**로 둡니다.
- **Configure Prompts** - 각 기능의 시스템 프롬프트를 편집합니다.
- **Advanced** - **Cache AI responses per commit SHA**(기본 on), **Max diff size**(기본 200 KB, 범위 10–2000), **Clear AI Response Cache**.

## Appearance & Behavior → Notifications {id="notifications"}

플러그인은 라우팅할 수 있는 두 개의 알림 그룹(popup / tool window / log-only)을 등록합니다:

| 그룹 | 대상 |
|-------|-----|
| **Azure DevOps Pull Requests** | 리뷰 요청, @멘션, 답글, 투표 변경, 푸시 제안. |
| **Azure DevOps AI** | AI 요약 / 리뷰 완료 풍선 알림. |

## Keymap

<ui-path>Settings | Keymap</ui-path>을 열고 **Azure DevOps**를 검색하여 아무 액션이나 다시 바인딩합니다. 액션 ID가 포함된 전체 목록은 [키보드 단축키](Keyboard-Shortcuts-ko.md)에 있습니다.

## Per-project vs application-level

대부분의 설정은 **애플리케이션 수준**(모든 프로젝트에 적용)입니다: 계정, 알림 기본 설정, AI 공급자. 두 가지는 **프로젝트별**(프로젝트의 워크스페이스에 저장)입니다: **default account**와 **PR 목록 필터**.
