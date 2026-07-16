# 통계

PR 기록을 KPI와 차트로 바꿔 주는 전용 편집기 탭입니다. 사용자 지정 Azure DevOps 쿼리도, IDE를 떠날 필요도 없습니다.

![풀 리퀘스트 통계 대시보드](statistics-dashboard.png){ width="720" border-effect="line" }

> **실시간 폴링이 아니라 캐시된 데이터로 계산됩니다.** 통계는 도구 창이 이미 가져온 데이터를 그대로 사용합니다. 패널을 여는 것은 즉시 이루어지며 추가 API 호출을 하지 않습니다. 백그라운드 동기화가 새 데이터를 가져오면 숫자가 갱신됩니다.
> {style="note"}

## 열기

도구 창 툴바에서 **Pull Request Statistics**(차트) 아이콘을 클릭하거나 *Find Action* → **Pull Request Statistics**를 실행하세요. 편집기 영역에 탭이 열리며, **Refresh statistics**로 다시 계산할 수 있습니다.

## KPI 타일

상단을 가로지르는 대표 숫자 행입니다:

| KPI | 의미 |
|-----|---------|
| **Created** · **Merged** · **Abandoned** · **Open now** | 해당 기간의 PR 개수 |
| **Merge rate** | 해결된 PR 중 병합된 PR의 비율 |
| **Median merge (h)** | 생성부터 완료까지 걸린 일반적인 시간(시) |
| **Approval rate** | 리뷰어 투표 중 Approved(제안 포함)의 비율 |
| **First response (h)** | 작성자가 아닌 사람의 첫 댓글까지 걸린 중앙값 시간 |

> 시간 기반 KPI는 평균이 아니라 **중앙값**을 사용합니다. 일주일씩 걸린 몇몇 이상치가 일반적인 PR 수치를 왜곡해서는 안 되기 때문입니다. 평균이 표시되는 경우에는 별도로 표기됩니다.
> {style="note"}

## 차트

차트는 세 가지 섹션으로 묶여 있습니다:

- **Workload** - *Top creators*, *Top reviewers*, *Top commenters*, *Reviewer × Author* 협업.
- **Process health** - *Vote distribution*, *Time to merge*, *PR status*, *Open PR aging*, *PR cycle time (days)*, *PRs merged per week*.
- **Where work goes** - *Target branches*, *Day-of-week activity*, *Daily activity*.

## 필터와 범위

고정된 헤더가 모든 지표의 범위를 한 번에 지정합니다:

- **Window** - 최근 7일, 30일, 90일, 6개월, 1년 또는 전체 기간.
- **Author**, **Reviewer**, **Target branch** - 특정 사람이나 브랜치로 좁힙니다.
- **Clear filters** - 기본값으로 초기화합니다.

## 유의 사항

> **로컬 보기 전용입니다.** 통계는 사용자 계정이 볼 수 있는 PR만 다룹니다. 접근 권한이 없는 리포지토리는 집계되지 않습니다.
> {style="warning"}

이 기능은 Azure DevOps Analytics를 대체하지 않습니다. 편집기 안에서 빠르게 확인하는 신호일 뿐입니다. 조직 전체 보고가 필요하면 Azure DevOps의 Analytics 서비스를 직접 사용하세요.
