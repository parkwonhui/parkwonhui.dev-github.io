---
layout: post
title: Star Draw(별 그리기1)
categories: [algorithmus]
tags: [algorithmus]
---
### 문제
https://www.acmicpc.net/problem/2438

### 문제풀이

starCount는 행(row) 겸 *갯수를 의미한다

다음 행으로 갈때마다 *개수가 1씩 늘어나므로 row와 같다

### 소스

~~~
package algo;
import java.util.Scanner;
public class Main {
     public static void main(String[] args) {         
     Scanner sc = new Scanner(System.in);
     int count = sc.nextInt();
     
     for(int starCount = 1; starCount <= count; ++starCount)
     {
           for(int col = 1; col <= starCount;++col)
           {
                System.out.print("*");
           }
           System.out.print("\n");
     }
    }
}
~~~