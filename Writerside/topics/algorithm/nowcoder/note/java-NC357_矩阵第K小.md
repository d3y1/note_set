# java-NC357 矩阵第K小


    import java.util.*;
    
    /**
     * NC357 矩阵第K小
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param matrix int整型ArrayList<ArrayList<>> 
         * @param k int整型 
         * @return int整型
         */
        public int KthinMatrix (ArrayList<ArrayList<Integer>> matrix, int k) {
            // return solution1(matrix, k);
            // return solution2(matrix, k);
            return solution3(matrix, k);
        }
    
        /**
         * 堆
         * @param matrix
         * @param k
         * @return
         */
        private int solution1(ArrayList<ArrayList<Integer>> matrix, int k){
            PriorityQueue<Integer> minHeap = new PriorityQueue<Integer>();
            int n = matrix.size();
    
            for(int i=0; i<n; i++){
                for(int j=0; j<n; j++){
                    minHeap.offer(matrix.get(i).get(j));
                }
            }
    
            while(!minHeap.isEmpty() && --k>0){
                minHeap.poll();
            }
    
            return minHeap.peek();
        }
    
        /**
         * 归并 + 小根堆: 利用行有序性
         * @param matrix
         * @param k
         * @return
         */
        private int solution2(ArrayList<ArrayList<Integer>> matrix, int k){
            int n = matrix.size();
    
    //        PriorityQueue<int[]> minHeap = new PriorityQueue<>(new Comparator<int[]>(){
    //            @Override
    //            public int compare(int[] o1, int[] o2){
    //                return o1[0]-o2[0];
    //            }
    //        });
    //        PriorityQueue<int[]> minHeap = new PriorityQueue<>((o1, o2) -> o1[0]-o2[0]);
            PriorityQueue<int[]> minHeap = new PriorityQueue<>(Comparator.comparingInt(o -> o[0]));
    
            int row,col,num;
            for(int i=0; i<n; i++){
                row = i;
                col = 0;
                num = matrix.get(row).get(col);
                minHeap.offer(new int[]{num, row, col});
            }
    
            while(!minHeap.isEmpty() && --k>0){
                int[] curr = minHeap.poll();
                if(curr[2] != n-1){
                    row = curr[1];
                    col = curr[2]+1;
                    num = matrix.get(row).get(col);
                    minHeap.offer(new int[]{num, row, col});
                }
            }
    
            return minHeap.peek()[0];
        }
    
        /**
         * 二分: 利用行列有序性
         * @param matrix
         * @param k
         * @return
         */
        private int solution3(ArrayList<ArrayList<Integer>> matrix, int k){
            int n = matrix.size();
            // 矩阵最小值
            int left = matrix.get(0).get(0);
            // 矩阵最大值
            int right = matrix.get(n-1).get(n-1);
            int mid;
            while(left <= right){
                mid = left+(right-left)/2;
                // 若cnt(mid)<k, left=mid+1(left增大); 最终left为第一个满足cnt(left)>=k的数, 即为所求
                if(check(matrix, k, n, mid)){
                    left = mid+1;
                }else{
                    right = mid-1;
                }
            }
    
            return left;
        }
    
        /**
         * 校验: 小于等于mid的个数(cnt)是否小于k
         * @param matrix
         * @param k
         * @param n
         * @param mid
         * @return
         */
        private boolean check(ArrayList<ArrayList<Integer>> matrix, int k, int n, int mid){
            // 从左下角开始(matrix[n-1][0])
            int row = n-1;
            int col = 0;
            int cnt = 0;
            int curr;
            while(row>=0 && col<n){
                curr = matrix.get(row).get(col);
                // 统计小于等于mid的个数
                if(curr <= mid){
                    cnt += row+1;
                    col++;
                }else{
                    row--;
                }
            }
    
            return cnt<k;
        }
    }

  

