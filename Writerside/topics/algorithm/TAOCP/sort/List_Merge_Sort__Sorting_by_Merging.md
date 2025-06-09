# List_Merge_Sort__Sorting_by_Merging

﻿#Algorithm L
**Algorithm L** (**List merge sort**). Records R1, ... , RN are assumed to contain 
keys K1,..., KN, together with link fields L1, ..., LN capable of holding the 
numbers -(N + 1) through (N + 1). There are two auxiliary link fields L0 and 
LN+1 in artificial records R0 and RN+1 at the beginning and end of the file. This 
algorithm is a "list sort" that sets the link fields so that the records are linked 
together in ascending order. After sorting is complete, L0 will be the index of 
the record with the smallest key; and Lk, for 1 <= k <= N, will be the index of the 
record that follows Rk, or Lk = 0 if Rk is the record with the largest key. (See 
Eq. 5.2.1-(13).) 
During the course of this algorithm, R0 and RN+1 serve as list heads for two 
linear lists whose sublists are being merged. A negative link denotes the end of 
a sublist known to be ordered; a zero link denotes the end of the entire list. We 
assume that N >=2. 
The notation "|LS| <-- p" means "Set Ls to p or -p, retaining the previous 
sign of Ls." This operation is well-suited to MIX, but unfortunately not to most 
computers; it is possible to modify the algorithm in straightforward ways to 
obtain an equally efficient method for most other machines. 
**L1**. [Prepare two lists.] Set L0 <-- 1, LN+1 <-- 2, Li <-- -(i + 2) for 1 <= i <= N-2, 
and LN-1 <-- LN <-- 0. (We have created two lists containing R1, R3, R5, ... 
and R2, R4, R6, ... respectively; the negative links indicate that each or- 
dered sublist consists of one element only. For another way to do this step, 
taking advantage of ordering that may be present in the initial data, see 
exercise 12.) 
**L2**. [Begin new pass.] Set s <-- 0, t <-- N + 1, p <-- Ls, q <-- Lt. If q = 0, the 
algorithm terminates. (During each pass, p and q traverse the lists being 
merged; s usually points to the most recently processed record of the current 
sublist, while t points to the end of the previously output sublist.) 
**L3**. [Compare Kp : Kq] If Kp > Kq, go to L6. 
**L4**. [Advance p.] Set |LS| <-- p, s <-- p, p <-- Lp. If p > 0, return to L3. 
**L5**. [Complete the sublist.] Set Ls <-- q, s <-- t. Then set t <-- q and q <-- Lq, one 
or more times, until q <= 0. Finally go to L8. 
**L6**. [Advance q] (Steps L6 and L7 are dual to L4 and L5.) Set |LS| <-- q, s <-- q, 
q <-- Lq. If q > 0, return to L3. 
**L7**. [Complete the sublist.] Set Ls <-- p, s <-- t. Then set t <-- p and p <-- Lp, one 
or more times, until p <= 0. 
**L8**. [End of pass?] (At this point, p <= 0 and q <= 0, since both pointers have 
moved to the end of their respective sublists.) Set p <-- -p, q <-- -q. If 
q = 0, set |LS| <-- p, |Lt| <-- 0 and return to L2. Otherwise return to L3. **|** 

---
#Data table
![这里写图片描述](https://img-blog.csdn.net/20151106154411576)

---
#Java program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.

```java
/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/4/13
 * Time: 10:01 PM
 * :)~
 * List Merge Sort:Sorting by Merging:Internal Sorting
 */
public class Main {

    public static void main(String[] args) {
        int N = 16;
        int[] K = new int[17];
        int[] L = new int[18];

        /*Prepare the input data*/
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
        int s;
        int t;
        int p;
        int q;

        L[0] = 1;                               /*L1*/
        L[N+1] = 2;
        for(int i=1; i<=N-2; i++){
            L[i] = -(i+2);
        }
        L[N-1] = L[N] = 0;

        do{
            s = 0;                             /*L2*/
            t = N+1;
            p = L[s];
            q = L[t];

            if(q == 0){
                break;
            }
            do{
                if(K[p] > K[q]){                 /*L3*/
                    if(L[s] >= 0){               /*L6*/
                        L[s] = Math.abs(q);
                    }else {
                        L[s] = -Math.abs(q);
                    }
                    s = q;
                    q = L[q];

                    if(q > 0){
                        continue;
                    }
                    L[s] = p;                    /*L7*/
                    s = t;
                    do{
                        t = p;
                        p = L[p];
                    }while (p > 0);
                } else {
                    if(L[s] >= 0){              /*L4*/
                        L[s] = Math.abs(p);
                    }else {
                        L[s] = -Math.abs(p);
                    }
                    s = p;
                    p = L[p];
                    if(p > 0){
                        continue;
                    }
                    L[s] = q;                   /*L5*/
                    s = t;
                    do{
                        t = q;
                        q = L[q];
                    }while (q > 0);
                }

                p = -p;                          /*L8*/
                q = -q;
                if(q == 0){
                    if(L[s] >= 0){
                        L[s] = Math.abs(p);
                    }else {
                        L[s] = -Math.abs(p);
                    }
                    L[t] = 0;
                    break;
                }
            }while (true);
        }while (true);

        /*Output sorted Ks*/
        System.out.println("Sorted Ks:");
        int index = 0;
        int i = 1;
        while (L[index] > 0){
            System.out.println(i+":"+K[L[index]]);
            index = L[index];
            i++;
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
