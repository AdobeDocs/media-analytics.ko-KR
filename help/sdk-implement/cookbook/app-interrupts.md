---
seo-title: 재생 중 애플리케이션 중단 처리
title: 재생 중 애플리케이션 중단 처리
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# 재생 중 애플리케이션 중단 처리{#handling-application-interrupts-during-playback}

미디어 애플리케이션에서 재생은 다음과 같은 다양한 방식으로 중단될 수 있습니다.사용자가 명시적으로 일시 중지를 누르거나 사용자가 응용 프로그램을 백그라운드에 놓을 때 미디어 재생 중단의 원인이 무엇이든지 추적 지침은 동일합니다.

1. Call **`trackPause`** when the application is interrupted (goes to background, media pauses, etc.).
1. Call **`trackPlay`** when the application returns to the foreground and/or the media resumes playing.

>[!NOTE]
>
>The Media Analytics team has seen instances where customers called `trackSessionStart` when their app returned from the background. 이렇게 하면 이전 진행률 마커, 세그먼트 등이 손실되면서 총 재생 시간을 계산하지 않는 지점까지 재생이 수행됩니다. Instead, call `trackPlay` when the app returns and/or the media resumes playing.

## 애플리케이션 중단 처리에 대한 FAQ: {#faq-about-handling-application-interrupts}

* _앱은 얼마나 오래 배경에서 실행되어야 세션이 닫힙니까?_

   애플리케이션이 배경 재생을 허용하는 경우 애플리케이션은 Adobe의 API를 호출하여 추적을 계속할 수 있으며 Adobe의 모든 일반 추적 ping이 전송됩니다. YouTube Red를 제외하고 백그라운드 재생을 허용하는 비디오 앱은 많지 않지만 모든 오디오 앱에서 이를 허용합니다. 애플리케이션에서 백그라운드 재생을 허용하지 않는 경우 1분 동안 일시 중지 상태를 유지한 다음 추적 세션을 종료하는 것이 좋습니다. 일시 중지 ping을 계속 보낼 수 없습니다. 대부분의 경우 사용자가 다시 돌아와 미디어를 계속 볼 것인지 또는 언제 종료될지 알 수 없으므로 응용 프로그램이 계속 일시 중지 ping을 보낼 수 없습니다. 또한 배경에 있을 때 ping을 계속 전송하는 것도 바람직하지 않습니다.

* _앱이 오랜 시간 동안 배경에 있었는데 추적을 다시 시작하려 할 때 처리하는 올바른 방법은 무엇입니까?_

   애플리케이션이 `trackSessionEnd`를 호출하여 추적 세션을 종료해야 합니다. 버전 2.1부터 SDK는 "end" ping을 전송하여 추적 세션이 닫혔음을 백엔드에 알립니다.

* _동일한 세션을 다시 시작하는 것은 어떻습니까?_ 

   추적 세션을 다시 시작하는 방법에 대한 자세한 지침은 [비활성화 세션 다시 시작 페이지를 참조하십시오.](/help/sdk-implement/cookbook/resuming-inactive.md) SDK가 재개 ping을 전송하여 사용자가 세션을 수동으로 재개하고 있음을 백엔드에 알립니다.

