# 웹크롤러 만들기

> 2017-11-14





urllib.requests

BeatifulSoup

Selenium - webdriver



scrapy

[Scrapy를 이용한 뉴스 크롤링 하기](http://excelsior-cjh.tistory.com/entry/04-Scrapy%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%89%B4%EC%8A%A4%ED%81%AC%EB%A1%A4%EB%A7%81-%ED%95%98%EA%B8%B0)



```bash
$ source activate <가상환경명>			# 웹크롤링 가상환경으로 진입

$ pip install scrapy				# scrapy 설치
$ scrapy startproject <프로젝트명>		# Scrapy 프로젝트 생성
```



프로젝트 구조 

```
project-name/
│   ├── spiders 			크롤링할 로직 및 내용들을 프로그래밍
│   │	 └── __init__.py
│   │ 		
│   ├── __init__.py			
│   ├── items.py 			데이터를 크롤링해 올 때 해당 데이터를 클래스(class)형태로 만들어줌
│   ├── middlewares.py		
│   ├── pipelines.py		데이터를 크롤링해 온 후 데이터를 처리해 줄 때 사용
│   └── settings.py			프로젝트 모듈간 연결 및 설정정의 
└── scrapy.cfg
```