---
title: 스트리밍 미디어용 태그를 사용하여 모바일 SDK를 설정하는 방법
description: 모바일 앱용 Adobe 스트리밍 미디어를 구현하는 방법을 알아봅니다.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 28%

---

# Mobile SDK 설치 {#install-mobile-sdks}

Android 또는 iOS에서 모바일 앱용 스트리밍 미디어를 구현하려면 다음을 설치 및 구성합니다.

* **Adobe Experience Platform Mobile SDK**

   데이터를 수집하려면 Adobe Experience Platform에서 태그를 사용합니다. Adobe Experience Platform의 태그는 다른 태그 지정 요구 사항과 함께 Analytics 코드를 배포할 수 있도록 해 주는 태그 관리 솔루션입니다.

* **Android용 Media SDK** 또는 **iOS용 Media SDK**

* **Adobe Media Analytics for Audio 및 Video 확장**

SDK를 다운로드하고 추가 설명서 리소스를 보려면 [Media SDK, 태그를 사용한 확장 프로그램 및 OTT SDK를 가져옵니다](/help/getting-started/download-sdks.md)

* **올바른 구성 매개 변수 가져오기**

   이러한 매개 변수는 Analytics 계정을 설정한 후 Adobe 담당자에게서 얻을 수 있습니다.

* **미디어 플레이어에 다음 API 포함**

   * *플레이어 이벤트에 가입할 API* - Media SDK를 사용하려면 이벤트가 플레이어에서 발생할 때 단순 API 세트를 호출해야 합니다.

   * *플레이어 정보를 제공하는 API* - 현재 재생 중인 미디어 이름, 재생 헤드 위치, 광고 또는 장 등의 정보가 포함됩니다.