# Open_Addressing_With_Double_Hashing

﻿#Algorithm D
**Algorithm D** (**Open addressing with double hashing**). This algorithm is almost 
identical to Algorithm L, but it probes the table in a slightly different fashion by 
making use of two hash functions h1(K) and h2(K). As usual h1(K) produces a 
value between 0 and M-1, inclusive; but h2(K) must produce a value between 
1 and M-1 that is relatively prime to M. (For example, if M is prime, h2(K) 
can be any value between 1 and M-1 inclusive; or if M = 2^m, h2(K) can be 
any odd value between 1 and 2^m - 1.) 
**D1**. [First hash.] Set i <-- h1(K) 
**D2**. [First probe.] If TABLE[i] is empty, go to D6. Otherwise if KEY[i] = K, the 
algorithm terminates successfully. 
**D3**. [Second hash.] Set c <-- h2(K). 
**D4**. [Advance to next.] Set i <-- i-c; if now i < 0, set i <-- i+M. 
**D5**. [Compare.] If TABLE[i] is empty, go to D6. Otherwise if KEY[i] = K, the 
algorithm terminates successfully. Otherwise go back to D4. 
**D6**. [Insert.] If N = M-1, the algorithm terminates with overflow. Otherwise 
set N <-- N + 1, mark TABLE[i] occupied, and set KEY[i] <-- K. **|** 

---
#Java program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.

```java
package com.algorithms.searching;

/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/13/13
 * Time: 6:52 PM
 * :)~
 * Open Addressing With Double Hashing:Searching
 */
public class Main {

    public static int[] TABLE = new int[19];
    public static int M = 19;
    public static int N = 0;

    public static void searchAndInsertNode(int key){
        int hash = key%19;                           /*Hash function:h1(K)*/

        if(TABLE[hash] == 0){
            TABLE[hash] = key;
            N++;
            System.out.println(String.format("%4s",key+":")+" not found in the hash table, then insert it in TABLE["+hash+"]");
        }else {
            if(key == TABLE[hash]){
                System.out.println(key+" found in the hash table: TABLE["+hash+"]");
            }else {
                int c = 1+(key%18);                  /*Hash function:h2(K)*/
                do{
                    hash-=c;
                    if(hash < 0){
                        hash+=M;
                    }
                    if(TABLE[hash] == 0){
                        if(N == M-1){
                            System.out.println("Error: Hash Table Overflow!"+", Key:"+key+" can not be inserted!");
                            break;
                        }else {
                            TABLE[hash] = key;
                            N++;
                            System.out.println(String.format("%4s",key+":")+" not found in the hash table, then insert it in TABLE["+hash+"]");
                            break;
                        }
                    }
                }while (true);
            }
        }
    }

    public static void main(String[] args) {

        /*Prepare the Hash Table: suppose all the numbers are not zero!!!*/
        System.out.println("Prepare the Hash Table:");
        searchAndInsertNode(503);
        searchAndInsertNode(87);
        searchAndInsertNode(512);
        searchAndInsertNode(61);
        searchAndInsertNode(908);
        searchAndInsertNode(170);
        searchAndInsertNode(897);
        searchAndInsertNode(275);
        searchAndInsertNode(653);
        searchAndInsertNode(426);
        searchAndInsertNode(154);
        searchAndInsertNode(509);
        searchAndInsertNode(612);
        searchAndInsertNode(677);
        searchAndInsertNode(765);
        searchAndInsertNode(703);
        System.out.println();

        /*Print the current Hash Table with 16 nodes*/
        System.out.println("Print the current Hash Table with 16 nodes:");
        for(int j=0; j<19; j++){
            if(TABLE[j] != 0){
                System.out.println(String.format("%3s", j+":")+TABLE[j]);
            }
        }
        System.out.println();

        /*Search Node 765 in current Hash Table*/
        System.out.println("Search Node 765 in current Hash Table:");
        searchAndInsertNode(765);
        System.out.println();

        searchAndInsertNode(1);
        searchAndInsertNode(2);
        searchAndInsertNode(3);
        searchAndInsertNode(4);
        searchAndInsertNode(5);
    }
}
```

---
#Outputs
```
Prepare the Hash Table:
503: not found in the hash table, then insert it in TABLE[9]
 87: not found in the hash table, then insert it in TABLE[11]
512: not found in the hash table, then insert it in TABLE[18]
 61: not found in the hash table, then insert it in TABLE[4]
908: not found in the hash table, then insert it in TABLE[15]
170: not found in the hash table, then insert it in TABLE[0]
897: not found in the hash table, then insert it in TABLE[7]
275: not found in the hash table, then insert it in TABLE[3]
653: not found in the hash table, then insert it in TABLE[1]
426: not found in the hash table, then insert it in TABLE[8]
154: not found in the hash table, then insert it in TABLE[2]
509: not found in the hash table, then insert it in TABLE[16]
612: not found in the hash table, then insert it in TABLE[17]
677: not found in the hash table, then insert it in TABLE[12]
765: not found in the hash table, then insert it in TABLE[5]
703: not found in the hash table, then insert it in TABLE[13]

Print the current Hash Table with 16 nodes:
 0:170
 1:653
 2:154
 3:275
 4:61
 5:765
 7:897
 8:426
 9:503
11:87
12:677
13:703
15:908
16:509
17:612
18:512

Search Node 765 in current Hash Table:
765 found in the hash table: TABLE[5]

  1: not found in the hash table, then insert it in TABLE[14]
  2: not found in the hash table, then insert it in TABLE[6]
Error: Hash Table Overflow!, Key:3 can not be inserted!
Error: Hash Table Overflow!, Key:4 can not be inserted!
Error: Hash Table Overflow!, Key:5 can not be inserted!
```

---
#Reference
<< The art of computer programming: Sorting and Searching>> VOLUME 3, DONALD E. KNUTH
