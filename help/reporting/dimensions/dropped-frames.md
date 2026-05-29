---
title: 드롭된 프레임(치수)
description: 세션당 드롭된 프레임 누적 수를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 6%

---


# 드롭된 프레임(치수)

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**삭제된 프레임**차원을 다룹니다. Adobe Analytics은 동일한 `a.media.qoe.droppedFrameCount` 컨텍스트 데이터 변수에서 쌍을 이루는 [드롭된 프레임(지표)](/help/reporting/metrics/dropped-frames.md)을 자동으로 채웁니다. Customer Journey Analytics은 차원 또는 지표로 사용할 수 있는 단일 `xdm.mediaReporting.qoeDataDetails.droppedFrames` 필드를 노출합니다. 이 변수를 수집하는 방법은 [삭제된 프레임](/help/implementation/variables/quality/dropped-frames.md)을 참조하세요.*

>[!ENDSHADEBOX]

**드롭된 프레임** 차원은 세션 중에 드롭된 프레임의 누적 수를 보고합니다. 차원을 사용하여 정확한 놓기 횟수별로 참여를 분류합니다.

## 이 차원이 채워지는 방법

QoE 개체가 누적되면 플레이어가 해당 개체의 `droppedFrames` 값을 업데이트합니다. 백엔드가 닫기 호출에 대한 최신 값을 보고합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.droppedFrameCount`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `videoqoedroppedframecountevar`, `post_videoqoedroppedframecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

## 차원 항목

각 항목은 닫기 호출에서 보고된 리터럴 드롭카운트 값입니다. 세션 수준 부울 보고(프레임이 모두 삭제되었는지 여부)의 경우 [삭제된 프레임의 영향을 받은 스트림](/help/reporting/metrics/dropped-frame-impacted-streams.md)을 사용하십시오.
