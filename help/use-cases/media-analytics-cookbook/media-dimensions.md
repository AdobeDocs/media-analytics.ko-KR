---
title: 미디어 스트림 속성이란 무엇입니까?
description: 추가 처리 규칙 및 사용자 정의 변수 없이도 애플리케이션 작업을 미디어 추적 데이터에 연결 방법에 대해 알아봅니다.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/G0RufpSDBB65tr4XJRvPU2keKgKxv1uDviyhqzxEVD4
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e4f5f438-eabb-4c54-9133-b817e3d125f5
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 215
ht-degree: 87%

---

# 미디어 스트림 속성 {#media-stream-attribution}

미디어 스트림 속성을 사용하면 추가 처리 규칙 및 사용자 지정 변수 없이도 애플리케이션 작업을 미디어 추적 데이터에 연결할 수 있습니다.

## 미디어 추적 외부의 미디어 차원

페이지 조회수 및 사용자 정의 링크와 같은 분석 호출에 미디어 차원을 추가할 수 있습니다. 구현 중에 미디어 컨텍스트 데이터 매개 변수를 Analytics 추적 호출에 추가해야 합니다.

특정 보고서에 이 기능을 사용하려면 Admin Console에서 미디어 추적 구성을 다시 사용하도록 설정합니다.

>[!NOTE]
>
>미디어 지표는 미디어 추적 외부에서 사용할 수 _없습니다_. 미디어 지표의 대부분이 하트비트 이벤트를 기반으로 하여 스트리밍 미디어 서비스에서 계산되기 때문입니다. 또한 미디어 지표가 다른 구현에 의해 부풀려지지 않는 것이 중요합니다.

## 미디어 스트림 속성 사용

아래의 JavaScript 예제에서는 이름이 “Hero Banner”로 설정된 사용자 정의 링크 추적 호출을 생성합니다.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Analytics 보고에서 `Show` eVar를 사용하여 데이터를 분류할 수 있으며, 추적 링크 인스턴스를 카운트할 수 있습니다. 보고 모양은 다음과 비슷합니다.

![](/assets/myShow-rpt-1.png)

## 사용 사례

다음 예는 다음에 대한 사용 사례를 보여 줍니다.

* 범주 배치
* Hero 배치
* 참여
* 구독

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
