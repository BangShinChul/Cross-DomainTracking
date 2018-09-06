# Cross-DomainTracking
> 참조: </br>
> https://www.analyticspros.com/blog/rollup-properties/implications-of-cross-domain-tracking/ </br>
> https://support.google.com/analytics/answer/1034342?hl=ko </br>
> https://developers.google.com/analytics/devguides/collection/gtagjs/cross-domain </br>
   
   
## 교차 도메인 추적 이란?
교차 도메인 추적을 이용하면 애널리틱스 시스템이 관련 사이트 2개에서 발생하는 여러 세션을 단일 세션으로 처리</br>
Google 웹 로그 분석은 고유 한 클라이언트 ID를 생성하여 사용자가 신규인지 재방인지를 결정.</br>
일치하는 클라이언트 ID가 이미 전송 된 경우 재방문으로 간주</br>
교차 도메인 추적은 원본 도메인과 대상 도메인간에 클라이언트 ID를 공유하여 작동하며 클라이언트 ID는 브라우저의 쿠키에 저장</br>
여러 도메인을 소유하고 있으며 하나의 속성으로 취급하려는 경우 추적하려는 모든 도메인에서 클라이언트 ID를 공유하여 처리</br>
   
   
## 도메인간 클라이언트 ID 공유과정
 - 원본 도메인은 대상 도메인을 가리키는 모든 URL에 원본 도메인의 클라이언트 ID가 포함되도록 처리</br>
 - 대상 도메인은 사용자가 URL을 탐색 할 때 URL에서 클라이언트 ID가 있는지 확인</br>
 - gtag.js로 교차 도메인 추적은 대상 도메인을 가리키는 URL에 링커 매개변수를 추가하여 처리</br>
 - 링커 매개변수에는 클라이언트 ID와 그 안에 인코딩 된 현재 타임 스탬프 및 브라우저 메타 데이터가 포함</br>
   
    
## 설정별 추적가이드
   - gtag.js로 교차 도메인 추적 : https://support.google.com/analytics/answer/7476333 </br>
   - Google 태그 관리자를 사용하여 교차 도메인 추적 설정 : https://support.google.com/tagmanager/answer/6106951 </br>
   - 추적 코드를 수정하여 교차 도메인 추적 설정 : https://support.google.com/analytics/answer/1034342?hl=ko </br>
   
   
## 추적확인
   - Google Tag Assistant Recordings </br>
   - 가이드 : https://support.google.com/analytics/answer/6280771 </br>
   
   
## gtag.js로 교차 도메인 추적
> 참조 : https://developers.google.com/analytics/devguides/collection/gtagjs/cross-domain </br>
   - 도메인 자동 연결 </br>
   ```
   gtag('config', 'GA_TRACKING_ID', {
     'linker': {
         'domains': ['example.com']
      }
   });
   ```
   
  - 링커 매개 변수를 허용하도록 사이트 구성</br>
   ```
   gtag('config', 'GA_TRACKING_ID', {
     'linker': {
          'accept_incoming': true
      }
   });
   ```
   
   - 양방향 교차 도메인 추적 </br>
   ```
   //example-source.com 설정
   gtag('config', 'GA_TRACKING_ID', {
     'linker': {
          'domains': ['example-destination.com']
      }
   });
   
   //example-destination.com 설정
   gtag('config', 'GA_TRACKING_ID', {
      'linker': {
          'domains': ['example-source.com']
      }
   });
   ```
   
   - 양방향 교차 도메인 추적 단순화 (모든 도메인에서 단일 스 니펫 사용) </br>
   ```
   //example-1.com
   gtag('config', 'GA_TRACKING_ID_1', {
      'linker': {
          'domains': ['example-1.com', 'example-2.com']
       }
   });
   
   //example-2.com
   gtag('config', 'GA_TRACKING_ID_2', {
      'linker': {
          'domains': ['example-1.com', 'example-2.com']
      }
   });
   ```
