# Quick_Sequential_Search

﻿#Algorithm Q
**Algorithm Q** (**Quick sequential search**). This algorithm is the same as Algo- 
rithm S, except that it assumes the presence of a dummy record RN+1 at the 
end of the file. 
**Q1**. [Initialize.] Set i <-- 1, and set KN+1 <-- K. 
**Q2**. [Compare.] If K = Ki, go to Q4. 
**Q3**. [Advance.] Increase i by 1 and return to Q2. 
**Q4**. [End of file?] If i <= N, the algorithm terminates successfully; otherwise it 
terminates unsuccessfully (i = N + 1). **|** 

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
 * Quick Sequential Search:Searching
 */
public class Main {

    public static void main(String[] args) {
        int N = 16;
        int[] K = new int[18];

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
        int Key = 653;               /*Key to be found*/
        int i;
        K[N+1] = Key;

        for(i=1; i<=N+1; i++){
            if(Key == K[i]){
                break;
            }
        }
        if(i == N+1){
            System.out.println("Outputs: "+Key+" not found.");
        }else {
            System.out.println("Outputs: "+Key+" in K["+i+"].");
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

Outputs: 653 in K[9].
```

---
#Reference
<< The art of computer programming: Sorting and Searching >> VOLUME 3, DONALD E. KNUTH

