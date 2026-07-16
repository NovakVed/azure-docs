# Git 통합

이 플러그인은 IDE에 번들로 포함된 Git 플러그인과 함께 작동하여 Azure DevOps 원격을 감지하고, 현재 브랜치를 해당 PR과 매칭하며, HTTPS 자격 증명을 전달하여 `git fetch`와 `git push`가 바로 작동하도록 합니다.

## 리포지토리 감지

프로젝트를 열면 플러그인이 모든 Git 원격에서 다음 패턴을 검색합니다.

- `https://dev.azure.com/<org>/<project>/_git/<repo>`
- `https://<org>.visualstudio.com/<project>/_git/<repo>` (레거시)
- `git@ssh.dev.azure.com:v3/<org>/<project>/<repo>` (SSH)
- 계정에 등록된 자체 호스팅 Azure DevOps Server URL

일치하는 원격이 있으면 **Pull Requests** 도구 창이 나타나고 백그라운드 동기화가 시작됩니다. 일치하는 것이 없으면 플러그인은 방해가 되지 않도록 물러나 있습니다.

## 현재 브랜치 → PR

플러그인은 체크아웃된 브랜치를 감시하여 (원본 브랜치 이름으로) 매칭되는 열린 PR로 확인합니다. 매칭되는 것을 찾으면 두 개의 위젯이 켜집니다.

### 메인 툴바 브랜치 위젯

**main toolbar**의 Git 브랜치 위젯에 Azure DevOps 배지가 추가됩니다 - `!1234 on feature/login`. 클릭하면 해당 PR의 작업을 볼 수 있습니다.

![메인 툴바 브랜치 위젯 팝업](branch-widget-popup.png){ width="440" border-effect="line" }

- **Show in Tool Window** - PR의 상세 보기를 엽니다.
- **Update Pull Request Branch** - 로컬 브랜치가 PR head에서 갈라졌을 때 나타납니다(*Update Project*를 실행합니다).
- **Review in Editor** - 에디터 내 리뷰 오버레이를 토글합니다. [에디터에서 리뷰하기](Review-in-Editor-ko.md)를 참조하세요.

### 상태 표시줄 위젯

**status bar**에 있는 별도의 위젯은 `ADO PR !1234`를 표시합니다. 이를 클릭하면 도구 창에서 해당 PR이 열립니다. (상태 표시줄 위젯 선택기를 통해 숨기거나 표시할 수 있습니다 - 이름은 *Azure DevOps PR (current branch)*입니다.)

브랜치를 전환하면 두 위젯 모두 업데이트되며, 새 브랜치에 PR이 없으면 사라집니다.

## HTTPS 인증

Git이 Azure DevOps 원격에 대한 HTTPS 자격 증명을 필요로 할 때, 플러그인이 저장된 토큰을 자동으로 제공합니다.

<procedure title="HTTPS 인증 전달이 작동하는 방식">
    <step>IDE 내부에서(Update Project, Git 도구 창, 또는 내장 터미널) <code>git fetch</code> 또는 <code>git push</code>를 실행합니다.</step>
    <step>Git이 IDE에 자격 증명을 요청합니다.</step>
    <step>플러그인이 원격을 로그인된 계정과 매칭하고 해당 토큰을 제공합니다.</step>
    <step>Git이 진행됩니다 - 비밀번호 프롬프트가 없습니다.</step>
</procedure>

로그인된 여러 계정이 동일한 URL과 매칭되면 프로젝트의 **default account**가 사용됩니다([설정](Settings-ko.md) 참조).

> IDE 외부의 **system shell**에서 실행되는 Git 명령은 이 제공자를 볼 수 없습니다. 주로 외부 터미널에서 작업한다면 시스템 전체 Git 자격 증명 헬퍼를 구성하세요 - [문제 해결](Troubleshooting-ko.md#git-push-asks-for-a-password)을 참조하세요.
> {style="note"}

## 푸시 → PR 생성

아직 PR이 없는 브랜치를 푸시하면, 플러그인이 풍선 알림으로 **Create a pull request**를 제안할 수 있습니다 - 툴바보다 더 빠른 경로입니다. [설정](Settings-ko.md)의 **Offer Create PR after I push to an Azure DevOps remote**로 토글하세요. 기타 Git 기반 알림(리뷰 요청, 투표 변경, 답글)은 [알림 및 주의](Notifications-and-Attention-ko.md)에서 다룹니다.

## 다중 리포지토리 및 자체 호스팅

- 한 프로젝트에 있는 **여러 리포지토리**는 각각 독립적으로 감지됩니다. 도구 창의 **Switch Account / Repository…**를 사용하여 하나에 집중하세요.
- **Azure DevOps Server(온프레미스)**는 클라우드 제품과 똑같이 작동합니다 - 로그인할 때 서버 URL을 추가하고, 해당 서버에서 생성한 토큰을 사용하세요.
