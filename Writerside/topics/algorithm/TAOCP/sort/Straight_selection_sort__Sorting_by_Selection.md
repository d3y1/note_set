# Straight_selection_sort__Sorting_by_Selection

﻿#Straight selection sort:直接选择排序

---

##Animation
![straight selection sort](https://img-blog.csdn.net/20151113124611426)
Selection sort animation

---

![这里写图片描述](https://img-blog.csdn.net/20151113124700426)
Selection sort animation. Red is current min. Yellow is sorted list. Blue is current item.

---

##Complexity

Class										|	Sorting algorithm
------											|	----
Data structure 							|	Array
Worst case performance 			|	$О(n^2)$
Best case performance 			|	$О(n^2)$
Average case performance 		|	$О(n^2)$
Worst case space complexity	|	$О(n)$ total, $O(1)$ auxiliary


---

#Algorithm S
**Algorithm S** (**Straight selection sort**). Records $R_1,..., R_N$ are rearranged in 
place; after sorting is complete, their keys will be in order, $K_1<=...<=K_N$. 
Sorting is based on the method indicated above, except that it proves to be 
more convenient to select the largest element first, then the second largest, etc. 
**S1**. [Loop on $j$.] Perform steps S2 and S3 for $j = N, N-1,..., 2$. 
**S2**. [Find $max(K_1,..., K_j)$.] Search through keys $K_j, K_{j-1},..., K_1$ to find a 
maximal one; let it be $K_i$, where $i$ is as large as possible. 
**S3**. [Exchange with $R_j$.] Interchange records $R_i \leftrightarrow R_j$. (Now records $R_j,..., R_N$ 
are in their final position.) **|** 

---
#Flow diagram
![](https://img-blog.csdn.net/20151106144854885)

---
#Data table
![](https://img-blog.csdn.net/20151106145001126)

---
#Jave program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.

```java
/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/1/13
 * Time: 10:01 PM
 * :)~
 * Straight selection sort:Sorting by Selection:Internal Sorting
 */
public class Main {

    public static void main(String[] args) {
        int N = 16;
        int[] K = new int[17];
        int temp;
        int maxIndex;

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
        for(int j=N; j>=2; j--){
            maxIndex = j;
            for(int i=1; i<=j; i++){
                if(K[i] > K[maxIndex]){
                    maxIndex = i;
                }
            }
            temp = K[j];
            K[j] = K[maxIndex];
            K[maxIndex] = temp;
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
https://en.wikipedia.org/wiki/Selection_sort
