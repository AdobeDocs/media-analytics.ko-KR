---
seo-title: Test 2 비디오 중단
title: Test 2 비디오 중단
uuid: Eeccd 534-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 테스트 2: 비디오 중단{#test-video-interruption}

이 테스트 사례는 인증 요청 양식의 일부로 필요하며, 모바일 중단 동작의 유효성을 검사합니다.

Download the certification request here: [Certification Request Form.](cert_req_form_nielsen.docx)

다음 순서로 이 작업을 완료하고 기록해야 합니다.

1. **비디오 플레이어 시작**

   비디오 플레이어가 시작되면 다음 호출이 다음 순서로 전송됩니다.

   1. Media Analytics 시작
   1. 하트비트 시작
   1. 하트비트 분석 시작
   위의 처음 두 호출에는 추가 메타데이터 및 변수가 포함되어 있습니다. For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md)

1. **적어도 5분 동안 중단되지 않은 상태로 기본 컨텐츠 비디오 재생**

   **컨텐츠 재생**

   기본 컨텐츠 재생 중에 하트비트 호출은 10초마다 하트비트 서버로 전송됩니다.

   For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **앱 또는 브라우저를 백그라운드로 이동**

   앱이 백그라운드에서 실행되는 동안 main:pause 호출만 VHL 버전 1.6.6 이상으로 시작되는 하트비트 서버로 전송되어야 합니다.

1. **앱 또는 브라우저를 백그라운드로 가져오기**

   백그라운드에서 돌아올 때 컨텐츠 재생이 재개되어야 합니다.

1. **적어도 5분 동안 중단되지 않은 상태로 기본 컨텐츠 비디오 재생**

   For call parameters and metadata, see [Test Call Details.](/help/sdk-implement/validation/test-call-details.md)

1. **비디오 플레이어 닫기**

   비디오 플레이어를 닫으면 추가 추적 통화가 발생하지 않습니다.

