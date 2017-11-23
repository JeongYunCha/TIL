# 웹스크래퍼 만들기

> 2017-11-14
>
> 



웹크롤링 (web crawling) : 웹에서 링크를 타고 다니며 웹피이지들을 수집하는 행위

웹스크래핑 (web scraping) : 웹사이트에서 정보를 추출하는 행위

크롤러 (crawler) : 크롤링하는 소프트웨어 

[검색엔진 & 웹크롤러](https://brunch.co.kr/@highfree/25)

[웹서버 검색엔진 봇 접근 제한하기](http://kensei.co.kr/270)

[Scrapy를 이용한 뉴스 크롤링 하기](http://excelsior-cjh.tistory.com/entry/04-Scrapy%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%89%B4%EC%8A%A4%ED%81%AC%EB%A1%A4%EB%A7%81-%ED%95%98%EA%B8%B0)

1. **수집**(crawling: 크롤링): 웹의 어디에 어떤 정보가 있는지 알아내는 작업.
2. **색인**(indexing: 인덱싱): 수집된 정보를 정리하여 나중에 쉽고 빠르게 찾을 수 있게 하는 작업.
3. **순위의 결정과 제공**(ranking and serving: 랭킹과 서빙): 원하는 정보를 색인으로부터 꺼내서 사용자에게 보여주는 작업

순위를 매기는방법 (검색 알고리즘)<br>- 주어진 검색어와 연관된 정보를 색인에서 모조리 찾아 내는 것 <br>- 찾아낸 정보 중 어느것이 사용자가 원하는 것인가를 결정 하는 것







urllib.requests, BeatifulSoup, Selenium - webdriver, scrapy

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
│   ├── pipelines.py		데이터를 크롤링해 온 후 데이터가공 및 DB저장
│   └── settings.py			프로젝트 모듈간 연결 및 설정정의 
└── scrapy.cfg
```