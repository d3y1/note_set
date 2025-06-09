# Chained_Hash_Table_Search_And_Insertion-1

﻿#Algorithm C
**Algorithm C** (**Chained hash table search and insertion**). This algorithm looks 
for a given key K in an M-node table. If K is not in the table and the table is 
not full, K is inserted. 
        The nodes of the table are denoted by TABLE[i], for 0 <= i <= M, and they 
are of two distinguishable types, empty and occupied. An occupied node contains 
a key field KEY[i], a link field LINK[i], and possibly other fields. 
        The algorithm makes use of a hash function h(K). An auxiliary variable 
R is also used, to help find empty spaces; when the table is empty, we have 
R = M + 1, and as insertions are made it will always be true that TABLE [j] is 
occupied for all j in the range R <= j <= M. By convention, TABLE[0] will always 
be empty. 
**C1**. [Hash.] Set i <-- h(K) + 1. (Now 1 <= i <= M.) 
**C2**. [Is there a list?] If TABLE[i] is empty, go to C6. (Otherwise TABLE[i] is 
occupied; we will look at the list of occupied nodes that starts here.) 
**C3**. [Compare.] If K = KEY[i], the algorithm terminates successfully. 
**C4**. [Advance to next.] If LINK[i] != 0, set i <-- LINK[i] and go back to step C3. 
**C5**. [Find empty node.] (The search was unsuccessful, and we want to find an 
empty position in the table.) Decrease R one or more times until finding 
a value such that TABLE[R] is empty. If R = 0, the algorithm terminates 
with overflow (there are no empty nodes left); otherwise set LINK[i] <-- R, 
i <-- R. 
**C6**. [Insert new key.] Mark TABLE[i] as an occupied node, with KEY[i] <-- K 
and LINK[i] <-- 0. **|** 

---
#Flow diagram
 ![flow_diagram_chained_hash_table.png](flow_diagram_chained_hash_table.png)

---
#Coalesced chaining
![coalesced_chaining.png](coalesced_chaining.png)

---
#Java program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.


**Node.java**
```java
package com.algorithms.searching;

/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/13/13
 * Time: 6:52 PM
 * :)~
 * Chained Hash Table Search And Insertion:Searching
 */
public class Node {
    int KEY;
    int LINK;
    Node(int key){
        KEY = key;
        LINK=0;
    }
}
```

**Main.java**
```java
package com.algorithms.searching;

/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/13/13
 * Time: 6:52 PM
 * :)~
 * Chained Hash Table Search And Insertion:Searching
 */
public class Main {

    public static Node[] TABLE = new Node[20];
    public static int M = 19;
    public static int R = M+1;

    public static void searchAndInsertNode(int key){
        int hash = key%19+1;                  /*Hash function:h(K)*/

        if(TABLE[hash] == null){
            Node node = new Node(key);
            TABLE[hash] = node;
            System.out.println(String.format("%4s",key+":")+" not found in the hash table, then insert it in TABLE["+hash+"]");
        }else {
            do{
                if(key == TABLE[hash].KEY){
                    System.out.println(key+" found in the hash table: TABLE["+hash+"]");
                    break;
                }
                if(TABLE[hash].LINK != 0){
                    hash = TABLE[hash].LINK;
                }else {
                    do{
                        if(R == 0){
                            System.out.println("Error: Hash Table Overflow!"+", Key:"+key+" can not be inserted!");
                            break;
                        }else {
                            R--;
                            if(R!=0 && TABLE[R]==null){
                                TABLE[hash].LINK = R;
                                hash = R;
                                break;
                            }
                        }
                    }while (true);
                    if(R == 0){
                        break;
                    }
                    Node node = new Node(key);
                    TABLE[hash] = node;
                    System.out.println(String.format("%4s",key+":")+" not found in the hash table, then insert it in TABLE["+hash+"]");
                    break;
                }
            }while (true);
        }
    }

    public static void main(String[] args) {

        /*Prepare the Hash Table*/
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
        for(int j=1; j<=19; j++){
            if(TABLE[j] != null){
                System.out.println(String.format("%3s", j+":")+TABLE[j].KEY);
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
503: not found in the hash table, then insert it in TABLE[10]
 87: not found in the hash table, then insert it in TABLE[12]
512: not found in the hash table, then insert it in TABLE[19]
 61: not found in the hash table, then insert it in TABLE[5]
908: not found in the hash table, then insert it in TABLE[16]
170: not found in the hash table, then insert it in TABLE[18]
897: not found in the hash table, then insert it in TABLE[17]
275: not found in the hash table, then insert it in TABLE[15]
653: not found in the hash table, then insert it in TABLE[8]
426: not found in the hash table, then insert it in TABLE[9]
154: not found in the hash table, then insert it in TABLE[3]
509: not found in the hash table, then insert it in TABLE[14]
612: not found in the hash table, then insert it in TABLE[13]
677: not found in the hash table, then insert it in TABLE[11]
765: not found in the hash table, then insert it in TABLE[6]
703: not found in the hash table, then insert it in TABLE[1]

Print the current Hash Table with 16 nodes:
 1:703
 3:154
 5:61
 6:765
 8:653
 9:426
10:503
11:677
12:87
13:612
14:509
15:275
16:908
17:897
18:170
19:512

Search Node 765 in current Hash Table:
765 found in the hash table: TABLE[6]

  1: not found in the hash table, then insert it in TABLE[2]
  2: not found in the hash table, then insert it in TABLE[7]
  3: not found in the hash table, then insert it in TABLE[4]
Error: Hash Table Overflow!, Key:4 can not be inserted!
Error: Hash Table Overflow!, Key:5 can not be inserted!
```

---
#Reference
<< The art of computer programming: Sorting and Searching >> VOLUME 3, DONALD E. KNUTH
