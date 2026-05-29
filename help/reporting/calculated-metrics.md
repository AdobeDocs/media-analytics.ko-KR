---
title: 계산된 지표
description: Adobe Analytics 및 Customer Journey Analytics의 스트리밍 미디어 보고를 위한 사용자 지정 계산된 지표입니다.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 5%

---

# 계산된 지표

Adobe 스트리밍 미디어 서비스에 대한 계산된 지표는 표준 스트리밍 미디어 지표에서 작성한 사용자 지정 지표이므로 구현을 변경하지 않고 평균 광고 체류 시간 또는 미디어 완료율과 같은 비율을 도출할 수 있습니다.

Analysis Workspace에서 이러한 계산된 지표를 만들려면 [Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/components/calculated-metrics/cm-overview) 또는 [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)에서 각각의 계산된 지표 개요를 참조하십시오.

| 계산된 지표 | 설명 | 공식 |
| --- | --- | --- |
| 평균 미디어 스트림당 광고 | [[!UICONTROL 미디어 시작]](/help/reporting/metrics/media-starts.md)당 [[!UICONTROL 광고 시작]](/help/reporting/metrics/ad-starts.md) | `[Ad starts] / [Media starts]` |
| 평균 미디어 스트림당 챕터 | [[!UICONTROL 챕터 시작]](/help/reporting/metrics/chapter-starts.md)/[[!UICONTROL 미디어 시작]](/help/reporting/metrics/media-starts.md) | `[Chapter starts] / [Media starts]` |
| 평균 미디어 체류 시간 | [[!UICONTROL 미디어 시작]](/help/reporting/metrics/media-starts.md)(`HH:MM:SS`)당 [[!UICONTROL 미디어 체류 시간]](/help/reporting/metrics/media-time-spent.md) | `[Media time spent] / [Media starts]` |
| 평균 콘텐츠 체류 시간 | [[!UICONTROL 콘텐츠 시작]](/help/reporting/metrics/content-starts.md)(`HH:MM:SS`)당 [[!UICONTROL 콘텐츠 체류 시간]](/help/reporting/metrics/content-time-spent.md) | `[Content time spent] / [Content starts]` |
| 평균 광고 체류 시간 | [[!UICONTROL 광고 시작]](/help/reporting/metrics/ad-starts.md)(`HH:MM:SS`)당 [[!UICONTROL 광고 체류 시간]](/help/reporting/metrics/ad-time-spent.md) | `[Ad time spent] / [Ad starts]` |
| 평균 챕터 체류 시간 | [[!UICONTROL 챕터 시작]](/help/reporting/metrics/chapter-starts.md)(`HH:MM:SS`)당 [[!UICONTROL 챕터 체류 시간]](/help/reporting/metrics/chapter-time-spent.md) | `[Chapter time spent] / [Chapter starts]` |
| 미디어 완료율 | [[!UICONTROL 콘텐츠 완료]](/help/reporting/metrics/content-completes.md)와 [[!UICONTROL 미디어 시작]](/help/reporting/metrics/media-starts.md)의 비율 | `[Content completes] / [Media starts]` |
| 컨텐츠 완료율 | [[!UICONTROL 콘텐츠 완료]](/help/reporting/metrics/content-completes.md)와 [[!UICONTROL 콘텐츠 시작]](/help/reporting/metrics/content-starts.md)의 비율 | `[Content completes] / [Content starts]` |
| 광고 완료율 | [[!UICONTROL 광고 완료]](/help/reporting/metrics/ad-completes.md)와 [[!UICONTROL 광고 시작]](/help/reporting/metrics/ad-starts.md)의 비율 | `[Ad completes] / [Ad starts]` |
| 챕터 완료율 | [[!UICONTROL 챕터 완료]](/help/reporting/metrics/chapter-completes.md)와 [[!UICONTROL 챕터 시작]](/help/reporting/metrics/chapter-starts.md)의 비율 | `[Chapter completes] / [Chapter starts]` |
| 시작 전 드롭 비율 | [[!UICONTROL 시작 전 드롭]](/help/reporting/metrics/drops-before-start.md)과(와) [[!UICONTROL 미디어 시작]](/help/reporting/metrics/media-starts.md)의 비율 | `[Drops before start] / [Media starts]` |
| 컨텐츠 일시 중단 기간 비율 | [[!UICONTROL 총 일시 중단 기간]](/help/reporting/metrics/total-pause-duration.md)과(와) [[!UICONTROL 콘텐츠 체류 시간]](/help/reporting/metrics/content-time-spent.md)의 비율 | `[Total pause duration] / [Content time spent]` |
| 컨텐츠 버퍼 지속 시간 비율 | [[!UICONTROL 총 버퍼 지속 시간]](/help/reporting/metrics/total-buffer-duration.md)과(와) [[!UICONTROL 콘텐츠 체류 시간]](/help/reporting/metrics/content-time-spent.md)의 비율 | `[Total buffer duration] / [Content time spent]` |
| 컨텐츠 TTL(Time-To-Start) 비율 | [[!UICONTROL 시작 시간]](/help/reporting/metrics/time-to-start.md)과(와) [[!UICONTROL 콘텐츠 체류 시간]](/help/reporting/metrics/content-time-spent.md)의 비율 | `[Time to start] / [Content time spent]` |
| 광고 체류 시간 비율 | [[!UICONTROL 광고 체류 시간]](/help/reporting/metrics/ad-time-spent.md)과(와) [[!UICONTROL 콘텐츠 체류 시간]](/help/reporting/metrics/content-time-spent.md)의 비율 | `[Ad time spent] / [Content time spent]` |

