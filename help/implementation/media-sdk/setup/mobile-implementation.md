---
title: Streaming Media용 태그를 사용하여 모바일 SDK를 설정하는 방법
description: 모바일 앱용 Adobe Streaming Media를 구현하는 방법에 대해 알아봅니다.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 81%

---

# 모바일 SDK 설치 {#install-mobile-sdks}

Android 또는 iOS에서 모바일 앱용 Streaming Media Collection 추가 기능을 구현하려면 다음을 설치하고 구성합니다.

* **Adobe Experience Platform Mobile SDK**

  데이터를 수집하려면 다음 중 하나를 사용합니다.
   * Adobe Experience Platform의 태그. Adobe Experience Platform의 태그는 다른 태그 지정 요구 사항과 함께 Analytics 코드를 배포할 수 있도록 해 주는 태그 관리 솔루션입니다.
   * Adobe Experience Platform Edge

* **Android용 Media SDK** 또는 **iOS용 Media SDK**

* **오디오 및 비디오용 Adobe Media Analytics 확장 프로그램**

SDK를 다운로드하고 추가 설명서 리소스를 보려면 [Media SDK, 태그를 사용한 확장 기능 및 OTT SDK 가져오기](/help/getting-started/download-sdks.md)를 참조하십시오.

* **유효한 구성 매개 변수 얻기**

  이러한 매개 변수는 분석 계정을 설정한 후에 Adobe 담당자로부터 얻을 수 있습니다.

* **미디어 플레이어에서 다음 API 포함**

   * *플레이어 이벤트에 가입할 API* - Media SDK를 사용하려면 이벤트가 플레이어에서 발생할 때 단순 API 세트를 호출해야 합니다.

   * *플레이어 정보를 제공하는 API* - 여기에는 미디어 이름, 재생 헤드 위치, 광고 또는 챕터와 같이 현재 재생 중인 정보가 포함됩니다.
