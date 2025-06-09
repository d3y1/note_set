# Bubble_sort__Sorting_by_Exchanging

﻿#Bubble sort:冒泡排序

---
##Animation
![这里写图片描述](https://img-blog.csdn.net/20151113114854661)
Static visualization of bubble sort

---

![这里写图片描述](https://img-blog.csdn.net/20151113114956504)
An example of bubble sort. Starting from the beginning of the list, compare every adjacent pair, swap their position if they are not in the right order (the latter one is smaller than the former one). After each iteration, one less element (the last one) is needed to be compared until there are no more elements left to be compared.

---

![这里写图片描述](https://img-blog.csdn.net/20151113115106541)
A bubble sort, a sorting algorithm that continuously steps through a list, swapping items until they appear in the correct order. The list was plotted in a Cartesian coordinate system, with each point (x,y) indicating that the value y is stored at index x. Then the list would be sorted by bubble sort according to every pixel's value. Note that the largest end gets sorted first, with smaller elements taking longer to move to their correct positions.

---

##Complexity

Class										|	Sorting algorithm
------											|	----
Data structure 							|	Array
Worst case performance 			|	$O(n^2)$
Best case performance 			|	$O(n)$
Average case performance 		|	$O(n^2)$
Worst case space complexity	|	$O(1)$ auxiliary


---

#Algorithm B
**Algorithm B** (**Bubble sort**). Records $R_1,..., R_N$ are rearranged in place; after 
sorting is complete their keys will be in order, $K_1<=...<= K_N$. 
**B1**. [Initialize $BOUND$.] Set $BOUND \leftarrow N$. ($BOUND$ is the highest index for which 
the record is not known to be in its final position; thus we are indicating 
that nothing is known at this point.) 
**B2**. [Loop on $j$.] Set $t \leftarrow 0$. Perform step B3 for $j = 1, 2, ..., BOUND-1$, and 
then go to step B4. (If $BOUND=1$, this means go directly to B4.) 
**B3**. [Compare/exchange $R_j:R_{j+1}$.] If $K_j > K_{j+1}$, interchange $R_j \leftrightarrow R_{j+1}$ and 
set $t \leftarrow j$. 
**B4**. [Any exchanges?] If $t = 0$, terminate the algorithm. Otherwise set $BOUND \leftarrow t$ 
and return to step B2. **|** 

---
#Flow diagram
![Bubble sort:Sorting by Exchanging:Internal Sorting](https://img-blog.csdn.net/20151106143939376)
 

---
#Data table
![](https://img-blog.csdn.net/20151106144011677)

---
#Java program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.

```java
/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 11/26/13
 * Time: 10:01 PM
 * :)~
 * Bubble sort:Sorting by Exchanging:Internal Sorting
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
        for(int BOUND=N; BOUND>1; BOUND--){
            for(int j=1; j<= BOUND-1; j++){
                if(K[j] > K[j+1]){
                    temp = K[j];
                    K[j] = K[j+1];
                    K[j+1] = temp;
                }
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
https://en.wikipedia.org/wiki/Bubble_sort
