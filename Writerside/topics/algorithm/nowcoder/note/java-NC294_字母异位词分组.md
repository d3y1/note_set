# java-NC294 字母异位词分组


    import java.util.*;
    
    /**
     * NC294 字母异位词分组
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param strs string字符串一维数组
         * @return string字符串二维数组
         */
        public String[][] groupAnagrams (String[] strs) {
            // return solution1(strs);
            return solution2(strs);
        }
    
        /**
         * 排序+哈希
         * @param strs
         * @return
         */
        private String[][] solution1(String[] strs){
            HashMap<String, ArrayList<String>> map = new HashMap<>();
    
            String key;
            char[] chars;
            ArrayList<String> list;
            for(String str: strs){
                chars = str.toCharArray();
                Arrays.sort(chars);
                key = String.valueOf(chars);
                if(map.containsKey(key)){
                    list = map.get(key);
                }else{
                    list = new ArrayList<>();
                }
                list.add(str);
                map.put(key, list);
            }
    
            String[][] result = new String[map.size()][];
            int i = 0;
            for(String keyWord: map.keySet()){
                list = map.get(keyWord);
                result[i] = new String[list.size()];
                for(int j=0; j<list.size(); j++){
                    result[i][j] = list.get(j);
                }
                i++;
            }
    
            return result;
        }
    
        /**
         * 排序+哈希: 简化
         * @param strs
         * @return
         */
        private String[][] solution2(String[] strs){
            HashMap<String, ArrayList<String>> map = new HashMap<>();
    
            String key;
            char[] chars;
            ArrayList<String> list;
            for(String str: strs){
                chars = str.toCharArray();
                Arrays.sort(chars);
                key = String.valueOf(chars);
                if(map.containsKey(key)){
                    list = map.get(key);
                }else{
                    list = new ArrayList<>();
                }
                list.add(str);
                map.put(key, list);
            }
    
            String[][] result = new String[map.size()][];
            int i = 0;
            for(String keyWord: map.keySet()){
                list = map.get(keyWord);
                result[i] = new String[list.size()];
                list.toArray(result[i]);
                i++;
            }
    
            return result;
        }
    }

  

