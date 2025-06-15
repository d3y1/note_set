# java-NC317 链表相加(一)


    import java.util.*;
    
    /*
     * public class ListNode {
     *   int val;
     *   ListNode next = null;
     *   public ListNode(int val) {
     *     this.val = val;
     *   }
     * }
     */
    
    /**
     * NC317 链表相加(一)
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param l1 ListNode类
         * @param l2 ListNode类
         * @return ListNode类
         */
        public ListNode ListAdd (ListNode l1, ListNode l2) {
            return solution1(l1,l2);
            // return solution2(l1,l2);
        }
    
        /**
         * 迭代
         * @param l1
         * @param l2
         * @return
         */
        private ListNode solution1(ListNode l1, ListNode l2){
            ListNode head = new ListNode(-1);
            ListNode tail = head;
            ListNode node;
            int val1,val2,sum,carry=0;
            while(l1!=null || l2!=null || carry>0){
                if(carry == 0){
                    if(l1 == null){
                        tail.next = l2;
                        break;
                    }
                    if(l2 == null){
                        tail.next = l1;
                        break;
                    }
                }
    
                val1 = 0;
                if(l1 != null){
                    val1 = l1.val;
                    l1 = l1.next;
                }
    
                val2 = 0;
                if(l2 != null){
                    val2 = l2.val;
                    l2 = l2.next;
                }
    
                sum = val1+val2+carry;
                carry = sum/10;
                node = new ListNode(sum%10);
                // 尾插法
                tail.next = node;
                tail = node;
            }
    
            return head.next;
        }
    
        //////////////////////////////////////////////////////////////////////////////
    
        private int val1,val2,sum,carry=0;
        private ListNode head = new ListNode(-1);
        private ListNode tail = head;
        private ListNode node;
    
        /**
         * 递归: 超出内存限制!
         * @param l1
         * @param l2
         * @return
         */
        private ListNode solution2(ListNode l1, ListNode l2){
            add(l1,l2);
            return head.next;
        }
    
        private void add(ListNode l1, ListNode l2){
            if(l1==null && l2==null && carry==0){
                return;
            }
    
            val1 = 0;
            if(l1 != null){
                val1 = l1.val;
                l1 = l1.next;
            }
    
            val2 = 0;
            if(l2 != null){
                val2 = l2.val;
                l2 = l2.next;
            }
    
            sum = val1+val2+carry;
            carry = sum/10;
            node = new ListNode(sum%10);
            // 尾插法
            tail.next = node;
            tail = node;
    
            add(l1,l2);
        }
    }

  

