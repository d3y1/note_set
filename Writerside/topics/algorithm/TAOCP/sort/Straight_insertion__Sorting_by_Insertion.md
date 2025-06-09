# Straight_insertion__Sorting_by_Insertion

﻿#Straight insertion sort:直接插入排序

---

##Animation
![这里写图片描述](https://img-blog.csdn.net/20151114111539011)
Graphical illustration of insertion sort

---

![这里写图片描述](https://img-blog.csdn.net/20151114111701588)
A graphical example of insertion sort.

---

![这里写图片描述](https://img-blog.csdn.net/20151114111739887)
Animation of the insertion sort sorting a 30 element array.

---

##Complexity

Class										|	Sorting algorithm
------											|	----
Data structure 							|	Array
Worst case performance 			|	$O(n^2)$ comparisons, swaps
Best case performance 			|	$\Omega(n)$ comparisons, $O(1)$ swaps
Average case performance 		|	$O(n^2)$ comparisons, swaps
Worst case space complexity	|	$O(n)$ total, $O(1)$ auxiliary


---

#Algorithm S
**Algorithm S** (**Straightinsertion sort**). Records $R_1,...,R_N$ are rearranged in
place; after sorting is complete, their keys will be in order,$K_1<=...<=K_N$.
**S1**. [Loop on $j$] Perform steps S2 through S5 for $j =2,3,...,N$; then terminate
the algorithm.
**S2**. [Set up $i, K, R$] Set $i \leftarrow j-1, K \leftarrow K_j, R \leftarrow R_j$. (In the following steps
we will attempt to insert $R$ into the correct position, by comparing $K$ with
$K_i$ for decreasing values of $i$.)
**S3**. [Compare $K : K_i$] If $K >= K_i$, goto step S5. (We have found the desired
position for record $R$.)
**S4**. [Move $R_i$, decrease $i$] Set $R_{i+1} \leftarrow R_i$, then $i \leftarrow i-1$. If $i > 0$, go back to
step S3. (If $i = 0$, $K$ is the smallest key found so far, so record $R$ belongs in
position $1$.)
**S5**. [$R$ into $R_{i+1}$] Set $R_{i+1} \leftarrow R$.**|**

---
#Flow diagram
![](https://img-blog.csdn.net/20151106142954570)


---
#Data table
![](https://img-blog.csdn.net/20151106143024400)

---
#Java program
In thisprogram, **R1,...,RN** were simplified to **K1,...,KN**.

```java
/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 11/20/13
 * Time: 10:01 PM
 * :)~
 * Straight insertion:Sorting by Insertion:Internal Sorting
 */
public class Main {

    public static void main(String[] args) {
        int N = 16;
        int[] K = new int[17];

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
        for(int j=2; j<=N; j++){
            int Key = K[j];
            int i=j-1;
            while (i > 0){
                if(Key >= K[i]){
                    K[i+1] = Key;
                    break;
                }else {
                    K[i+1] = K[i];
                    i--;
                }
            }
            if(i == 0){
                K[1] = Key;
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
https://en.wikipedia.org/wiki/Insertion_sort
