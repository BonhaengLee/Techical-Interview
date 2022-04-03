# Promises와 그 Polyfill에 대한 당신의 경험은 어느 정도인가요? #

Promises는 어느 시점에 resolve된 값 또는 resolve되지 않은 이유(예: 네트워크 오류가 발생) 중 하나의 값을 생성할 수 있는 객체입니다.  
promise는 fulfilled, rejected, pending 3가지 상태 중 하나가 될 수 있습니다.  
promise는 콜백을 붙여서 fulfill된 값이나 reject된 이유를 처리할 수 있습니다.  

일반적인 polyfill은 `$.deferred`, Q, Bluebird이지만 모두 스펙을 따르는 것은 아닙니다.  
ES2015는 즉시 사용할 수 있는 Promise를 지원하며 대부분 polyfill이 필요하지 않습니다.(폴리필을 사용하지 않습니다.)
