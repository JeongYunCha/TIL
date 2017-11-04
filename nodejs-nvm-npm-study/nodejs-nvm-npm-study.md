# Node.js 시작하기

### 1. nvm 
#### 1.1 nvm이란 
 nvm (Node Version Manager)을 통해 node를 설치하면 <br/>
 여러 버전을 복수로 설치해 쉽게 관리 할 수 있고 특정 버전을 선택하여 사용 할 수 있다.
#### 1.2 nvm 설치
````
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.4/install.sh | bash

````
 
#### 1.3 nvm 명령어
- nvm에서 지원하는 node 버전 확인하기
````
$ nvm ls-remote

````
- node 최신 버전 설치하기
````
$ nvm install node

````
- node 특정 버전 설치하기 <br/>
변경 사항이 많은 최신 버전보다 LTS 버전을 사용하는 것을 권장한다.<br>
([node.js 사이트](https://nodejs.org/ko/)에서 LTS 버전 확인 가능)
````
$ nvm install v8.9.0

````
- 현재 사용중인 node 버전 확인하기 

````
$ nvm current // 또는
$ node -v

````
- 설치된 node 버전 확인하기

````
$ nvm ls

````
- 특정 버전 사용하기 

````
$ nvm use v8.9.0

````
- default 사용 버전 설정하기

````
$ nvm alias default v8.9.0

````
### 2. npm
#### 2.1 npm이란 
npm(Node Package Manger)을 사용하면 Node.js 패키지 설치와 버전관리를 쉽게 할 수 있다.<br/>
- [모듈화와 CommonJS](http://poiemaweb.com/nodejs-npm#1-모듈화와-commonjs)
- [지역(local)설치와 전역(global)설치](http://poiemaweb.com/nodejs-npm#22-지역local-설치와-전역global-설치)
- [package.json과 의존성(dependency) 관리](http://poiemaweb.com/nodejs-npm#23-packagejson과-의존성dependency-관리)
- [Semantic versioning(유의적 버전)](http://poiemaweb.com/nodejs-npm#24-semantic-versioning유의적-버전)
#### 2.2 npm 설치
npm은 Node.js 설치시 기본으로 함께 설치 되지만 최신버전이 아닐수 있으니 따로 버전 업데이트를 해주면 좋다.<br>

- npm 버전 확인하기
````
$ npm -v
````
- npm 최신버전 업데이트 하기
````
$ npm install npm@latest -g
````

#### 2.3 npm 명령어
- 명령어 모를 때 콘솔에서 빨리 찾아보기
````
$ npm <command> -h     // quick help on <command>
$ npm -l               // display full usage info
$ npm help <term>      // search for help on <term>
````
- [package.json](https://docs.npmjs.com/files/package.json) 기본설정으로 파일 만들기 
````
$ npm init -y
````
- [package.json](https://docs.npmjs.com/files/package.json)에 명시된 의존 패키지 한번에 설치하기
````
$ npm install 
````

- 특정 패키지 설치하기 1<br>
패키지 설치와 함께 package.json의 dependencies에 설치된 패키지와 버전을 기록한다.
````
$ npm install <패키지명>
````
- 특정 패키지 설치하기 2<br>
devDependencies(개발시에만 사용하는 의존 패키지)에 설치된 패키지와 버전을 기록한다.
````
$ npm install <패키지명> --save-dev
````
- 특정 패키지 설치하기 3
````
$ npm install <패키지명> --save-exact  // 설치된 버전을 범위 지정없이 기록한다.
$ npm install <패키지명>@<특정버전>      // 패키지 특정버전 지정
````
- [Semantic versioning](https://docs.npmjs.com/misc/semver) 으로 버전 관리하기
