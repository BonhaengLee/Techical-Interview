# `.forEach` 루프와  `.map` 루프의 주요 차이점을 설명할 수 있나요?  어떤 루프를 언제 사용해야 할까요? #

이 두 함수의 차이점은 먼저 각 함수가 무엇을 하는지 알아야 합니다.

`forEach`

- 배열의 요소를 반복합니다.
- 각 요소에 대해 콜백을 실행합니다.
- 값을 반환하지 않습니다.  

```javascript
const a = [1, 2, 3];
const doubled = a.forEach((num, index) => {
  // 하고 싶은 것
});

// doubled = undefined : forEach는 값을 반환하지 않으므로..
```

`map`

- 배열의 요소를 반복합니다.
- 각 요소에서 함수를 호출하여 그 결과로 새 배열을 작성하며 `각 요소를 새 요소에 매핑`합니다.

```javascript
const a = [1, 2, 3];
const doubled = a.map((num) => {
  return num * 2;
});

// doubled = [2, 4, 6]
```

.forEach와 .map()의 가장 큰 차이점은 .map()이 새로운 배열을 반환한다는 것입니다.  

결과가 필요하지만 `원본 배열을 변경하고 싶지 않으면`, `.map`이 확실한 선택입니다.  
단순히 배열을 반복할 필요가 있다면, `.forEach`가 좋은 선택입니다.
