---
title: 평균 비트율(차원)
description: 각 세션의 버킷 평균 비트율을 100kbps 간격으로 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

---


# 평균 비트율(차원)

>[!BEGINSHADEBOX]

*이 페이지는 각 세션의 버킷 비트 전송률을 보고하는&#x200B;**평균 비트 전송률**&#x200B;차원을 다룹니다. 원시 가중 평균 지표에 대해서는 [평균 비트 전송률(지표)](/help/reporting/metrics/average-bitrate.md)을 참조하십시오. 이 변수를 수집하는 방법은 [Bitrate](/help/implementation/variables/quality/bitrate.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

**평균 비트율** 차원은 100kbps 간격으로 그룹화된 세션당 평균 재생 비트율을 보고합니다. 백엔드는 해당 값을 세션 전체의 모든 비트율 값에 대한 가중 평균으로 계산한 다음 버킷에 할당합니다. 차원을 사용하여 비트율 계층별로 참여 및 품질을 분석합니다.

## 이 차원이 채워지는 방법

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.bitrateAverageBucket`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `videoqoebitrateaverageevar`, `post_videoqoebitrateaverageevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateAverageBucket` |

## 차원 항목

각 항목은 비트율 버킷 레이블(예: `800-899`, `3200-3299`)입니다. 버킷 차원이 아닌 원시 가중 평균 값에 [평균 비트 전송률(지표)](/help/reporting/metrics/average-bitrate.md)을 사용하십시오.
