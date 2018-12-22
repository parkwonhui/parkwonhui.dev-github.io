---
layout: post
title: 공공 데이터 open api
categories: [server]
tags: [server,openapi]
comments: true
---

# 공공 데이터 포털 OpenAPI 사용법
### API 신청
- https://www.data.go.kr
- 자신이 활용하고 싶은 데이터를 찾는다
- 활용신청 버튼을 누른다
- 활용신청이 끝나면 곧바로 사용할 수 있다
- 지역코드는 [여기](https://www.mois.go.kr/frt/bbs/type001/commonSelectBoardArticle.do?bbsId=BBSMSTR_000000000052&nttId=61552)서 확인할 수 있다

### 개발계정 API키 받기
- 마이페이지-개발계정 메뉴에서 '일반 인증키 받기' 선택
- 참고문서에서 API 사용법을 확인한다
- 내가 신청한 API 는 단독/다가구 전월세 자료이고 아래 url로 요청하면 결과를 받을 수 있다고 적혀있다
- http://openapi.molit.go.kr:8081/OpenAPI_ToolInstallPackage/service/rest/RTMSOBJSvc/getRTMSDataSvcSHRent?LAWD_CD=11110&DEAL_YMD=201512&serviceKey=서비스키
- 위 url을 주소창에 입력하면 다음결과를 받을 수 있다

~~~
<response>
<header>
<resultCode>00</resultCode>
<resultMsg>NORMAL SERVICE.</resultMsg>
</header>
<body>
<items>
<item>
<건축년도>1991</건축년도>
<계약면적>53.76</계약면적>
<년>2015</년>
<법정동> 청운동</법정동>
<보증금액> 25,000</보증금액>
<월>12</월>
<월세금액> 0</월세금액>
<일>11~20</일>
<지역코드>11110</지역코드>
</item>
<item>
<건축년도>1995</건축년도>
<계약면적>95.48</계약면적>
<년>2015</년>
<법정동> 청운동</법정동>
<보증금액> 30,000</보증금액>
<월>12</월>
<월세금액> 50</월세금액>
<일>21~31</일>
<지역코드>11110</지역코드>
</item>
....
~~~

### Parsing
- 서버로 요청한 결과값은 글자 덩어리이므로 데이터 셋에 알맞게 Parsing해야함
- 아래는 XML 데이터를 파싱해서 출력하는 예제

~~~
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;
import org.w3c.dom.Document;
import org.w3c.dom.Element;
import org.w3c.dom.Node;
import org.w3c.dom.NodeList;
public class Main {
       
       public static String getValue(String item, Element eElement) {
       
              // 몇몇 태그가 없는 경우도 있기 때문에 체크한다
              if(null == eElement) {
                     return null;
              }
              
              if(null == eElement.getElementsByTagName(item)) {
                     return null;
              }             
              
              if(null == eElement.getElementsByTagName(item).item(0)) {
                     return null;
              }             
              
              NodeList nlList =  eElement.getElementsByTagName(item).item(0).getChildNodes();
              Node nValue = (Node)nlList.item(0);
              if(nValue == null)
                     return null;
              
              return nValue.getNodeValue();
       }
       
       public static void ParsingXML(String result) {
              DocumentBuilderFactory dbFactory =  DocumentBuilderFactory.newInstance();
              DocumentBuilder dBuilder;
              try {
                     dBuilder = dbFactory.newDocumentBuilder();
                     Document doc = (Document) dBuilder.parse(result);
                     doc.getDocumentElement().normalize();
                     System.out.println("Root element :  "+doc.getDocumentElement().getNodeName());
                     
                    // item 태그로 묶여진 데이터들을 전부 가져온다
                     NodeList nList = doc.getElementsByTagName("item");
                     System.out.println("개수:"+nList.getLength());
                     for(int temp = 0; temp < nList.getLength(); ++temp) {
                           Node nNode = nList.item(temp);
                           if(nNode.getNodeType() == Node.ELEMENT_NODE){
                                  Element eElement = (Element) nNode;
                                  System.out.println(temp+"번째");
                                  System.out.println("건축년도:"+getValue("건축년도",eElement));
                                  System.out.println("계약면적:"+getValue("계약면적",eElement));
                                  System.out.println("년:"+getValue("년",eElement));
                                  System.out.println("법정동:"+getValue("법정동",eElement));
                                  System.out.println("보증금액:"+getValue("보증금액",eElement));
                                  System.out.println("월:"+getValue("월",eElement));
                                  System.out.println("월세금액:"+getValue("월세금액",eElement));
                                  System.out.println("일:"+getValue("일",eElement));
                                  System.out.println("지역코드:"+getValue("지역코드",eElement));
                           }
                     }
              } catch (Exception e) {
                     // TODO Auto-generated catch block
                     e.printStackTrace();
              }
              
              
       }
       
       public static void main(String[] args) {
              
              BufferedReader br = null;
              try {
                     String LAWD_CD = "11110";
                     String DEAL_YMD = "201512";
                     String myKey =  "vH4iE0jHiRxyh0nHKQbGEDAnidosddWarT8ipF8KWpJMrP5%2FGURFpDIzy7xdXsfXYK8KX4zhqvm1EzYK7X%2FSvg%3D%3D";
                     String urlstr =  "http://openapi.molit.go.kr:8081/OpenAPI_ToolInstallPackage/service/rest/RTMSOBJSvc/getRTMSDataSvcSHRent?LAWD_CD="+LAWD_CD+"&DEAL_YMD="+DEAL_YMD+
                                         "&serviceKey="+myKey;
                           
                     URL url = new URL(urlstr);
                     HttpURLConnection urlconnection = (HttpURLConnection)  url.openConnection();
                     urlconnection.setRequestMethod("GET");
                     br = new BufferedReader(new  InputStreamReader(urlconnection.getInputStream(), "UTF-8"));
                     String result = "";
                     String line;
                     while((line = br.readLine()) != null) {
                           result = result + line + "\n";
                     }
                     
                     //System.out.println(result);
                     ParsingXML(urlstr);  
                     
              }catch(Exception e) {
                     System.out.println(e.getMessage());
              }
       }
}
~~~