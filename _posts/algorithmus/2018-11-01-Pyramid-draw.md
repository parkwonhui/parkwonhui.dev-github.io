---
layout: post
title: pyramid draw
categories: [algorithmus]
tags: [algorithmus]
---
### 문제

피라미드 그리기

### result

        *
       ***
      *****
     *******
    *********

### 문제풀이

공백은 한칸씩 늘어난다.  그래서1열에 길이가 1씩 증가. 

그리는 위치는 한칸씩 앞으로 간다.

> row value와 공백은 비례한다

> row value와 *위치는 반비례한다

> if(col >= count - row) * 위치를 이렇게 체크할 수 있다

### source

~~~
package kosta.basic;
package pack.com;
import java.util.Scanner;
import MyExample.src.pack.com;
public class Main {
     public static void main(String[] args) {
           // TODO Auto-generated method stub
           Scanner sc = new Scanner(System.in);
           int count = sc.nextInt();
           int starCount = 1;
           int colCount = count;
           for(int row = 0; row < count; ++row )
           {
                for(int col = 1; col <= colCount; ++col)
                {
                      if(col >= count - row)
                           System.out.print("*");
                      else
                           System.out.print(" ");                           
                }
                ++colCount;
                System.out.print("\n");
           }
     }
}
~~~
