<h1 id="📊state">📊State</h1>
<p>React에서의 state는 React component의 상태를 의미한다. 쉽게 말하면 React component의 변경 가능한 데이터를 State라고 부른다.</p>
<p>State는 사전에 미리 정해진 것이 아니라 React component를 개발하는 각 개발자가 직접 정의해서 사용하게 된다. State를 정의할 때 중요한 점은 꼭 <code>렌더링이나 데이터 흐름에 사용되는 것만 State에 포함시켜야 한다</code>는 것이다. State가 변경될 경우 component가 재렌더링되기 때문에 렌더링과 데이터 흐름에 관련 없는 값을 포함하면 불필요한 경우에 component가 다시 렌더링되어 성능을 저하시킬 수 있기 때문이다. 그래서 렌더링과 데이터 흐름에 관련 있는 값만 state에 포함하고, 그렇지 않은 값은 component의 인스턴스 필드로 정의하면 된다. </p>
<p>React의 state는 따로 복잡한 형태가 있는 것이 아니라 그냥 하나의 자바스크립트 객체이다. </p>
<pre><code class="language-jsx">class LikeButton extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            liked: false
        };
    }
    ...
}</code></pre>
<p>이 코드는 LikeButton이라는 React 클래스 컴포넌트를 나타낸 것이다. 모든 클래스 컴포넌트에는 constructor라는 이름의 함수가 존재하는데, 생성자라는 의미를 갖고 있으며 클래스가 생성될 때 실행되는 함수이다.</p>
<p>생성자 코드에 <code>this.state</code> 라는 부분이 현재 컴포넌트의 state를 정의하는 부분이다.</p>
<p>클래스 컴포넌트의 경우 state를 생성자에서 정의하고, 함수 컴포넌트의 경우 state를 useState라는 Hook을 사용해서 정의한다.</p>
<h2 id="🔧state-수정">🔧state 수정</h2>
<p>정의된 state는 정의된 이후 일반적인 자바스크립트 변수처럼 직접 수정할 수는 없다. 수정이 가능하긴 하지만 아래 코드처럼 직접 수정하면 안되고 <code>setState 함수를 통해 수정</code>해야한다.</p>
<pre><code class="language-jsx">// state를 직접 수정 (잘못된 방법)
this.state = {
    name: 'hjoo830'
};

// setState 함수를 통해 수정 (정상적인 방법)
this.setState({
    name: 'hjoo830'
});</code></pre>
<h1 id="⌛️lifecycle">⌛️Lifecycle</h1>
<p>Lifecycle은 생명 주기라는 뜻을 가진 영어 단어이다. React 컴포넌트도 생명 주기를 갖고 있다. 컴포넌트가 생성되는 시점과 사라지는 시점이 정해져있다는 의미이다.</p>
<p>아래 그림은 React 클래스 컴포넌트의 생명 주기를 나타낸 것이다. 각 과정의 하단에 초록색 부분은 생명 주기에 따라 호출되는 클래스 컴포넌트의 함수이다. 이 함수들은 Lifecycle Method라고 부르며, 번역하면 생명 주기 함수이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/1927d829-c857-40d2-8f1c-f439ed1312ef/image.png" /></p>
<h2 id="🐣mount">🐣Mount</h2>
<ul>
<li>컴포넌트가 생성되는 시점</li>
<li>이때 컴포넌트의 생성자가 실행된다. 위에서 말한 것처럼 생성자에서는 컴포넌트의 state를 정의하게 된다.</li>
<li>컴포넌트가 렌더링되며 이후에 componentDidMount 함수가 호출된다.</li>
</ul>
<h2 id="🐥update">🐥Update</h2>
<ul>
<li>사람이 인생을 살아가며 신체적, 정신적 변화를 겪듯이 React 컴포넌트도 생애동안 변화를 겪으면서 여러 번 렌더링된다. 이를 업데이트라고 한다.</li>
<li>업데이트 과정에서는 컴포넌트의 props가 변경되거나 setState 함수 호출에 의해 state가 변경되거나 forceUpdate라는 강제 업데이트 함수 호출로 인해 컴포넌트가 다시 렌더링 된다.</li>
<li>렌더링 이후에 componentDidUpdate 함수가 호출된다.</li>
</ul>
<h2 id="💀unmount">💀Unmount</h2>
<ul>
<li>React 컴포넌트도 언젠가는 사라지는 과정을 겪는데 이 과정을 Unmount라고 한다.</li>
<li>상위 컴포넌트에서 현재 컴포넌트를 더이상 화면에 표시하지 않게 될 때 Unmount 된다.</li>
<li>Unmount 직전에 componentWillUnmount 함수가 호출된다.</li>
</ul>
<h3 id="❗️기억해야할-점">❗️기억해야할 점</h3>
<blockquote>
<p>State를 정의할 때 렌더링이나 데이터 흐름에 사용되는 것만 State에 포함시켜야 한다.</p>
</blockquote>
<blockquote>
<p>State를 수정할 때 직접 수정하면 안되고 <code>setState</code> 함수를 통해 수정해야한다.</p>
</blockquote>
<blockquote>
<p>컴포넌트가 계속 존재하는 것이 아니라 시간의 흐름에 따라 생성되고 업데이트 되다가 사라진다.</p>
</blockquote>