---
product: adobe analytics
audience: end-user
user-guide-title: 스트리밍 미디어 컬렉션
breadcrumb-title: 스트리밍 미디어 컬렉션 안내서
user-guide-description: 스트리밍 미디어 구현. Media SDK 및 Media Collection API를 포함합니다.
sub-product: media analytics
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 96%

---


# 스트리밍 미디어 컬렉션 {#using}

+ [스트리밍 미디어 컬렉션 안내서](media-overview.md)
+ 릴리스 정보 {#release-notes}
   + [스트리밍 미디어 컬렉션 릴리스 정보](additional-resources/release-notes.md)
+ 시작하기 {#getting-started}
   + [사전 요구 사항](getting-started/prereqs.md)
   + [지원되는 디바이스](getting-started/supported-devices.md)
   + [스트리밍 미디어 컬렉션 구현 설명서](getting-started/implementation-documentation.md)
   + [SDK, 라이브러리 및 확장 기능](getting-started/download-sdks.md)
   + 지원 종료 {#end-of-support}
      + [Media Analytics Mobile SDK 지원 종료](additional-resources/end-of-support-faqs.md)
      + 레거시 - 독립형 Media SDK에서 Launch로의 마이그레이션 {#sdk-to-launch}
         + [개요](legacy/sdk-to-launch/sdk-to-launch-migration.md)
         + [Android - Media SDK에서 Launch로의 마이그레이션](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS - Media SDK에서 Launch로의 마이그레이션](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JavaScript - Media SDK에서 Launch로의 마이그레이션](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ 구현 {#implementation}
   + [구현 개요](implementation/overview.md)
   + Edge 구현 (권장) {#edge-recommended}
      + [사전 요구 사항](/help/implementation/edge/prerequisites-edge.md)
      + Media Edge SDK / 확장 기능 {#media-edge-sdk}
         + [Media Edge SDK / 확장 기능 설정](/help/implementation/edge/implementation-edge.md)
         + [Media Edge 웹 SDK](/help/implementation/edge/edge-web-sdk.md)
         + [Media Edge Mobile SDK](/help/implementation/edge/edge-mobile-sdk.md)
      + [Media Edge API](/help/implementation/edge/implementation-edge-api.md)
   + Adobe Analytics 전용 구현 {#analytics-only}
      + [사전 요구 사항](/help/implementation/media-sdk/setup/prerequisites-analytics.md)
      + Media SDK / 확장 기능 {#media-sdk}
         + [JavaScript Web SDK](implementation/media-sdk/setup/web-implementation.md)
         + [Media Analytics 확장 기능](implementation/media-sdk/setup/web-implementation-tags.md)
         + [Mobile SDK](implementation/media-sdk/setup/mobile-implementation.md)
         + OTT SDK {#ott-setup}
            + [Chromecast SDK 설치](implementation/media-sdk/setup/set-up-chromecast.md)
            + [Roku SDK 설치](implementation/media-sdk/setup/set-up-roku.md)
      + Media Collection API - 구현 {#streaming-media-apis}
         + [미디어 컬렉션](implementation/media-collection-api/mc-api-overview.md)
         + [API 빠른 시작](implementation/media-collection-api/mc-api-impl/mc-api-quick-start.md)
         + [세션 요청](implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)
         + [이벤트 요청](implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)
         + [요청 매개변수](implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)
         + [이벤트 유형 및 설명](implementation/media-collection-api/mc-api-ref/mc-api-event-types.md)
         + API 구현 {#mc-api-impl}
            + [플레이어에서 HTTP 요청 유형 설정](implementation/media-collection-api/mc-api-impl/mc-api-set-http-req.md)
            + [세션 ID 가져오기](implementation/media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
            + [이벤트 요청 구현](implementation/media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
            + [JSON 유효성 검사 스키마](implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md)
            + [이벤트 요청 확인](implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
            + [Ping 이벤트 보내기](implementation/media-collection-api/mc-api-impl/mc-api-sed-pings.md)
            + [QoE 데이터 보내기](implementation/media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
            + [사용자 정의 메타데이터 지원](implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)
            + [시간 제한 조건](implementation/media-collection-api/mc-api-impl/mc-api-timeout.md)
            + [이벤트 순서 제어](implementation/media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
            + [세션 응답이 느린 경우 큐에 이벤트 저장](implementation/media-collection-api/mc-api-impl/mc-api-queuing.md)
   + 변수 {#variables}
      + [스트리밍 미디어 매개변수](implementation/variables/audio-video-parameters.md)
      + [광고 매개변수](implementation/variables/ad-parameters.md)
      + [챕터 매개변수](implementation/variables/chapter-parameters.md)
      + [플레이어 상태 매개변수](implementation/variables/player-state-parameters.md)
      + [품질 매개변수](implementation/variables/quality-parameters.md)
      + [계산된 지표](implementation/variables/calculated-metrics.md)
+ 보고 {#media-reports}
   + [미디어 보고서 지원](reporting/media-reports-enable.md)
   + Workspace의 미디어 패널 {#media-workspace-panels}
      + [미디어 대상자 평균 시간 패널](reporting/workspace/average-minute-audience.md)
      + [미디어 동시 뷰어 패널](reporting/workspace/media-concurrent-viewers-overview.md)
      + [미디어 재생 소요 시간 패널](reporting/workspace/media-playback-time-spent.md)
   + [Workspace의 미디어 보고서](reporting/workspace/media-workspace-templates.md)
   + [미디어 세그먼트](reporting/segments.md)
   + 기본 미디어 보고서 {#media-default-reports}
      + [기본 보고서 개요](reporting/reports-and-analytics/default-reports-overview.md)
      + [미디어 개요](reporting/reports-and-analytics/media-reports-overview.md)
      + [미디어 세부 정보](reporting/reports-and-analytics/media-reports-detail.md)
      + [미디어 방송 시간 보고서](reporting/reports-and-analytics/media-reports-daypart.md)
      + [미디어 동시 뷰어 보고서](reporting/reports-and-analytics/media-concurrent-viewers-reports.md)
   + Media API {#media-api}
      + [동시 뷰어 데이터 가져오기](reporting/reports-and-analytics/get-concurrent-json20.md)
      + [미디어 재생 소요 시간 데이터 가져오기](reporting/reports-and-analytics/get-mediaplaybacktimespent-json20.md)
+ 사용 사례 {#media-use-cases}
   + [Media SDK 사용 사례](use-cases/cookbook/sdk-cookbook-overview.md)
   + 플레이어 상태 추적 {#player-state-tracking}
      + [개요](use-cases/player-state-tracking/player-state-overview.md)
      + [표준 및 사용자 정의 상태](use-cases/player-state-tracking/standard-and-custom-states.md)
      + [구현 및 보고](use-cases/player-state-tracking/implementation-and-reporting.md)
      + [여러 플레이어 상태 추적](use-cases/player-state-tracking/multiple-player-states.md)
      + [플레이어 상태 추적 예](use-cases/player-state-tracking/player-state-examples.md)
   + [다운로드한 콘텐츠 추적](use-cases/track-downloaded-content.md)
   + [페더레이션 미디어](use-cases/federated-media.md)
   + [재생 중 애플리케이션 중단 처리](use-cases/cookbook/app-interrupts.md)
   + [미디어 스트림 속성](use-cases/media-analytics-cookbook/media-dimensions.md)
   + [비활성 세션 다시 시작](use-cases/cookbook/resuming-inactive.md)
   + [SceneGraph에서 Roku 추적](use-cases/cookbook/sdk-track-scenegraph.md)
   + [광고 사이의 간격 처리](use-cases/cookbook/fix-ad-play-ad.md)
   + 타임라인 {#timelines}
      + [챕터 시작과 끝](use-cases/timelines/chapter-start-end.md)
      + [콘텐츠 끝까지 보기](use-cases/timelines/view-to-end-of-content.md)
      + [세션 포기](use-cases/timelines/user-abandons-session.md)
   + OTT 앱의 분석 사용 {#analytics-with-ott}
      + [앱 상태 추적](use-cases/analytics-with-ott/track-app-states.md)
      + [앱 작업 추적](use-cases/analytics-with-ott/track-app-actions.md)
      + [사용자 ID 설정](use-cases/analytics-with-ott/set-user-ids.md)
      + [OTT 및 Audience Manager](use-cases/analytics-with-ott/ott-am.md)
      + [OTT 및 Experience Cloud](use-cases/analytics-with-ott/ott-experience-cloud.md)
+ 추적 {#tracking}
   + [개요](use-cases/track-av-playback/track-core-overview.md)
   + 코어 스트리밍 미디어 재생 추적 {#track-core}
      + [JavaScript 3.x에서 코어 재생 추적](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
      + [Chromecast에서 코어 재생 추적](use-cases/track-av-playback/track-core/track-core-chromecast.md)
      + [Roku에서 코어 재생 추적](use-cases/track-av-playback/track-core/track-core-roku.md)
   + 버퍼링 추적 {#track-buffering}
      + [JavaScript 3.x에서 버퍼링 추적](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
      + [Chromecast에서 버퍼링 추적](use-cases/track-av-playback/track-buffering/track-buffering-chromecast.md)
      + [Roku에서 버퍼링 추적](use-cases/track-av-playback/track-buffering/track-buffering-roku.md)
   + 찾기 추적 {#track-seeking}
      + [JavaScript 3.x에서 찾기 추적](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
      + [Chromecast에서 찾기 추적](use-cases/track-av-playback/track-seeking/track-seeking-chromecast.md)
      + [Roku에서 찾기 추적](use-cases/track-av-playback/track-seeking/track-seeking-roku.md)
   + 표준 메타데이터 구현 {#impl-std-metadata}
      + [JavaScript 3.x에서 표준 메타데이터 구현](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
      + [Chromecast에서 표준 메타데이터 구현](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
      + [표준 메타데이터 매개변수 - Chromecast](use-cases/track-av-playback/impl-std-metadata/chromecast-metadata.md)
      + [Roku에서 표준 메타데이터 구현](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
      + [표준 메타데이터 매개변수 - Roku](use-cases/track-av-playback/impl-std-metadata/roku-metadata.md)
   + 광고 추적 {#track-ads}
      + [개요](use-cases/track-ads/track-ads-overview.md)
      + [JavaScript 3.x에서 광고 추적](use-cases/track-ads/track-ads-js/track-ads-js3.md)
      + [Chromecast에서 광고 추적](use-cases/track-ads/track-ads-chromecast.md)
      + [Roku에서 광고 추적](use-cases/track-ads/track-ads-roku.md)
      + 표준 광고 메타데이터 구현 {#impl-std-ad-metadata}
         + [JavaScript 3.x에서 표준 광고 메타데이터 구현](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Roku에서 표준 광고 메타데이터 구현](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + 챕터 및 세그먼트 추적 {#track-chapters}
      + [개요](use-cases/track-chapters/track-chapters-overview.md)
      + [JavaScript 3.x에서 챕터 및 세그먼트 추적](use-cases/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Chromecast에서 챕터 및 세그먼트 추적](use-cases/track-chapters/track-chapters-chromecast.md)
      + [Roku에서 챕터 및 세그먼트 추적](use-cases/track-chapters/track-chapters-roku.md)
   + 체감 품질 추적 {#track-qos}
      + [개요](use-cases/track-qos/track-qos-overview.md)
      + [JavaScript 3.x에서 체감 품질 추적](use-cases/track-qos/track-qos-js/track-qos-js3.md)
      + [Chromecast에서 체감 품질 추적](use-cases/track-qos/track-qos-chromecast.md)
      + [Roku에서 체감 품질 추적](use-cases/track-qos/track-qos-roku.md)
   + 오류 추적 {#track-errors}
      + [개요](use-cases/track-errors/track-errors-overview.md)
      + [JavaScript 3.x에서 오류 추적](use-cases/track-errors/track-errors-js/track-errors-js3.md)
      + [Chromecast에서 오류 추적](use-cases/track-errors/track-errors-chromecast.md)
      + [Roku에서 오류 추적](use-cases/track-errors/track-errors-roku.md)
+ 개인정보 보호 및 보안 {#streaming-media-privacy}
   + [옵트아웃 및 개인정보 보호 설정](privacy/opt-out-privacy.md)
   + [보안](privacy/security.md)
+ 레거시 구현 {#legacy-implementations}
   + [레거시 개요](legacy/setup/legacy-setup-overview.md)
   + [레거시 — SDK 다운로드](legacy/legacy-download-sdks.md)
   + 레거시 - Media SDK {#legacy-media-sdks}
      + [레거시 - Media SDK 개요](legacy/media-sdk/setup/setup-overview.md)
      + [Android 설정](legacy/media-sdk/setup/set-up-android.md)
      + [iOS 설정](legacy/media-sdk/setup/set-up-ios.md)
      + JavaScript 설정 {#setup-javascript}
         + [JavaScript 2.x 설정](legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
   + [하트비트 측정 정보](legacy/heartbeat-measurement.md)
   + [Adobe Primetime](legacy/intro-to-ava/implementation-paths/primetime-path.md)
   + [Adobe 대상자 관리 지원](legacy/intro-to-ava/am-enablement.md)
   + [사용자 정의 링크 구현](legacy/measurement-options/cl-in-aa/cl-impl-guide.md)
   + 이전 마일스톤 추적 {#legacy-milestone-tracking}
      + [이전 마일스톤 추적](legacy/measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [마일스톤을 VA로 마이그레이션](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [마일스톤을 CL로 마이그레이션](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + 유효성 검사 {#validation}
      + [유효성 검사 개요](legacy/validation/validation-overview.md)
      + [테스트 1: 표준 재생](legacy/validation/test1-standard-playback.md)
      + [테스트 2: 미디어 중단](legacy/validation/test2-media-interrupt.md)
      + [테스트 호출 세부 사항](legacy/validation/test-call-details.md)
      + [하트비트 매개변수 설명](legacy/validation/heartbeat-params.md)
      + 디버깅 {#debugging}
         + [SDK 디버깅](legacy/validation/debugging/sdk-debugging.md)
   + [이전 마이그레이션: VHL 1.x에서 VHL 2.x로](legacy/va-1x-to-2x/mig-1x-2x-overview.md)
   + [코드 비교 v1.x대 v2.x](legacy/va-1x-to-2x/code-comparison-1x-2x.md)
   + [API 1x에서 2x로 추적](legacy/va-1x-to-2x/1x-2x-api-change.md)
   + [레거시 - AVA 소개](legacy/intro-to-ava/implementation-paths/implementation-paths.md)
   + [클라이언트측 경로](legacy/intro-to-ava/implementation-paths/client-side-path.md)
   + 이전 추적 {#track-av-playback}
      + [Android에서 코어 재생 추적](use-cases/track-av-playback/track-core/track-core-android.md)
      + [iOS에서 코어 재생 추적](use-cases/track-av-playback/track-core/track-core-ios.md)
      + JavaScript에서 코어 재생 추적 {#track-core-javascript}
         + [JavaScript 2.x에서 코어 재생 추적](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js.md)
         + [Android에서 버퍼링 추적](use-cases/track-av-playback/track-buffering/track-buffering-android.md)
         + [iOS에서 버퍼링 추적](use-cases/track-av-playback/track-buffering/track-buffering-ios.md)
         + JavaScript에서 버퍼링 추적 {#track-buffering-js}
            + [JavaScript 2.x에서 버퍼링 추적](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
         + [Android에서 찾기 추적](use-cases/track-av-playback/track-seeking/track-seeking-android.md)
         + [iOS에서 찾기 추적](use-cases/track-av-playback/track-seeking/track-seeking-ios.md)
         + JavaScript에서 찾기 추적 {#track-seeking-js}
            + [JavaScript 2.x에서 찾기 추적](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
         + [Android에서 표준 메타데이터 구현](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [iOS에서 표준 메타데이터 구현](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS 메타데이터 키](use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + JavaScript에서 표준 메타데이터 구현 {#impl-std-md-js}
            + [JavaScript 2.x에서 표준 메타데이터 구현](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
      + 광고 추적 {#track-ads}
         + [Android에서 광고 추적](use-cases/track-ads/track-ads-android.md)
         + [iOS에서 광고 추적](use-cases/track-ads/track-ads-ios.md)
         + JavaScript에서 광고 추적 {#track-ads-js}
            + [JavaScript 2.x에서 광고 추적](use-cases/track-ads/track-ads-js/track-ads-js.md)
            + [Android에서 표준 광고 메타데이터 구현](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
            + [iOS에서 표준 광고 메타데이터 구현](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
            + JavaScript에서 표준 광고 메타데이터 구현 {#impl-std-ad-md-js}
               + [JavaScript 2.x에서 표준 광고 메타데이터 구현](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
      + 챕터 및 세그먼트 추적 {#track-chapters}
         + [Android에서 챕터 및 세그먼트 추적](use-cases/track-chapters/track-chapters-android.md)
         + [iOS에서 챕터 및 세그먼트 추적](use-cases/track-chapters/track-chapters-ios.md)
         + JavaScript에서 챕터 및 세그먼트 추적 {#track-chapters-js}
            + [JavaScript 2.x에서 챕터 및 세그먼트 추적](use-cases/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Android에서 체감 품질 추적](use-cases/track-qos/track-qos-android.md)
         + [iOS에서 체감 품질 추적](use-cases/track-qos/track-qos-ios.md)
         + JavaScript에서 체감 품질 추적 {#track-qos-js}
            + [JavaScript 2.x에서 체감 품질 추적](use-cases/track-qos/track-qos-js/track-qos-js.md)
      + 오류 추적 {#track-errors}
         + [Android에서 오류 추적](use-cases/track-errors/track-errors-android.md)
         + [iOS에서 오류 추적](use-cases/track-errors/track-errors-ios.md)
         + JavaScript에서 오류 추적 {#track-errors-js}
            + [JavaScript 2.x에서 오류 추적](use-cases/track-errors/track-errors-js/track-errors-js.md)
      + 추적 시나리오 {#tracking-scenarios}
         + [광고가 없는 VOD 재생](use-cases/tracking-scenarios/vod-no-intrs-details.md)
         + [프리롤 광고가 있는 VOD 재생](use-cases/tracking-scenarios/vod-preroll-ads.md)
         + [건너뛴 광고가 있는 VOD 재생](use-cases/tracking-scenarios/vod-skipped-ads.md)
         + [한 개의 챕터가 있는 VOD 재생](use-cases/tracking-scenarios/vod-one-chapter.md)
         + [건너뛴 챕터가 있는 VOD 재생](use-cases/tracking-scenarios/vod-skipped-chapter.md)
         + [주요 콘텐츠에 찾기가 있는 VOD 재생](use-cases/tracking-scenarios/vod-seeking.md)
         + [버퍼링이 있는 VOD 재생](use-cases/tracking-scenarios/vod-buffering.md)
         + [VOD 여러 추적기 동시 실행](use-cases/tracking-scenarios/vod-multi-trackers.md)
         + [VOD 여러 세션에 대한 한 개의 추적기](use-cases/tracking-scenarios/vod-multi-track-one-session.md)
         + [라이브 주요 콘텐츠](use-cases/tracking-scenarios/live-main-content.md)
         + [순차적 추적을 사용하는 라이브 주요 콘텐츠](use-cases/tracking-scenarios/live-sequential.md)
