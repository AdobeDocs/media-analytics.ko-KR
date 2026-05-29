---
title: 옵트아웃 및 개인 정보 보호 설명
description: 옵트인, 옵트아웃 및 개인정보 보호를 처리하는 방법에 대해 알아봅니다.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eF09wxu2mIUoFph5EdHz5y0XtcpXHHLINqSGLQEMoHU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: 750
ht-degree: 4%

---

# 옵트아웃 및 개인정보 보호

사용자가 추적을 옵트아웃하면 스트리밍 미디어 라이브러리는 즉시 모든 데이터 수집 활동을 중지합니다. 해당 사용자에 대해 세션 시작 호출, 하트비트 Ping 및 이벤트 추적 데이터가 Adobe 데이터 수집 서버로 전송되지 않습니다.

## 옵트아웃 / 옵트인

옵트아웃 컨트롤은 장치 또는 브라우저별로 작동합니다. 사용자 동의를 존중하는 것은 구현 조직의 책임입니다. Adobe의 개인 정보 보호 방침에 대한 개요는 [Adobe 개인 정보 보호 센터](https://www.adobe.com/kr/privacy.html)를 참조하십시오.

## 권장 구현 유형

>[!BEGINTABS]

>[!TAB 웹 SDK]

웹 SDK은 `setConsent` 명령을 사용하여 설정된 동의 환경 설정을 준수합니다. 동의가 `"out"`(으)로 설정되면 웹 SDK에서 스트리밍 미디어 추적 호출을 포함한 모든 이벤트를 Edge Network으로 전달하는 것을 중지합니다. 동의 상태는 세션 간 브라우저 스토리지에서 유지됩니다.

옵트아웃을 구현하기 전에 웹 SDK이 스트리밍 미디어 구성 요소로 구성되었는지 확인하십시오. 자세한 내용은 [웹 SDK 설정](../implementation/edge/edge-web-sdk.md)을 참조하세요.

Adobe 2.0 동의 표준을 사용하여 동의 를 옵트아웃에 설정합니다.

```javascript
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: { val: "n" }
    }
  }]
});
```

동의 값:

* `"y"`: 옵트인(데이터 수집 허용)
* `"n"`: 옵트아웃(데이터 수집이 제외됨)
* `"p"`: 보류 중(사용자 결정 대기 중, 확인될 때까지 수집된 데이터 없음)

추적을 복원하려면 `"y"`을(를) `collect.val` 값으로 사용하여 `setConsent`을(를) 다시 호출하십시오.

IAB TCF 2.0을 포함한 다른 형식은 웹 SDK 설명서에서 [setConsent 명령](https://experienceleague.adobe.com/ko/docs/experience-platform/web-sdk/commands/setconsent)을 참조하십시오.

>[!TAB iOS]

Adobe Experience Platform Mobile SDK은 `MobileCore.setPrivacyStatus()`을(를) 사용하여 설정된 개인 정보 상태를 준수합니다. 상태를 `.optedOut`(으)로 설정하면 Streaming Media를 포함한 모든 AEP 확장에 대한 모든 데이터 수집이 억제됩니다. 상태는 앱 세션 간에 지속됩니다.

```swift
MobileCore.setPrivacyStatus(.optedOut)
```

추적을 복원하려면 개인 정보 상태를 `.optedIn`(으)로 다시 설정합니다.

```swift
MobileCore.setPrivacyStatus(.optedIn)
```

자세한 내용은 AEP Mobile SDK 설명서에서 [개인 정보 및 GDPR](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus)을 참조하십시오.

>[!TAB Android]

Adobe Experience Platform Mobile SDK은 `MobileCore.setPrivacyStatus()`을(를) 사용하여 설정된 개인 정보 상태를 준수합니다. 상태를 `MobilePrivacyStatus.OPT_OUT`(으)로 설정하면 Streaming Media를 포함한 모든 AEP 확장에 대한 모든 데이터 수집이 억제됩니다. 상태는 앱 세션 간에 지속됩니다.

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT)
```

추적을 복원하려면 개인 정보 상태를 `MobilePrivacyStatus.OPT_IN`(으)로 다시 설정합니다.

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_IN)
```

자세한 내용은 AEP Mobile SDK 설명서에서 [개인 정보 및 GDPR](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus)을 참조하십시오.

>[!TAB Roku]

AEP Roku SDK은 Adobe 2.0 동의 표준과 함께 `setConsent()`을(를) 사용합니다. `collect.val`을(를) `"n"`(으)로 설정하면 스트리밍 미디어 이벤트를 포함한 모든 데이터 수집이 즉시 중지됩니다.

동의 값:

* `"y"` — 옵트인(데이터 수집 허용)
* `"n"` — 옵트아웃(데이터 수집이 제외됨)
* `"p"` — 보류 중(사용자 결정 대기 중, 확인될 때까지 수집된 데이터 없음)

```brightscript
currentDate = CreateObject("roDateTime")
timestampInISO8601 = currentDate.ToISOString("milliseconds")

collectConsentNo = {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "metadata": { "time": timestampInISO8601 },
      "collect": { "val": "n" }
    }
  }]
}

m.aepSdk.setConsent(collectConsentNo)
```

추적을 복원하려면 `collect.val`을(를) `"y"`(으)로 설정하고 `setConsent()`을(를) 다시 호출하십시오.

`ADB_CONSTANTS.CONFIGURATION.CONSENT_DEFAULT` 키와 함께 `updateConfiguration()`을(를) 사용하여 SDK 초기화 시 기본 동의 값을 설정할 수도 있습니다. 자세한 내용은 [AEP Roku SDK 설명서](https://github.com/adobe/aepsdk-roku)를 참조하세요.

>[!TAB 미디어 Edge API]

Media Edge API는 서버측 구현입니다. 자동으로 동의를 강제하는 SDK 레이어가 없습니다. 애플리케이션이 API를 호출하기 전에 사용자 동의 상태를 확인하고 옵트아웃된 사용자에 대한 요청을 억제해야 합니다.

전체 옵트아웃의 경우 옵트아웃한 사용자의 `/va/v2/sessions` 엔드포인트(또는 후속 이벤트 엔드포인트)에 POST를 수행하지 마십시오.

```javascript
// Check consent status before initiating a media session
if (userHasOptedOut) {
  // Do not call the Media Edge API
  return;
}

// Only call the API for users who have not opted out
fetch("https://edge.adobedc.net/va/v2/sessions", {
  method: "POST",
  body: JSON.stringify(sessionStartPayload)
});
```

자세한 내용은 [Media Edge API 참조](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)를 참조하십시오.

>[!ENDTABS]

## 이전 구현 유형(Analytics 전용)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Media SDK JS 3.x 라이브러리는 Adobe 방문자 API(ID 서비스) 옵트아웃 상태를 따릅니다. 사용자가 방문자 API를 사용하여 옵트아웃하면 Media SDK은 모든 추적 호출을 자동으로 억제합니다.

```javascript
var visitor = Visitor.getInstance("YOUR_ORG_ID@AdobeOrg");
visitor.setOptOut(true);
```

`YOUR_ORG_ID@AdobeOrg`을(를) Adobe Admin Console의 조직 ID로 바꾸십시오.

추적을 복원하려면 `false`을(를) `setOptOut()`에 전달합니다.

자세한 내용은 [Adobe Experience Platform ID 서비스](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ko)를 참조하십시오.

>[!TAB Chromecast]

Chromecast Media SDK 3.x는 `ADBMobile.config.setPrivacyStatus()`을(를) 사용하여 설정된 개인 정보 상태를 따릅니다. 상태를 `PRIVACY_STATUS_OPT_OUT`(으)로 설정하면 모든 데이터 수집이 제외됩니다.

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT);
```

추적을 복원하려면 상태를 다시 옵트인으로 설정합니다.

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN);
```

`ADBMobileConfig` 개체에서 SDK 초기화 시 기본 개인 정보 상태를 설정할 수도 있습니다.

```javascript
var ADBMobileConfig = {
  "analytics": {
    "privacyDefault": "optedout"
  }
};
```

>[!TAB 미디어 컬렉션 API]

Media Collection API는 서버측 구현입니다. 애플리케이션이 API를 호출하기 전에 사용자 동의 상태를 확인하고 옵트아웃 사용자에 대한 요청을 억제해야 합니다.

전체 옵트아웃의 경우 옵트아웃한 사용자의 세션 엔드포인트에 POST를 수행하지 마십시오.

CCPA에서 부분 옵트아웃을 수행하려면 `sessionStart` 요청의 `params` 개체에 옵트아웃 플래그를 포함하십시오.

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "analytics.optOutServerSideForwarding": true,
    "analytics.optOutShare": true
  }
}
```

* `analytics.optOutServerSideForwarding`: Adobe Analytics과 다른 Experience Cloud 솔루션(예: Audience Manager) 간에 공유되는 데이터를 옵트아웃하려면 `true`(으)로 설정합니다.
* `analytics.optOutShare`: 다른 Adobe Analytics 클라이언트와의 페더레이션 데이터 공유를 옵트아웃하려면 `true`(으)로 설정하십시오.

사용 가능한 매개 변수의 전체 목록을 보려면 [Media Collection API 요청 매개 변수 참조](../implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)를 참조하십시오.

>[!ENDTABS]
