<h1 id="📖jsx의-정의">📖JSX의 정의</h1>
<p>JSX는 흔히 개발자들이 알고 있는 XML과 유사한 내장형 구문이다. JSX가 포함된 구문을 아무런 처리 없이 그대로 실행하면 에러가 발생하며, 반드시 트랜스파일러를 거쳐야 비로소 자바스크립트 런타임이 이해할 수 있는 의미 있는 자바스크립트 코드로 변환된다. JSX의 설계 목적은 다양한 트랜스파일러에서 다양한 속성을 가진 트리 구조를 토큰화 해 ECMAScript로 변환하는데 초점을 두고 있다. </p>
<blockquote>
<p>요약하자면 JSX는 자바스크립트 내부에서 표현하기 까다로웠던 XML 스타일의 트리 구문을 작성하는 데 많은 도움을 주는 새로운 문법이라고 볼 수 있다.</p>
</blockquote>
<p>JSX는 기본적으로 <code>JSXElement</code>, <code>JSXAttributes</code>, <code>JSXChildren</code>, <code>JSXStrings</code>라는 4가지 컴포넌트를 기반으로 구성되어 있다.</p>
<hr />
<h2 id="jsxelement">JSXElement</h2>
<p>JSX를 구성하는 가장 기본 요소로, HTML의 element와 비슷한 역할을 한다. JSXElement가 되기 위해서는 다음과 같은 형태 중 하나여야 한다.</p>
<ul>
<li><code>JSXOpeningElement</code><ul>
<li>일반적으로 볼 수 있는 요소</li>
<li><code>JSXOpeningElement</code>로 시작했다면 후술할 <code>JSXClosingElement</code>가 동일한 요소로 같은 단계에서 선언되어 있어야 올바른 JSX 문법으로 간주된다.</li>
<li><code>&lt;JSXElemnt JSXAttributes(optional)&gt;</code></li>
</ul>
</li>
<li><code>JSXClosingElement</code><ul>
<li><code>JSXOpeningElement</code>가 종료됐음을 알리는 요소</li>
<li>반드시 <code>JSXOpeningElement</code>와 쌍으로 사용되어야 한다.</li>
<li><code>&lt;/JSXElemnt&gt;</code></li>
</ul>
</li>
<li><code>JSXSelfClosingElement</code><ul>
<li>요소가 시작되고 스스로 종료되는 형태</li>
<li>내부적으로 자식을 포함할 수 없다.</li>
<li><code>&lt;JSXElement JSXAttributes(optional) /&gt;</code></li>
</ul>
</li>
<li><code>JSXFragment</code><ul>
<li>아무런 요소가 없는 형태</li>
<li><code>JSXSelfClosingElement</code> 형태를 띨 수는 없다.</li>
<li><code>&lt;&gt;JSXChildren(optional)&lt;/&gt;</code></li>
</ul>
</li>
</ul>
<h3 id="jsxelementname">JSXElementName</h3>
<p><code>JSXElement</code>의 요소 이름으로 쓸 수 있는 것을 의미</p>
<ul>
<li><code>JSXIdentifier</code><ul>
<li>JSX 내부에서 사용할 수 있는 식별자</li>
</ul>
</li>
<li><code>JSXNamespacedName</code><ul>
<li><code>JSXIdentifier:JSXIdentifier</code>의 조합</li>
</ul>
</li>
<li><code>JSXMemberExpression</code><ul>
<li><code>JSXIdentifier.JSXIdentifier</code>의 조합</li>
</ul>
</li>
</ul>
<hr />
<h2 id="jsxattributes">JSXAttributes</h2>
<p><code>JSXElement</code>에 부여할 수 있는 속성을 의미한다.
모든 경우에서 필수값이 아니고, 존재하지 않아도 에러가 나지 않는다.</p>
<pre><code class="language-js">function Example() {
    return (
        &lt;Component attribute=&quot;hello&quot;&gt;&lt;/Component&gt;
        &lt;Component attribute=&lt;div&gt;hello&lt;/div&gt;&gt;&lt;/Component&gt;
    );
}</code></pre>
<hr />
<h2 id="jsxchildren">JSXChildren</h2>
<p><code>JSXElement</code>의 자식 값을 나타낸다.</p>
<h3 id="jsxchild">JSXChild</h3>
<p><code>JSXChildren</code>을 이루는 기본 단위
<code>JSXChildren</code>은 <code>JSXChild</code>를 0개 이상 가질 수 있다.</p>
<pre><code class="language-js">function Example() {
    return (
        &lt;&gt;{'{}'}&lt;/&gt;
        &lt;&gt;{(() =&gt; 'foo')()}&lt;/&gt;
    );
}</code></pre>
<hr />
<h2 id="jsxstrings">JSXStrings</h2>
<p>HTML에서 사용 가능한 모든 문자열은 JSXStrings에서도 사용 가능하다.
자바스크립트와는 한가지 중요한 차이점이 있다.</p>
<blockquote>
<p>\로 시작하는 이스케이프 문자 형태소 또한 제약없이 사용할 수 있다.</p>
</blockquote>
<p>\는 자바스크립트에서 특수문자를 처리할 때 사용되므로 제약사항이 있지만, HTML에서는 아무런 제약 없이 사용할 수 있다.</p>
<hr />
<h1 id="🔄jsx는-어떻게-자바스크립트에서-변환될까">🔄JSX는 어떻게 자바스크립트에서 변환될까?</h1>
<p><code>@babel/plugin-transform-react-jsx</code> 플러그인은 JSX 구문을 자바스크립트가 이해할 수 있는 형태로 변환한다.</p>
<ul>
<li>JSX 코드<pre><code class="language-js">const ComponentA = &lt;A required={true}&gt;Hello World&lt;/A&gt;
</code></pre>
</li>
</ul>
<p>const ComponentB = &lt;&gt;Hello World&lt;/&gt;</p>
<p>const ComponentC= (
    <div>
        <span>Hello World</span>
    </div>
)</p>
<pre><code>
- JSX 코드를 ```@babel/plugin-transform-react-jsx``` 로 변환한 결과
```js
'use strict’

var ComponentA =React.createElement(
 A, 
  {
    required: true,
  },
'Hello World',
)

var ComponentB = React.createElement(React.Fragment, null, ’Hello World’) 


var ComponentC = React.createElement(
      ’div’,
      null,
      React.createElement(’span’, null, ’Hello World'),
)</code></pre><ul>
<li>리액트 17, 바벨 7.9.0 이후 버전에서 추가된 자동 런타임으로 트랜스파일한 결과<pre><code class="language-js">'use strict’
</code></pre>
</li>
</ul>
<p>var _jsxRuntime = require (’custom-jsx-library/jsx-runtime')</p>
<p>var ComponentA = (0, _jsxRuntime.jsx)(A, 
{ 
  required: true,
  children : 'Hello World' ,
})</p>
<p>var ComponentB = (0, _jsxRuntime.jsx)(_jsxRuntime.Fragment, { 
  children : 'Hello World’,
})</p>
<p>var ComponentC = (0, _jsxRuntime.jsx)('div’, {<br />  children: (0, _jsxRuntime.jsx)(’span’, {
    children: ’Hello World’ 
  }),
})</p>
<pre><code>
JSX 반환값이 결국 React.createElement로 귀결된다는 사실을 활용해 리팩터링할 수 있다.

# 📝정리
## JSX 문법에는 있지만 리액트에서 사용하지 않는 것
- JSXNamespacedName
- JSXMemberExpression

## JSX와 React.createElement의 효율적 사용
JSX는 대부분의 경우 편리하고 간결하게 컴포넌트를 작성하는데 많은 도움을 주지만, 때에 따라서는 직접 createElement를 사용해 컴포넌트를 구성하는 편이 더 효율적일 수 있다.

# 🔍더 알아보기
## JSX와 HTML의 차이점

JSX는 HTML과 아주 유사한 문법을 사용하지만 몇 가지 중요한 차이점이 존재한다. 이러한 차이점은 JSX가 자바스크립트로 변환되는 과정에서 발생하며, React에서 컴포넌트를 효율적으로 작성하기 위한 특수한 규칙을 따른다.

### class 대신 className 사용
HTML에서는 요소의 클래스를 지정할 때 `class` 속성을 사용하지만 JSX에서는 자바스크립트 키워드인 `class`와의 충돌을 피하기 위해 `className`을 사용한다.

```jsx
// HTML
&lt;div class=&quot;container&quot;&gt;&lt;/div&gt;

// JSX
&lt;div className=&quot;container&quot;&gt;&lt;/div&gt;</code></pre><h3 id="for-대신-htmlfor-사용">for 대신 htmlFor 사용</h3>
<p>for은 자바스크립트에서 예약어이기 때문에 JSX에서는 htmlFor를 사용해야 한다. </p>
<pre><code>// HTML
&lt;label for=&quot;input&quot;&gt;Input&lt;/label&gt;

// JSX
&lt;label htmlFor=&quot;input&quot;&gt;Input&lt;/label&gt;</code></pre><h3 id="camelcase-속성명-사용">CamelCase 속성명 사용</h3>
<p>JSX에서는 HTML 속성명 대신 자바스크립트에서 일반적으로 사용하는 CamelCase 스타일을 사용한다.</p>
<pre><code>// HTML
&lt;button onclick=&quot;handleClick()&quot;&gt;Click Me&lt;/button&gt;

// JSX
&lt;button onClick={handleClick}&gt;Click Me&lt;/button&gt;</code></pre><h3 id="소문자와-대문자의-구분">소문자와 대문자의 구분</h3>
<p>HTML에서는 태그명이 대소문자를 구분하지 않지만, JSX에서는 대문자로 시작하는 태그를 컴포넌트로 인식한다. 
소문자로 시작하는 태그는 HTML 기본 태그로 처리되고 대문자로 시작하는 태그는 React 컴포넌트로 인식한다.</p>
<pre><code>// HTML 태그
&lt;div&gt;&lt;/div&gt;

// React 컴포넌트
&lt;MyComponent /&gt;</code></pre><h3 id="jsx의-태그는-반드시-닫혀야-함">JSX의 태그는 반드시 닫혀야 함</h3>
<p>JSX에서는 모든 태그가 반드시 닫혀야 한다. HTML에서는 닫히지 않는 태그를 사용할 수 있지만 JSX에서는 모든 태그가 스스로 닫히거나 종료 태그가 있어야 한다.</p>
<pre><code>// HTML
&lt;img src=&quot;image.png&quot;&gt;

// JSX (self-closing)
&lt;img src=&quot;image.png&quot; /&gt;</code></pre><h3 id="주석-처리-방식">주석 처리 방식</h3>
<p>HTML에서는 <code>&lt;!-- --&gt;</code>를 사용해 주석을 작성하지만 JSX에서는 자바스크립트 문법과 동일하게 <code>{/* */}</code>를 사용해 주석을 작성한다.</p>
<pre><code>// HTML
&lt;!-- This is a comment --&gt;

// JSX
{/* This is a comment */}</code></pre><h3 id="boolean-속성-처리">Boolean 속성 처리</h3>
<p>HTML에서 checked, disabled와 같은 Boolean 속성은 속성명만 작성해도 적용되지만 JSX에서는 true 값을 명시적으로 지정해야 한다.</p>
<pre><code>// HTML
&lt;input type=&quot;checkbox&quot; checked&gt;

// JSX
&lt;input type=&quot;checkbox&quot; checked={true} /&gt;</code></pre>