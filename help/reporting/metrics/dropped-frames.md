---
title: 드롭된 프레임(지표)
description: 세션 간 합계 및 평균에 대해 드롭된 누적 프레임을 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 7%

---


# 드롭된 프레임(지표)

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**드롭된 프레임**&#x200B;지표를 다룹니다. Adobe Analytics은 동일한 `a.media.qoe.droppedFrameCount` 컨텍스트 데이터 변수에서 쌍을 이루는 [드롭된 프레임(차원)](/help/reporting/dimensions/dropped-frames.md)을 자동으로 채웁니다. Customer Journey Analytics은 차원 또는 지표로 사용할 수 있는 단일 `xdm.mediaReporting.qoeDataDetails.droppedFrames` 필드를 노출합니다. 이 변수를 수집하는 방법은 [삭제된 프레임](/help/implementation/variables/quality/dropped-frames.md)을 참조하세요.*

>[!ENDSHADEBOX]

**드롭된 프레임** 지표는 세션 간 누적 드롭된 프레임을 보고하며 합계, 평균 및 백분위수 롤업에 적합합니다. 지표를 사용하여 보고서 기간의 총 감소 볼륨을 계산하고 콘텐츠, 네트워크 또는 플레이어 간의 프레임 렌더링 품질을 비교할 수 있습니다.

## 이 지표의 계산 방법

드롭이 누적되면 플레이어가 QoE 개체의 `droppedFrames` 값을 업데이트합니다. 백엔드가 닫기 호출에 대한 최신 값을 보고합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.droppedFrameCount`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

세션 수준 부울 보고(프레임이 모두 삭제되었는지 여부)의 경우 [삭제된 프레임의 영향을 받은 스트림](dropped-frame-impacted-streams.md)을 사용하십시오.
