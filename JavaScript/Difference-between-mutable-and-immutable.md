# Mutable 객체와 Immutable 객체의 차이점은 무엇인가요? #

## JavaScript에서 immutable 객체의 예는 무엇인가요? ##

Javascript의 원시 타입은 변경 불가능한 값이다.

- Boolean
- null
- undefined
- Number
- String
- Symbol

하지만 객체는 참조로 관리되는 변경 가능한 값이다.

## Immutability의 장점과 단점은 무엇인가요? ##

객체는 참조의 형태로 주고 받으므로 공유되는 동안 상태가 변경될 수 있다. 참조가 공유되는 다른 위치에서 영향을 받게 되는 것은 문제가 될 수 있어 이와 같은 의도치 않은 상태 변경을 방지해주는 것이 Immutability다.  
 또한, 복제나 비교에 대한 조작을 단순화할 수 있다.  

단점은 객체가 변경이 필요한 경우 객체를 방어적 복사(defensive copy)하여 새로운 객체를 생성한 다음 변경해야 하기 때문에 비용이 든다.  

## 자신의 코드에서 어떻게 immutability를 얻을 수 있나요? ##

1. 객체의 방어적 복사(defensive copy)  
`Object.assign`
2. 불변객체화를 통한 객체 변경 방지  
`Object.freeze`
