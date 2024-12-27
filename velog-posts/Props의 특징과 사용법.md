<h1 id="🧪props의-특징">🧪Props의 특징</h1>
<h2 id="📖read-only">📖Read-only</h2>
<p>Props의 중요한 특징은 Read-only, 즉 읽기 전용이라는 것이다. 읽을 수만 있고 값을 변경할 수 없다.
props의 값은 React component가 element를 생성하기 위해 사용하는 값인데, 이 값들이 element를 생성하는 도중에 바뀌어 버리면 제대로된 element가 생성될 수 없다. 
다른 props의 값으로 element를 생성하려면 새로운 값을 component에 전달해 새로 element를 생성하면 된다.
이 과정에서 element가 다시 렌더링되는 것이다.</p>
<h2 id="😇pure-함수">😇pure 함수</h2>
<blockquote>
<p>All React components must act like pure functions with respect to their props.</p>
</blockquote>
<p>위 문장은 React 공식 문서에 나오는 component의 특징을 설명한 문장이다. 모든 React component는 그들의 props에 관해서는 pure 함수 같은 역할을 해야한다. 즉, <code>모든 React component는 props를 직접 바꿀 수 없고, 같은 props에 대해서는 항상 같은 결과를 보여주어야 한다.</code>
함수가 pure하다는 것은 함수의 입력 값인 파라미터를 바꿀 수 없다는 의미를 포함하고 있기 때문에 React component에서는 props를 바꿀 수 없다는 의미가 된다. pure 함수는 같은 입력 값에 대해 항상 같은 결과를 보여주어야 하기 때문에 React component에서는 같은 props에 대해 항상 같은 결과(React element)를 보여줘야한다.</p>
<h3 id="😇pure">😇pure</h3>
<p>입력값을 변경하지 않으며, 같은 입력값에 대해서는 항상 같은 출력값을 리턴하는 함수를 pure하다고 한다.</p>
<pre><code>function sum(a,b) {
    return a+b;
}</code></pre><h3 id="😈impure">😈impure</h3>
<p>입력값을 변경하는 함수는 impure하다고 한다.
아래 코드의 경우 은행 계좌 정보와 금액을 파라미터로 받아서 계좌의 현재 총 잔액을 나타내는 total에서 출금할 금액인 amount를 뺀다. 이 함수는 입력으로 받은 파라미터 account의 값을 변경했으므로 impure하다.</p>
<pre><code>function withdraw(account, amount) {
    account.total -= amount;
}</code></pre><h1 id="✨props-사용법">✨Props 사용법</h1>
<h2 id="📌jsx를-사용하는-경우">📌JSX를 사용하는 경우</h2>
<p>component에 props라는 객체를 전달하기 위해서는 키와 값으로 이루어진 키값쌍의 형태로 전달한다.</p>
<pre><code>function App(props) {
    return (
        &lt;Profile
            name=&quot;hjoo830&quot;
            introduction=&quot;안녕하세요&quot;
            viewCount={1500}
        /&gt;
    );
}</code></pre><p>이 코드에는 App component가 나오고 그 안에서 Profile component를 사용하고 있다. Profile component에 name, introduction, viewCount라는 3가지 속성을 넣었다. 
props에 값을 넣을 때, 문자열 이외에 정수, 변수, 다른 component 등이 들어갈 경우는 <code>{ }</code>를 사용해 감싸줘야 한다. 문자열도 중괄호로 감싸도 상관은 없다.
이렇게 하면 이 속성의 값들이 모두 Profile component의 props로 전달된다.</p>
<h2 id="📌jsx를-사용하지-않는-경우">📌JSX를 사용하지 않는 경우</h2>
<p>JSX를 사용하지 않을 경우 createElement를 사용하여 element를 생성한다. createElement의 두번째 파라미터가 props인데, 여기에 JavaScript 객체를 넣으면 그게 해당 component의 props가 된다.</p>
<pre><code>React.createElement(
    Profile,
    {
        name: &quot;hjoo830&quot;,
        introduction: &quot;안녕하세요&quot;,
        viewCount: 1500
    },
    null
);</code></pre><p>첫번째 파라미터인 type에는 component 이름인 Profile이 들어가고, 두번째 파라미터인 props로 JavaScript 객체가 들어간다. 하위 component가 없기 때문에 세번째 파라미터인 children에는 null이 들어간다.</p>
<h3 id="❗️기억해야할-점">❗️기억해야할 점</h3>
<blockquote>
<p>React component의 props는 바꿀 수 없고, 같은 props가 들어오면 항상 같은 element를 리턴해야한다.</p>
</blockquote>