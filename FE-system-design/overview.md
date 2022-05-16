# 프론트엔트 시스템 설계 개요 #

프론트엔드 시스템 설계 리소스는 놀랍도록 없는데, 아마 프론트엔드 엔지니어 후보자의 수요나 공급이 적기 때문일 겁니다.

여기서 시스템은 일반적인 sw 엔지니어의 분산 시스템 설계 질문과는 상당히 다릅니다. "Build user interfaces"와 같은 질문과 매우 유사할 수 있지만 아키텍쳐나 디자인에 더 중점을 둘 수 있습니다. 그들은 서로 상당히 겹칠 수 있습니다. (UI를 빌드할 때 일부 디자인(data model, API)을 수행하고 당신의 아이디어나 App의 state를 설명하기 위해 코딩해야 합니다.)

"Build user interfaces"와 다른 점은 이 질문이 일반적으로 더 크다는 겁니다.  
세션이 반 시간도 안된다면, the design tradeoffs, possible implementations에 대해서 이야기해야 합니다.  
시스템 설계 질문에는 일반적으로 웹 스택 전반에 걸쳐 여러 구성 요소와 지식이 포함되므로 일반적으로 하위 수준 세부 정보까지 자세히 설명할 필요가 없습니다.  
`클라이언트와 서버 간의 API` 디자인 및 `구성 요소 간의 API`에 대한 토론을 더 높은 수준으로 유지할 수 있습니다.

"Build user interfaces"에서 언급한 API 디자인, 확장성, 성능, 사용자 경험, i18n, 접근성, 보안 등은 프론트엔드 시스템 설계와도 관련이 있습니다. 후보자가 주도권을 잡고 토론을 이끌어야 합니다.  
성능, 접근성, i18n는 senior와 junior를 구별하는 고급 주제입니다.

프론트엔드 시스템 디자인의 두 가지 주요 종류는 UI 컴포넌트와 응용 프로그램입니다.  

예제

    UI 구성 요소
        사진 갤러리
        선택자
    응용 프로그램
        뉴스 피드
        비디오 시청 웹 사이트
        채팅 응용 프로그램

## 라다드 프레임 워크 ##

시스템 설계 인터뷰 질문은 개방적이고 모호한 경향이 있으므로 탐색 할 여지가 많습니다. 면접관이 어떤 특정 영역에 집중해야하는지 알려주면 좋은데, 당신이 다룰 내용에 대한 개요를 제공하는 데 사용할 수있는 프레임 워크가 아래 있습니다.  
이 프레임 워크는 직장에서 **새로운 프런트 엔드 프로젝트를 작업 할 때도 유용**합니다.

이 프레임 워크는 `RADAD`라고하며 각 단계의 첫 번째 문자로 구성됩니다.

- `Requirements clarifications/alignment` - 시스템의 요구 사항에 대해 물어보십시오.
- `Architecture` - 시스템의 아키텍처를 간략하게 설명합니다(질문에 따라 UI 컴포넌트 또는 앱일 수 있음). 관련된 곳에 다이어그램을 그립니다.
- `Data model` - 컴포넌트는 전달 된 데이터를 어떻게 저장합니까? 어떤 데이터 구조가 사용됩니까?
- `API design` - 이 컴포넌트를 사용하기 위한 API는 무엇입니까? 컴포넌트에서 어떤 옵션이 허용됩니까?
- `Deep dive` - 사용자 경험(UX), 성능, 접근성(a11y), 국제화(i18n), 다중 장치 지원, 보안

응용 프로그램 및 UI 컴포넌트에 대한 시스템 디자인 질문에 접근하는 방법은 크게 다를 수 있습니다.

Things you would not have to do (probably)

Because front end system design interviews focus on front end, you probably do not have to:

- Design a database schema
- Know about which kind of database to use (SQL vs NoSQL)
- Scaling your servers and database (sharding, vertical/horizontal scaling)
- Talk about availability, fault tolerance, latency, etc

---
https://www.frontendinterviewhandbook.com/kr/front-end-system-design