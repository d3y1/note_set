# java-NC21 链表内指定区间反转


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
     * NC21 链表内指定区间反转
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 
         * @param head ListNode类 
         * @param m int整型 
         * @param n int整型 
         * @return ListNode类
         */
        public ListNode reverseBetween (ListNode head, int m, int n) {
            // 总共一个 不用反转
            if(m == n){
                return head;
            }
    
            // 假头
            ListNode dummyHead = new ListNode(-1);
            dummyHead.next = head;
            // 前面
            ListNode pre = dummyHead;
            // 当前
            ListNode curr = pre.next;
            // 后面
            ListNode next;
            // 头插法 反转节点插入位置
            ListNode flag = new ListNode(-1);
            // dummyHead->head->...->flag->pre->curr->next...
            for(int i=1; i<=n; i++){
                if(curr == null){
                    break;
                }
                next = curr.next;
                // 指针右移
                if(i < m){
                    pre = curr;
                    curr = next;
                }
                // 标记插入位置 指针右移
                else if(i == m){
                    flag = pre;
                    pre = curr;
                    curr = next;
                }
                // 反转节点 头插法插入
                else if(i > m){
                    pre.next = curr.next;
                    curr.next = flag.next;
                    flag.next = curr;
                    curr = next;
                }
            }
    
            return dummyHead.next;
        }
    }

  

