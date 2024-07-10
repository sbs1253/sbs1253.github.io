---
layout: post
title: '깃허브 페이지 작성 Jekyll Chirpy '
date: 2024-05-29 16:08 +0900
description: Jekyll Chirpy 테마로 페이지 작성
category: [Blogging,세팅]
tags: [깃허브]
pin: true
math: true
mermaid: true
author: sbs1253
---

# 깃허브 페이지 Jekyll 적용

## 깃허브 페이지인 이유
- **깃허브 페이지는 github.io라는 도메인을 제공해주고 블로그에 자동으로 https를 지원해주고
 jekyll 테마 템플릿이 많아 다양하게 꾸미기 용이하며 수정해서 커스터 마이징을 할 수 있다.** 

- **jekyll serve로 로컬에서 라이브로 결과를 확인할 수 있다** 
# 1. Git Pages 생성

먼저 GitHub에서 GitPages를 생성하도록 하겠습니다.

### 1-1.  **Github로 이동하여 새로운 레포지토리를 만듭니다.**
### 1-2.  **레포지토리 이름을 [내 유저네임.github.io] 로 만들어줍니다.**

>  참고 https://sbs1253.github.io/

### 1-3.  **로컬로 코드를 가져오기 위해 git clone합니다.**

# Ruby 설치
###  Jekyll을 사용하기 위해서는 먼저 **Ruby**를 설치해야합니다. → [Ruby 다운로드 페이지](https://rubyinstaller.org/downloads/)
모든 설치가 끝난 후 `ruby -v` 커맨드를 입력해서 버전 확인
```shell
    $ ruby -v
    ruby 3.2.4 (2024-04-23 revision af471c0e01) [x64-mingw-ucrt]
```
# Jekyll 설치
### 터미널을 열어서 커맨드 입력
```shell
    $ gem install jekyll 
    $ gem install bundler
```

### 버전 확인까지 해줍시다.
```shell
$ jekyll -v
jekyll 4.3.3
$ bundler -v
Bundler version 2.5.10
```

# Jekyll 사이트 생성
> 클론한 폴더로 이동 후 수행해야합니다!
{: .prompt-warning } 
```shell
$ jekyll new ./
```

### bundle 설치 및 업데이트 
- **Ruby를 편하게 이용하는 기능 npm과유사**
```shell
$ bundle install
$ bundle update
$ bundle install
```
### 서버를 실행해 봅시다.

> node.js 모듈을 설치하지 않으면 assets/js/dist/*.min.js Not Found 에러 발생과 함께 블로그 기능이 정상적으로 동작하지 않습니다.
{: .prompt-warning }

```shell
$ bundle exec jekyll serve
```

### jekyll-compose 로 포스트 쉽게 올리기

jekyll-compose 설치 후 아래의 명령어를 입력하면 _post폴더에 작성시간이 찍힌 파일이 생성된다.
```
 bundle exec jekyll post "글 제목!"
```
다른 명령어
- draft -> 입력받은 제목으로 초안 생성 (작성시간이 안 찍힘)
- post -> 입력받은 제목으로 게시글 생성 (작성시간이 찍힘)
- publish -> 입력받은 초안을 _post로 옮기고 작성시간 찍어줌
- unpublish -> 입력받은 게시글을 다시 _draft로 옭김
- page -> 입력받은 이름으로 페이지 생성
- rename -> 입력받은 초안의 이름 변경
- compose -> 입력받은 이름으로 파일 생성

### 빌드 및 배포
**공식 설명서에 깃허브 배포방법 필독!**

### 참고
[jekyll](https://jekyllrb.com/docs/)


[chirpy 공식설명서](https://chirpy.cotes.page/posts/getting-started/)


[jekyll-chirpy 설치방법](https://www.irgroup.org/posts/jekyll-chirpy/)


[jekyll-compose 설치방법](https://10kseok.github.io/posts/easy-to-make-default-mdfile-to-use-jekyll-compose/)