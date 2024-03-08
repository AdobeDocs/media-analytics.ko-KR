---
title: 하트비트 매개 변수 설명
description: Adobe가 Media Analytics(하트비트) 서버에서 수집하고 처리하는 하트비트 매개 변수를 살펴봅니다.
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
exl-id: ffa67b5e-ee54-4a5b-8064-decd108f944b
feature: "Media Analytics, Variables"
role: User, Admin, Data Engineer
source-git-commit: 917c87d759a43f124dfb3e3ac7f6a441c65fde94
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 99%

---

# Media Analytics(하트비트) 매개 변수 설명{#heartbeat-parameter-descriptions}

Adobe가 Media Analytics(하트비트) 서버에서 수집하고 처리하는 Media Analytics 매개 변수 목록입니다.

## 모든 이벤트

| 이름 | 데이터 소스 |  설명  |
| ---  | --- | --- |
| `s:event:type` | Media SDK | (필수)<br/><br/>추적 중인 이벤트 유형입니다. 이벤트 유형: <ul> <li> s:event:type=start </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | Media SDK | (필수)<br/><br/>이 세션에서 같은 유형의 마지막 이벤트의 타임스탬프입니다. 값은 -1입니다. |
| `l:event:ts` | Media SDK | (필수)<br/><br/>이벤트의 타임스탬프입니다. |
| `l:event:duration` | Media SDK | (필수)<br/><br/>이 값은 플레이어가 아닌 Media SDK에 의해 내부적으로 설정됩니다(밀리초). 백엔드에서 보낸 지표 시간을 계산하는 데 사용됩니다. 예: a.media.totalTimePlayed는 생성된 모든 Play(type=play) 하트비트에 대한 기간 합계로 계산됩니다. <br/>*참고:* 이 매개 변수는 &quot;상태 변경 이벤트&quot;(예: type=complete, type=chapter_complete 또는 type=bitrate_change)이므로 특정 이벤트에 대해 0으로 설정됩니다. |
| `l:event:playhead` | VideoInfo | (필수)<br/><br/>플레이헤드는 이벤트가 기록될 때 현재 활성 자산(주 자산 또는 광고 자산) 내부에 있었습니다. |
| `s:event:sid` | Media SDK | (필수)<br/><br/>세션 ID(임의로 생성된 문자열)입니다. 특정 세션(비디오 + 광고)의 모든 이벤트는 같아야 합니다. |
| `l:asset:duration` / `l:asset:length` <br/>(길이 지속 시간에서 이름이 변경됨) | VideoInfo | (필수)<br/><br/>주 자산의 비디오 자산 길이입니다. |
| `s:asset:publisher` | MediaHeartbeatConfig | (필수)<br/><br/>자산 게시자입니다. |
| `s:asset:video_id` | VideoInfo | (필수)<br/><br/>게시자의 카탈로그에서 비디오를 고유하게 식별하는 ID입니다. |
| `s:asset:type` | Media SDK | (필수)<br/><br/>자산 유형(주 자산 또는 광고 자산)입니다. |
| `s:stream:type` | VideoInfo | (필수)<br/><br/>스트림 유형입니다. 다음 중 하나일 수 있습니다. <ul> <li> live </li> <li> vod </li> <li> linear </li> </ul> |
| `s:user:id` | 모바일, 앱 측정 VisitorID에 대한 구성 개체 | (선택 사항)<br/><br/>사용자가 특별히 설정한 방문자 ID입니다. |
| `s:user:aid` | Experience Cloud 조직 | (선택 사항)<br/><br/>사용자의 Analytics 방문자 ID 값입니다. |
| `s:user:mid` | Experience Cloud 조직 | (필수)<br/><br/>사용자의 Experience Cloud 방문자 ID 값입니다. |
| `s:cuser:customer_user_ids_x` | MediaHeartbeatConfig | (선택 사항)<br/><br/>Audience Manager에 설정된 모든 고객 사용자 ID입니다. |
| `l:aam:loc_hint` | MediaHeartbeatConfig | (필수)<br/><br/>aa_start 후에 각 페이로드에 전송된 AAM 데이터 |
| `s:aam:blob` | MediaHeartbeatConfig | (필수)<br/><br/>aa_start 후에 각 페이로드에 전송된 AAM 데이터 |
| `s:sc:rsid` | 보고서 세트 ID | (필수)<br/><br/>보고서를 전송해야 하는 Adobe Analytics RSID입니다. |
| `s:sc:tracking_server` | MediaHeartbeatConfig | (필수)<br/><br/>Adobe Analytics 추적 서버입니다. |
| `h:sc:ssl` | MediaHeartbeatConfig | (필수)<br/><br/>트래픽이 HTTPS를 통해 전송되는지(1로 설정된 경우) 또는 HTTP를 통해 전송되는지(0으로 설정된 경우) 여부입니다. |
| `s:sp:ovp` | MediaHeartbeatConfig | (선택 사항)<br/><br/>Primetime 플레이어의 경우 &quot;primetime&quot;으로 설정되고, 다른 플레이어의 경우 실제 OVP로 설정됩니다. |
| `s:sp:sdk` | MediaHeartbeatConfig | (필수)<br/><br/>OVP 버전 문자열입니다. |
| `s:sp:player_name` | VideoInfo | (필수)<br/><br/>비디오 플레이어 이름(실제 플레이어 소프트웨어, 플레이어를 식별하는 데 사용됨)입니다. |
| `s:sp:channel` | MediaHeartbeatConfig | (선택 사항)<br/><br/>사용자가 콘텐츠를 보고 있는 채널입니다. 모바일 앱의 경우 앱 이름입니다. 웹 사이트의 경우 도메인 이름입니다. |
| `s:sp:hb_version` | Media SDK | (필수)<br/><br/>호출을 실행하는 Media SDK 라이브러리의 버전 번호입니다. |
| `l:stream:bitrate` | QoSInfo | (필수)<br/><br/>스트림 비트율의 현재 값(bps)입니다. |

## 오류 이벤트

| 이름 | 데이터 소스 | 설명   |
| ---  | --- | --- |
| `s:event:source` | Media SDK | (필수)<br/><br/>오류 원인으로, 플레이어 내부 또는 애플리케이션 수준입니다. |
| `s:event:id` | Media SDK | (필수)<br/><br/>오류를 고유하게 식별하는 오류 ID입니다. |

## 광고 이벤트

| 이름 | 데이터 소스 | 설명   |
| ---  | --- | --- |
| `s:asset:ad_id` | AdInfo | (필수)<br/><br/>광고의 이름입니다. |
| `s:asset:ad_sid` | Media SDK | (필수)<br/><br/>Media SDK에서 생성된 고유 식별자로, 모든 광고 관련 Ping에 추가됩니다. |
| `s:asset:pod_id` | Media SDK | (필수)<br/><br/>비디오 내부의 Pod ID입니다. 이 값은 다음 수식을 기반으로 하여 자동으로 계산됩니다. <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| `s:asset:pod_position` | AdBreakInfo | (필수)<br/><br/>pod 내부의 광고 색인입니다(첫 번째 광고는 색인 0, 두 번째 광고는 색인 1을 가짐). |
| `s:asset:resolver` | AdBreakInfo | (필수)<br/><br/>광고 해결자입니다. |
| `s:meta:custom_ad_metadata.x` | MediaHeartbeat | (선택 사항)<br/><br/>사용자 지정 광고 메타데이터입니다. |

## 챕터 이벤트

| 이름 | 데이터 소스 | 설명   |
| ---  | --- | --- |
| `s:stream:chapter_sid` | Media SDK | (필수)<br/><br/>챕터의 재생 인스턴스에 연결된 고유한 식별자입니다. <br/> **참고:** 사용자가 수행한 뒤로 이동 작업으로 인해 챕터가 여러 번 재생될 수 있습니다. |
| `s:stream:chapter_name` | ChapterInfo | (선택 사항)<br/><br/>챕터의 친숙한(사용자가 읽을 수 있는) 이름입니다. |
| `s:stream:chapter_id` | Media SDK | (필수)<br/><br/>챕터의 고유한 ID입니다. 이 값은 다음 수식을 기반으로 하여 자동으로 계산됩니다. <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| `l:stream:chapter_pos` | ChapterInfo | (필수)<br/><br/>챕터 목록에 있는 챕터 인덱스입니다(1로 시작). |
| `l:stream:chapter_offset` | ChapterInfo | (필수)<br/><br/>광고를 제외한 기본 콘텐츠 내에 있는 챕터의 오프셋(초 단위)입니다. |
| `l:stream:chapter_length` | ChapterInfo | (필수)<br/><br/>챕터 기간(초 단위)입니다. |
| `s:meta:custom_chapter_metadata.x` | ChapterInfo | (선택 사항)<br/><br/>사용자 지정 챕터 메타데이터입니다. |

## 세션 종료 이벤트

| 이름 | 데이터 소스 | 설명   |
| ---  | --- | --- |
| `s:event:type=end` | Media SDK | (필수)<br/><br/> `end` `close` |
