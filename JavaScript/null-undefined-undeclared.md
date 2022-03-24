# null, undefined, undeclared의 차이점은 무엇인가요?<br/>어떻게 이 상태들에 대한 확인을 할 것인가요? #

Undeclared 변수는 이전에 var, let, const를 사용하여 `생성되지 않은 식별자에 값을 할당할 때` 생성됩니다.  
Undeclared 변수는 현재 `범위 외부에 전역`으로 정의됩니다.  

strict 모드에서는 Undeclared 변수에 할당하려고 할 때,  
`ReferenceError`가 발생합니다.  

Undeclared 변수는 전역 변수처럼 좋지 않습니다.  
이것들은 모두 사용을 피하세요!  
이를 검사하려면, 사용할 때 try/catch 블록에 감싸세요.

```javascript
function foo() {
  x = 1; // strict 모드에서 ReferenceError를 발생시킵니다.
}


foo();
console.log(x); // `1`
```

undefined 변수는 `선언되었지만,  
값이 할당되지 않은 변수`입니다.  
이는 undefined 타입입니다.

함수가 실행 결과에 따라 아무값도 반환하지 않으면,  
변수에 할당되며, 그 변수가 undefined 값을 갖습니다.  

이를 검사하기 위해, 엄격한 비교/일치 비교 (`===`) 연산자 또는 `typeof에 undefined 문자열`을 사용하여 비교하세요.  
확인을 위해 형변환 비교/동등 비교 연산자(`==`)를 사용해서는 안되며, 이는 값이 null이면 true를 반환하기 때문입니다.

```javascript
var foo;
console.log(foo); // undefined
console.log(foo === undefined); // true
console.log(typeof foo === 'undefined'); // true

console.log(foo == null); // true. 옳지않습니다. 이렇게 사용하지 마세요.

function bar() {}
var baz = bar();
console.log(baz); // undefined
```

null인 변수는 `null 값이 명시적으로 할당`된 것입니다.  
그것은 값을 나타내지 않으며,  
명시적으로 할당됐다는 점에서 **undefined와 다릅니다.**

null을 체크하기 위해서 단순히 일치 비교 연산자(`===`)를 사용하여 비교하면 됩니다.  
위와 같이, 동등 비교 연산자 (`==`)를 사용해서는 안되며, 값이 undefined이면 true를 반환합니다.

```javascript
var foo = null;
console.log(foo === null); // true

console.log(foo == undefined); // true. 옳지않습니다. 이렇게 사용하지 마세요.
```

개인적 습관으로, 저는 **변수를 선언하지 않거나(undeclared) 할당하지 않은 상태(unassigned)로 두지 않습니다.**  

아직 사용하지 않으려는 경우, **선언한 후에 명시적으로 null을 할당할 것입니다.**  
작업시 **linter**를 사용하면, 일반적으로 Undeclared 변수를 참조하지는 않는지 확인할 수 있습니다.
