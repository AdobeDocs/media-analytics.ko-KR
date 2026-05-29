---
title: 화면 속 화면 총 시간
description: 세션 중 뷰어가 PIP(Picture-in-Picture)에서 보낸 누적 시간(초)을 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 7%

---


# 화면 속 화면 총 시간

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**화면 속 화면 총 시간**&#x200B;보고 지표를 다룹니다. 이 변수를 수집하는 방법은 [화면 속 화면](/help/implementation/variables/player-state/picture-in-picture.md)을 참조하세요.*

>[!ENDSHADEBOX]

**화면 속 화면 총 기간** 지표는 뷰어가 세션 중에 화면 속 화면을 사용한 누적 시간을 초 단위로 보고합니다. 백엔드는 PIP(Picture-in-Picture) 상태 시작과 일치하는 상태 끝 이벤트 사이의 모든 간격을 합합니다.

## 이 지표의 계산 방법

미디어 백엔드는 세션 동안 모든 PIP(Picture-in-Picture) 간격에 걸쳐 경과된 시간을 합산합니다. 지표는 닫기 호출에 보고됩니다. Analysis Workspace은 값을 `HH:MM:SS`(으)로 표시합니다. 데이터 피드, Data Warehouse 및 보고 API는 값(초)을 표시합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 플레이어 상태 추적]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.states.pictureinpicture.time`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/media-reporting-details) 항목 위치: `name = "pictureInPicture"`, 필드: `time` |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.time` |
