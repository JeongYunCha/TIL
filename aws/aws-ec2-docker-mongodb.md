## EC2 Linux, Mac OS X에서 접속하기

> 참고링크:  [아마존 웹 서비스를 다루는 기술 4장 - 4.2. Linux, Mac OS X에서 접속하기](http://pyrasis.com/book/TheArtOfAmazonWebServices/Chapter04/04/02) 

Linux와 Mac OS X에서는 pem 파일을 변환하지 않아도 바로 사용가능.<br> chmod 명령어로 권한을 변경하는 것은 한 번만 하면된다. 

```bash
$ chmod 600 <file-path>/awskeypair.pem
```

서버를 신뢰하겠는지 묻는 문구. yes를 입력하면 EC2 인스턴스에 접속이 완료.

```bash
$ ssh -i <file-path>/awskeypair.pem ec2-user@<host주소>
```

 config파일에 pem파일경로를 지정해 주면 ``` ssh ec2-user@<host주소> ``` 로 접속가능

```bash
$ sudo vim /etc/ssh/ssh_config
```

```bash
# 아래내용 ssh_config파일에 추가
IdentityFile <file-path>/awskeypair.pem
```



## EC2 Linux 인스턴스에 Docker 설치하기 





## MongoDB 설치/설정하기

> 참고링크: [한번에-끝내는-AWS-EC2에-MongoDB-설치하고-보안설정하기](http://chichi.space/2017/05/12/%ED%95%9C%EB%B2%88%EC%97%90-%EB%81%9D%EB%82%B4%EB%8A%94-AWS-EC2%EC%97%90-MongoDB-%EC%84%A4%EC%B9%98%ED%95%98%EA%B3%A0-%EB%B3%B4%EC%95%88%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0/)

1. 접속후 root권한으로 변경

```bash
[ec2-user@ip-000-00-00-000 ~]$ sudo su
[root@ip-000-00-00-000 ec2-user]#
```

2. mongodb 설치하기

```bash
$ vi /etc/yum.repos.d/mongodb-org-3.4.repo

# 위경로 파일 생성후 아래내용 입력

[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/amazon/2013.03/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

```bash
$ yum install -y mongodb-org
```

3. mongod 실행/종료하기 (root계정일때 )

```bash
$ service mongod start
$ service mongod restart
$ service mongod stop
```

4. mongodb 접속하기

```bash
$ mongo
```

5. mongodb 계정생성

```bash
# 관리자 계정생성
use admin
db.createUser({ user: "사용자 계정",
  pwd: "패스워드",
  roles: [ "userAdminAnyDatabase",
    "dbAdminAnyDatabase",
    "readWriteAnyDatabase"
  ]
})

# 일반 계정생성
use customDB
db.createUser({ user: "계정",
  pwd: "패스워드",
  roles: ["dbAdmin", "readWrite"]
})
```

6. mongodb 보안설정

```bash
$ vi /etc/mongod.conf
```

```bash
# bind된 ip 이외에도 접속가능하게 하기 (EC2 Security Group에서 접근 제어)
# network interfaces
net:
  port: 27017
  #bindIp: 127.0.0.1  
  
# MongoDB 익명으로 로그인 막기
security:
    authorization: enabled

```


## EC2 SSH 연결 단순화 하기

> 참고링크: [Simplifying EC2 SSH Connenections 번역글](https://charsyam.wordpress.com/2011/12/08/발-번역-ec2-ssh-연결-단순화-하기/)

