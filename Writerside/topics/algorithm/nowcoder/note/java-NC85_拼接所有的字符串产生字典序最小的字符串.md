# java-NC85 拼接所有的字符串产生字典序最小的字符串


    import java.util.*;
    
    /**
     * NC85 拼接所有的字符串产生字典序最小的字符串
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param strs string字符串一维数组 the strings
         * @return string字符串
         */
        public String minString (String[] strs) {
            // return solution1(strs);
            return solution2(strs);
        }
    
        /**
         * 贪心: 数组排序
         * @param strs
         * @return
         */
        private String solution1(String[] strs){
            // "bc" "bca"
            // 直接比较字典 bc<bca              => bcbca
            // 连接比较字典 bc>bca(bcbca>bcabc) => bcabc
            Arrays.sort(strs, new Comparator<String>(){
                @Override
                public int compare(String o1, String o2){
                    return (o1+o2).compareTo(o2+o1);
                }
            });
    
            StringBuilder sb = new StringBuilder();
            for(String str: strs){
                sb.append(str);
            }
    
            return sb.toString();
        }
    
        /**
         * 贪心: 优先队列(小根堆)
         * @param strs
         * @return
         */
        private String solution2(String[] strs){
            // "bc" "bca"
            // 直接比较字典 bc<bca              => bcbca
            // 连接比较字典 bc>bca(bcbca>bcabc) => bcabc
            PriorityQueue<String> minHeap = new PriorityQueue<>((o1, o2) -> (o1+o2).compareTo(o2+o1));
    
            for(String str: strs){
                minHeap.offer(str);
            }
    
            StringBuilder sb = new StringBuilder();
            while(!minHeap.isEmpty()){
                sb.append(minHeap.poll());
            }
    
            return sb.toString();
        }
    }

  

