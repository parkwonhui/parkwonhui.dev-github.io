---
layout: post
title: 정수값의 짝수,홀수 갯수 구하기
categories: [algorithmus]
tags: [algorithmus]
---

### 문제
정수값에 대해서 전체 자리수 중 짝수, 홀수갯수를 구하자.
(5자리로 한정)삼항연산자

문제풀이
~~~
package kosta.mission;

public class Mission03 {

	public static void main(String[] args) {
		int num = 26129;
		final int max_size = String.valueOf(num).length();
		int[] arr = new int[max_size];
		int i = 1;
		for(int m = 0; m < max_size - 1; ++m)
		{
			i = i * 10;
		}
		
		for(int j = 0; j < max_size; i/=10, ++j)
		{
			
			arr[j] = num / i;		// 나누기 몫을 구함
			num -= (i * arr[j]);	// 나누기 몫 * 현재 자리수 = 현재 자리수의 값만 빼준다
		}
		
		int even = 0;
		int odd = 0;			// 홀수
		for(int k = 0; k < max_size; ++k)
		{
			
			int temp = (0 == (arr[k] % 2)) ? ++even : ++odd;
		}
		
		
		System.out.println("짝수의 개수:"+even);
		System.out.println("홀수의 개수:"+odd);	
	}

}
~~~

문제풀이2
~~~
int num = 12345;
int even = 0;
int odd = 0;
even += (num/10000%2 == 0) ? 1 : 0;
even += (num/1000%10%2 == 0) ? 1: 0;
even += (num/100%10%2 == 0) ? 1: 0;
even += (num/10%10%2 == 0) ? 1: 0;
even += (num%2 == 0) ? 1: 0;
		
odd = 5 - even;

System.out.println("짝수의 개수:"+even);
System.out.println("홀수의 개수:"+odd);	
~~~