---
title: 계산된 지표
description: 스트리밍 미디어 컬렉션의 계산된 지표 및 지표 공식에 대해 알아봅니다.
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 72%

---

# 계산된 지표{#calculated-metrics}

Adobe 스트리밍 미디어 컬렉션에 대한 계산된 지표는 평균 광고 체류 시간 또는 미디어 스트림당 평균 광고 수와 같은 타겟팅된 스트리밍 미디어 데이터를 얻을 수 있는 사용자 지정 지표입니다.

Adobe Analytics 계산된 지표에 대한 자세한 내용은 Adobe Analytics 구성 요소 안내서에서 [계산된 지표 및 고급 계산된(파생) 지표](https://experienceleague.adobe.com/docs/analytics/components/calculated-metrics/cm-overview.html?lang=ko-KR)를 참조하십시오.

>[!NOTE]
>
>다음 계산된 지표는 2018년 9월 13일에 도입되었습니다.

| 지표 | 설명 | 공식 |
|---|---|---|
| 미디어 스트림당 평균 광고 수 | 미디어 시작당 광고 시작 | `Ad Starts / Media Starts` |
| 미디어 스트림당 평균 챕터 수 | 미디어 시작당 챕터 시작 | `Chapter Start / Media Starts` |
| 평균 미디어 사용 시간 | 미디어 시작당 총 체류 시간(`HH:MM:SS`) | `Media Time Spent / Media Starts` |
| 평균 콘텐츠 체류 시간 | 콘텐츠 시작당 콘텐츠 체류 시간(`HH:MM:SS`) | `Content Time Spent / Content Start` |
| 평균 광고 체류 시간 | 광고 시작당 광고 체류 시간(`HH:MM:SS`) | `Ad Time Spent / Ad Start` |
| 평균 챕터 체류 시간 | 챕터 시작당 챕터 체류 시간(`HH:MM:SS`) | `Chapter Time Spent / Chapter Start` |
| 미디어 완료율 | 시작된 미디어에 대한 완료된 콘텐츠의 비율 (%) | `Content Completes/ Media Starts` |
| 콘텐츠 완료율 | 콘텐츠 시작에 대한 완료된 콘텐츠의 비율 (%) | `Content Completes / Content Starts` |
| 광고 완료율 | 광고 완료와 광고 시작 비율 (%) | `Ad Completes / Ad Starts` |
| 챕터 완료율 | 챕터 완료 횟수와 챕터 시작 비율 (%) | `Chapter Completes / Chapter Starts` |
| 시작 전 드롭 비율 | 시작 전 드롭과 미디어 시작 비율 (%) | `Drops before Starts / Media Starts` |
| 콘텐츠 일시 중단 기간 비율 | 총 일시 중단 기간과 콘텐츠 체류 시간의 비율 (%) | `Total Pause Duration / Content Time Spent` |
| 콘텐츠 버퍼 지속 시간 비율 | 총 버퍼 지속 시간과 콘텐츠 체류 시간의 비율 (%) | `Total Buffer Duration / Content Time Spent` |
| 콘텐츠 시작 시간 비율 | 시작 시간과 콘텐츠 체류 시간의 비율 (%) | `Time to Start / Content Time Spent` |
| 광고 체류 시간 비율 | 광고 체류 시간과 콘텐츠 체류 시간의 비율 (%) | `Ad Time Spent / Content Time Spent` |
