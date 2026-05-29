---
title: 콘텐츠 다시 시작
description: 이전에 중단된 재생을 재개한 세션을 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 9%

---


# 콘텐츠 다시 시작

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**콘텐츠 다시 시작**&#x200B;보고 지표를 다룹니다. 이 변수를 수집하는 방법은 [콘텐츠 다시 시작](/help/implementation/variables/core/content-resumes.md)을 참조하세요.*

>[!ENDSHADEBOX]

**콘텐츠 다시 시작** 지표는 이전에 중단된 재생을 다시 시작한 세션을 계산합니다. 플레이어가 `sessionStart`에서 세션에 다시 시작으로 플래그를 지정할 때(예: 버퍼, 일시 중지 또는 중단이 30분을 초과한 후) 증가합니다. 동일한 뷰어 및 에셋에 대한 연속 세션에서 진짜 새 세션을 분리하는 데 사용합니다.

## 이 지표의 계산 방법

[세션 시작](/help/implementation/events/session/session-start.md) 이벤트에서 `xdm.mediaCollection.sessionDetails.hasResume`이(가) `true`인 경우 미디어 백엔드가 이 플래그를 설정합니다. 플레이어는 명시적으로 세션을 다시 시작으로 플래그를 지정해야 합니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.resume`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasResume`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | 해당 사항 없음 |
