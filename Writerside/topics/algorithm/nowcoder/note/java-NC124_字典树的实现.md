# java-NC124 字典树的实现


    import java.util.*;
    
    /**
     * NC124 字典树的实现
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param operators string字符串二维数组 the ops
         * @return string字符串一维数组
         */
        public String[] trieU (String[][] operators) {
            List<String> resultList = new ArrayList<>();
            Trie root = new Trie();
            for(String[] op: operators){
                switch(op[0]){
                    case "1":{
                        root.insert(op[1]);
                        break;
                    }
                    case "2":{
                        root.delete(op[1]);
                        break;
                    }
                    case "3":{
                        boolean found = root.search(op[1]);
                        if(found){
                            resultList.add("YES");
                        }else{
                            resultList.add("NO");
                        }
                        break;
                    }
                    case "4":{
                        int count = root.prefixNumber(op[1]);
                        resultList.add(String.valueOf(count));
                    }
                    default:break;
                }
            }
    
            String[] result = new String[resultList.size()];
            for(int i=0; i<resultList.size(); i++){
                result[i] = resultList.get(i);
            }
    
            return result;
        }
    
        /**
         * 字典树Trie
         */
        private class Trie {
            private Trie[] children;
            boolean isEnd;
            private int count;
    
            public Trie(){
                children = new Trie[26];
                isEnd = false;
                count = 0;
            }
    
            public void insert(String word){
                Trie curr = this;
                int index;
                for(char ch: word.toCharArray()){
                    index = ch - 'a';
                    if(curr.children[index] == null){
                        curr.children[index] = new Trie();
                    }
                    curr = curr.children[index];
                    curr.count++;
                }
                curr.isEnd = true;
            }
    
            public void delete(String word){
                Trie curr = this;
                int index;
                for(char ch: word.toCharArray()){
                    index = ch - 'a';
                    if(curr.children[index] != null){
                        curr = curr.children[index];
                        curr.count--;
                    }
                }
                if(curr.count == 0){
                    curr.isEnd = false;
                }
            }
    
            public boolean search(String word){
                Trie curr = this;
                int index;
                for(char ch: word.toCharArray()){
                    index = ch - 'a';
                    if(curr.children[index] == null){
                        return false;
                    }
                    curr = curr.children[index];
                }
                if(!curr.isEnd){
                    return false;
                }
    
                return true;
            }
    
            public int prefixNumber(String pre){
                Trie curr = this;
                int index;
                for(char ch: pre.toCharArray()){
                    index = ch - 'a';
                    if(curr.children[index] == null){
                        return 0;
                    }
                    curr = curr.children[index];
                }
    
                return curr.count;
            }
        }
    }

  

