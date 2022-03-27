# `function Person() {}`, `var person = Person()`와 `var person = new Person()`의 차이를 알려주세요 #

function 키워드를 사용한 함수 선언문, 변수에 할당하는 함수 표현식 이 둘을 묶어서 뒤의 생성자 함수로 호출해 인스턴스를 변수에 담는 방식과의 차이를 말해달라는 질문으로 추측할 수 있습니다.  

`function Person(){}`은 함수 생성자로 사용하기 위해 함수이름에 PascalCase를 사용합니다.

`var person = Person()`은 생성자가 아니라 함수로 호출합니다.  
생성자로 사용할 때 이렇게 하는 건 일반적인 실수입니다.  
**일반적인 생성자는 아무것도 반환하지 않으므로 undefined**가 반환되어 변수에 할당됩니다.

`var person = new Person()`은 `new` 연산자를 사용하여 `Person.prototype`을 상속받은 `Person` 객체의 인스턴스를 생성합니다.  
또 다른 방법은 `Object.create(Person.prototype)`과 같이 `Object.create`를 사용하는 것입니다.  

```javascript
function Person(name) {
  this.name = name;
}

var person = Person('John');
console.log(person); // undefined
console.log(person.name); // Uncaught TypeError: Cannot read property 'name' of undefined

var person = new Person('John');
console.log(person); // Person { name: "John" }
console.log(person.name); // "john"
```
