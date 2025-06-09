# Radix_sort__Sorting_by_Exchanging

﻿#Java program

```java
/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 11/30/13
 * Time: 10:01 PM
 * :)~
 * Radix sort:Sorting by Exchanging:Internal Sorting
 */
public class Main {

    public static void main(String[] args) {
        int N = 16;
        int[] K = new int[17];
        int[][] D = new int[4][17];
        int digit_len = 3;
        int temp;
        int tempDigit;

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
        for(int i=1; i<=digit_len; i++){
            for(int j=1; j<=N; j++){
                switch (i){
                    case 1: D[1][j] = K[j]%10; break;
                    case 2: D[2][j] = (K[j]/10)%10; break;
                    case 3: D[3][j] = K[j]/100; break;
                }
            }
            /*Stable bubble sort*/
            for(int BOUND=N; BOUND>1; BOUND--){
                for(int m=1; m<=BOUND-1; m++){
                    if(D[i][m] > D[i][m+1]){
                        tempDigit = D[i][m];
                        D[i][m] = D[i][m+1];
                        D[i][m+1] = tempDigit;

                        temp = K[m];
                        K[m] = K[m+1];
                        K[m+1] = temp;
                    }
                }
            }

            System.out.println("The "+i+" digit sorted Ks:");
            for(int n=1; n<=N; n++){
                System.out.println(n+":"+K[n]);
            }
            System.out.println();
        }

        /*Output sorted Ks*/
        System.out.println("Final sorted Ks:");
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

The 1 digit sorted Ks:
1:170
2:61
3:512
4:612
5:503
6:653
7:703
8:154
9:275
10:765
11:426
12:87
13:897
14:677
15:908
16:509

The 2 digit sorted Ks:
1:503
2:703
3:908
4:509
5:512
6:612
7:426
8:653
9:154
10:61
11:765
12:170
13:275
14:677
15:87
16:897

The 3 digit sorted Ks:
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

Final sorted Ks:
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
