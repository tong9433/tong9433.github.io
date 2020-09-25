---
layout: post
title: Github과 Jekyll를 이용한 개발 블로그를 만들어보자
date: 2020-09-25T09:52:20.613Z
thumbnail: /assets/img/blog_main/jekyll.png
category: blog
summary: on Window
keywords: jekyll, github, blog, window
permalink: /blog/001
---

개발 블로그를 만들어 봅시다. : ) 
### 지킬 테마 선택하기
* 테마 선정 기준

  1. 카테고리 분류
  2. 깔끔함
  3. 쉽게 커스터마이징 가능
  4. 가독성

     ...

* 오픈소스 Jekyll 테마 사이트

  1. [http://jekyllthemes.org/](http://jekyllthemes.org/)

     ![image-20200919150432072](/assets/img/blog/image-20200919150432072.png)
  
  2. [http://themes.jekyllrc.org/](http://themes.jekyllrc.org/)
  3. [https://jekyllthemes.io/](https://jekyllthemes.io/)

* 나의 선택 => [Devlopr](https://github.com/sujaykundu777/devlopr-jekyll)
  
    ![image-20200919150852234](/assets/img/blog/image-20200919150852234.png)
  
  1. 깔끔합니다. 가독성이 좋을 것 같습니다? 개인적으로 white 선호합니다.
  
    ![image-20200919151101131](/assets/img/blog/image-20200919151101131.png)
  
  2. 카테고리를 잘 분류 할 수 있습니다.
  
    ![image-20200919151124672](/assets/img/blog/image-20200919151124672.png)
  
  3. Portfolio 탭이 미리 잘 구성되어 있습니다.

    ![image-20200919151232283](/assets/img/blog/image-20200919151232283.png)

* 준비 완료! 이제 블로그를 구축해 봅시다.

## github 블로그 만들기 on Window 10

Window 10에서 github 블로그 구축 환경을 포스팅해보려고 합니다. 

`루비`와 `Jekyll`을 설치하는 과정은 `Mac OS`와는 다르지만 그 이외의 과정은 같을 것 같아요.



###  jekyll를 간단하게 이해해보자

jekyll은 정적 웹사이트 생성기에요. 정적? 동적?  쉽게 이해해보면 동적 웹 사이트는 서버와 사용자간에 끊임없이 데이터를 주고 받는 사이트죠. 예를 들면 쿠팡같은 쇼핑몰 사이트는 장바구니, 구매과정에서 서버와 데이터를 주고 받죠. 이러한 사이트를 **Dynamic Web Site**라고 합니다.

하지만 우리가 만들고자 하는 Blog는 이런 과정이 굳이 필요할까요?ㅎㅎ

블로그를 만드는 저희는 블로그 포스팅에 관한 파일을 미리 웹서버에 올려놓고, 유저들은 해당 포스팅만 보면 되겠죠. 이러한 사이트를 **Static Web Site**라고 합니다.

![image-20200919153615872](/assets/img/blog/image-20200919153615872.png)

Jeykyll은 이러한 **Static Web Site**의 생성에 특화되어 있는 플랫폼입니다.

Jeykyll은 Web Backend가 `Ruby on Rails`로 구현되어 있기 때문에 Ruby 설치가 필수적입니다.

그럼 Jekyll을 설치해봅시다.





### 1. jekyll 설치 (Window os)

* Ruby 설치

  * 설치 사이트 : [https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/)

  본인의 윈도우 환경에 맞춰 위 사이트를 방문한 후 `Ruby+Devkit 2.6.6-1(x64)`를 다운로드 합시다. 이때 꼭 Devkit을 설치해야 해요.. 잘못하면 상당히 꼬입니다.

  * 설치과정

  ![image-20200919153921303](/assets/img/blog/image-20200919153921303.png)

  ![image-20200919153929303](/assets/img/blog/image-20200919153929303.png)

  ![image-20200919153944006](/assets/img/blog/image-20200919153944006.png)

  ![image-20200919154232086](/assets/img/blog/image-20200919154232086.png)

  ![image-20200919154402811](/assets/img/blog/image-20200919154402811.png)

  msys2 설치 필수!

  msys2 : 

  > 윈도우 환경에서 Unix의 Terminal 환경을 제공해줍니다. 이때 MinGW는 꼭 알아야 하는 프로그램인데요. MinGW는 Minimalist GNU for Window의 약자로 우리가 Ubuntu나 unix 기반 환경에서 사용하는 오픈소스 패키지를 Window에서 실행할 수 있도록 합니다.

* Jekyll 설치

  위 Ruby 설치가 완료되었으면 시작며뉴에서 Ruby 터미널을 실행합시다!

  * 우선 gem이 잘 설치 됬는지 확인!

    gem : 

    > Ruby 프로그램 및 라이브러리 배포를 위한 표준입니다.
    >
    > Ruby의 패키지 관리자 (Python의 pipe, Node.js의 npm같은..)

  ![image-20200919155156882](/assets/img/blog/image-20200919155156882.png)

  * `jekyll`에 관련된 패키지를 모두 설치합시다

  ```shell
  $ gem install jekyll bundler
  ```

  ![image-20200919155504393](/assets/img/blog/image-20200919155504393.png)

  gem이 설치를 잘 해주었네요.

  * jekyll 의 설치 확인

  ```shell
  $ jekyll --version
  ```

  ![image-20200919155948512](/assets/img/blog/image-20200919155948512.png)

* jekyll로 새로운 blog repo 생성 (시작메뉴에서 poweshell x86을 실행)

```powershell
$ mkdir blog
$ cd blog
$ jekyll new devtong
```

![image-20200919160832620](/assets/img/blog/image-20200919160832620.png)

* jekyll 서버 실행 확인

```shell
$ jekyll serve
```

![image-20200919160929545](/assets/img/blog/image-20200919160929545.png)

* [http://127.0.0.1:4000/](http://127.0.0.1:4000/) 확인

  ![image-20200919161057729](/assets/img/blog/image-20200919161057729.png)

  * 나만의 블로그 폴더가 완성되었고 지킬이 정상적으로 실행되어 호스팅되는 것까지 완료되었습니다.  이제 제가 선택한 블로그의 테마를 넣어서 github과 연동해 볼까요?



### 2. github Repository 생성

* 왜 github과 연동하냐구요???  

> 우리의 블로그를 인터넷상에 보여주기 위해서는 그것을 hosting 해주는 매개체가 필요합니다. Github에서는 Static Website를 무료로 호스팅해주고 있습니다.
>
> 만약 github를 사용하지 않고 컴퓨터나 AWS 등에서 웹호스팅도 물론 가능하지만 그렇다면 24시간 컴퓨터를 가동하거나, 돈이 들겠죠.. 그렇기에 우리는 Github Page와 Jekyll를 이용해서 blog 환경을 구축하는 것입니다.

* git 설치

  우선 git 을 설치합시다. 미리 설치되어 있다면 Pass!

  * [git 설치](https://wonderbout.tistory.com/64) 참고바랍니다 :)
    
    ![image-20200919162855841](/assets/img/blog/image-20200919162855841.png)

* github.io 주소만들기

  1. 선택한 테마의 github 사이트에 접속한 후 Fork 혹은 `Use this template` 버튼을 클릭한다.
  
    ![image-20200919164030936](/assets/img/blog/image-20200919164030936.png)
    
    [https://github.com/sujaykundu777/devlopr-jekyll/](https://github.com/sujaykundu777/devlopr-jekyll)

  2. `Repo name`과 `Description`을 적고 `Create repository frome template`를 click!
  
    ![image-20200919183336754](/assets/img/blog/image-20200919183336754.png)

  3. 생성되는 중

    ![image-20200919164231774](/assets/img/blog/image-20200919164231774.png)
  
    ![image-20200919183352191](/assets/img/blog/image-20200919183352191.png)
  
    ![image-20200919183649106](/assets/img/blog/image-20200919183649106.png)

  호스팅이 된 것을 확인 할 수 있다. 이제 소스를 수정해보자.

  4. local에 해당 repo를 `clone` 한다.

  ```shell
  $ git clone https://github.com/tong9433/tong9433.github.io.git
  $ cd tong9433.github.io
  $ bundle update
  $ bundle install
  $ bundle exec jekyll serve --watch
  ```
    ![image-20200919184753808](/assets/img/blog/image-20200919184753808.png)

  5. 컨텐츠 수정하기

     테마의 Rule을 참고해서 다양하게 수정해보자.

     * `_config.yml` 파일 수정 (반드시 **base url**을 수정해야 함)

       ```
       title: DevTong
       subtitle: A Jekyll Theme Built for Developers
       description: >- # this means to ignore newlines until "baseurl:"
         devlopr-jekyll is a beautiful Jekyll Theme Built For Developers, which is optimized for speed and readability.
       
       url: "https://tong9433.github.io" # the base hostname & protocol for your site, e.g. 
       baseurl: "https://tong9433.github.io" # the subpath of your site, e.g. /blog
       ```

       이미지 파일 수정도 간단히 해보고,, scss 파일도 간단히 수정해 봅시다.

  6. git 에 반영

     ```shell
     $ git add -A
     $ git commit -m "DevTong blog init"
     $ git push origin master
     ```

  7. 약 1분정도 기다린 뒤 확인해보자.

    ![image-20200919190331749](/assets/img/blog/image-20200919190331749.png)

  블로그가 준비되었습니다!!!!

  그럼 이제 커스터 마이징과 포스팅을 시작해봅시다 : )

