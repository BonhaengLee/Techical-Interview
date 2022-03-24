# `this`가 JavaScript에서 어떻게 작동하는지 설명하세요 #

this는 자바스크립트에서 가장 혼란스러운 개념 중 하나입니다.  
`this`의 값은 함수가 호출되는 방식에 따라 달라집니다.  
많은 설명 중에 Arnav Aggrawal의 설명이 가장 명확했습니다.  
규칙은 다음과 같습니다.

## 규칙 ##

1. 함수를 호출할 때 `new` 키워드를 사용하는 경우,  
함수 내부에 있는 `this`는 완전히 새로운 객체입니다.
2. `apply`, `call`, `bind`가 함수의 호출/생성에 사용되는 경우,  
함수 내의 `this`는 인수로 전달된 객체입니다.
3. `obj.method()`와 같이 함수를 메서드로 호출하는 경우,  
`this`는 해당 함수를 프로퍼티로 가진 객체입니다.
4. 함수가 자유 함수로 호출되는 경우,  
즉, 위의 조건 없이 호출되는 경우 `this`는 전역 객체입니다.  
브라우저에서는 `window`이고  
strict 모드(`use strict`)에서는 `undefined`가 됩니다.
5. 위의 규칙 중 다수가 적용되면 더 상위 규칙이 적용됩니다.
6. 화살표 함수인 경우 위의 모든 규칙을 무시하고 생성된 시점에서 상위 스코프의 `this`값을 받습니다.

### 참조 ###

[Medium](https://codeburst.io/the-simple-rules-to-this-in-javascript-35d97f31bde3)

<https://www.frontendinterviewhandbook.com/kr/javascript-questions/#%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EC%9C%84%EC%9E%84%EC%97%90-%EB%8C%80%ED%95%B4-%EC%84%A4%EB%AA%85%ED%95%98%EC%84%B8%EC%9A%94>
