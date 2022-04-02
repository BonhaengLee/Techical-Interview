# event bubbling에 대해 설명하세요 #

DOM 요소에서 이벤트가 트리거되면 **리스너가 연결되어 있는 경우 이벤트 처리를 시도**한 다음, 해당 이벤트가 부모에게 bubbling 되고 **부모에서 같은 이벤트가 발생**합니다.  

이 bubbling은 요소의 **최상단 부모 요소**인 `document`까지 계속적으로 발생시킵니다.  
event bubbling은 event delegation의 작동 메커니즘입니다.
