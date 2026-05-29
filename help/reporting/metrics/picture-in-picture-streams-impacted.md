---
title: 화면 속 화면의 영향을 받은 스트림
description: 뷰어가 PIP(Picture-in-Picture)를 입력한 세션을 한 번 이상 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 7%

---


# 화면 속 화면의 영향을 받은 스트림

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**화면 속 화면의 영향을 받은 스트림**&#x200B;보고 지표를 다룹니다. 이 변수를 수집하는 방법은 [화면 속 화면](/help/implementation/variables/player-state/picture-in-picture.md)을 참조하세요.*

>[!ENDSHADEBOX]

**화면 속 화면의 영향을 받은 스트림** 지표는 뷰어가 화면 속 화면 재생을 한 번 이상 입력한 세션을 계산합니다. 지표는 세션 수준 부울입니다. 동일한 세션 내의 여러 PIP(Picture-in-Picture) 항목이 하나의 영향을 받은 스트림과 같습니다. 전체 PIP(Picture-in-Picture) 항목 볼륨에 대해 [PIP(Picture in Picture) 개수](picture-in-picture-count.md)를 사용합니다.

## 이 지표의 계산 방법

미디어 백엔드는 세션 중에 PIP(Picture-in-Picture) 상태 시작 이벤트가 처음 수신될 때 이 플래그를 설정합니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 플레이어 상태 추적]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.states.pictureinpicture.set`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/media-reporting-details) 항목 위치: `name = "pictureInPicture"`, 필드: `isSet` |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.set` |
