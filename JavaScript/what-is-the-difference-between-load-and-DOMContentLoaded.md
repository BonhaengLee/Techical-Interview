# document `load` 이벤트와 document `DOMContentLoaded` 이벤트의 차이점은 무엇인가요? #

`DOMContentLoaded` 이벤트는 **스타일시트, 이미지, 서브프레임 로딩을 기다리지 않고**, 초기 HTML 문서가 완전히 로드되고 파싱되면 발생합니다.

`window`의 `load` 이벤트는 **DOM**과 모든 종속 리소스의 **assets**가 로딩된 후에 발생합니다.
