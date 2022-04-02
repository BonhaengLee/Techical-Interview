# `호이스팅`에 대해 설명하세요 #

호이스팅은 코드에서 변수 선언의 동작을 설명하는데 사용되는 용어입니다. `var` 키워드로 선언되거나 초기화된 변수는 현재 스코프의 최상위까지 `옮겨`집니다.  
이것을 호이스팅이라고 합니다. 그러나 선언문만 `호이스팅`되며 할당되는 위치는 그대로입니다.  

사실 선언은 실제로 이동되지 않습니다.  
JS 엔진은 컴파일 중에 선언을 파싱하고 선언과 해당 스코프를 인식합니다. 선언을 해당 스코프의 맨 위로 옮겨지는 것으로 생각하여 동작을 이해하는 것이 더 쉬울 뿐입니다.  

몇 가지 예를 들어 봅니다.

```javascript
// var 선언이 호이스팅됩니다
console.log(foo); // **undefined**
var foo = 1;
console.log(foo); // 1

// let/const 선언은 호이스팅되긴 합니다. 하지만 TDZ에 빠져서 Error가 난다는 점이 다릅니다.
console.log(bar); // ReferenceError: bar is not defined
let bar = 2;
console.log(bar); // 2
```

함수 선언은 함수몸체가 호이스팅되는 반면, 변수 선언 형태로 작성된 **함수 표현식**은 **변수 선언만** 호이스팅됩니다.

```javascript
// 함수 선언
console.log(foo); // [Function: foo]
foo(); // 'FOOOOO'
function foo() {
  console.log('FOOOOO');
}
console.log(foo); // [Function: foo]

// 함수 표현식
console.log(bar); // undefined
bar(); // Uncaught TypeError: bar is not a function
var bar = function () {
  console.log('BARRRR');
};
console.log(bar); // [Function: bar]
```
