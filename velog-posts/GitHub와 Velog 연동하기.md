<blockquote>
<p><em>Velog에 글을 쓸 때 잔디가 심긴다면 좀 더 동기 부여가 되지 않을까?</em></p>
</blockquote>
<p>요새 벨로그 포스팅이 좀 뜸해지고 있었는데, 주변 사람을 통해 벨로그 글 쓰면 깃허브 잔디가 심을 수 있다는 얘기를 듣게 되었다.
깃허브 잔디가 동기부여가 되어서 1일 1커밋 이상을 하고 있는 나에게는 흥미로운 소식이었다. 
깃허브 잔디가 심어진다면 글 쓰는 것 자체가 더 큰 동기부여가 될 것 같았다. 
그래서 바로 어떻게 연동할 수 있는지 알아보았다.</p>
<h1 id="1️⃣-github-repository-생성-및-clone">1️⃣ GitHub repository 생성 및 clone</h1>
<ul>
<li>Public repository로 생성한 다음, 초록색 Code 버튼을 눌러 URL을 복사해 clone한다.
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/e4427df2-4586-4b51-b7a4-1ac741589594/image.png" /></li>
</ul>
<pre><code>// git clone https://github.com/hjoo830/velog.git
git clone (복사한 URL)</code></pre><h1 id="2️⃣-파일-생성">2️⃣ 파일 생성</h1>
<ul>
<li>아래 사진과 같은 파일 구조를 생성한다.
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/3a8c0c79-c535-4d28-8fc4-dedc1ebbf5e3/image.png" /></li>
</ul>
<h2 id="⚙️-update_blogyml">⚙️ update_blog.yml</h2>
<p>update_blog.yml 파일에 github action을 작성한다. 
매일 자정 또는 해당 repository에 push 될 때 파이썬 스크립트를 실행하는 코드이다.
<code>hjoo830</code>이라고 적힌 부분엔 본인의 github 아이디를, velog 라고 적힌 부분엔 본인의 repository 이름을 넣으면 된다.</p>
<pre><code>name: Update Blog Posts

on:
  push:
    branches:
      - main
  schedule:
    - cron: '0 0 * * *' # 매일 자정에 실행

jobs:
  update_blog:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Push changes
        run: |
          git config --global user.name 'github-actions[bot]'
          git config --global user.email 'github-actions[bot]@users.noreply.github.com'
          git pull origin main --rebase
          git push https://${{ secrets.GH_PAT }}@github.com/hjoo830/velog.git
          // git push https://${{ secrets.GH_PAT }}@github.com/[깃허브 아이디]/[레포 이름].git

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.x'

      - name: Install dependencies
        run: |
          pip install feedparser gitpython

      - name: Run script
        run: python scripts/update_blog.py</code></pre><h2 id="💻-update_blogpy">💻 update_blog.py</h2>
<p>실행될 파이썬 스크립트이다.
마찬가지로 <code>hjoo830</code>이라고 적힌 부분엔 본인의 velog 아이디를 넣으면 된다.</p>
<pre><code>import feedparser
import git
import os

# 벨로그 RSS 피드 URL
rss_url = 'https://api.velog.io/rss/@hjoo830'

# 깃허브 레포지토리 경로
repo_path = '.'

# 'velog-posts' 폴더 경로
posts_dir = os.path.join(repo_path, 'velog-posts')

# 'velog-posts' 폴더가 없다면 생성
if not os.path.exists(posts_dir):
    os.makedirs(posts_dir)

# 레포지토리 로드
repo = git.Repo(repo_path)

# RSS 피드 파싱
feed = feedparser.parse(rss_url)

# 각 글을 파일로 저장하고 커밋
for entry in feed.entries:
    # 파일 이름에서 유효하지 않은 문자 제거 또는 대체
    file_name = entry.title
    file_name = file_name.replace('/', '-').replace('\\', '-').replace('?', '').replace(':', '').replace('*', '').replace('&lt;', '').replace('&gt;', '').replace('|', '').strip()
    file_name += '.md'
    file_path = os.path.join(posts_dir, file_name)

    # 파일이 이미 존재하지 않으면 생성
    if not os.path.exists(file_path):
        with open(file_path, 'w', encoding='utf-8') as file:
            file.write(entry.description)  # 글 내용을 파일에 작성

        # 깃허브 커밋
        repo.git.add(file_path)
        repo.git.commit('-m', f'Add post: {entry.title}')

# 변경 사항을 깃허브에 푸시
repo.git.push()</code></pre><h3 id="🔄-수동-실행-트리거-추가">🔄 수동 실행 트리거 추가</h3>
<p>update_blog.yml 파일에 <code>workflow_dispatch:</code> 를 추가하면 필요할 때마다 Actions를 수동으로 실행할 수 있다.
매일 자정에 자동으로 실행되지만, 잘 연동된건지 테스트하거나 바로바로 반영하고 싶을 때 수동으로 실행할 수 있으면 편할 것 같아서 추가했다.</p>
<pre><code>name: Update Blog Posts

on:
  push:
    branches:
      - main
  workflow_dispatch: # 수동 실행 트리거 추가
  schedule:
    - cron: '0 0 * * *' # 매일 자정에 실행

jobs:
  update_blog:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Push changes
        run: |
          git config --global user.name 'github-actions[bot]'
          git config --global user.email 'github-actions[bot]@users.noreply.github.com'
          git pull origin main --rebase
          git push https://${{ secrets.GH_PAT }}@github.com/hjoo830/velog.git

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.x'

      - name: Install dependencies
        run: |
          pip install feedparser gitpython

      - name: Run script
        run: python scripts/update_blog.py</code></pre><h3 id="🧑💻-커밋-작성자-설정">🧑‍💻 커밋 작성자 설정</h3>
<p>위의 코드로 연동하면, 벨로그 글들이 깃허브에 커밋될 때 작성자가 github-actions[bot]으로 된다.
내 계정으로 커밋을 하기 위해서 update_blog.py 파일의 코드를 수정했다.</p>
<pre><code>name: Update Blog Posts

on:
  push:
    branches:
      - main
  workflow_dispatch: # 수동 실행 트리거 추가
  schedule:
    - cron: '0 0 * * *' # 매일 자정에 실행

jobs:
  update_blog:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Push changes
        env:
          GH_EMAIL: ${{ secrets.GH_EMAIL}}
          GH_NAME: ${{ secrets.GH_NAME}}
        run: |
          git config --global user.name '${{ env.GH_NAME}}'
          git config --global user.email '${{ env.GH_EMAIL}}'
          git pull origin main --rebase
          git push https://${{ secrets.GH_PAT }}@github.com/hjoo830/velog.git


      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.x'

      - name: Install dependencies
        run: |
          pip install feedparser gitpython

      - name: Run script
        run: python scripts/update_blog.py</code></pre><h1 id="3️⃣-personal-access-tokens">3️⃣ Personal access tokens</h1>
<ul>
<li><p>Settings - Developer Settings - Personal access tokens - Tokens (classic) - Generate new token - Generate new token (classic)
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/7b21489a-ff6f-4750-864a-150f0331b2c9/image.png" /></p>
</li>
<li><p>Note에 토큰 이름을 쓰고 원하는 유효기간을 선택한 뒤, repo와 workflow 체크해주고 Generate new token을 누른다.
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/f60c726d-9237-41db-acb2-72d2e81bc73e/image.png" /></p>
</li>
<li><p>그러면 토큰이 생성되는데, 한 번만 볼 수 있으므로 <strong>반드시 복사</strong>해 둔다.</p>
</li>
</ul>
<h1 id="4️⃣-repository-secret">4️⃣ Repository Secret</h1>
<ul>
<li>1️⃣에서 생성한 repository의 Settings - Secrets and variables - Actions - New Repository Secret</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/hjoo830/post/95b66efe-3928-495e-abdb-b61e6de356db/image.png" /></p>
<ul>
<li><p>Name에 <code>GH_PAT</code>를 쓰고 Secret에 3️⃣에서 복사한 토큰을 붙여넣는다
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/5df68386-280a-4b3f-a00b-21283439e79e/image.png" /></p>
</li>
<li><p>2️⃣에서 update_blog.yml을 첫번째 코드로 했다면 GH_PAT만 추가하면 되고, 커밋 작성자 설정도 했다면 본인의 user.name과 user.email을 넣어 총 3개를 추가하면 된다 
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/6cd35f0f-7928-42a7-a7d8-d3199ccc6ded/image.png" /></p>
</li>
</ul>
<h3 id="✅-username과-useremail-확인하는-방법">✅ user.name과 user.email 확인하는 방법</h3>
<pre><code>git config user.name
git config user.email</code></pre><h1 id="5️⃣-확인하기">5️⃣ 확인하기</h1>
<ul>
<li><p>update_blog.yml 파일이 매일 자정 또는 해당 repository에 push 될 때 파이썬 스크립트를 실행하는 코드였으므로 새로운 커밋을 push 해보거나 자정까지 기다려서 기존 velog 글이 잘 커밋되는지 확인한다.</p>
</li>
<li><p>수동 실행 트리거를 추가했다면?</p>
<ul>
<li>Actions - Update Blog Posts(또는 update_blog.yml에서 name에 적은 이름) - Run workflow 를 눌러 수동 실행
<img alt="" src="https://velog.velcdn.com/images/hjoo830/post/6204a982-42a1-413c-b79c-4e7a12b79045/image.png" /></li>
</ul>
</li>
<li><p>초록색 체크모양이 뜨고 velog-posts 폴더 내에 velog 글들이 잘 올라왔다면 연동 성공!!</p>
</li>
</ul>
<p>🔗 참고 블로그
<a href="https://velog.io/@sooozi/velog%EC%99%80-github-%EC%97%B0%EB%8F%99-%EB%B2%A8%EB%A1%9C%EA%B7%B8-%EA%B8%80%EC%93%B0%EA%B3%A0-%EC%9E%94%EB%94%94%EC%8B%AC%EA%B8%B0">https://velog.io/@sooozi/velog%EC%99%80-github-%EC%97%B0%EB%8F%99-%EB%B2%A8%EB%A1%9C%EA%B7%B8-%EA%B8%80%EC%93%B0%EA%B3%A0-%EC%9E%94%EB%94%94%EC%8B%AC%EA%B8%B0</a></p>