<h1 id="✨elements의-특징">✨Elements의 특징</h1>
<h2 id="🛡️불변성">🛡️불변성</h2>
<blockquote>
<p>React elements are immutable</p>
</blockquote>
<p>불변성은 변하지 않는 성질을 의미한다. elements가 불변성을 갖고 있다는 것은 <code>한 번 생성된 Elements는 변하지 않는다</code> 는 것이다. 즉, elements 생성 후에는 children이나 attributes를 바꿀 수 없다.</p>
<h2 id="🤔변하지-않으면-화면-갱신은-어떻게">🤔변하지 않으면 화면 갱신은 어떻게?</h2>
<p>elements가 변할 수 없다면 화면 갱신이 안되는거 아니야? 라는 생각이 들 수 있다.</p>
<p>위의 내용에서 중요한 것은 <strong><code>elements 생성 후에는</code></strong> children이나 attributes를 바꿀 수 없다는 것이다. 즉, elements는 다양한 모습으로 존재할 수 있지만 한 번 생성된 다음에는 변경이 불가능하다는 것이다.</p>
<p>화면에 변경된 elements들을 보여주기 위해서는 기존의 elements를 변경하는 것이 아니라 새로운 elements를 만들면 된다. <code>새로운 elements를 만들어서 기존 elements와 바꿔치기 하는 것</code>이다.</p>
<h1 id="🎨elements-렌더링">🎨Elements 렌더링</h1>
<p>elements를 생성한 이후에 실제로 화면에 보여주기 위해선 렌더링이라는 과정을 거쳐야 한다. </p>
<h3 id="🌳root-dom-node">🌳Root DOM Node</h3>
<p><code>&lt;div id=&quot;root&quot;&gt;&lt;/div&gt;</code></p>
<p>이 HTML 코드는 root라는 id를 가진 div 태그이다. 이 코드는 모든 React 앱에 필수적으로 들어가는 아주 중요한 코드이다. </p>
<p>이 div 태그 안에 React elements들이 렌더링되며, 이것을 Root DOM Node라고 한다. 이 div 태그 안에 있는 모든 것이 React DOM에 의해 관리되기 때문이다.</p>
<p>오직 React만으로 만들어진 모든 웹사이트들은 단 하나의 Root DOM Node를 가지게 된다. 반면에 기존에 있던 웹사이트에 추가적으로 React를 연동하게 되면 여러개의 분리된 수많은 Root DOM Node를 가질 수도 있다.</p>
<pre><code class="language-jsx">const element = &lt;h1&gt;hello, react&lt;/h1&gt;;
ReactDOM.render(element, document.getElementById('root'));</code></pre>
<p>Root div에 실제로 React elements를 렌더링하기 위해서는 위와 같은 코드를 사용한다.</p>
<p>이 코드는 먼저 element를 하나 생성하고, 생성된 element를 Root div에 렌더링하는 코드이다.</p>
<p>렌더링을 위해 ReactDOM에 render라는 함수를 사용하게 된다. 이 함수는 첫번째 파라미터인 React elements를 두번째 파라미터인 HTML element(DOM element)에 렌더링하는 역할을 한다.</p>
<p>React elements는 React의 Virtual DOM에 존재하는 것이고 DOM element는 실제 브라우저의 DOM에 존재하는 것으로 다른 것이다.</p>
<p>결국 React elements가 렌더링되는 과정은 Virtual DOM에서 실제 DOM으로 이동하는 과정이라고 할 수 있다.</p>
<h3 id="🔄한번-렌더링된-elements를-업데이트-하려면">🔄한번 렌더링된 elements를 업데이트 하려면?</h3>
<p>elements는 한 번 생성되면 바꿀 수 없기 때문에 업데이트하기 위해서는 다시 생성해야 한다.</p>
<pre><code class="language-jsx">function tick() {
    const element = (
        &lt;div&gt;
            &lt;h1&gt;안녕, 리액트! &lt;/h12
            &lt;h2&gt;현재 시간: {new Date(). toLocaleTimeString()}&lt;/h2&gt;
        &lt;/div&gt;
    );
    ReactDOM.render(element, document.getElementById('root'));
}

setInterval(tick, 1000);</code></pre>
<p>위의 코드에서 tick 함수는 현재 시간을 포함하고 있는 elements를 생성해 root에 렌더링하는 역할을 한다. 그리고 JavaScrtpt의 setInterval 함수를 사용해 tick 함수를 1000ms마다 호출하고 있다.</p>
<p>내부적으로는 tick 함수가 호출될 때마다 기존 elements를 변경하는 것이 아니라, 새로운 elements를 생성해서 바꿔치기 하는 것이다.</p>
<p>매 초 새로운 elements가 생성되어 기존 elements와 교체되면서 내용이 변경된다.</p>
<h3 id="❗️기억해야할-점">❗️기억해야할 점</h3>
<blockquote>
<p>React elements의 불변성 때문에  elements를 업데이트 하기 위해서는 새로운 elements를 만들어야한다.</p>
</blockquote>