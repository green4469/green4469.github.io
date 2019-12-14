---
title: "Jekyll, Github Pages, Minimal Mistakes 로 시작하는 블로깅 튜토리얼"
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

{: .notice--danger}
아직 완성되지 않은 포스트입니다!

이런 류의 블로그 포스트를 보면 자세한 설명 없이 "이걸 눌러라, 이걸 입력해라. 짜잔~" 이런식으로 설명하더군요.

저는 기본적인 개념은 숙지하고 진행해야 나중에 막히는 상황이나 커스터마이징 할 상황이 올 때 응용할 능력이 길러진다고 생각합니다.

따라서 Jekyll, Github Pages 를 먼저 설명하고 튜토리얼을 진행하겠습니다.

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

Jekyll 은 여러분이 작성한 포스트를 html 파일로 만들어줍니다. 하지만 여전히 문제가 있죠. html 파일을 서버에 올려놔야 다른 사람들이 열람할 수 있다는 것입니다. 호스트를 만들고 서버를 구축해 도메인을 할당하는 일은 굉장히 번거로운 작업입니다. 우리는 단순히 문서를 업로드해서 다른 사람들에게 보여주고 싶을 뿐인데 말이죠.

여러분을 위해 서버를 대신 구축해주는 서비스가 바로 Github Pages 입니다. Github 계정을 만들어 Repository 를 생성해 이곳에 코드를 업로드하면 Github 서버가 우리의 포스트를 호스팅합니다.

{: .notice--info}
Github Pages 는 서버를 대체하는 서비스가 아닙니다! 정적 페이지(블로그 포스트, 이미지 등)만을 호스팅해주며 데이터베이스가 수반되는 작업은 수행할 수 없습니다.

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

## Github Repository 만들기

[Github](https://github.com/) 회원가입을 완료하고 로그인 해주세요. 그리고 새 Repository 를 생성합니다.

![create new repository](/assets/images/2019-12-08-start_github_blog/create_repository.png)

위 이미지에서 중요한 부분은 **Repository name** 입니다. 이름을 "{자신의 Github 아이디}.github.io" 로
 설정해야 Github 가 Github Pages 블로깅을 위한 레포지토리라고 인식합니다.

## Minimal Mistakes 테마로 시작하기

빈 레포지토리가 생성됐으니 이를 우리의 컴퓨터로 가져오겠습니다. 적당한 디렉토리로 이동해 터미널을 실행해주세요.

```console
$ git clone https://github.com/{자신의 Github 아이디}.github.io.git
```

처음부터 Jekyll 프로젝트를 생성해 시작할 수도 있지만, 이미 만들어진 좋은 테마들이 많습니다. 
이 블로그의 테마인 [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) 테마로 블로그를 만들어봅시다.

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
```

먼저 로컬에서 여러분의 블로그가 잘 만들어졌는지 확인해봅시다. "{자신의 Github 아이디}.github.io" 디렉토리로 이동해 아래의 커맨드를 입력합니다.

```console
$ bundle install
$ jekyll serve
```

위의 커맨드는 필요한 루비 의존성 패키지들을 자동으로 설치하는 커맨드입니다. 이것을 통해 Jekyll 이 설치되죠!

아래의 커맨드는 jekyll 로 블로그를 빌드하고 개발 서버를 띄우는 커맨드입니다.

이제 브라우저를 키고 주소창에 "127.0.0.1:4000"을 입력해보세요. 여러분만의 블로그가 보이실겁니다! 

![create new repository](/assets/images/2019-12-08-start_github_blog/blog.png)

위의 이미지는 제 블로그입니다. 여러분의 것과는 약간 다르겠지만, 거의 비슷한 느낌이지 않나요?

## Github Pages 로 블로그 호스팅하기

여러분이 방금 보신 블로그는 로컬 컴퓨터에서만 볼 수 있습니다. 다른 사람들은 열람할 수 없죠.

Github 레포지토리에 여러분의 코드를 업로드해 다른 사람이 블로그를 볼 수 있도록 만들어 봅시다.

블로그 디렉토리로 이동해 터미널에 아래의 코드를 입력해주세요.

```console
$ git add .
$ git commit -m "initial commit"
$ git push origin master
```

이제 어려분의 코드가 업로드됐습니다. "https://{자신의 Github 아이디}.github.io" 을 브라우저로 들어가보시면 블로그가 보이실겁니다.

## 블로그 커스터마이징

## 새 글 포스트하기

# 응용

## 댓글 기능 추가하기

## 포스트에 목차 추가하기

# References
커버 이미지: https://live.staticflickr.com/8084/8396909762_813a2b1829_h.jpg
