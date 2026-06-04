---
title: 화면 속 화면 카운트
description: 세션 중 뷰어가 PIP(Picture-in-Picture)를 입력한 횟수를 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 8%

---


# 화면 속 화면 카운트

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**화면 속 화면 수**&#x200B;보고 지표를 다룹니다. 이 변수를 수집하는 방법은 [화면 속 화면](/help/implementation/variables/player-state/picture-in-picture.md)을 참조하세요.*

>[!ENDSHADEBOX]

**화면 속 화면 카운트** 지표는 세션 중 뷰어가 화면 속 화면 재생을 입력한 횟수를 보고합니다. 각 PIP(Picture-in-Picture) 상태 시작 이벤트는 수를 증가시킵니다. 세션 수준 부울 롤업의 경우 [화면 속 화면의 영향을 받은 스트림](picture-in-picture-streams-impacted.md)과(와) 상태 내 총 시간의 경우 [화면 속 화면 총 기간](picture-in-picture-total-duration.md)을 연결합니다.

## 이 지표의 계산 방법

미디어 백엔드는 모든 PIP(Picture-in-Picture) 상태 시작 이벤트에서 이 수를 증가시킵니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 플레이어 상태 추적]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.states.pictureinpicture.count`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) 항목 위치: `name = "pictureInPicture"`, 필드: `count` |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.count` |
