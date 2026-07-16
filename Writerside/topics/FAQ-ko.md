# FAQ

%product%을(를) 사용할지 여부와 사용 방법에 대한 결정 중심의 질문들입니다. "고장 났는데 어떻게 고치나요?" 유형의 질문은 [문제 해결](Troubleshooting-ko.md)을 참조하세요.

## 이 플러그인은 Azure DevOps Server(온프레미스)를 지원하나요?

예. 계정을 만들 때 서버의 URL을 추가하세요. Azure DevOps Server 2019 이상과 Azure DevOps Services(클라우드)를 모두 지원합니다.

클라우드 제품은 `dev.azure.com/<org>`을 사용합니다. 온프레미스는 사용자 고유의 서버 URL(예: `https://devops.example.com`)을 사용합니다. PAT 인증은 두 경우 모두에서 작동합니다. Microsoft Entra를 통한 OAuth는 **클라우드 전용**입니다.

## Azure Pipelines를 지원하나요?

예. 전용 **Pipelines** 도구 창에서 파이프라인과 실행을 탐색하고, 대화형 스테이지 그래프를 보고, 색상으로 구분된 단계 로그를 읽고, 수동 승인 게이트를 승인하거나 거부할 수 있습니다. 이 모든 작업을 IDE 안에서 수행할 수 있습니다. 풀 리퀘스트 CI 검사가 Azure 빌드를 가리키는 경우, **Details…**를 클릭하면 해당 실행이 브라우저 대신 IDE에서 열립니다.

기본적으로 켜져 있습니다. <ui-path>Settings | Version Control | Azure DevOps</ui-path>에서 **Enable Pipelines integration**을 토글하세요. 꺼져 있으면 도구 창이 숨겨지고, 파이프라인 알림이나 배지가 발생하지 않으며, 파이프라인 검사가 브라우저에서 열립니다. [파이프라인](Pipelines-ko.md)을 참조하세요.

## 클래식 TFVC(비 Git) 리포지토리에서 작동하나요?

아니요. 이 플러그인은 Git 기반 Azure Repos 전용입니다. **TFVC**(Team Foundation Version Control, Azure DevOps에서 Git 이전에 사용된 Microsoft의 중앙 집중식 VCS)는 지원하지 않습니다.

## Azure DevOps 계정 없이도 사용할 수 있나요?

아니요. 이 플러그인은 오직 Azure DevOps 전용입니다. GitHub이나 GitLab의 경우, 각각 번들로 제공되는 GitHub 플러그인이나 JetBrains GitLab 플러그인을 사용하세요.

## 같은 IDE에서 GitHub과 Azure DevOps PR 플러그인을 모두 사용할 수 있나요?

예. 두 플러그인은 독립적인 도구 창을 등록하며 상태를 공유하지 않습니다. 단일 프로젝트에 GitHub과 Azure DevOps 양쪽을 가리키는 원격이 있으면 두 도구 창이 모두 나타나며, 각각은 자신의 원격에 대한 PR만 나열합니다.

## OAuth와 PAT 중 어느 것을 선택해야 하나요?

| 사용해야 하는 것…  | 언제                                                                                                          |
|-----------------|--------------------------------------------------------------------------------------------------------------|
| **OAuth**       | 클라우드 제품(`dev.azure.com`)을 사용하고, 조직이 OAuth를 금지하지 않으며, MFA 프롬프트를 인라인으로 원할 때.  |
| **PAT**         | Azure DevOps Server(온프레미스)를 사용하거나, 조직 정책이 PAT를 의무화하거나, OAuth 핸들러 문제를 겪은 경우.|

OAuth 토큰은 자동으로 갱신됩니다. PAT는 생성 시 설정한 날짜에 만료됩니다. PAT는 설계상 MFA를 우회합니다. PAT를 생성하려면 사용자가 이미 인증되어 있어야 하지만, 토큰 자체는 다시 인증을 요구하지 않습니다.

## 내 코드가 Azure DevOps 외의 다른 곳으로 전송되나요?

AI 기능을 명시적으로 활성화하고 공급자를 구성한 경우가 아니라면 전송되지 않습니다. 기능별 전체 데이터 흐름은 [개인정보 및 데이터](Privacy-and-Data-ko.md)를 참조하세요.

AI가 비활성화되어 있으면(마스터 스위치가 꺼져 있으면) 플러그인은 사용자의 Azure DevOps 조직 외부로 어떠한 아웃바운드 호출도 하지 않습니다.

## AI 호출 없이 플러그인을 사용하려면 어떻게 하나요?

<ui-path>Settings | Version Control | Azure DevOps | AI Settings</ui-path> 상단에서 **Enable AI assistance**의 체크를 해제하세요. 모든 AI 기능이 메뉴와 툴바에서 사라지고, AI 호출이 전혀 이루어지지 않습니다.

또는 AI를 켜 둔 채 모든 기능을 로컬 **Ollama** 인스턴스로 라우팅하여 완전히 온디바이스 추론을 할 수도 있습니다.

## PR 지표는 어디에서 볼 수 있나요?

[통계](Statistics-ko.md) 탭에는 KPI와 차트(병합까지의 시간, 리뷰 속도, 투표 분포 등)가 캐시된 데이터에서 로컬로 계산되어 표시됩니다. 이는 보기 전용 대시보드입니다. 내보내기가 가능한 조직 전체 보고서가 필요하면 Azure DevOps Analytics를 사용하세요.

## 메모리와 CPU 사용량은 어느 정도인가요?

이 플러그인은 IDE에 번들로 제공되는 `collaboration-tools` 툴킷(GitHub 플러그인이 사용하는 것과 동일한 툴킷) 위에 놓인 얇은 Swing UI입니다. 유휴 상태에서는 IDE 기준선에 더해 약 30~60MB의 힙을 추가합니다. 활성 동기화(PR 목록, 댓글, diff 가져오기)는 몇 MB를 더 추가합니다.

대규모 조직(여러 리포지토리에 걸쳐 1000개 이상의 PR)의 경우, PR 목록은 가상화되어 보이는 행만 UI 구성 요소를 보유합니다.

## 플러그인이 익명으로 무언가를 업로드하나요? 텔레메트리는요?

아니요. 출시 버전은 텔레메트리, 크래시 보고서, 사용 분석을 수집하지 않습니다. 유일한 아웃바운드 호출은 사용자의 Azure DevOps 조직과 (AI가 활성화된 경우) 구성된 AI 공급자로의 호출뿐입니다. [개인정보 및 데이터](Privacy-and-Data-ko.md)를 참조하세요.

## Azure Repos Wiki를 지원하나요?

아니요. 이 플러그인의 범위는 풀 리퀘스트로 한정됩니다. 위키 편집은 Azure DevOps의 웹 UI를 사용하세요.
