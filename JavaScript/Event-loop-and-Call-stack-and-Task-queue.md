# 이벤트 루프란 무엇인가요? 콜 스택과 태스크 큐의 차이점은 무엇인가요? #

이벤트 루프는 **콜 스택을 모니터링**하고 **태스크 큐에서 수행할 작업이 있는지 확인**하는 `싱글 스레드 루프`입니다. 콜 스택이 비어 있고 태스크 큐에 실행해야 할 콜백함수가 남아있는 경우, 함수는 큐에서 제거되고 실행될 콜스택으로 푸시됩니다.

[talk on the Event loop](https://2014.jsconf.eu/speakers/philip-roberts-what-the-heck-is-the-event-loop-anyway.html)  
