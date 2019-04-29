---
layout: post
title: 게시판 만들기-제품 등록
categories: [spring]
tags: [java,spring,board]
comments: true
---

### 상품 등록2
- 임의의 데이터를 출력하는 것 까지 완료
- 이제 상품 등록을 페이지에서 하는 기능을 추가 필요
- 이미지는 upload기능이 들어가므로 나중에 구현한다
- 유저, 관리자가 나뉘어져 있지 않도록 권한 체크와 관리자 페이지는 등록 다음으로 구현한다

### Controller, Service, Query 처리
- 상품 생성 날짜가 필요하여서 생성 날짜 필드를 추가하였다

~~~
Alter table product  Add create_date Timestamp  DEFAULT NOW() NOT NULL;
~~~
- 상품을 등록하는 쿼리문을 만든다

~~~
<insert id="createProductVO" parameterType="ProductVO">
           INSERT INTO product
           (                    
                   category
                  , pic
                  , title
                  , price
                  , text
                  , user_seq
           )
           VALUES
           (
                #{category}
                ,#{pic}
                ,#{title}
                ,#{price}
                ,#{text}
                ,#{userSeq}
                ,#{userSeq}
           )
     </insert>
~~~
- Service에서는 상품의 값이 올바르게 들어갔는지 체크하고 쿼리문을 호출한다

~~~
@Override
public ResultMap createProduct(ProductVO productVO) throws Exception{
    int category = productVO.getCategory();
    String picSrc = productVO.getPic();
    String title = productVO.getTitle();
    Long price = productVO.getPrice();
    String text = productVO.getText();
    
    if(title == null || text == null || picSrc == null) {
        throw new LogicException("990", "알 수 없는 에러가 발생했습니다");
    }
    
    if(title.isEmpty()) {
        throw new LogicException("1000", "상품명을 입력해주세요");    
    }
    
    if(TITLE_SIZE_MAX < title.length()) {
        throw new LogicException("1001", "상품명이 너무 깁니다");
    }
    
    // 이미지 체크
    
    if(0 >= price) {
        throw new LogicException("1004", "가격은 1원 이상이여야 합니다");
    }
    
    if(PRICE_SIZE_MAX <= price) {
        throw new LogicException("1006", "가격은 1,000,000,000원 이하만 입력 가능합니다");
    }
    
    if(text.isEmpty()) {
        throw new LogicException("1007", "설명을 입력해주세요");                
    }
    
    if(TEXT_SIZE_MAX <= text.length()) {
        throw new LogicException("1008", "설명은 100자 이하여야 합니다");
    }
    
    int result = dao.createProduct(productVO);
    if(0 == result) {
        throw new LogicException("990", "알 수 없는 에러가 발생했습니다");
    }
    
    ResultMap resultMap = new ResultMap();
    resultMap.setStatus("200");
    resultMap.setMsg("");
    
    return resultMap;
}
~~~

- Contorller에서는 /post url 을 POST, GET 방식 2가지의 방식으로 받는다
- POST 방식은 상품 등록이 가능한 권한이 있는지 체크한다
- GET 방식은 상품 등록 페이지로 이동한다
- 상품 등록 요청 url은 method를 PUT으로 받는다
- json 데이터와 ProductVO가 매핑이 되지 않는 상황 발생 => @RequestBody를 추가하니 매핑되었음

~~~
@RequestMapping(value = "/post", method = RequestMethod.POST)
public String checkPost(HttpSession session, Model model) throws Exception {
    ResultMap resultMap = service.getCheckPost();
    model.addAllAttributes(resultMap);
    
    return JSON_VIEW;    
}

@RequestMapping(value = "/post", method = RequestMethod.PUT)
public String postProduct(@RequestBody ProductVO productVO, HttpSession session, Model model) throws Exception {
    ResultMap resultMap = service.createProduct(productVO);
    model.addAllAttributes(resultMap);
    
    return JSON_VIEW;
}
~~~

### View
- '등록' 버튼을 클릭하면 해당 데이터를 PUT method로 전달하고 성공할 시 list로 페이지 이동되도록 만듬

~~~
// 페이지 이동
$('#product-new-product-create').click(function(){
     console.log('product-new-product-create');
     ajaxRequest("/product/post", "", "POST",  "location.href='/product/post'");
});

// 상품 등록
$("#product-new-add-product").click(function(){
     var category = $('#product-add-select-input').val();
     var title = $('#product-title-input-text').val();
     var price = $('#product-price-input-text').val();
     var text = $('#product-text-input-text').val();
     
     if(category == undefined || title == undefined || price ==  undefined || text == undefined){
           return;
     }
     price = price.replace(",", "");
     
     var data ={
                "category":category,
                "title":title,
                "price":price,
                "text":text
     };
     
     ajaxRequest("/product/post", JSON.stringify(data), "PUT",  "location.href='/product/list'");    
});
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

