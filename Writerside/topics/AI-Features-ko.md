# AI 기능

선택적 AI 도우미: PR 요약, 전체 diff(변경 내용) 리뷰, 코드 설명, 커밋 메시지, PR 제목/설명 초안, 문법 다듬기. **자신의 공급자를 직접 사용하세요** - OpenAI, Claude, Gemini, Ollama 또는 GitHub Copilot - 그리고 각 기능을 원하는 곳으로 라우팅하세요.

> 여기 있는 모든 것은 **켜기 전까지는 꺼져 있습니다**. 공급자에게 정확히 무엇이 전송되는지는 [개인정보 및 데이터](Privacy-and-Data-ko.md)를 참조하세요.
> {style="note"}

## 플러그인이 AI로 할 수 있는 일

| 기능 | 하는 일 | 위치 |
|---------|--------------|-------|
| **Summarize Pull Request** | 설명에 넣을 수 있는 diff(변경 내용) 요약 초안을 작성합니다. | 타임라인 카드 / 오버플로 메뉴 |
| **Run AI Review** | diff(변경 내용)를 살펴보고 인라인 리뷰 댓글을 제안합니다. | Diff 도구 모음 / 변경 내용 트리 메뉴 / 오버플로 |
| **Explain This File** | 파일이나 선택 영역에 대한 쉬운 영어 설명을 스트리밍합니다. | diff(변경 내용)에서 오른쪽 클릭 |
| **Generate Commit Message with AI** | 스테이징된 변경 사항으로 커밋 메시지 초안을 작성합니다. | Commit 도구 창 |
| **Title + Description** | 브랜치의 diff(변경 내용)로 Create-PR 양식을 미리 채웁니다. | Create Pull Request 양식 |
| **Polish grammar &amp; spelling with AI** | 모든 댓글이나 설명을 제자리에서 정리합니다. | 모든 댓글 편집기 |

![PR 타임라인의 AI 요약 카드](ai-summary-card.png){ width="700" border-effect="line" }

> **Run AI Review**는 diff(변경 내용)에 인라인 제안을 제안합니다. 각 제안은 **Add to review** - AI의 텍스트를 해당 줄의 새 댓글 편집기에 넣어 편집하고 초안으로 대기열에 넣을 수 있게 합니다 - 또는 이를 숨기는 **Discard**를 제공합니다. **대기 중인 댓글을 제출하기 전까지는 Azure DevOps에 아무것도 게시되지 않습니다.** 실행이 실패하면 원클릭 **Open AI Settings** 이동 기능이 있는 풍선이 나타납니다.
> {style="tip"}

### 요약 조정

**AI summary** 카드의 오른쪽 상단 모서리에 있는 **Summary settings** 기어를 누르면 요약 생성 방식을 제어하는 팝업이 열립니다:

| 컨트롤 | 옵션 |
|---------|---------|
| **Generate automatically on open** | 체크박스 - 기본적으로 꺼짐. 켜면 PR이 열리는 즉시 카드가 요약 초안을 작성합니다. |
| **Verbosity** | 슬라이더: **Brief** · **Neutral** · **Verbose**. |
| **Formality tone** | 슬라이더: **Informal** · **Neutral** · **Formal**. |
| **Personality** | 자유 텍스트 - 선택적 페르소나, 예: "약간 냉소적인 수석 엔지니어". |
| **Customization prompt** | 자유 텍스트 - 기본값을 사용하려면 비워 두세요. 이는 AI Settings의 **Configure Prompts → Pull Request summary**와 동일한 재정의이므로 어느 쪽에서 편집하든 동기화가 유지됩니다. |

Save 버튼은 없습니다 - 컨트롤을 편집하고 팝업을 닫으면 적용됩니다.

![AI 요약 카드의 기어에서 나오는 Summary settings 팝업](ai-summary-settings-popup.png){ width="520" border-effect="line" }

## 공급자 구성

<ui-path>Settings | Version Control | Azure DevOps | AI Settings</ui-path>를 열고 **Enable AI assistance**(마스터 스위치)를 켜세요. 그런 다음 **AI Providers** 표에서 공급자를 추가하세요.

![AI Settings 페이지: 공급자 및 기능별 라우팅](ai-settings.png){ width="720" border-effect="line" }

각 행은 **Provider**, **Model**, **Enabled** 열이 있는 하나의 공급자 인스턴스입니다. 활성화된 첫 번째 행이 기본값입니다. **Add AI Provider** 대화 상자는 다섯 가지 제품군을 제공합니다:

| 제품군 | 참고 |
|--------|-------|
| **OpenAI** | GPT 모델. OpenAI 호환 base URL(Azure OpenAI, vLLM, …)과 함께 작동합니다. |
| **Claude** | Anthropic Claude 모델. |
| **Gemini** | Google Gemini 모델. |
| **Ollama** | 로컬 모델 - 무료, 키 불필요. |
| **GitHub Copilot** | Copilot 구독을 사용합니다(CLI 전용). |

> Add/Edit 대화 상자의 **Model** 드롭다운은 스스로 채워집니다: 번들된 추천 목록을 즉시 표시한 다음, 공급자에 대한 실시간 쿼리(예: OpenAI 및 Claude의 `/v1/models`)에서 새로 고쳐 새로 출시된 모델이 플러그인 업데이트 없이 나타나도록 합니다. 실시간 목록은 약 30분 동안 캐시됩니다. 대화 상자를 열 때마다, 그리고 제품군이나 모드를 변경할 때마다 새로 고쳐지므로 수동 새로 고침 버튼은 없습니다. 검색에는 저장된 키가 필요합니다 - 키가 입력될 때까지 드롭다운은 추천 목록으로 대체됩니다. 필드는 계속 편집 가능하므로 언제든지 모델 id를 직접 입력할 수 있습니다.
> {style="note"}

대부분의 제품군은 두 가지 **모드** 중 하나로 실행됩니다:

- **HTTP API (use an API key)** - 키를 붙여 넣으세요. 선택적으로 사용자 지정 엔드포인트를 가리키도록 **API URL**을 설정하세요. 키는 IDE 키체인(PasswordSafe)에 저장됩니다.
- **CLI (use the local command-line tool)** - 키 없음. 로컬 바이너리가 자체 인증을 처리합니다. 마찰이 가장 적은 경로이지만 CLI 공급업체의 약관을 감수해야 합니다.

저장하기 전에 공급자가 작동하는지 확인하려면 대화 상자에서 **Test Connection**을 사용하세요.

## 기능을 공급자로 라우팅

**Per-Feature Provider** 패널은 각 기능을 특정 인스턴스에 고정합니다 - 저렴한 기능은 작은 모델로, 무거운 리뷰는 똑똑한 모델로 보내는 데 유용합니다:

```
AI Summary          → [Default ▾]
AI Review           → [Default ▾]
Title + Description → [Default ▾]   (also used by Generate Commit Message)
Explain Code        → [Default ▾]
```

행을 **Default**로 두면 활성화된 첫 번째 공급자가 사용됩니다. **같은 제품군을 두 번 이상** 추가할 수 있으며(예: 저렴한 모델과 똑똑한 모델의 OpenAI 행 두 개), 각각에 독립적으로 라우팅할 수 있습니다.

### Configure Prompts

**Configure Prompts** 패널을 사용하면 각 기능 뒤에 있는 시스템 프롬프트를 편집할 수 있습니다. 프롬프트를 편집하면 해당 기능에 대한 캐시된 응답이 무효화됩니다.

## 캐싱, 비용 및 한도

AI 응답은 **PR별 + 커밋 SHA별**로 캐시됩니다(토글: **Cache AI responses per commit SHA**, 기본적으로 켜짐). 캐시 적중 시 API 호출 없이 즉시 반환됩니다. 새 커밋이나 편집된 프롬프트는 이를 무효화합니다. **Advanced**의 **Clear AI Response Cache**로 강제 새로 고침을 할 수 있습니다.

사용한 토큰에 대해서는 공급자 요금을 지불합니다. 사용량을 낮게 유지하려면:

- 기능별 라우팅을 통해 저렴한 기능(커밋 메시지, 제목)을 작은 모델로 라우팅하세요.
- **Advanced**에서 **Max diff size**를 낮춰 큰 diff(변경 내용)를 전송하기 전에 잘라내세요.
- 캐시를 켜 두어 PR을 다시 열 때 요금이 다시 청구되지 않도록 하세요.

> 공급자 할당량 및 사용 한도 오류는 공급자에서 직접 옵니다 - 플러그인은 이를 분류하고 조용히 실패하는 대신 명확하고 실행 가능한 문구를 표시합니다. 자체 속도 제한이나 재시도를 추가하지 않습니다.
> {style="note"}

## 모든 것을 로컬에 유지하거나, 끄기

- **로컬 추론:** 모든 기능을 `localhost`의 **Ollama** 인스턴스로 라우팅하세요 - 어떤 코드도 사용자의 컴퓨터를 벗어나지 않습니다.
- **완전히 끄기:** **Enable AI assistance**의 체크를 해제하세요. 모든 AI 기능이 메뉴와 도구 모음에서 사라지고 플러그인은 아웃바운드 AI 호출을 전혀 하지 않습니다.
