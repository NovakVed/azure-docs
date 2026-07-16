# 설치

빌드 %min_ide_build% 이상을 실행하는 모든 JetBrains IDE에 %product%을(를) 설치합니다.

> **요약** - <ui-path>Settings | Plugins | Marketplace</ui-path>에서 **Azure DevOps Pull Requests**를 검색하고 **Install**을 클릭한 다음 재시작합니다. 그런 다음 Azure DevOps 원격이 있는 프로젝트를 열고 [로그인](Authentication-ko.md)합니다.
> {style="tip"}

## 지원되는 IDE

이 플러그인은 IntelliJ 플랫폼을 대상으로 하며, 해당 플랫폼을 기반으로 하는 모든 IDE에서 실행됩니다.

- IntelliJ IDEA (Ultimate &amp; Community)
- JetBrains Rider
- PyCharm (Professional &amp; Community)
- WebStorm, PhpStorm, GoLand, RubyMine, CLion, DataGrip, RustRover
- Android Studio (작동할 수 있으나 공식적으로 지원되지 않음)

### 최소 빌드

이 플러그인은 그 시점에 도입된 플랫폼 API를 사용하기 때문에 IDE 빌드 `%min_ide_build%.*` 이상 - 모든 JetBrains IDE의 **%min_ide_version%** 릴리스 - 이(가) 필요합니다.

> **버전 확인:** IDE 메뉴에서 **About**을 열고 `%min_ide_build%`(으)로 시작하는 빌드 번호를 확인하세요. 더 낮다면 먼저 **Help → Check for Updates**를 실행하세요.
> {style="note"}

## Marketplace에서 설치

<procedure title="플러그인 설치">
    <step><ui-path>Settings | Plugins | Marketplace</ui-path>를 엽니다(macOS에서는 <shortcut>⌘,</shortcut>, Windows/Linux에서는 <shortcut>Ctrl+Alt+S</shortcut>).</step>
    <step><b>Azure DevOps Pull Requests</b>를 검색합니다.</step>
    <step><b>Install</b>을 클릭합니다.</step>
    <step>메시지가 표시되면 IDE를 재시작합니다.</step>
</procedure>

![JetBrains Marketplace에서 설치하기](marketplace-install.png){ width="700" border-effect="line" }

### 제대로 설치되었는지 확인

Azure DevOps Git 원격이 있는 프로젝트를 연 다음 확인합니다.

- 왼쪽 도구 창 표시줄에 **Pull Requests** 스트라이프 아이콘이 나타납니다.
- <ui-path>Settings | Version Control | Azure DevOps</ui-path>가 존재합니다.

> **도구 창이 보이지 않나요?** 프로젝트에 **Azure DevOps 원격이 없으면** 숨겨집니다. `git remote -v`를 실행하여 URL에 `dev.azure.com` 또는 `visualstudio.com`이 포함되어 있는지 확인하세요. [문제 해결](Troubleshooting-ko.md)을 참고하세요.
> {style="note"}

## 디스크에서 설치

사전 릴리스 `.zip` 빌드의 경우:

<procedure title="디스크에서 설치">
    <step><ui-path>Settings | Plugins</ui-path>를 엽니다.</step>
    <step>기어 아이콘 → <b>Install Plugin from Disk…</b>을 클릭합니다.</step>
    <step><code>.zip</code>을 선택하고 재시작합니다.</step>
</procedure>

## 시스템 요구 사항

| 구성 요소 | 최소 | 참고 |
|-----------|---------|-------|
| IDE 빌드 | %min_ide_build%.* | JetBrains %min_ide_version% 이상 |
| JDK | 21 | IDE에 번들로 제공 |
| Git | 2.20+ | 브랜치 감지 및 HTTPS 인증 전달 |
| OS | macOS / Windows / Linux | IDE가 지원하는 모든 플랫폼 |
| 네트워크 | Azure DevOps로의 HTTPS | `dev.azure.com` 또는 자체 호스팅 서버 |

> **프록시 뒤에 있나요?** 이 플러그인은 IDE 자체의 HTTP 프록시를 사용합니다. <ui-path>Settings | Appearance &amp; Behavior | System Settings | HTTP Proxy</ui-path>에서 한 번만 설정하면 Azure DevOps와 (HTTP) AI 호출 모두 이를 상속합니다. CLI 기반 AI 제공자는 외부 바이너리이므로 이를 통해 라우팅되지 않습니다.
> {style="note"}

## 필수 번들 플러그인

이 플러그인은 두 개의 IDE 번들 플러그인(모든 곳에서 기본적으로 활성화됨)에 **의존합니다**. 둘 중 하나라도 비활성화되면 플러그인이 로드되지 않으므로 <ui-path>Settings | Plugins | Installed</ui-path>에서 다시 활성화하세요.

- **Git** (`Git4Idea`) - 브랜치 감지 및 HTTPS 자격 증명.
- **Markdown** - 댓글 및 설명 편집기를 구동합니다.

## 업데이트 및 제거

업데이트는 <ui-path>Settings | Plugins | Installed</ui-path>에 표시됩니다. 업데이트가 제공되면 **Update**를 클릭한 다음 새 버전이 완전히 로드되도록 **IDE를 재시작**하세요. 제거하려면 기어 아이콘 → **Uninstall**을 사용하세요. 저장된 자격 증명도 키체인에서 제거됩니다.

> **설치 또는 업데이트 후 재시작하세요.** 이 플러그인은 몇 가지 시작 후크(예: 도구 창 활성화 단축키)를 등록하므로 제자리에서 핫 리로드되지 않습니다. 전체 IDE 재시작을 통해 모든 것이 올바르게 연결되었는지 확인할 수 있습니다.
> {style="note"}

> **다음 단계:** 1분 둘러보기는 [빠른 시작](Quick-Start-ko.md)을, 로그인은 [인증](Authentication-ko.md)을 참고하세요. 요약 및 AI 리뷰를 활성화하려면 [AI 기능](AI-Features-ko.md)을 참고하세요.
> {style="tip"}
