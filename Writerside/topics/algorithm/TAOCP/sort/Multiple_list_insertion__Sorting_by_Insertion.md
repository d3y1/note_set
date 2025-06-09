# Multiple_list_insertion__Sorting_by_Insertion

﻿#Data table
![Multiple list insertion:Sorting by Insertion:Internal Sorting](https://img-blog.csdn.net/20151106143802359)

---
#Java program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.

```java
/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 11/25/13
 * Time: 10:01 PM
 * :)~
 * Multiple list insertion:Sorting by Insertion:Internal Sorting
 */
public class Main {

    public static void main(String[] args) {
        int N = 16;
        int[] K = new int[17];
        int[] L1 = new int[17];
        int[] L2 = new int[17];
        int[] L3 = new int[17];
        int[] L4 = new int[17];
        L1[0] = 0;
        L2[0] = 0;
        L3[0] = 0;
        L4[0] = 0;

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
        for(int j=N; j>=1; j--){
            int Key = K[j];
            if(Key>=0 && Key<=249){
                int p1 = L1[0];
                int q1 = 0;
                while (p1 > 0){
                    if(Key <= K[p1]){
                        break;
                    }else {
                        q1 = p1;
                        p1 = L1[q1];
                    }
                }
                L1[q1] = j;
                L1[j] = p1;
            }else if(Key>=250 && Key<=499){
                int p2 = L2[0];
                int q2 = 0;
                while (p2 > 0){
                    if(Key <= K[p2]){
                        break;
                    }else {
                        q2 = p2;
                        p2 = L2[q2];
                    }
                }
                L2[q2] = j;
                L2[j] = p2;
            }else if(Key>=500 && Key<=749){
                int p3 = L3[0];
                int q3 = 0;
                while (p3 > 0){
                    if(Key <= K[p3]){
                        break;
                    }else {
                        q3 = p3;
                        p3 = L3[q3];
                    }
                }
                L3[q3] = j;
                L3[j] = p3;
            }else if(Key>=750 && Key<=999){
                int p4 = L4[0];
                int q4 = 0;
                while (p4 > 0){
                    if(Key <= K[p4]){
                        break;
                    }else {
                        q4 = p4;
                        p4 = L4[q4];
                    }
                }
                L4[q4] = j;
                L4[j] = p4;
            }
        }

        /*Output sorted Ks*/
        System.out.println("Sorted Ks:");
        int index1 = 0;
        int index2 = 0;
        int index3 = 0;
        int index4 = 0;
        int pos = 0;
        while (L1[index1] != 0){
            pos++;
            System.out.println(pos+":"+K[L1[index1]]);
            index1 = L1[index1];
        }
        while (L2[index2] != 0){
            pos++;
            System.out.println(pos+":"+K[L2[index2]]);
            index2 = L2[index2];
        }
        while (L3[index3] != 0){
            pos++;
            System.out.println(pos+":"+K[L3[index3]]);
            index3 = L3[index3];
        }
        while (L4[index4] != 0){
            pos++;
            System.out.println(pos+":"+K[L4[index4]]);
            index4 = L4[index4];
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
