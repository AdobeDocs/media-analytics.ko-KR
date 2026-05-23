---
title: 계산된 지표
description: Adobe Analytics 및 Customer Journey Analytics의 스트리밍 미디어 보고를 위한 사용자 지정 계산된 지표입니다.
feature: Metrics
role: User, Admin
source-git-commit: 1251b66173158b8fea92516197b3b9f444bfaaf7
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 5%

---

# 계산된 지표

Adobe 스트리밍 미디어 서비스에 대한 계산된 지표는 표준 스트리밍 미디어 지표에서 작성한 사용자 지정 지표이므로 구현을 변경하지 않고 평균 광고 체류 시간 또는 미디어 완료율과 같은 비율을 도출할 수 있습니다.

Analysis Workspace에서 이러한 계산된 지표를 만들려면 [Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/components/calculated-metrics/cm-overview) 또는 [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)에서 각각의 계산된 지표 개요를 참조하십시오.

| 계산된 지표 | 설명 | 공식 |
| --- | --- | --- |
| 평균 미디어 스트림당 광고 | 미디어 시작당 광고 시작 | [`Ad Starts`](/help/reporting/metrics/ad-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 평균 미디어 스트림당 챕터 | 미디어 시작당 챕터 시작 | [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 평균 미디어 체류 시간 | 미디어 시작당 총 체류 시간(`HH:MM:SS`) | [`Media Time Spent`](/help/reporting/metrics/media-time-spent.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 평균 콘텐츠 체류 시간 | 콘텐츠 시작당 콘텐츠 체류 시간(`HH:MM:SS`) | [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| 평균 광고 체류 시간 | 광고 시작당 광고 체류 시간(`HH:MM:SS`) | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| 평균 챕터 체류 시간 | 챕터 시작당 챕터 체류 시간(`HH:MM:SS`) | [`Chapter Time Spent`](/help/reporting/metrics/chapter-time-spent.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| 미디어 완료율 | 시작된 미디어에 대한 완료된 콘텐츠의 비율 | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 컨텐츠 완료율 | 완료된 콘텐츠와 콘텐츠 시작의 비율 | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| 광고 완료율 | 광고 완료와 광고 시작 비율 | [`Ad Completes`](/help/reporting/metrics/ad-completes.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| 챕터 완료율 | 챕터 완료 횟수와 챕터 시작 비율 | [`Chapter Completes`](/help/reporting/metrics/chapter-completes.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| 시작 전 드롭 비율 | 시작 전 드롭과 미디어 시작 비율 | [`Drops Before Start`](/help/reporting/metrics/drops-before-start.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 컨텐츠 일시 중단 기간 비율 | 총 일시 중단 기간과 콘텐츠 체류 시간의 비율 | [`Total Pause Duration`](/help/reporting/metrics/total-pause-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| 컨텐츠 버퍼 지속 시간 비율 | 총 버퍼 지속 시간과 콘텐츠 체류 시간의 비율 | [`Total Buffer Duration`](/help/reporting/metrics/total-buffer-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| 컨텐츠 TTL(Time-To-Start) 비율 | 시작 시간과 콘텐츠 체류 시간의 비율 | [`Time to Start`](/help/reporting/metrics/time-to-start.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| 광고 체류 시간 비율 | 광고 체류 시간과 콘텐츠 체류 시간의 비율 | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |

