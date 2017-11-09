# Node.js 시작하기

### 



### 1. nvm 

#### 1.1 nvm이란 
 nvm (Node Version Manager)을 통해 node를 설치하면
 여러 버전을 복수로 설치해 쉽게 관리 할 수 있고 특정 버전을 선택하여 사용 할 수 있다.

변경 사항이 많은 최신 버전보다 LTS 버전을 사용하는 것을 권장한다. ([node.js 사이트](https://nodejs.org/ko/)에서 LTS 버전 확인 가능)

#### 1.2 nvm 설치
````bash
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.4/install.sh | bash
````

#### 1.3 nvm으로 node 설치, 버전관리하기
````bash
$ nvm ls-remote				// 설치 가능한 node 버전목록 확인하기
$ nvm install node			// node 최신버전 설치하기
$ nvm install v8.9.0		// node 특정버전(LTS) 설치하기

$ nvm current 				// 사용중인 node 버전 확인하기

$ nvm ls					// 설치된 node 버전 목록 확인하기
$ nvm use v8.9.0			// 특정 버전 사용하기
$ nvm alias default v8.9.0	// default 사용 버전 설정하기
````


### 2. npm

##### 2.1 npm이란

npm(Node Package Manger)을 사용하면 Node.js 패키지 설치와 버전관리를 쉽게 할 수 있다.

- [모듈화와 CommonJS](http://poiemaweb.com/nodejs-npm#1-모듈화와-commonjs)
- [지역(local)설치와 전역(global)설치](http://poiemaweb.com/nodejs-npm#22-지역local-설치와-전역global-설치)
- [package.json과 의존성(dependency) 관리](http://poiemaweb.com/nodejs-npm#23-packagejson과-의존성dependency-관리)
- [Semantic versioning(유의적 버전)](http://poiemaweb.com/nodejs-npm#24-semantic-versioning유의적-버전)
##### 2.2 npm 설치

````bash
$ npm -v						// 모듈 설치 전, npm 버전 확인하기
$ npm install npm@latest -g		// npm 최신버전 업데이트 하기
````
##### 2.3 npm 으로 모듈 설치, 버전 관리하기

````bash
$ npm <command> -h		// quick help on <command>
$ npm -l				// display full usage info
$ npm help <term>		// search for help on <term>

$ npm init -y				// pakage.json 기본설정파일 만들기
$ npm install 				// pakage.json에 명시된 의존패키지 한번에 설치

$ npm install <패키지명>	  			// 특정패키지 설치 (dependencies에 기록)
$ npm install <패키지명> --save-dev		// 특정패키지 설치 (devDependencies에 기록 - 개발시에만 사용)

$ npm install <패키지명> --save-exact  // 설치된 버전을 범위 지정없이 기록한다.
$ npm install <패키지명>@<특정버전>      // 패키지 특정버전 지정
````
- [package.json](https://docs.npmjs.com/files/package.json) 문서 참고
- [Semantic versioning](https://docs.npmjs.com/misc/semver) 으로 버전 관리하기




### 3. Node.js

```bash
$ node -v				// 사용중인 node 버전 확인하기
$ node server.js 		// js파일 실행하기
```

