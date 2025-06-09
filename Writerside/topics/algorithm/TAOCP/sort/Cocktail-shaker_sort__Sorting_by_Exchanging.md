# Cocktail-shaker_sort__Sorting_by_Exchanging

﻿#Cocktail-shaker sort:鸡尾酒排序

---

##Animation
![cocktail shaker sort](https://img-blog.csdn.net/20151113120229688)

---

##Complexity

Class										|	Sorting algorithm
------											|	----
Data structure 							|	Array
Worst case performance 			|	$O(n^2)$
Best case performance 			|	$O(n)$
Average case performance 		|	$O(n^2)$
Worst case space complexity	|	$O(1)$


---

#Data table
![Cocktail-shaker sort:Sorting by Exchanging:Internal Sorting](https://img-blog.csdn.net/20151106144354479)

---
#Jave program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.

```java
/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 11/27/13
 * Time: 10:01 PM
 * :)~
 * Cocktail-shaker sort:Sorting by Exchanging:Internal Sorting
 */
public class Main {

    public static void main(String[] args) {
        int N = 16;
        int[] K = new int[17];
        int temp;

        /*Prepare the data*/
        K[1] = 503;
        K[2] = 87;
        K[3] = 512;
        K[4] = 61;
        K[5] = 908;
        K[6] = 170;
        K[7] = 897;
        K[8] = 275;
        K[9] = 653;
        K[10] = 426;
        K[11] = 154;
        K[12] = 509;
        K[13] = 612;
        K[14] = 677;
        K[15] = 765;
        K[16] = 703;

        /*Output unsorted Ks*/
        System.out.println("Unsorted Ks:");
        for(int i=1; i<=N; i++){
            System.out.println(i+":"+K[i]);
        }
        System.out.println();

        /*Kernel of the Algorithm!*/
        int LEFT = 1;
        int RIGHT = N;
        int DIRECTION = 1;
        while (LEFT < RIGHT){
            if(DIRECTION%2 == 1){
                for(int j=LEFT; j<=RIGHT-1; j++){
                    if(K[j] > K[j+1]){
                        temp = K[j];
                        K[j] = K[j+1];
                        K[j+1] = temp;
                    }
                }
                RIGHT--;
                DIRECTION++;
            }else {
                for(int j=RIGHT; j>=LEFT+1; j--){
                    if(K[j] < K[j-1]){
                        temp = K[j];
                        K[j] = K[j-1];
                        K[j-1] = temp;
                    }
                }
                LEFT++;
                DIRECTION++;
            }
        }

        /*Output sorted Ks*/
        System.out.println("Sorted Ks:");
        for(int i=1; i<=N; i++){
            System.out.println(i+":"+K[i]);
        }
    }
}
```

---
#Outputs
```
Unsorted Ks:
1:503
2:87
3:512
4:61
5:908
6:170
7:897
8:275
9:653
10:426
11:154
12:509
13:612
14:677
15:765
16:703

Sorted Ks:
1:61
2:87
3:154
4:170
5:275
6:426
7:503
8:509
9:512
10:612
11:653
12:677
13:703
14:765
15:897
16:908
```

---
#Reference
<< The art of computer programming: Sorting and Searching >> VOLUME 3, DONALD E. KNUTH
https://en.wikipedia.org/wiki/Cocktail_sort
