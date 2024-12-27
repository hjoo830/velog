<h1 id="🧩component-만들기">🧩Component 만들기</h1>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/afe615f6-6c88-4f38-97eb-c32c4c1d8699/image.png" /></p>
<p>React에서 component는 위와 같이 크게 클래스 컴포넌트와 함수 컴포넌트로 나뉜다.
React 초기 버전에서는 클래스 컴포넌트를 주로 사용하다가 사용하기 불편하다는 의견이 많이 나왔고, 이후 함수 컴포넌트를 개선해서 주로 사용하게 되었다. 함수 컴포넌트를 개선하는 과정에서 개발된 것이 Hook이다.</p>
<h2 id="🪄함수-컴포넌트">🪄함수 컴포넌트</h2>
<p>이전 포스팅에서 모든 React component는 pure 함수 같은 역할을 해야한다고 했다. 이 말은 결국 React component를 일종의 함수라고 생각한다는 뜻이다. </p>
<pre><code>function Welcome(props) {
    return &lt;h1&gt;안녕, {props.name}&lt;/h1&gt;;
}</code></pre><p>위의 함수의 경우 하나의 props 객체를 받아서 인사말이 담긴 React element를 리턴하기 때문에 React component라고 할 수 있다. 이렇게 생긴 것을 함수 컴포넌트라고 부른다. 함수 컴포넌트는 간단한 코드를 장점으로 가진다.</p>
<h2 id="🏛️클래스-컴포넌트">🏛️클래스 컴포넌트</h2>
<p>클래스 컴포넌트는 JavaScript ES6의 Class라는 것을 사용해서 만들어진 형태의 컴포넌트이다.
클래스 컴포넌트의 경우 함수 컴포넌트에 비해 몇가지 추가적인 기능을 가지고 있다.</p>
<pre><code>class Welcome extends React.Component {
    render() {
        return &lt;h1&gt;안녕, {this.props.name}&lt;/h1&gt;;
    }
}</code></pre><p>이 코드는 위의 함수 컴포넌트 Welcome과 동일한 역할을 하는 컴포넌트를 클래스 형태로 만든 것이다. 함수 컴포넌트와 가장 큰 차이점은 React의 모든 클래스 컴포넌트는 React.Component를 상속받아서 만든다는 것이다. React.Component라는 클래스를 상속받아서 Welcome이라는 클래스를 만들었기 때문에 결과적으로 React component가 되는 것이다.</p>
<h1 id="📝component-이름-짓기">📝Component 이름 짓기</h1>
<p>component의 이름을 지을 때 한가지 유의해야할 중요한 점이 있다. </p>
<blockquote>
<p><strong>component의 이름은 항상 대문자로 시작해야 한다.</strong></p>
</blockquote>
<p>React는 소문자로 시작하는 컴포넌트를 DOM 태그로 인식하기 때문이다. 
div나 span과 같이 사용하는 것은 내장 컴포넌트라는 것을 뜻하며, div나 span과 같은 문자열 형태로 React.createElement에 전달된다.
하지만 Foo와 같이 대문자로 시작하는 경우에는 React.createElement Foo 형태로 컴파일되며, JavaScript 파일 내에서 사용자가 정의했거나 import 한 component를 가리킨다. 그렇기 때문에 component의 이름은 항상 대문자로 시작해야 한다.</p>
<h1 id="🎨component-렌더링">🎨Component 렌더링</h1>
<p>렌더링을 하기 위해서는 가장 먼저 component로부터 element를 만들어야 한다.</p>
<pre><code>const element = &lt;div /&gt;; // DOM 태그를 사용한 element</code></pre><pre><code>const element = &lt;Welcome name=&quot;hjoo830&quot; /&gt;; // 사용자가 정의한 component를 사용한 element</code></pre><p>이 두 코드는 모두 React element를 만들어낸다.
이제 이 element를 렌더링 하면 된다.</p>
<pre><code>function Welcome(props) {
    return &lt;h1&gt;안녕, {props.name}&lt;/h1&gt;;
}
const element = ‹Welcome name=&quot;hjoo830&quot; /&gt;;
ReactDOM.render(
    element,
    document.getElementById('root')
);</code></pre><p>위의 코드에서, 먼저 Welcome이라는 함수 컴포넌트를 선언한다. 
그리고 name=&quot;hjoo830&quot; 이라는 값을 가진 element를 파라미터로 해서 ReactDOM.render 함수를 호출한다.
이렇게 하면 React는 Welcome 컴포넌트에 name=&quot;hjoo830&quot;이라는 props를 넣어서 호출하고 그 결과로 React element가 생성된다. 
이렇게 생성된 element는 최종적으로  ReactDOM을 통해 실제 DOM에 업데이트되고, 브라우저를 통해 볼 수 있게 된다.</p>