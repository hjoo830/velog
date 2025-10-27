<h1 id="📌aop란">📌AOP란?</h1>
<blockquote>
<p>AOP: Aspect Oriented Programming
공통 관심 사항(cross-cutting concern) vs 핵심 관심 사항(core concern) 분리</p>
</blockquote>
<h1 id="🔍aop가-필요한-상황">🔍AOP가 필요한 상황</h1>
<h2 id="⏱️모든-메서드의-호출-시간을-측정하고-싶다면">⏱️모든 메서드의 호출 시간을 측정하고 싶다면?</h2>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/57f0e131-f752-44c9-b90b-f64faa625c42/image.png" /></p>
<blockquote>
<p>모든 메서드에 시작과 종료 시간을 구하는 코드를 추가한다</p>
</blockquote>
<pre><code class="language-java">public Long join(Member member){
    long start = System.currentTimeMillis();

    try{   
        validateDuplicateMember(member); // 중복 회원 검증
        memberRepository.save(member);
        return member.getId();
    } finally {
        long finish = System.currentTimeMillis();
        long timeMs = finish - start;
        System.out.println(&quot;join &quot; + timeMs + &quot;ms&quot;);
    }
}

public List&lt;Member&gt; findMembers(){
    long start = System.currentTimeMillis();

    try {
        return memberRepository.findAll();
    } finally {
        long finish = System.currentTimeMillis();
        long timeMs = finish - start;
        System.out.println(&quot;findMembers &quot; + timeMs + &quot;ms&quot;);
    }
}</code></pre>
<h2 id="⚠️문제점">⚠️문제점</h2>
<ul>
<li>회원가입, 회원 조회에 시간을 측정하는 기능은 핵심 관심 사항이 아니다. </li>
<li>시간을 측정하는 로직은 공통 관심 사항이다.</li>
<li>시간을 측정하는 로직과 핵심 비즈니스의 로직이 섞여서 유지보수가 어렵다.</li>
<li>시간을 측정하는 로직을 별도의 공통 로직으로 만들기 매우 어렵다.</li>
<li>시간을 측정하는 로직을 변경할 때 모든 로직을 찾아가면서 변경해야 한다.</li>
</ul>
<p>→ AOP를 적용하자!</p>
<h1 id="✨aop-적용">✨AOP 적용</h1>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/07ef5c64-aeb0-4698-912d-77045201f972/image.png" /></p>
<ul>
<li>회원가입, 회원 조회등 핵심 관심사항과 시간을 측정하는 공통 관심 사항을 분리한다.</li>
<li>시간을 측정하는 로직을 별도의 공통 로직으로 만들었다.</li>
<li>핵심 관심 사항을 깔끔하게 유지할 수 있다.</li>
<li>변경이 필요하면 이 로직만 변경하면 된다.</li>
<li>원하는 적용 대상을 선택할 수 있다.</li>
</ul>
<pre><code class="language-java">@Aspect
@Component
public class TimeTraceAop {

    @Around(&quot;execution(* hello.hello_spring..*(..))&quot;)
    public Object execute(ProceedingJoinPoint joinPoint) throws Throwable {
        long start = System.currentTimeMillis();

        System.out.println(&quot;START: &quot; + joinPoint.toString());

        try {
            return joinPoint.proceed();
        } finally {
            long finish = System.currentTimeMillis();
            long timeMs = finish - start;
            System.out.println(&quot;END: &quot; + joinPoint.toString()+ &quot; &quot; + timeMs + &quot;ms&quot;);
        }
    }
}</code></pre>
<h1 id="🧩스프링의-aop-동작-방식">🧩스프링의 AOP 동작 방식</h1>
<h2 id="💥aop-적용-전">💥AOP 적용 전</h2>
<table>
<thead>
<tr>
<th>의존 관계</th>
<th>전체 그림</th>
</tr>
</thead>
<tbody><tr>
<td><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/e5ae7c52-ff0b-4070-aea0-4b1bc9d8698d/image.png" /></td>
<td><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/d0a50b68-06b6-4708-a0ea-ba03e0325b91/image.png" /></td>
</tr>
</tbody></table>
<h2 id="🛠️aop-적용-후">🛠️AOP 적용 후</h2>
<table>
<thead>
<tr>
<th>의존 관계</th>
<th>전체 그림</th>
</tr>
</thead>
<tbody><tr>
<td><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/fcc8b859-37db-42dc-a6d3-02f093c0a0de/image.png" /></td>
<td><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/e4ca2922-59a9-4f77-b6d2-fd9ffc2410ba/image.png" /></td>
</tr>
</tbody></table>