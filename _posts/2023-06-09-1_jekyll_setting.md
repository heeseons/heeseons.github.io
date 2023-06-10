---
title: "[1] Jekyll 기반 GitBlog 생성(Setting)"
layout: post
comments: true
toc: true
category:
- Git
tag:
- jekyll
- gitblog
---

그동안 참여했던 프로젝트 및 공부한 내용의 정리를 위해 사용할 수 있는 다양한 블로그 플랫폼이 존재합니다. \
가장 접근하기 쉬운 네이버 블로그, 개발자들이 흔히 사용하는 티스토리까지 다양하지만, \
저는 UI/UX에 있어서 높은 자율성과 확장성을 갖는 GitBlog를 사용하여 포트폴리오를 정리하고자 합니다.\
Git 초보 입장에서, 초기 세팅부터 많은 난관을 겪었기 때문에 해당 포스팅은 초기 세팅만을 설명하고 있습니다.

---
> 운영체제: mac OS (Ventura)\
> 사용테마: [Chirpy Jekyll Theme](https://github.com/cotes2020/jekyll-theme-chirpy)

<br>
## 1. 로컬 환경설정
### 1.1. Homebrew 설치
간편한 설치를 위해, 본 포스팅에서는 `Homebrew`를 이용합니다.\
한 번 설치해두면 다른 패키지 설치 시에도 유용하게 사용할 수 있습니다.
* 참고: [Homebrew 공식 문서](https://brew.sh/index_ko)

```terminal
$/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

<br>
### 1.2. Ruby 및 Jekyll 설치
Jekyll은 Ruby 기반이므로, Ruby 설치가 선행되어야 합니다.
* 참고: [Jekyll 공식 문서](https://jekyllrb.com/docs/installation/)

Ruby 설치를 위해 Homebrew를 이용하여 chruby와 ruby-install을 설치합니다.
```terminal
$ brew install chruby ruby-install xz
```
```terminal
$ ruby-install ruby 3.1.3
```

<br>
Jekyll을 설치합니다.
```terminal
$ gem install jekyll
```

<br>
Gem을 설치합니다.
```terminal
$ gem install jekyll bundler
```

<br>
## 2. 테마 적용
1을 완료하셨다면 반은 끝난 거예요! ('시작이 반이다'라는 얘기도 있잖아요. ㅎㅎ)\
이제 본격적으로 사용하고 싶은 테마를 찾아봅시다.\
일반적인 블로그는 **블로그 생성 ➡ 테마(디자인) 적용** 순이지만, 깃블로그의 경우에는 두 단계가 한 번에 이루어집니다.\
본 포스팅에서는 `Chrispy Jekyll Theme`를 적용하려고 합니다.\
더 많은 테마는 [Jekyll Themes](https://jekyllthemes.dev)에서 확인 가능합니다.

### 2.1. Git Fork
가장 먼저, 사용하려는 테마를 본인의 Repository에 [Fork](https://github.com/cotes2020/jekyll-theme-chirpy/fork) 해주어야 합니다.\
최종 블로그 생성 후 쉽게 접속하기 위해서 Repository 이름을 `<깃허브 ID>.github.io`로 설정해줍니다. \
이렇게 할 경우에만 `https://<깃허브ID>.github.io`로 접속할 수 있습니다.\
`Create Fork`를 통해 새로운 Repository를 생성해보세요.

<br>
### 2.2. 로컬 환경으로 Clone
본격적인 블로그 생성을 위해, 로컬 환경으로 소스를 내려받아야 합니다.\
**2.1**에서 생성한 본인의 Repository에 들어가면, `Code` 버튼이 존재하는데요, 이걸 눌러주세요.\
다음으로 `Clone` ➡ `HTTPS`에 있는 URL을 복사해주시면 됩니다.\
<br>
이제 터미널에서 본격적인 작업을 시작합니다.\
저의 경우에는 `Git`이라는 폴더에서 모든 Git 작업을 수행하기 때문에, 디렉토리를 이동합니다.
```terminal
$ cd Git
```
다음으로 복사한 링크를 이용해 깃 프로젝트를 복제합니다.
```terminal
$ git clone <복사한 주소>
```
`git clone`을 실행하면 `Git` 폴더 내부에 `<깃허브 ID>.github.io` 폴더가 생성됩니다.\
해당 폴더에서 이제 작업을 하고, `git push`를 통해 서버에 업로드하면 됩니다.

<br>
### 2.3. 정상 설치 확인
기본적인 준비는 끝났습니다.\
로컬에서 실행하여 정상적으로 설치된 것이 맞는지 확인해보겠습니다.
```terminal
$ jekyll serve
```

`jekyll serve`를 입력하면 터미널에는 `Server address: http://127.0.0.1:4000/` 문구가 나타납니다.\
브라우저에서 `http://127.0.0.1:4000/`를 입력하여 정상적으로 홈페이지에 접속되는지 확인해보세요.\
종료하시려면 `Ctrl+c`를 누르시면 됩니다.

<br>
어떤 홈페이지에 접속된다면 정상적으로 설치가 완료된 것입니다.\
본 게시물에서는 **로컬에서의**  접속만을 다루고 있으므로, 아직은 블로그가 완성된 것이 아닙니다.\
이후 게시물에서 블로그 커스터마이징 방법, 게시물 작성 방법 등에 대해 설명하겠습니다.

<br>

---

## 참고
* [Jekyll Chirpy 테마 사용하여 블로그 만들기](https://www.irgroup.org/posts/jekyll-chirpy/)
* [Getting Started](https://chirpy.cotes.page/posts/getting-started/)
