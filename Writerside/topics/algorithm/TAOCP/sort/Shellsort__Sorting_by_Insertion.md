# Shellsort__Sorting_by_Insertion

﻿#Shellsort:希尔排序

---

##Animation
![shellsort](https://img-blog.csdn.net/20151114112748347)
Shellsort with gaps 23, 10, 4, 1 in action.

---

![这里写图片描述](https://img-blog.csdn.net/20151114112828231)
The step-by-step process of replacing pairs of items during the shell sorting algorithm.

---

##Complexity

Class										|	Sorting algorithm
------											|	----
Data structure 							|	Array
Worst case performance 			|	$O(n^2)$
Best case performance 			|	$O(n log^2 n)$
Average case performance 		|	depends on gap sequence
Worst case space complexity	|	$О(n)$ total, $O(1)$ auxiliary


---

#Algorithm D
**Algorithm D** (**Shellsort**).Records $R_1, ..., R_N$ are rearranged in place; after 
sorting is complete, their keys will be in order, $K_1<=...<=K_N$.Anauxiliary 
sequence of increments $h_{t-1}, h_{t-2}, ... ,h_0$ is used to control the sorting process, 
where $h_0 = 1$;proper choice of these increments can significantly decrease the 
sorting time. This algorithm reduces to Algorithm S when $t = 1$. 
**D1**. [Loop on $s$.] Performstep D2 for $s=t-1, t-2, ..., 0$; then terminate the 
algorithm. 
**D2**. [Loop on $j$.] Set $h \leftarrow h_s$, and perform steps D3 through D6 for $h$
(We will use a straight insertion method to sort elements that are $h$ positions 
apart, so that $K_i<=K_{i+h}$ for $1<=i<=N-h$. Steps D3 through D6 are 
essentially the same as steps S2 through S5, respectively, in Algorithm S.) 
**D3**. [Set up $i, K, R$.]Set $i \leftarrow j-h, K \leftarrow K_j, R \leftarrow R_j$. 
**D4**. [Compare $K :K_i$.] If $K>=K_i$, go to step D6. 
**D5**. [Move $R_i$, decrease $i$.] Set $R_{i+h} \leftarrow R_i$, then $i \leftarrow i-h$. If $i > 0$, go back to 
step D4. 
**D6**. [$R$ into $R_{i+h}$.] Set $R_{i+h} \leftarrow R$. **|** 

---
#Data table
![Shellsort:Sorting by Insertion:Internal Sorting](https://img-blog.csdn.net/20151106143426436)

---
#Java program
In this program, **R1,...,RN** weresimplified to **K1,...,KN**.

```java
/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 11/23/13
 * Time: 10:01 PM
 * :)~
 * Shellsort:Sorting by Insertion:Internal Sorting
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
        for(int h=N/2; h>=1; h/=2){
            for(int j=h+1; j<=N; j+=h){
                int Key = K[j];
                int i = j-h;
                while (i > 0){
                    if(Key >= K[i]){
                        K[i+h] = Key;
                        break;
                    }else {
                        K[i+h] = K[i];
                        i-=h;
                    }
                }
                if(i <= 0){
                    K[i+h] = Key;
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
UnsortedKs:
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

SortedKs:
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
https://en.wikipedia.org/wiki/Shellsort
