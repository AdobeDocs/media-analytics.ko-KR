---
seo-title: Test 2 미디어 중단
title: Test 2 미디어 중단
uuid: Eeccd 534-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: 5822e634c51cb53a60400623d115c6d862dad44f

---


# 테스트 2: 미디어 중단{#test-media-interruption}

이 테스트 케이스는 모바일 중단 비헤이비어를 확인합니다. 이것은 인증 요청의 필수 요소입니다.

## 인증 요청 양식

**여기에서 인증 요청 양식을 다운로드하십시오. = = &gt;**  [Certification Request Form.](cert_req_form.docx)

## 테스트 절차

다음 순서로 이 작업을 완료하고 기록해야 합니다.

1. **미디어 플레이어 시작**

   미디어 플레이어가 시작되면 다음 순서로 다음 호출이 전송됩니다.

   1. Adobe Analytics (appmeasurement) 시작
   1. 미디어 분석 (하트 비트) 시작
   1. 미디어 분석 (하트 비트) Adobe Analytics 시작 호출이 요청됨
   위의 처음 두 호출에는 추가 메타데이터 및 변수가 포함되어 있습니다. 호출 매개 변수 및 메타데이터의 경우 테스트 호출 세부 정보를 참조하십시오 [.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   위의 세 번째 호출은 미디어 SDK가 Adobe Analytics 시작 호출 (`pev2=ms_s`) 이 Adobe Analytics 서버로 전송되도록 미디어 SDK를 요청합니다.

1. **최소 5 분 동안 기본 컨텐츠 재생 중단**

   **컨텐츠 재생**

   컨텐츠 재생 중에 미디어 SDK는 10 초마다 play 호출 (하트 비트) 를 Media Analytics 서버로 전송합니다.

   호출 매개 변수 및 메타데이터의 경우 테스트 호출 세부 정보를 참조하십시오 [.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **앱 또는 브라우저를 백그라운드로 이동**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **앱 또는 브라우저를 다시 전경으로 가져오기**

   백그라운드에서 돌아올 때 컨텐츠 재생이 재개되어야 합니다.

1. **최소 5 분 동안 기본 컨텐츠 미디어 재생 중단**

   호출 매개 변수 및 메타데이터의 경우 테스트 호출 세부 정보를 참조하십시오 [.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Close Media Player**

   미디어 플레이어를 닫으면 추가 추적 호출이 실행되지 않습니다.

