# Mac 에서 Jekyll 로 github.io 블로그 개설하기

## 순서
1. sudo 없이 설치하기 :
https://jekyllrb-ko.github.io/docs/troubleshooting/#installation-problems
```
# .bashrc 에 적기
export GEM_HOME=$HOME/gems
export PATH=$HOME/gems/bin:$PATH
```
2. 앱스토어에서 Xcode 설치하기
3. 루비, 지킬, 번들 설치하기
```
brew install ruby
gem install jekyll bundle
```
4. 새 지킬 만들고 웹서버 띄우기
```
jekyll new your_id.github.io
cd your_id.github.io
bundle exec jekyll serve
```
5. 띄운 사이트에 접속해서 확인하기

link : https://localhost:4000


https://stackoverflow.com/questions/7438809/run-bundle-install-in-ruby-on-rails-new-project
