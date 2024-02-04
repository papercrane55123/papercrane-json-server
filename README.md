# papercrane-json-server

![LGTM](https://i.lgtm.fun/2p1c.png)

# RUN
```
npm i json-server

wsl@DESKTOP-QKTLER8  ~/code/papercrane-json-server  npx json-server db.json
JSON Server started on PORT :3000
Press CTRL-C to stop
Watching db.json...

♡( ◡‿◡ )

Index:
http://localhost:3000/

Static files:
Serving ./public directory if it exists

Endpoints:
http://localhost:3000/posts
http://localhost:3000/comments
http://localhost:3000/profile
```

# FROM
https://www.npmjs.com/package/json-server

# Hands-on with Fly.io
```
세상에는 수많은 서버와 언어가 있다. 그중 무료로 서버 구축에 대해 이해하기 쉬운 서비스(Fly)가 있으니 함께 작동시켜보자. (Fly.io는 클라우드 기반의 플랫폼으로, 애플리케이션을 전 세계의 여러 지역에 분산시키고 더 빠르게 배포할 수 있게 도와주는 도구다)
사용방법을 적는 이유는, 여기서 하라는 대로 수행했다가는 연습삼아 한 프로젝트가 통장의 돈이 빼가는 아쉬움을 느낄 수 있기 때문이다. 하고 나서 좋았다면 회사에 기부하자

필자는 설치부터 실행까지 공식문서를 참고했다. Hands-on with Fly.io를 따르면 서비스를 실제로 사용하면서 경험하거나 실험해볼 수 있다.
https://fly.io/docs/hands-on/install-flyctl/
Documentation and guides from the team at Fly.io.
fly.io

아래 방법은 모두 Linux 환경, ubuntu 22.04 버전에서 작업하였으니 참고하자.
1) 페이지를 띄우려는 디렉토리 만들기(또는 그 환경에서 작업하기).

2) Dockerfile 이라는 이름을 가진 파일을 새로 만들어 아래 내용 추가하기
$ vi Dockerfile
FROM node:20.11

WORKDIR /app

RUN npm install -g npm

RUN npm install -g json-server

COPY ./db.json /app

CMD ["json-server", "-p", "80", "-w", "/app/db.json"]
3) flyctl 설치
사진 설명을 입력하세요.
4) (홈페이지 회원가입이 되어 있다는 가정하에) 로그인하기.
$ fly auth login
만약 zsh: command not found: fly와 같은 에러가 발생했다면
$ curl -L https://fly.io/install.sh | sh
명령에서 나온 아래와 같은 결과 값 중
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  1735    0  1735    0     0   3916      0 --:--:-- --:--:-- --:--:--  3925
######################################################################## 100.0%
set update channel to shell
flyctl was installed successfully to /home/wsl/.fly/bin/flyctl
Manually add the directory to your $HOME/.bash_profile (or similar)
  export FLYCTL_INSTALL="/home/wsl/.fly"
  export PATH="$FLYCTL_INSTALL/bin:$PATH"
Run '/home/wsl/.fly/bin/flyctl --help' to get started
export FLYCTL_INSTALL="/home/wsl/.fly"
export PATH="$FLYCTL_INSTALL/bin:$PATH"
부분을 .zhrc 파일에 추가해주자.
$ vi ~/.zshrc
아래는 추가한 .zhrc 파일의 20줄 정도를 나타낸 부분이다.
# Set personal aliases, overriding those provided by oh-my-zsh libs,
# plugins, and themes. Aliases can be placed here, though oh-my-zsh
# users are encouraged to define aliases within the ZSH_CUSTOM folder.
# For a full list of active aliases, run `alias`.
#
# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"



export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

# java env
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64/bin/java
export PATH=$JAVA_HOME/bin:$PATH
export CLASS_PATH=$JAVA_HOME/lib:$CLASS_PATH

#fly
export FLYCTL_INSTALL="/home/wsl/.fly"
export PATH="$FLYCTL_INSTALL/bin:$PATH"
이러한 문제가 발생하는 이유는 필자가 많은 shell (bashShell 등) 중에 zShell을 사용하고 있기 때문이다. fly 경로를 지정하지 않았기 때문에 설정 파일에 경로 지정이 필요하다.

5) Launch하기
사진 설명을 입력하세요.
$ fly launch --image flyio/hellofly:latest
명령어를 실행하면 아래와 같은 질문이 나오는데
? Do you want to tweak these settings before proceeding?
반드시 y를 입력해서 세팅을 해줘야 무료버전을 사용할 수 있다.
사진 설명을 입력하세요.
수정에서 가장 중요한 부분은 VM Memory로 256MB로 바꿔줘야만 무료로 사용할 수 있다.
사진 설명을 입력하세요.

6) fly,toml 파일 수정하기
설치가 완료되면 fly,toml 파일이 깔려있을 것이다. 이때 internal_port부분을 80으로 수정한다.
internal_port = 80
7) flyctl deploy
이후 flyctl deploy명령어를 실행해서 서버를 띄우면 완성~
$ flyctl deploy
```
