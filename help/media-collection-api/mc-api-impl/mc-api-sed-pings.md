---
seo-title: Ping 이벤트 보내기
title: Ping 이벤트 보내기
uuid: C 92 C 1 A 92-3 AF 6-4474-9 E 42-FFB 8 F 6 C 94 B 33
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Ping 이벤트 보내기{#sending-ping-events}

**기본 컨텐츠의 경우 전송한 다른 API 이벤트와 관계없이 재생 10초 후부터 ping 이벤트를 10초마다 실행해야 합니다. For Ad tracking, you must fire ping events every 1 second.**

ping 이벤트는 미디어 분석의 "하트비트" 입니다. ping 호출에 대한 유일한 필수 매개 변수는   개체(플레이헤드 위치 및 타임스탬프)와 함께 `eventType: ping``playerTime`입니다. 

다음 코드 조각은 기본 컨텐츠에 대해 시간이 지정된 메커니즘 ping 테스트를 구현하는 한 가지 방법을 보여 줍니다(10초 간격).

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

