<h1 id="📌assertthat이란">📌assertThat이란?</h1>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/ccc6b3a0-f12d-491f-ab19-188cffa870ac/image.png" /></p>
<blockquote>
<p><code>assertThat(T actual)</code>의 형태로, 메서드를 사용하여 두 값을 비교할 수 있다.</p>
</blockquote>
<p>AssertJ에서 <code>assertThat</code> 메서드를 사용할 때, 첫 번째 인자가 'actual' (실제 값)이고, 그 뒤에 이어지는 메서드들은 'expected' (기대하는 값)를 명시한다.</p>
<h1 id="📌isequalto">📌isEqualTo</h1>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/58162601-aa08-49b1-85cf-48901b2c3f39/image.png" /></p>
<blockquote>
<p><code>isEqualTo(Object expected)</code>의 형태로, <code>assertThat(실제값)</code> 뒤에서 두 값의 동등성을 검증하는 메서드이다.</p>
</blockquote>
<p><code>assertThat(실제값).isEqualTo(기댓값)</code> 형태로 사용된다.</p>
<h1 id="📌assertions">📌Assertions</h1>
<p><code>assertThat</code>을 사용하기 위해서는 <code>Assertions.assertThat(실제값).isEqualTo(기댓값)</code> 형태로 사용해야한다.
그런데 Assertions를 import 하려니 두가지가 뜬다!
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/afcdd68d-599e-4bfa-990f-bcb34ff77f47/image.png" /></p>
<h2 id="✅orgjunitjupiterapiassertions">✅org.junit.jupiter.api.Assertions</h2>
<ul>
<li><code>JUnit 5</code>에서 제공되는 단언(Assertion) 유틸리티 클래스.</li>
<li>대표적인 메서드로 <code>assertEquals(expected, actual)</code>가 있다</li>
</ul>
<pre><code class="language-java">@Test
public void save(){
    Member member = new Member();
    member.setName(&quot;spring&quot;);

    repository.save(member);
    Member result = repository.findById(member.getId()).get();

    Assertions.assertEquals(result, member); // (기댓값, 실제값)
}</code></pre>
<h2 id="✅orgassertjcoreapiassertions">✅org.assertj.core.api.Assertions</h2>
<ul>
<li><code>AssertJ</code>가 제공하는 플루언트 단언(Fluent Assertion) 유틸리티 클래스.</li>
<li>대표적인 메서드로 <code>assertThat(actual).isEqualTo(expected)</code>가 있다.</li>
</ul>
<blockquote>
<p>두 메서드의 기댓값, 실제값 순서가 반대이므로 주의!</p>
</blockquote>
<h1 id="🔎사용-예시">🔎사용 예시</h1>
<pre><code class="language-java">@Test  
public void save(){
    Member member = new Member()
    member.setName(&quot;spring&quot;);

    repository.save(member);
    Member result = repository.findById(member.getId()).get();
    assertThat(member).isEqualTo(result);
}</code></pre>
<ul>
<li><code>save()</code> 기능을 테스트하기 위해서 실제로 save된 대상(actual)이 <code>member</code>가 되고 기대하는 값(expected)이 <code>result</code>가 된다.</li>
</ul>
<pre><code class="language-java">@Test
public void findByName(){
    Member member1 = new Member();
    member1.setName(&quot;spring1&quot;);
    repository.save(member1);

    Member member2 = new Member();
    member2.setName(&quot;spring2&quot;);
    repository.save(member2);

    Member result = repository.findByName(&quot;spring1&quot;).get();
    assertThat(result).isEqualTo(member1);
}</code></pre>
<ul>
<li><code>findByName()</code> 기능을 테스트하기 위해서 실제로 findByName으로 조회 된 된 대상(actual)이 <code>result</code>가 되고 기대하는 값(expected)이 <code>member1</code>이 된다.</li>
</ul>
<h3 id="🍯tip">🍯Tip</h3>
<p>위의 사용 예시에서 </p>
<pre><code class="language-java">Assertions.assertThat(member).isEqualTo(result); </code></pre>
<p>하지 않고 </p>
<pre><code class="language-java">assertThat(member).isEqualTo(result); </code></pre>
<p>로 사용하였다.
아래와 같이 정적 임포트를 하면 매번 <code>Assertions.</code>을 붙이지 않고도 사용 가능하다.</p>
<p><code>import static org.assertj.core.api.Assertions.*;</code></p>