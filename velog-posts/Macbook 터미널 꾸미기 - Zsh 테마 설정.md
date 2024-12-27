<h1 id="🎡zsh-테마란">🎡Zsh 테마란?</h1>
<ul>
<li>Zsh 테마는 프롬프트(터미널 입력 줄)의 모양과 동작을 정의한다. </li>
<li>Zsh 테마는 프롬프트에서 디렉토리, Git 상태, 시간, 사용자 이름 등의 정보를 시각적으로 예쁘게 표시해준다.</li>
</ul>
<p><a href="https://velog.io/@hjoo830/Macbook-%ED%84%B0%EB%AF%B8%EB%84%90-%EA%BE%B8%EB%AF%B8%EA%B8%B0-iTerm2%EC%9D%98-%EC%83%89%EC%83%81-%ED%85%8C%EB%A7%88-%EC%84%A4%EC%A0%95">https://velog.io/@hjoo830/Macbook-%ED%84%B0%EB%AF%B8%EB%84%90-%EA%BE%B8%EB%AF%B8%EA%B8%B0-iTerm2%EC%9D%98-%EC%83%89%EC%83%81-%ED%85%8C%EB%A7%88-%EC%84%A4%EC%A0%95</a>
이전 포스트에선 색상 테마를 지정했었고, 이번 포스트에선 프롬포트를 꾸미는 과정을 설명한다.
이전 포스트에서 <code>Oh My Zsh</code>를 설치했는데, 안했다면 설치를 해야한다.</p>
<h1 id="📋zsh-테마-목록-확인">📋Zsh 테마 목록 확인</h1>
<p><code>ls ~/.oh-my-zsh/themes/</code> 명령어를 입력하면 themes 디렉토리에 있는 모든 테마 파일의 목록을 볼 수 있다</p>
<p><a href="https://github.com/ohmyzsh/ohmyzsh/wiki/Themes">https://github.com/ohmyzsh/ohmyzsh/wiki/Themes</a> 에서 테마들을 사진으로 볼 수 있다</p>
<p>나는 Powerlevel10k 테마를 적용할거라 Powerlevel10k 기준으로 설명을 하겠다.</p>
<h1 id="🛠️테마-설치">🛠️테마 설치</h1>
<ol>
<li><p>터미널에서 다음 명령어를 실행하여 Powerlevel10k 테마를 설치한다.
<code>git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/.oh-my-zsh/custom/themes/powerlevel10k</code></p>
</li>
<li><p><code>nano ~/.zshrc</code> 명령어를 입력해 <code>.zshrc</code> 파일을  열어 ZSH_THEME를 아래와 같이 설정한다.
<code>ZSH_THEME=&quot;powerlevel10k/powerlevel10k&quot;</code></p>
<p>❗️입력 후 저장은 <code>control(^)</code> + <code>O</code>, 나가기는 <code>control(^)</code> + <code>X</code></p>
</li>
<li><p>파일을 저장한 후, 터미널에서 다음 명령어를 입력하여 변경 사항을 적용한다.
<code>source ~/.zshrc</code></p>
</li>
</ol>
<h1 id="🦄powerlevel10k-설정-마법사">🦄Powerlevel10k 설정 마법사</h1>
<p><code>p10k configure</code>를 입력해 Powerlevel10k 설정 마법사 실행</p>
<h2 id="📝폰트-설정">📝폰트 설정</h2>
<p>기호가 잘 보이는지 확인하는 과정이다.</p>
<p>나는 처음에 기호가 깨져보여서 MesloLGS NF 폰트 설치 후 재실행하니까 기호들이 모두 잘 보였다.
MesloLGS NF 폰트는 아래 링크로 들어가서 설치하면 된다
<a href="https://github.com/romkatv/powerlevel10k#manual-font-installation">https://github.com/romkatv/powerlevel10k#manual-font-installation</a></p>
<h3 id="✅utf-8-인코딩-체크">✅UTF-8 인코딩 체크</h3>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/d5164074-1ea5-4a17-8752-7a8ccac649de/image.png" /></p>
<h3 id="✅puaprivate-use-area에-해당하는-글자-체크">✅PUA(Private Use Area)에 해당하는 글자 체크</h3>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/17a133b9-3487-4ade-b85e-69d6b3e92f2d/image.png" /></p>
<h3 id="✅utf-16-인코딩-체크">✅UTF-16 인코딩 체크</h3>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/951055ba-cdf2-4c6e-a856-7d28d1450187/image.png" /></p>
<h3 id="✅폰트의-크기와-폭-체크">✅폰트의 크기와 폭 체크</h3>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/cf170d3c-81ca-47be-8a52-2d100c4ae63c/image.png" /></p>
<h3 id="✅겹치는지-체크">✅겹치는지 체크</h3>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/2a752576-dee3-4bda-b7ab-b175e5cf7e37/image.png" /></p>
<h2 id="💖프롬포트-스타일-선택">💖프롬포트 스타일 선택</h2>
<p>계속해서 다양한 프롬프트 스타일을 선택할 수 있는 질문이 뜬다. 자신의 취향에 맞게 선택하면 된다.
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/d7504d94-8e27-45ff-8945-22c829a7b8a9/image.png" />
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/b2ac0d55-2d5b-4ae6-ab55-447b7fb75a5b/image.png" />
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/6b6d2a0d-b64c-41b4-b92a-7a65a9dee749/image.png" />
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/5a63844a-51ec-4121-a72e-fbcb0ea74b3f/image.png" />
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/df0d14ca-a93d-4776-a3e3-d0c16c8e339e/image.png" />
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/3e0c0aa1-f528-4206-9f17-754daeedd7f7/image.png" />
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/fdf97d42-2822-41c3-a93b-5413521057c5/image.png" />
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/695b1d36-224a-4628-8e24-3f776a206a55/image.png" />
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/6f6216fb-4777-4642-8bc3-1f11d01e0b28/image.png" />
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/d89a0b4a-52b5-4611-8a87-bdb22ee44c98/image.png" />
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/a4abdd43-ae4d-429d-9958-2f4a03b2ebac/image.png" /></p>
<h2 id="🔍instant-prompt-mode">🔍Instant Prompt Mode</h2>
<p><code>Instant Prompt Mode</code>는 Powerlevel10k 테마의 기능으로, 터미널이 실행될 때 즉시 프롬프트를 표시하여 Zsh 초기화 과정이 완료되기를 기다리지 않고도 명령어를 입력할 수 있게 해준다. 
이 모드가 활성화되면 터미널이 조금 더 빠르게 응답할 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/7af8e9b0-5686-47fd-a7fc-45c8962750c0/image.png" /></p>
<ul>
<li>Verbose <ul>
<li>터미널이 실행될 때 프롬프트를 즉시 표시하며, Zsh의 초기화 과정에서 발생하는 출력도 모두 표시된다. </li>
<li>권장되는 옵션</li>
</ul>
</li>
<li>Quiet<ul>
<li>터미널이 실행될 때 프롬프트가 즉시 표시되지만, 초기화 과정에서 발생하는 출력은 표시되지 않는다. </li>
<li>터미널 출력이 간결해지지만, 초기화 중 발생하는 정보가 숨겨진다.</li>
</ul>
</li>
<li>Off<ul>
<li>Instant Prompt 기능 비활성화</li>
<li>프롬프트는 Zsh 초기화가 완료된 후에야 표시된다. </li>
<li>특정 Zsh 설정과 충돌하거나 Instant Prompt가 필요 없다면 선택<h2 id="🔍변경사항-적용">🔍변경사항 적용</h2>
Powerlevel10k 설정 마법사가 완료된 후, 설정 내용을 ~/.zshrc 파일에 적용할지 선택
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/383da223-d0d5-46f2-978a-5e49ef2e5746/image.png" /></li>
</ul>
</li>
<li>Yes<ul>
<li>마법사가 생성한 설정이 ~/.zshrc 파일에 자동으로 추가된다. </li>
<li>권장되는 옵션</li>
</ul>
</li>
<li>No. I know which changes to apply and will do it myself.<ul>
<li>마법사가 제안한 설정을 직접 수동으로 추가하거나 수정해야 한다.</li>
</ul>
</li>
</ul>
<h2 id="✨테마-설정-완료">✨테마 설정 완료</h2>
<p>Powerlevel10k 설정 마법사가 끝나면 지정한 테마가 잘 적용된다.
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/18c16168-72d2-4bd0-b8c7-15d0eb2e4e70/image.png" /></p>
<p>하지만 보라색 뾰족한 부분이 미묘하게 어긋난게 거슬렸다..
폰트 크기가 12로 되어있었는데 14로 바꾸니까 해결되었다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/76779588-7913-4a5e-ba99-74e1264c0435/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/56030115-20ff-4627-8040-a7d028dc4caf/image.png" /></p>