---
title: 광고 창
description: 자동 생성된 pod ID로 키로 표시되는 각 고유한 광고 브레이크를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 5%

---


# 광고 창

**광고 pod** 차원은 자동 생성된 pod ID로 처리된 각각의 고유한 광고 브레이크를 보고합니다. 세션의 모든 광고는 상위 광고 Pod에 속하며 Pod는 연달아 재생되는 여러 광고를 그룹화합니다. 광고 브레이크별로 참여를 분류하고 [Pod 이름](pod-name.md) 및 [Pod 위치](pod-position.md) 분류의 조인 키로 차원을 사용합니다.

## 이 차원이 채워지는 방법

`media.adBreakStart`이(가) 실행될 때 SDK에서 광고 pod ID를 자동으로 생성합니다. 직접 API 구현은 브레이크 색인 및 시작 시간에서 이를 구성하거나 사용자 지정 pod ID를 제공합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 광고]](/help/reporting/media-reports-enable.md)를 사용하도록 설정한 경우 컨텍스트 데이터 `a.media.ad.pod`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.advertisingPodDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| 데이터 피드 | `videoadpod, post_videoadpod` |

## 차원 항목

각 항목은 고유한 광고 pod ID입니다. ID는 불투명하며(일반적으로 세션 ID, 콘텐츠 ID 및 브레이크 인덱스의 해시), 친숙한 레이블의 [Pod 이름](pod-name.md)과(와) 결합할 때 그룹화 키로 가장 유용합니다.
