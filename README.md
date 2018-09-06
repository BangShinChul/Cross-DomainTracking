# Cross-DomainTracking
> 참조: </br>
> https://www.analyticspros.com/blog/rollup-properties/implications-of-cross-domain-tracking/ </br>
> https://support.google.com/analytics/answer/1034342?hl=ko </br>
> https://developers.google.com/analytics/devguides/collection/gtagjs/cross-domain </br>
   
   
## 교차 도메인이란?
교차 도메인 추적을 이용하면 애널리틱스 시스템이 관련 사이트 2개에서 발생하는 여러 세션을 단일 세션으로 처리</br>
Google 웹 로그 분석은 고유 한 클라이언트 ID를 생성하여 사용자가 신규인지 재방인지를 결정.</br>
일치하는 클라이언트 ID가 이미 전송 된 경우 재방문으로 간주</br>
교차 도메인 추적은 원본 도메인과 대상 도메인간에 클라이언트 ID를 공유하여 작동하며 클라이언트 ID는 브라우저의 쿠키에 저장</br>
여러 도메인을 소유하고 있으며 하나의 속성으로 취급하려는 경우 추적하려는 모든 도메인에서 클라이언트 ID를 공유하여 처리</br>
도메인간에 클라이언트 ID를 공유하는 과정은 두 단계처리</br>
 - 원본 도메인은 대상 도메인을 가리키는 모든 URL에 원본 도메인의 클라이언트 ID가 포함되도록해야합니다.</br>
 - 대상 도메인은 사용자가 URL을 탐색 할 때 URL에서 클라이언트 ID가 있는지 확인해야합니다.</br>
   
    
## 설정별 추적가이드
   - gtag.js로 교차 도메인 추적 : https://support.google.com/analytics/answer/7476333 </br>
   - Google 태그 관리자를 사용하여 교차 도메인 추적 설정 : https://support.google.com/tagmanager/answer/6106951 </br>
   - 추적 코드를 수정하여 교차 도메인 추적 설정 : https://support.google.com/analytics/answer/1034342?hl=ko </br>
   
   
## 추적확인
   - Google Tag Assistant Recordings </br>
   - 가이드 : https://support.google.com/analytics/answer/6280771 </br>
   
   
## gtag.js로 교차 도메인 추적
> 참조 : https://developers.google.com/analytics/devguides/collection/gtagjs/cross-domain </br>

