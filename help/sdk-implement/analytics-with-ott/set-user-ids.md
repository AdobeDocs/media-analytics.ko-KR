---
seo-title: 사용자 ID 설정
title: 사용자 ID 설정
uuid: FDD 54 FEC -79 CD -4 BF 8-B 17 E -4 D 61 D 84 F 6310
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# 사용자 ID 설정{#set-user-ids}

사용자 ID는 애플리케이션에서 사용자에 대해 정의한 고유한 사용자 지정 방문자 ID입니다.

다음과 같이 ADBMobile SDK에서 고유한 사용자 ID를 설정하고 가져옵니다.

* **설정:**

   * **Roku:**

      ```
      ADBMobile().setUserIdentifer("app-generated-unique-id")
      ```

   * **Chromecast:**

      ```
      ADBMobile().config.setUserIdentifer("app-generated-unique-id");
      ```

* **가져오기:**

   * **Roku:**

      ```
      vid = ADBMobile().userIdentifer()
      ```

   * **Chromecast:**

      ```
      vid = ADBMobile().config.getUserIdentifer();
      ```
