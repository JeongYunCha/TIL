# python 시작하기

> 2017-11-13
>
> [pyenv + virtualenv + autoenv 를 통한 Python 개발 환경 구축하기](https://ansuchan.com/how-to-set-python-dev-env/) 를 참고하여  내가 적용한 내용을 정리하였다.  pyenv install 로 파이썬 설치시 macOS High Sierra 문제로 설치가 되지않는 문제가 있었는데 함께 정리해 두었다.



### 1. pyenv로 파이썬 버전 관리하기 

1.1. pyenv 설치하기

```bash
$ brew update
$ brew install pyenv

# 사용중인 쉘(bash /zsh)에 맞게 입력
$ echo 'eval "$(pyenv init -)"' >> ~/.zshrc
$ echo 'eval "$(pyenv init -)"' >> ~/.bash_profile

$ source ~/.zshrc 	# 재실행
$ exec "$SHELL" 	# shell 재실행
```

1.2. pyenv로 python 설치하기

```bash
$ pyenv version			# 현재 사용중인 파이썬 버전 확인
$ pyenv versions		# .pyenv 폴더안에 설치된 버전 리스트 확인

$ pyenv install -list 	# .pyenv로 설치 가능한 파이썬 버전 목록 확인 
$ pyenv install 3.6.0 	# .pyenv로 python 특정 버전 설치
```

1.3. pyenv로 python 설치하기 __→ mac os 하이시에라 관련 설치오류 __

```bash
Downloading Python-3.6.0.tar.xz...
-> https://www.python.org/ftp/python/3.6.0/Python-3.6.0.tar.xz
Installing Python-3.6.0...
ERROR: The Python ssl extension was not compiled. Missing the OpenSSL lib?

Please consult to the Wiki page to fix the problem.
https://github.com/pyenv/pyenv/wiki/Common-build-problems

BUILD FAILED (OS X 10.13 using python-build 20160602)

# 해결방법
brew uninstall openssl && brew install openssl && CFLAGS="-I$(brew --prefix openssl)/include" LDFLAGS="-L$(brew --prefix openssl)/lib" pyenv install 3.6.2
# 또는 
CFLAGS="-I$(brew --prefix openssl)/include" LDFLAGS="-L$(brew --prefix openssl)/lib" pyenv install 3.6.3
```



### 2. virtualenv로 파이썬 개발 환경 관리하기 

virtualenv(독립된 개발환경을 제공해주는 프로그램) 를 활용하여 가상 개발환경을 구축한다.

2.1. pyenv-virtualenv 설치하기

```bash
$ brew install pyenv-virtualenv

# 사용중인 쉘(bash /zsh)에 맞게 입력
$ echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc
$ echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bash_profile

$ source ~/.zshrc 	# 재실행
$ exec "$SHELL" 	# shell 재실행
```

2.2. pyenv-virtualenv로  새로운 개발환경 만들기

```bash
# pyenv virtualenv <PYTHON_VERSION> <VIRTUAL_ENV_NAME> 
$ pyenv virtualenv 3.6.0 my-virtual 	# my-virtual이라는 이름의 가상 환경을 추가
$ pyenv virtualenv versions 			# 추가된 가상 환경 리스트 확인

# 가상환경 실행 및 종료
$ source activate my-virtual
$ source deactivate

```



### 3. pip & requirement.txt 로 패키지 관리하기

```bash
$ pip install <패키지명>

$ pip list > requirements.txt 		 # 패키지 목록을 txt 파일로 만들기
$ pip install -r requirements.txt 	 # 한번에 패키지 설치하기
```



### 4. autoenv로 자동 실행하기

4.1. autoenv 설치하기<br> - [autoenv](https://github.com/kennethreitz/autoenv/blob/master/activate.sh) 는 터미널에서 디렉토리가 변경될 때마다 폴더 안에 있는 .env 파일을 찾는 스크립트이다.

```bash
$ brew install autoenv

# 사용중인 쉘(bash /zsh)에 맞게 입력
$ echo 'source $(brew --prefix autoenv)/activate.sh' >> ~/.zshrc
$ echo 'source $(brew --prefix autoenv)/activate.sh' >> ~/.bash_profile

$ source ~/.zshrc 	# 재실행
$ exec "$SHELL" 	# shell 재실행
```

4.2. autoenv 사용하기<br> - 프로젝트 폴더안에 `.env` 파일을 생성하고 해당 디렉토리에서 자동으로 실행시키고 싶은 스크립트를 넣어두면 된다.

```bash
# ~/project_folder/.env

echo “***********************************”  
echo “Python Virtual Env > Python 2.7.14”  
echo “***********************************”

source activate my-virtual
```







