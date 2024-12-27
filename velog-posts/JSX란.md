<h1 id="🏷️jsx란">🏷️JSX란?</h1>
<p>JavaScript를 줄여서 보통 JS라고 많이 표기한다. React도 사실 공식 명칭은 React JS이다.</p>
<p>JSX는 <code>A syntax extension to JavaScript</code> 라는 의미를 가지고 있다. 자바스크립트의 확장 문법이라는 뜻이다. </p>
<p>JSX는 자바스크립트와 XML, HTML을 합친 것이라고 볼 수 있다.</p>
<pre><code class="language-jsx">const element = &lt;h1&gt;hello&lt;/h1&gt;;</code></pre>
<p>위의 코드를 보면 대입 연산자로 오른쪽에 있는 값을 왼쪽에 있는 변수에 대입하고 있다. 여기까진 흔히 사용하는 자바스크립트 문법이다. 하지만 대입 연산자의 오른쪽에 HTML 코드가 있다.</p>
<p>이 코드는 자바스크립트 코드와 HTML 코드가 결합되어 있는 JSX 코드인 것이다. h1 태그로 둘러싸인 문자열을 element 변수에 저장하는 코드이다. </p>
<h1 id="🔍jsx의-역할">🔍JSX의 역할</h1>
<p>JSX는 내부적으로 XML, HTML 코드를 JavaScript로 변환하는 과정을 거치게 된다.</p>
<p>여기서 JSX 코드를 JavaScript 코드로 변환하는 역할을 하는 것이 React의 createElement라는 함수이다.</p>
<pre><code class="language-jsx">class Hello extends React.Component {
    render() {
        return &lt;div&gt;Hello {this.props.toWhat}&lt;/div&gt;;
    }
}

ReactDOM.render(
    &lt;Hello toWhat=&quot;World&quot; /&gt;,
    document.getElementById('root')
);</code></pre>
<p>위의 코드를 보면 Hello라는 이름의 React 컴포넌트 내부에서 JavaScript 코드와 HTML 코드가 결합된 JSX를 사용하고 있다. 이렇게 만들어진 컴포넌트를 ReactDOM의 render 함수를 사용해 렌더링하고 있다.</p>
<pre><code class="language-jsx">class Hello extends React.Component {
    render() {
        return React.createElement('div', null, `Hello ${this.props.toWhat}`);
    }
}

ReactDOM.render(
    React.createElement(Hello, {toWhat: &quot;World&quot;}, null),
    document.getElementById('root')
);</code></pre>
<p>반면에 위의 코드는 이전 코드와 동일한 역할을 하지만 JSX를 사용하지 않고 순수하게 JavaScript만을 사용해서 만든 코드이다.</p>
<p>두 코드를 비교해보면 Hello 컴포넌트 내부에서 JSX를 사용했던 부분이 React.createElement로 대체되었다.</p>
<p>결국 JSX 문법을 사용하면 React에서는 내부적으로 모두 createElement라는 함수를 사용하도록 변환하게 되는 것이다. 최종적으로는 createElement 함수를 호출한 결과로 JavaScript 객체가 나오게 된다.</p>
<ul>
<li><p>JSX를 사용한 코드</p>
<ul>
<li><pre><code class="language-jsx">const element = (
&lt;h1 className=&quot;greeting&quot;&gt;
    Hello, World!
&lt;/h1&gt;
)


</code></pre>
</li>
</ul>
</li>
</ul>
<ul>
<li><p>JSX를 사용하지 않은 코드</p>
<ul>
<li><pre><code class="language-jsx">const element = React.createElement(
'h1',
{className: 'greeting'},
'Hello, World!'
)

</code></pre>
</li>
</ul>
</li>
</ul>
<p>이 두 개의 코드는 동일한 역할을 한다. JSX를 사용한 코드도 내부적으로는 createElement 함수를 사용하도록 변환되기 때문이다. createElement 함수 호출의 결과로 아래와 같은 JavaScript 객체가 나오게 된다.</p>
<pre><code class="language-jsx">const element = {
    type: 'h1',
    props: {
        className: 'greeting',
        children: 'Hello, World!'
    }
}</code></pre>
<p>React는 이 객체들을 읽어서 DOM을 만드는데 사용하고 항상 최신 상태로 유지한다.
React에서는 이 객체를 element라고 부른다.</p>
<h3 id="📌createelement-함수의-파라미터">📌createElement 함수의 파라미터</h3>
<ul>
<li>createElement 함수의 파라미터로는 type, props, children이 있다.</li>
<li>type에는 HTML 태그가 올 수도 있고, 다른 React 컴포넌트가 들어갈 수도 있다.</li>
<li>props에는 속성들이 들어가며, children에는 현재 element가 포함하고 있는 자식 element들이 들어간다.</li>
</ul>
<p>이처럼 React는 JSX 코드를 모두 createElement 함수를 사용하도록 변환하기 때문에 JSX를 사용하지 않고 직접 createElement 함수를 사용해서 개발해도 된다. </p>
<p>하지만 JSX를 사용했을 때 코드가 간결해지고 생산성과 가독성이 올라가기 때문에 JSX를 사용하는 것을 권장한다.</p>