---
layout: post
title: reference,abstract 정리
categories: [java]
tags: [java,reference,abstract]
comments: true
---
### 기본데이터(PrimitiveType)
- 변수에 데이터가 저장됨
- 부동소수점 타입(float, double)
- 정수 타입(char, long, int, short, byte)

### 레퍼런스 타입(ReferenceType)
- 변수가 객체를 가르킴
- 열거 타입(enum), 배열 타입(array), 인터페이스 타입(Interface), 클래스 타입(class)

### 참조값과 데이터
- 레퍼런스 변수를 또 다른 레퍼런스 변수에 대입할 때 일어나는 일
- obj2이 가르키는 주소를 obj1도 가르키게 했다
- obj1 = obj2;
- obj가 obj1에게 참조 주소를 준다(call by reference)

~~~
Object obj
Func(obj);
void Func(Object obj1){}
~~~

### null 참조값
- 아무것도 가지고 있지 않음, 초기화가 되지 않은 것과는 다르다

### 부모, 자식 간 형변환
- 자식 클래스를 부모 클래스로 형변환 하고 나선 오버라이딩 된 함수만 호출 가능하다

~~~
Account obj = new SpecielAccount("name", 2);
obj.addSpecielPoint() > 에러

Account obj = new SpecielAccount("name", 2);
SpecielAccount ob2 = obj; // 에러
SpecielAccount ob2 = (SpecielAccount)obj; // 성공
~~~

- 부모클래스는 자식클래스로 변환되지 않는다

~~~
Account obj = new Account("name", 2);
SpecielAccount = (SpecielAccount) obj; // 에러
~~~

### instanceof 연산자
- 캐스트 연산 가능성을 검사하는 연산자. 자바 키워드
- obj instanceof CheckingAccount
- obj가 CheckingAccount 형으로 형변환으로 변경할 수 있는지 체크
- 자식클래스 객체 of instanceof 자식클래스 => 성공
- 자식클래스 객체 of instanceof 부모클래스 => 성공
- 다만 if문으로 클래스 체크를 해서 다른 동작을 하도록 하는 것은 객체지향에 어긋남 

### 열거타입
- 상수체크 시 유용하게 사용

~~~
enum Season{
    SPRING, SUMMER, FALL, WINTER
}
~~~

### 클래스의 상속
- 인스턴스화를 금지하는 abstract 키워드
- 자식클래스에게 반드시 오버라이딩 하도록 강제시킨다
- 추상메소드를 가지고 있다
- abstract class Account

### 추상메소드
- 메소드의 본체가 없는 함수

~~~
abstract void sendMessage();
~~~

- 추상클래스는 인스턴스화 못시킨다. 오로지 상속으로만 사용 가능하다
- 추상클래스, 인터페이스 쓰는 이유 => 코드의 독립성

### 추상클래스 예시
Person class는 현재 Work class를 멤버로 가지고 있다<br>
그리고 role.doit() 함수 실행 시 'work 역활'이 출력된다.<br>
이 때 Driver라는 클래스도 추가해서 doit 함수 실행 시 'Driver 역활' 이라고 출력하고 싶다고 가정한다<br>
Work에서 Driver로 수정하려면 많은 수정이 필요하다(생성자, return 값을 전부 Work에서 Driver로 바꿔야 한다)<br>
하지만 Work와 Driver가 Role이라는 추상클래스를 상속하고 Person의 Work를 Role로 수정하면 코드 수정없이 Work에서 Driver로 수정할 수 있다 <br>
추상클래스로 만들어야 하는 이유는 doIt메소드를 만드기를 강제시키기 때문이다.<br>
(기본클래스는 doit함수를 만든다는 보장이 없다)<br>

수정전

~~~
public class Person {
     private String name;
     private Work role;
     
     public Person(){
           
     }
     public Person(String name, Work role) {
           super();
           this.name = name;
           this.role = role;
     }
     public Work getRole() {
           return role;
     }
     public void setRole(Work role) {
           this.role = role;
     }
}

public class Work{
     public void doIt() {
           System.out.println("work 역활");
}

~~~

수정후

- Work가 Role을 상속하고, Person이 Work 대신 Role가상클래스를 멤버변수로 가짐
- Role을 상속하는 Driver class를 추가해도 Person 소스코드 수정이 필요없다

~~~
public class Person{
     private String name;
     private Role role;
     
     public Person(){
           
     }
     public Person(String name, Role role) {
           super();
           this.name = name;
           this.role = role;
     }
     public Role getRole() {
           return role;
     }
     public void setRole(Role role) {
           this.role = role;
     }
}

public class Work extends Role{
     public void doIt() {
           System.out.println("work 역활");
}
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
                            