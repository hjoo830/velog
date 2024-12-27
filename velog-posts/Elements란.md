<h1 id="🔍elements란">🔍Elements란?</h1>
<p>Elements라는 영어 단어는 요소, 성분이라는 뜻을 가지고 있다. 즉, 어떤 물체를 구성하는 성분을 Elements라고 한다.</p>
<p>React의 Elements도 React 앱을 구성하는 요소를 의미한다.</p>
<p>React 공식 홈페이지에서는 Elements를 아래와 같이 정의하고 있다</p>
<blockquote>
<p>Elements are the smallest building blocks of React apps.</p>
</blockquote>
<p>번역해보면 <code>React 앱을 구성하는 가장 작은 블록들</code>을 Elements라고 한다.</p>
<p>React Elements는 화면에서 보이는 것을 기술하고, 기술한 내용을 토대로 실제 우리가 화면에서 보게되는 DOM Elements가 만들어진다.</p>
<pre><code class="language-jsx">const element = &lt;h1&gt;Hello, world&lt;/h1&gt;;</code></pre>
<p>위의 코드가 실행될 때 대입 연산자의 오른쪽 부분은 createElement 함수를 사용해 element를 생성하게 된다.</p>
<h1 id="✨elements의-생김새">✨Elements의 생김새</h1>
<p>React Elements는 JavaScript 객체 형태로 존재한다.</p>
<p>element는 type, props, children에 대한 정보를 포함하고 있는 일반적인 JavaScript 객체이다.</p>
<h3 id="🔤type에-html-태그-이름이-문자열로-들어가는-경우">🔤type에 HTML 태그 이름이 문자열로 들어가는 경우</h3>
<pre><code class="language-jsx">{
    type: 'button',
    props: {
        className: 'bg-green',
        children: {
            type: 'b',
            props: {
                children: 'Hello, element'
            }
        }
    }
}</code></pre>
<p>위의 코드는 버튼을 나타내기 위한 Elements이다. 이 코드처럼 type에 HTML 태그 이름이 문자열로 들어가는 경우 Elements는 해당 태그 이름을 가진 DOM 노드를 나타내고 props는 속성에 해당한다.</p>
<p>이 Elements가 실제로 렌더링 되면 아래와 같은 DOM Elements가 될 것이다.</p>
<pre><code class="language-jsx">&lt;button class='bg-green'&gt;
    &lt;b&gt;
        Hello, element
    &lt;/b&gt;
&lt;/button&gt;</code></pre>
<h3 id="🧩type에-html-태그-이름이-문자열로-들어가지-않는-경우">🧩type에 HTML 태그 이름이 문자열로 들어가지 않는 경우</h3>
<pre><code class="language-jsx">{
    type: Button,
    props: {
        color: 'green',
        children: 'Hello, element'
    }
}</code></pre>
<p>위의 코드는 React의 컴포넌트 Elements를 나타낸 것이다. 이것도 일반적인 JavaScript 객체이다.</p>
<p>이전의 코드와 다른 점은 type이 문자열로 된 HTML 태그가 아닌, React 컴포넌트의 이름이 들어갔다는 점이다.</p>
<p>이처럼 React Elements는 JavaScript 객체 형태로 존재한다.</p>
<h3 id="❗️기억해야할-점">❗️기억해야할 점</h3>
<blockquote>
<p>컴포넌트 렌더링을 위해 모든 컴포넌트가 createElement 함수를 통해 Elements로 변환된다.</p>
</blockquote>
<blockquote>
<p>React Elements는 우리 눈에 실제로 보이는 것을 기술한다.</p>
</blockquote>