<h1 id="🍎neofetch란">🍎neofetch란?</h1>
<ul>
<li>터미널에서 시스템 정보를 깔끔하게 표시해주는 명령줄 유틸리티</li>
<li>운영 체제, 커널 버전, Uptime, 패키지 수, 셸 정보, 해상도, DE(데스크톱 환경), WM(윈도우 매니저), 테마 정보, CPU, GPU, 메모리 상태 등의 다양한 정보를 텍스트와 함께 아스키 아트로 출력해준다.</li>
</ul>
<p><a href="https://velog.io/@hjoo830/Macbook-%ED%84%B0%EB%AF%B8%EB%84%90-%EA%BE%B8%EB%AF%B8%EA%B8%B0-Zsh-%ED%85%8C%EB%A7%88-%EC%84%A4%EC%A0%95">이전 포스팅</a>에서 설명한 부분까지 설정하면 아래와 같이 프롬포트는 예쁘게 적용되어 있다. 하지만 썸네일과 같이 알록달록한 사과 모양과 정보들이 나오진 않는다. 썸네일과 같이 터미널에 표시하기 위해서는 neofetch를 설치해야한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/d338a57e-6bce-414e-ab2e-fca35d935ef9/image.png" /></p>
<h1 id="🛠️neofetch-설치">🛠️neofetch 설치</h1>
<ol>
<li><p>Homebrew를 사용하여 neofetch를 설치한다.
<code>brew install neofetch</code>
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/e7166e64-56fc-4399-9224-abbc3628e773/image.png" /></p>
</li>
<li><p>Zsh 설정 파일인 .zshrc에 neofetch 명령을 추가하여 터미널이 열릴 때마다 자동으로 실행되도록 설정한다.
<code>echo &quot;neofetch&quot; &gt;&gt; ~/.zshrc</code>
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/dbb96214-d9d5-4ed3-a555-8c95d9c7d0a8/image.png" /></p>
</li>
<li><p>위에서 설정한 내용을 적용하기 위해 Zsh 설정 파일을 다시 로드한다.
<code>source ~/.zshrc</code>
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/d5f068bb-60e9-460b-8a12-7c8720ca5391/image.png" /></p>
</li>
</ol>
<h2 id="⚠️warning">⚠️WARNING</h2>
<p>이제 사과 모양이 잘 뜬다. 하지만 아래와 같은 문구가 떴다.</p>
<pre><code>[WARNING]: Console output during zsh initialization detected.

When using Powerlevel10k with instant prompt, console output during zsh
initialization may indicate issues.

You can:

  - Recommended: Change ~/.zshrc so that it does not perform console I/O
    after the instant prompt preamble. See the link below for details.

    * You will not see this error message again.
    * Zsh will start quickly and prompt will update smoothly.

  - Suppress this warning either by running p10k configure or by manually
    defining the following parameter:

      typeset -g POWERLEVEL9K_INSTANT_PROMPT=quiet

    * You will not see this error message again.
    * Zsh will start quickly but prompt will jump down after initialization.

  - Disable instant prompt either by running p10k configure or by manually
    defining the following parameter:

      typeset -g POWERLEVEL9K_INSTANT_PROMPT=off

    * You will not see this error message again.
    * Zsh will start slowly.

  - Do nothing.

    * You will see this error message every time you start zsh.
    * Zsh will start quickly but prompt will jump down after initialization.

For details, see:
https://github.com/romkatv/powerlevel10k#instant-prompt

-- console output produced during zsh initialization follows --</code></pre><p>이 메시지는 Zsh가 초기화될 때 콘솔 출력이 감지되었음을 알려주며, 이로 인해 instant prompt 기능이 제대로 작동하지 않을 수 있다는 경고이다.</p>
<h2 id="✅경고-메시지-해결-방법">✅경고 메시지 해결 방법</h2>
<ol>
<li><p>~/.zshrc을 연다
<code>nano ~/.zshrc</code></p>
</li>
<li><p>마지막줄에 neofetch라고 적힌곳 바로 윗 줄에 아래 명령어를 작성하고 저장한다.
<code>typeset -g POWERLEVEL9K_INSTANT_PROMPT=quiet</code></p>
</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/b1e0dd44-66a3-4871-901a-d586eae2bca9/image.png" /></p>
<ol start="3">
<li>다시 <code>source ~/.zshrc</code>를 입력하면 앞으로 iTerm2 터미널을 열때마다 경고 메시지 없이 정상적으로 잘 뜬다</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/ee8784b9-ff86-4670-a1ea-55ede599cbbf/image.png" /></p>