# Distribution_counting__Sorting_by_counting

﻿#Distribution counting sort:分布计数排序

---

#Algorithm D
**Algorithm D** (**Distribution counting**). Assuming that all keys are integers in
the range $u<=K_j<=v$ for $1< j < N$, this algorithm sorts the records $R_1,..., R_N$
by making use of an auxiliary table $COUNT[u] ,..., COUNT[v]$. At the conclusion
of the algorithm the records are moved to an output area $S_1,..., S_N$ in the
desired order.
**D1**. [**Clear COUNTs**.] Set $COUNT[u]$ through $COUNT[v]$ all to zero.
**D2**. [**Loop on j**.] Perform step D3 for $1<=j<=N$; then go to step D4.
**D3**. [**Increase COUNT[$K_j$].**] Increase the value of $COUNT[K_j]$ by $1$.
**D4**. [**Accumulate.**] (At this point $COUNT[i]$ is the number of keys that are equal
to $i$.) Set $COUNT[i] \leftarrow COUNT[i]+COUNT[i-1]$ , for $i= u+1, u+2, ...,v$.
**D5**. [**Loop on j**.] (At this point $COUNT[i]$ is the number of keys that are less than
or equal to $i$; in particular, $COUNT[v] = N$.) Perform step D6 for $j= N,
N-1, ..., 1$; then terminate the algorithm.
**D6**. [**Output Rj**] Set $i \leftarrow COUNT[K_j],S_i \leftarrow R_j,$ and $COUNT[K_j] \leftarrow i-1$. **|**

---
#Flow diagram
![Distribution counting:Sorting by counting:Internal Sorting](https://img-blog.csdn.net/20151106142541285)

---
#Java program
In thisprogram, **R1,...,RN** were simplified to **K1,...,KN**.

```java
/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 11/19/13
 * Time: 10:01 PM
 * :)~
 * Distribution counting:Sorting by counting:Internal Sorting
 */
public class Main {

    public static void main(String[] args) {
        int N = 16;
        int[] S = new int[17];
        int[] keys = new int[17];
        int[] COUNT = new int[62];
        int u = 3;
        int v = 61;

        /*Prepare the data,3<=keys<=61*/
        keys[1] = 3;
        keys[2] = 57;
        keys[3] = 12;
        keys[4] = 61;
        keys[5] = 8;
        keys[6] = 17;
        keys[7] = 7;
        keys[8] = 25;
        keys[9] = 53;
        keys[10] = 42;
        keys[11] = 14;
        keys[12] = 9;
        keys[13] = 12;
        keys[14] = 46;
        keys[15] = 50;
        keys[16] = 27;

        /*Output unsorted keys*/
        System.out.println("Unsorted keys:");
        for(int i=1; i<=N; i++){
            System.out.println(i+":"+keys[i]);
        }
        System.out.println();

        /*Clear COUNTs*/
        for(int i=u; i<=v; i++){
            COUNT[i] = 0;
        }

        /*Kernel of the Algorithm*/
        for(int j=1; j<=N; j++){
            COUNT[keys[j]]++;
        }
        for(int i=u+1; i<=v; i++){
            COUNT[i] = COUNT[i] + COUNT[i-1];
        }
        for(int j=N; j>=1; j--){
            int i = COUNT[keys[j]];
            S[i] = keys[j];
            COUNT[keys[j]] = i-1;
        }

        /*Output sorted keys*/
        System.out.println("Sorted keys:");
        for(int i=1; i<=N; i++){
            System.out.println(i+":"+S[i]);
        }
    }
}
```

---
#Outputs
```
Unsorted keys:
1:3
2:57
3:12
4:61
5:8
6:17
7:7
8:25
9:53
10:42
11:14
12:9
13:12
14:46
15:50
16:27

Sorted keys:
1:3
2:7
3:8
4:9
5:12
6:12
7:14
8:17
9:25
10:27
11:42
12:46
13:50
14:53
15:57
16:61
```

---
#Reference
<< The art of computer programming: Sorting and Searching >> VOLUME 3, DONALD E. KNUTH
https://en.wikipedia.org/wiki/Counting_sort
