<h1 id="🎨리액트의-렌더링이란">🎨리액트의 렌더링이란?</h1>
<blockquote>
<p>리액트 애플리케이션 트리 안에 있는 모든 컴포넌트들이 현재 자신들이 가지고 있는 props와 state의 값을 기반으로 어떻게 UI를 구성하고 이를 바탕으로 어떤 DOM 결과를 브라우저에 제공할 것인지 계산하는 일련의 과정</p>
</blockquote>
<h1 id="🔄리액트의-렌더링이-일어나는-이유">🔄리액트의 렌더링이 일어나는 이유</h1>
<h2 id="리액트에서-렌더링이-발생하는-시나리오">리액트에서 렌더링이 발생하는 시나리오</h2>
<ol>
<li>최초 렌더링: 사용자가 처음 애플리케이션에 진입하면 당연히 렌더링해야 할 결과물이 필요하다. 리액트는 브라우저에 이 정보를 제공하기 위해 최초 렌더링을 수행한다.</li>
<li>리렌더링: 처음 애플리케이션에 진입했을 때 최초 렌더링이 발생한 이후로 발생하는 모든 렌더링 </li>
</ol>
<ul>
<li>리렌더링이 발생하는 경우<ul>
<li>클래스 컴포넌트의 setState가 실행되는 경우</li>
<li>클래스 컴포넌트의 forceUpdate가 실행되는 경우</li>
<li>함수 컴포넌트의 useState()의 두 번째 배열 요소인 setter가 실행되는 경우 </li>
<li>함수 컴포넌트의 useReducer()의 두 번째 배열 요소인 dispatch가 실행되는 경우 </li>
<li>컴포넌트의 key props가 변경되는 경우<ul>
<li>리액트에서의 key는 리렌더링이 발생하는 동안 형제 요소들 사이에서 동일한 요소를 식별하는 값</li>
<li>current 트리와 workInProgress 트리 사이에서 같은 컴포넌트인지를 구별하는 값이 key</li>
<li><code>&lt;Child key={Math.random()} &gt;</code>과 같이 랜덤한 값을 key에 할당하면 memo로 선언해도 매번 리렌더링이 일어나기에 key를 활용해 강제로 리렌더링을 일으키는 것이 가능하다.</li>
</ul>
</li>
<li>props가 변경되는 경우</li>
<li>부모 컴포넌트가 렌더링될 경우<ul>
<li>부모 컴포넌트가 리렌더링된다면 자식 컴포넌트도 무조건 리렌더링이 일어난다</li>
</ul>
</li>
</ul>
</li>
</ul>
<h1 id="🛠️리액트의-렌더링-프로세스">🛠️리액트의 렌더링 프로세스</h1>
<ul>
<li><p>렌더링 프로세스가 시작되면 리액트는 컴포넌트의 루트에서부터 차근차근 아래쪽으로 내려가면서 업데이트가 필요하다고 지정돼 있는 모든 컴포넌트를 찾는다. </p>
</li>
<li><p>여기서 업데이트가 필요하다고 지정된 컴포넌트를 발견하면 클래스 컴포넌트의 경우 클래스 내부의 render() 함수를 실행하게 되고, </p>
</li>
<li><p>함수 컴포넌트의 경우 FunctionComponent() 자체를 호출한 뒤에, 그 결과물을 저장한다.</p>
</li>
<li><p>렌더링 결과물은 JSX 문법으로 구성되어 있고, 자바스크립트로 컴파일 되면서 React.createElement()를 호출하는 구문으로 변환된다.</p>
<pre><code class="language-js">function Hello() {
  // JSX 문법
  return (
    &lt;TestComponent a={35} b=&quot;yceffort&quot;&gt;
      안녕하세요
    &lt;/TestComponent&gt;
  )
}</code></pre>
<pre><code class="language-js">function Hello() {
  // React.createElement()를 호출하는 구문으로 변환
  return React.createElement(
    TestComponent,
    { a: 35, b: &quot;yceffort&quot;},
    '안녕하세요',
  )
}</code></pre>
</li>
<li><p>렌더링 프로세스가 실행되면서 각 컴포넌트의 렌더링 결과물을 수집한 다음, 가상 DOM과 비교해 실제 DOM에 반영하기 위한 모든 변경 사항을 차례차례 수집한다.</p>
</li>
<li><p>모든 변경 사항을 하나의 동기 시퀀스로 DOM에 적용해 변경된 결과물이 보이게 된다.</p>
</li>
<li><p><strong>리액트의 렌더링은 렌더 단계와 커밋 단계 총 두 단계로 분리되어 실행된다.</strong></p>
</li>
</ul>
<h1 id="🔧렌더와-커밋">🔧렌더와 커밋</h1>
<h2 id="렌더-단계">렌더 단계</h2>
<blockquote>
<p>컴포넌트를 렌더링하고 변경 사항을 계산하는 모든 작업 </p>
</blockquote>
<ul>
<li>렌더링 프로세스에서 컴포넌트를 실행해 이 결과와 이전 가상 DOM을 비교하는 과정을 거쳐 변경이 필요한 컴포넌트를 체크하는 단계 </li>
<li>key, props, key 중 하나라도 변경되면 변경이 필요한 컴포넌트로 체크</li>
</ul>
<h2 id="커밋-단계">커밋 단계</h2>
<blockquote>
<p>렌더 단계의 변경 사항을 실제 DOM에 적용해 사용자에게 보여주는 과정 </p>
</blockquote>
<ol>
<li>리액트가 먼저 DOM을 커밋 단계에서 업데이트 </li>
<li>모든 DOM 노드 및 인스턴스를 가리키도록 리액트 내부의 참조를 업데이트 </li>
<li>클래스 컴포넌트에서는 componentDidMount, componentDidUpdate 메서드를 호출, 함수 컴포넌트에서는 useLayoutEffect 훅을 호출</li>
</ol>
<p><strong>리액트의 렌더링이 일어난다고 해서 무조건 DOM 업데이트가 일어나는 것은 아니다.</strong>
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/aeb0ca5a-9deb-40a3-a1d7-0beed920ed19/image.png" /></p>
<h2 id="동시성-렌더링">동시성 렌더링</h2>
<ul>
<li>의도된 우선순위로 컴포넌트를 렌더링해 최적화할 수 있는 비동기 렌더링</li>
<li>렌더링 중 렌더 단계가 비동기로 작동해 특정 렌더링의 우선순위를 낮추거나, 필요하다면 중단하거나 재시작하거나, 경우에 따라서 포기할 수도 있다. </li>
<li>이를 통해 브라우저의 동기 작업을 차단하지 않고 백그라운드에서 새로운 리액트 트리를 준비할 수도 있으므로 사용자는 더욱 매끄러운 사용자 경험을 느낄 수 있다.</li>
</ul>
<h1 id="🖥️일반적인-렌더링-시나리오-살펴보기">🖥️일반적인 렌더링 시나리오 살펴보기</h1>
<pre><code class="language-js">import { useState } from 'react'

export default function A() {
  return (
    &lt;div className=&quot;App&quot;&gt;
      &lt;h1&gt;Hello React&lt;/h1&gt;
      &lt;B /&gt;
    &lt;/div&gt;
  )
}

function B() {
  const [counter, setCounter] = useState(0)

  function handleButtonClick() {
    setCounter((previous) =&gt; previous + 1)
  }

  return (
    &lt;&gt;
      &lt;label&gt;
        &lt;C number={counter} /&gt;
      &lt;/label&gt;
      &lt;button onClick={handleButtonClick}&gt;+&lt;/button&gt;
    &lt;/&gt;
  )
}

function C({ number }) {
  return (
    &lt;div&gt;
    {number} &lt;D /&gt;
    &lt;/div&gt;
  )
}

function D() {
  return &lt;&gt;리액트 재밌다!&lt;/&gt;
}</code></pre>
<ul>
<li>사용자가 B 컴포넌트의 버튼을 눌러 counter 변수를 업데이트한다고 가정</li>
</ul>
<ol>
<li>B 컴포넌트의 setState가 호출된다.</li>
<li>B 컴포넌트의 리렌더링 작업이 렌더링 큐에 들어간다.</li>
<li>리액트는 트리 최상단에서부터 렌더링 경로를 검사한다.</li>
<li>A 컴포넌트는 리렌더링이 필요한 컴포넌트로 표시되어 있지 않으므로 별다른 작업을 하지 않는다.</li>
<li>그다음 하위 컴포넌트인 B 컴포넌트는 업데이트가 필요하다고 체크되어 있으므로 B를 리렌더링한다.</li>
<li>5번 과정에서 B는 C를 반환했다.</li>
<li>C는 props인 number가 업데이트 됐다. 그러므로 업데이트가 필요한 컴포넌트로 체크되어 있고 업데이트 한다.</li>
<li>7번 과정에서 C는 D를 반환했다.</li>
<li>D도 마찬가지로 업데이트가 필요한 컴포넌트로 체크되지 않았다. 그러나 C가 렌더링됐으므로 그 자식인 D도 렌더링됐다.</li>
</ol>
<blockquote>
<p>컴포넌트를 렌더링하는 작업은 하위 모든 컴포넌트에 영향을 미친다.</p>
</blockquote>
<blockquote>
<p>부모가 변경됐다면 props가 변경됐는지와 상관없이 무조건 자식 컴포넌트도 리렌더링 된다.</p>
</blockquote>