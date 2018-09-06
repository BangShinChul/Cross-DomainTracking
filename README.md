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
   > 대상 도메인을 원본 도메인에 자동 교차 도메인 추적을 설정하려면 linker, domains매개 변수 설정</br>
   > gtag.js는 대상 도메인(또는 도메인)을 가리키는 링크를 수신하고 탐색 시작 직전에 링크에 자동으로 링커 매개 변수를 추가</br>
   > 링커 매개 변수는 2 분 후에 만료되기 때문에 사용자가 링크를 클릭하여 링커 매개 변수를 추가 할 때까지 대기
   ```
   gtag('config', 'GA_TRACKING_ID', {
     'linker': {
         'domains': ['example.com']
      }
   });
   ```
   </br>
  - 링커 매개 변수를 허용하도록 사이트 구성</br>
  > 사용자가 URL에 링커 매개 변수가 있는 대상 도메인의 페이지에 도착하면 gtag.js는 해당 매개 변수를 추적
  > 대상 도메인이 도메인을 자동으로 연결하도록 구성된 경우 기본적으로 링커 매개 변수를 수락
  > 대상 도메인이 도메인을 자동으로 연결하도록 구성되지 않은 경우 대상 속성의 config에 매개 변수 accept_incoming속성을 설정
   ```
   gtag('config', 'GA_TRACKING_ID', {
     'linker': {
          'accept_incoming': true
      }
   });
   ```
   </br>
   - 양방향 교차 도메인 추적</br>
   > 먼저 방문할 도메인을 알 수 없는 경우 적용
   > 두 도메인 모두 자동연결 활성화 및 링커 매개변수 허용, 도메인 자동연결로 구성
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
   </br>
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
