# 문제 해결

사용자가 가장 자주 겪는 문제에 대한 빠른 해결책입니다. 판단이 필요한 질문("OAuth를 써야 하나 PAT를 써야 하나?", "온프레미스를 지원하나?")은 [FAQ](FAQ-ko.md)를 참고하세요. 여기서 다루지 않는 문제라면 맨 아래의 [버그 신고하기](#filing-a-bug)를 참고하세요.

## 도구 창이 나타나지 않음

Azure DevOps Git 원격이 감지되지 않으면 Pull Requests 도구 창이 숨겨집니다. 다음을 확인하세요:

<procedure>
    <step>프로젝트 루트에서 <code>git remote -v</code>를 실행하세요. 하나 이상의 원격 URL에 <code>dev.azure.com</code> 또는 <code>visualstudio.com</code>(또는 구성한 자체 호스팅 서버)이 포함되어 있어야 합니다.</step>
    <step>번들 <b>Git</b> 플러그인(<code>Git4Idea</code>)이 <ui-path>Settings | Plugins | Installed</ui-path>에서 활성화되어 있는지 확인하세요.</step>
    <step>IDE를 재시작하세요 - 원격 스캔은 프로젝트를 열 때 실행됩니다.</step>
</procedure>

## 로그인 후 "401 Unauthorized"

- PAT에 필요한 범위가 없을 수 있습니다 - [인증](Authentication-ko.md)을 참고하세요. 가장 쉬운 해결책은 **Full access**로 재발급하는 것입니다.
- PAT가 만료되었을 수 있습니다. 토큰은 생성 시 설정한 날짜에 만료됩니다.
- 조직에서 PAT를 비활성화했을 수 있습니다 - 이 경우 OAuth를 사용하세요.

## 특정 작업에서 "403 Forbidden"

PAT는 유효하지만 Azure DevOps 계정에 해당 작업에 대한 권한이 없습니다(예: 풀 리퀘스트를 읽을 수는 있지만 투표는 못 하거나, 병합할 수 없음). Azure DevOps 관리자에게 프로젝트나 리포지토리에 필요한 권한을 부여해 달라고 요청하세요.

## OAuth 브라우저가 IDE로 돌아오지 않음

OAuth는 **로컬 루프백 리디렉션**을 통해 완료됩니다 - 브라우저가 IDE 내장 웹 서버가 제공하는 `http://127.0.0.1:<port>/azure-oauth/callback`로 다시 전송되고, 그런 다음 *"Sign-in complete. You can close this tab."*가 표시됩니다. 이 왕복이 실패하는 경우:

- 방화벽이나 보안 도구가 IDE 내장 서버(포트 범위 **63342–63352**)로의 localhost 연결을 차단하고 있을 수 있습니다.
- 차단된 팝업이나 기본이 아닌 브라우저가 리디렉션을 막을 수 있습니다 - 의도한 브라우저가 기본 브라우저인지 확인하세요.
- 로그인 창에는 **5분** 제한이 있습니다. 만료되었다면 처음부터 다시 시작하세요.

해결책: OAuth 대신 개인용 액세스 토큰(Personal Access Token)을 사용하세요.

## 동기화 후에도 풀 리퀘스트에 새 댓글이 표시되지 않음

<procedure>
    <step><shortcut>⌘R</shortcut> / <shortcut>Ctrl+R</shortcut> / <shortcut>F5</shortcut>를 눌러(또는 마우스 오른쪽 클릭 → <b>Refresh List</b>) 즉시 동기화를 강제하세요 - Reload 도구 모음 버튼은 없습니다.</step>
    <step>동기화 오류가 있는지 <b>idea.log</b>를 확인하세요(자세한 내용은 <a anchor="enabling-debug-logs">디버그 로그 활성화</a>).</step>
    <step>동기화 간격은 기본값이 60초입니다. <a href="Settings-ko.md">Settings</a>에서 이를 늘렸다면 더 긴 지연을 예상하세요.</step>
</procedure>

## diff(변경 내용)에 인라인 댓글이 나타나지 않음

- 플러그인은 **Code (Read)** 권한이 있는 풀 리퀘스트에만 인라인 스레드를 렌더링합니다.
- 풀 리퀘스트가 아닌 로컬 작업 트리에서 diff(변경 내용)를 보고 있다면 인라인 스레드가 렌더링되지 않습니다 - 도구 창에서 풀 리퀘스트를 열어 변경 내용 트리와 스레드를 로드하세요.
- 로컬 브랜치가 풀 리퀘스트 head에서 분기되었다면 편집기 내 리뷰가 자동으로 비활성화됩니다. 변경 사항을 푸시하거나 풀 리퀘스트 head를 정확히 체크아웃하세요.

## Git 푸시가 비밀번호를 요구함 {id="git-push-asks-for-a-password"}

플러그인의 HTTPS 자격 증명 공급자는 **IDE 내부에서** 실행된 Git 작업에만 작동합니다(IDE 내부에서 실행한 터미널은 "내부"로 간주됩니다). 외부 터미널의 경우 시스템 수준 Git 자격 증명 도우미를 구성하세요:

```bash
# macOS Keychain
git config --global credential.helper osxkeychain

# Windows
git config --global credential.helper manager

# Linux (libsecret)
git config --global credential.helper libsecret
```

## AI 기능이 없거나 오류를 반환함

- <ui-path>Settings | Version Control | Azure DevOps | AI Settings</ui-path>를 열고 **Enable AI assistance**가 체크되어 있으며 하나 이상의 공급자가 구성되고 활성화되어 있는지 확인하세요.
- 공급자 행에서 **Test connection**을 클릭하세요 - 실패하면 API 키, 모델 이름, 엔드포인트 URL을 다시 확인하세요.
- **Ollama**의 경우 데몬이 로컬에서 실행 중이고(`ollama serve`) 지정한 모델을 가져왔는지(`ollama list`) 확인하세요.
- **CLI 공급자**(Claude Code, Codex, Copilot CLI)의 경우 바이너리가 `PATH`에 있고 로그인되어 있는지(`claude /login` 등) 확인하세요.
- 공급자의 속도 제한 또는 할당량 오류는 공급자로부터 그대로 전달됩니다 - 재시도되지 않습니다.

## 플러그인 충돌

이 플러그인은 IDE의 `collaboration-tools` 툴킷을 번들 **GitHub** 플러그인 및 **GitLab** 플러그인과 공유합니다. 두 플러그인과 공존합니다 - 독립적인 도구 창, 독립적인 상태. 알려진 상호작용 지점이 두 가지 있습니다:

- 프로젝트에 Azure DevOps 원격과 GitHub 원격이 모두 있으면 두 도구 창이 모두 나타나며, 마우스 오른쪽 클릭 컨텍스트 메뉴에 각각의 작업이 표시될 수 있습니다.
- 타사 플러그인이 AI 확장 지점(`intellij.vcs.azuredevops.aiSummaryExtension` 등, [개인정보 및 데이터](Privacy-and-Data-ko.md) 참고)을 재정의하면 해당 기능에 대해 내장 기본값이 우회됩니다. AI 기능이 예상과 다르게 동작하면 <ui-path>Settings | Plugins</ui-path>에서 EP를 후킹할 수 있는 다른 Azure DevOps 또는 AI 플러그인을 확인하세요.

## 네트워크 시간 초과 또는 "request failed"

이 플러그인은 IntelliJ의 HTTP 프록시 구성을 사용합니다 - 별도의 프록시 설정은 없습니다. 회사 네트워크 제한이 아웃바운드 HTTPS를 차단하는 경우:

- <ui-path>Settings | Appearance &amp; Behavior | System Settings | HTTP Proxy</ui-path>를 확인하세요. 플러그인은 여기서 설정한 것을 그대로 따릅니다.
- AI 스트리밍 요청의 HTTP 시간 제한은 **5분**입니다. 그보다 오래 걸리면 멈춤으로 표시되어 알림으로 보고됩니다.
- Azure DevOps API 호출의 재시도 동작은 "빠른 실패"입니다 - 일시적인 오류는 재시도되지 않으므로 UI에 중복 호출이 쌓이지 않습니다. 60초 백그라운드 동기화가 실패한 요청이 중단된 지점을 이어받습니다.

## 플러그인 업데이트로 무언가가 망가짐

이전 버전으로 롤백하세요:

<procedure>
    <step><ui-path>Settings | Plugins | Installed</ui-path>를 열고 <b>Azure DevOps Pull Requests</b>를 찾으세요.</step>
    <step>기어 아이콘 → <b>Manage Plugin Versions</b>를 클릭하세요.</step>
    <step>이전 버전을 선택해 설치하세요.</step>
    <step>IDE를 재시작하세요.</step>
</procedure>

## 디버그 로그 활성화 {id="enabling-debug-logs"}

더 심층적인 문제 해결을 위해 추적 로깅을 활성화하세요:

<procedure>
    <step><ui-path>Help | Diagnostic Tools | Debug Log Settings…</ui-path>를 여세요.</step>
    <step>다음 줄을 추가하세요:
        <code-block lang="text">
#com.vednovak.azure
#com.vednovak.azure.sync
#com.vednovak.azure.api
        </code-block>
    </step>
    <step>문제를 재현하세요.</step>
    <step><ui-path>Help | Show Log in Explorer/Finder</ui-path>를 열어 <code>idea.log</code>를 찾으세요.</step>
</procedure>

로그는 IDE의 캐시 디렉터리에 있습니다:

<tabs>
    <tab title="macOS">
        <code>~/Library/Logs/JetBrains/&lt;IDE&gt;&lt;Version&gt;/idea.log</code>
    </tab>
    <tab title="Windows">
        <code>&#37;LOCALAPPDATA&#37;\JetBrains\&lt;IDE&gt;&lt;Version&gt;\log\idea.log</code>
    </tab>
    <tab title="Linux">
        <code>~/.cache/JetBrains/&lt;IDE&gt;&lt;Version&gt;/log/idea.log</code>
    </tab>
</tabs>

## 버그 신고하기 {id="filing-a-bug"}

재현 가능한 문제를 발견했다면:

<procedure>
    <step><ui-path>Help | Diagnostic Tools | Collect Logs and Diagnostic Data</ui-path>를 실행하세요.</step>
    <step><a href="%repo_url%/issues/new">새 GitHub 이슈</a>를 열고 다음을 포함하세요:
        <ul>
            <li>IDE 버전(<b>About</b>)</li>
            <li>플러그인 버전</li>
            <li>OS 및 아키텍처</li>
            <li>재현 단계</li>
            <li>예상 동작과 실제 동작</li>
            <li>정리된 <code>idea.log</code> 스니펫(게시 전 토큰 제거)</li>
        </ul>
    </step>
</procedure>

> **공개 이슈에 PAT나 OAuth 갱신 토큰을 절대 붙여넣지 마세요.** 로그는 기본적으로 편집된(redacted) 토큰을 캡처하지만, 제출 전에 항상 다시 확인하세요.
> {style="warning"}
