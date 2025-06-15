# java-NC119 最小的K个数


    import java.util.*;
    
    /**
     * NC119 最小的K个数
     * @author d3y1
     */
    public class Solution {
        private int N;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param input int整型一维数组
         * @param k int整型
         * @return int整型ArrayList
         */
        public ArrayList<Integer> GetLeastNumbers_Solution (int[] input, int k) {
            // return solution1(input, k);
            return solution2(input, k);
            // return solution3(input, k);
            // return solution4(input, k);
        }
    
        /**
         * 堆排序: 最小堆|小顶堆|小根堆
         * @param input
         * @param k
         * @return
         */
        private ArrayList<Integer> solution1(int[] input, int k){
            PriorityQueue<Integer> minHeap = new PriorityQueue<>();
            for(int num: input){
                minHeap.offer(num);
            }
    
            ArrayList<Integer> list = new ArrayList<>();
            while(!minHeap.isEmpty() && k-->0){
                list.add(minHeap.poll());
            }
    
            return list;
        }
    
        /**
         * 堆排序: 最大堆|大顶堆|大根堆
         * @param input
         * @param k
         * @return
         */
        private ArrayList<Integer> solution2(int[] input, int k){
            if(k == 0){
                return new ArrayList<>();
            }
    
            // PriorityQueue<Integer> maxHeap = new PriorityQueue<>((o1,o2) -> (o2-o1));
            PriorityQueue<Integer> maxHeap = new PriorityQueue<>(new Comparator<Integer>(){
                @Override
                public int compare(Integer o1, Integer o2){
                    return o2-o1;
                }
            });
            
            int top;
            for(int num: input){
                if(maxHeap.size() < k){
                    maxHeap.offer(num);
                }else{
                    if(!maxHeap.isEmpty()){
                        top = maxHeap.peek();
                        if(num < top){
                            maxHeap.poll();
                            maxHeap.offer(num);
                        }
                    }
                }
            }
    
            ArrayList<Integer> list = new ArrayList<>();
            while(!maxHeap.isEmpty()){
                list.add(maxHeap.poll());
            }
    
            return list;
        }
    
        /**
         * 快速排序(quickSort)
         * @param input
         * @param k
         * @return
         */
        private ArrayList<Integer> solution3(int[] input, int k){
            N = input.length;
    
            quickSort(input, 0, N-1, k);
    
            ArrayList<Integer> list = new ArrayList<>();
            for(int i=0; i<k; i++){
                list.add(input[i]);
            }
    
            return list;
        }
    
        /**
         * 快排
         * @param nums
         * @param p
         * @param r
         * @param k
         */
        private void quickSort(int[] nums, int p, int r, int k){
            if(p < r){
                int q = partition(nums, p, r);
                // 判断 q==k 或者 q==k-1 都可以
                if(q == k){
                    return;
                }else if(q < k){
                    quickSort(nums, q+1, r, k);
                }else{
                    quickSort(nums, p, q-1, k);
                }
            }
        }
    
        /**
         * 分治(分区)
         * @param nums
         * @param p
         * @param r
         * @return
         */
        private int partition(int[] nums, int p, int r){
            int x = nums[r];
            int i = p-1;
            for(int j=p; j<r; j++){
                if(nums[j] < x){
                    i++;
                    swap(nums, i, j);
                }
            }
            swap(nums, i+1, r);
    
            return i+1;
        }
    
        /**
         * 交换
         * @param nums
         * @param i
         * @param j
         */
        private void swap(int[] nums, int i, int j){
            int tmp = nums[i];
            nums[i] = nums[j];
            nums[j] = tmp;
        }
    
        /**
         * 排序: 数组
         * @param input
         * @param k
         * @return
         */
        private ArrayList<Integer> solution4(int[] input, int k){
            Arrays.sort(input);
    
            ArrayList<Integer> list = new ArrayList<Integer>();
            for(int i=0; i<k; i++){
                list.add(input[i]);
            }
    
            return list;
        }
    }

  

