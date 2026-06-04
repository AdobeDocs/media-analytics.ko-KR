---
title: 챕터
description: 자동 생성된 챕터 ID로 처리된 각 고유한 챕터를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 8%

---


# 챕터

**Chapter** 차원은 자동 생성된 챕터 ID로 입력된 재생된 각 고유한 챕터를 보고합니다. 이 ID는 콘텐츠 ID, 챕터 인덱스 및 챕터 시작 시간에서 SDK 또는 백엔드에 의해 생성되므로 동일한 콘텐츠에 있는 동일한 챕터의 두 세션은 단일 라인 항목으로 롤업됩니다. 챕터 이름, 챕터 길이, 챕터 오프셋 및 챕터 위치와 같은 챕터 수준 분류를 위한 조인 키로 차원을 사용합니다.

## 이 차원이 채워지는 방법

[챕터 시작](/help/implementation/events/chapters/chapter-start.md) 이벤트가 실행되면 챕터 ID가 자동으로 생성됩니다. 값은 직접 설정되지 않습니다. 챕터 위치, 오프셋 및 콘텐츠 ID에서 파생됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 챕터]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.chapter.name`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.ID`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 데이터 피드 | `videochapter`, `post_videochapter` |
| Audience Manager | 해당 사항 없음 |

## 차원 항목

각 항목은 고유한 챕터 ID입니다. ID는 불투명하며(일반적으로 콘텐츠 ID + 인덱스 + 오프셋의 해시) 그룹화 키로 가장 유용합니다. [챕터 이름](chapter-name.md)과(와) 연결하여 알기 쉬운 레이블을 지정하십시오.
