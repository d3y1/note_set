# Merge_exchange_sort__Sorting_by_Exchanging

﻿#Merge exchange sort:归并交换排序

---

##Animation
![这里写图片描述](https://img-blog.csdn.net/20151114115249475)
An example of merge sort. First divide the list into the smallest unit (1 element), then compare each element with the adjacent list to sort and merge the two adjacent lists. Finally all the elements are sorted and merged.

---

![这里写图片描述](https://img-blog.csdn.net/20151114115324101)
Merge sort animation. The sorted elements are represented by dots.

---

![这里写图片描述](https://img-blog.csdn.net/20151114115555188)
A recursive merge sort algorithm used to sort an array of 7 integer values. These are the steps a human would take to emulate merge sort (top-down).

---

##Complexity

Class										|	Sorting algorithm
------											|	----
Data structure 							|	Array
Worst case performance 			|	$O(n log n)$
Best case performance 			|	$O(n log n)$ typical, $O(n)$ natural variant
Average case performance 		|	$O(n log n)$
Worst case space complexity	|	$О(n)$ total, $O(n)$ auxiliary


---

#Algorithm M
**Algorithm M** (**Merge exchange**). Records $R_1,..., R_N$ are rearranged in place; 
after sorting is complete their keys will be in order, $K_1<=...<=K_N$. We assume 
that $N >=2$. 
**M1**. [Initialize $p$.] Set $p \leftarrow 2^{(t-1)}$, where $t = \left \lceil \lg N \right \rceil$ is the least integer such that 
$2^t >= N$. (Steps M2 through M5 will be performed for $p = 2^{(t-1)}, 2^{(t-2)}, ..., 1$.) 
**M2**. [Initialize $q, r, d$.] Set $q \leftarrow 2^{(t-1)}, r \leftarrow 0, d \leftarrow p$. 
**M3**. [Loop on $i$.] For all $i$ such that $0 <= i < N-d$ and $i & p = r$, do step M4. 
Then go to step M5. (Here $i & p$ means the "bitwise and" of the binary 
representations of $i$ and $p$; each bit of the result is zero except where both 
$i$ and $p$ have $1$ bits in corresponding positions. Thus $13 & 21$ = $(1101)$ & 
$(10101)$ = $(00101)$ = $5$. At this point, $d$ is an odd multiple of $p$, and $p$ is 
a power of $2$, so that $i&p != (i+d)&p$ ; it follows that the actions of step M4 
can be done for all relevant $i$ in any order, even simultaneously.) 
**M4**. [Compare/exchange $R_{i+1} :R_{i+d+1}$.] If $K_{i+1} > K_{i+d+1}$, interchange the 
records $R_{i+1} \leftrightarrow R_{i+d+1}$ .
**M5**. [Loop on $q$.] If $q != p$, set $d \leftarrow q-p, q \leftarrow \frac q2, r \leftarrow p$, and return to M3. 
**M6**. [Loop on $p$.] (At this point the permutation $K_1 K_2 ... K_N$ is p-ordered.) 
Set $p \leftarrow \left \lfloor \frac p2 \right \rfloor$. If $p > 0$, go back to M2. **|** 

---
#Flow diagram
![Merge exchange sort:Sorting by Exchanging:Internal Sorting](https://img-blog.csdn.net/20151106144617076)

---
#Data table
![这里写图片描述](https://img-blog.csdn.net/20151106144643101) 
 

---
#Jave program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.

```java
/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 11/28/13
 * Time: 10:01 PM
 * :)~
 * Merge exchange sort:Sorting by Exchanging:Internal Sorting
 */
public class Main {

    public static void main(String[] args) {
        int N = 16;
        int[] K = new int[17];
        Double t = Math.ceil(Math.log(N)/Math.log(2));
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
        for(int p=(int)Math.pow(2, t-1); p>0; p=(int)Math.floor(p/2)){
            int q = (int)Math.pow(2, t-1);
            int r = 0;
            int d = p;

            for(int i=0; i<N-d; i++){
                if((i & p) == r){
                    if(K[i+1] > K[i+d+1]){
                        temp = K[i+1];
                        K[i+1] = K[i+d+1];
                        K[i+d+1] = temp;
                    }
                }
            }

            while (q > p){
                d = q - p;
                q /= 2;
                r = p;
                for(int i=0; i<N-d; i++){
                    if((i & p) == r){
                        if(K[i+1] > K[i+d+1]){
                            temp = K[i+1];
                            K[i+1] = K[i+d+1];
                            K[i+d+1] = temp;
                        }
                    }
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
https://en.wikipedia.org/wiki/Merge_sort
