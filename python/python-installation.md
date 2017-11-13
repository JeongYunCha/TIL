[초보몽키 파이썬 설치가이드](https://wayhome25.github.io/django/2017/04/29/python-dev-environments/#pyenv-설치) 를 참고하여 파이썬 개발환경 설정을 했다!



### 1. pyenv

파이썬 버전관리 프로그램 설치

```bash
$ brew update
$ brew install pyenv

$ vi ~/.zshrc  		# .zshrc파일 열어서 아래 내용 입력

export PYENV_ROOT=/usr/local/var/pyenv
if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi

$ source ~/.zshrc 	# 재실행
$ exec "$SHELL" 	# shell 재실행
```



### 2. pyenv로 python 설치

```bash
$ pyenv version
$ pyenv install --list 	# 설치 가능한 패키지 목록 (파이썬 버전별 목록)
$ pyenv install 3.6.0 	# python 설치

$ python --version		# 현재 사용중인 버전 확인
$ pyenv versions		# .pyenv 폴더안에 설치된 버전 리스트 확인

$ pyenv shell 3.6.0		# pyhotn 3.6.0으로 shell 실행 > autoenv를 사용하면 별도 지정이 필요 없음

$ pyenv global 3.5.3	# 기본으로 실행된 python 버전 변경
$ pyenv global system	# 시스템에 설치된 python으로 다시 변경


```

- mac os 하이시에라 관련 설치오류 

```bash
Downloading Python-3.6.0.tar.xz...
-> https://www.python.org/ftp/python/3.6.0/Python-3.6.0.tar.xz
Installing Python-3.6.0...
ERROR: The Python ssl extension was not compiled. Missing the OpenSSL lib?

Please consult to the Wiki page to fix the problem.
https://github.com/pyenv/pyenv/wiki/Common-build-problems

BUILD FAILED (OS X 10.13 using python-build 20160602)
```

- 해결방법

```bash
brew uninstall openssl && brew install openssl && CFLAGS="-I$(brew --prefix openssl)/include" LDFLAGS="-L$(brew --prefix openssl)/lib" pyenv install 3.6.2
# 또는 
CFLAGS="-I$(brew --prefix openssl)/include" LDFLAGS="-L$(brew --prefix openssl)/lib" pyenv install 3.6.3
```



### 3. virtualenv 설치 

virtualenv(독립된 개발환경을 제공해주는 프로그램) 를 활용하여 가상 개발환경을 구축한다.

```bash
# brew로 설치
$ brew install pyenv-virtualenv

# 설치 후 .zshrc 파일에 아래 내용 추가
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```



### 4. pip & requirement.txt 로 패키지 관리하기

```bash
$ pip install <패키지명>
$ pip freeze 						 # 설치한 패키지 리스트 확인

$ pip3 freeze > requirements.txt 	 # 패키지 목록을 txt 파일로 만들기
$ pip3 install -r requirements.txt 	 # 한번에 패키지 설치
```



### 5. 가상환경 설정

##### 5.1. pyenv local

```bash
$ pyenv local fc-python(가상환경이름)
$ pyenv global <가상환경이름>		 # 기본으로 사용할 환경 설정
```

##### 5.2. autoenv

- autoenv를 설치하고 프로젝트 폴더에 .env 파일을 만들어 자동으로 가상환경이 실행되도록 만든다.
- autoenv : Directory-based environments, 폴더 안에 .env 파일이 있으면 해당 폴더에 들어갈 때 자동으로 가상환경이 실행된다.

```bash
$ brew install autoenv # 설치 (Using Homebrew)
$ echo "source $(brew --prefix autoenv)/activate.sh" >> ~/.zshrc
$ exec "$SHELL" # 재실행

### .env 파일 작성 및 실행
# 프로젝트 폴더로 이동 후
$ touch .env
$ vim .env

# .env 파일에 아래 내용 입력   
$ pyenv activate css-3.6.0 # 원하는 가상환경 이름 (virtualenv로 생성한) 을 입력
$ cd ./ # 나갔다가 다시 들어오면 virtualenv 환경이 켜짐
```









