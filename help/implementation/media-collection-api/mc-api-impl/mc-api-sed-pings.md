---
title: Ping 이벤트 보내기
description: Ping 이벤트는 Adobe 스트리밍 미디어 서비스의 하트비트입니다. 주요 콘텐츠 또는 광고 추적을 위해 시간이 지정된 ping을 보내는 방법에 대해 알아봅니다.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 50%

---

# Ping 이벤트 보내기{#sending-ping-events}

**전송한 다른 API 이벤트와 관계없이 재생 10초 후부터 ping 이벤트를 10초마다 실행해야 합니다. 기본 콘텐츠와 광고 추적 모두에 적용됩니다.**

ping 이벤트는 Adobe 스트리밍 미디어 서비스의 &quot;하트비트&quot;입니다. ping 호출에 대한 유일한 필수 매개 변수는 `playerTime` 개체(플레이헤드 위치 및 타임스탬프)와 함께`eventType: ping`입니다.

다음 코드 조각은 기본 콘텐츠에 대해 시간이 지정된 메커니즘 ping 테스트를 구현하는 한 가지 방법을 보여 줍니다(10초 간격).

```js
... 
Pinger.init(10000); 
... 
Pinger.kill();

var Pinger = { 
    init: function(interval) { 
        this._timer = window.setInterval(function() { 
                $.event.trigger({type: "onPing", _data: ""}); 
            }, interval); 
    }, 
     
    kill: function() { 
        window.clearInterval(this._timer); 
    } 
}
```
