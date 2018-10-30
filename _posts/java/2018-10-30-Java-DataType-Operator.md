---
layout: post
title: 자바 데이터 타입, 데이터 연산
categories: [java]
tags: [java]
---
### Java의 플랫폼 독립성
- '플랫폼 독립성'은 특정 플랫폼에 의존적이지 않다는 것을 의미
- Java는 컴파일하면 .class 파일을 생성하고 JVM 위에서 실행된다. 그래서 운영체제가 달라도 실행가능하다
- 하지만 C++은 컴파일하면 어셈블리어->기계어->실행파일이 나오는데 해당 플랫폼의 어셈블리어에 맞게 변환되어 
다른 플랫폼에선 실행이 안된다
- 예를 들어 windows 실행파일은 linux에서 사용안되고 그 반대도 마찬가지 이다
- Java의 단점은 JVM 위에 있어서 느리다. 그래서 플랫폼과 상관없는 웹에서 사용된다

### 데이터 기본 리터럴
- 10 => int
- 3.14 => double 
- ' ' => char
- " " => String ( 기본적인 자료형이 아니다. char로 문자열 사용하기 불편해서 사용 )
- float value = 3.14; 하면 에러가 나서 3.14f처럼 형변환을 해야한다.
- 그런데 short, long 변수에 정수값을 줄 땐 형변환 에러 안나는데 왜 float만 난다.
- 아마 소수점끼리 형변환하면 소실되는 값이 있으니까 에러 내는 듯 하다.
- double에 정수 대입은 에러 안남

~~~
double d = 3.14+1;

System.out.println(d);
if(a == 4.14)
{
	System.out.println("같다");
}
else
{
	System.out.println("다르다");			
}
~~~
- 결과는 다르다 출력.
- d를 출력하면 4.140000000000001 이 나온다
		
### 데이터타입에 따른 출력 결과
데이터타입에 따라 결과가 달라질 수 있다
~~~
char c = 'A'
System.out.println(c); 결과 A
System.out.println((int)c); 결과 65
~~~
소수점 둘째자리까지 실수를 표현하고 싶다면?
~~~
System.out.printf("평균:%.2f", avg);
~~~

### casting(형변환)
- byte < short < int < long < float < double < String
- 큰자료형 = 큰 자료형+작은 자료형(묵시적 형변환)
- 큰자료형과 작은자료형을 더하면 큰 자료형이 된다.
- 아래처럼 연산결과를 작은자료형으로 받으면 에러난다.

~~~
int n1 = 10;
double n2 = 3.14;
int re = n1+n2;
		
short b1 = 10000;
byte a = 1 + b1;
~~~

### casting String <=> 정수형, 실수형
- 모든 정수는 String과 연산하면 String이 된다

~~~
String n3 = 10 + 5 + "0";
System.out.println(n3);
~~~
결과 150

### final 변수
- 변수에 값을 딱 한번만 대입할 수 있다(값변경x)

### 증감 연산자 우선순위
~~~
int n7 = 10;
int n8 = 2;
int n9 = n7-- - n8;		// 10 - 2 한다음 n7은 1뺀다
System.out.println(n9);
~~~		
- 연산자 우선순위대로 연산한다.
-  --가 모든 연산이 끝난 후 실행하는 후위연산자이기 때문에 10 - 2 를 해서 n9는 8이 되고 n7은 9가 된다

### String 비교
- String 값이 같은지 비교할 땐 == 연산자가 아닌 String.equals 함수 사용
- == 연산자는 주소값이 같은지 비교

~~~
String str1 = "abc";
String str2 = "abc";
~~~
- str1 == str2는 true이다. 처음 abc 글자를 str1에 대입하면 "abc" 단어가 없으므로 등록된다.
- str2값에 "abc"를 넣으면 메모리에 "abc" 글자가 있는지 찾아보고 있으므로 같은 메모리 주소를 전달한다.



