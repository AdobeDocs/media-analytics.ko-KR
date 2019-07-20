---
seo-title: 하트비트 매개 변수 설명
title: 하트비트 매개 변수 설명
uuid: E 9 DDDA 32-0952-43 D 0-A 702-49 F 5 B 1 BFD 8 CF
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# 하트비트 매개 변수 설명{#heartbeat-parameter-descriptions}

Adobe가 하트비트 서버에서 수집하고 처리하는 하트비트 매개 변수 목록입니다:

## 모든 이벤트

| 이름 | 필수/선택적 | 데이터 소스 | 설명   |
| ---  | :---: | --- | --- |
| `s:event:type` | R | Media SDK | 추적 중인 이벤트 유형입니다. 이벤트 유형: <ul> <li> `s:event:type=start` </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | R | Media SDK | 이 세션에서 같은 유형의 마지막 이벤트의 타임스탬프입니다. The value is `-1` |
| `l:event:ts` | R | Media SDK | 이벤트의 타임스탬프입니다. |
| `l:event:duration` | R | Media SDK | 이 값은 플레이어가 아닌 VHL 라이브러리에 의해 내부적으로 설정됩니다(밀리초). 백엔드에서 보낸 지표 시간을 계산하는 데 사용됩니다. `a.media.totalTimePlayed``type=play` 예를 들면 다음과 같습니다. 전송된 일부 HB에 대해 이 매개 변수를 "상태 변경 이벤트" (예: `type=complete``type=chapter_complete``type=bitrate_change` |
| `l:event:playhead` | R | `VideoInfo` | 플레이헤드는 이벤트가 기록될 때 현재 활성 자산(주 자산 또는 광고 자산) 내부에 있었습니다. |
| `s:event:sid` | R | Media SDK | 세션 ID(임의로 생성된 문자열)입니다. 특정 세션(비디오 + 광고)의 모든 이벤트는 같아야 합니다. |
| `l:asset:duration / l:asset:length` (이름이 `length``duration` | R | `VideoInfo` | 주 자산의 비디오 자산 길이입니다. |
| `s:asset:publisher` | R | `MediaHeartbeatConfig` | 자산 게시자입니다. |
| `s:asset:video_id` | R | `VideoInfo` | 게시자의 카탈로그에서 비디오를 고유하게 식별하는 ID입니다. |
| `s:asset:type` | R | Media SDK | 자산 유형(주 자산 또는 광고 자산)입니다. |
| `s:stream:type` | R | `VideoInfo` | 스트림 유형이며, 다음 중 하나일 수 있습니다. <ul> <li> `live` </li> <li> `vod` </li> <li> `linear` </li> </ul>에서 보냅니다. |
| `s:user:id` | O | 모바일, 앱 측정 VisitorID에 대한 구성 개체 | 사용자가 특별히 설정한 방문자 ID입니다. |
| `s:user:aid` | O | Experience Cloud 조직 | 사용자의 Analytics 방문자 ID 값입니다. |
| `s:user:mid` | R | Experience Cloud 조직 | 사용자의 Experience Cloud 방문자 ID 값입니다. |
| `s:cuser:customer_user_ids_x` | O | `MediaHeartbeatConfig` | Audience Manager에 설정된 모든 고객 사용자 ID입니다. |
| `l:aam:loc_hint` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:aam:blob` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:sc:rsid` | R | 보고서 세트 ID | 보고서를 전송해야 하는 SiteCatalyst RSID. |
| `s:sc:tracking_server` | R | `MediaHeartbeatConfig` | SiteCatalyst 추적 서버. |
| `h:sc:ssl` | R | `MediaHeartbeatConfig` | 트래픽이 HTTPS를 통해 전송되는지(1로 설정된 경우) 또는 HTTP를 통해 전송되는지(0으로 설정된 경우) 여부입니다. |
| `s:sp:ovp` | O | `MediaHeartbeatConfig` | Primetime 플레이어의 경우 "primetime"으로 설정되고, 다른 플레이어의 경우 실제 OVP로 설정됩니다. |
| `s:sp:sdk` | R | `MediaHeartbeatConfig` | OVP 버전 문자열입니다. |
| `s:sp:player_name` | R | `VideoInfo` | 비디오 플레이어 이름(실제 플레이어 소프트웨어, 플레이어를 식별하는 데 사용됨). |
| `s:sp:channel` | O | `MediaHeartbeatConfig` | 사용자가 컨텐츠를 보고 있는 채널입니다. 모바일 앱인 경우 앱 이름입니다. 웹 사이트인 경우 도메인 이름입니다. |
| `s:sp:hb_version` | R | Media SDK | 호출하는 VideoHeartbeat 라이브러리의 버전 번호입니다. |
| `l:stream:bitrate` | R | `QoSInfo` | 스트림 비트율의 현재 값(bps)입니다. |

## 오류 이벤트

| 이름 | 필수/선택적 | 데이터 소스 | 설명   |
| ---  | :---: | --- | --- |
| `s:event:source` | R | Media SDK | 오류 원인으로, 플레이어 내부 또는 애플리케이션 수준입니다. |
| `s:event:id` | R | Media SDK | 오류를 고유하게 식별하는 오류 ID입니다. |

## 광고 이벤트

| 이름 | 필수/선택적 | 데이터 소스 | 설명   |
| ---  | :---: | --- | --- |
| `s:asset:ad_id` | R | `AdInfo` | 광고 이름입니다. |
| `s:asset:ad_sid` | R | Media SDK | Media SDK에서 생성된 고유 식별자로, 모든 광고 관련 Ping에 추가됩니다. |
| `s:asset:pod_id` | R | Media SDK | 비디오 내부의 Pod ID입니다. 이 값은 수식을 기반으로 하여 자동으로 계산됩니다. `MD5(video_id) + "_" + [pod index]` |
| `s:asset:pod_position` | R | `AdBreakInfo` | pod 내부의 광고 색인입니다(첫 번째 광고는 색인 0, 두 번째 광고는 색인 1을 가짐). |
| `s:asset:resolver` | R | `AdBreakInfo` | 광고 확인 프로그램입니다. |
| `s:meta:custom_ad_metadata.x` | O | `MediaHeartbeat` | 사용자 지정 광고 메타데이터입니다. |

## 챕터 이벤트

| 이름 | 필수/선택적 | 데이터 소스 | 설명   |
| ---  | :---: | --- | --- |
| `s:stream:chapter_sid` | R | Media SDK | 챕터의 재생 인스턴스에 연결된 고유한 식별자입니다.  참고: 사용자가 수행한 뒤로 이동 작업으로 인해 챕터가 여러 번 재생될 수 있습니다. |
| `s:stream:chapter_name` | O | `ChapterInfo` | 챕터의 친숙한(사용자가 읽을 수 있는) 이름입니다. |
| `s:stream:chapter_id` | R | Media SDK | 챕터의 고유한 ID입니다. 이 값은 수식을 기반으로 하여 자동으로 계산됩니다. `MD5(video_id) + "_" + chapter_pos` |
| `l:stream:chapter_pos` | R | `ChapterInfo` | 챕터 목록에 있는 챕터 인덱스입니다(1로 시작). |
| `l:stream:chapter_offset` | R | `ChapterInfo` | 광고를 제외한 기본 컨텐츠 내에 있는 챕터의 오프셋(초 단위)입니다. |
| `l:stream:chapter_length` | R | `ChapterInfo` | 챕터 기간(초 단위). |
| `s:meta:custom_chapter_metadata.x` | O | `ChapterInfo` | 사용자 지정 챕터 메타데이터. |

## 세션 종료 이벤트

| 이름 | 필수/선택적 | 데이터 소스 | 설명   |
| ---  | :---: | --- | --- |
| `s:event:type=end` | R | Media SDK |  `end` `close` |

