---
title: Adobe Experience Platform 및 Customer Journey Analytics에 대한 Media Analytics 매개 변수 매핑
description: Analytics Source 커넥터 및 Customer Journey Analytics과 함께 사용되는 Media Analytics 매개 변수에 대한 XDM 필드 패스 매핑.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 79203a2f-8158-44f2-83b2-146179be9180
TQID: https://experienceleague.adobe.com/ct8mDbIpg15Jzvf1MRaG4XFtuxbq-EUKPe106zyO7zQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 1325
ht-degree: 20%

---

# Adobe Experience Platform 및 Customer Journey Analytics에 대한 Media Analytics 매개 변수 매핑

이 문서에서는 Adobe Experience Platform 및 Customer Journey Analytics 내에서 사용되는 모든 Media Analytics 매개 변수의 포괄적인 목록을 제공합니다. 각 매개 변수를 해당 XDM 필드 경로에 매핑하여 [Analytics Source 커넥터](https://experienceleague.adobe.com/ko/docs/experience-platform/sources/connectors/adobe-applications/analytics) 또는 [분류용 Analytics Source 커넥터](https://experienceleague.adobe.com/kr/docs/experience-platform/sources/connectors/adobe-applications/classifications)를 통해 Adobe Analytics에서 플랫폼으로 가져온 데이터의 통합을 지원하기 위한 것입니다.

>[!NOTE]
>
>이 참조는 Adobe Analytics 보고 또는 다른 Platform 서비스와 함께 사용할 수 있도록 스트리밍 미디어 데이터를 Customer Journey Analytics에서 Adobe Experience Platform으로 가져오기 위해 [Analytics 소스 커넥터](https://experienceleague.adobe.com/ko/docs/experience-platform/sources/connectors/adobe-applications/analytics)를 사용하는 조직에 적용됩니다. 이러한 변경 사항은 데이터 수집, 처리 및 보고를 포함하여 독립 실행형 애플리케이션으로서의 Adobe Analytics에 영향을 주지 않습니다.

## Media Analytics 예약 변수

2025년 10월부터 `media.mediaTimed` XDM 필드 경로는 완전히 더 이상 사용되지 않으며 `mediaReporting`(으)로 대체됩니다. 2025년 10월 이후에 수집된 데이터에는 `mediaReporting`개의 필드만 포함됩니다. 이전 데이터는 이전 필드 경로에서 사용할 수 있으며, 아래 표에 **이전 XDM 필드**&#x200B;에 반영됩니다.

### Keep-alive 호출 동작

스트리밍 미디어용 Analytics 소스 커넥터를 사용하면 Adobe Analytics의 keep-alive 호출이 이제 Adobe Experience Platform으로 수집됩니다. 이 경우 Customer Journey Analytics 보고에 영향을 줄 수 있습니다.

* **세션 수**: Keep-alive 호출은 직접적인 미디어 상호 작용 없이도 활성 사용자 세션을 유지하는 데 도움이 됩니다. 이러한 호출은 미디어 재생당 마지막 이벤트 후 20분마다 생성됩니다. 최적의 세션 추적을 보장하려면 데이터 보기에서 방문 만료를 30분으로 구성합니다.

* **이벤트 카운트**: Keep-alive 호출은 이제 Customer Journey Analytics 이벤트 지표에 포함됩니다. 제외하려면 이벤트 유형이 `media.keepalive`인 이벤트를 제외하는 필터를 만드십시오.

## 스트리밍 미디어 매개 변수

| 필드 이름 | 이전 XDM 필드 | 보고 XDM 필드 패스 | 데이터 유형 | 파생 필드 | 참고 |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL 스트림 형식]](/help/reporting/dimensions/stream-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.streamType` | `xdm.mediaReporting.`<br>`sessionDetails.streamType` | 차원 | [[!UICONTROL 스트림 형식]](/help/reporting/dimensions/stream-type.md) | |
| [[!UICONTROL 콘텐츠 ID]](/help/reporting/dimensions/asset-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id` | `xdm.mediaReporting.`<br>`sessionDetails.name` | 차원 | [[!UICONTROL 콘텐츠 ID]](/help/reporting/dimensions/asset-id.md) | |
| [[!UICONTROL 콘텐츠 길이]](/help/reporting/dimensions/content-length.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`sessionDetails.length` | 차원 | [[!UICONTROL 콘텐츠 길이]](/help/reporting/dimensions/content-length.md) | |
| [[!UICONTROL 콘텐츠 형식]](/help/reporting/dimensions/content-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastContentType` | `xdm.mediaReporting.`<br>`sessionDetails.contentType` | 차원 | [[!UICONTROL 콘텐츠 형식]](/help/reporting/dimensions/content-type.md) | |
| [[!UICONTROL 미디어 세션 ID]](/help/reporting/dimensions/media-session-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails._id` | `xdm.mediaReporting.`<br>`sessionDetails.ID` | 차원 | [[!UICONTROL 미디어 세션 ID]](/help/reporting/dimensions/media-session-id.md) | |
| [[!UICONTROL 콘텐츠 플레이어 이름]](/help/reporting/dimensions/content-player-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`sessionDetails.playerName` | 차원 | [[!UICONTROL 콘텐츠 플레이어 이름]](/help/reporting/dimensions/content-player-name.md) | |
| [[!UICONTROL 콘텐츠 채널]](/help/reporting/dimensions/content-channel.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastChannel` | `xdm.mediaReporting.`<br>`sessionDetails.channel` | 차원 | [[!UICONTROL 콘텐츠 채널]](/help/reporting/dimensions/content-channel.md) | |
| [[!UICONTROL 콘텐츠 세그먼트]](/help/reporting/dimensions/content-segment.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.videoSegment` | `xdm.mediaReporting.`<br>`sessionDetails.segment` | 차원 | [[!UICONTROL 콘텐츠 세그먼트]](/help/reporting/dimensions/content-segment.md) | |
| [[!UICONTROL 컨텐츠 이름]](/help/reporting/dimensions/content-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._dc.title` | `xdm.mediaReporting.`<br>`sessionDetails.friendlyName` | 차원 | [[!UICONTROL 컨텐츠 이름]](/help/reporting/dimensions/content-name.md) | |
| 비디오 경로 | *AEP/CJA에서 사용되지 않음* | | | | Adobe Analytics 관련 속성 |
| [[!UICONTROL 표시]](/help/reporting/dimensions/show.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.show` | 차원 | [[!UICONTROL 표시]](/help/reporting/dimensions/show.md) | |
| [[!UICONTROL 시즌]](/help/reporting/dimensions/season.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.season` | 차원 | [[!UICONTROL 시즌]](/help/reporting/dimensions/season.md) | |
| [[!UICONTROL 에피소드]](/help/reporting/dimensions/episode.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.episode` | 차원 | [[!UICONTROL 에피소드]](/help/reporting/dimensions/episode.md) | |
| [[!UICONTROL 장르]](/help/reporting/dimensions/genre.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Genre` | `xdm.mediaReporting.`<br>`sessionDetails.genreList` | 차원 | 지원되지 않음 | `mediaReporting` 필드 사용 |
| [[!UICONTROL 네트워크]](/help/reporting/dimensions/network.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastNetwork` | `xdm.mediaReporting.`<br>`sessionDetails.network` | 차원 | [[!UICONTROL 네트워크]](/help/reporting/dimensions/network.md) | |
| [[!UICONTROL 표시 형식]](/help/reporting/dimensions/show-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.showType` | `xdm.mediaReporting.`<br>`sessionDetails.showType` | 차원 | [[!UICONTROL 표시 형식]](/help/reporting/dimensions/show-type.md) | |
| [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | `xdm.media.mediaTimed.`<br>`idp` | `xdm.mediaReporting.`<br>`sessionDetails.mvpd` | 차원 | [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | |
| [[!UICONTROL 인증됨]](/help/reporting/metrics/authorized.md) | 지원되지 않음 | `xdm.mediaReporting.`<br>`sessionDetails.authorized` | 차원 | [[!UICONTROL 인증됨]](/help/reporting/metrics/authorized.md) | |
| [[!UICONTROL 일 파트]](/help/reporting/dimensions/day-part.md) | 지원되지 않음 | `xdm.mediaReporting.`<br>`sessionDetails.dayPart` | 차원 | [[!UICONTROL 일 파트]](/help/reporting/dimensions/day-part.md) | |
| [[!UICONTROL 미디어 피드 유형]](/help/reporting/dimensions/media-feed-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sourceFeed` | `xdm.mediaReporting.`<br>`sessionDetails.feed` | 차원 | [[!UICONTROL 미디어 피드 유형]](/help/reporting/dimensions/media-feed-type.md) | |
| [[!UICONTROL 아티스트]](/help/reporting/dimensions/artist.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.artist` | `xdm.mediaReporting.`<br>`sessionDetails.artist` | 차원 | [[!UICONTROL 아티스트]](/help/reporting/dimensions/artist.md) | |
| [[!UICONTROL 앨범]](/help/reporting/dimensions/album.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.album` | `xdm.mediaReporting.`<br>`sessionDetails.album` | 차원 | [[!UICONTROL 앨범]](/help/reporting/dimensions/album.md) | |
| [[!UICONTROL 레이블]](/help/reporting/dimensions/label.md) | 지원되지 않음 | `xdm.mediaReporting.`<br>`sessionDetails.label` | 차원 | [[!UICONTROL 레이블]](/help/reporting/dimensions/label.md) | |
| [[!UICONTROL 작성자]](/help/reporting/dimensions/author.md) | 지원되지 않음 | `xdm.mediaReporting.`<br>`sessionDetails.author` | 차원 | [[!UICONTROL 작성자]](/help/reporting/dimensions/author.md) | |
| [[!UICONTROL 스테이션]](/help/reporting/dimensions/station.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TRSN` | `xdm.mediaReporting.`<br>`sessionDetails.station` | 차원 | [[!UICONTROL 스테이션]](/help/reporting/dimensions/station.md) | |
| [[!UICONTROL 게시자]](/help/reporting/dimensions/publisher.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TPUB` | `xdm.mediaReporting.`<br>`sessionDetails.publisher` | 차원 | [[!UICONTROL 게시자]](/help/reporting/dimensions/publisher.md) | |
| [[!UICONTROL 미디어 시작]](/help/reporting/metrics/media-starts.md) | `xdm.media.mediaTimed.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`sessionDetails.isViewed` | 지표 | [[!UICONTROL 미디어 시작]](/help/reporting/metrics/media-starts.md) | |
| [[!UICONTROL 콘텐츠 시작]](/help/reporting/metrics/content-starts.md) | `xdm.media.mediaTimed.`<br>`starts.value` | `xdm.mediaReporting.`<br>`sessionDetails.isPlayed` | 지표 | [[!UICONTROL 콘텐츠 시작]](/help/reporting/metrics/content-starts.md) | |
| [[!UICONTROL 컨텐츠 완료]](/help/reporting/metrics/content-completes.md) | `xdm.media.mediaTimed.`<br>`completes.value` | `xdm.mediaReporting.`<br>`sessionDetails.isCompleted` | 지표 | [[!UICONTROL 컨텐츠 완료]](/help/reporting/metrics/content-completes.md) | |
| [[!UICONTROL 콘텐츠 체류 시간]](/help/reporting/metrics/content-time-spent.md) | `xdm.media.mediaTimed.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.timePlayed` | 지표 | [[!UICONTROL 콘텐츠 체류 시간]](/help/reporting/metrics/content-time-spent.md) | |
| [[!UICONTROL 미디어 사용 시간]](/help/reporting/metrics/media-time-spent.md) | `xdm.media.mediaTimed.`<br>`totalTimePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.totalTimePlayed` | 지표 | [[!UICONTROL 미디어 사용 시간]](/help/reporting/metrics/media-time-spent.md) | |
| [[!UICONTROL 고유 재생 시간]](/help/reporting/metrics/unique-time-played.md) | 지원되지 않음 | `xdm.mediaReporting.`<br>`sessionDetails.uniqueTimePlayed` | 지표 | [[!UICONTROL 고유 재생 시간]](/help/reporting/metrics/unique-time-played.md) | |
| [[!UICONTROL 10% 진행률 마커]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress10.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress10` | 지표 | [[!UICONTROL 10% 진행률 마커]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 25% 진행률 마커]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress25.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress25` | 지표 | [[!UICONTROL 25% 진행률 마커]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 50% 진행률 마커]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress50.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress50` | 지표 | [[!UICONTROL 50% 진행률 마커]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 75% 진행률 마커]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress75.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress75` | 지표 | [[!UICONTROL 75% 진행률 마커]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 95% 진행률 마커]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress95.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress95` | 지표 | [[!UICONTROL 95% 진행률 마커]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 평균 분당 시청 대상자]](/help/reporting/metrics/average-minute-audience.md) | 지원되지 않음 | `xdm.mediaReporting.`<br>`sessionDetails.averageMinuteAudience` | 지표 | [[!UICONTROL 평균 분당 시청 대상자]](/help/reporting/metrics/average-minute-audience.md) | |
| 마지막 통화 이후 지난 시간 (초) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sessionTimeout` | `xdm.mediaReporting.`<br>`sessionDetails.secondsSinceLastCall` | 지표 | 마지막 통화 이후 지난 시간 (초) | |
| [[!UICONTROL 일시 중지된 영향을 받은 스트림]](/help/reporting/metrics/paused-impacted-streams.md) | 지원되지 않음 | `xdm.mediaReporting.`<br>`sessionDetails.hasPauseImpactedStreams` | 지표 | [[!UICONTROL 일시 중지된 영향을 받은 스트림]](/help/reporting/metrics/paused-impacted-streams.md) | 다른 이벤트에서 이 값을 계산하여 mediaTimed를 다룹니다 |
| [[!UICONTROL 이벤트 일시 중지]](/help/reporting/metrics/pause-events.md) | `xdm.media.mediaTimed.`<br>`pauses.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseCount` | 지표 | [[!UICONTROL 이벤트 일시 중지]](/help/reporting/metrics/pause-events.md) | |
| [[!UICONTROL 총 일시 중단 기간]](/help/reporting/metrics/total-pause-duration.md) | `xdm.media.mediaTimed.`<br>`pauseTime.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseTime` | 지표 | [[!UICONTROL 총 일시 중단 기간]](/help/reporting/metrics/total-pause-duration.md) | |
| [[!UICONTROL 콘텐츠 다시 시작]](/help/reporting/metrics/content-resumes.md) | `xdm.media.mediaTimed.`<br>`resumes.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasResume` | 지표 | [[!UICONTROL 콘텐츠 다시 시작]](/help/reporting/metrics/content-resumes.md) | |
| [[!UICONTROL 콘텐츠 세그먼트 보기]](/help/reporting/metrics/content-segment-views.md) | `xdm.media.mediaTimed.`<br>`mediaSegmentViews.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasSegmentView` | 지표 | [[!UICONTROL 콘텐츠 세그먼트 보기]](/help/reporting/metrics/content-segment-views.md) | |

## 플레이어 상태 매개 변수 업데이트

| 필드 이름 | 이전 XDM 필드 | 보고 XDM 필드 패스 | 데이터 유형 | 파생 필드 | 참고 |
| --- | --- | --- | --- | --- | --- |
| 플레이어 상태의 영향을 받는 스트림 | 지원되지 않음 | `xdm.mediaReporting.`<br>`states.isSet` | 지표 | 지원되지 않음 | `mediaReporting` 필드 사용 |
| 플레이어 상태 카운트 | 지원되지 않음 | `xdm.mediaReporting.`<br>`states.count` | 지표 | 지원되지 않음 | `mediaReporting` 필드 사용 |
| 플레이어 상태 총 기간 | 지원되지 않음 | `xdm.mediaReporting.`<br>`states.time` | 지표 | 지원되지 않음 | `mediaReporting` 필드 사용 |
| 플레이어 상태 이름 | 지원되지 않음 | `xdm.mediaReporting.`<br>`states.name` | 차원 | 지원되지 않음 | `mediaReporting` 필드 사용 |

## 챕터 매개변수

| 필드 이름 | 이전 XDM 필드 | 보고 XDM 필드 패스 | 데이터 유형 | 파생 필드 | 참고 |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL 챕터]](/help/reporting/dimensions/chapter.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.chapterAssetReference._id` | `xdm.mediaReporting.`<br>`chapterDetails.ID` | 차원 | [[!UICONTROL 챕터]](/help/reporting/dimensions/chapter.md) | |
| [[!UICONTROL 챕터 시작]](/help/reporting/metrics/chapter-starts.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.impressions.value` | `xdm.mediaReporting.`<br>`chapterDetails.isStarted` | 지표 | [[!UICONTROL 챕터 시작]](/help/reporting/metrics/chapter-starts.md) | |
| [[!UICONTROL 챕터 완료]](/help/reporting/metrics/chapter-completes.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.completes.value` | `xdm.mediaReporting.`<br>`chapterDetails.isCompleted` | 지표 | [[!UICONTROL 챕터 완료]](/help/reporting/metrics/chapter-completes.md) | |
| [[!UICONTROL 챕터 체류 시간]](/help/reporting/metrics/chapter-time-spent.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.timePlayed.value` | `xdm.mediaReporting.`<br>`chapterDetails.timePlayed` | 지표 | [[!UICONTROL 챕터 체류 시간]](/help/reporting/metrics/chapter-time-spent.md) | |

## 광고 매개변수

| 필드 이름 | 이전 XDM 필드 | 보고 XDM 필드 패스 | 데이터 유형 | 파생 필드 | 참고 |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL 광고 ID]](/help/reporting/dimensions/ad.md) | `xdm.advertising.`<br>`adAssetReference._id` | `xdm.mediaReporting.`<br>`advertisingDetails.name` | 차원 | [[!UICONTROL 광고 ID]](/help/reporting/dimensions/ad.md) | |
| [[!UICONTROL Pod의 광고 위치]](/help/reporting/dimensions/ad-in-pod-position.md) | `xdm.advertising.`<br>`adAssetViewDetails.index` | `xdm.mediaReporting.`<br>`advertisingDetails.podPosition` | 차원 | [[!UICONTROL Pod의 광고 위치]](/help/reporting/dimensions/ad-in-pod-position.md) | |
| [[!UICONTROL 광고 길이]](/help/reporting/dimensions/ad-length.md) | `xdm.advertising.`<br>`adAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`advertisingDetails.length` | 지표 | [[!UICONTROL 광고 길이]](/help/reporting/dimensions/ad-length.md) | |
| [[!UICONTROL 광고 플레이어 이름]](/help/reporting/dimensions/ad-player-name.md) | `xdm.advertising.`<br>`adAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`advertisingDetails.playerName` | 차원 | [[!UICONTROL 광고 플레이어 이름]](/help/reporting/dimensions/ad-player-name.md) | |
| [[!UICONTROL 광고 브레이크 ID]](/help/reporting/dimensions/ad-pod.md) | `xdm.advertising.`<br>`adAssetViewDetails.adBreak._id` | `xdm.mediaReporting.`<br>`advertisingPodDetails.ID` | 차원 | [[!UICONTROL 광고 브레이크 ID]](/help/reporting/dimensions/ad-pod.md) | |
| [[!UICONTROL 광고 이름]](/help/reporting/dimensions/ad-name.md) | `xdm.advertising.`<br>`adAssetReference._dc.title` | `xdm.mediaReporting.`<br>`advertisingDetails.friendlyName` | 차원 | [[!UICONTROL 광고 이름]](/help/reporting/dimensions/ad-name.md) | |
| [[!UICONTROL 광고주]](/help/reporting/dimensions/advertiser.md) | `xdm.advertising.`<br>`adAssetReference.advertiser` | `xdm.mediaReporting.`<br>`advertisingDetails.advertiser` | 차원 | [[!UICONTROL 광고주]](/help/reporting/dimensions/advertiser.md) | |
| [[!UICONTROL 캠페인 ID]](/help/reporting/dimensions/campaign-id.md) | `xdm.advertising.`<br>`adAssetReference.campaign` | `xdm.mediaReporting.`<br>`advertisingDetails.campaignID` | 차원 | [[!UICONTROL 캠페인 ID]](/help/reporting/dimensions/campaign-id.md) | |
| [[!UICONTROL 광고 시작]](/help/reporting/metrics/ad-starts.md) | `xdm.advertising.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isStarted` | 지표 | [[!UICONTROL 광고 시작]](/help/reporting/metrics/ad-starts.md) | |
| [[!UICONTROL 광고 완료]](/help/reporting/metrics/ad-completes.md) | `xdm.advertising.`<br>`completes.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isCompleted` | 지표 | [[!UICONTROL 광고 완료]](/help/reporting/metrics/ad-completes.md) | |
| [[!UICONTROL 광고 체류 시간]](/help/reporting/metrics/ad-time-spent.md) | `xdm.advertising.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`advertisingDetails.timePlayed` | 지표 | [[!UICONTROL 광고 체류 시간]](/help/reporting/metrics/ad-time-spent.md) | |

## 품질 매개변수

| 필드 이름 | 이전 XDM 필드 | 보고 XDM 필드 패스 | 데이터 유형 | 파생 필드 | 참고 |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL 평균 비트율]](/help/reporting/metrics/average-bitrate.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateAverage.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateAverage` | 모두 | [[!UICONTROL 평균 비트율]](/help/reporting/metrics/average-bitrate.md) | |
| [[!UICONTROL 시작 시간]](/help/reporting/metrics/time-to-start.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.timeToStart.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.timeToStart` | 모두 | [[!UICONTROL 시작 시간]](/help/reporting/metrics/time-to-start.md) | |
| [[!UICONTROL 삭제된 프레임]](/help/reporting/metrics/dropped-frames.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.droppedFrames.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.droppedFrames` | 모두 | [[!UICONTROL 삭제된 프레임]](/help/reporting/metrics/dropped-frames.md) | |
| [[!UICONTROL 버퍼 이벤트]](/help/reporting/metrics/buffer-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.buffers.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferCount` | 모두 | [[!UICONTROL 버퍼 이벤트]](/help/reporting/metrics/buffer-events.md) | |
| [[!UICONTROL 총 버퍼 지속 시간]](/help/reporting/metrics/total-buffer-duration.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bufferTime.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferTime` | 모두 | [[!UICONTROL 총 버퍼 지속 시간]](/help/reporting/metrics/total-buffer-duration.md) | |
| [[!UICONTROL 비트율 변경]](/help/reporting/metrics/bitrate-changes.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateChanges.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateChangeCount` | 모두 | [[!UICONTROL 비트율 변경]](/help/reporting/metrics/bitrate-changes.md) | |
| [[!UICONTROL 오류/오류 이벤트]](/help/reporting/metrics/error-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.errors.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.errorCount` | 모두 | [[!UICONTROL 오류/오류 이벤트]](/help/reporting/metrics/error-events.md) | |
| [[!UICONTROL 플레이어 SDK 오류 ID]](/help/reporting/dimensions/player-sdk-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.playerSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.playerSdkErrors` | 차원 | 지원되지 않음 | `mediaReporting` 필드 사용 |
| [[!UICONTROL 외부 오류 ID]](/help/reporting/dimensions/external-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.externalSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.externalErrors` | 차원 | 지원되지 않음 | `mediaReporting` 필드 사용 |
| [[!UICONTROL 시작 전 드롭]](/help/reporting/metrics/drops-before-start.md) | `xdm.media.mediaTimed.`<br>`dropBeforeStarts.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.isDroppedBeforeStart` | 지표 | [[!UICONTROL 시작 전 드롭]](/help/reporting/metrics/drops-before-start.md) | |
| [[!UICONTROL 버퍼 영향을 받은 스트림]](/help/reporting/metrics/buffer-impacted-streams.md) | 지원되지 않음 | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBufferImpactedStreams` | 지표 | [[!UICONTROL 버퍼 영향을 받은 스트림]](/help/reporting/metrics/buffer-impacted-streams.md) | 다른 이벤트에서 계산됨 |
| [[!UICONTROL 비트율 변경의 영향을 받은 스트림]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | 지원되지 않음 | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBitrateChangeImpactedStreams` | 지표 | [[!UICONTROL 비트율 변경의 영향을 받은 스트림]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | 다른 이벤트에서 계산됨 |
| [[!UICONTROL 오류 영향을 받은 스트림]](/help/reporting/metrics/error-impacted-streams.md) | 지원되지 않음 | `xdm.mediaReporting.`<br>`qoeDataDetails.hasErrorImpactedStreams` | 지표 | [[!UICONTROL 오류 영향을 받은 스트림]](/help/reporting/metrics/error-impacted-streams.md) | 다른 이벤트에서 계산됨 |
| [[!UICONTROL 드롭된 프레임 영향을 받은 스트림]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | 지원되지 않음 | `xdm.mediaReporting.`<br>`qoeDataDetails.hasDroppedFrameImpactedStreams` | 지표 | [[!UICONTROL 드롭된 프레임 영향을 받은 스트림]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | 다른 이벤트에서 계산됨 |

## 미디어 분석 분류

Media Analytics 분류는 ACDC라고 하는 별도의 플로우를 통해 AEP에 수집됩니다. 아래 표에 나열된 각 분류 그룹은 AEP 내의 고유한 데이터 세트에 해당합니다. CJA에서 Media Analytics 이벤트 데이터 세트와 각 분류 데이터 세트 간에 연결을 설정해야 합니다.

### Customer Journey Analytics에서 데이터 세트 연결

Customer Journey Analytics에서 연결을 설정하려면 다음을 수행하십시오.

* **연결** 탭으로 이동하여 **새 연결 만들기**&#x200B;를 선택합니다.
* 연결 인터페이스에서 **데이터 세트 추가**&#x200B;를 선택하고 4개의 관련 분류 데이터 세트와 함께 Media Analytics 이벤트 데이터 세트(ADC를 통해 미디어 데이터를 가져오는 데 사용됨)를 찾습니다.

### 구성 세부 정보

각 조회 데이터 세트(분류 데이터 세트)에 대해 다음과 같이 구성합니다.

* **비디오 데이터 세트**:
   * 키: `_sandbox.key`
   * 일치하는 키: `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   * 데이터 원본 형식: `Web Data`

* **videoad 데이터 세트**:
   * 키: `_sandbox.key`
   * 일치하는 키: `Ad ID (advertising.adAssetReference._id)`
   * 데이터 원본 형식: `Web Data`

* **videoadpod 데이터 세트**:
   * 키: `_sandbox.key`
   * 일치하는 키: `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   * 데이터 원본 형식: `Web Data`

* **videochapter 데이터 집합**:
   * 키: `_sandbox.key`
   * 일치하는 키: `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   * 데이터 원본 형식: `Web Data`

### 보고 고려 사항

보고하는 동안 분류 데이터 세트로 작업할 때 표준 Media Analytics XDM 필드 대신 분류별 필드 경로(`ACDC XDM Path`)를 참조해야 합니다.

## 분류 테이블

| 분류 이름(그룹) | 필드 이름 | ACDC XDM 경로 |
| --- | --- | --- |
| video | 키/자산 ID | `xdm.<_sandbox>.key` |
| video | 비디오 길이 | `xdm.<_sandbox>.video_length` |
| video | 비디오 이름 | `xdm.<_sandbox>.video_name` |
| video | [[!UICONTROL 자산 ID]](/help/reporting/dimensions/asset-id.md) | `xdm.<_sandbox>.asset_id` |
| video | [[!UICONTROL 첫 방송 날짜]](/help/reporting/dimensions/first-air-date.md) | `xdm.<_sandbox>.first_air_date` |
| video | [[!UICONTROL 첫 번째 디지털 날짜]](/help/reporting/dimensions/first-digital-date.md) | `xdm.<_sandbox>.first_digital_date` |
| video | [[!UICONTROL 콘텐츠 등급]](/help/reporting/dimensions/content-rating.md) | `xdm.<_sandbox>.content_rating` |
| video | [[!UICONTROL 작성자]](/help/reporting/dimensions/originator.md) | `xdm.<_sandbox>.originator` |
| videoad | 키/광고 ID | `xdm.<_sandbox>.key` |
| videoad | [[!UICONTROL 광고 길이]](/help/reporting/dimensions/ad-length.md) | `xdm.<_sandbox>.ad_length` |
| videoad | [[!UICONTROL 광고 이름]](/help/reporting/dimensions/ad-name.md) | `xdm.<_sandbox>.ad_name` |
| videoad | [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md) | `xdm.<_sandbox>.creative_id` |
| videoadpod | 키/광고 Pod ID | `xdm.<_sandbox>.key` |
| videoadpod | [[!UICONTROL Pod 위치]](/help/reporting/dimensions/pod-position.md) | `xdm.<_sandbox>.pod_position` |
| videoadpod | [[!UICONTROL Pod 이름]](/help/reporting/dimensions/pod-name.md) | `xdm.<_sandbox>.pod_name` |
| videochapter | 키 / 챕터 | `xdm.<_sandbox>.key` |
| videochapter | [[!UICONTROL 챕터 길이]](/help/reporting/dimensions/chapter-length.md) | `xdm.<_sandbox>.chapter_length` |
| videochapter | [[!UICONTROL 챕터 오프셋]](/help/reporting/dimensions/chapter-offset.md) | `xdm.<_sandbox>.chapter_offset` |
| videochapter | [[!UICONTROL 챕터 위치]](/help/reporting/dimensions/chapter-position.md) | `xdm.<_sandbox>.chapter_position` |
| videochapter | [[!UICONTROL 챕터 이름]](/help/reporting/dimensions/chapter-name.md) | `xdm.<_sandbox>.chapter_name` |

## Media Analytics 사용자 지정 변수

Adobe Analytics에서 사용자 지정 변수는 각 보고서 세트 내에 정의된 구현 규칙에 따라 다른 이벤트 또는 eVar에 할당됩니다. 따라서 이러한 사용자 지정 변수를 Adobe Experience Platform(AEP)로 가져오면 다른 XDM 경로에 매핑됩니다.

* 이벤트는 다음 경로 아래에 저장됩니다.

  `_experience.analytics.event<x>to<y>.event<number>.value`

* eVar는 다음 경로 아래에 저장됩니다.

  `_experience.analytics.customDimensions.eVars.eVar<number>`

두 경우 모두 `<number>`은(는) 원래 Adobe Analytics 보고서 세트 구성에 사용된 특정 이벤트 또는 eVar 번호에 해당합니다.

### 사용자 지정 변수

| 필드 이름 | XDM 경로 | 데이터 유형 |
| --- | --- | --- |
| [[!UICONTROL 미디어 다운로드 플래그]](/help/reporting/dimensions/media-downloaded-flag.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 지표 |
| SDK 버전 | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 차원 |
| 미디어 라이브러리 버전 | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 차원 |
| [[!UICONTROL 스트림 형식]](/help/reporting/dimensions/stream-format.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 차원 |
| [[!UICONTROL 첫 방송 날짜]](/help/reporting/dimensions/first-air-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 차원 |
| [[!UICONTROL 첫 번째 디지털 날짜]](/help/reporting/dimensions/first-digital-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 차원 |
| [[!UICONTROL 페더레이션 데이터]](/help/reporting/metrics/federated-data.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>및<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 모두 |
| [[!UICONTROL 예상 스트림]](/help/reporting/metrics/estimated-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 지표 |
| [[!UICONTROL 광고 수]](/help/reporting/metrics/ad-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 지표 |
| [[!UICONTROL 챕터 수]](/help/reporting/metrics/chapter-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 지표 |
| [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 차원 |
| [[!UICONTROL 사이트 ID]](/help/reporting/dimensions/site-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 차원 |
| [[!UICONTROL Creative URL]](/help/reporting/dimensions/creative-url.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 차원 |
| [[!UICONTROL 배치 ID]](/help/reporting/dimensions/placement-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 차원 |
| 초당 프레임 | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>및<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 모두 |
| Media SDK 오류 ID | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 지표 |
| [[!UICONTROL 영향을 받는 스트림 중단]](/help/reporting/metrics/stall-impacted-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 지표 |
| [[!UICONTROL 중단 이벤트]](/help/reporting/metrics/stall-events.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 지표 |
| [[!UICONTROL 총 중단 기간]](/help/reporting/metrics/total-stalling-duration.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 지표 |
