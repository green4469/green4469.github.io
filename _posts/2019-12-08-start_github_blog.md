---
title: "Jekyll, Github Pages, Minimal Mistakes 로 시작하는 깃허브 블로그 튜토리얼"
header:
  image: https://live.staticflickr.com/8084/8396909762_813a2b1829_h.jpg
categories:
  - blog
tags:
  - jekyll
  - ruby
  - github pages
toc: true
toc_label: "목차"
toc_icon: "heart"
toc_sticky: true
---

가장 쉽게 나만의 깃허브 블로그를 시작하는 방법을 알려드립니다.

인터넷을 뒤져 깃허브 블로그를 만드는 방법을 설명한 포스트를 보면 자세한 설명 없이 "이걸 눌러라, 저걸 입력해라. 짜잔~" 이런식으로 설명합니다. 개념을 모르니 버전이 바뀌거나 설정이 다르면 에러가 발생하고 따라할 수 없는 상황이 발생하더군요.

개인적으로 찾아보면서 고생도 했고, 시원하게 원리부터 설명해주는 튜토리얼이 없어 제가 직접 만들어봤습니다.

저는 기본적인 개념은 숙지하고 진행해야 나중에 막히는 상황이나 커스터마이징 할 상황이 올 때 응용할 능력이 길러진다고 생각합니다.

그러니 일단 Jekyll, Github Pages 를 먼저 설명하고 튜토리얼을 진행하겠습니다.

# 개념 잡고 가기

## Jekyll

> Jekyll 은 아주 심플하고 블로그 지향적인 정적 사이트 생성기입니다. - [Jekyll 공식 홈페이지 문서](https://jekyllrb-ko.github.io/docs/home/)

Jekyll 을 가장 잘 설명한 문장입니다. 여러분이 블로그 포스트를 마크다운 형식의 문서(md 파일)로 작성하면 Jekyll 은 이를 컴파일해서 html 파일로 만들어줍니다. (웹에서 보이는 페이지는 html 파일이란 것은 잘 알고 계시죠?)

말로만 들으면 감이 오지 않으니, 실제로 마크다운 파일을 만들고 빌드하는 간단한 예시를 들어보겠습니다.

먼저 마크다운 파일을 보실게요.

```
# Overview
자바로 어느정도 규모가 있는 프로젝트를 진행하다보면, 빌드 프로세스가 복잡해집니다. 컴파일러는 코드를 기계어로 번역하고 최적화하는 것에는 통달해 있지만, 빌드 프로세스까지 책임져주지는 않기 때문입니다. 매번 빌드하기 위해 콘솔에 복잡한 명령어들을 반복하여 입력하다 보면, 자동화할 수는 없을까 하는 생각이 듭니다. 이런 요구를 충족시키기 위해 만들어진 것이 빌드 자동화 시스템 [Gradle](https://gradle.org/) 입니다.

Gradle이 자바 전용은 아닙니다. 자바 뿐만아니라 C++, 파이썬과 같이 다양한 메이저 프로그래밍 언어들을 지원합니다. 하지만 C++ 에는 Makefile 이 존재하고, 파이썬은 애초에 컴파일 언어가 아니란 점 등을 고려하면 Gradle 로 가장 큰 편리함을 얻을 수 있는 언어는 역시 자바가 아닐까하는 생각이 듭니다. 

> We do truly feel that Gradle is the best build system for the JVM…
*– Justin Ryan, Senior Software Engineer at Netflix*
```

아래는 Jekyll 이 위의 마크다운 파일을 빌드해 생성된 html 파일입니다.

```html
<h1 id="overview">Overview</h1>
<p>자바로 어느정도 규모가 있는 프로젝트를 진행하다보면, 빌드 프로세스가 복잡해집니다. 컴파일러는 코드를 기계어로 번역하고 최적화하는 것에는 통달해 있지만, 빌드 프로세스까지 책임져주지는 않기 때문입니다. 매번 빌드하기 위해 콘솔에 복잡한 명령어들을 반복하여 입력하다 보면, 자동화할 수는 없을까 하는 생각이 듭니다. 이런 요구를 충족시키기 위해 만들어진 것이 빌드 자동화 시스템 <a href="https://gradle.org/">Gradle</a> 입니다.</p>

<p>Gradle이 자바 전용은 아닙니다. 자바 뿐만아니라 C++, 파이썬과 같이 다양한 메이저 프로그래밍 언어들을 지원합니다. 하지만 C++ 에는 Makefile 이 존재하고, 파이썬은 애초에 컴파일 언어가 아니란 점 등을 고려하면 Gradle 로 가장 큰 편리함을 얻을 수 있는 언어는 역시 자바가 아닐까하는 생각이 듭니다.</p>

<blockquote>
  <p>We do truly feel that Gradle is the best build system for the JVM…
  <em>– Justin Ryan, Senior Software Engineer at Netflix</em></p>
</blockquote>
```

간단하죠? 여러분 마크다운 파일만 작성해서 Jekyll 에게 넘겨주면 알아서 복잡한 html 파일을 만들어줍니다.

마크다운 문법을 이해하셔야 문서를 작성할 수 있습니다. [여기](https://www.markdownguide.org/basic-syntax/)서 마크다운 문법을 학습하실 수 있습니다.

## Github Pages

Jekyll 은 여러분이 작성한 포스트를 html 파일로 만들어주는 고마운 녀석입니다. 하지만, 그뿐입니다. html 파일을 서버에 올려놔야 다른 사람들이 열람할 수 있습니다. 호스트를 만들고, 서버를 구축해 도메인을 할당하는 일은 굉장히 번거로운 작업입니다. 우리는 단순히 문서를 업로드해서 다른 사람들에게 보여주고 싶을 뿐인데 말이죠.

여러분을 위해 서버를 대신 구축해주는 서비스가 바로 Github Pages 입니다. Github 계정을 만들어 Repository 를 생성해 이곳에 우리 블로그를 업로드하면 Github 서버가 대신 호스팅합니다.

{: .notice--info}
Github Pages 는 서버를 대체하는 서비스가 아닙니다! 정적 페이지(블로그 포스트, 이미지 등)만을 호스팅해주며 데이터베이스가 수반되는 작업은 수행할 수 없습니다. (AWS 가 아니에요~)

요약하면 여러분이 블로그 포스트를 작성하는 프로세스는 다음과 같습니다.

1. 마크다운 파일로 문서를 작성한다.
2. Jekyll 로 빌드해 작성한 문서가 내 블로그에 어떻게 보이는지 확인한다.
3. 만족스러우면 Github 에 push 한다.
4. 블로그 url 로 접속해 정상적으로 업로드 됐는지 확인한다.

# 튜토리얼

## 루비(Ruby) 설치
Jekyll 은 루비(Ruby)라는 프로그래밍 언어를 사용해 만들어졌습니다. Jekyll 을 이용해 빌드하기 위해서는 Ruby 를 설치해야합니다.

루비를 설치하는 방법에는 여러가지가 있겠지만, Rvm 을 이용하는 방법이 가장 좋습니다. [Rvm](https://rvm.io/) 은 루비 버전 매니저로 다양한 버전의 루비를 설치하고
필요한 순간에 필요한 버전을 사용할 수 있도록 해줍니다.

Rvm 의 설치 방법은 [여기](https://rvm.io/rvm/install)에서 확인하실 수 있습니다. 우분투에서 설치하는 방법은 아래와 같습니다.

```console
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository -y ppa:rael-gc/rvm
$ sudo apt-get update
$ sudo apt-get install rvm
```

Rvm 을 설치하셨다면 루비를 설치하는 방법은 간단합니다!

```console
$ rvm install ruby
```

최신 버전의 루비 설치가 완료됐습니다. :+1:

{: .notice--info}
Rvm 설치가 어려우신 분은 그냥 루비를 직접 설치하셔도 됩니다. 반드시 Rvm 이 먼저 설치돼야하는 것은 아닙니다. 단지 나중에 다른 루비 버전이 필요하다던가 하는 상황이 오면, Rvm 으로 설치했을 때는 쉽게 루비 버전을 바꿀 수 있으나 직접 루비를 설치했으면 환경변수를 바꿔주는 등 귀찮은 작업이 수반됩니다. 조삼모사냐 조사모삼이냐의 문제죠.

## Github Repository 만들기

블로그를 업로드하려면 깃허브 레포지토리가 필요합니다.

[Github](https://github.com/) 회원가입을 완료하고 로그인 해주세요. 그리고 새 Repository 를 생성합니다.

![create new repository](/assets/images/2019-12-08-start_github_blog/create_repository.png)

레포지토리를 생성할 때 중요한 부분은 **Repository name** 입니다. 이름을 "{자신의 Github 아이디}.github.io" 로
 설정해야 Github 가 Github Pages 블로깅을 위한 레포지토리라고 인식합니다. 제 경우엔 깃허브 아이디가 "green4469" 이기 때문에 "green4469.github.io" 로 레포지토리 네임을 설정했습니다. (레포지토리 네임은 나중에 여러분의 블로그 주소가 됩니다. 제 블로그 주소가 https://green4469.github.io 인 이유죠.)

## Minimal Mistakes 테마로 시작하기

빈 레포지토리가 생성됐으니 이를 우리의 컴퓨터로 가져오겠습니다. 적당한 디렉토리로 이동해 터미널을 실행해주세요.

```console
$ git clone https://github.com/{자신의 Github 아이디}.github.io.git
```

처음부터 Jekyll 프로젝트를 생성해 시작할 수도 있지만, 이미 만들어진 좋은 테마들이 많습니다. 이 블로그의 테마인 [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) 테마로 블로그를 만들어봅시다.

Minimal Mistakes 테마 제공자가 만들어 놓은 starter 레포지토리가 있습니다. 우리는 이 레포지토리를 가져와 내용물을 우리 프로젝트에
복사할 것입니다.

```console
$ git clone https://github.com/mmistakes/mm-github-pages-starter.git
```

이제 두 폴더가 생겼을 것입니다. 하나는 우리가 방금 생성한 빈 레포지토리를 클론한 "{자신의 Github 아이디}.github.io.git}" 이고 
나머지 하나는 Minimal Mistakes 스타터 레포지토리를 클론한 "mm-github-pages-starter" 입니다. 이제 후자의 내용물을 전자로 옮기는 일을 합니다.

파일 탐색기로 복사 & 붙여넣기 하셔도 되고, 커맨드라인을 이용하셔도 좋습니다. 커맨드라인을 입력하실 경우 아래의 커맨드를 터미널에 입력해주세요.

```console
$ cp -rf mm-github-pages-starter/ {자신의 Github 아이디}.github.io/
$ rm -rf mm-github-pages-starter/
```

먼저 로컬에서 여러분의 블로그가 잘 만들어졌는지 확인해봅시다. "{자신의 Github 아이디}.github.io" 디렉토리로 이동해 아래의 커맨드를 입력합니다.

```console
$ bundle install
$ jekyll serve
```

"bundle install"은 필요한 루비 의존성 패키지들을 자동으로 설치하는 커맨드입니다. 이것을 통해 Jekyll 이 설치되죠!

"jekyll serve"는 jekyll 로 블로그를 빌드하고 개발 서버를 띄우는 커맨드입니다.

이제 브라우저를 키고 주소창에 "127.0.0.1:4000"을 입력해보세요. 여러분만의 블로그가 보이실겁니다! 

![create new repository](/assets/images/2019-12-08-start_github_blog/blog.png)

위의 이미지는 제 블로그입니다. 여러분의 것과는 약간 다르겠지만, 거의 비슷한 느낌이지 않나요?

## Github Pages 로 블로그 호스팅하기

여러분이 방금 보신 블로그는 여러분의 컴퓨터에서만 볼 수 있습니다. 다른 사람들은 열람할 수 없습니다.

Github 레포지토리에 여러분의 코드를 업로드해 다른 사람이 블로그를 볼 수 있도록 만들어봅시다.

여러분의 블로그 디렉토리로 이동해 터미널에 아래의 코드를 입력해주세요.

```console
$ git add .
$ git commit -m "initial commit"
$ git push origin master
```

이제 어려분의 코드가 업로드됐습니다. "https://{자신의 Github 아이디}.github.io" 을 브라우저로 들어가보시면 블로그가 보이실겁니다.

## 블로그 커스터마이징

지금까지 수고하셨습니다! 여러분이 한 일을 요약해보면 
1. 최신 버전 루비를 설치하고,
2. 깃허브 레포지토리를 생성했으며,
3. Minimal Mistakes 테마에서 remote theme starter 레포지토리를 클론해, 여러분이 생성한 레포지토리에 업로드했습니다.

정말 많은 일들이 있었네요... 드디어 여러분의 블로그를 호스팅할 수 있었습니다.

하지만 아직 만족하기엔 이릅니다. 여러분을 나타내는 정보가 블로그에 전혀 없기 때문이죠. 이걸 보고 누가 여러분의 블로그라고 생각할 수 있겠어요?

먼저 프로젝트의 루트(최상위 디렉토리)에 존재하는 "_config.yml" 파일을 수정해봅시다. 이 파일엔 블로그 설정이 모여있습니다. 지금은 테마 배포자가 임의로 값을 넣어놨습니다. 이를 여러분의 정보로 바꿔줍시다. 아래는 제 설정 파일의 일부를 가져온 것입니다.

### 블로그 제목, 컬러 스킨, 검색 엔진
```yaml
title: 코드 무민
email: green4469@gmail.com
description: >- # this means to ignore newlines until "baseurl:"
  개발자 무민의 성장 일대기
twitter_username: 
github_username: green4469
minimal_mistakes_skin: "air" # "default", "air", "aqua", "contrast", "dark", "dirt", "neon", "mint", "plum", "sunrise"
search: true
```

따로 설명하지 않아도 키 값을 읽어보시면 어떤 설정인지 감이 오실겁니다. 중요한 부분만 따로 설명해보면,
- 'title' 은 여러분의 블로그 제목에 해당합니다. 블로그 상단 네비게이션 바의 왼쪽에 나타나게되므로 짧고 분명한 어구를 쓰시는 것이 좋습니다.
- 'minimal_mistakes_skin' 은 테마의 컬러 스킨을 의미합니다. 여러 가지 적용해보시고 마음에 드는 것으로 결정하세요.
- 'search' 는 여러분의 블로그가 웹으로 검색할 경우 나타나는지에 관한 것입니다. 이것이 true 이면 구글 검색 엔진이 여러분의 블로그를 크롤링할 것입니다.

### 프로필 관리

블로그의 프로필을 관리할 수 있습니다. 지금은 카카오톡 기본 프로필사진같은 이미지로 프로필 이미지가 나타날텐데요, 이것도 바꾸고 그 아래에 있는 여러분에 대한 설명과 링크들도 수정해봅시다.

아까처럼 "_config.yml" 파일을 수정해줍니다.

```yaml
author:
  name   : "김유민"
  avatar : "/assets/images/moomin-sit-down2.jpg"
  bio    : "연세대학교 컴퓨터과학 전공<br/><br/> 우아한테크코스 1기 수료<br/><br/> 우아한형제들 서비스인프라실 시스템신뢰성개발팀(SRE)<br/><br/> 주니어 서버(백엔드) 개발자"
  links:
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/green4469/"
    - label: "Linkedin"
      icon: "fab fa-fw fa-linkedin"
      url: "https://www.linkedin.com/in/yuminkimdev/"
    - label: "Email"
      icon: "fas fa-fw fa-envelope-square"
      url: mailto:green4469@gmail.com

footer:
  links:
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/green4469/"
    - label: "Linkedin"
      icon: "fab fa-fw fa-linkedin"
      url: "https://www.linkedin.com/in/yuminkimdev/"
```

author 는 페이지 좌측에 나타나는 항목이고, footer 는 페이지 하단에 나타나는 항목입니다. 이미지는 웹에 존재하는 이미지의 주소를 입력하여도 되고, 여러분이 프로젝트에 저장하여 상대 경로로 참조해 줄수도 있습니다. 이미지 크기는 정사각형의 비율이어야 테마에 잘 어울립니다.

bio 는 여러분에 대한 짧은 설명입니다. 저 문자열 그대로 html 파일에 들어가기 때문에 엔터를 쳐도 줄바꿈이 되지 않습니다. 그럴 땐 제가 한 것처럼 br 태그를 이용하시면 됩니다.

links 는 여러분의 sns 나 링크드인, 깃허브 주소를 넣을 수 있습니다. 적절한 아이콘은 [Font Awesome](https://fontawesome.com/) 에서 찾으실 수 있습니다.

## 새 글 포스트하기

이제 조금 여러분의 블로그처럼 보일겁니다. 하지만 블로그에 보이는 포스트들이 여러분이 작성한 것이 아니라는 문제가 있습니다. 테마 제작자가 기본으로 넣어 놓은 더미 포스트들입니다.

프로젝트 루트의 "_posts" 디렉터리에 마크다운 파일들이 있습니다. 이녀석들이 아까 본 더미 포스트들입니다. 여러분도 이렇게 마크다운 형식으로 블로그 포스트를 작성해야합니다.

{: .notice--info}
앞에서 언급했듯이 Jekyll 은 마크다운 파일을 읽어들여 html 파일을 생성해주는 정적 사이트 생성기입니다. 블로그 포스트를 마크다운 형식으로 작성해야하는 이유이죠.

"2010-01-07-post-standard.md" 파일만 남겨놓고 나머지는 지웁니다. 우리는 이 파일을 수정해 여러분의 첫 블로그 포스트를 만들겁니다. 

먼저 파일의 이름을 바꿔줍니다. "2010-01-07" 부분을 오늘 날짜로 바꾸고, "post-standard" 부분을 원하는 이름으로 바꿔줍니다. 날짜는 포스트의 생성시각으로 반영되고 이름은 해당 포스트의 url 주소로 반영됩니다.

이름을 바꾸었으면 파일을 열어봅니다.

```yaml
---
title: "Post: Standard"
excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - Post Formats
  - readability
  - standard
---

... 본문
```

중요한건 대쉬라인(---) 사이에 있는 내용들입니다. 이 부분을 포스트의 '메타데이터'라고 부르는데요, 메타데이터는 포스트의 설정을 나타냅니다. 실제로 보여지는 부분은 본문이고, 메타데이터는 보여지지 않습니다.

메타데이터에는 크게 title, categories, tags가 있습니다.
- title 은 포스트의 제목을 의미합니다. 
- categories 는 포스트의 분류를 의미하는데요, 포스트를 가장 잘 나타낼 수 있는 하나의 카테고리를 적어주시면 됩니다.
- tags 는 카테고리와 달리 여러 개를 지정하는 게 좋습니다. 이 포스트와 관련된 키워드들을 태그로 달아줍시다.

카테고리와 태그는 아래 사진처럼 나중에 포스트를 찾는 중요한 단서가 되기때문에 빼먹지 말고 적어줍시다!

![카테고리의 효용](/assets/images/2019-12-08-start_github_blog/categories.png)

본문은 여러분이 채워넣고 싶은 내용을 마음껏 적으면 됩니다. 물론 마크다운 형식을 따라야합니다.

# 응용

## 포스트에 목차 추가하기

## 댓글 기능 추가하기

# 마무리

막상 튜토리얼을 만들고나니 개발자가 아니고서야 쉽게 따라하기는 어려워 보입니다. 깃허브 블로그는 역시 접근성이 아쉽네요. 

하지만 개발자 전용 블로그로는 이만한 게 없는 것 같네요. (깃허브에 잔디 심기에도 좋고 ^^) 

# References
커버 이미지: https://live.staticflickr.com/8084/8396909762_813a2b1829_h.jpg
