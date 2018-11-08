---
layout: post
title: Java Exception(예외처리)
categories: [java]
tags: [java,exception]
comments: true
---
## Java Exception(예외처리)

### try-catch문
- 컴파일 익셉션 :  컴파일 과정에서 에러
- 런타임 익셉션 :  실행프로그램 구동 중 에러
- try-catch문은 런타임 익셉션 발생
- 아래 예제는 Exception in thread "main" java.lang.ArithmeticException: / by  zero 익셉션 발생

~~~
public static void main(String[] args) {
    int a = 3, b = 0;
    int result;
    result = a / b;
    System.out.println(result);
    System.out.println("Done.");
} 
~~~

### try-cath문 사용 방법
- 익셉션이 발생할 것 같은 구문을 try catch 문으로 감싼다
- try는 소스코드를 실행했을 때 에러가 발생할 것 같은 부분을 넣는다
- catch는 에러가 났을 때 처리를 하는 부분이다(여러번 쓸 수 있다)
- finaly는 예외가 일어나든 안 일어나든 실행한다.(생략가능)
- 에러 출력 방법 e.printStackTrace(), e.getMessage()

~~~
public class C{
     public static void main(String[] args) {
           int a = 3, b = 0;
           int result;
           
           try{
                result = a / b;
                System.out.println(result);
           
           }catch(Exception e){
           
                System.out.println("잘못된 연산입니다");           
           }
           
           System.out.println("Done.");
     }    
}
~~~

### try-catch문 순서
- try문에서 예외가 발생하면 아래 소스코드는 실행하지 않는다.그러므로 2번을 제외하고 전부 출력된다
- 만약 10/1이라면 예외가 발생하지 않는다. 그래서 3번빼고 전부 출력된다

~~~
public static void main(String[] args) {
           int a = 3, b = 0;
           int result;
           try{
                System.out.println("1");
                int a = 10/0;
                System.out.println("2");
           }catch(Exception e){
                System.out.println("3");
           }finally{
                System.out.println("4");              
           }
           
           System.out.println("5");
}
~~~

### throws
- throws는 예외발생 처리를 함수 호출한 부분으로 넘긴다

~~~
returnvalue functionname() throws Exception
{
}
~~~

### throws 사용방법
- 예외를 넘길 함수의 인자 옆에 throws Exception 을 추가한다
- 아래 예제에선 main함수에서 add함수를 호출하는데 인자1과 인자2의 더한 값이 0보다 작다면
- throws 발생 시키고 있다.
- add함수가 throws를 발생시키고 있으므로 호출할 때 try-catch 블록안에 넣어야 한다. try문으로 감싸지 않으면 에러가 뜬다

~~~
public class Ex{
     static void add(int a, int b) throws Exception
     {
           int sum = a + b;
           if(sum < 0){
                throw new Exception("음수는 싫어");
           }
     }
     
     public static void main(String[] args) {
           
           try {
                add(10, -20);
           } catch (Exception e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
           }
	}
}
~~~

### throw
- 함수에 throws 키워드를 안쓰고 그냥 예외를 발생시킬 수 있다
- 아래 예제처럼 그냥 사용하면 에러난다
- throw를 사용하면 사용한 구문을 try-catch 문으로 감싸줘야 한다.

~~~
public static void main(String[] args) {
    throw new Exception();
}
~~~

### Exception extends
- Exception을 상속받아 예외 class를 만들어 try-catch문을 강제할 수 있다 
- 예외처리할 class를 만들고 Exception클래스를 상속 받는다
- 함수에 throws 예외를 발생시키는데 new Exception 대신 우리가 만든 클래스로 new ExceptionEx 한다
- 예외가 발생할 때 ExceptionEx 생성자가 호출된다

~~~
class ExceptionEx extends Exception
{
     public ExceptionEx()
     {
           System.out.println("errorFunc");
           
     }    
}

public class C{
     
     static void func() throws ExceptionEx
     {
           throw new ExceptionEx();
     }
     
     
     public static void main(String[] args) {
           
           try {
                func();
           } catch (Exception e) {
           }
}
~~~
