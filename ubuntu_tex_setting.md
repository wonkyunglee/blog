# Ubuntu 16.04 Texmaker setting

논문을 작성하기 위해 ACM Format 을 받았지만, 약간의 난관이 있었기에 정리해둡니다.

## 설정 파일 받기
각 저널 혹은 컨퍼런스의 논문 제출 양식이 압축 파일 혹은 깃헙 리포로 배포됩니다.
ACM-CCS 과 NIPS 의 포멧을 받아봅시다.
- [ACM-CCS 2018 Tex Format Zipfile Download  Link](https://www.acm.org/binaries/content/assets/publications/consolidated-tex-template/acmart-master.zip)
- [NIPS 2018 Tex Format Download Link](https://media.nips.cc/Conferences/NIPS2018/Styles/nips_2018.tex)
- [NIPS 2018 Style Format Download Link](https://media.nips.cc/Conferences/NIPS2018/Styles/nips_2018.sty)

ACM 포멧은 압축 해제 해주시고, NIPS 2018 파일 두개는 같은 폴더에 위치시켜주세요.

## texmaker 설치

```
sudo apt-get install texmaker
```

texmaker 만 설치하면 될 줄 알았는데 아니더군요
ACM 포멧을 로드해서 렌더링하는데 다음과 같은 에러가 나게 됩니다.
```
LaTeX Error: File iftex.sty not found
```
texlive-generic-extra 패키지를 설치하여 해결하였습니다.
```
sudo apt-get install texlive-generic-extra
```
참고 링크 : https://tex.stackexchange.com/questions/392577/how-to-fix-iftex-sty-not-found-issue

더불어 한글 주석을 쓰면 ko.tex 가 설치되어있지 않아 에러가 납니다. 이는 texlive-full 을 설치하여 해결하였습니다.
```
sudo apt-get install texlive-full
```


## texmaker 실행, 로드 및 빌드
설치가 잘 되었다면, 터미널에 다음 명령어를 실행하여 texmaker 를 실행시킬 수 있습니다.
```
texmaker
```

1. ACM-CCS 포멧 로드하기
GUI 가 켜졌다면, open 을 누르고 ACM 폴더에 있는 ccs-template.tex 를 열어봅시다.
F1 키를 누르면 Quick Build 가 되고 오른쪽에 pdf 렌더링이 보이게 됩니다.

2. NIPS 포멧 로드하기
마찬가지로 open 을 누르고 nips 폴더에 있는 nips_2018.tex 를 열어봅시다.
F1 키를 누르고 렌더링된 pdf 를 오른쪽에서 확인합니다.

## 논문 작성
각 포멧마다 건드리면 안되는 부분과, 꼭 고쳐야하는 부분들이 있습니다.  
예를 들면, ACM-CCS 같은 경우 [링크](https://dl.acm.org/ccs/ccs.cfm) 에서 논문 주제의 카테고리에 해당하는 xml 코드를 붙여넣어야합니다.
잘 확인해서 좋은 논문 작성하시길 바랍니다.
