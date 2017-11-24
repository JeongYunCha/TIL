# 크롤링 기반의 웹서비스 만들기 

> 2017-11-23
>
> 





## 1. 데이터 수집

#### 1.1. API 사용해서 데이터 수집하기

- 인스타그램 API <https://www.instagram.com/developer/>
- 페이스북 API <https://developers.facebook.com/docs/graph-api>
- 트위터 API <https://developer.twitter.com/en/docs>
- 네이버 검색 API <https://developers.naver.com/docs/search/blog/>
- 다음카카오 검색 API <https://developers.kakao.com/docs/restapi/search>
- 구글맵 장소검색 API <https://developers.google.com/places/web-service/?hl=ko>

#### 1.2. 웹크롤링으로 데이터 수집하기

__1.2.1. 특정 사이트 구조 분석해 사이트에서 제공하는 컨텐츠를 수집__

- 메타서치 서비스 ([호텔스컴바인](https://www.hotelscombined.co.kr/),  [지그재그](https://zigzag.kr/), [네이버 가격비교/쇼핑몰리뷰](http://shopping.naver.com/detail/detail.nhn?nv_mid=5729606943&cat_id=50000265&frm=NVSHMDL&query=%EC%B9%B4%EB%A9%94%EB%9D%BC))
  - 각 사이트에 흩어진 정보를 모아 한곳에서 비교 검색
  - 컨텐츠 자체를 가져다 쓰지 않고 리스트 형식으로 사용자에게 제공.
  - 상세 선택 시, 링크를 통해 해당 사이트로 넘겨준다

__1.2.2. 특정 키워드에 대해 검색엔진에 검색된 결과리스트를 수집__

- [다이닝코드 - 추천 블로그 리스트](https://www.diningcode.com/profile.php?rid=dJ22npLWzNDD) 같은 경우에는 검색엔진을 통해 수집할수있겠지..?

<br>

## 2. 서비스 제공을 위한 데이터 가공

#### 2.1. 인덱싱 (indexing)

- 수집된 정보를 정리하여 나중에 쉽고 빠르게 찾을 수 있게 하는 작업. <br>수집 작업 중에 각 문서의 정보에 가중치(weight)와 연관도(relevance)를 부여해 저장


- 데이터 분석 (키워드 뽑아내기) : [자연어 처리(KoNLPy)](https://www.lucypark.kr/slides/2014-pyconkr/#1), [명사추출 및 빈도분석](http://konlpy.org/ko/v0.4.3/examples/wordcloud/) 
- 데이터 저장 (검색성능을 고려한 DB화): [Inverted Index](https://blog.lael.be/post/3056)

#### 2.2. 랭킹 (ranking)

- 순위 결정은 알고리즘을 활용해 사용자가 검색한 특정 키워드에 수많은 문서와 정보들 중 어떤것들을 먼저 보여주고 나중에 보여주느냐에 대한 순서를 정해주는 것이다. 이를 랭킹이라고 하는데 포털, 전자상거래, 커뮤니티 등 비즈니스 특성에 따라 다양한 정보와 항목들을 결합해 점수화하고 이에따라 순위를 결정짓는 랭킹 알고리즘을 만들 수있다. 

- 랭킹 알고리즘  = 검색 알고리즘? <br>주어진 검색어와 __연관된 정보__를 색인에서 모조리 찾아 내고. 그 중 __어느것이 사용자가 원하는 것인가__를 결정 하는 것	

- 다이닝코드 소개글 중 아이디어 발췌 

  - 읽어볼만한 기사: [네이버에서 ‘오빠랑’은 이제 그만 빅데이터 기반 맛집 검색 다이닝코드](http://www.ditoday.com/articles/articles_view.html?idno=18908)


  - 프랜차이즈 맛집이 식상하다면 “오래된집”으로 검색해 보세요. “강남 오래된집” 이렇게요. 가끔은 “부모님”으로 검색해서 부모님과의 외식도 좋습니다. 어떤 말로 검색해도 한눈에 랭킹을 볼 수 있습니다. 당신만의 키워드를 찾아보세요.
  - __자체 서비스 내부에서 수집한 사용자 데이터__ : 다이닝코드 사용자가 직접 맛집에 대하여 별점을 매긴 데이터가 랭킹에 영향을 미칩니다. 어뷰징된 별점으로 판별되는 사용자 평가는 랭킹 결과에 잘 반영되지 않습니다.
  - __수집된 블로그 리뷰를 바탕으로 데이터 신뢰도 만들기__: 맛집 블로그 내용의 우수성, 블로거의 평판도, 블로그에 대한 다른 사용자의 긍정적/부정적 반응 등 다양한 요소로 판단이 됩니다.
  - __데이터의 실시간성__ : 최근에 작성된 사용자 평가, 좋아요, 블로그는 가중치가 주어집니다. 오래되고 전통있는 맛집이 항상 일등하는 것을 방지하고, 최근에 인기있는 맛집이 상단에 노출될 수 있는 기회를 제공합니다.		

#### 2.3. 시각화 아이디어

- 워드클라우드
- 지리정보기반 시각화
- 트위터 api로 키워드에 대한 실시간 소셜 반응 보여주기 ([네이버 실시간검색](https://search.naver.com/search.naver?where=realtime&sm=tab_rea&query=%EC%A7%80%EC%A7%84&ie=utf8&best=1))
- 인스타그램 location API로 [특정 장소에 대한 소셜 이미지](https://www.instagram.com/explore/locations/216489075/great-market-hall/) 보여주기기 





배치 자동화 (AWS Batch)



client-server 통신 (소켓통신 / Rmote Procedure Call)

API 만들어 웹어플리케이션과 데이터 주고받기 (Restful API)

[RPC에서 REST까지 간단한 개념소개](https://www.slideshare.net/WonchangSong1/rpc-restsimpleintro)

