<h1 id="🧩components">🧩Components</h1>
<p>React는 component 기반의 구조이다. 모든 페이지가 component로 구성되어있고, 하나의 component는 또 다른 여러 개의 component의 조합으로 구성될 수 있다.</p>
<p>하나의 component를 반복적으로 사용함으로써 전체 코드의 양을 줄일 수 있어서 자연스럽게 개발 시간과 유지보수 비용도 줄일 수 있다.</p>
<p>React component는 개념적으로는 JavaScript의 함수와 비슷하다. 함수가 입력을 받아서 출력을 내뱉는 것처럼 React component도 입력을 받아서 정해진 출력을 내뱉는다.</p>
<p>하지만 React component의 입력과 출력은 일반적인 JavaScript 함수와는 조금 다르다. React component에서의 입력은 props이고, 출력은 React element가 된다.</p>
<p>즉, React component가 해주는 역할은 어떠한 속성들을 입력으로 받아서 그에 맞는 React element를 생성해 리턴해주는 것이다. 만들고자 하는 대로 props를 넣으면 해당 속성에 맞춰 화면에 나타날 element를 만들어 주는 것이다.</p>
<h1 id="🧪props">🧪Props</h1>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/db281fc0-c058-4995-ac92-5fcc17a73779/image.png" /></p>
<p>props는 prop 뒤에 복수형을 나타내는 s를 붙인 것이다. prop은 속성을 의미하는 영어 단어 property를 줄여서 쓴 것이다.</p>
<p>즉, props는 React component의 속성들을 말한다. 같은 React component에서 눈에 보이는 글자나 색깔 등의 속성을 바꾸고 싶을 때 사용하는 component의 속 재료라고 생각하면 된다.</p>
<p>아래 이미지를 보면 모서리가 둥근 사각형 모양에 상단에는 그림, 하단에는 색깔 배경과 글자가 들어간 형태로 모두 동일한 형태이다.</p>
<p>하지만 안에 들어있는 그림과 색상, 글자는 모두 다르다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/a9dccb60-4035-490d-95d0-ff051e03cc98/image.png" /></p>
<p>React component의 관점에서 보면 4가지 모두 다 같은 component에서 생성된 element라고 할 수 있다. 각자 다른 이미지와 텍스트를 가지고 있는 것은 props를 다르게 전달했기 때문이다.</p>
<p>이렇게 component의 모습과 속성을 결정하는 것이 props이다. props는 component에 전달할 다양한 정보를 담고 있는 JavaScript 객체이다.</p>
<p>component에 전달된 데이터에 따라 다른 모습의 element를 화면에 렌더링하고 싶을 때 해당 데이터를 props에 넣어서 전달하는 것이다.</p>