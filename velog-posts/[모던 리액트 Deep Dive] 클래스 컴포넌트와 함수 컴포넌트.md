<h1 id="🏛️클래스형-컴포넌트">🏛️클래스형 컴포넌트</h1>
<p>기본적으로 클래스 컴포넌트를 만들기 위해서는 클래스를 선언하고 extends로 만들고 싶은 컴포넌트를 extends 해야 한다. </p>
<pre><code class="language-js">import React from 'react'

class SampleComponent extends React.Component {
  render() {
    return &lt;h2&gt;Sample Component&lt;/h2&gt;
  }
}</code></pre>
<ul>
<li><p>extends 구문에 넣을 수 있는 클래스</p>
<ul>
<li>React.Component</li>
<li>React.PureComponent</li>
</ul>
</li>
<li><p>props: 컴포넌트에 특정 속성을 전달하는 용도로 쓰인다. </p>
</li>
<li><p>state: 클래스 컴포넌트 내부에서 관리하는 값. 이 값은 항상 객체여야만 한다. </p>
</li>
<li><p>메서드: 렌더링 함수 내부에서 사용되는 함수</p>
<ul>
<li>메서드를 만드는 방식<ol>
<li>constructor에서 this 바인드를 하는 방법</li>
<li>화살표 함수를 쓰는 방법</li>
<li>렌더링 함수 내부에서 함수를 새롭게 만들어 전달하는 방법 ⮕ 이 방법을 사용하면 최적화를 수행하기가 어렵기 때문에 지양하는 것이 좋다</li>
</ol>
</li>
</ul>
</li>
</ul>
<hr />
<h2 id="클래스-컴포넌트의-생명주기-메서드">클래스 컴포넌트의 생명주기 메서드</h2>
<h3 id="생명주기-메서드가-실행되는-시점">생명주기 메서드가 실행되는 시점</h3>
<ul>
<li>마운트: 컴포넌트가 생성되는 시점</li>
<li>업데이트: 이미 생성된 컴포넌트의 내용이 변경되는 시점</li>
<li>언마운트: 컴포넌트가 더 이상 존재하지 않는 시점</li>
</ul>
<h3 id="render">render()</h3>
<ul>
<li>생명주기 메서드 중 하나로, 리액트 클래스 컴포넌트의 유일한 필수 값으로 항상 쓰인다. </li>
<li>컴포넌트가 UI를 렌더링하기 위해 쓰이며 업데이트와 마운트 과정에서 일어난다. </li>
<li>항상 순수해야 하며 부수 효과가 없어야 한다. <ul>
<li>같은 입력값이 들어가면 항상 같은 결과물을 반환해야 한다는 뜻 </li>
<li>따라서 render() 내부에서 state를 직접 업데이트하는 this.setState를 호출해서는 안된다.</li>
</ul>
</li>
</ul>
<h3 id="componentdidmount">componentDidMount()</h3>
<ul>
<li>클래스 컴포넌트가 마운트되고 준비되면 그다음으로 호출되는 생명주기 메서드 </li>
<li>컴포넌트가 마운트되고 준비되는 즉시 실행된다.</li>
<li>this.setState()로 state값을 변경 가능 </li>
<li>브라우저가 실제로 UI를 업데이트하기 전에 실행되어 사용자가 변경되는 것을 눈치챌 수 없게 만든다.</li>
</ul>
<h3 id="componentdidupdate">componentDidUpdate()</h3>
<ul>
<li>컴포넌트 업데이트가 일어난 이후 바로 실행된다. </li>
<li>일반적으로 state나 props의 변화에 따라 DOM을 업데이트하는데 쓰인다.</li>
<li>this.setState() 사용 가능</li>
</ul>
<pre><code class="language-js">componentDidUpdate(prevProps: Props, prevState: State) {
      // 만약 이런 조건문이 없다면 props가 변경되는 매 순간마다 fetchData가 실행되는 불상사가 발생할 것.
    // 이 조건문 덕분에 props의 userName이 이전과 다른 경우에만 호출될 것
    if (this.props.userName !== prevProps.userName) {
      this.fetchData(this.props.userName);
    }
}</code></pre>
<h3 id="componentwillunmount">componentWillUnmount()</h3>
<ul>
<li>컴포넌트가 언마운트되거나 더이상 사용되지 않기 직전에 호출된다. </li>
<li>메모리 누수나 불필요한 작동을 막기 위한 클린업 함수를 호출하기 위한 최적의 위치</li>
<li>this.setState() 사용 불가능</li>
<li>이벤트를 지우거나, API 호출을 취소하거나, setInterval, setTimeout으로 생성된 타이머를 지우는 등의 작업을 하는데 유용</li>
</ul>
<pre><code class="language-js">componentWillUnmount() {
  window.removeEventListener('resize', this.resizeListener)
  clearInterval(this.intervalId)

}</code></pre>
<h3 id="shouldcomponentupdate">shouldComponentUpdate()</h3>
<ul>
<li>state나 props의 변경으로 리액트 컴포넌트가 리렌더링되는 것을 막기 위해 쓰인다.</li>
<li>일반적으로 state의 변화에 따라 컴포넌트가 리렌더링되는 것은 자연스러운 일이므로 이 메서드를 사용하는 것은 특정한 성능 최적화 상황에서만 고려해야 한다.</li>
</ul>
<pre><code class="language-js">shouldComponentUpdate(nextProps: Props, nextState: State) {
      // true인 경우 컴포넌트를 업데이트한다.
    // 이외의 경우에는 업데이트하지 않는다.
    return this.props.title !== nextProps.title || this.state.input !== nextState.input
}</code></pre>
<h3 id="component와-purecomponent의-차이점">Component와 PureComponent의 차이점</h3>
<ul>
<li>Component: state가 업데이트되는 대로 렌더링이 일어난다.</li>
<li>PureComponent: state 값에 대해 얕은 비교를 수행해 결과가 다를 때만 렌더링을 수행한다.</li>
</ul>
<h3 id="static-getderivedstatefromprops">static getDerivedStateFromProps()</h3>
<ul>
<li>이전에 존재했으나 이제는 사라진 componenetWillReceiveProps를 대체할 수 있는 메서드 </li>
<li>render()를 호출하기 직전에 호출된다.</li>
<li>static으로 선언되어 있어 this에 접근할 수 없다.</li>
</ul>
<pre><code class="language-js">static getDerivedStateFromProps(nextProps: Props, prevState: State) {
  // 다음에 올 props를 바탕으로 현재의 state를 변경하고 싶을 때 사용
  if (props.name !== state.name) {
    return {
      // state가 이렇게 변경된다
      name: props.name
    }
  }

  // state에 영향을 미치지 않는다
  return null
}</code></pre>
<h3 id="getsnapshotbeforeupdate">getSnapShotBeforeUpdate()</h3>
<ul>
<li>componentWillUpdate()를 대체할 수 있는 메서드 </li>
<li>DOM이 업데이트 되기 직전에 호출된다. </li>
<li>반환된 값은 componentDidUpdate로 전달된다.</li>
<li>DOM이 렌더링되기 전에 윈도우 크기를 조절하거나 스크롤 위치를 조정하는 등의 작업을 처리하는 데 유용하다.</li>
</ul>
<pre><code class="language-js">getSnapShotBeforeUpdate(prevProps: Props, prevState: State){
  // props로 넘겨받은 배열의 길이가 이전보다 길어질 경우 현재 스크롤 높이 값을 반환
  if (prevProps.list.length &lt; this.props.list.length){
      const list = this.listRef.current;
    return list.scrollHeight - list.scrollTop;
  }
  return null;
}

// 3번째 인수인 snapshot은 클래스 제네릭의 3번째 인수로 넣어줄 수 있다.
componentDidUpdate(prevProps: Props, prevState: State, snapshot: Snapshot){
  // getSnapShotBeforeUpdate로 넘겨받은 값은 snapshot에서 접근 가능
  // 이 snapshot 값이 있다면 스크롤 위치를 재조정해 기존 아이템이 스크롤에서 밀리지 않도록 도와준다
  if (snapshot !== null){
    const list = this.listRef.current;
    list.scrollTop = list.scrollHeight - snapshot;
  }
}</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/a24ad3f0-1f4a-4b7e-9d32-207eb809625b/image.png" /></p>
<h3 id="getderivedstatefromerror">getDerivedStateFromError()</h3>
<ul>
<li>자식 컴포넌트에서 에러가 발생했을 때 호출되는 에러 메서드 </li>
<li>인수로 하위 컴포넌트에서 발생하나 error를 받는다.</li>
<li>반드시 state 값을 반환해야 한다.<ul>
<li>하위 컴포넌트에서 에러가 발생했을 때 어떻게 자식 리액트 컴포넌트를 렌더링할지 결정하는 용도로 제공되는 메서드이기 때문에 반드시 미리 정해둔 state 값을 반환해야한다.</li>
</ul>
</li>
<li>렌더링 과정에서 호출되는 메서드이기 때문에 부수 효과를 발생시켜서는 안된다.</li>
</ul>
<h3 id="componentdidcatch">componentDidCatch</h3>
<ul>
<li>자식 컴포넌트에서 에러가 발생했을 때 실행되며, getDerivedStateFromError에서 에러를 잡고 state를 결정한 이후에 실행된다.</li>
<li>두 개의 인수를 받는다<ul>
<li>getDerivedStateFromError와 동일한 error</li>
<li>정확히 어떤 컴포넌트가 에러를 발생시켰는지 정보를 가지고 있는 info</li>
</ul>
</li>
<li>부수 효과를 수행할 수 있다.<ul>
<li>render 단계에서 실행되는 getDerivedStateFromError와 다르게 커밋 단계에서 실행되기 때문</li>
</ul>
</li>
</ul>
<hr />
<h2 id="클래스-컴포넌트의-한계">클래스 컴포넌트의 한계</h2>
<ul>
<li>데이터의 흐름을 추적하기 어렵다. </li>
<li>애플리케이션 내부 로직의 재사용이 어렵다. </li>
<li>기능이 많아질수록 컴포넌트의 크기가 커진다. </li>
<li>클래스는 함수에 비해 상대적으로 어렵다. </li>
<li>코드 크기를 최적화하기 어렵다. </li>
<li>핫 리로딩을 하는 데 상대적으로 불리하다.<ul>
<li>핫 리로딩: 코드에 변경 사항이 있을 때 앱을 다시 시작하지 않고서도 해당 변경된 코드만 업데이트해 변경 사항을 적용하는 기법</li>
</ul>
</li>
</ul>
<h1 id="🪄함수형-컴포넌트">🪄함수형 컴포넌트</h1>
<ul>
<li>render 내부에서 필요한 함수를 선언할 때 this 바인딩을 조심할 필요가 없다.</li>
<li>state는 객체가 아닌 각각의 원시값으로 관리되어 훨씬 사용이 편리하다. </li>
<li>state는 객체도 관리할 수 있다. </li>
<li>return에서도 굳이 this를 사용하지 않더라도 props와 state에 접근할 수 있다.</li>
</ul>
<h1 id="🆚함수형-컴포넌트-vs-클래스형-컴포넌트">🆚함수형 컴포넌트 vs 클래스형 컴포넌트</h1>
<h2 id="생명주기-메서드의-부재">생명주기 메서드의 부재</h2>
<ul>
<li>생명주기 메서드는 React.Component에서 오기 때문에 함수형 컴포넌트에서 사용할 수 없다.</li>
<li>함수형 컴포넌트는 useEffect를 통해 생명주기 메서드인 componentDidMount, componentDidUpdate, componentWillUnmount를 비슷하게 구현할 수 있다.</li>
<li>그러나 비슷할 뿐이지 똑같다는 것이 아니다.<ul>
<li>useEffect는 생명주기를 위한 훅이 아니라 useEffect 컴포넌트의 state를 활용해 동기적으로 부수 효과를 만드는 메커니즘이다.</li>
</ul>
</li>
</ul>
<h2 id="렌더링-된-값">렌더링 된 값</h2>
<ul>
<li>함수형 컴포넌트는 렌더링 된 값을 고정</li>
<li>클래스형 컴포넌트는 렌더링 된 값을 고정하지 않는다.<pre><code class="language-js">import React from 'react'
</code></pre>
</li>
</ul>
<p>interface Props {
  user: string
}</p>
<p>// 함수형 컴포넌트로 구현한 setTimeout 예제
export function FunctionalComponent(props: Props) {
  const showMessage = () =&gt; {
    alert('Hello' + props.user)
  }</p>
<p>  const handleClick = () =&gt; {
    setTimeout(showMessage, 3000)
  }</p>
<p>  return <button>Follow</button>
}</p>
<p>// 클래스형 컴포넌트로 구현한 setTimeout 예제
export class ClassComponent extends React.Component&lt;Props, {}&gt; {
  private showMessage = () =&gt; {
    alert('Hello' + this.props.user)
  }</p>
<p>  private handleClick = () =&gt; {
    setTimeout(this.showMessage, 3000)
  }</p>
<p>  public render(){
    return <button>Follow</button>
  }
}</p>
<pre><code>
- 클래스형 컴포넌트는 props의 값을 this에서 가져온다.
- 클래스형 컴포넌트의 props는 외부에서 변경되지 않는 이상 불변 값이지만 this가 가리키는 객체, 즉 컴포넌트의 인스턴스의 멤버는 변경 가능한 값이다.


- this에 바인딩 된 props를 사용하는 클래스형 컴포넌트와 다르게, 함수형 컴포넌트는 props를 인수로 받는다.
- this와 다르게 props는 인수로 받기 때문에 컴포넌트는 그 값을 변경할 수 없고 해당 값을 그대로 사용한다.


- 함수형 컴포넌트는 렌더링이 일어날 때마다 그 순간의 값인 Props와 state를 기준으로 렌더링된다.
- 클래스형 컴포넌트는 시간의 흐름에 따라 변화하는 this를 기준으로 렌더링이 일어난다.</code></pre>