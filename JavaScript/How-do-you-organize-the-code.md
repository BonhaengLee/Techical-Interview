# 코드를 어떻게 구성하세요? ( 모듈 패턴, 고전적인 상속 ) #

과거에는 MVC패턴에 맞게 모델을 만들어 모델에 메서드를 연결하는 등 OOP 접근 방식을 사용했습니다.

[모듈 패턴](https://forgottenknowledge.tistory.com/60)은 여전히 훌륭하지만,  
요즘에는 React.js/Redux 기반의 `Flux 아키텍쳐`를 사용합니다.  
이 아키텍쳐는 **단방향 프로그래밍 방식을 권장**합니다.  

React.js는 `데이터 변화에 따른 렌더링을 관리`하기 위한 라이브러리이므로 결국 **데이터 변화나 데이터 자체를 잘 다루는 것이 중요**합니다.    
`여러 컴포넌트에서 공유`해야 하는 데이터의 위치를 정하는 것에 대한 고민을 Redux가 해결합니다.  

Redux에서 상태(State)는 다른 Redux 응용 프로그램에서와 마찬가지로 action 및 reducer를 사용하여 조작됩니다.

또, 가능한 고전적인 상속을 사용하지 않습니다.  
이 [규칙](https://medium.com/@dan_abramov/how-to-use-classes-and-sleep-at-night-9af8de78ccb4)들을 지킵니다.

### 참고 ###

-<https://www.frontendinterviewhandbook.com/kr/javascript-questions/#%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EC%9C%84%EC%9E%84%EC%97%90-%EB%8C%80%ED%95%B4-%EC%84%A4%EB%AA%85%ED%95%98%EC%84%B8%EC%9A%94>