# java-NC97 字符串出现次数的TopK问题


    import java.util.*;
    
    /**
     * NC97 字符串出现次数的TopK问题
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * return topK string
         * @param strings string字符串一维数组 strings
         * @param k int整型 the k
         * @return string字符串二维数组
         */
        public String[][] topKstrings (String[] strings, int k) {
            // return solution1(strings, k);
            // return solution2(strings, k);
            return solution3(strings, k);
        }
    
        /**
         * 哈希 + 排序
         * @param strings
         * @param k
         * @return
         */
        private String[][] solution1(String[] strings, int k){
            if(k == 0){
                return new String[][]{};
            }
    
            HashMap<String, Integer> map = new HashMap<>();
            for(String str: strings){
                map.put(str, map.getOrDefault(str,0)+1);
            }
    
            ArrayList<Map.Entry<String,Integer>> list = new ArrayList<>(map.entrySet());
            Collections.sort(list, (o1, o2) -> {
                if(!o1.getValue().equals(o2.getValue())){
                    // 降序
                    return o2.getValue()-o1.getValue();
                }else{
                    // 升序
                    return (o1.getKey()).compareTo(o2.getKey());
                }
            });
    
            int size = Math.min(list.size(), k);
            String[][] results = new String[size][2];
            Map.Entry<String,Integer> entry;
            for(int i=0; i<size; i++){
                entry = list.get(i);
                results[i] = new String[]{entry.getKey(), String.valueOf(entry.getValue())};
            }
    
            return results;
        }
    
        //////////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 哈希 + 小根堆
         * @param strings
         * @param k
         * @return
         */
        private String[][] solution2(String[] strings, int k){
            if(k == 0){
                return new String[][]{};
            }
    
            HashMap<String, Integer> map = new HashMap<>();
            for(String str: strings){
                map.put(str, map.getOrDefault(str,0)+1);
            }
    
            // PriorityQueue<Node> minHeap = new PriorityQueue<>(new Comparator<Node>(){
            //     @Override
            //     public int compare(Node o1, Node o2){
            //         if(o1.cnt != o2.cnt){
            //             return o1.cnt-o2.cnt;
            //         }else{
            //             // 输入: ["abab","b","b","ab"],2  ->  输出: [["b","2"],["abab","1"]]  -> 错误
            //             // return (o2.str+o1.str).compareTo(o1.str+o2.str);
            //             // 输入: ["abab","b","b","ab"],2  ->  输出: [["b","2"],["ab","1"]]  -> 正确
            //             return (o2.str).compareTo(o1.str);
            //         }
            //     }
            // });
            PriorityQueue<Node> minHeap = new PriorityQueue<>((o1, o2) -> {
                if(o1.cnt != o2.cnt){
                    // 升序
                    return o1.cnt-o2.cnt;
                }else{
                    // 降序
                    // 输入: ["abab","b","b","ab"],2  ->  输出: [["b","2"],["abab","1"]]  -> 错误
                    // return (o2.str+o1.str).compareTo(o1.str+o2.str);
                    // 输入: ["abab","b","b","ab"],2  ->  输出: [["b","2"],["ab","1"]]  -> 正确
                    return (o2.str).compareTo(o1.str);
                }
            });
            for(Map.Entry<String, Integer> entry: map.entrySet()){
                minHeap.offer(new Node(entry.getKey(), entry.getValue()));
                if(minHeap.size() > k){
                    minHeap.poll();
                }
            }
    
            // maxHeap.size() <= k
            // int size = Math.min(maxHeap.size(), k);
            int size = minHeap.size();
            String[][] results = new String[size][2];
            int i = size-1;
            Node top;
            while(!minHeap.isEmpty()){
                top = minHeap.poll();
                results[i--] = new String[]{top.str, String.valueOf(top.cnt)};
            }
    
            return results;
        }
    
        private class Node {
            String str;
            int cnt;
            Node(String str, int cnt){
                this.str = str;
                this.cnt = cnt;
            }
        }
    
        //////////////////////////////////////////////////////////////////////////////////////
    
        /**
         * 自定义比较器
         */
        private class EntryComparator implements Comparator<Map.Entry<String,Integer>>{
            @Override
            public int compare(Map.Entry<String, Integer> o1, Map.Entry<String, Integer> o2) {
                if(!o1.getValue().equals(o2.getValue())){
                    // 升序
                    return o1.getValue()-o2.getValue();
                }else{
                    // 降序
                    return (o2.getKey()).compareTo(o1.getKey());
                }
            }
        }
    
        /**
         * 哈希 + 小根堆
         * 优化
         * @param strings
         * @param k
         * @return
         */
        private String[][] solution3(String[] strings, int k){
            if(k == 0){
                return new String[][]{};
            }
    
            HashMap<String, Integer> map = new HashMap<>();
            for(String str: strings){
                map.put(str, map.getOrDefault(str,0)+1);
            }
    
            Comparator<Map.Entry<String, Integer>> entryComparator = new EntryComparator();
            PriorityQueue<Map.Entry<String,Integer>> minHeap = new PriorityQueue<>(k, entryComparator);
            for(Map.Entry<String, Integer> entry: map.entrySet()){
                if(minHeap.size() < k){
                    minHeap.offer(entry);
                }else{
                    // minHeap.peek() < entry
                    if(entryComparator.compare(minHeap.peek(), entry) < 0){
                        minHeap.poll();
                        minHeap.offer(entry);
                    }
                }
            }
    
            // maxHeap.size() <= k
            // int size = Math.min(maxHeap.size(), k);
            int size = minHeap.size();
            String[][] results = new String[size][2];
            int i = size-1;
            Map.Entry<String,Integer> top;
            while(!minHeap.isEmpty()){
                top = minHeap.poll();
                results[i--] = new String[]{top.getKey(), String.valueOf(top.getValue())};
            }
    
            return results;
        }
    }

  

