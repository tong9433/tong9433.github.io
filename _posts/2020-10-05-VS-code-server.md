---
layout: post
title: VS code-server를 통해 어디에서든 PC환경으로 개발하자
date: 2020-10-05T09:52:20.613Z
thumbnail: /assets/img/blog_main/002.jpg
category: blog
summary: VS Code + Chrome 
keywords: VS code, code-server
permalink: /blog/002
---

안녕하세요. `DevTong` 입니다. 


오늘 소개해드릴 내용은 code-server를 이용한 원격 개발환경 만들기입니다.

Window PC에서 VS code-server를 통해 외부에서 접속 가능한 개발환경을 만드는 방법을 포스팅하고자 합니다.

먼저 VS Code 및 code-server에 대한 간단한 소개드리고자 합니다.



### Visual Studio Code, VS Code

![image-20201011231810733](/assets/img/blog/image-20201011231810733.png)

우선 VS Code에 대한 간단한 설명을 해보겠습니다.

 마이크로소프트에서 오픈소스 프로젝트로 개발하고 있는 소스코드 에디터입니다. Electron을 기반으로 만들어져 mac, linux, window등 거의 대부분의 운영체제에서 사용하는 것이 가능합니다. 

VS Code는 IDE보다는 Editor에 가까워 일반 IDE에 비해 상당히 가볍지만, extensions을 통해 본인이 쓰고자 하는 기능들을 손쉽게 확장시켜 여러 프로그래밍 언어를 지원하는 IDE로 확장시킬 수 있습니다. 따라서 현재 많은 개발자가 사용하고 상당히 Hot한 에디터입니다.

[VS Code 설치](https://code.visualstudio.com/)



### code-server

한편 Electron 기반 오픈소스인 VS Code를 Node.js 통해 Server를 올리고 크롬 브라우져에서 직접 VS Code 에디터를 사용할 수 있도록 만들어진 오픈소스가 `vs code-server`입니다. 

* 공식 github에서 소개
  - Code everywhere
    - Code on your Chromebook, tablet, and laptop with a consistent development environment.
    - Develop on a Linux machine and pick up from any device with a web browser.
  - Server-powered
    - Take advantage of large cloud servers to speed up tests, compilations, downloads, and more.
    - Preserve battery life when you're on the go as all intensive tasks runs on your server.
    - Make use of a spare computer you have lying around and turn it into a full development environment.

![image-20201011231740645](/assets/img/blog/image-20201011231740645.png)

**즉 크롬 기반의 웹브라우져가 있는 환경이라면** VS code를 사용할 수 있다는 뜻이겠죠?

저는 window PC 환경에서 Ubuntu 환경을 만든 뒤, VS code-server를 실행시킴으로써 언제 어디서나 Chrome 브라우져가 있는 곳이라면 제 PC환경의 VS code editor를 통해 개발할 수 있는 환경을 만드는 것이 **최종목표**였습니다^^


### Ubuntu 환경 만들기 on Windows 10

Windows 10은 `WSL`을 지원합니다!!

`Window Subsystem for Linux(WSL)`인데요. 이 기능을 이용하면 손쉽게 Ubuntu 환경을 Setup 할 수 있습니다.

먼저 WSL 기능을 사용하기 위해서는 Windows 10의 Build version이 `14316` 이상이어야 한다고 합니다. 최신 윈도우로 업데이트 해주시길 바랍니다.



1. 우선 개발자 모드를 아래처럼 `켬`주세요. (설정 > 업데이트 및 보안 > 개발자용 > 개발자 모드 켬)
  ![image-20201011232211651](/assets/img/blog/image-20201011232211651.png)

2. Windows 기능 중 `Linux용 Windws 하위 시스템` 기능을 켜주세요 (제어판 > 프로그램 > 프로그램 및 기능 > Windows 기능 켜기/끄기 > Linux용 Windows 하위 시스템 체크!)
  ![image-20201011232507982](/assets/img/blog/image-20201011232507982.png)

3. Microsoft Store를 검색에서 입력해 주신뒤 그 후 Ubuntu를 검색해서 설치합시다. 설치가 완료되면 아래처럼 실행이 가능합니다.
  ![image-20201011232650942](/assets/img/blog/image-20201011232650942.png)

4. 설치가 완료되면 아래처럼 검색한 뒤, 관리자 권한으로 실행해줍시다.
관리자 권한으로 실행하지 않으면 **방화벽 문제 등**이 발생할 수 있습니다.
  ![image-20201011232739922](/assets/img/blog/image-20201011232739922.png)

5. 이제 Ubuntu에 필수 프로그램을 설치한 뒤 code-server를 설치해줍니다.
  ```bash
  $ sudo apt-get install build-essential net-tools
  $ wget -q https://github.com/cdr/code-server/releases/download/3.4.1/code-server_3.4.1_amd64.deb
  $ sudo dpkg -i code-server_3.4.1_amd64.deb
  $ echo "export PASSWORD='{비밀번호}'" >> ~/.bashrc # 접속 시 암호, 꼭 설정!
  $ source ~/.bashrc
  $ sudo ufw allow 8080/tcp # 8080 port 방화벽 해제
  ```

6. 몇 가지 VS Code extensions 패키지를 설치 후, code-server 실행해줍니다.
  ```bash
  $ code-server --install-extension ms-vscode.cpptools ms-vscode.cpptools formulahendry.terminal hookyqr.beautify
  $ code-server
  ```
  ![image-20201011233853617](/assets/img/blog/image-20201011233853617.png)
  ![image-20201011234040062](/assets/img/blog/image-20201011234040062.png)

이제 크롬브라우져에서 [http://localhost:8080](http://localhost:8080)에 접속하면 위와 같이 VS Code 에디터가 동작하고 에디터에 설치한 확장 패키지가 적용된 것을 볼 수 있습니다. 



### 포트 포워딩 해주기

저희의 최종 목표인 외부에서 해당 에디터에 접속하기 위해서 포트 포워딩을 해주어야 합니다.

자세한 내용은 [https://studyforus.tistory.com/125](https://studyforus.tistory.com/125)를 참고하시면 이해하기 쉬울 것 같습니다.

![image-20201011234224201](/assets/img/blog/image-20201011234224201.png)

먼저 `ifconfig`를 통해 inet address `192.168.0.5`를 메모해줍니다.
공유기 설정을 바꾸기 위해 http://192.168.0.1/에 접속합니다. ( ipTIME 공유기를 사용중 )

로그인을 후

아래와 같이 `새규칙 추가`를 합니다. 이때 저희는 `8080`포트를 사용할 것이므로 아래와 같이 set 해줍니다.

![image-20201011234632903](/assets/img/blog/image-20201011234632903.png)



이제 다시 Ubuntu Terminal로 돌아와서 아래 command로 `code-server`를 실행합니다. 이때 ip주소는 방금 전 메모해둔 `inet`주소로 `--bind-addr`를 설정합니다.

```bash
$ code-server --bind-addr 192.168.0.5:8080
```



네이버에서 본인 ip 주소를 확인 한 뒤

![image-20201011234824231](/assets/img/blog/image-20201011234824231.png)

크롬 브라우져로 접속합니다.

`http://[본인 ip]:8080` 로 접속하면 아래와 같이 접속이 되는 것을 알 수 있습니다.

![image-20201011235412651](/assets/img/blog/image-20201011235412651.png)



이제 크롬브라우져만 있다면 어디에서든 내 PC 환경에서 프로그래밍이 가능합니다 !!
이상으로 포스팅을 마치도록 하겠습니다 :)