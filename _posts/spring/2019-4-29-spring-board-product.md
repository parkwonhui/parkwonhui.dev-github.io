---
layout: post
title: 게시판 만들기-제품 페이지 제작
categories: [spring]
tags: [java,spring,board]
comments: true
---
### 제품 페이지 제작
- 마켓컬리, 쿠팡, 웹쇼핑몰 처럼 상품의 목록이 나온는 상품 페이지 제작
- 제품에 대한 정보를 뽑아내고 DB 생성및 쿼리, VO 등을 작성한다
- 카테고리 디저트는 1005, 이유식은 1006

| 필드명 | 데이터형 | 설명 |
|---------|-----------|-------|
| product_seq | bigint(20) | 상품 고유 시퀀스  |
| category | bigint(20)  | 상품 카테고리 |
| pic | varchar(30) | 상품 사진 |
| title | varchar(20) | 상품 이름 |
| price |  int | 상품 가격 |
| text | varchar(100)| 상품 설명 |
| count | bigint(20) | 조회수 |
| product_del | tinyint(1) | 삭제 여부 |
| user_seq| bigint(20) | 작성자 시퀀스 |

- 상품 DB 생성 쿼리문

~~~
CREATE TABLE `product` (
  `PRODUCT_SEQ` bigint(20) NOT NULL AUTO_INCREMENT,
  `CATEGORY` int NOT NULL,
  `PIC` text DEFAULT 'img/1.jpg',
  `TITLE` varchar(20) NOT NULL,
  `PRICE` bigint NOT NULL DEFAULT 0,
  `TEXT` varchar(100) DEFAULT '',
  `COUNT` bigint(20) DEFAULT 0,
  `PRODUCT_DEL` bigint(20) DEFAULT 0,
  `USER_SEQ` bigint(20),
  PRIMARY KEY (`PRODUCT_SEQ`)
  
) ENGINE=InnoDB AUTO_INCREMENT=97 DEFAULT CHARSET=utf8
~~~
- 임시 데이터 넣기

~~~
INSERT INTO PRODUCT(CATEGORY, TITLE, PRICE, TEXT)
VALUES(1005, '달콤유자케익', 20000, '유자를 흠뻑 넣은 케익');
INSERT INTO PRODUCT(CATEGORY, TITLE, PRICE, TEXT)
VALUES(1005, '자몽이슬톡톡', 3000, '이슬 톡톡');
INSERT INTO PRODUCT(CATEGORY, TITLE, PRICE, TEXT)
VALUES(1005, '머랭쿠키', 2000, '머랭~머랭~');
~~~

### URL 결정
- 마켓컬리에서 소분류를 선택 시 카테고리가 달라진다
- 즉 하나의 테이블에서 대분류, 소분류에 따라 데이터를 다르게 가져온다
https://www.kurly.com/shop/goods/goods_list.php?category=908003
- 베스트 상품은 기존 카테고리가 있고 그 중에서 베스트 상품 선별 
- 상품에 관한 기능은 상품 조회, 상품 등록, 상품 수정, 상품 삭제가 있다(상세페이지 X)

|url|설명|Method|
|:----|:----|:-----|
|/product/list | 상품 리스트 보기 |GET|
|/product/post | 작성할 수 있는 권한이 있는지 체크 | GET |
|/product/post | 새로운 상품 등록 | [POST |
|/product/post/{seq} | 작성할 수 있는 권한이 있는지 체크 | GET |
|/product/post/{seq} | 기존에 있는 상품 수정 | [POST |
|/product/delete | 상품 삭제 | GET |

### Controller, Service , VO
- product 테이블의 데이터를 불러오는 쿼리

~~~
<select id="getProductVOList" resultType="ProductVO">
           SELECT product_seq as productSeq
                   , category
                   , pic
                   , title
                   , price
                   , text
                   , count
                   , product_del as productDel
                   , user_seq as userSeq
           FROM product         
     </select>
~~~
- Service

~~~
public ResultMap getProductVOList(){
    List<ProductVO> list = dao.getProductVOList();
    ResultMap resultMap = new ResultMap();
    resultMap.setStatus("200");
    resultMap.put("list", list);
    return     resultMap;
}
~~~
- Conroller

~~~
@RequestMapping(value = "/list", method = RequestMethod.GET)
public String list(Model model) throws Exception {
    ResultMap resultMap = service.getProductVOList();
    model.addAllAttributes(resultMap);
    
    return "product/list";    
}
~~~

###  View
- list.jsp 를 생성하고 상품 리스트를 뿌려주는 화면 구성

~~~
<h2>상세 메뉴</h2>
<div><button id="product-new-product-create" class="btn  btn-info">새 상품 추가</button></div>
<div id="product-list" >
<c:forEach var = "product" items = "${list}">
<div class="row col-md-4 col-xs-12 product-elements">
     <input type="hidden" value="${product.productSeq}"/>
     <input type="hidden" value="${product.category}"/>
     <div><img src="/resources/${product.pic}" /></div>
     <div class="product-in-text">${product.title}</div>
     <div class="product-in-text">${product.price}원</div>
     <div class="product-in-text">${product.text}</div>
</div>
</c:forEach>
</div><!-- product-list -->
~~~

- 상품 리스트 페이지로 이동하는 url 추가

~~~
<div class="dropbtn">전체상품</div>
    <div class="dropdown-content">
        <a href="/product/list">디저트</a>
        <a href="/product/list">이유식</a>
    </div>
</div>
~~~


<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIA*BLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = 'https://parkwonhui.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>