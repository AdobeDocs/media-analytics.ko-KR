---
seo-title: Test 2  Media interruption
title: Test 2  Media interruption
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: 5822e634c51cb53a60400623d115c6d862dad44f

---


# Test 2: Media interruption{#test-media-interruption}

This test case validates mobile interruption behavior. 인증 요청의 필수 요소입니다.

## 인증 요청 양식

**여기에서 인증 요청 양식을 다운로드하십시오.==&gt;**&#x200B;인증 [요청 양식.](cert_req_form.docx)

## 테스트 절차

다음 순서로 이 작업을 완료하고 기록해야 합니다.

1. **미디어 플레이어 시작**

   When the media player starts, the following calls are sent in the following order:

   1. Adobe Analytics (AppMeasurement) Start
   1. 미디어 분석(하트비트) 시작
   1. 미디어 분석(하트비트) Adobe Analytics 시작 호출이 요청됨
   위의 처음 두 호출에는 추가 메타데이터와 변수가 포함됩니다. 호출 매개 변수 및 메타데이터에 대해서는 호출 세부 [사항 테스트를 참조하십시오.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   위의 세 번째 호출은 Media Analytics 서버에 Adobe Analytics 시작 호출(`pev2=ms_s`)을 Adobe Analytics 서버로 보내도록 미디어 SDK가 요청했음을 알려줍니다.

1. **중단 없이 최소 5분 동안 주요 컨텐츠 재생**

   **컨텐츠 재생**

   컨텐츠를 재생하는 동안 Media SDK는 10초마다 재생 호출(하트비트)을 Media Analytics 서버로 전송합니다.

   호출 매개 변수 및 메타데이터에 대해서는 호출 세부 [사항 테스트를 참조하십시오.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **앱 또는 브라우저를 백그라운드로 이동**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **앱 또는 브라우저를 전경으로 되돌리기**

   백그라운드에서 돌아올 때 컨텐츠 재생이 재개되어야 합니다.

1. **중단 없이 최소 5분 동안 주요 컨텐츠 미디어 재생**

   호출 매개 변수 및 메타데이터에 대한 자세한 내용은 테스트 [호출 세부 사항을 참조하십시오.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **미디어 플레이어 닫기**

   미디어 플레이어를 닫은 후에는 추가 추적 호출을 실행할 수 없습니다.

