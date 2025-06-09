# Comparison_counting__Sorting_by_counting

﻿#Comparison counting sort:比较计数排序

---

#Algorithm C
**Algorithm C** (**Comparison counting**). This algorithm sorts $R_1 ,..., R_N$ on the
keys $K_1,...,K_N$ by maintaining an auxiliary table $COUNT[1],..., COUNT[N]$ to
count the number of keys less than a given key. After the conclusion of the
algorithm, $COUNT[j] + 1$ will specify the final position of record $R_j$.
**C1**. [Clear COUNTs.] Set $COUNT[1]$ through $COUNT[N]$ to zero.
**C2**. [Loop on i.] Perform step C3, for $i = N, N-1, ..., 2$;then terminate the
algorithm.
**C3**. [Loop on j.] Perform step C4, for $j = i-1, i-2, ...,1$.
**C4**. [Compare $K_i$:$K_j$.] If $K_i< K_j$, increase $COUNT[j]$ by 1; otherwise increase
$COUNT[i]$ by $1$. **|**

---
#Flow diagram
![](https://img-blog.csdn.net/20151106142109554)

---
#Data table
![](https://img-blog.csdn.net/20151106142206389)

---
#Java program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.

```java
/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 11/18/13
 * Time: 10:01 PM
 * :)~
 * Comparison counting:Sorting by counting:Internal Sorting
 */
public class Main {

    /*Sorting by counting:Comparison counting*/
    public static void main(String[] args) {
        int N = 16;
        int[] keys = new int[17];
        int[] COUNT = new int[17];

        /*Prepare the input data*/
        keys[1] = 503;
        keys[2] = 87;
        keys[3] = 512;
        keys[4] = 61;
        keys[5] = 908;
        keys[6] = 170;
        keys[7] = 897;
        keys[8] = 275;
        keys[9] = 653;
        keys[10] = 426;
        keys[11] = 154;
        keys[12] = 509;
        keys[13] = 612;
        keys[14] = 677;
        keys[15] = 765;
        keys[16] = 703;

        /*Output unsorted keys*/
        System.out.println("Unsorted keys:");
        for(int i=1; i<=N; i++){
            System.out.println(i+":"+keys[i]);
        }
        System.out.println();

        /*Clear COUNTs*/
        for(int i=1; i<=N; i++){
            COUNT[i] = 0;
        }

        /*Kernel of the Algorithm*/
        for(int i=N; i>1; i--){
            for(int j=i-1; j>=1; j--){
                if(keys[i] < keys[j]){
                    COUNT[j]++;
                }else{
                    COUNT[i]++;
                }
            }
        }

        /*Output final COUNTs*/
        System.out.println("COUNT values:");
        for(int i=1; i<=N; i++){
            System.out.println("COUNT["+i+"]="+COUNT[i]);
        }
        System.out.println();

        /*Output sorted keys*/
        System.out.println("Sorted keys:");
        for(int i=0; i<=N-1; i++){
            for(int j=1; j<=N; j++){
                if(COUNT[j] == i){
                    System.out.println((COUNT[j]+1)+":"+keys[j]);
                }
            }
        }
    }
}
```

---
#Outputs
```
Unsortedkeys:
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

COUNTvalues:
COUNT[1]=6
COUNT[2]=1
COUNT[3]=8
COUNT[4]=0
COUNT[5]=15
COUNT[6]=3
COUNT[7]=14
COUNT[8]=4
COUNT[9]=10
COUNT[10]=5
COUNT[11]=2
COUNT[12]=7
COUNT[13]=9
COUNT[14]=11
COUNT[15]=13
COUNT[16]=12

Sortedkeys:
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
https://zh.wikipedia.org/wiki/%E8%AE%A1%E6%95%B0%E6%8E%92%E5%BA%8F
https://en.wikipedia.org/wiki/Counting_sort
