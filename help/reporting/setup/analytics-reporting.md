---
title: Analytics 전용 구현에 대한 보고 설정
description: 스트리밍 미디어 데이터를 수집 및 보고할 수 있도록 Adobe Analytics에서 미디어 보고서 세트 모듈을 활성화합니다.
feature: Streaming Media
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 8%

---

# Analytics 전용 구현에 대한 보고 설정

Analytics 전용 구현에서 스트리밍 미디어 데이터를 수집하려면 먼저 해당 데이터를 수신하는 각 보고서 세트가 적절한 미디어 모듈을 활성화하도록 구성되어야 합니다. 이 페이지에서는 이러한 모듈을 활성화하는 방법과 결과 보고서를 찾을 수 있는 위치를 설명합니다.

* **필수 구성 요소**: Adobe Analytics 구현입니다. [Analytics 전용 구현 개요](/help/implementation/analytics-only/overview.md) 및 선택한 구현 메서드를 참조하십시오.

## 보고서 세트에 대한 미디어 보고 활성화

미디어 데이터를 보내기 전에 미디어 지표를 수집하는 각 보고서 세트를 구성해야 합니다.

1. [Adobe Analytics](https://experience.adobe.com/analytics)에서 **[!UICONTROL 관리자]** → **[!UICONTROL 보고서 세트]**(으)로 이동합니다.
1. 미디어 데이터를 수집하는 보고서 세트를 선택합니다. **[!UICONTROL 설정 편집]** → **[!UICONTROL 미디어 관리]** → **[!UICONTROL 미디어 보고]**&#x200B;를 선택하십시오.

   ![보고서 세트 관리자 메뉴 스크린샷](assets/media-reporting.png)

1. **[!UICONTROL 미디어 보고]** 페이지에서 원하는 스트리밍 미디어 모듈을 사용하도록 설정합니다(아래 참조).

1. **[!UICONTROL 저장].** 선택

   이 보고서 세트가 이미 미디어 데이터를 수집하도록 구성된 경우 **[!UICONTROL 저장]**&#x200B;을 선택하면 추가 구성 페이지가 표시됩니다. **[!UICONTROL 미디어 코어 측정]** 페이지가 표시되면 다음 단계를 계속 진행합니다.

## 사용 가능한 스트리밍 미디어 모듈

미디어 측정에는 다음 모듈이 포함되어 있습니다.

* **[!UICONTROL 미디어 코어]**: 모든 스트리밍 미디어 추적에 필요합니다. 컨텐츠 재생 및 세션 데이터를 위한 솔루션 변수를 예약합니다.
   * **차원:**
      * [[!UICONTROL 콘텐츠]](/help/reporting/dimensions/content.md)
      * [[!UICONTROL 콘텐츠 채널]](/help/reporting/dimensions/content-channel.md)
      * [[!UICONTROL 콘텐츠 길이(변수)]](/help/reporting/dimensions/content-length.md)
      * [[!UICONTROL 콘텐츠 이름(변수)]](/help/reporting/dimensions/content-name.md)
      * [[!UICONTROL 콘텐츠 플레이어 이름]](/help/reporting/dimensions/content-player-name.md)
      * [[!UICONTROL 콘텐츠 세그먼트]](/help/reporting/dimensions/content-segment.md)
      * [[!UICONTROL 콘텐츠 형식]](/help/reporting/dimensions/content-type.md)
      * [[!UICONTROL 미디어 경로]](/help/reporting/dimensions/media-path.md)
      * [[!UICONTROL 미디어 세션 ID]](/help/reporting/dimensions/media-session-id.md)
      * [[!UICONTROL 스트림 형식]](/help/reporting/dimensions/stream-type.md)
   * **지표:**
      * [[!UICONTROL 평균 분당 시청 대상자]](/help/reporting/metrics/average-minute-audience.md)
      * [[!UICONTROL 컨텐츠 완료]](/help/reporting/metrics/content-completes.md)
      * [[!UICONTROL 콘텐츠 다시 시작]](/help/reporting/metrics/content-resumes.md)
      * [[!UICONTROL 콘텐츠 세그먼트 보기]](/help/reporting/metrics/content-segment-views.md)
      * [[!UICONTROL 콘텐츠 시작]](/help/reporting/metrics/content-starts.md)
      * [[!UICONTROL 콘텐츠 체류 시간]](/help/reporting/metrics/content-time-spent.md)
      * [[!UICONTROL 미디어 시작]](/help/reporting/metrics/media-starts.md)
      * [[!UICONTROL 이벤트 일시 중지]](/help/reporting/metrics/pause-events.md)
      * [[!UICONTROL 일시 중지된 영향을 받은 스트림]](/help/reporting/metrics/paused-impacted-streams.md)
      * [[!UICONTROL 진행률 마커]](/help/reporting/metrics/progress-markers.md)
      * [[!UICONTROL 총 일시 중단 기간]](/help/reporting/metrics/total-pause-duration.md)
      * [[!UICONTROL 재생된 고유 시간]](/help/reporting/metrics/unique-time-played.md)
* **[!UICONTROL 미디어 광고]**: 미디어 콘텐츠 내에서 광고를 추적할 수 있습니다.
   * **차원:**
      * [[!UICONTROL 광고]](/help/reporting/dimensions/ad.md)
      * [[!UICONTROL Pod 위치의 광고]](/help/reporting/dimensions/ad-in-pod-position.md)
      * [[!UICONTROL 광고 길이(변수)]](/help/reporting/dimensions/ad-length.md)
      * [[!UICONTROL 광고 이름(변수)]](/help/reporting/dimensions/ad-name.md)
      * [[!UICONTROL 광고 플레이어 이름]](/help/reporting/dimensions/ad-player-name.md)
      * [[!UICONTROL 광고 pod]](/help/reporting/dimensions/ad-pod.md)
      * [[!UICONTROL 광고주]](/help/reporting/dimensions/advertiser.md)
      * [[!UICONTROL 캠페인 ID]](/help/reporting/dimensions/campaign-id.md)
   * **분류 차원:**
      * [[!UICONTROL 자산 ID]](/help/reporting/dimensions/asset-id.md)
      * [[!UICONTROL 콘텐츠 등급]](/help/reporting/dimensions/content-rating.md)
      * [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md)
      * [[!UICONTROL 첫 방송 날짜]](/help/reporting/dimensions/first-air-date.md)
      * [[!UICONTROL 첫 번째 디지털 날짜]](/help/reporting/dimensions/first-digital-date.md)
      * [[!UICONTROL Pod 이름]](/help/reporting/dimensions/pod-name.md)
      * [[!UICONTROL Pod 위치]](/help/reporting/dimensions/pod-position.md)
   * **지표:**
      * [[!UICONTROL 광고 완료]](/help/reporting/metrics/ad-completes.md)
      * [[!UICONTROL 광고 시작]](/help/reporting/metrics/ad-starts.md)
      * [[!UICONTROL 광고 체류 시간]](/help/reporting/metrics/ad-time-spent.md)
      * [[!UICONTROL 미디어 체류 시간]](/help/reporting/metrics/media-time-spent.md)
* **[!UICONTROL 미디어 챕터]**: 미디어 콘텐츠 내에서 챕터를 추적할 수 있습니다.
   * **Dimension:**
      * [[!UICONTROL 챕터]](/help/reporting/dimensions/chapter.md)
   * **분류 차원:**
      * [[!UICONTROL 챕터 길이]](/help/reporting/dimensions/chapter-length.md)
      * [[!UICONTROL 챕터 이름]](/help/reporting/dimensions/chapter-name.md)
      * [[!UICONTROL 챕터 오프셋]](/help/reporting/dimensions/chapter-offset.md)
      * [[!UICONTROL 챕터 위치]](/help/reporting/dimensions/chapter-position.md)
      * [[!UICONTROL 작성자]](/help/reporting/dimensions/originator.md)
   * **지표:**
      * [[!UICONTROL 챕터 완료]](/help/reporting/metrics/chapter-completes.md)
      * [[!UICONTROL 챕터 시작]](/help/reporting/metrics/chapter-starts.md)
      * [[!UICONTROL 챕터 체류 시간]](/help/reporting/metrics/chapter-time-spent.md)
* **[!UICONTROL 미디어 품질]**: 버퍼링, 비트율 및 오류 이벤트를 포함한 재생 품질 데이터를 추적할 수 있습니다.
   * **차원:**
      * [[!UICONTROL 평균 비트율]](/help/reporting/dimensions/average-bitrate.md)
      * [[!UICONTROL 비트율 변경]](/help/reporting/dimensions/bitrate-changes.md)
      * [[!UICONTROL 버퍼 이벤트]](/help/reporting/dimensions/buffer-events.md)
      * [[!UICONTROL 삭제된 프레임]](/help/reporting/dimensions/dropped-frames.md)
      * [[!UICONTROL 오류]](/help/reporting/dimensions/errors.md)
      * [[!UICONTROL 외부 오류 ID]](/help/reporting/dimensions/external-error-ids.md)
      * [[!UICONTROL 플레이어 SDK 오류 ID]](/help/reporting/dimensions/player-sdk-error-ids.md)
      * [[!UICONTROL 시작 시간]](/help/reporting/dimensions/time-to-start.md)
      * [[!UICONTROL 총 버퍼 지속 시간]](/help/reporting/dimensions/total-buffer-duration.md)
   * **지표:**
      * [[!UICONTROL 평균 비트율]](/help/reporting/metrics/average-bitrate.md)
      * [[!UICONTROL 비트율 변경의 영향을 받은 스트림]](/help/reporting/metrics/bitrate-change-impacted-streams.md)
      * [[!UICONTROL 비트율 변경]](/help/reporting/metrics/bitrate-changes.md)
      * [[!UICONTROL 버퍼 이벤트]](/help/reporting/metrics/buffer-events.md)
      * [[!UICONTROL 버퍼 영향을 받은 스트림]](/help/reporting/metrics/buffer-impacted-streams.md)
      * [[!UICONTROL 드롭된 프레임 영향을 받은 스트림]](/help/reporting/metrics/dropped-frame-impacted-streams.md)
      * [[!UICONTROL 삭제된 프레임]](/help/reporting/metrics/dropped-frames.md)
      * [[!UICONTROL 시작 전 드롭]](/help/reporting/metrics/drops-before-start.md)
      * [[!UICONTROL 오류 이벤트]](/help/reporting/metrics/error-events.md)
      * [[!UICONTROL 오류 영향을 받은 스트림]](/help/reporting/metrics/error-impacted-streams.md)
      * [[!UICONTROL 시작 시간]](/help/reporting/metrics/time-to-start.md)
      * [[!UICONTROL 총 버퍼 지속 시간]](/help/reporting/metrics/total-buffer-duration.md)
* **[!UICONTROL 비디오 메타데이터]**: 쇼, 시즌 및 장르와 같은 표준 비디오 콘텐츠 특성을 추적할 수 있습니다.
   * **차원:**
      * [[!UICONTROL 광고 로드]](/help/reporting/dimensions/ad-load-type.md)
      * [[!UICONTROL 일 파트]](/help/reporting/dimensions/day-part.md)
      * [[!UICONTROL 에피소드]](/help/reporting/dimensions/episode.md)
      * [[!UICONTROL 장르]](/help/reporting/dimensions/genre.md)
      * [[!UICONTROL 미디어 피드 유형]](/help/reporting/dimensions/media-feed-type.md)
      * [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md)
      * [[!UICONTROL 네트워크]](/help/reporting/dimensions/network.md)
      * [[!UICONTROL 시즌]](/help/reporting/dimensions/season.md)
      * [[!UICONTROL 표시]](/help/reporting/dimensions/show.md)
      * [[!UICONTROL 표시 형식]](/help/reporting/dimensions/show-type.md)
   * **지표:**
      * [[!UICONTROL 인증됨]](/help/reporting/metrics/authorized.md)
* **[!UICONTROL 오디오 메타데이터]**: 아티스트, 앨범 및 스테이션과 같은 표준 오디오 콘텐츠 특성을 추적할 수 있습니다.
   * **차원:**
      * [[!UICONTROL 앨범]](/help/reporting/dimensions/album.md)
      * [[!UICONTROL 아티스트]](/help/reporting/dimensions/artist.md)
      * [[!UICONTROL 작성자]](/help/reporting/dimensions/author.md)
      * [[!UICONTROL 레이블]](/help/reporting/dimensions/label.md)
      * [[!UICONTROL 게시자]](/help/reporting/dimensions/publisher.md)
      * [[!UICONTROL 스테이션]](/help/reporting/dimensions/station.md)
* **[!UICONTROL 플레이어 상태 추적]**: 전체 화면, 자막 및 화면 속 사진과 같은 표준 플레이어 UI 상태를 측정할 수 있습니다.
   * **지표:**
      * [[!UICONTROL 자막 개수]](/help/reporting/metrics/closed-captioning-count.md)
      * [[!UICONTROL 자막 총 기간]](/help/reporting/metrics/closed-captioning-total-duration.md)
      * [[!UICONTROL 전체 화면 수]](/help/reporting/metrics/full-screen-count.md)
      * [[!UICONTROL 전체 화면 총 기간]](/help/reporting/metrics/full-screen-total-duration.md)
      * [[!UICONTROL 포커스 카운트]](/help/reporting/metrics/in-focus-count.md)
      * [[!UICONTROL 초점 총 기간]](/help/reporting/metrics/in-focus-total-duration.md)
      * [[!UICONTROL 음소거 카운트]](/help/reporting/metrics/mute-count.md)
      * [[!UICONTROL 음소거 총 기간]](/help/reporting/metrics/mute-total-duration.md)
      * [[!UICONTROL 화면 속 화면 수]](/help/reporting/metrics/picture-in-picture-count.md)
      * [[!UICONTROL 화면 속 화면 총 시간]](/help/reporting/metrics/picture-in-picture-total-duration.md)
      * [[!UICONTROL 닫힌 캡션의 영향을 받은 스트림]](/help/reporting/metrics/closed-captioning-streams-impacted.md)
      * [[!UICONTROL 전체 화면의 영향을 받은 스트림]](/help/reporting/metrics/full-screen-streams-impacted.md)
      * [[!UICONTROL 초점의 영향을 받은 스트림]](/help/reporting/metrics/in-focus-streams-impacted.md)
      * [[!UICONTROL 음소거의 영향을 받은 스트림]](/help/reporting/metrics/mute-streams-impacted.md)
      * [[!UICONTROL 화면 속 화면의 영향을 받은 스트림]](/help/reporting/metrics/picture-in-picture-streams-impacted.md)

>[!MORELIKETHIS]
>
>* [Workspace의 미디어 보고서](/help/reporting/workspace/media-workspace-templates.md)
>* [차원 개요](/help/reporting/dimensions/overview.md)
>* [지표 개요](/help/reporting/metrics/overview.md)
