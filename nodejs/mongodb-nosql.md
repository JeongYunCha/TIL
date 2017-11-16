# mongodb

> 2017-11-14	



#### 1. NoSQL

NoSQL이란 SQL을 사용하지 않는 비관계형 데이터 베이스를 말한다.<br>관계형 데이터베이스는 시스템의 신뢰도를 높이지만 SQL문을 읽어들이고 실행하는데 많은 리소스가 필요, 성능이 떨어지기쉽다.  반면에 NoSQL은 성능을 최우선시, 자바스크립트 객체를 그대로 저장할수 있어서 노드에서 데이터를 저장하기에 좋다.  실시간 처리, 대용량 트래픽 필요한 메시징시스템, 클라우드 서비스로 서버를 구성하는 경우 성능이 좋은 NoSQL을 사용.<br>

Homebrew로 설치하기

```bash
$ brew install mongodb

# brew로 몽고디비 실행
$ brew services start mongodb

# brew로 몽고디비 종료
$ brew services stop mongodb

## /usr/local/etc/mongod.conf 의 파일에 dbpath 정보
# systemLog:
#   destination: file
#   path: /usr/local/var/log/mongodb/mongo.log
#   logAppend: true
# storage:
#   dbPath: /usr/local/var/mongodb
# net:
#   bindIp: 127.0.0.1
```

쉘에서 실행하기

```bash
$ mongo
>
```



#### 2. mongoose

자바스크립트 객체를 그대로 저장할수 있는 noSQL은 객체안 속성을 유연하게 변경하여 데이터 저장 가능하지만, 객체를 조회 할때는 공통 속성이 보장되지 않기때문에 제약이 생길수 있다. 

몽구스 모듈의 역할<br> 데이터베이스의 구조를 정의하는 스키마(틀)을 만들고 저장하려는 자바스크립트 객체와 데이터베이스 객체(스키마)를 서로 매칭하여 바꿀수있게 하는것을 오브젝터 맵퍼(object mapper)라고 한다.

