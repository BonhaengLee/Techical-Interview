# UI Components #

예제

- Image carousel
- Selector which loads options over the network

## Framework ##

개요에서 말한 RADAD를 가지고 대화를 주도해야 합니다.  

## 요구 사항 설명 ##

모든 시스템 설계 인터뷰는 질문에 대한 요구 사항을 수집하고 명확히 해야 합니다. 거기에 적어도 몇 분을 소비하는 것이 좋습니다. 명확하게 하기 전에 아키텍쳐를 그리지 마세요.

고맙게도 컴포넌트는 잘 정의된 범위를 가지고 있으며 너무 많은 일을 하려고 하지 않습니다.  
당신은 이미 이러한 컴포넌트를 사용했을 것이고 이러한 컴포넌트에 필요한 요소가 무엇인지 알고 있을 수 있습니다.

몇 가지 고려 사항 :

- 시스템에서 **지원해야 하는 장치**는 무엇입니까? 데스크톱 웹, 모바일 웹 등
- 사용자가 시스템에 **액세스하는 기본 장치**는 무엇입니까?
- **어떤 브라우저를 지원**해야합니까?
- **국제화**를 지원해야 합니까?
- **얼마나 많은 스타일 사용자 정의를 허용**하고 싶습니까?

## Architecture ##

일반적으로 데이터베이스, load balancers 및 서버가 관련된 대규모 분산 시스템이 아닌 클라이언트 측 아키텍처에 중점을 둡니다.

컴포넌트의 경우 컴포넌트 내에 존재할 다양한 하위 컴포넌트와 각 컴포넌트 간에 전달되는 데이터를 나열합니다.
이미지 캐러셀의 예를 들어보겠습니다. 하위 컴포넌트는 아래와 같습니다.  

- Main image(기본 이미지) - 포커스가 있는 사진을 표시하는 이미지
- Thumbnail(썸네일) - 작은 이미지
- Image store - A client side cache of the list of photos to display  

사용자 상호 작용이 발생할 때 어떤 하위 컴포넌트와 통신하는지 **엔터티와 해당 관계를 설명하기 위해 다이어그램을 그리는 것**도 도움이 됩니다.

## Data Model ##

컴포넌트의 데이터 모델은 컴포넌트의 상태를 나타냅니다. state 개념은 프론트엔드 개발자에게는 익숙해야 합니다.  
어떤 데이터를 상태로 둘 것인지 결정하는 것은 잘 사용하기 위해 필수적입니다. 이를 결정하기 위해 고려해야 할 몇 가지 요소는 아래와 같습니다.  

- 상태는 컴포넌트의 라이프 사이클 동안 변경될 수 있고 일반적으로 유저 인터랙션의 결과입니다.  
- 각 컴포넌트는 컴포넌트의 여러 인스턴스가 단일 페이지에 `공존 할 수 있도록 자체 독립 상태를 유지`해야합니다. 컴포넌트 인스턴스의 상태는 `다른 인스턴스의 상태에 영향을 주지 않아야` 합니다.
- `State가 있는 영역이 적을수록 추론(이해)하기 쉽습니다.` 우리는 필요한 State의 양을 줄이기 위해 노력해야 합니다. 다른 State에서 파생될 수 있는 값(arr.length - isEmpty)이면 State가 아닐 가능성이 높습니다.
- 컴포넌트에 여러 하위 컴포넌트가 있는 경우 최상위 수준에서 State를 통합할 수 있고 나머지 컴포넌트가 `pure and stateless`인 것이 가장 좋습니다.  

## API Design #

`to be reused and abstract complexities` 하는 것이 컴포넌트의 핵심 아이디어입니다.
좋은 컴포넌트는 여러 시나리오에서 사용할 수 있고, 사용 시 내부적으로 어떻게 작동하는지 알 필요가 없습니다. 컴포넌트 API는 컴포넌트 개발자가 다른 개발자에게 지정하도록 노출하는 `configuration options`을 나타냅니다.

- 허용하는 Config options는 무엇입니까?(**props** in React)  
**Reasonable Defaults**는 무엇입니까?
- Follow the `Open-closed principle` - the component should be open for extension but closed for modification  
- 컴포넌트가 모양에 대해 신경쓰지 않고 유저에게 스타일링을 남겨두는 UI 라이브러리의 일부인 경우 props design에 각별히 주의를 기울여 사용자 정의할 수 있도록 해야 합니다.
React에서 해결 방법은 아래와 같습니다.  
  - `Composition` - Props which accept React components which also promotes code reuse.
  - `render props`는 컴포넌트가 렌더링할 내용을 알기 위해 사용하는 함수 props입니다. 모양을 신경쓰지 않고 행동을 재사용할 수 있게 됩니다.
  - `className or style props`를 사용자가 DOM 요소에 삽입할 수 있으면 부정적인 결과를 초래할 수 있지만 여전히 일반적인 방법입니다.  
- Possible configuration options:
  - `Lifecycle/event hooks` - onClick, onChange, onBlur, onFocus, etc.

## Deep dives​ ##

다루는 컴포넌트의 기본 사항을 통해 특별한 주의를 필요로 할 특정 영역에 다이브할 수 있습니다.  

이러한 분야에 지식을 보여주고 깊이 파고들 수 있다는 것은 수석 프론트엔드 엔지니어의 특성입니다.  

### 사용자 환경(UX) ###

UI는 엔지니어링에 크게 속하지 않을 수도 있지만 훌륭한 프론트 엔지니어는 훌륭한 UX로 UI를 구축합니다. 아래는 the most common ones/low hanging fruits입니다.

- 사용자에게 컴포넌트의 상태를 reflect합니다. - 만약 pending(보류)인 백그라운드 요청이 있다면 로딩 스피너를 표시합니다. 만약 오류가 있다면 조용히 실패하는 것이 아니라 오류를 표시해야 합니다.  
- 아무것도 렌더링하지 않는 대신 빈 상태를 표시합니다.  
- Destructive actions should have a confirmation step, especially irreversible ones. `파괴적인 행동에 확인 단계`가 필요합니다. 특히 돌이킬 수 없는 단계에서
- `async request를 트리거하는 것들이라면 상호작용을 한 요소를 disable`합니다. Prevents double firing of events in the case of accidental double clicking (possible for people with motor disabilities).  
- 만약 search input이 있다면 각 keystroke가 네트워크 요청을 발생시키지 않아야 합니다.
- Handle extreme cases
  - 문자열을 정말 길거나 짧을 수 있는데, 둘다 UI가 이상해서는 안됩니다. 너무 길면 더보기 버튼 뒤로 숨길 수 있습니다.
  - 컴포넌트에 표시할 항목이 매우 많은 경우 한 번에 모두 표시하고 페이지를 매우 길게 만들면 안됩니다. 페이지를 매기거나 max width/height의 컨테이너에 포함시킵니다.
- `Keyboard friendliness`
  - 키보드 전용 사용자를 위한 **Add shortcuts**
  - 컴포넌트에 **focus할 수 있고 tab 순서**가 올바른지 확인합니다.
- `Accessibility is part of UX` - 다음 섹션

### Performance​ ###

In front end, performance typically refers to a few things - loading speed(`로딩 속도`), how fast the UI responds to user interactions(`UI가 사용자 인터랙션에 반응하는 속도`), memory space (heap)(`컴포넌트에 필요한 메모리 공간`) required by the component.

- 로딩 속도 : 컴포넌트에 포함된 JS가 적을수록 브라우저가 로드하기 위해 `다운 받을 JS가 줄어들고 네트워크 요청 시간이 줄어듭니다.` `컴포넌트를 모듈화해서 유즈케이스에 필요한 JS 모듈만 다운로드`하게 하는 것이 중요합니다.  
- 사용자 인터랙션에 대한 응답성 :  
  - `인터랙션을 통해서 로드`되어야 할 데이터가 표시되는 경우에 인터랙션과 UI 업데이트 사이에 `딜레이가 발생`합니다. 이 지연을 최소화하거나 제거하는 것이 응답성 향상의 열쇠입니다.  
  - 브라우저의 JS는 단일 스레드입니다 한 번에 한 줄만 수행할 수 있으므로 페이지에서 작업을 수행할 때 컴포넌트의 `수행할 작업(JS 실행, DOM 업데이트)가 적을 수록 변경 사항에 응답하는 속도가 빨라집니다.`  
- 메모리 공간 : 컴포넌트가 `차지하는 메모리 공간이 많을수록` 브라우저 수행 속도가 느려지고 환경이 느리고 Janky(`저품질`/구리다)하게 느껴집니다. 컴포넌트가 수백 수천 개의 항목을 렌더링해야 하는 경우 중요한 고려 사항입니다. (e.g. number of images in a carousel, number of items in a selector)

### Optimization tips ###

- 화면에 표시되는 내용만 렌더링 : For example, in a selector, only a few items are displayed to the user even if the list can contain hundreds of elements. 모든 것을 렌더링하는 것은 처리 능력과 메모리 공간 낭비입니다. 우리는 윈도우/가상화 기술을 사용해 많은 요소가 있는 목록을 에뮬레이트하는 동시에 가능한 몇 개만 렌더링해서 최적화되지 않은 것처럼 보여줄 수 있습니다.(특히 스크롤 높이 유지) [Read more about virtualization here](https://web.dev/virtualize-long-lists-react-window/)
- Lazy loading/load only necessary data : 사진이 많은 갤러리 요소를 전부 로드할 필요 없습니다. 대부분의 유저는 해당 세션에서 모든 항목을 탐색하지 않을 가능성이 높습니다. `최적화는 사용자가 볼 가능성이 있거나 뷰포트 내에 있는 것만 로드`하는 것입니다. 나머지 사진은 필요에 따라 로드합니다. 다음 팁이 도움될 겁니다.
- Preloading/prefetching data ahead of time : 이미지 캐러셀에서 현재 이미지 다음으로 N개의 이미지를 로드해두어 네트워크 지연이 발생하지 않습니다.

### 접근성(a11y) ###

이것은 `가능한 한 많은 사람들`이 웹 사이트를 사용할 수 있게 하는 관행입니다.

- `색상 대비`(예: 색맹)
- `키보드 친화성`(예: 미세 모터 제어가 제한된 사람)
- `시각 장애`(예: 시각 장애인)
- `오디오 성적 증명서`(예: 청각 장애인)

모든 사람이 같은 방식으로 웹 서핑을하는 것은 아닙니다. 어떤 사람들은 스크린 리더와 키보드를 독점적으로 사용합니다.  
다음은 UI 컴포넌트에서 a11y를 달성하기 위한 몇 가지 기본 팁입니다.

- Foreground 색상은 배경색과 충분한 대비를 가져야합니다.
- 의미성에 적합한 HTML 태그 또는 올바른 aria-role 속성 사용
- 클릭 가능한 항목에는 `tabindex` 속성 (**초점이 맞춰지도록**)과 클릭할 수 있음을 나타내는 "cursor: pointer" 스타일이 있어야합니다.
- 이미지에는 alt 텍스트가 있어야 하며, 이 텍스트는 스크린 리더에서 읽게 되며 이미지가 로드되지 않을 경우 대체 설명 역할을 합니다.
- `aria-labels`는 비시각적 사용자에게 `명확하지 않은 요소에 대한 컨텍스트를 제공하는 데 도움이 됩니다.` 예를 들어 **텍스트 레이블이 없는 아이콘 버튼**에는 아이콘을 볼 수 없는 사용자에게 `의도가 명확하도록 aria-label 속성`이 있어야합니다.

a11y는 개발자에게 보이지 않는 대부분의 시간 동안 가장 일반적으로 무시되는 영역 중 하나입니다. a11y에 대한 지식을 보여주고 접근 가능한 구성 요소를 만드는 기술을 보유하는 것은 확실히 당신에게 잘 반영 될 것입니다. [More reading on Web Accessibility](https://www.w3.org/WAI/fundamentals/accessibility-intro/)

### Internationalization (i18n)​ ###

문화, 지역 또는 언어에 따라 다양한 대상 고객을 위해 쉽게 현지화할 수 있는 제품, 응용 프로그램 또는 문서 컨텐츠의 설계 및 개발입니다. 일반적인 컴포넌트는 아래의 특정한 상황만 신경쓰면 됩니다.

- 컴포넌트 문자열 사용 : 특정 언어로 하드 코딩되면 안됩니다. (e.g. "Prev" / "Next") 문자열은 `영어 버전을 기본으로 하여 props으로 지정`할 수 있습니다.  
- Order of content matters : upport RTL (right to left) languages like Arabic and Hebrew?(`RTL을 지원하는지`)

### Multi-device support​ ###

컴포넌트가 모바일 웹에서 사용될 것 같습니까? 모바일 장치는 고유한 제약이 있습니다.(HW가 덜 강력하고 뷰포트가 작습니다.) 아래의 노력을 해봅시다.

- `너무 많은 메모리를 쓰지 않음` : 장치 성능을 위해
- 상호작용할 요소의 hit box 늘리기 : 손가락으로 올바른 요소를 누를 수 있도록

### Security​ ###

다음이 알아야 할 일반적인 보안 취약점입니다.  

- XSS : 컴포넌트가 XSS(Cross-site Scripting)에 취약합니까? `.innerHTML` 또는 `dangerouslySetInnerHTML`를 통해 사용자 입력을 렌더링합니까?
- CSRF(Cross-site Request Forgery)
- Clickjacking
- [rel=noopener](https://mathiasbynens.github.io/rel-noopener/)
