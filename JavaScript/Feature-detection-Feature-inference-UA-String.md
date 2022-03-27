# Feature detection, Feature inference, UA String의 차이점은 무엇인가요? #

## Feature Detection ##

Feature Detection은 브라우저가 특정 코드 블록을 지원하는지에 따라 다른 코드를 실행하도록 하여,  
일부 브라우저에서 항상 오류 대신 무언가 작동하도록 합니다.  

예:

```javascript
if ('geolocation' in navigator) {
  // navigator.geolocation를 사용할 수 있습니다
} else {
  // 부족한 기능 핸들링
}
```

Modernizr는 Feature detection을 처리 ​​할 수 있는 훌륭한 라이브러리입니다.

## Feature Inference ##

Feature inference는 Feature detection과 마찬가지로 기능을 확인하지만 다른 함수도 존재한다고 가정하고 사용합니다.  

예:

```javascript
if (document.getElementsByTagName) {
  element = document.getElementById(id);
}
```

이것은 권장하지 않습니다.  
이유는 다음과 같이 사용하는 feature를 체크하지 않아 불일치가 발생할 수 있기 때문입니다.
![image](https://user-images.githubusercontent.com/59217352/160279999-e7713910-e8af-4b99-a22e-cf923ec5714b.png)  
https://lucybain.com/blog/2014/feature-detection-vs-inference/


## UA String ##

네트워크 프로토콜 피어가 요청하는 소프트웨어 `유저 에이전트`의 `응용 프로그램 유형, 운영 체제, 소프트웨어 공급 업체 또는 소프트웨어 버전을 식별할 수 있도록 해주는 browser-reported String`입니다.  
navigator.userAgent 를 통해 접근 할 수 있습니다.  
하지만 문자열은 `구문 분석하기 까다로우며 스푸핑될 수 있습니다.`  
예를 들어, Chrome은 Chrome과 Safari로 모두 보고됩니다.  
Safari를 감지하기 위해서는 Safari 문자열이 있는지와 Chrome 문자열이 없는지 확인해야 합니다.  
이 방법은 사용하지 마세요.
