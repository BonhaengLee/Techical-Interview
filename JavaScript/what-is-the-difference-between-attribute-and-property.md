# "attribute"와 "property"의 차이점은 무엇인가요? #

attribute는 HTML 마크업에 정의되지만 property는 DOM에 정의됩니다.  
차이점을 설명하기 위해 HTML에 다음 텍스트 필드가 있다고 가정해봅니다.  
`<input> type="text" value="Hello">`

```javascript
const input = document.querySelector('input');
console.log(input.getAttribute('value')); 
// Hello
console.log(input.value); 
// Hello
```

그러나 텍스트 필드에 "World!"를 추가하면 이렇게 될것입니다.

```javascript
console.log(input.getAttribute('value')); 
// Hello
console.log(input.value); 
// Hello World!
```
