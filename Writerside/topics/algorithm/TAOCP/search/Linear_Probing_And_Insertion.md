# Linear_Probing_And_Insertion

﻿#Algorithm L
**Algorithm L** (**Linear probing and insertion**). This algorithm searches an M- 
node table, looking for a given key K. If K is not in the table and the table is 
not full, K is inserted. 
        The nodes of the table are denoted by TABLE[i], for 0 <= i < M, and they 
are of two distinguishable types, empty and occupied. An occupied node contains 
a key, called KEY[i], and possibly other fields. An auxiliary variable N is used 
to keep track of how many nodes are occupied; this variable is considered to be 
part of the table, and it is increased by 1 whenever a new key is inserted. 
        This algorithm makes use of a hash function h(K), and it uses the linear 
probing sequence (20) to address the table. Modifications of that sequence are 
discussed below. 
**L1**. [Hash.] Set i <-- h(K). (Now 0 <= i < M.) 
**L2**. [Compare.] If TABLE[i] is empty, go to step L4. Otherwise if KEY[i] = K, 
the algorithm terminates successfully. 
**L3**. [Advance to next.] Set i <-- i-1; if now i < 0, set i <-- i+M. Go back to 
step L2. 
**L4**. [Insert.] (The search was unsuccessful.) If N = M-1, the algorithm 
terminates with overflow. (This algorithm considers the table to be full 
when N = M - 1, not when N = M; see exercise 15.) Otherwise set 
N <-- N + 1, mark TABLE[i] occupied, and set KEY[i] <-- K. **|** 

---
#Linear open addressing
![这里写图片描述](https://img-blog.csdn.net/20151106160154321)


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
 * Linear Probing And Insertion:Searching
 */
public class Main {

    public static int[] TABLE = new int[19];
    public static int M = 19;
    public static int N = 0;

    public static void searchAndInsertNode(int key){
        int hash = key%19;                           /*Hash function:h(K)*/

        if(TABLE[hash] == 0){
            TABLE[hash] = key;
            N++;
            System.out.println(String.format("%4s",key+":")+" not found in the hash table, then insert it in TABLE["+hash+"]");
        }else {
            if(key == TABLE[hash]){
                System.out.println(key+" found in the hash table: TABLE["+hash+"]");
            }else {
                do{
                    hash--;
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
170: not found in the hash table, then insert it in TABLE[17]
897: not found in the hash table, then insert it in TABLE[3]
275: not found in the hash table, then insert it in TABLE[8]
653: not found in the hash table, then insert it in TABLE[7]
426: not found in the hash table, then insert it in TABLE[6]
154: not found in the hash table, then insert it in TABLE[2]
509: not found in the hash table, then insert it in TABLE[14]
612: not found in the hash table, then insert it in TABLE[1]
677: not found in the hash table, then insert it in TABLE[12]
765: not found in the hash table, then insert it in TABLE[5]
703: not found in the hash table, then insert it in TABLE[0]

Print the current Hash Table with 16 nodes:
 0:703
 1:612
 2:154
 3:897
 4:61
 5:765
 6:426
 7:653
 8:275
 9:503
11:87
12:677
14:509
15:908
17:170
18:512

Search Node 765 in current Hash Table:
765 found in the hash table: TABLE[5]

  1: not found in the hash table, then insert it in TABLE[16]
  2: not found in the hash table, then insert it in TABLE[13]
Error: Hash Table Overflow!, Key:3 can not be inserted!
Error: Hash Table Overflow!, Key:4 can not be inserted!
Error: Hash Table Overflow!, Key:5 can not be inserted!
```

---
#Reference
<< The art of computer programming: Sorting and Searching >> VOLUME 3, DONALD E. KNUTH
