# 프로토타입 상속이 어떻게 작동하는지 설명하세요 #

이는 매우 일반적인 JavaScript 인터뷰 질문입니다.  

모든 JavaScript 객체는 **다른 객체에 대한 참조**인 `__proto__ 프로퍼티`를 가지고 있습니다.  

객체의 프로퍼티에 접근할 때,  
해당 객체에 해당 프로퍼티가 없으면 JavaScript 엔진은 객체의 __proto__와 __proto__의 __proto__등을 보고 **프로퍼티 정의가 있을 때까지 찾고**,  

만약 객체의 프로퍼티에 접근할 때,  
해당 객체에 해당 프로퍼티가 없으면 프로토타입 체인 중 하나에 있거나 **프로토타입 체인의 끝에 도달할 때까지** 찾습니다.  

이 동작은 고전적인 상속을 흉내내지만,  
실제로 [상속보다 `위임`](https://davidwalsh.name/javascript-objects)에 더 가깝습니다.

### 참조 ###

[Medium](https://codeburst.io/the-simple-rules-to-this-in-javascript-35d97f31bde3)

<https://www.frontendinterviewhandbook.com/kr/javascript-questions/#%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EC%9C%84%EC%9E%84%EC%97%90-%EB%8C%80%ED%95%B4-%EC%84%A4%EB%AA%85%ED%95%98%EC%84%B8%EC%9A%94>
