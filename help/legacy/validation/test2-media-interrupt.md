---
title: 테스트 2 미디어 중단
description: 유효성 검사에 사용된 미디어 중단 테스트에 대해 알아봅니다.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 89%

---

# 테스트 2: 미디어 중단{#test-media-interruption}

이 테스트 케이스는 모바일 중단 동작의 유효성을 검사합니다.

## 테스트 절차

다음 순서로 이 작업을 완료하고 기록해야 합니다.

1. **미디어 플레이어 시작**

   미디어 플레이어가 시작되면 다음 호출이 다음 순서로 전송됩니다.

   1. Adobe Analytics(AppMeasurement) 시작
   1. Media Analytics(하트비트) 시작
   1. Media Analytics(하트비트) Adobe Analytics 시작 호출 요청

   위의 처음 두 호출에는 추가 메타데이터와 변수가 포함되어 있습니다. 호출 매개 변수 및 메타데이터에 대해서는 [테스트 호출 세부 사항](/help/legacy/validation/test-call-details.md#start-the-media-player)을 참조하십시오.

   위에서 세 번째 호출은 Media SDK가 Adobe Analytics 시작 호출(`pev2=ms_s`)을 Adobe Analytics 서버로 전송하도록 요청했음을 Media Analytics 서버에 알려줍니다.

1. **적어도 5분 동안 중단되지 않은 상태로 기본 컨텐츠 재생**

   **컨텐츠 재생**

   컨텐츠를 재생하는 동안 Media SDK는 10초마다 재생 호출(하트비트)을 Media Analytics 서버로 전송합니다.

   호출 매개 변수 및 메타데이터에 대해서는 [테스트 호출 세부 사항](/help/legacy/validation/test-call-details.md#play-main-content)을 참조하십시오.

   플랫폼의 [광고 추적](/help/use-cases/track-ads/track-ads-overview.md) 이러한 광고 호출에 대한 추가 정보를 위한 지침.

1. **앱 또는 브라우저를 백그라운드로 이동**

   앱이 백그라운드에서 실행되는 동안 `main:pause` 호출만 VHL 버전 1.6.6 이상으로 시작되는 Media Analytics 서버로 전송되어야 합니다.

1. **앱 또는 브라우저를 전경으로 다시 가져오기**

   백그라운드에서 돌아올 때 컨텐츠 재생이 재개되어야 합니다.

1. **적어도 5분 동안 중단되지 않은 상태로 기본 컨텐츠 미디어 재생**

   호출 매개 변수 및 메타데이터에 대해서는 [테스트 호출 세부 사항](/help/legacy/validation/test-call-details.md#play-main-content)을 참조하십시오.

1. **미디어 플레이어 닫기**

   미디어 플레이어를 닫으면 추가 추적 통화가 발생하지 않습니다.
