# 익명 함수의 일반적인 사용 사례는 무엇인가요? #

익명함수는 IIFE로 사용되어 지역 범위 내에서 일부 코드를 `캡슐화`하므로 선언된 변수가 전역 범위로 누출되지 않습니다.

```javascript
(function () {
  // 코드
})();
```

한번 사용되고 다른 곳에서는 사용할 필요가 없는 콜백입니다.  
함수 본체를 찾기 위해 다른 곳을 찾아볼 필요 없이 `호출하는 코드 바로 안에 핸들러가 정의되어 있으면 코드가 보다 독립적이고 읽기 쉽습니다.`

```javascript
setTimeout(function () {
  console.log('Hello world!');
}, 1000);
```

함수형 프로그래밍 또는 Lodash에 대한 인수(콜백과 유사)로 사용하는 사례.

```javascript
const arr = [1,2,3];
const double = arr.map(function (el) {
  return el * 2;
});
console.log(double); // [2, 4, 6]
```

### 참고 ###

- <https://www.frontendinterviewhandbook.com/kr/javascript-questions/#%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EC%9C%84%EC%9E%84%EC%97%90-%EB%8C%80%ED%95%B4-%EC%84%A4%EB%AA%85%ED%95%98%EC%84%B8%EC%9A%94>