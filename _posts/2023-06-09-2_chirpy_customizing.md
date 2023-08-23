---
title: "[2] Jekyll Chirpy 테마 커스터마이징"
categories: [Computer Science, Git]
tags: [jekyll, gitblog]
---

[GitBlog 생성](https://heeseons.github.io/posts/1_jekyll_setting/)을 통해 초기 세팅을 완료했다면, 이제 블로그를 커스터마이징 하겠습니다.\
커스터마이징에 활용하는 모든 이미지에 대한 책임은 사용자 본인에게 있으니, 저작권 문제를 꼭 유념하시기 바랍니다.

---
> 운영체제: macOS (Ventura)\
> 사용테마: [Chirpy Jekyll Theme](https://github.com/cotes2020/jekyll-theme-chirpy)


<br>
## 1. 준비
### 1.1. 이미지 준비
프로필 이미지와 [파비콘](https://en.wikipedia.org/wiki/Favicon)으로 사용할 이미지를 찾아줍니다.\
저의 경우에는 맥북에서 제공되는 미모티콘을 프로필 이미지로 사용하고, 기본 이모티콘을 파비콘으로 활용했습니다.
* 참고: [파비콘 변환](https://favicon.io)

<br>
## 2. 테마 커스터마이징
### 2.1. 블로그명 및 연락처 수정
`_config.yml` 파일에는 블로그명, 저자 등 해당 테마의 기본적인 내용을 수정할 수 있습니다.\
본 게시물이 작성된 이 블로그의 세팅값은 아래와 같습니다.

| 변수 | 설정/입력값 | 설명 |
|:---:|:---:|---|
| `lang` | `en` | 테마(메뉴명 등)에서 사용하는 언어<br>변경 후 `_data/locales`에서 설정 필요 |
| `timezone` | `Asia/Korea` | 기준 시간대 |
| `title` | ByteHee | 블로그 제목 |
| `tagline` | Byte-sized thoughts ~ | 블로그 소개 |
| `description` | CS | SEO(Search Engine Optimization) 키워드 |
| `url` | https://`<깃허브 ID>`.github.io | 블로그 접속 URL |
| `github: username` | `<깃허브 ID>` | 깃허브 ID |
| `social: name` | Heeseon | 블로그 닉네임 |
| `social: email` | `user`@gmail.com | 이메일 주소 |
| `social: links` | https://github.com/`<깃허브 ID>` | 본인의 SNS 주소<br>사용하지 않는 항목은 주석처리 |
| `theme_mode` | `light` | 블로그 테마`light`/`dark` 중 선택<br>default = `light` |
| `avatar` | assets/img/avatar.jpeg | 프로필 사진 경로<br>`assets/img` 폴더의 `avatar.jpeg`파일 |
| `toc` | `true` | 포스팅 본문 내 오른쪽에 목차 표시여부<br>`2. 테마 커스터마이징` 등 |
| `paginate` | 10 | 한 페이지에 표시할 게시물 개수<br>default = 10 |

> `_config.yml` 수정 후에는 반드시 jekyll 재구동 (jekyll serve) 필요
{: .prompt-info}

<br>
### 2.2. ABOUT 편집
`_tabs/about.md` 파일 수정을 통해 블로그 ABOUT 메뉴의 내용을 수정할 수 있습니다.\
본인을 자유롭게 소개하는 글을 쓰시면 됩니다.\
[마크다운](https://ko.wikipedia.org/wiki/마크다운) 문법을 사용하여 작성하셔야 합니다.

<br>
### 2.3. Favicon(파비콘) 변경

`1.2.`에서 저장한 파비콘을 적용해보도록 하겠습니다.\
참고 링크에서 파비콘 이미지를 저장하고, 해당 파일을 `assets/img/favicon` 폴더에 넣어 줍니다.\
기존 파일을 덮어쓰셔도 무방합니다!

<br>
이제 본인에게 맞게 블로그 커스터마이징이 끝났습니다.\
다음 게시물에서는 포스팅 방법, 그리고 서버 push 방법에 대해 설명하겠습니다.

<br>

---
## 참고
* [Getting Started](https://chirpy.cotes.page/posts/getting-started/)
* [Customize the Favicon](https://chirpy.cotes.page/posts/customize-the-favicon/)
* [Jekyll Chirpy 테마 사용하여 블로그 만들기](https://www.irgroup.org/posts/jekyll-chirpy/)
* [Chirpy 테마 커스터마이징](https://www.irgroup.org/posts/Chirpy-테마-커스터마이징/)
