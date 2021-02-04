---
title: Media Stream Attribution 소개
description: 추가 처리 규칙 및 사용자 지정 변수 없이 애플리케이션 작업을 미디어 추적 데이터에 연결하는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: 901539a2095b23f9108a934eb61d182b14ccd9e8
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 89%

---


# 미디어 스트림 속성

이 기능을 사용하면 추가 처리 규칙 및 사용자 지정 변수 없이도 애플리케이션 작업을 미디어 추적 데이터에 연결할 수 있습니다.

## 미디어 추적 외부의 미디어 차원

이제 미디어 스트림 속성을 사용하여 고객이 페이지 보기 수 및 사용자 지정 링크와 같은 다른 모든 분석 호출에 미디어 차원을 추가할 수 있습니다. 구현 중에 미디어 컨텍스트 데이터 매개 변수를 Analytics 추적 호출에 추가해야 합니다. 미디어에 사용되는 컨텍스트 데이터 매개 변수의 전체 목록은 [오디오 및 비디오 매개 변수](/help/metrics-and-metadata/audio-video-parameters.md)에서 확인할 수 있습니다.

또한 이 기능을 활성화할 각 보고서에 대해 관리 콘솔에서 미디어 추적 구성을 다시 활성화해야 합니다.

>[!NOTE]
>
>미디어 지표는 미디어 추적 외부에서 사용할 수 _없습니다_. 미디어 지표의 대부분이 하트비트 이벤트를 기반으로 하여 Media Analytics에서 계산되기 때문입니다. 또한 미디어 지표가 다른 구현에 의해 부풀려지지 않는 것이 중요합니다.

## 방법

아래의 JavaScript 예제에서는 이름이 &quot;Hero Banner&quot;로 설정된 사용자 지정 링크 추적 호출을 생성합니다.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Analytics 보고에서 `Show` eVar를 사용하여 데이터를 분류할 수 있으며, 추적 링크 인스턴스를 카운트할 수 있습니다. 보고 모양은 다음과 비슷합니다.

![](/assets/myShow-rpt-1.png)

## 사용 사례

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
