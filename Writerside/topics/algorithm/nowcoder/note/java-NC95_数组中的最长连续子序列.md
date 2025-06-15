# java-NC95 数组中的最长连续子序列


    import java.util.*;
    
    /**
     * NC95 数组中的最长连续子序列
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * max increasing subsequence
         * @param arr int整型一维数组 the array
         * @return int整型
         */
        public int MLS (int[] arr) {
            // return solution1(arr);
            // return solution2(arr);
            // return solution3(arr);
            // return solution4(arr);
            return solution5(arr);
        }
    
        /**
         * 小根堆
         * @param arr
         * @return
         */
        private int solution1(int[] arr){
            PriorityQueue<Integer> minHeap = new PriorityQueue<>();
            for(int num: arr){
                minHeap.offer(num);
            }
    
            int result = 0;
            int len = 1;
            int pre = minHeap.poll();
            int cur;
            while(!minHeap.isEmpty()){
                cur = minHeap.poll();
                if(cur == pre){
                    continue;
                }
                else if(cur == pre+1){
                    len++;
                    result = Math.max(result, len);
                    pre = cur;
                }
                else{
                    len = 1;
                    pre = cur;
                }
            }
    
            return result;
        }
    
        /**
         * 排序
         * @param arr
         * @return
         */
        private int solution2(int[] arr){
            int n = arr.length;
            Arrays.sort(arr);
    
            int result = 0;
            int len = 1;
            for(int i=0; i+1<n; i++){
                if(arr[i+1] == arr[i]){
                    continue;
                }
                else if(arr[i+1] == arr[i]+1){
                    len++;
                    result = Math.max(result, len);
                }
                else{
                    len = 1;
                }
            }
    
            return result;
        }
    
        /**
         * HashSet
         * @param arr
         * @return
         */
        private int solution3(int[] arr){
            HashSet<Integer> set = new HashSet<>();
    
            for(int num: arr){
                set.add(num);
            }
    
            int result = 0;
            int len;
            for(int num: arr){
                if(set.contains(num-1)){
                    continue;
                }
    
                int start = num;
                len = 1;
                while(set.contains(++start)){
                    len++;
                }
    
                result = Math.max(result, len);
            }
    
            return result;
        }
    
        /**
         * HashMap
         * @param arr
         * @return
         */
        private int solution4(int[] arr){
            HashMap<Integer, Integer> map = new HashMap<>();
    
            int result = 0;
            int leftLen,rightLen,curLen;
            for(int num: arr){
                if(!map.containsKey(num)){
                    leftLen = map.getOrDefault(num-1, 0);
                    rightLen = map.getOrDefault(num+1, 0);
                    curLen = leftLen+1+rightLen;
                    map.put(num, curLen);
                    result = Math.max(result, curLen);
                    map.put(num-leftLen, curLen);
                    map.put(num+rightLen, curLen);
                }
            }
    
            return result;
        }
    
        /**
         * 并查集
         * @param arr
         * @return
         */
        private int solution5(int[] arr){
            UnionFind uf = new UnionFind(arr);
    
            HashSet<Integer> set = new HashSet<>();
            for(int num: arr){
                set.add(num);
            }
    
            for(int num: arr){
                if(set.contains(num-1)){
                    uf.union(num, num-1);
                }
            }
    
            return uf.maxSize();
        }
    
        private class UnionFind {
            int size;
            HashMap<Integer, Integer> parent = new HashMap<>();
            HashMap<Integer, Integer> sizeMap = new HashMap<>();
    
            UnionFind(int[] nums){
                this.size = 0;
                for(int num: nums){
                    parent.put(num, num);
                    sizeMap.put(num, 1);
                }
            }
    
            int find(int x){
                int par = parent.get(x);
                while(x != par){
                    parent.put(x, parent.get(par));
                    x = par;
                    par = parent.get(x);
                }
    
                return x;
            }
    
            void union(int p, int q){
                int rootP = find(p);
                int rootQ = find(q);
                if(rootP != rootQ){
                    int unionSize = sizeMap.get(rootP)+sizeMap.get(rootQ);
                    if(rootP < rootQ){
                        parent.put(rootP, rootQ);
                        sizeMap.put(rootQ, unionSize);
                    }else{
                        parent.put(rootQ, rootP);
                        sizeMap.put(rootP, unionSize);
                    }
                    this.size = Math.max(size, unionSize);
                }
            }
    
            int maxSize(){
                return this.size;
            }
        }
    }

  

