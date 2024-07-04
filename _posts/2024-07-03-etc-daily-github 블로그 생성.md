---
layout: post
title: github 블로그 만들기
subtitle: "깃허브 블로그 만드는 방법"
date: 2024-07-03
categories: etc
tags: daily
comments: true
typora-root-url: ../
---





>[https://iingang.github.io/posts/windows-github-set/#로컬-repository-생성-내-깃허브와-연동](https://iingang.github.io/posts/windows-github-set/#로컬-repository-생성-내-깃허브와-연동 ) 
>
>-> 설명이 잘 되어있지만 뒷부분에서는 오류가 많이 나서 설명을 추가했다:smile:
>
>
>
>📝만들기 전 준비 사항📝
>
>- git에 가입이 되어있는가?
>- git bash가 있는가?





## 1. ruby 설치



Jekyll은 정적 웹사이트 생성기로, Markdown과 같은 마크업 언어로 작성된 내용을 HTML로 변환하여 웹사이트를 만들어주는 역할을 한다.

Jekyll을 설치하기 위해서는 Ruby Installer를 먼저 설치해야 한다. 

Ruby는 Jekyll의 기본 프로그래밍 언어이며, Ruby Installer를 통해 Ruby를 쉽게 설치하고 설정할 수 있습니다. 그런 다음 Jekyll을 설치하고 웹사이트를 개발할 준비가 됩니다.



- Ruby설치: 하단의 사이트에 들어가서 설치한다

​	[https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/)



<img src="/images/2024-07-03-etc-daily-github 블로그 생성/image-20240703223313739.png" alt="image-20240703223313739" style="zoom:50%;" />



표시해둔 버전을 설치

Ruby Installer 설치가 완료되었다면, **Ruby Command 창**을 실행.

<img src="/images/2024-07-03-etc-daily-github 블로그 생성/image-20240703223504176.png" alt="image-20240703223504176" style="zoom:50%;" />



실행한 Ruby Command 창에서 다음 명령어를 실행

```bash
gem install jekyll
gem install minima
gem install bundler
gem install jekyll-feed
gem install tzinfo-data

//설치 완료 후 아래 명령어를 실행했을 때
//버전이 잘 나오면 성공!
jekyll -v 
```







------







## 2. Jekyll Theme 다운



Jekyll Theme Page에 가서 원하는 테마를 고르기! 저는 Monos가 깔끔한 것 같아서 골랐지만 원하는 테마 모두 가능합니다.



<img src="/images/2024-07-03-etc-daily-github 블로그 생성/image-20240703223539294.png" alt="image-20240703223539294" style="zoom:50%;" />





이렇게 맘에 드는 테마를 고르면 클릭 후 Homepage로 들어간다. 들어가면고른 테마의 github 페이지로 들어가진다.



<img src="/images/2024-07-03-etc-daily-github 블로그 생성/image-20240703223742106.png" alt="image-20240703223742106" style="zoom:50%;" />



해당 페이지에서 깃허브 주소를 사진처럼 복사한다. 이렇게 복사한 url은 repository를 만드는데 사용한다.







---







## 3. repository 생성



이제 블로그로 사용한 repository를 만들기 위해서 내 github에 들어간다!

새로운 레파지토리 생성하기를 누르고 아래 보이는 Import a repository 링크를 클릭하거나 처음부터 import repository를 눌러 생성한다.



<img src="/images/2024-07-03-etc-daily-github 블로그 생성/image-20240703223807231.png" alt="image-20240703223807231" style="zoom:50%;" />



Import repository를 클릭한후

*The URL for your source repository*에 아까 복사한 url을 넣어준다.  



<img src="/images/2024-07-03-etc-daily-github 블로그 생성/image-20240703223840113.png" alt="image-20240703223840113" style="zoom:50%;" />



⚠️주의사항⚠️

내 Repository name을 적는 칸에는 [본인아이디].github.io을 입력한다

**[본인아이디]에는 아무거나 넣을 수 없다!** 꼭 github에 저장된 이름을 사용해야 한다!!

예시로 아이디(Owner)가 hong이면 Repository name은 hong.hithub.io 이여야 한다



<img src="/images/2024-07-03-etc-daily-github 블로그 생성/image-20240703223955986.png" alt="image-20240703223955986" style="zoom:50%;" />



모두 입력했다면 생성하기를 클릭한다.

생성 후 https://[본인아이디].github.io 로 접속했을 때 페이지 뜨면 성공!







---







## 4. 로컬 Repository 생성



`git bash`를 실행하여 깃허브를 clone하기 위한 폴더를 하나 생성한다.

사용자 등록을 진행하는 코드를 실행

```bash
//관리를 위해 폴더생성
mkdir blog

//사용자 등록
git config --global user.name "깃허브네임"
git config --global user.email "깃허브이메일"
```





등록 후 방금 새로 생성한 Repository url을 복사한다.

<img src="/images/2024-07-03-etc-daily-github 블로그 생성/image-20240703224126408.png" alt="image-20240703224126408" style="zoom:50%;" />



복사한 후 다시 git bash로 가서 아까 만든 repository를 clone 하기 위해 만든 폴더(blog) 위치로 이동한다

```
cd blog
```





해당 위치로 이동 후 다음 명령어를 실행

```
git clone [복사해온 URL] -b master --single-branch
```





실행하면 내가 만든 Repository가 가져와 진다!

dir 명령어를 실행해서 잘 가져와 졌는지 확인해본다.





---





## 5. 로컬에서 블로그 실행



clone 명령어를 실행후 dir명령어를 실행해 보면 repository가 잘 가져와진 것을 확인할 수 있다.

이제 로컬로 가져와진 repository 경로로 이동

```bash
cd [아이디].github.io

//이동 후 파일 확인
dir
```





내가 다운받은 jekyll 테마는 lock이 존재하기 때문에 오류가 생길 수 있다

dir 명령을 실행해서 Gemfile.lock 파일이 존재하는지 확인!

결론은 Gemfile.lock 파일이 있으면 나중에 오류가 생길 수 있으므로 아래의 명령어를 사용해 파일을 삭제한다.

```bash
//Gemfile.lock 파일 확인 후 삭제
dir 

//파일 삭제
rm Gemfile.lock 
```





일반적으로 Jekyll이나 다른 Ruby 웹 서버에서 웹 서버를 실행할 때 기본적으로 **`webrick`**을 사용한다.

아래 코드를 사용해서 **`webrick`** 다운

```bash
Bundle add webrick
```





아래 명령어를 순차적으로 실행한다.

```bash
gem install tzinfo
gem install tzinfo-data
bundle install
bundle update
bundle install
```





위 명령어 들이 오류 없이 실행된다면 다음 명령어 실행

```bash
bundle exec jekyll serve --trace
```



잘 실행되고 [http://127.0.0.1:4000](http://127.0.0.1:4000/)로 접속이 가능하다면 접속이 성공한 것이다.





---





## 6. 원격 접속



이제 로컬에서 블로그를 만들어서 접속할 수 있게 된 것이다.

하지만 이건 나만 접속할 수 있는 것이다.

그럼 블로그를 만든 이유가 없으므로 변경사항을 다시 github으로 push 한다.



아래 명령어를 실행

```bash
//현재 위치로 수정코드 추가
git add . 

//추가한 코드에 대한 설명 작성
git commit -m "modify config file"

//add, commit 한 코드 git에 보내기
git push origin master
```







🎉🎉🎉🎉🎉🎉🎉🎉

[아이디].github.io 로 잘 접속이 된다면 이제 github 블로그가 완성된 것이다!!

🎉🎉🎉🎉🎉🎉🎉🎉
