---
seo-title: 개요
title: 개요
uuid: D 71429 E 6-EF 8 B -4 EA 2-8491-FF 3 CDBF 4357 F
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 개요{#overview}

>[!IMPORTANT]
>
>다음은 모든 2.x SDK에 구현과 관련된 지침입니다. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 오류 추적 구현

1. 미디어 플레이어 오류를 추적할 수 있습니다.

   오류 이벤트에서 오류 정보로 `trackError`를 호출하십시오.

>[!NOTE]
>
>미디어 플레이어 오류를 추적해도 미디어 추적 세션이 중지되지 않습니다. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

