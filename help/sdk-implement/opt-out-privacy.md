---
seo-title: 옵트아웃 및 개인 정보
title: 옵트아웃 및 개인 정보
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# 옵트아웃 및 개인 정보{#opt-out-and-privacy}

## 옵트아웃 / 옵트인 {#opt-out-opt-in}

추적 활동을 특정 장치에서 허용할지 여부를 제어할 수 있습니다.

* **모바일 앱 -** VA 라이브러리는 `AdobeMobile` 라이브러리의 개인 정보 및 옵트아웃 설정을 따릅니다. 추적을 옵트아웃하려면 `AdobeMobile` 라이브러리를 사용해야 합니다. `AdobeMobile` 라이브러리의 옵트아웃 및 개인 정보 설정에 대한 자세한 내용은 [옵트아웃 및 개인 정보 설정](https://docs.adobe.com/content/help/en/mobile-services/android/gdpr-privacy-android/privacy.html)을 참조하십시오.
* **JavaScript/브라우저 앱 -** VA 라이브러리는 `VisitorAPI` 개인 정보 보호 및 옵트아웃 설정을 따릅니다. 추적을 옵트아웃하려면 방문자 API 서비스에서 옵트아웃해야 합니다. For further information on opt­out and privacy, see [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/).
* **OTT 앱(Chromecast, Roku) - OTT SDK는** 데이터 수집 및 전송에 대한 `opt` 상태 플래그를 설정하고 로컬에 저장된 ID를 검색할 수 있는 GDPR(General Data Protection Regulation) 지원 API를 제공합니다.

   >[!NOTE]
   >
   >개인 정보 상태가 옵트아웃으로 설정된 경우 미디어 하트비트 추적 호출도 비활성화됩니다.

   다음 설정을 사용하여 Analytics 데이터가 특정 장치에서 전송되는지 여부를 제어할 수 있습니다.

   * The `privacyDefault` setting in the `ADBMobile.json` config file. 이 설정은 코드에서 변경되기 전까지 초기 설정을 제어하고 유지됩니다.

   * `ADBMobile().setPrivacyStatus()` 메서드.

      * **옵트아웃:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_OUT)
            ```
         >[!IMPORTANT]
         >
         >사용자가 추적을 옵트아웃하면 사용자가 다시 옵트인할 때까지 지속되는 장치 데이터 및 ID가 모두 삭제됩니다.

      * **다시 옵트인:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
            ```
      * **현재 설정 반환:**

         * **Chromecast:**

            ```
            ADBMobile.config.getPrivacyStatus()
            ```

         * **Roku:**

            ```
            ADBMobile().getPrivacyStatus()
            ```
   `setPrivacyStatus`를 사용하여 개인 정보 설정을 변경한 후에는 이 메서드를 사용하여 다시 변경할 때까지 또는 앱을 제거하고 다시 설치하기 전까지 변경 내용이 영구적으로 유지됩니다.

## 저장된 ID 검색(OTT 앱) {#retrieving-stored-identifiers-ott-apps}

이 정보는 Roku 앱에서 로컬로 저장된 사용자 ID를 검색하는 데 도움이 됩니다.

>[!IMPORTANT]
>
>모든 식별자를 검색하는 방법은 SDK에 의해 알려져 지속되는 모든 사용자 ID를 가져옵니다. 사용자가 옵트아웃하기 **전에** 이 메서드를 호출해야 합니다.

로컬로 저장된 ID는 다음을 포함할 수 있는 JSON 문자열로 반환됩니다.

* 회사 컨텍스트 - IMS 조직 ID
* 사용자 ID
* Experience Cloud ID(MCID)
* 데이터 소스 ID(DPID, DPUUID)
* Analytics ID(AVID, AID, VID 및 연관된 RSID)
* Audience Manager ID(UUID)

예:

* **Chromecast:**

   ```
   ADBMobile.config.getAllIdentifiersAsync(callback)
   ```

* **Roku:**

   ```
   vids = ADBMobile().getAllIdentifiers()
   ```

