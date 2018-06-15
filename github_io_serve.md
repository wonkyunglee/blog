# Mac 에서 Jekyll 로 github.io 블로그 개설하기

## 설명
웹사이트를 직접 개설하기 위해서는 **도메인**과 **호스팅 서버**가 필요하다. 도메인이란 쉽게 얘기해서 내 블로그의 주소이다. 개인적으로 도메인을 보유하고 싶으면 후이즈같은 사이트에서 현재 비어있는 도메인을 구매할 수 있다. 호스팅 서버는 블로그에 쓴 글이나 사진, 블로그의 소스코드, 만약 회원가입이 가능하다면 회원정보 등 블로그에 필요한 모든 데이터를 저장한다. 웹호스팅 사이트에서 기간과 용량 별로 구매가 가능하다.

개인 블로그를 개설하는 방법에는 여러가지가 있다. 가장 쉬운 방법은 네이버, 다음, 티스토리 등 블로그 개설을 도와주는 서비스를 이용하는 방법이다. 이들은 도메인과 호스팅 서버 등 필요한 모든 것을 제공해준다. 우리는 블로그 테마를 고르고 글만 쓰면 된다. 물론 매우 편리한 서비스이지만 그만큼 블로그의 주인이 커스터마이징 할 수 있는 부분은 적다. 누군가는 더 자유로운 블로그 화면 구성과 더 다양한 기능들을 넣고 싶을 수 있다. 하지만 그렇다고 해서 블로그를 html 과 javascript, php 등으로 저 밑단부터 구현하기엔 시간과 노력이 너무나도 많이 들며 일반인에겐 어려운 일이다.

오늘 소개하고자 하는 방법은 네이버나 다음보다는 자유롭고, 처음부터 코딩하는 것 보다는 쉬운, 그리고 무엇보다 **무료**인 블로깅 개설 방법이다. github 은 도메인과 호스팅 서버 모두를 무료로 제공해주며 지킬은 쉽게 블로그 커스터마이징을 할 수 있게 도와준다. 지금부터 간단히 jekyll 을 이용해서 github에 블로그를 개설하는 방법을 소개한다.


## 순서
1. sudo 없이 설치하기
```
# .bashrc 에 적기
export GEM_HOME=$HOME/gems
export PATH=$HOME/gems/bin:$PATH
```
2. 터미널 다시 시작
3. 앱스토어에서 Xcode 설치하기
4. 루비, 지킬, 번들 설치하기
```
brew install ruby
gem install jekyll bundle
```
5. 새 지킬 만들고 웹서버 띄우기
```
jekyll new your_id.github.io
cd your_id.github.io
bundle exec jekyll serve
```
6. 띄운 웹서버에 접속해서 확인하기
```
link : https://localhost:4000
```
7. _config.yml 파일에 title, email, github username, url 등 설정하기.

```
vi _config.yml

title: title
email: your@email.com
description: description
baseurl: "" # the subpath of your site, e.g. /blog
url: "https://your_id.github.io" # the base hostname & protocol for your site, e.g. http://example.com
github_username: username
# Build settings
markdown: kramdown
theme: minima
plugins:
 - jekyll-feed

```


8. github Repository에 push 하기
```
git commit -m "commit message"
git remote add https://github.com/your_id/your_repo.git
git push origin master
```

9. 설정한 url 가서 확인하기

## Output
위의 순서대로 진행하여 간단한 이력 정리 웹사이트를 만들어 보았다.

> [https://wonkyunglee.github.io](https://wonkyunglee.github.io)

위와 같은 양식으로 이력 정리 사이트를 만들고 싶다면, 다음의 깃헙 주소에서 레포지토리를 클론하고, 자신에게 맞게 고쳐서 사용하면 된다.

> [https://github.com/wonkyunglee/wonkyunglee.github.io](https://github.com/wonkyunglee/wonkyunglee.github.io)

## Themes
Jekyll 은 다양한 테마를 제공한다. 다음의 사이트에서 마음에 드는 theme 을 다운받아 사용 가능하다.

> [http://jekyllthemes.org/](http://jekyllthemes.org/)


## References
- [https://jekyllrb-ko.github.io/](https://jekyllrb-ko.github.io/)
- [https://jekyllrb-ko.github.io/docs/troubleshooting/#installation-problems](https://jekyllrb-ko.github.io/docs/troubleshooting/#installation-problems)
- [https://stackoverflow.com/questions/7438809/run-bundle-install-in-ruby-on-rails-new-project](https://stackoverflow.com/questions/7438809/run-bundle-install-in-ruby-on-rails-new-project)
