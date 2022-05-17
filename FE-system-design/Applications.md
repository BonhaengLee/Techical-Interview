# Applications #

예제

    - 소셜 네트워크
    - 비디오 시청 웹 사이트
    - 채팅 응용 프로그램
    - 메일 응용 프로그램

## Framework ##

    - 요구 사항 설명/정렬
    - Architecture
    - 데이터 모델
    - API 디자인
    - Deep dive
        - 사용자 환경(UX)
        - 성능
        - 접근성(a11y)
        - 국제화 (i18n)
        - 다중 장치 지원
        - 보안

## 요구사항 설명 ##

- 시스템에서 지원해야 하는 장치는 무엇인가요?  
- 사용자가 기본적으로 액세스하는 기본 장치는 무엇인가요?
- 어떤 브라우저를 지원해야 하나요?  
- 국제화를 지원해야 하나요?
- 앱이 오프라인으로 작동해야 하나요?

## Architecture ##

클라이언트 측 아키텍쳐에 중점을 둡니다.  

애플리케이션은 일반적으로 Model-View-Controller, Model-View-ViewModel, Flux, N 계층(데이터 계층이 클라이언트에 있는 경우)등이 포함됩니다.  

## 데이터 모델 ##

`서버 상태(DB)와 실제 클라이언트 상태(서버에 지속되지 않는)의 조합인 클라이언트 앱 상태`입니다.

...

## API 디자인 ##

애플리케이션용 API 설계는 HTTP/네트워크 `API 파라미터와 응답 모양을 참조`합니다.  

...

## Deep dive ##

모두 다루기 힘들 것이고 모두 연관 있지도 않을 것입니다.

    - 사용자 환경(UX)
    - 성능
    - 접근성(a11y)
    - 국제화 (i18n)
    - 다중 장치 지원
    - 보안

## 유용한 기사 ##

많은 기업들이 FE 도메인에서의 기술적 과제에 대해 블로그를 작성하며 FE 시스템 설계에 대해 자세히 알아볼 수있는 훌륭한 콘텐츠를 제공합니다.

    - [구글 포토 웹 UI 구축](https://medium.com/google-design/google-photos-45b714dfbed1)
    - [Twitter Lite와 고성능 React Progressive Web Apps at Scale](https://medium.com/@paularmstrong/twitter-lite-and-high-performance-react-progressive-web-apps-at-scale-d28a00e780a3)
    - [넷플릭스 웹 성능 사례 연구](https://medium.com/dev-channel/a-netflix-web-performance-case-study-c0bcde26a9d9)
    - [틴더 프로그레시브 웹 앱 성능 사례 연구](https://medium.com/@addyosmani/a-tinder-progressive-web-app-performance-case-study-78919d98ece0)
    - [Pinterest 프로그레시브 웹 앱 성능 사례 연구](https://medium.com/dev-channel/a-pinterest-progressive-web-app-performance-case-study-3bd6ed2e6154)
    - [A React And Preact Progressive Web App Performance Case Study: Treebo](https://medium.com/dev-channel/treebo-a-react-and-preact-progressive-web-app-performance-case-study-5e4f450d5299)
    - [새로운 Facebook.com 을 위한 기술 스택 재건](https://engineering.fb.com/2020/05/08/web/facebook-redesign/)  
