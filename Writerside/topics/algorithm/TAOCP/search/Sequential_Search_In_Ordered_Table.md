# Sequential_Search_In_Ordered_Table

﻿#Algorithm T
**Algorithm T** (**Sequential search in ordered table**). Given a table of records 
R1, R2,..., RN whose keys are in increasing order K1 < K2 < ... < KN, 
this algorithm searches for a given argument K. For convenience and speed, 
the algorithm assumes that there is a dummy record RN+1 whose key value is 
KN+1 = Positive Infinite > K. 
**T1**. [Initialize.] Set i <-- 1. 
**T2**. [Compare.] If K <= Ki, go to T4. 
**T3**. [Advance.] Increase i by 1 and return to T2. 
**T4**. [Equality?] If K = Ki, the algorithm terminates successfully. Otherwise it 
terminates unsuccessfully. **|** 

---
#Java program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.

```java
/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/10/13
 * Time: 6:52 PM
 * :)~
 * Sequential Search In Ordered Table:Searching
 */
public class Main {

    public static void main(String[] args) {
        int N = 16;
        int[] K = new int[18];

        /*Prepare the ordered data table*/
        K[1] = 61;
        K[2] = 87;
        K[3] = 154;
        K[4] = 170;
        K[5] = 275;
        K[6] = 426;
        K[7] = 503;
        K[8] = 509;
        K[9] = 512;
        K[10] = 612;
        K[11] = 653;
        K[12] = 677;
        K[13] = 703;
        K[14] = 765;
        K[15] = 897;
        K[16] = 908;

        /*Output sorted Ks*/
        System.out.println("Sorted Ks:");
        for(int i=1; i<=N; i++){
            System.out.println(i+":"+K[i]);
        }
        System.out.println();

        /*Kernel of the Algorithm!*/
        int Key = 653;               /*Key to be found*/
        int i;
        K[N+1] = 10000;              /*Positive infinite*/

        for(i=1; i<=N+1; i++){
            if(Key <= K[i]){
                break;
            }
        }
        if(Key == K[i]){
            System.out.println("Outputs: "+Key+" in K["+i+"].");
        }else {
            System.out.println("Outputs: "+Key+" not found.");
        }
    }
}
```

---
#Outputs
```
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

Outputs: 653 in K[11].
```

---
#Reference
<< The art of computer programming: Sorting and Searching >> VOLUME 3, DONALD E. KNUTH
