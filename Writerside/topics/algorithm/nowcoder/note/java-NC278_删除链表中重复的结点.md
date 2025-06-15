# java-NC278 删除链表中重复的结点


    import java.util.*;
    /*
     public class ListNode {
        int val;
        ListNode next = null;
        ListNode(int val) {
            this.val = val;
        }
    }
    */
    
    /**
     * NC278 删除链表中重复的结点
     * @author d3y1
     */
    public class Solution {
        public ListNode deleteDuplication(ListNode pHead) {
            // return solution1(pHead);
            // return solution2(pHead);
            // return solution3(pHead);
            // return solution33(pHead);
            return solution4(pHead);
        }
    
        /**
         * 指针
         * @param pHead
         * @return
         */
        private ListNode solution1(ListNode pHead){
            if(pHead==null || pHead.next==null){
                return pHead;
            }
    
            ListNode dummyHead = new ListNode(-1);
            dummyHead.next = pHead;
    
            ListNode pre,curr,next;
            pre = dummyHead;
            curr = pHead;
            while(curr!=null && curr.next!=null){
                next = curr.next;
                if(curr.val == next.val){
                    while(next!=null && next.val==curr.val){
                        next = next.next;
                    }
                    pre.next = next;
                }else{
                    pre = curr;
                }
                curr = next;
            }
    
            return dummyHead.next;
        }
    
        /**
         * 指针: 简化
         * @param pHead
         * @return
         */
        private ListNode solution2(ListNode pHead){
            if(pHead==null || pHead.next==null){
                return pHead;
            }
    
            ListNode dummyHead = new ListNode(-1);
            dummyHead.next = pHead;
    
            ListNode curr = dummyHead;
            int val;
            while(curr.next!=null && curr.next.next!=null){
                if(curr.next.val == curr.next.next.val){
                    val = curr.next.val;
                    while(curr.next!=null && curr.next.val==val){
                        curr.next = curr.next.next;
                    }
                }else{
                    curr = curr.next;
                }
            }
    
            return dummyHead.next;
        }
    
        /**
         * 哈希
         * 
         * 有序无序 均可!
         * 
         * @param pHead
         * @return
         */
        private ListNode solution3(ListNode pHead){
            if(pHead==null || pHead.next==null){
                return pHead;
            }
    
            ListNode dummyHead = new ListNode(-1);
            dummyHead.next = pHead;
    
            HashMap<Integer,Integer> cntMap = new HashMap<>();
            ListNode curr = pHead;
            while(curr != null){
                cntMap.put(curr.val, cntMap.getOrDefault(curr.val,0)+1);
                curr = curr.next;
            }
    
            ListNode pre = dummyHead;
            curr = pHead;
            while(curr != null){
                if(cntMap.get(curr.val) >= 2){
                    curr = curr.next;
                    pre.next = curr;
                }else{
                    pre = curr;
                    curr = curr.next;
                }
            }
    
            return dummyHead.next;
        }
    
        /**
         * 哈希: 简化
         * 
         * 有序无序 均可!
         * 
         * @param pHead
         * @return
         */
        private ListNode solution33(ListNode pHead){
            if(pHead==null || pHead.next==null){
                return pHead;
            }
    
            ListNode dummyHead = new ListNode(-1);
            dummyHead.next = pHead;
    
            HashMap<Integer,Integer> cntMap = new HashMap<>();
            ListNode curr = pHead;
            while(curr != null){
                cntMap.put(curr.val, cntMap.getOrDefault(curr.val,0)+1);
                curr = curr.next;
            }
    
            curr = dummyHead;
            while(curr.next != null){
                if(cntMap.get(curr.next.val) >= 2){
                    curr.next = curr.next.next;
                }else{
                    curr = curr.next;
                }
            }
    
            return dummyHead.next;
        }
    
        /**
         * 递归
         * @param pHead
         * @return
         */
        private ListNode solution4(ListNode pHead){
            return del(pHead);
        }
    
        /**
         * 删除重复: 递归
         * @param pHead
         * @return
         */
        private ListNode del(ListNode pHead){
            if(pHead==null || pHead.next==null){
                return pHead;
            }
    
            if(pHead.val == pHead.next.val){
                ListNode tail = pHead.next;
                while(tail!=null && tail.val==pHead.val){
                    tail = tail.next;
                }
                return del(tail);
            }else{
                pHead.next = del(pHead.next);
                return pHead;
            }
        }
    }
    

  

