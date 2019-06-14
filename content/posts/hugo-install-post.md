---
title: "Hugo 설치 및 포스팅 하기"
date: 2019-06-14T10:37:56+09:00
categories: ["how to"]
tags: ["hugo", "go", "golang", "github", "github.io"]
---
# 조건
- 사용자 PC는 Mac 이다.
- github를 이용한다.

# 준비
- github에 repository를 생성한다.
	- hugo new site 로 만든 디렉토리가 담길 repository : 이름은 원하는대로
	- {username}.github.io 라는 이름으로 만든 repository : repository 이름이 url 주소가 된다.
- mac에 hugo를 설치한다.
	- brew install hugo
	- 다른 방법도 있지만 생략한다. 그 중 직접 코드를 빌드해서 사용해보고 싶다면 golang 개발 환경 설정 및 부가적인 요소가 필요하다. [hugo github](https://github.com/gohugoio/hugo)

# 만들기
[quick start](https://gohugo.io/getting-started/quick-start/)는 많이 있다. 그래서 큰 그림으로 개념 설명 차원으로 기록한다.

1. 사이트를 만든다.
2. theme를 다운받는다.
3. 글을 만든다.
4. git repository를 연결하고, 빌드를 한다.
5. commit과 push를 한다.

아주 간단해 보이지만 repository가 두 군데인데 어떻게 되느냐이다. 그래서 사이트를 만들었다는 가정하에(blog라는 이름으로) 디렉토리 구조를 설명해보겠다.

### 1. 사이트를 만든다.
여기선 blog라는 이름으로 예를 들어보겠다.

>$ hugo new site blog

```
blog
├── archetypes
├── config.toml
├── data
├── layouts
├── resources
├── static
└── themes
```
특별한 건 없다.

### 2. theme를 다운받는다.
```
blog
├── archetypes
├── config.toml
├── data
├── layouts
├── resources
├── static
└── themes (git submodule <theme>)
```
themes 디렉토리 아래 다운받은 themes 파일들이 있다. 그리고 themes에는 선택한 theme의 git submodule이 등록되어 있다.

[https://themes.gohugo.io/](https://themes.gohugo.io/)

### 3. 글을 만든다.

>$ hugo new posts/first-post.md

```
blog
├── archetypes
├── config.toml
├── content
│   └── posts
│       └── first-post.md
├── data
├── layouts
├── resources
├── static
└── themes (git submodule <theme>)
```
여기서 first-post.md의 draft 라인을 삭제하거나, false로 해야 웹에서 해당 글이 보인다.

항상 새로운 글은 hugo new 를 통해서 생성 시킨 후 작성해야 한다.

### 4. git repository를 연결하고, 빌드를 한다.
#### github.io repository 연결하기
> $ git submodule add -b master https://github.com/{username}/{username}.github.io.git public

public 디렉토리에 github.io repository를 submodule로 연결한다.

#### build 하기
> $ hugo -t {themes}

혹은

> $ hugo

build를 하고 나면 public 디렉토리 밑에 html 등등의 필요한 파일들이 생성된다.

#### <blog> repository 연결하기

> $ git remote add origin https://github.com/{username}/blog.git

```
blog (git <blog>)
├── archetypes
├── config.toml
├── content
│   └── posts
│       └── first-post.md
├── data
├── layouts
├── public (git submodule <username.github.io>)
├── resources
├── static
└── themes (git submodule <theme>)
```

여기까지 마치면 위의 디렉토리 구조가 된다. 그리고 두 곳의 repository로 push 하면 된다.

# 정리
글을 쓸 때 마다 빌드를 하고, 이를 통해 public 디렉토리에 생성된 파일들을 username.github.io 에 push 하는 방식이다.

처음엔 두 군데의 repository 중 어느 것을 submodule로 잡아야 하는지 헷갈렸지만 몇 번 실패하고 다시 하다 보면 금방 알게 될 것이다.

시간을 들여 themes를 고민해봐야겠다. 나중에 어떤 theme를 썼는지 기억을 못하거나 사라졌다면 어떻게 해야 할 것인가?

#### 참고
- [quick start](https://gohugo.io/getting-started/quick-start/)
- [github에 배포하기](https://gohugo.io/hosting-and-deployment/hosting-on-github/)
	- gitlab, firebase, aws 등등 여러 곳에 배포하는 방법이 나와있다.
- [hugo themes](https://themes.gohugo.io/)