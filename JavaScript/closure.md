# 클로저는 무엇이고, 어떻게/왜 사용하나요? #

클로저는 함수와 그 함수가 선언된 렉시컬 환경의 조합입니다.  
`렉시컬`은 렉시컬 범위 지정이 변수가 사용 가능한 위치를 결정하기 위해 소스코드 내에서 변수가 선언된 위치를 사용한다는 사실을 나타냅니다.  
클로저는 외부 함수가 반환된 후에도 외부 함수의 변수 범위 체인에 접근할 수 있는 함수입니다.  

## 어떻게 클로저를 사용합니까? ##

```javascript
function makeFunc() {
      var name = "Mozilla";
      function displayName() {
        alert(name);
      }
      return displayName;
    }

    var myFunc = makeFunc();
    //myFunc변수에 displayName을 리턴함
    //유효범위의 어휘적 환경을 유지
    myFunc();
    //리턴된 displayName 함수를 실행(name 변수에 접근)
```

이 코드는 바로 전의 예제와 완전히 동일한 결과가 실행된다.  
하지만 흥미로운 차이는 `displayName()` 함수가 실행되기 전에 `외부함수인 makeFunc()로부터 리턴`되어 myFunc 변수에 `저장`된다는 것이다.

---

하지만 위의 예시와 자바스크립트의 경우는 몇몇 프로그래밍 언어와 달리 함수 안의 지역변수들이 그 함수가 처리되는 동안만 유지되지 않는다!  

그 이유는 자바스크립트는 함수를 리턴하고, 리턴하는 함수가 클로저를 형성하기 때문이다.  

클로저는 함수와 함수가 선언된 어휘적 환경의 조합이다.  
이 환경은 클로저가 생성된 시점의 유효 범위 내에 있는 모든 지역 변수로 구성된다.  

첫 번째 예시의 경우, myFunc은 `makeFunc이 실행 될 때 생성된 displayName 함수의 인스턴스`에 대한 `참조`다.  
**displayName의 인스턴스는 변수 name 이 있는 어휘적 환경에 대한 참조를 유지**한다.  
이런 이유로 myFunc가 호출될 때 변수 name은 사용할 수 있는 상태로 남게 되고 "Mozilla" 가 alert 에 전달된다.

## 왜 클로저를 사용합니까? ##

- 클로저로 데이터 프라이버시 / private method를 모방할 수 있어, 일반적으로 [모듈 패턴](https://addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript)에 사용됩니다.
- [부분 적용 or currying](https://medium.com/javascript-scene/curry-or-partial-application-8150044c78b8#.l4b6l1i3x)

### 참고 ###

- <https://developer.mozilla.org/ko/docs/Web/JavaScript/Closures>
- <https://www.frontendinterviewhandbook.com/kr/javascript-questions/#%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EC%9C%84%EC%9E%84%EC%97%90-%EB%8C%80%ED%95%B4-%EC%84%A4%EB%AA%85%ED%95%98%EC%84%B8%EC%9A%94>
