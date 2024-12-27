<h1 id="😄jsx의-장점">😄JSX의 장점</h1>
<h2 id="➕코드가-간결해진다">➕코드가 간결해진다</h2>
<pre><code class="language-jsx">&lt;div&gt;Hello, {name}&lt;/div&gt;</code></pre>
<pre><code class="language-jsx">React.createElement('div', null, `Hello, ${name}`);</code></pre>
<p>위의 두 코드는 동일한 역할을 한다. JSX를 사용한 코드는 HTML의 div 태그를 사용해 name이라는 변수가 들어간 인사말을 표현하고 있다.</p>
<p>JSX를 사용하지 않은 코드는 createElement 함수를 사용해 동일한 작업을 수행하고 있다.</p>
<p>두 코드를 비교해 봤을 때, JSX를 사용한 코드가 훨씬 더 간결한 것을 알 수 있다.</p>
<h2 id="➕가독성이-향상된다">➕가독성이 향상된다</h2>
<p>이전의 코드를 봤을 때, JSX를 사용한 코드가 사용하지 않은 코드에 비해 훨씬 더 코드의 의미가 빠르게 와닿는 것을 알 수 있다. </p>
<p>가독성은 코드를 작성할 때 뿐만 아니라 유지 보수 관점에서도 굉장히 중요한 부분이다.</p>
<p>가독성이 높을수록 코드에 존재하는 버그를 쉽게 발견할 수 있기 때문이다.</p>
<h2 id="➕보안성이-올라간다">➕보안성이 올라간다</h2>
<p>입력창에 문자나 숫자 같은 일반적인 값이 아닌 소스코드를 입력해 해당 코드가 실행되도록 만드는 해킹 방법인 <code>Injection attacks</code>을 방어함으로써 보안성이 올라간다.</p>
<h1 id="🧩jsx-사용법">🧩JSX 사용법</h1>
<p>JSX는 JavaScript 문법을 확장시킨 것이기 때문에 모든 JavaScript 문법을 지원한다.</p>
<p>여기에 추가로 XML과 HTML을 섞어서 사용하면 된다.</p>
<h3 id="📝javascript-코드-사용">📝JavaScript 코드 사용</h3>
<p>XML, HTML 코드를 사용하다가 중간에 JavaScript 코드를 사용하고 싶으면 <code>{ }</code>를 써서 묶어주면 된다</p>
<pre><code class="language-jsx">const element = &lt;h1&gt;Hello, {name}&lt;/h1&gt;;</code></pre>
<p>위의 코드에서 <code>{name}</code>은 name이라는 JavaScript 변수를 참조하기 위해 중괄호를 사용한 것이다. 변수 뿐만 아니라 함수도 사용 가능하다.</p>
<h3 id="🏷️태그의-속성에-값-넣기">🏷️태그의 속성에 값 넣기</h3>
<pre><code class="language-jsx">const element = &lt;div tabIndex=&quot;0&quot;&gt;&lt;/div&gt;
const element = &lt;img src={user.avatarUrl}&gt;&lt;/img&gt;</code></pre>
<p>HTML 태그 중간이 아닌, 태그의 속성에 값을 넣고 싶을 때는 <code>“ ”</code> 사이에 문자열을 넣거나 <code>{ }</code> 사이에 JavaScript 코드를 넣으면 된다.</p>
<h3 id="👶children-정의">👶children 정의</h3>
<pre><code class="language-jsx">const element = (
    &lt;div&gt;
        &lt;h1&gt;안녕&lt;/h1&gt;
        &lt;h2&gt;리액트&lt;/h2&gt;
    &lt;/div&gt; 
);</code></pre>
<p>위 코드와 같이 상위 태그가 하위 태그를 둘러싸도록 하면 자연스럽게 children이 정의된다.</p>
<p>여기에서 div 태그의 children은 h1 태그와 h2 태그가 된다.</p>