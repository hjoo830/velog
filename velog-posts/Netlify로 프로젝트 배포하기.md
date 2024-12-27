<h1 id="🌐netlify란">🌐Netlify란?</h1>
<blockquote>
<p>정적 웹사이트와 프론트엔드 애플리케이션을 간편하게 배포하고 관리할 수 있는 클라우드 플랫폼</p>
</blockquote>
<ul>
<li>AWS로도 배포할 수 있지만, Netlify는 Git과 연동하여 자동으로 빌드와 배포가 진행되기 때문에 설정이 더 간단하다.</li>
<li>GitHub에 커밋할 때마다 Netlify가 변경사항을 감지해 자동으로 사이트를 최신 상태로 업데이트해 주기 때문에 편리하다.</li>
</ul>
<h1 id="🚀netlify로-프로젝트-배포하기">🚀Netlify로 프로젝트 배포하기</h1>
<h2 id="1️⃣-새-사이트-추가">1️⃣ 새 사이트 추가</h2>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/adfa615e-7242-4550-a57e-470b70fed808/image.png" /></p>
<p><a href="https://www.netlify.com/">Netlify</a> 사이트에 로그인 후, <code>Add new site</code> - <code>import an existing project</code> 버튼을 클릭한다.</p>
<h2 id="2️⃣-연결할-플랫폼-선택">2️⃣ 연결할 플랫폼 선택</h2>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/26b793fb-0e6b-44ad-8e71-e7b4284dfbb3/image.png" />
배포할 프로젝트가 있는 Git 저장소를 선택한다.</p>
<h2 id="3️⃣-배포할-프로젝트-레포지토리-선택">3️⃣ 배포할 프로젝트 레포지토리 선택</h2>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/8c3a173f-69a6-40e4-91c7-b5a23f240de0/image.png" />
GitHub 선택하고 Authorized 하면</p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/655fad73-28db-4ca4-b156-8ef87c72f431/image.png" /></p>
<p>GitHub에 있는 레포지토리 목록이 나타난다.
이 중에 배포할 프로젝트를 선택한다.</p>
<h2 id="4️⃣-배포-설정">4️⃣ 배포 설정</h2>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/927e9914-d711-4fd5-87c0-9b0ecd05da0d/image.png" /></p>
<p>배포할 사이트 이름을 작성하고, 사용 가능한지 확인한다.
URL은 <code>https://작성한이름.netlify.app</code> 형식이 된다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/93f7a9cf-dad1-429e-b78b-af9ecaa638dc/image.png" /></p>
<p>빌드 설정을 한다.</p>
<ul>
<li>Branch to deploy<ul>
<li>어떤 브랜치를 기준으로 배포할지 선택한다.</li>
<li>일반적으로 main이나 master 브랜치를 선택한다.</li>
</ul>
</li>
<li>Base directory<ul>
<li>프로젝트의 루트 디렉토리 지정한다. </li>
<li>프론트엔드와 백엔드가 같은 저장소에 있는 경우 프론트엔드 디렉토리를 지정해 해당 폴더만 배포하게 할 수 있다.</li>
<li>프론트엔드 코드만 있는 경우 빈칸으로 두면 된다.</li>
</ul>
</li>
<li>Build command<ul>
<li>프로젝트를 빌드할 때 사용하는 명령어를 입력한다. 이때, 기본으로 <code>npm run build</code>가 입력되어 있는데, 그대로 하면 에러 난다. <code>CI= npm run build</code>으로 해야된다.</li>
<li>CI 환경에서는 테스트 실패를 에러로 처리하기 때문에 <code>CI=</code>를 앞에 붙여 테스트를 무시하도록 설정해야 빌드가 정상적으로 진행된다.</li>
</ul>
</li>
<li>Publish directory<ul>
<li>빌드가 완료된 후 생성되는 폴더 이름이다.</li>
</ul>
</li>
<li>Functions directory<ul>
<li>서버리스 함수를 사용할 때 필요한 디렉토리이다.</li>
</ul>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/3799005f-4a05-42ff-b88a-f38db4d63df1/image.png" /></p>
<p>필요한 경우 환경 변수를 추가한다.</p>
<p>모든 설정이 완료되면 <code>Deploy {사이트 이름}</code> 버튼을 클릭해 배포를 시작한다.</p>
<h2 id="5️⃣-배포-완료">5️⃣ 배포 완료</h2>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/ab1758a2-3dbc-43de-ba97-81bb0958f5b3/image.png" /></p>
<p>배포가 진행 중일 때는 <code>Site deploy in progress</code>라는 문구가 표시된다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/3727da54-16ec-4e9b-9b1e-bd2a4345ddca/image.png" /></p>
<p>배포가 완료되면 웹 사이트 주소가 나타나고, 들어가보면 성공적으로 배포가 된 것을 확인할 수 있다.</p>
<p>추가적으로 사이트 보안을 위해 HTTPS를 설정하거나 도메인을 연결할 수 있다.</p>