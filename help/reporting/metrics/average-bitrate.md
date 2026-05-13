---
title: 평균 비트율(지표)
description: 각 세션의 원시 가중 평균 비트율을 kbps 단위로 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 7%

---


# 평균 비트율(지표)

>[!BEGINSHADEBOX]

*이 페이지에서는 세션당 원시 가중 평균 비트 전송률을 보고하는&#x200B;**평균 비트 전송률**이벤트 지표를 다룹니다. 버킷 차원에 대해서는 [평균 비트율(차원)](/help/reporting/dimensions/average-bitrate.md)을 참조하세요. 이 변수를 수집하는 방법은 [Bitrate](/help/implementation/variables/quality/bitrate.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

**평균 비트율** 지표는 각 세션에 대해 원시 가중 평균 재생 비트율(kbps)을 보고합니다. [버킷 차원](/help/reporting/dimensions/average-bitrate.md)과 달리 지표는 세션 간 합계, 평균 및 백분위수 롤업에 적합한 연속 숫자 값입니다.

## 이 지표의 계산 방법

미디어 백엔드는 각 비트율이 활성 상태인 기간으로 가중된 세션 동안 보고된 모든 비트율 값의 가중 평균을 계산합니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.bitrateAverage`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateAverage`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
