# `Function.prototype.bind`에 대해 설명하세요 #

[MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_objects/Function/bind)에서 인용:

<blockquote>
bind() 메소드는 호출될 때,<br/>주어진 첫번째 인자 값은 this에 할당되고,<br/>이어지는 인자들은 바인드된 함수의 인수에 제공되어<br/>새로 바인딩한 함수를 생성하는 함수입니다.
</blockquote>

저의 경험상, 다른 함수로 전달하고자 하는 클래스의 메소드에서 this의 값을 바인딩할 때 가장 유용합니다. 이는 React 클래스형 컴포넌트에서 자주 사용됩니다.
