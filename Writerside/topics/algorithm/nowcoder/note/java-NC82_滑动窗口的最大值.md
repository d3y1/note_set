# java-NC82 滑动窗口的最大值


    import java.util.*;
    
    /**
     * NC82 滑动窗口的最大值
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param num int整型一维数组
         * @param size int整型
         * @return int整型ArrayList
         */
        public ArrayList<Integer> maxInWindows (int[] num, int size) {
            // return solution1(num, size);
            // return solution2(num, size);
            return solution3(num, size);
        }
    
        /**
         * 双指针+TreeMap
         * @param num
         * @param size
         * @return
         */
        private ArrayList<Integer> solution1(int[] num, int size){
            int n = num.length;
            if(n<size || size==0){
                return new ArrayList<>();
            }
    
            // TreeMap<Integer,Integer> map = new TreeMap<>((o1,o2) -> (o2-o1));
            // TreeMap<Integer,Integer> map = new TreeMap<>(Comparator.comparing(o -> o, Comparator.reverseOrder()));
            TreeMap<Integer,Integer> map = new TreeMap<>(new Comparator<Integer>(){
                @Override
                public int compare(Integer o1, Integer o2){
                    return o2-o1;
                }
            });
            ArrayList<Integer> list = new ArrayList<>();
    
            // 双指针
            int i = 0;
            int j = 0;
            while(j < size){
                map.put(num[j], map.getOrDefault(num[j], 0)+1);
                j++;
            }
            list.add(map.firstKey());
    
            int numL,numR;
            while(j < n){
                numL = num[i++];
                numR = num[j++];
                map.put(numL, map.get(numL)-1);
                if(map.get(numL) == 0){
                    map.remove(numL);
                }
                map.put(numR, map.getOrDefault(numR, 0)+1);
                list.add(map.firstKey());
            }
    
            return list;
        }
    
        /**
         * 大根堆(优先队列)
         * @param num
         * @param size
         * @return
         */
        private ArrayList<Integer> solution2(int[] num, int size){
            int n = num.length;
            if(n<size || size==0){
                return new ArrayList<>();
            }
    
            // 大根堆(优先队列)
            // PriorityQueue<Node> maxHeap = new PriorityQueue<>((o1,o2) -> (o2.num-o1.num));
            // PriorityQueue<Node> maxHeap = new PriorityQueue<>(Comparator.comparing(o -> o.num, Comparator.reverseOrder()));
            // PriorityQueue<Node> maxHeap = new PriorityQueue<>(Comparator.comparing(Node::getNum, Comparator.reverseOrder()));
            // PriorityQueue<Node> maxHeap = new PriorityQueue<>(Comparator.comparingInt(Node::getNum).reversed());
            PriorityQueue<Node> maxHeap = new PriorityQueue<>(new Comparator<Node>(){
                @Override
                public int compare(Node o1, Node o2){
                    return o2.num-o1.num;
                }
            });
            ArrayList<Integer> list = new ArrayList<>();
    
            for(int i=0; i<n; i++){
                maxHeap.offer(new Node(num[i], i));
    
                // 当前窗口之外(左端越界)
                while(!maxHeap.isEmpty() && maxHeap.peek().idx<=i-size){
                    maxHeap.poll();
                }
                // 能够形成窗口
                if(i+1 >= size){
                    list.add(maxHeap.peek().num);
                }
            }
    
            return list;
        }
    
        /**
         * 单调栈(双端队列)
         * @param num
         * @param size
         * @return
         */
        private ArrayList<Integer> solution3(int[] num, int size){
            int n = num.length;
            if(n<size || size==0){
                return new ArrayList<>();
            }
    
            // Deque<Integer> stack = new ArrayDeque<>();
            Deque<Integer> stack = new LinkedList<>();
            ArrayList<Integer> list = new ArrayList<>();
    
            // 单调栈 双端队列
            for(int i=0; i<n; i++){
                // 单调减
                while(!stack.isEmpty() && num[stack.peekLast()]<=num[i]){
                    stack.pollLast();
                }
                stack.offerLast(i);
    
                // 当前窗口之外(左端越界)
                if(stack.peekFirst() <= i-size){
                    stack.pollFirst();
                }
                // 能够形成窗口
                if(i+1 >= size){
                    list.add(num[stack.peekFirst()]);
                }
            }
    
            return list;
        }
    
        private class Node {
            private int num;
            private int idx;
    
            private int getNum(){
                return num;
            }
    
            private Node(int num, int idx){
                this.num = num;
                this.idx = idx;
            }
        }
    }

  

