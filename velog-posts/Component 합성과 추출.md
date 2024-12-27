<h1 id="🧩component-합성">🧩Component 합성</h1>
<p>component 합성은 여러 개의 component를 합쳐서 하나의 component를 만드는 것이다.</p>
<p>React에서는 component 안에도 다른 component를 사용할 수 있기 때문에 복잡한 화면을 여러 개의 component로 나눠서 구현할 수 있다. </p>
<pre><code class="language-jsx">function Welcome(props) {
    return &lt;h1&gt;Hello, {props.name}&lt;/h1&gt;;
}

function App(props) {
    return (
        &lt;div&gt;
            &lt;Welcome name=&quot;Mike&quot; /&gt;
            &lt;Welcome name=&quot;Steve&quot; /&gt;
            &lt;Welcome name=&quot;Jane&quot; /&gt;
        &lt;/div&gt;
    )
}

ReactDOM.render(
    &lt;App /&gt;,
    document.getElementById('root')
);</code></pre>
<p>위의 코드를 보면 props의 값을 다르게 해서 Welcome component를 여러 번 사용하는 것을 볼 수 있다. 이렇게 하면 App이라는 component는 Welcome component 3개를 포함하고 있는 component가 된다.</p>
<p>이렇게 여러 개의 component를 합쳐서 또 다른 component를 만드는 것을 component 합성이라고 한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/b39db823-fc85-4e13-87f3-637a2f2fbe4b/image.png" /></p>
<h1 id="✂️component-추출">✂️Component 추출</h1>
<p>component 추출은 component 합성과 반대로 복잡한 component를 쪼개서 여러 개의 component로 나누는 과정이다. 큰 component에서 일부를 추출해서 새로운 component를 만드는 것이다.</p>
<p>component 추출을 잘 활용하면 component의 재사용성이 올라가게 된다. component가 작아질수록 해당 component의 기능과 목적이 명확해지고 props도 단순해지기 때문에 다른 곳에서 사용할 수 있을 확률이 높아지기 때문이다. 재사용성이 올라감으로써 동시에 개발 속도도 향상된다.</p>
<pre><code class="language-jsx">function Comment(props) {
    return (
        &lt;div className=&quot;comment&quot;&gt;
            &lt;div className=&quot;user-info&quot;&gt;
                &lt;img className=&quot;avatar&quot;
                    src={props.author.avatarUrl}
                    alt={props.author.name}
                /&gt;
                &lt;div className=&quot;user-info-name&quot;&gt;
                    {props.author.name}
                &lt;/div&gt;
            &lt;/div&gt;

            &lt;div className=&quot;comment-text&quot;&gt;
                    {props.text}
            &lt;/div&gt;

            &lt;div className=&quot;comment-date&quot;&gt;
                    {formatDate(props.date)}
            &lt;/div&gt;
        &lt;/div&gt;
    );
}</code></pre>
<p>위의 Comment라는 component는 댓글을 표시하기 위한 component로 내부에 작성자의 프로필 이미지와 이름, 댓글 내용과 작성일을 포함하고 있다. 이 component의 props는 아래와 같은 형태일 것이다.</p>
<pre><code class="language-jsx">props = {
    author: {
        name: &quot;hjoo830&quot;,
        avatarUrl: &quot;https://...&quot;,
    },
    text: &quot;댓글&quot;,
    date: Date.now(),
}</code></pre>
<p>이제 Comment component에서 하나씩 component 추출을 해보려고 한다.</p>
<h3 id="👤avatar-추출">👤Avatar 추출</h3>
<p>Comment component에는 이미지 태그를 사용해 사용자의 프로필 이미지를 표시하고 있다. 이부분을 추출해 Avatar라는 별도의 component로 만들 수 있다. </p>
<p>기존의 author 대신 보편적인 user를 사용하였는데, 보편적인 단어를 사용하는 것은 재사용성 측면을 고려하는 것이다. 다른 곳에서 이 component를 사용할 때도 의미상 큰 차이없이 사용할 수 있게하기 위해서이다.</p>
<pre><code class="language-jsx">function Avatar(props) {
    return (
        &lt;img className=&quot;avatar&quot;
            src={props.user.avatarUrl}
            alt={props.user.name}
        /&gt;
    );
}</code></pre>
<p>추출한 Avatar component를 실제 Comment component에 적용하면 아래와 같다.</p>
<pre><code class="language-jsx">function Comment(props) {
    return (
        &lt;div className=&quot;comment&quot;&gt;
            &lt;div className=&quot;user-info&quot;&gt;
                &lt;Avatar user={props.author} /&gt;
                &lt;div className=&quot;user-info-name&quot;&gt;
                    {props.author.name}
                &lt;/div&gt;
            &lt;/div&gt;

            &lt;div className=&quot;comment-text&quot;&gt;
                    {props.text}
            &lt;/div&gt;

            &lt;div className=&quot;comment-date&quot;&gt;
                    {formatDate(props.date)}
            &lt;/div&gt;
        &lt;/div&gt;
    );
}</code></pre>
<h3 id="ℹ️userinfo-추출">ℹ️UserInfo 추출</h3>
<p>아래 코드는 사용자 정보를 담고 있는 부분을 추출해 UserInfo라는 component로 추출한 것이다. 이전에 추출했던 Avatar component도 여기 함께 추출된 것을 볼 수 있다.</p>
<pre><code class="language-jsx">function UserInfo(props) {
    return (
        &lt;div className=&quot;user-info&quot;&gt;
            &lt;Avatar user={props.user} /&gt;
            &lt;div className=&quot;user-info-name&quot;&gt;
                {props.user.name}
            &lt;/div&gt;
        &lt;/div&gt;
    );
}</code></pre>
<p>추출한 UserInfo component를 실제 Comment component에 적용하면 아래와 같다. 코드가 처음에 비해 훨씬 더 단순해진 것을 볼 수 있다.</p>
<pre><code class="language-jsx">function Comment(props) {
    return (
        &lt;div className=&quot;comment&quot;&gt;
            &lt;UserInfo user={props.author} /&gt;
            &lt;div className=&quot;comment-text&quot;&gt;
                    {props.text}
            &lt;/div&gt;
            &lt;div className=&quot;comment-date&quot;&gt;
                    {formatDate(props.date)}
            &lt;/div&gt;
        &lt;/div&gt;
    );
}</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/cd3cf0b1-a96e-4693-8453-0cb30d4b1052/image.png" /></p>
<p>지금까지 추출한 component들의 구조를 그림으로 나타내면 위 그림과 같다. Comment component가 UserInfo component를 포함하고 있고 UserInfo component가 Avatar component를 포함하고 있는 구조이다.</p>
<p>지금까지 추출한 것 외에도 추가적으로 Comment의 글과 작성일 부분도 별도의 component로 추출이 가능하다.</p>