# React hooks의 인기 있는 패턴과 안티 패턴 #

## 모든 표준 규칙 적용 ##

1. `단일 책임 원칙` : 하나의 훅은 하나의 기능을 캡슐화해야 합니다. 단일 슈퍼 훅을 만드는 대신 여러 개의 작고 독립적인 것으로 분할하는 것이 좋습니다.  
2. `명확하게 정의된 API` : 일반 함수/메서드와 유사하게 훅이 너무 많은 인수를 취하면 이 훅이 더 잘 캡슐화되게 하기 위해서 리팩터링이 필요하다는 신호입니다. 마찬가지로 너무 많은 props를 가진 컴포넌트를 피하라는 권장 사항이 있었습니다. 또한 최소한의 인수도 가져야 합니다.  
3. `예측 가능한 동작` : 훅의 이름은 기능과 일치해야 하며 예기치 않은 추가 동작이 없어야 합니다.  

## 훅 의존성 다루기 ##

몇몇 훅은 "dependencies"의 개념을 도입하는데, 이것은 `훅을 업데이트하게 하는 것들의 목록`입니다.  
대부분 useEffect이지만 useMemo, useCallback에서도 볼 수 있습니다.  
코드의 dependencies 배열을 관리하는 데 도움이 되는 ESLint 규칙이 있지만, **이 규칙은 코드의 구조만 확인할 수 있고 사용자의 의도는 확인할 수 없습니다.**  
훅의 dependency를 관리하는 것은 가장 까다로운 개념이며 개발자의 많은 관심이 필요합니다. 코드를 더 읽기 쉽고 유지 관리하기 쉽게 하기 위해 훅의 dependency 수를 줄일 수 있습니다.  

간단한 속임수로 훅 기반 코드가 더 쉬워질 수 있습니다.  

```javascript
function Demo({ options }) {
  const [ref, handleKeyDown] = useFocusMove({
    isInteractive: (option) => !option.disabled,
  });
  return (
    <ul onKeyDown={handleKeyDown}>
      {options.map((option) => (
        <Option key={option.id} option={option} />
      ))}
    </ul>
  );
}
```

이 커스텀 훅은 isInteractive에 dependency를 갖고, 훅 구현 내부에서 사용할 수 있습니다.  

```javascript
function useFocusMove({ isInteractive }) {
  const [activeItem, setActiveItem] = useState();

  useEffect(() => {
    if (isInteractive(activeItem)) {
      focusItem(activeItem);
    }
    // update focus whenever active item changes
  }, [activeItem, isInteractive]);

  // ...other implementation details...
}
```

커스텀 훅이 사용되는 위치와 이 인수가 변경되는지 여부를 알 수 없기 때문에 ESLint 규칙은 useEffect dependency를 사용하려면 isInteractive 인수를 추가해야 합니다.  
그러나, 개발자로서 우리는 이 함수를 정의하면 항상 동일한 구현이 이뤄지며 dependency 배열에 추가하는 것은 코드만 흐트러뜨린다는 것을 압니다.  

표준 `factory function` 패턴은 다음과 같습니다. 

```javascript
function createFocusMove({ isInteractive }) {
  return function useFocusMove() {
    const [activeItem, setActiveItem] = useState();

    useEffect(() => {
      if (isInteractive(activeItem)) {
        focusItem(activeItem);
      }
    }, [activeItem]); // no ESLint rule violation here :)

    // ...other implementation details...
  };
}

// usage
const useFocusMove = createFocusMove({
  isInteractive: (option) => !option.disabled,
});
function Demo({ options }) {
  const [ref, handleKeyDown] = useFocusMove();
  // ...other code unchanged...
}
```

여기서 트릭은 런타임 매개변수와 개발 시 매개변수를 분리하는 것입니다.  
컴포넌트 라이프타임 동안 변경 사항이 있으면 런타임 dependency이며 dependency 배열에 이동합니다.  
컴포넌트에 대해 `한번 결정된 후 런타임에 변경되지 않는 경우 factory function pattern을 사용`해보고 훅 dependency 관리를 더 쉽게 하는 것이 좋습니다. 

## useEffect 리팩터링 ##

useEffect는 React 구성 요소 내부의 명령적 DOM 상호 작용을 위한 장소를 제공합니다. 때로는 매우 복잡해져서 종속성 배열을 더하면 코드를 읽고 유지하기가 더 어려워질 수 있습니다.  
이는 후크 코드 외부에서 명령형 DOM 로직을 추출함으로써 해결할 수 있습니다.  

예를 들어, TooltipPlacement를 사용하는 후크를 생각해 보십시오.

```javascript
function useTooltipPosition(placement) {
  const tooltipRef = useRef();
  const triggerRef = useRef();
  useEffect(() => {
    if (placement === "left") {
      const triggerPos = triggerRef.current.getBoundingElementRect();
      const tooltipPos = tooltipPos.current.getBoundingElementRect();
      Object.assign(tooltipRef.current.style, {
        top: triggerPos.top,
        left: triggerPos.left - tooltipPos.width,
      });
    } else {
      // ... and so on of other placements ...
    }
  }, [tooltipRef, triggerRef, placement]);
  return [tooltipRef, triggerRef];
}
```

훅 내부 코드가 매우 길고 dependency가 제대로 사용되고 있는지 추적하기 어렵습니다.  
우리는 effect content를 별도의 함수로 분리할 수 있습니다.

```javascript
// here is the pure DOM-related logic
function applyPlacement(tooltipEl, triggerEl, placement) {
  if (placement === "left") {
    const triggerPos = tooltipEl.getBoundingElementRect();
    const tooltipPos = triggerEl.getBoundingElementRect();
    Object.assign(tooltipEl.style, {
      top: triggerPos.top,
      left: triggerPos.left - tooltipPos.width,
    });
  } else {
    // ... and so on of other placements ...
  }
}

// here is the hook binding
function useTooltipPosition(placement) {
  const tooltipRef = useRef();
  const triggerRef = useRef();
  useEffect(() => {
    applyPlacement(tooltipRef.current, triggerRef.current, placement);
  }, [tooltipRef, triggerRef, placement]);
  return [tooltipRef, triggerRef];
}
```

추가적으로 리액트 외부에서 사용 및 테스트할 수 있는 위치한 순수한 DOM 구현도 얻었습니다.  

## useMemo, useCallback과 조기 최적화(premature optimisations) ##

<blockquote>
You may rely on useMemo as a performance optimisation
</blockquote>

어떤 이유에서인지 개발자들은 이 부분을 "You may"가 아닌 "You must"로 읽고 모든 것을 메모화하려고 합니다. 이것은 얼핏 보기에 좋은 생각처럼 들릴 수도 있지만, 세부 사항에 관한 한 더 까다로워 보입니다.

메모화의 이점을 활용하려면 React.memo 또는 PureComponent 래퍼를 사용하여 구성 요소가 원하지 않는 업데이트를 방지해야 합니다.  
또한 매우 세밀한 조정과 검증이 필요하므로 필요한 것보다 더 자주 속성을 변경할 필요가 없습니다.  
모든 잘못된 속성은 카드 하우스처럼 모든 메모화를 깨뜨릴 수 있습니다.

이제 YAGNI 접근 방식을 떠올리고 앱의 가장 인기 있는 일부 장소에서만 메모 작업을 집중하기 좋은 시기입니다.  
`코드의 나머지 부분에서는 useMemo/useCallback으로 더 이상의 복잡성을 추가할 가치가 없다.` 일반 함수를 사용하여 보다 단순하고 읽기 쉬운 코드를 작성하고 나중에 그 `이점이 더 명확해지면 메모화 패턴을 적용`할 수 있습니다.

메모화의 길을 가기 전에 메모화의 대안을 찾을 수 있는 ["Before You memo()"](https://overreacted.io/before-you-memo/)라는 글도 확인해보라고 권할 수 있다.

## 다른 리액트 API는 여전히 존재 ##

<blockquote>

If you have a hammer, everything looks like a nail

</blockquote>

훅 도입으로 몇몇 리액트 패턴을 쓸모 없어졌습니다.  
예를 들어 useContext 훅을 쓰면 Consumer 컴포넌트보다 편리해보였습니다.  

그러나 다른 React features는 여전히 있고 잊어서는 안됩니다.  
예를 들어 다음의 코드를 봅시다. 

```javascript
function useFocusMove() {
  const ref = useRef();
  useEffect(() => {
    function handleKeyDown(event) {
      // actual implementation is extracted outside as shown in learning #3 above
      moveFocus(ref.current, event.keyCode);
    }
    ref.current.addEventListener("keydown", handleKeyDown);
    return () => ref.current.removeEventListener("keydown", handleKeyDown);
  }, []);
  return ref;
}

// usage
function Demo() {
  const ref = useFocusMove();
  return <ul ref={ref} />;
}
```

적합해 보이지만, 실제 이벤트 구독(subscription)을 수동으로 하지 않고 리액트에 위임(delegation)하지 않는 이유는 무엇입니까?

다음은 대체 버전입니다.  

```javascript
function useFocusMove() {
  const ref = useRef();
  function handleKeyDown(event) {
    // actual implementation is extracted outside as shown in learning #3 above
    moveFocus(ref.current, event.keyCode);
  }
  return [ref, handleKeyDown];
}

// usage
function Demo() {
  const [ref, handleKeyDown] = useFocusMove();
  return <ul ref={ref} onKeyDown={handleKeyDown} />;
}
```

새로운 훅 구현은 더 짧고 훅의 consumer가 더 복잡한 UI일 경우 listener를 부착할 위치를 결정할 수 있다는 장점이 있습니다.  

이것은 하나의 예이며 다른 시나리오가 있을 수 있습니다. 즉, 많은 리액트 패턴(high-order components, render props 등등)이 존재하며 의미가 있습니다.  

모든 학습은 한 가지 기본적인 측면입니다. 코드를 짧고 읽기 쉽게 유지하는 것입니다. 나중에 확장 및 리팩터링할 수 있습니다.  

### 참고 

https://dev.to/justboris/popular-patterns-and-anti-patterns-with-react-hooks-4da2