---
title: 사용자 ID 설정
description: 사용자 ID를 설정하는 API를 참조하십시오.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

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
