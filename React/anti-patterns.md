# 리액트 안티 패턴은 무엇인가요? #

## loops로 렌더링할 때 index를 key로 사용하는 것 ##

  유사한 컴포넌트의 목록을 렌더링할 때 **key는 React가 변경, 추가 또는 제거된 item을 식별하는 데 도움이 됩니다.**  
  배열 내부의 요소에 key를 부여하여 안정적인 ID를 제공해야 합니다.  
  그리고 대부분의 JS 개발자들은 안티패턴으로 간주될 수 있는 배열의 index를 key로 사용하는 경향이 있습니다.  

  item의 순서가 변경될 수 있는 경우 key에 index를 사용하지 않는 게 좋습니다. 이로 인해 `성능이 저하되고 컴포넌트의 state에 문제가 발생할 수 있습니다.`  

  렌더링할 item에 대한 안정적인 ID가 없는 경우 최후의 수단으로 item의 index를 key로 사용할 수 있습니다.

  [왜 안티패턴인지에 대한 설명한 포스트가 있습니다.](https://medium.com/@vraa/why-using-an-index-as-key-in-react-is-probably-a-bad-idea-7543de68b17c)

### Solution ###

  key는 `안정적이고 고유하고 예측 가능`해야 합니다.  
  index, random numbers or timestamps

## 컴포넌트 내 일정한 배치(class component) ##

상수를 정의할 때, 컴포넌트 내의 배치를 결정해야 합니다.  
대부분 개발자는 React에서 render 메서드 내에 상수 객체 리터럴과 배열을 정의하는 경향이 있습니다.  
이러한 접근 방식은 성능에 영향을 줄 수 있으며 대형 컴포넌트에서 지연(lag)이 나타날 수 있습니다.

```javascript
class App extends Component {
  render() {
    const styles = { width: "400px", height: "400px", position:  "relative" };
  }
}
```

### Solution ###

images, styles에 대한 상수들은 컴포넌트 밖에 배치한다.

```javascript
const styles = { width: "400px", height: "400px", position: "relative" };

class MyComponent extends React.component {}
```

또는 constructor 내에 배치한다.

```javascript
class MyComponent extends React.component {
  constructor(){
    this.styles = { width: "400px", height: "400px", position:
  }
}
```

## props에서 파생된 state 관리 ##

클래스형 컴포넌트에서 componentWillReceiveProps(to be deprecated) & getDerivedStateFromProps는 props의 변화에 대응하여 state를 업데이트하는 방법을 제공합니다.  

리액트 문서에 따르면, 위 두 메서드가 props가 변경될 때만 호출된다는 것입니다. 이러한 라이프사이클은 props가 이전과 다른지 여부와 상관 없이 상위 컴포넌트가 리렌더링될 때 언제든지 호출됩니다.  

이러한 이유로, 이 라이프사이클 중 하나를 사용하여 state를 무조건 재정의하는 것은 항상 안전하지 않습니다. ***state 업데이트가 안될 수 있습니다.***

```javascript
class EmailInput extends Component {
  state = { email: this.props.email };

  render() {
    return <input onChange={this.handleChange} value={this.state.email} />;
  }

  handleChange = event => {
    this.setState({ email: event.target.value });
  };

  componentWillReceiveProps(nextProps) {
    // This will erase any local state updates!
    // Do not do this.
    this.setState({ email: nextProps.email });
  }
}
```

### Solution ###

- single source를 유지하는 Redux 같은 상태 관리 라이브러리.  
- 단방향 데이터 흐름을 강조하는 데이터 다운 액션 업 방식을 쓸 수 있습니다.  
하위 컴포넌트는 데이터에 대한 읽기 전용 액세스 권한을 가지지만 데이터를 직접 수정할 수 없습니다.  
대신 하위 컴포넌트는 상위 컴포넌트의 데이터를 업데이트하는 데 사용할 수 있는 actions나 callbacks에 접근할 수 있습니다.  

## 공통 프로미스 안티 패턴 ##

자바스크립트의 promises와 async, await를 쓰는 개발자들은 애플리케이션에 혼란스러운 blogs를 도입하는 흔한 실수를 할 수 있습니다.

```javascript
loadSomething().then(function(something) {
    loadAnotherthing().then(function(another) {
                    DoSomethingOnThem(something, another);
    });
});
```

이것은 코드베이스를 리팩터링하는 것을 어렵게 만들고 중첩된 promises가 제대로 처리되지 않으면 버그가 생길 수도 있습니다.  
더 꺠끗한 방식은 `Promise.all`입니다.(or `Promise.allSettled`)

```javascript
promise.all([loadSomething(), loadAnotherThing()])
 .spread(function(something, another) {
 doSomethingOnThem(something, another);
});
```

또, `async`, `await`를 씁니다.

```javascript
const async myFunction(){
  const res1 = await dataFromApi()
  const res2 = await dataFromAnotherApi()  
  doSomething(res1) // blocked by dataFromAnotherApi which is wrong
}
```

이것은 response가 resolved될 때까지 코드의 실행을 차단합니다.  
따라서 변수가 resolved될 프로미스에 의존하지 않는 경우 위의 예와 같이 안티패턴입니다!

## setState 사용하는 것 ##

몇가지 번거로운 것이 있습니다. 
setState는 비동기입니다. 따라서 setState 내에서 state 자체를 사용해서는 안됩니다. 이 문제를 방지하기 위해 다음 구문을 사용할 수 있습니다.

```javascript
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}));
```

prevState는 state 콜백 함수를 설정하기 위해 전달된 인수에 지은 이름입니다. 이 값은 `리액트에 의해 setState가 트리거되기 전의 상태값`입니다.  

## useEffect에서 async 함수 사용하는 것 ##

```javascript
useEffect(async () => {
    try {
        const response = await fetch(http://hn.algolia.com/api/v1');
        setData(response)
    } catch (e) {
        console.error(e);
    }
}, []);
```

MDN에 따르면, async 함수 선언은 비동기 함수를 정의하며, 비동기 함수 객체를 반환합니다.  
그러나 useEffect 훅은 아무것도 반환하지 않거나 clean up 함수를 반환해야 합니다.  
따라서 다음과 같은 경고가 표시됩니다.

```javascript
useEffect(() => {
   const fetchData = async () => {
   const result = await axios('https://hn.algolia.com/api/v1');
   setData(result.data);
};
  fetchData();
}, []);
```

## multiple useState hooks ##

```javascript
const [user, setUser] = useState('');
const [loading, setLoading] = useState(true);
const [error, setError] = useState('');
```

리액트 훅은 내부적으로 상태 내 객체에 대한 업데이트 처리 방식을 변경했기 때문에 항상 insetState와 같은 하나의 큰 useState 훅 대신 multiple useState 훅을 사용해야 합니다.  

`클래스형 컴포넌트에서 setState를 호출하면 새 값이 기존 state 객체에 병합`됩니다.  
값이 변경되지 않은 키가 있으면 해당 키의 기존 값을 바꿀 필요가 없습니다.  

그러나 `useState 훅을 사용하면 기본 값이 완전히 대채`됩니다.  
모든 상태 속성을 가진 객체가 있다면 **모든 업데이트에서 useState 훅으로 모든 상태를 대체**하는 것입니다.  
그래서 우리는 상태를 여러 훅으로 분할해야 합니다.  
리액트 엔진이 isolation 상태로 state를 대체하도록 말입니다. 

### 참고 ###

https://medium.com/@suraj.kc/react-anti-patterns-909ecf193701