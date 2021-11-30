---
product: adobe analytics
audience: end-user
user-guide-title: 스트리밍 미디어용 Adobe Analytics
breadcrumb-title: 미디어 분석 안내서
user-guide-description: 스트리밍 미디어용 Adobe Analytics 구현. Media SDK 및 Media Collection API를 포함합니다.
sub-product: media analytics
source-git-commit: 819f4a7035e5d9704d17abce6a7cd4c607b7ce39
workflow-type: ht
source-wordcount: '828'
ht-degree: 100%

---


# 스트리밍 미디어용 Adobe Analytics {#using}

+ [Adobe Analytics에서 스트리밍 미디어 측정](media-overview.md)
+ [지원되는 디바이스 및 플랫폼](measurement-options/supported-devices.md)
+ 스트리밍 미디어 분석 소개 {#intro-to-ava}
   + [사전 요구 사항](intro-to-ava/prereqs.md)
   + 구현 경로 {#implementation-paths}
      + [개요](intro-to-ava/implementation-paths/implementation-paths.md)
      + [클라이언트측](intro-to-ava/implementation-paths/client-side-path.md)
      + 기타 구현 경로 {#other-paths}
         + 미디어 모듈 이정표 추적 {#mm-milestone-tracking}
            + [이정표 개요](measurement-options/mm-milestone-tracking/milestone-overview.md)
            + [이정표를 Media Analytics로 마이그레이션](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
            + [이정표에서 사용자 지정 링크로의 마이그레이션](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
         + Analytics의 사용자 지정 링크 {#cl-in-aa}
            + [사용자 지정 링크 구현 안내서](measurement-options/cl-in-aa/cl-impl-guide.md)
         + Primetime {#primetime}
            + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
         + [Audience Manager 지원](intro-to-ava/am-enablement.md)
+ Media Analytics SDK {#sdk-implement}
   + [Media Analytics SDK 지원 종료 FAQ](sdk-implement/end-of-support-faqs.md)
   + [SDK 다운로드](sdk-implement/download-sdks.md)
   + 설정 및 구성 {#setup}
      + [개요](sdk-implement/setup/setup-overview.md)
      + [Android 설정](sdk-implement/setup/set-up-android.md)
      + [iOS 설정](sdk-implement/setup/set-up-ios.md)
      + JavaScript 설정 {#setup-javascript}
         + [JavaScript 2.x 설정](sdk-implement/setup/setup-javascript/set-up-js-2.md)
         + [JavaScript 3.x 설정](sdk-implement/setup/setup-javascript/set-up-js-3.md)
      + [Chromecast 설정](sdk-implement/setup/set-up-chromecast.md)
      + [Roku 설정](sdk-implement/setup/set-up-roku.md)
   + 스트리밍 미디어 재생 추적 {#track-av-playback}
      + [개요](sdk-implement/track-av-playback/track-core-overview.md)
      + 코어 스트리밍 미디어 재생 추적 {#track-core}
         + [Android에서 코어 재생 추적](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [iOS에서 코어 재생 추적](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + JavaScript에서 코어 재생 추적 {#track-core-javascript}
            + [JavaScript 2.x에서 코어 재생 추적](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js.md)
            + [JavaScript 3.x에서 코어 재생 추적](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
         + [Chromecast에서 코어 재생 추적](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Roku에서 코어 재생 추적](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + 버퍼링 추적 {#track-buffering}
         + [Android에서 버퍼링 추적](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [iOS에서 버퍼링 추적](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + JavaScript에서 버퍼링 추적 {#track-buffering-js}
            + [JavaScript 2.x에서 버퍼링 추적](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
            + [JavaScript 3.x에서 버퍼링 추적](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
         + [Chromecast에서 버퍼링 추적](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Roku에서 버퍼링 추적](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + 찾기 추적 {#track-seeking}
         + [Android에서 찾기 추적](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [iOS에서 찾기 추적](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + JavaScript에서 찾기 추적 {#track-seeking-js}
            + [JavaScript 2.x에서 찾기 추적](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
            + [JavaScript 3.x에서 찾기 추적](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
         + [Chromecast에서 찾기 추적](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Roku에서 찾기 추적](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + 표준 메타데이터 구현 {#impl-std-metadata}
         + [Android에서 표준 메타데이터 구현](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [iOS에서 표준 메타데이터 구현](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS 메타데이터 키](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + JavaScript에서 표준 메타데이터 구현 {#impl-std-md-js}
            + [JavaScript 2.x에서 표준 메타데이터 구현](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
            + [JavaScript 3.x에서 표준 메타데이터 구현](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
         + [Chromecast에서 표준 메타데이터 구현](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [표준 메타데이터 매개 변수 - Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Roku에서 표준 메타데이터 구현](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [표준 메타데이터 매개 변수 - Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + 광고 추적 {#track-ads}
      + [개요](sdk-implement/track-ads/track-ads-overview.md)
      + [Android에서 광고 추적](sdk-implement/track-ads/track-ads-android.md)
      + [iOS에서 광고 추적](sdk-implement/track-ads/track-ads-ios.md)
      + JavaScript에서 광고 추적 {#track-ads-js}
         + [JavaScript 2.x에서 광고 추적](sdk-implement/track-ads/track-ads-js/track-ads-js.md)
         + [JavaScript 3.x에서 광고 추적](sdk-implement/track-ads/track-ads-js/track-ads-js3.md)
      + [Chromecast에서 광고 추적](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Roku에서 광고 추적](sdk-implement/track-ads/track-ads-roku.md)
      + 표준 광고 메타데이터 구현 {#impl-std-ad-metadata}
         + [Android에서 표준 광고 메타데이터 구현](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [iOS에서 표준 광고 메타데이터 구현](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + JavaScript에서 표준 광고 메타데이터 구현 {#impl-std-ad-md-js}
            + [JavaScript 2.x에서 표준 광고 메타데이터 구현](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
            + [JavaScript 3.x에서 표준 광고 메타데이터 구현](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Roku에서 표준 광고 메타데이터 구현](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + 챕터 및 세그먼트 추적 {#track-chapters}
      + [개요](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Android에서 챕터 및 세그먼트 추적](sdk-implement/track-chapters/track-chapters-android.md)
      + [iOS에서 챕터 및 세그먼트 추적](sdk-implement/track-chapters/track-chapters-ios.md)
      + JavaScript에서 챕터 및 세그먼트 추적 {#track-chapters-js}
         + [JavaScript 2.x에서 챕터 및 세그먼트 추적](sdk-implement/track-chapters/track-chapters-js/track-chapters-js.md)
         + [JavaScript 3.x에서 챕터 및 세그먼트 추적](sdk-implement/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Chromecast에서 챕터 및 세그먼트 추적](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Roku에서 챕터 및 세그먼트 추적](sdk-implement/track-chapters/track-chapters-roku.md)
   + 체감 품질 추적 {#track-qos}
      + [개요](sdk-implement/track-qos/track-qos-overview.md)
      + [Android에서 체감 품질 추적](sdk-implement/track-qos/track-qos-android.md)
      + [iOS에서 체감 품질 추적](sdk-implement/track-qos/track-qos-ios.md)
      + JavaScript에서 체감 품질 추적 {#track-qos-js}
         + [JavaScript 2.x에서 체감 품질 추적](sdk-implement/track-qos/track-qos-js/track-qos-js.md)
         + [JavaScript 3.x에서 체감 품질 추적](sdk-implement/track-qos/track-qos-js/track-qos-js3.md)
      + [Chromecast에서 체감 품질 추적](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Roku에서 체감 품질 추적](sdk-implement/track-qos/track-qos-roku.md)
   + 오류 추적 {#track-errors}
      + [개요](sdk-implement/track-errors/track-errors-overview.md)
      + [Android에서 오류 추적](sdk-implement/track-errors/track-errors-android.md)
      + [iOS에서 오류 추적](sdk-implement/track-errors/track-errors-ios.md)
      + JavaScript에서 오류 추적 {#track-errors-js}
         + [JavaScript 2.x에서 오류 추적](sdk-implement/track-errors/track-errors-js/track-errors-js.md)
         + [JavaScript 3.x에서 오류 추적](sdk-implement/track-errors/track-errors-js/track-errors-js3.md)
      + [Chromecast에서 오류 추적](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Roku에서 오류 추적](sdk-implement/track-errors/track-errors-roku.md)
   + [옵트아웃 및 개인정보 보호](sdk-implement/opt-out-privacy.md)
   + 추적 시나리오 {#tracking-scenarios}
      + [광고가 없는 VOD 재생](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [프리롤 광고가 있는 VOD 재생](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [건너뛴 광고가 있는 VOD 재생](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [한 개의 챕터가 있는 VOD 재생](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [건너뛴 챕터가 있는 VOD 재생](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [주요 콘텐츠에 찾기가 있는 VOD 재생](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [버퍼링이 있는 VOD 재생](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [VOD 여러 추적기 동시 실행](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [VOD 여러 세션에 대한 1개의 추적기](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [라이브 주요 콘텐츠](sdk-implement/tracking-scenarios/live-main-content.md)
      + [순차적 추적을 사용하는 라이브 주요 콘텐츠](sdk-implement/tracking-scenarios/live-sequential.md)
   + 유효성 검사 {#validation}
      + [유효성 검사 개요](sdk-implement/validation/validation-overview.md)
      + [테스트 1: 표준 재생](sdk-implement/validation/test1-standard-playback.md)
      + [테스트 2: 미디어 중단](sdk-implement/validation/test2-media-interrupt.md)
      + [테스트 호출 세부 사항](sdk-implement/validation/test-call-details.md)
      + [하트비트 매개 변수 설명](sdk-implement/validation/heartbeat-params.md)
      + 디버깅 {#debugging}
         + [SDK 디버깅](sdk-implement/validation/debugging/sdk-debugging.md)
   + OTT 앱용 분석 {#analytics-with-ott}
      + [앱 상태 추적](sdk-implement/analytics-with-ott/track-app-states.md)
      + [앱 작업 추적](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [사용자 ID 설정](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT 및 Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT 및 Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + Cookbook {#cookbook}
      + [SDK Cookbook](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [재생 중 애플리케이션 중단 처리](sdk-implement/cookbook/app-interrupts.md)
      + [광고 사이에 표시되는 main:play 해결](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [비활성 세션 다시 시작](sdk-implement/cookbook/resuming-inactive.md)
      + [SceneGraph(Roku)에서 추적](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + Media Analytics 1.x에서 2.x로의 마이그레이션 {#va-1x-to-2x}
      + [마이그레이션 개요](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [코드 비교: 1.x대 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [1.x에서 2.x로의 API 전환](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
   + Media Analytics SDK에서 Launch로의 마이그레이션 {#sdk-to-launch}
      + [SDK에서 Launch로의 마이그레이션](sdk-implement/sdk-to-launch/sdk-to-launch-migration.md)
      + SDK에서 Launch로의 마이그레이션 플랫폼 안내서 {#sdk-to-launch-migration-platforms}
         + [Android](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ Media Collection API (RESTful) {#media-collection-api}
   + [개요](media-collection-api/mc-api-overview.md)
   + API 참조 {#mc-api-ref}
      + [세션 요청](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [이벤트 요청](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [요청 매개 변수](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [이벤트 유형 및 설명](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [JSON 유효성 검사 스키마](media-collection-api/mc-api-ref/mc-api-json-validation.md)
   + API 구현 {#mc-api-impl}
      + [빠른 시작](media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [플레이어에서 HTTP 요청 유형 설정](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
      + [세션 ID 가져오기](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
      + [이벤트 요청 구현](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
      + [이벤트 요청 확인](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
      + [Ping 이벤트 보내기](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
      + [QoE 데이터 보내기](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
      + [사용자 지정 메타데이터 지원](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
      + [시간 제한 조건](media-collection-api/mc-api-impl/mc-api-timeout.md)
      + [이벤트 순서 제어](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
      + [세션 응답이 느린 경우 큐에 이벤트 저장](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + 미디어 추적 타임라인 {#mc-api-timelines}
      + [타임라인 1 - 콘텐츠 끝까지 보기](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [타임라인 2 - 사용자가 세션을 중단함](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [타임라인 3 - 챕터](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
+ Cookbook {#media-analytics-cookbook}
   + [Cookbook](media-analytics-cookbook/media-analytics-cookbook.md)
   + [미디어 스트림 속성](media-analytics-cookbook/media-dimensions.md)
+ 지표 및 메타데이터 {#metrics-and-metadata}
   + [스트리밍 미디어 매개 변수](metrics-and-metadata/audio-video-parameters.md)
   + [광고 매개 변수](metrics-and-metadata/ad-parameters.md)
   + [챕터 매개 변수](metrics-and-metadata/chapter-parameters.md)
   + [플레이어 상태 매개 변수](metrics-and-metadata/player-state-parameters.md)
   + [품질 매개 변수](metrics-and-metadata/quality-parameters.md)
   + [세그먼트](metrics-and-metadata/segments.md)
   + [계산된 지표](metrics-and-metadata/calculated-metrics.md)
+ 보고 및 분석 {#media-reports}
   + [미디어 보고서 지원](media-reports/media-reports-enable.md)
   + 미디어 기본 보고서 {#media-default-reports}
      + [기본 보고서 개요](media-reports/media-default-reports/default-reports-overview.md)
      + [미디어 개요](media-reports/media-default-reports/media-reports-overview.md)
      + [미디어 세부 사항](media-reports/media-default-reports/media-reports-detail.md)
      + [미디어 날짜 보고서](media-reports/media-default-reports/media-reports-daypart.md)
      + [미디어 동시 뷰어 보고서](media-reports/media-default-reports/media-concurrent-viewers.md)
   + 미디어 작업 영역 패널 {#media-workspace-panels}
      + [미디어 동시 뷰어 패널](media-reports/media-workspace-panels/media-concurrent-viewers.md)
      + [미디어 재생 소요 시간 패널](media-reports/media-workspace-panels/media-playback-time-spent.md)
   + [미디어 작업 영역 템플릿](media-reports/media-workspace-templates.md)
   + [API를 통해 동시 뷰어 데이터 가져오기](media-reports/media-default-reports/get-concurrent-json20.md)
   + [API를 통해 미디어 재생 소요 시간 데이터 가져오기](media-reports/media-default-reports/get-mediaplaybacktimespent-json20.md)
+ [다운로드한 콘텐츠 추적](media-collection-api/track-downloaded-content.md)
+ 플레이어 상태 추적 {#player-state-tracking}
   + [개요](sdk-implement/player-state-tracking/player-state-overview.md)
   + [표준 및 사용자 지정 상태](sdk-implement/player-state-tracking/standard-and-custom-states.md)
   + [구현 및 보고](sdk-implement/player-state-tracking/implementation-and-reporting.md)
   + [플레이어 상태 추적 예](sdk-implement/player-state-tracking/player-state-examples.md)
+ [Federated Analytics](federated-analytics.md)
+ 추가 리소스 {#additional-resources}
   + [릴리스 정보](additional-resources/doc-updates.md)

<!-- + Player State Tracking {#player-state-tracking}
    + [Overview](sdk-implement/player-state-tracking/player-state-overview.md)
    + [Standard and custom states](sdk-implement/player-state-tracking/standard-and-custom-states.md)
    + [Implementation and reporting](sdk-implement/player-state-tracking/implementation-and-reporting.md)
    + [Player state tracking examples](sdk-implement/player-state-tracking/player-state-examples.md)
-->
