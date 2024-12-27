<p>iTerm2의 색상 테마는 터미널 창의 배경색, 글자색, 강조 색상 등을 지정한다.</p>
<h1 id="🛠️homebrew-설치">🛠️Homebrew 설치</h1>
<p>Homebrew는 macOS에서 사용되는 오픈 소스 패키지 관리자이다.
<a href="https://brew.sh/">https://brew.sh/</a> 로 들어가서 명령어를 복사한 뒤, 터미널에 붙여넣고 비밀번호를 입력한다. (Mac 로그인 비밀번호)</p>
<pre><code>/bin/bash -c &quot;$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)&quot;</code></pre><p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/95e1312d-dd21-4420-a6b3-2cf16e33d951/image.png" /></p>
<p><code>Press RETURN/ENTER to continue or any other key to abort:</code>가 뜨면 엔터 입력</p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/0fd1f08f-2c29-4676-9c2a-8f2ce522d7e3/image.png" /></p>
<p><code>Run these two commands in your terminal to add Homebrew to your PATH:</code> 아래의 두줄을 각각 복사해서 붙여넣으면 설치 완료</p>
<p><code>brew -v</code> 명령어로 설치된 것을 확인할 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/f2a32a1b-d2c1-468c-90e9-dbbc3176ccb5/image.png" /></p>
<h1 id="🛠️iterm2-설치">🛠️iTerm2 설치</h1>
<p>iTerm2는 macOS에서 사용할 수 있는 대체 터미널 응용 프로그램이다.</p>
<p><code>brew install iterm2</code> 입력
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/ea9c1506-aa36-4279-bba1-e3a9ef16b3d4/image.png" /></p>
<h1 id="🛠️oh-my-zsh-설치">🛠️oh my zsh 설치</h1>
<p>Oh My Zsh는 zsh 셸 환경을 개선하고 확장하기 위한 오픈 소스 프레임워크이다.</p>
<p><code>brew install zsh</code></p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/e759271c-cddc-4b55-9820-4522ef0a287a/image.png" /></p>
<p><a href="https://ohmyz.sh/#install">https://ohmyz.sh/#install</a> 로 들어가서 명령어를 복사한 뒤, 터미널에 붙여넣는다.</p>
<pre><code>sh -c &quot;$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)&quot;</code></pre><p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/303922e9-a7ce-4a4a-838c-766eaed0e42d/image.png" /></p>
<h1 id="▶️iterm2-실행">▶️iTerm2 실행</h1>
<h2 id="🫥기본-iterm2-터미널다크-모드">🫥기본 iTerm2 터미널(다크 모드)</h2>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/e9fd7f76-b8a0-414f-b0fc-9e4ea5b49dc2/image.png" /></p>
<h2 id="⚙️기본-테마-설정">⚙️기본 테마 설정</h2>
<p><code>command</code>와 <code>,</code>를 눌러 설정 열기</p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/4138b24d-cd14-490a-86d9-d3a1f2d71f43/image.png" /></p>
<h2 id="⬇️테마-다운로드">⬇️테마 다운로드</h2>
<p><a href="https://iterm2colorschemes.com/">https://iterm2colorschemes.com/</a> 에 들어가서 원하는 테마의 이름을 누른 뒤, url을 복사한다.</p>
<h3 id="🛠️curl-설치">🛠️curl 설치</h3>
<p><code>brew install curl</code>
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/def460dc-b9de-4ad3-a74f-ad81ad86e48b/image.png" /></p>
<h3 id="📂util-디렉토리-생성-후-이동">📂util 디렉토리 생성 후 이동</h3>
<p><code>mkdir util &amp;&amp; cd util</code></p>
<p><code>curl -LO [url]</code> 입력</p>
<p><code>curl -LO https://raw.githubusercontent.com/mbadolato/iTerm2-Color-Schemes/master/schemes/Dracula%2B.itermcolors</code>
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/e216b59d-9f9e-4776-871e-998d126519fe/image.png" /></p>
<h3 id="🌈컬러-테마-설정">🌈컬러 테마 설정</h3>
<p>Setting - Profiles - Colors - Color Presets
util 폴더에서 다운로드 받은 파일을 import 해준 후 설정해준다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/4e9b2eeb-8fc3-4534-84a0-7a046dde7075/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/1bf182d2-4f3b-43f2-919d-95e8186ca380/image.png" /></p>
<p>여기까지 하면 터미널 창의 배경색, 글자색, 강조 색상 등 색상 테마를 바꿀 수 있다. 
아래와 같이 프롬포트 테마를 설정해 터미널을 꾸밀 수 있는데, 이건 다음 포스트에서 다루었다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/677f00ad-8ecc-4c50-92da-0b67c57ec251/image.png" /></p>