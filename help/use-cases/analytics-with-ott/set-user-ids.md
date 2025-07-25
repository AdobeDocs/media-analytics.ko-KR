---
title: 사용자 ID 설정
description: 고유한 고객 식별자 역할을 하는 사용자 ID 설정을 위한 API입니다.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Streaming Media, API"
role: User, Admin, Data Engineer
source-git-commit: 70900e305c3ed7a2be4069c6f296d56f1f6e0966
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 100%

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
