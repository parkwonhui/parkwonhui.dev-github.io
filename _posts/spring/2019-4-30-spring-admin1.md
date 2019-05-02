---
layout: post
title: 관리자 페이지
categories: [spring]
tags: [java,spring]
comments: true
---

### 관리자 추가
- 상품 페이지를 만들면서 오로지 관리자만이 상품을 등록할 수 있게 만들어야 한다
- 하나의 필드를 추가하여 0일 땐 일반유저, 1일 땐 관리자로 설정할 수 있지만 고객과 관리자의 데이터는 많이 다르므로 분리해야한다(예를들어 고객은 구매횟수나 구매금액이 필요하지만 관리자는 필요 없다)
- 유저, 관리자의 기능을 정리하여 필요한 데이터를 뽑아낸다

|  | 고객 | 쇼핑몰 관리자 |
|:--------|:--------|--------|
| 정의 | 상품을 구매하는 고객을 의미한다 | 쇼핑몰 운영자를 의미한다(개발자 x) QA와 테스터와도 구분된다 |
| 기능1 | 상품 조회 | 상품 조회 |
| 기능2 | 상품 구매 및 장바구니 | 상품 관리 |
| 기능3 | 상품 결제 | 고객 관리 |
| 기능4 | - | 주문 조회 및 관리 |
| 기능5 | - | 게시판 관리 |

- 표를 바탕으로 유저와 관리자의 데이터를 정의한다
- 너무 기능이 많으므로 장바구니, 결제 기능은 제외,  관리자도 주문, 게시판 기능은 제외하고 정의
- 유저는 총 구매 금액 , 한달 구매 금액 , 구매 등급 , 가입일 , 마지막 구매일
- 관리는 상품 보기/관리 권한, 고객 보기/관리 권한
- 정리된 데이터를 바탕으로 테이블을 정의한다

- 고객 테이블(Customer)

| 필드명 | 데이터형 | 설명 |
|---------|-----------|-------|
| user_seq | bigint | 유저 id |
| total_price | bigint | 총 구매 금액 |
| total_month_price | bigint | 이번달 구매 금액 |
| price_grade | tinyint | 구매 등급 |
| join_date | timestamp | 가입일 |
| last_buy_date |  timestamp | 마지막 구매일 |

- 관리자 테이블(Admin)

| 필드명 | 데이터형 | 설명 |
|---------|-----------|-------|
| user_seq | bigint | 유저 id |
| product_view_author | tinyint(1) | 상품 조회 권한 |
| product_update_author | tinyint(1) | 상품 관리 권한 |
| customer_view_author | tinyint(1) | 고객 조회 권한 |
| customer_update_author | tinyint(1) | 고객 관리 권한 |

- 데이터를 바탕으로 테이블 생성 쿼리를 작성한다
- 고객 테이블

~~~
CREATE TABLE `customer` (
  `user_seq` bigint NOT NULL,
  `total_price` bigint DEFAULT 0,
  `total_month_price` bigint DEFAULT 0,
  `price_grade` tinyint DEFAULT 0,
  `join_date` timestamp NULL DEFAULT NOW(),
  `last_buy_date` timestamp,
  PRIMARY KEY (`user_seq`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8
~~~
- 관리자 테이블

~~~
CREATE TABLE `admin`(
  `user_seq` bigint NOT NULL,
  `product_view_author` tinyint(1) DEFAULT 0,
  `product_update_author` tinyint(1) DEFAULT 0,
  `customer_view_author` tinyint(1) DEFAULT 0,
  `customer_update_author` tinyint(1) DEFAULT 0,
  PRIMARY KEY (`user_seq`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8
~~~

- 일반 고객과 관리자를 구분짓는 플래그를 user에 추가한다

~~~
ALTER TABLE USER ADD ADMIN TINYINT(1) DEFAULT 0;
~~~
- 관리자로 만들 유저는 ADMIN 필드 값을 1로 준다
- ADMIN에 해당 유저 정보를 추가한다
- 유저의 정보를 가져오는 쿼리에 admin 필드를 가져오도록 한다
~~~
INSERT INTO admin(user_seq, product_view_author, product_update_author, customer_view_author, customer_update_author)
VALUES(12, 1, 1, 1, 1);
~~~

### 페이지 정의
- 관리자의 기능을 바탕으로 페이지를 정의 한다
- 페이지는 2개. 상품 보기,관리 페이지, 회원 보기, 관리 페이지
- 상품은 조회, 추가, 삭제, 수정 기능이 기본적으로 들어가야 한다(페이징, 검색은 나중에)
- 회원은 조회, 추가, 수정 기능이 기본적으로 들어간다(페이징, 검색은 나중에)
- 아래와 같은 url을 정의 한다(이전에 정의했지만 재정의 해야한다. 관리자 페이지를 따로 만들므로)

| url | 설명 | Method |
|---------|-----------|-------|
| /admin/product/list | 상품 리스트 보기  | GET |
| /admin/product/{seq} | 상품이 있는지 체크  | POST |
| /admin/product/{seq} | 상품 상세 보기  | GET |
| /admin/product/post | 작성할 수 있는 권한이 있는지 체크 | POST |
| /admin/product/post | 새로운 상품 등록 페이지 이동 | GET |
| /admin/product/post | 새로운 상품 등록 | POST |
| /admin/product/post/{seq} | 작성할 수 있는 권한이 있는지 체크 | GET |
| /admin/product/post/{seq} | 기존에 있는 상품 페이지 이동 | POST |
| /admin/product/post/{seq} | 기존에 있는 상품 수정 | PUT |
| /admin/product/delete |  상품 삭제| GET |

| url | 설명 | Method |
|---------|-----------|-------|
| /admin/user/list | 고객 조회  | GET |
| /admin/user/{seq} | 고객이 있는지 체크 | POST |
| /admin/user/{seq} | 고객 상세 보기 | GET |
| /admin/user/post | 고객 추가 체크 | POST |
| /admin/user/post | 고객 추가 이동 | GET |
| /admin/user/post | 고객 추가 | PUT |
| /admin/user/post/{seq} | 고객 정보 수정 체크 | POST |
| /admin/user/post/{seq} | 고객 정보 수정 페이지 이동 | GET |
| /admin/user/post/{seq} | 고객 정보 수정  | PUT |
| /admin/user/delete |  고객 정보 삭제 | GET |

### 고객, 관리자 VO, Service, DAO, xml 생성
- 고객. 관리자 페이지의 고객 정보와 관련 있다.
- Service, DAO, xml 파일도 생성한다

~~~
import java.util.Date;
import lombok.Data;
@Data
public class CustomerVO{
     private Long userSeq;
     private Long totalPrice;
     private Long totalMonthPrice;
     private    Byte priceGrade;
     private Date joinDate;
     private Date lastBuyDate;
}
~~~
- 관리자. 관리자의 권한과 관련 있다

~~~
import lombok.Data;
@Data
public class AdminVO{
     private Long userSeq;
     private boolean productViewAuthor;
     private boolean productUpdateAuthor;
     private boolean customerViewAuthor;
     private boolean customerUpdateAuthor;
}
~~~

### 관리자 화면 추가
- 일반 고객과 관리자가 보는 화면이 다르다.
- userVO객체의 admin 값이 true일 때 관리자 메뉴가 보이도록 수정한다

~~~
<c:choose>
    <c:when test="${true eq userVO.admin}">
        <div class="col-md-3 col-xs-3">
            <a href="#">상품 관리</a>
        </div>
        <div class="col-md-3 col-xs-3">
            <a href="#">고객 관리</a>
        </div>
        <div class="dropdown col-md-3 col-xs-3">주문 관리</div>
        <div class="col-md-3 col-xs-3">게시판 관리</div>
    </c:when>
    <c:otherwise>
        <div class="col-md-3 col-xs-3">
            <a href="/main">메인화면</a>
        </div>
        <div class="col-md-3 col-xs-3">공지사항</div>
        <div class="dropdown col-md-3 col-xs-3">
            <div class="dropbtn">전체상품</div>
            <div class="dropdown-content">
                <a href="/product/list">디저트</a> <a href="/product/list">이유식</a>
            </div>
        </div>
        <div class="col-md-3 col-xs-3">
            <a href="/board/list?page=1&count=10">자유게시판</a>
        </div>
    </c:otherwise>
</c:choose>
~~~

### 상품 관리
- 상품 리스트 가져오기
- 상품 재고 필드 추가 및 VO, 쿼리 수정, 제품 pic 필드 -> img로 변경

~~~
alter table product add stock Long Default 0;
alter table product change pic img varchar(50)
~~~

- 메뉴에서 관리자 상품관리 페이지로 이동되도록 수정(관리자 상품관리, 상세페이지, 추가, 수정 페이지를 만든다)

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


