# java-NC51 合并k个已排序的链表


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
     * NC51 合并k个已排序的链表
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param lists ListNode类ArrayList
         * @return ListNode类
         */
        public ListNode mergeKLists (ArrayList<ListNode> lists) {
            // return solution1(lists);
            // return solution2(lists);
            return solution22(lists);
            // return solution3(lists);
        }
    
        /**
         * 连续归并
         * @param lists
         * @return
         */
        private ListNode solution1(ArrayList<ListNode> lists){
            ListNode dummyHead = new ListNode(-1);
            for(ListNode list: lists){
                dummyHead.next = merge(dummyHead.next, list);
            }
    
            return dummyHead.next;
        }
    
        /**
         * 合并
         * 合并两个有序链表
         * @param list1
         * @param list2
         * @return
         */
        private ListNode merge(ListNode list1, ListNode list2){
            if(list1 == null){
                return list2;
            }
            if(list2 == null){
                return list1;
            }
    
            if(list1.val <= list2.val){
                list1.next = merge(list1.next, list2);
                return list1;
            }else{
                list2.next = merge(list1, list2.next);
                return list2;
            }
        }
    
        /**
         * 二分归并
         * @param lists
         * @return
         */
        private ListNode solution2(ArrayList<ListNode> lists){
            int k = lists.size();
            if(k == 0){
                return null;
            }
    
            int left,right;
            for(int gap=k; gap>1; gap=(gap+1)/2){
                for(int i=0; i<(gap+1)/2; i++){
                    left = i;
                    right = gap-i-1;
                    if(left < right){
                        lists.set(left, merge(lists.get(left), lists.get(right)));
                        lists.remove(right);
                    }
                }
            }
    
            return lists.get(0);
        }
    
        /**
         * 递归归并
         * @param lists
         * @return
         */
        private ListNode solution22(ArrayList<ListNode> lists){
            return divide(lists, 0, lists.size()-1);
        }
    
        /**
         * 分治: 递归
         * @param lists
         * @param left
         * @param right
         * @return
         */
        private ListNode divide(ArrayList<ListNode> lists, int left, int right){
            if(left > right){
                return null;
            }
            else if(left == right){
                return lists.get(left);
            }
    
            int mid = left+(right-left)/2;
    
            return merge(divide(lists, left, mid), divide(lists, mid+1, right));
        }
    
        /**
         * 堆: 优先队列
         * @param lists
         * @return
         */
        private ListNode solution3(ArrayList<ListNode> lists){
            PriorityQueue<Integer> minHeap = new PriorityQueue<>();
            for(ListNode node: lists){
                while(node != null){
                    minHeap.offer(node.val);
                    node = node.next;
                }
            }
    
            ListNode head = new ListNode(-1);
            ListNode tail = head;
            while(!minHeap.isEmpty()){
                tail.next = new ListNode(minHeap.poll());
                tail = tail.next;
            }
    
            return head.next;
        }
    }

  

