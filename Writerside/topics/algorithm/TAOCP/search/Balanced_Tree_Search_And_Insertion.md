# Balanced_Tree_Search_And_Insertion

#Algorithm A
**Algorithm A** (**Balanced tree search and insertion**). Given a table of records 
that form a balanced binary tree as described above, this algorithm searches for 
a given argument K. If K is not in the table, a new node containing K is inserted 
into the tree in the appropriate place and the tree is rebalanced if necessary. 
The nodes of the tree are assumed to contain KEY, LLINK, and RLINK fields 
as in Algorithm 6.2.2T. We also have a new field 
                                   B(P) = balance factor of NODE (P), 
the height of the right subtree minus the height of the left subtree; this field 
always contains either +1, 0, or -1. A special header node also appears at the 
top of the tree, in location HEAD; the value of RLINK (HEAD) is a pointer to the 
root of the tree, and LLINK (HEAD) is used to keep track of the overall height of 
the tree. (Knowledge of the height is not really necessary for this algorithm, but 
it is useful in the concatenation procedure discussed below.) We assume that 
the tree is nonempty, namely that RLINK (HEAD) != Null. 
For convenience in description, the algorithm uses the notation LINK (a,P) 
as a synonym for LLINK (P) if a = -1, and for RLINK (P) if a = +1. 
**A1**. [Initialize.] Set T <-- HEAD, S <-- P <-- RLINK (HEAD). (The pointer variable P 
will move down the tree; S will point to the place where rebalancing may 
be necessary, and T always points to the parent of S.) 
**A2**. [Compare.] If K < KEY(P), go to A3; if K > KEY(P), go to A4; and if 
K = KEY(P), the search terminates successfully. 
**A3**. [Move left.] Set Q <-- LLINK(P). If Q = Null, set Q <= AVAIL and LLINK(P) <-- Q 
and go to step A5. Otherwise if B(Q) != 0, set T <-- P and S <-- Q. Finally 
set P <-- Q and return to step A2. 
**A4**. [Move right.] Set Q <-- RLINK(P). If Q = Null, set Q <= AVAIL and RLINK (P) <-- Q 
and go to step A5. Otherwise if B(Q) != 0, set T <-- P and S <-- Q. Finally set 
P <-- Q and return to step A2. (The last part of this step may be combined 
with the last part of step A3.) 
**A5**. [Insert.] (We have just linked a new node, NODE(Q), into the tree, and its 
fields need to be initialized.) Set KEY(Q) <-- K, LLINK(Q) <-- RLINK(Q) <-- Null, 
and B(Q) <-- 0. 
**A6**. [Adjust balance factors.] (Now the balance factors on nodes between S 
and Q need to be changed from zero to ±1.) If K < KEY(S) set a <-- -1, 
otherwise set a <-- +1. Then set R <-- P <-- LINK (a, S), and repeatedly do 
the following operations zero or more times until P = Q: If K < KEY(P) set 
B(P) <-- -1 and P <-- LLINK(P); if K > KEY(P), set B(P) <-- +1 and P <-- 
RLINK(P). (If K = KEY(P), then P = Q and we proceed to the next step.) 
**A7**. [Balancing act.] Several cases now arise: 
i) If B(S) =0 (the tree has grown higher), set B(S) <-- a, LLINK(HEAD) 
<-- LLINK(HEAD) + 1, and terminate the algorithm, 
ii) If B(S) = -a (the tree has gotten more balanced), set B(S) <-- 0 and 
terminate the algorithm. 
iii) If B(S) = a (the tree has gotten out of balance), go to step A8 if 
B(R) = a, to A9 if B(R) = -a. 
(Case (iii) corresponds to the situations depicted in (i) when a = +1; 
S and R point, respectively, to nodes A and B, and LINK(-a,S) points 
to alpha, etc.) 
**A8**. [Single rotation.] Set P <-- R, LINK (a, S) <-- LINK (-a, R), LINK (-a, R) <-- S, 
B(S) <-- B(R) <-- 0. Go to A10. 
**A9**. [Double rotation.] Set P <-- LINK(-a,R), LINK (-a,R) <-- LINK(a,P), 
LINK(a,P) <-- R, LINK(a.S) <-- LINK(-a,P), LINK(-a,P) <-- S. Now set 
                                             { (-a,0), if B(P)= a; 
               (B(S), B(R))  <--  { ( 0,0), if B(P) = 0;                                      (3)  
                                             {( 0,a), if B(P) =-a; 
and then set B(P) <-- 0. 
**A10**. [Finishing touch.] (We have completed the rebalancing transformation, 
taking (1) to (2)), with P pointing to the new subtree root and T pointing 
to the parent of the old subtree root S.) If S = RLINK(T) then set 
RLINK(T) <-- P, otherwise set LLINK(T) <-- P. **|** 

---
#Flow diagram
![这里写图片描述](https://img-blog.csdn.net/20151106155707619)

---
#Balanced tree
![这里写图片描述](https://img-blog.csdn.net/20151106155723168) 

![这里写图片描述](https://img-blog.csdn.net/20151106155739347)


---
#Java program
In this program, **R1,...,RN** were simplified to **K1,...,KN**.


**Node.java**
```java
package com.algorithms.searching;

/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/12/13
 * Time: 6:52 PM
 * :)~
 * Balanced Tree Search And Insertion:Searching
 */
public class Node {
    int KEY;
    int B;
    Node LLINK;
    Node RLINK;
    Node(int key){
        KEY = key;
        LLINK=null;
        RLINK=null;
        B=0;
    }
}
```

**Tree.java**
```java
package com.algorithms.searching;

/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/12/13
 * Time: 5:22 PM
 * :)~
 * Balanced Tree Search And Insertion:Searching
 */

public class Tree {
    public Node HEAD = new Node(0);
    public Node ROOT = null;
    private int index = 1;

    public void insertNode(Node P, int key){
        Node node = new Node(key);
        node.LLINK = null;
        node.RLINK = null;
        if(ROOT == null){
            ROOT = node;
            HEAD.RLINK = ROOT;
        }else if(key < P.KEY){
            P.LLINK = node;
        }else if(key > P.KEY){
            P.RLINK = node;
        }
    }

    public void inorderTreePrint(Node root){
        if(root != null){
            inorderTreePrint(root.LLINK);
            System.out.println((index++)+":"+root.KEY);
            inorderTreePrint(root.RLINK);
        }
    }
}
```

**Main.java**
```java
package com.algorithms.searching;

/**
 * Created with IntelliJ IDEA.
 * User: 1O1O
 * Date: 12/12/13
 * Time: 6:52 PM
 * :)~
 * Balanced Tree Search And Insertion:Searching
 */
public class Main {

    public static Tree tree = new Tree();
    public static int i =1;

    public static void searchAndInsertNode(int key){
        Node T = tree.HEAD;
        Node S = tree.HEAD.RLINK;
        Node P = tree.HEAD.RLINK;
        int a;
        if(P == null){
            tree.insertNode(P, key);
            System.out.println(String.format("%2s", i++)+":"+String.format("%4s", key)+": not found in the current balanced tree, and then insert it in the tree.");
        }else {
            do{
                if(key < P.KEY){
                    Node Q = P.LLINK;
                    if(Q == null){
                        tree.insertNode(P, key);
                        System.out.println(String.format("%2s", i++)+":"+String.format("%4s", key)+": not found in the current balanced tree, and then insert it in the tree.");
                        Node R = null;
                        if(key < S.KEY){                    /*A6*/
                            a = -1;
                        }else {
                            a = 1;
                        }
                        if(a == -1){
                            R = P = S.LLINK;
                        }else if(a == 1){
                            R = P = S.RLINK;
                        }
                        do{
                            if(key < P.KEY){
                                P.B = -1;
                                P = P.LLINK;
                            }else if(key > P.KEY){
                                P.B = 1;
                                P = P.RLINK;
                            }else {
                                break;
                            }
                        }while (true);
                        if(S.B == 0){                            /*A7 i)*/
                            S.B = a;
                            tree.HEAD.KEY++; /*Keep track of overall height of tree*/
                            break;
                        }else if(S.B == -a){                     /*A7 ii)*/
                            S.B = 0;
                            break;
                        }else if(S.B == a){                      /*A7 iii)*/
                            if(R.B == a){
                                P = R;                           /*A8*/
                                if(a == -1){
                                    S.LLINK = R.RLINK;
                                    R.RLINK = S;
                                }else if(a == 1){
                                    S.RLINK = R.LLINK;
                                    R.LLINK = S;
                                }
                                S.B = R.B = 0;
                            }else if(R.B == -a){
                                if(a == -1){                  /*A9*/
                                    P = R.RLINK;
                                    R.RLINK = P.LLINK;
                                    P.LLINK = R;
                                    S.LLINK = P.RLINK;
                                    P.RLINK = S;
                                }else if(a == 1){
                                    P = R.LLINK;
                                    R.LLINK = P.RLINK;
                                    P.RLINK = R;
                                    S.RLINK = P.LLINK;
                                    P.LLINK = S;
                                }
                                if(P.B == a){
                                    S.B = -a;
                                    R.B = 0;
                                }else if(P.B == 0){
                                    S.B = 0;
                                    R.B = 0;
                                }else if(P.B == -a){
                                    S.B = 0;
                                    R.B = a;
                                }
                                P.B = 0;
                            }
                            if(S == T.RLINK){              /*A10*/
                                T.RLINK = P;
                            }else {
                                T.LLINK = P;
                            }
                        }
                        break;
                    }else {
                        if(Q.B != 0){
                            T = P;
                            S = Q;
                        }
                        P = Q;
                    }
                }else if(key > P.KEY){
                    Node Q = P.RLINK;
                    if(Q == null){
                        tree.insertNode(P, key);
                        System.out.println(String.format("%2s", i++)+":"+String.format("%4s", key)+": not found in the current balanced tree, and then insert it in the tree.");
                        Node R = null;
                        if(key < S.KEY){                    /*A6*/
                            a = -1;
                        }else {
                            a = 1;
                        }
                        if(a == -1){
                            R = P = S.LLINK;
                        }else if(a == 1){
                            R = P = S.RLINK;
                        }
                        do{
                            if(key < P.KEY){
                                P.B = -1;
                                P = P.LLINK;
                            }else if(key > P.KEY){
                                P.B = 1;
                                P = P.RLINK;
                            }else {
                                break;
                            }
                        }while (true);
                        if(S.B == 0){                            /*A7 i)*/
                            S.B = a;
                            tree.HEAD.KEY++; /*Keep track of overall height of tree*/
                            break;
                        }else if(S.B == -a){                     /*A7 ii)*/
                            S.B = 0;
                            break;
                        }else if(S.B == a){                      /*A7 iii)*/
                            if(R.B == a){
                                P = R;                           /*A8*/
                                if(a == -1){
                                    S.LLINK = R.RLINK;
                                    R.RLINK = S;
                                }else if(a == 1){
                                    S.RLINK = R.LLINK;
                                    R.LLINK = S;
                                }
                                S.B = R.B = 0;
                            }else if(R.B == -a){
                                if(a == -1){                  /*A9*/
                                    P = R.RLINK;
                                    R.RLINK = P.LLINK;
                                    P.LLINK = R;
                                    S.LLINK = P.RLINK;
                                    P.RLINK = S;
                                }else if(a == 1){
                                    P = R.LLINK;
                                    R.LLINK = P.RLINK;
                                    P.RLINK = R;
                                    S.RLINK = P.LLINK;
                                    P.LLINK = S;
                                }
                                if(P.B == a){
                                    S.B = -a;
                                    R.B = 0;
                                }else if(P.B == 0){
                                    S.B = 0;
                                    R.B = 0;
                                }else if(P.B == -a){
                                    S.B = 0;
                                    R.B = a;
                                }
                                P.B = 0;
                            }
                            if(S == T.RLINK){              /*A10*/
                                T.RLINK = P;
                            }else {
                                T.LLINK = P;
                            }
                        }
                        break;
                    }else {
                        if(Q.B != 0){
                            T = P;
                            S = Q;
                        }
                        P = Q;
                    }
                }else {
                    System.out.println(key+" found in the balanced binary tree.");
                    break;
                }
            }while (true);
        }
    }

    public static void main(String[] args) {

        /*Prepare the binary tree*/
        System.out.println("Prepare the balanced binary tree:");
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

        /*Inorder print the current balanced binary tree with 16 nodes*/
        System.out.println("Inorder print the current balanced binary tree with 16 nodes:");
        tree.inorderTreePrint(tree.ROOT);
        System.out.println();

        /*Search Node 765 in current balanced binary tree*/
        System.out.println("Search Node 765 in current balanced binary tree:");
        searchAndInsertNode(765);
    }
}
```

---
#Outputs
```
Prepare the balanced binary tree:
 1: 503: not found in the current balanced tree, and then insert it in the tree.
 2:  87: not found in the current balanced tree, and then insert it in the tree.
 3: 512: not found in the current balanced tree, and then insert it in the tree.
 4:  61: not found in the current balanced tree, and then insert it in the tree.
 5: 908: not found in the current balanced tree, and then insert it in the tree.
 6: 170: not found in the current balanced tree, and then insert it in the tree.
 7: 897: not found in the current balanced tree, and then insert it in the tree.
 8: 275: not found in the current balanced tree, and then insert it in the tree.
 9: 653: not found in the current balanced tree, and then insert it in the tree.
10: 426: not found in the current balanced tree, and then insert it in the tree.
11: 154: not found in the current balanced tree, and then insert it in the tree.
12: 509: not found in the current balanced tree, and then insert it in the tree.
13: 612: not found in the current balanced tree, and then insert it in the tree.
14: 677: not found in the current balanced tree, and then insert it in the tree.
15: 765: not found in the current balanced tree, and then insert it in the tree.
16: 703: not found in the current balanced tree, and then insert it in the tree.

Inorder print the current balanced binary tree with 16 nodes:
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

Search Node 765 in current balanced binary tree:
765 found in the balanced binary tree.
```

---
#Reference
<< The art of computer programming: Sorting and Searching >> VOLUME 3, DONALD E. KNUTH
