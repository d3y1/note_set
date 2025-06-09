# 重复的DNA序列
https://www.nowcoder.com/practice/fe9099e5308042a8af2f7aabdb3719fe

    import java.util.*;
    
    /**
     * NC220 重复的DNA序列
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param DNA string字符串 1
         * @return string字符串一维数组
         */
        public String[] repeatedDNA (String DNA) {
            return solution1(DNA);
            // return solution2(DNA);
        }
    
        /**
         * 滑动窗口: HashSet
         * @param DNA
         * @return
         */
        private String[] solution1(String DNA){
            List<String> results = new ArrayList<>();
            HashSet<String> subSet = new HashSet<>();
    
            int gap = 10;
            int len = DNA.length();
            String sub;
            for(int i=0; i+gap<=len; i++){
                sub = DNA.substring(i, i+gap);
                // 当前sub: 第一次找到 且 今后还会找到
                if(!subSet.contains(sub) && DNA.substring(i+1).contains(sub)){
                    subSet.add(sub);
                    results.add(sub);
                }
            }
    
            return results.toArray(new String[results.size()]);
        }
    
        /**
         * 滑动窗口: HashSet + HashMap
         * @param DNA
         * @return
         */
        private String[] solution2(String DNA){
            List<SubDNA> resultList = new ArrayList<>();
            HashSet<String> subSet = new HashSet<>();
            HashSet<String> foundSet = new HashSet<>();
            HashMap<String, Integer> map = new HashMap<>();
    
            int gap = 10;
            int len = DNA.length();
            String sub;
            for(int i=0; i+gap<=len; i++){
                sub = DNA.substring(i, i+gap);
                if(!subSet.contains(sub)){
                    subSet.add(sub);
                    if(!map.containsKey(sub)){
                        map.put(sub, i);
                    }
                }else{
                    if(!foundSet.contains(sub)){
                        foundSet.add(sub);
                        resultList.add(new SubDNA(sub, map.get(sub)));
                    }
                }
            }
    
            // 序号升序
            Collections.sort(resultList, new Comparator<SubDNA>(){
                @Override
                public int compare(SubDNA o1, SubDNA o2){
                    return o1.seq-o2.seq;
                }
            });
    
            String[] results = new String[resultList.size()];
            for(int i=0; i<resultList.size(); i++){
                results[i] = resultList.get(i).sub;
            }
    
            return results;
        }
    
        /**
         * DNA子串
         */
        private class SubDNA {
            String sub;
            int seq;
    
            public SubDNA(String sub, int seq){
                this.sub = sub;
                this.seq = seq;
            }
        }
    }
    

