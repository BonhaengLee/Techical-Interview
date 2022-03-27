# `.call`과 `.apply`의 차이점은 무엇인가요? #

.call과 .apply는 모두 **함수를 호출하는데 사용**되며,  
`첫 번째` 매개변수는 함수 내에서 `this의 값으로 사용`됩니다.   

그러나 .call은 `쉼표로 구분`된 인수를 `두 번째` 인수로 취하고 .apply는 인수의 `배열`을 `두 번째` 인수로 취합니다.  
call은 `C`: Comma 로 구분되며, apply는 인수 배열인 `A`: arguments 라고 기억하면 쉽습니다.

```javascript
function add(a, b) {
  return a + b;
}

console.log(add.call(null, 1, 2)); // 3
console.log(add.apply(null, [1, 2])); // 3
```
