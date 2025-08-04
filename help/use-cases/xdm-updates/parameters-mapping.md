---
title: 스트리밍 미디어용 새 Adobe Analytics 데이터 유형으로 대상자 마이그레이션
description: 스트리밍 미디어용 새로운 Adobe Analytics 데이터 유형으로 대상자를 마이그레이션하는 방법을 알아봅니다
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 3056a384535b3f5f2a9bc2d950bd5ee3410ec0a5
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 44%

---

# Adobe Experience Platform 및 Customer Journey Analytics에 대한 Media Analytics 매개 변수 매핑

이 문서에서는 Adobe Experience Platform 및 Customer Journey Analytics 내에서 사용되는 모든 Media Analytics 매개 변수의 포괄적인 목록을 제공합니다. 각 매개 변수를 해당 XDM 필드 경로에 매핑하여 [Analytics Source 커넥터](https://experienceleague.adobe.com/ko/docs/experience-platform/sources/connectors/adobe-applications/analytics) 또는 [분류용 Analytics Source 커넥터](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/classifications)를 통해 Adobe Analytics에서 플랫폼으로 가져온 데이터의 통합을 지원하기 위한 것입니다.

## Media Analytics 예약 변수

모든 Media Analytics 예약 변수의 경우 2025년 5월까지(포함) Adobe Analytics에서 AEP으로 수집된 데이터는 아래 표에 나온 &#39;현재 XDM 필드 패스&#39;에서 찾을 수 있습니다.

현재 Media Analytics 및 ADC 팀이 &#39;보고 XDM 필드 패스&#39;로의 전체 마이그레이션을 위해 작업하고 있으므로, 이 마이그레이션이 완료되고 &#39;보고 XDM 필드 패스&#39;를 사용할 수 있게 되면 공식 통신이 공유됩니다.

## 스트리밍 미디어 매개 변수

| 필드 이름 | 현재 XDM 필드 패스(더 이상 사용되지 않음) | 보고 XDM 필드 패스 | 데이터 유형 | 파생 필드 | 참고 |
|--------------------|---------------------------------------------------------------------------|---------------------------------------------------|-----------|-------------------|-----------------------------------------------------------------------|
| 스트림 유형 | media.mediaTimed.primaryAssetReference.streamType | mediaReporting.sessionDetails.streamType | 차원 | 스트림 유형 |                                                                       |
| 콘텐츠 ID | media.mediaTimed.primaryAssetReference._ID | mediaReporting.sessionDetails.name | 차원 | 콘텐츠 ID |                                                                       |
| 콘텐츠 길이 | media.mediaTimed.primaryAssetReference._xmpDM.duration | mediaReporting.sessionDetails.length | 차원 | 콘텐츠 길이 |                                                                       |
| 콘텐츠 유형 | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | mediaReporting.sessionDetails.contentType | 차원 | 콘텐츠 유형 |                                                                       |
| 미디어 세션 ID | media.mediaTimed.primaryAssetViewDetails._ID | mediaReporting.sessionDetails.ID | 차원 | 미디어 세션 ID |                                                                       |
| 콘텐츠 플레이어 이름 | media.mediaTimed.primaryAssetViewDetails.playerName | mediaReporting.sessionDetails.playerName | 차원 | 콘텐츠 플레이어 이름 |                                                                       |
| 콘텐츠 채널 | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | mediaReporting.sessionDetails.channel | 차원 | 콘텐츠 채널 |                                                                       |
| 콘텐츠 세그먼트 | media.mediaTimed.primaryAssetViewDetails.videoSegment | mediaReporting.sessionDetails.segment | 차원 | 콘텐츠 세그먼트 |                                                                       |
| 컨텐츠 이름 | media.mediaTimed.primaryAssetReference._dc.title | mediaReporting.sessionDetails.friendlyName | 차원 | 컨텐츠 이름 |                                                                       |
| 비디오 경로 | *AEP/CJA에서 사용되지 않음* |                                                   |           |                   | Adobe Analytics 관련 속성 |
| 표시 | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | mediaReporting.sessionDetails.show | 차원 | 표시 |                                                                       |
| 시즌 | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | mediaReporting.sessionDetails.season | 차원 | 시즌 |                                                                       |
| 에피소드 | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | mediaReporting.sessionDetails.episode | 차원 | 에피소드 |                                                                       |
| 장르 | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | mediaReporting.sessionDetails.genreList | 차원 | 지원되지 않음 | MediaReporting 필드 사용 |
| 네트워크 | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | mediaReporting.sessionDetails.network | 차원 | 네트워크 |                                                                       |
| 표시 유형 | media.mediaTimed.primaryAssetReference.showType | mediaReporting.sessionDetails.showType | 차원 | 표시 유형 |                                                                       |
| MVPD | media.mediaTimed.idp | mediaReporting.sessionDetails.mvpd | 차원 | MVPD |                                                                       |
| 인증됨 | 지원되지 않음 | mediaReporting.sessionDetails.authorized | 차원 | 인증됨 |                                                                       |
| 방송 시간대 | 지원되지 않음 | mediaReporting.sessionDetails.dayPart | 차원 | 방송 시간대 |                                                                       |
| 미디어 피드 유형 | media.mediaTimed.primaryAssetViewDetails.sourceFeed | mediaReporting.sessionDetails.feed | 차원 | 미디어 피드 유형 |                                                                       |
| 아티스트 | media.mediaTimed.primaryAssetReference._xmpDM.artist | mediaReporting.sessionDetails.artist | 차원 | 아티스트 |                                                                       |
| 앨범 | media.mediaTimed.primaryAssetReference._xmpDM.album | mediaReporting.sessionDetails.album | 차원 | 앨범 |                                                                       |
| 레이블 | 지원되지 않음 | mediaReporting.sessionDetails.label | 차원 | 레이블 |                                                                       |
| 작성자 | 지원되지 않음 | mediaReporting.sessionDetails.author | 차원 | 작성자 |                                                                       |
| 방송국 | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TRSN | mediaReporting.sessionDetails.station | 차원 | 방송국 |                                                                       |
| 게시자 | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TPUB | mediaReporting.sessionDetails.publisher | 차원 | 게시자 |                                                                       |
| 미디어 시작 | media.mediaTimed.impressions.value | mediaReporting.sessionDetails.isViewed | 지표 | 미디어 시작 |                                                                       |
| 콘텐츠 시작 | media.mediaTimed.starts.value | mediaReporting.sessionDetails.isPlayed | 지표 | 콘텐츠 시작 |                                                                       |
| 콘텐츠 완료 | media.mediaTimed.completes.value | mediaReporting.sessionDetails.isCompleted | 지표 | 콘텐츠 완료 |                                                                       |
| 콘텐츠 체류 시간 | media.mediaTimed.timePlayed.value | mediaReporting.sessionDetails.timePlayed | 지표 | 콘텐츠 체류 시간 |                                                                       |
| 미디어 사용 시간 | media.mediaTimed.totalTimePlayed.value | mediaReporting.sessionDetails.totalTimePlayed | 지표 | 미디어 사용 시간 |                                                                       |
| 재생된 고유 시간 | 지원되지 않음 | mediaReporting.sessionDetails.uniqueTimePlayed | 지표 | 재생된 고유 시간 |                                                                       |
| 10% 진행률 마커 | media.mediaTimed.progress10.value | mediaReporting.sessionDetails.hasProgress10 | 지표 | 10% 진행률 마커 |                                                                       |
| 25% 진행률 마커 | media.mediaTimed.progress25.value | mediaReporting.sessionDetails.hasProgress25 | 지표 | 25% 진행률 마커 |                                                                       |
| 50% 진행률 마커 | media.mediaTimed.progress50.value | mediaReporting.sessionDetails.hasProgress50 | 지표 | 50% 진행률 마커 |                                                                       |
| 75% 진행률 마커 | media.mediaTimed.progress75.value | mediaReporting.sessionDetails.hasProgress75 | 지표 | 75% 진행률 마커 |                                                                       |
| 95% 진행률 마커 | media.mediaTimed.progress95.value | mediaReporting.sessionDetails.hasProgress95 | 지표 | 95% 진행률 마커 |                                                                       |
| 대상자 분당 평균 시청 시간 | 지원되지 않음 | mediaReporting.sessionDetails.averageMinuteAudience | 지표 | 대상자 분당 평균 시청 시간 |                                                                  |
| 마지막 통화 이후 지난 시간 (초) | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | mediaReporting.sessionDetails.secondsSinceLastCall | 지표 | 마지막 통화 이후 지난 시간 (초) |                                                              |
| 일시 중지된 영향을 받은 스트림 | 지원되지 않음 | mediaReporting.sessionDetails.hasPauseImpactedStreams | 지표 | 일시 중지된 영향을 받은 스트림 | 다른 이벤트에서 이 값을 계산하여 mediaTimed를 다룹니다 |
| 일시 중지 이벤트 | media.mediaTimed.pauses.value | mediaReporting.sessionDetails.pauseCount | 지표 | 일시 중지 이벤트 |                                                                       |
| 총 일시 중지 기간 | media.mediaTimed.pauseTime.value | mediaReporting.sessionDetails.pauseTime | 지표 | 총 일시 중지 기간 |                                                                       |
| 콘텐츠 다시 시작 | media.mediaTimed.resumes.value | mediaReporting.sessionDetails.hasResume | 지표 | 콘텐츠 다시 시작 |                                                                       |
| 콘텐츠 세그먼트 보기 수 | media.mediaTimed.mediaSegmentViews.value | mediaReporting.sessionDetails.hasSegmentView | 지표 | 콘텐츠 세그먼트 보기 수 |                                                                     |

{style="table-layout:auto"}

## 플레이어 상태 매개 변수 업데이트

| 필드 이름 | 현재 XDM 필드 패스(더 이상 사용되지 않음) | 보고 XDM 필드 패스 | 데이터 유형 | 파생 필드 | 참고 |
|----------------------------|-------------------------------------|----------------------------------|-----------|----------------|--------------------------------------|
| 플레이어 상태의 영향을 받는 스트림 | 지원되지 않음 | mediaReporting.states.isSet | 지표 | 지원되지 않음 | mediaReporting 필드 사용 |
| 플레이어 상태 카운트 | 지원되지 않음 | mediaReporting.states.count | 지표 | 지원되지 않음 | mediaReporting 필드 사용 |
| 플레이어 상태 총 기간 | 지원되지 않음 | mediaReporting.states.time | 지표 | 지원되지 않음 | mediaReporting 필드 사용 |
| 플레이어 상태 이름 | 지원되지 않음 | mediaReporting.states.name | 차원 | 지원되지 않음 | mediaReporting 필드 사용 |

{style="table-layout:auto"}

## 챕터 매개변수

| 필드 이름 | 현재 XDM 필드 패스(더 이상 사용되지 않음) | 보고 XDM 필드 패스 | 데이터 유형 | 파생 필드 | 참고 |
|------------------|--------------------------------------------------------------|-------------------------------------------|-----------|----------------|-----------|
| 챕터 | media.mediaTimed.mediaChapter.chapterAssetReference._ID | mediaReporting.chapterDetails.ID | 차원 | 챕터 |           |
| 챕터 시작 | media.mediaTimed.mediaChapter.impressions.value | mediaReporting.chapterDetails.isStarted | 지표 | 챕터 시작 |           |
| 챕터 완료 | media.mediaTimed.mediaChapter.completes.value | mediaReporting.chapterDetails.isCompleted | 지표 | 챕터 완료 |          |
| 챕터 체류 시간 | media.mediaTimed.mediaChapter.timePlayed.value | mediaReporting.chapterDetails.timePlayed | 지표 | 챕터 체류 시간 |        |

{style="table-layout:auto"}

## 광고 매개변수

| 필드 이름 | 현재 XDM 필드 패스(더 이상 사용되지 않음) | 보고 XDM 필드 패스 | 데이터 유형 | 파생 필드 | 참고 |
|------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| 광고 ID | advertising.adAssetReference._ID | mediaReporting.advertisingDetails.name | 차원 | 광고 ID |           |
| Pod의 광고 위치 | advertising.adAssetViewDetails.index | mediaReporting.advertisingDetails.podPosition | 차원 | Pod의 광고 위치 |     |
| 광고 길이 | advertising.adAssetReference._xmpDM.duration | mediaReporting.advertisingDetails.length | 지표 | 광고 길이 |           |
| 광고 플레이어 이름 | advertising.adAssetViewDetails.playerName | mediaReporting.advertisingDetails.playerName | 차원 | 광고 플레이어 이름 |           |
| 광고 브레이크 ID | advertising.adAssetViewDetails.adBreak._ID | mediaReporting.advertisingPodDetails.ID | 차원 | 광고 브레이크 ID |           |
| 광고 이름 | advertising.adAssetReference._dc.title | mediaReporting.advertisingDetails.friendlyName | 차원 | 광고 이름 |           |
| 광고주 | advertising.adAssetReference.advertiser | mediaReporting.advertisingDetails.advertiser | 차원 | 광고주 |           |
| 캠페인 ID | advertising.adAssetReference.campaign | mediaReporting.advertisingDetails.campaignID | 차원 | 캠페인 ID |           |
| 광고 시작 | advertising.impressions.value | mediaReporting.advertisingDetails.isStarted | 지표 | 광고 시작 |           |
| 광고 완료 | advertising.completes.value | mediaReporting.advertisingDetails.isCompleted | 지표 | 광고 완료 |           |
| 광고 체류 시간 | advertising.timePlayed.value | mediaReporting.advertisingDetails.timePlayed | 지표 | 광고 체류 시간 |           |

{style="table-layout:auto"}

## 품질 매개변수

| 필드 이름 | 현재 XDM 필드 패스(더 이상 사용되지 않음) | 보고 XDM 필드 패스 | 데이터 유형 | 파생 필드 | 참고 |
|------------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| 평균 비트율 | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage.value | mediaReporting.qoeDataDetails.bitrateAverage | 변수 | 평균 비트율 |           |
| 시작 시간 | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value | mediaReporting.qoeDataDetails.timeToStart | 변수 | 시작 시간 |           |
| 드롭된 프레임 | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value | mediaReporting.qoeDataDetails.droppedFrames | 변수 | 드롭된 프레임 |           |
| 버퍼 이벤트 | media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value | mediaReporting.qoeDataDetails.bufferCount | 변수 | 버퍼 이벤트 |           |
| 총 버퍼 지속 시간 | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value | mediaReporting.qoeDataDetails.bufferTime | 변수 | 총 버퍼 지속 시간 |     |
| 비트율 변경 | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value | mediaReporting.qoeDataDetails.bitrateChangeCount | 변수 | 비트율 변경 |         |
| 오류 이벤트 | media.mediaTimed.primaryAssetViewDetails.qoe.errors.value | mediaReporting.qoeDataDetails.errorCount | 변수 | 오류 이벤트 |  |
| 플레이어 SDK 오류 ID | media.mediaTimed.primaryAssetViewDetails.qoe.playerSdkErrors | mediaReporting.qoeDataDetails.playerSdkErrors | 차원 | 지원되지 않음 | mediaReporting 필드 사용 |
| 외부 오류 ID | media.mediaTimed.primaryAssetViewDetails.qoe.externalSdkErrors | mediaReporting.qoeDataDetails.externalErrors | 차원 | 지원되지 않음 | mediaReporting 필드 사용 |
| 시작 전 드롭 | media.mediaTimed.dropBeforeStarts.value | mediaReporting.qoeDataDetails.isDroppedBeforeStart | 지표 | 시작 전 드롭 |     |
| 버퍼 영향을 받은 스트림 | 지원되지 않음 | mediaReporting.qoeDataDetails.hasBufferImpactedStreams | 지표 | 버퍼 영향을 받은 스트림 | 다른 이벤트에서 계산됨 |
| 비트율 변경의 영향을 받은 스트림 | 지원되지 않음 | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams | 지표 | 비트율 변경의 영향을 받은 스트림 | 다른 이벤트에서 계산됨 |
| 오류 영향을 받은 스트림 | 지원되지 않음 | mediaReporting.qoeDataDetails.hasErrorImpactedStreams | 지표 | 오류 영향을 받은 스트림 | 다른 이벤트에서 계산됨 |
| 드롭된 프레임 영향을 받은 스트림 | 지원되지 않음 | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams | 지표 | 드롭된 프레임 영향을 받은 스트림 | 다른 이벤트에서 계산됨 |

{style="table-layout:auto"}

## 미디어 분석 분류

Media Analytics 분류는 ACDC라고 하는 별도의 플로우를 통해 AEP에 수집됩니다. 아래 표에 나열된 각 분류 그룹은 AEP 내의 고유한 데이터 세트에 해당합니다. CJA에서 Media Analytics 이벤트 데이터 세트와 각 분류 데이터 세트 간에 연결을 설정해야 합니다.

### Customer Journey Analytics에서 데이터 세트 연결

Customer Journey Analytics에서 연결을 설정하려면 다음을 수행하십시오.

- **연결** 탭으로 이동하여 **새 연결 만들기**&#x200B;를 선택합니다.
- 연결 인터페이스에서 **데이터 세트 추가**&#x200B;를 선택하고 4개의 관련 분류 데이터 세트와 함께 Media Analytics 이벤트 데이터 세트(ADC를 통해 미디어 데이터를 가져오는 데 사용됨)를 찾습니다.

### 구성 세부 정보

각 조회 데이터 세트(분류 데이터 세트)에 대해 다음과 같이 구성합니다.

- **비디오 데이터 세트**:
   - 키: `_sandbox.key`
   - 일치하는 키: `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   - 데이터 원본 형식: `Web Data`

- **videoad 데이터 세트**:
   - 키: `_sandbox.key`
   - 일치하는 키: `Ad ID (advertising.adAssetReference._id)`
   - 데이터 원본 형식: `Web Data`

- **videoadpod 데이터 세트**:
   - 키: `_sandbox.key`
   - 일치하는 키: `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   - 데이터 원본 형식: `Web Data`

- **videochapter 데이터 집합**:
   - 키: `_sandbox.key`
   - 일치하는 키: `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   - 데이터 원본 형식: `Web Data`

### 보고 고려 사항

보고하는 동안 분류 데이터 세트로 작업할 때 표준 Media Analytics XDM 필드 대신 분류별 필드 경로(`ACDC XDM Path`)를 참조해야 합니다.

## 분류 테이블

| 분류 이름(그룹) | 필드 이름 | ACDC XDM 경로 |
|------------|----------|-------------|
| video | 키/자산 ID | `<_sandbox>.key` |
| video | 비디오 길이 | `<_sandbox>.video_length` |
| video | 비디오 이름 | `<_sandbox>.video_name` |
| video | 자산 ID | `<_sandbox>.asset_id` |
| video | 최초 방송 날짜 | `<_sandbox>.first_air_date` |
| video | 최초 디지털 날짜 | `<_sandbox>.first_digital_date` |
| video | 콘텐츠 등급 | `<_sandbox>.content_rating` |
| video | 작성자 | `<_sandbox>.originator` |
| videoad | 키/광고 ID | `<_sandbox>.key` |
| videoad | 광고 길이 | `<_sandbox>.ad_length` |
| videoad | 광고 이름 | `<_sandbox>.ad_name` |
| videoad | 광고 ID | `<_sandbox>.creative_id` |
| videoadpod | 키/광고 Pod ID | `<_sandbox>.key` |
| videoadpod | Pod 위치 | `<_sandbox>.pod_position` |
| videoadpod | Pod 이름 | `<_sandbox>.pod_name` |
| videochapter | 키 / 챕터 | `<_sandbox>.key` |
| videochapter | 챕터 길이 | `<_sandbox>.chapter_length` |
| videochapter | 챕터 오프셋 | `<_sandbox>.chapter_offset` |
| videochapter | 챕터 위치 | `<_sandbox>.chapter_position` |
| videochapter | 챕터 이름 | `<_sandbox>.chapter_name` |

{style="table-layout:auto"}

## Media Analytics 사용자 지정 변수

Adobe Analytics에서 사용자 지정 변수는 각 보고서 세트 내에 정의된 구현 규칙에 따라 다른 이벤트 또는 eVar에 할당됩니다. 따라서 이러한 사용자 지정 변수를 Adobe Experience Platform(AEP)로 가져오면 다른 XDM 경로에 매핑됩니다.

- 이벤트는 다음 경로 아래에 저장됩니다.

  `_experience.analytics.event<x>to<y>.event<number>.value`

- eVar는 다음 경로 아래에 저장됩니다.

  `_experience.analytics.customDimensions.eVars.eVar<number>`

두 경우 모두 `<number>`은(는) 원래 Adobe Analytics 보고서 세트 구성에 사용된 특정 이벤트 또는 eVar 번호에 해당합니다.

### 사용자 지정 변수

| 필드 이름 | XDM 경로 | 데이터 유형 |
|-------------|-------------|-----------|
| 미디어에서 다운로드한 플래그 | `_experience.analytics.event<x>to<y>.event<number>.value` | 지표 |
| SDK 버전 | `_experience.analytics.customDimensions.eVars.eVar<number>` | 차원 |
| VHL 버전 | `_experience.analytics.customDimensions.eVars.eVar<number>` | 차원 |
| 스트림 형식 | `_experience.analytics.customDimensions.eVars.eVar<number>` | 차원 |
| 최초 방송 날짜 | `_experience.analytics.customDimensions.eVars.eVar<number>` | 차원 |
| 최초 디지털 날짜 | `_experience.analytics.customDimensions.eVars.eVar<number>` | 차원 |
| 페더레이션된 데이터 | `_experience.analytics.customDimensions.eVars.eVar<number>` 및 `_experience.analytics.event<x>to<y>.event<number>.value` | 변수 |
| 예상 스트림 | `_experience.analytics.event<x>to<y>.event<number>.value` | 지표 |
| 광고 수 | `_experience.analytics.event<x>to<y>.event<number>.value` | 지표 |
| 챕터 수 | `_experience.analytics.event<x>to<y>.event<number>.value` | 지표 |
| 광고 ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | 차원 |
| 사이트 ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | 차원 |
| 광고 URL | `_experience.analytics.customDimensions.eVars.eVar<number>` | 차원 |
| 게재위치 ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | 차원 |
| 초당 프레임 | `_experience.analytics.customDimensions.eVars.eVar<number>` 및 `_experience.analytics.event<x>to<y>.event<number>.value` | 변수 |
| Media SDK 오류 ID | `_experience.analytics.event<x>to<y>.event<number>.value` | 지표 |
| 지연 영향을 받은 스트림 | `_experience.analytics.event<x>to<y>.event<number>.value` | 지표 |
| 지연 이벤트 | `_experience.analytics.event<x>to<y>.event<number>.value` | 지표 |
| 총 지연 기간 | `_experience.analytics.event<x>to<y>.event<number>.value` | 지표 |

{style="table-layout:auto"}






