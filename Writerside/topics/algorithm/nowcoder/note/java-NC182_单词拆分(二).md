# java-NC182 单词拆分(二)

```java
import java.util.*;

/**
 * NC182 单词拆分(二)
 * @author d3y1
 */
public class Solution {
    private int len;
    private ArrayList<String> list = new ArrayList<>();

    private HashSet<String> set = new HashSet<>();

    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     *
     * @param s string字符串
     * @param dic string字符串一维数组
     * @return string字符串一维数组
     */
    public String[] wordDiv (String s, String[] dic) {
        // return solution1(s, dic);
        return solution2(s, dic);
        // return solution3(s, dic);
        // return solution4(s, dic);
    }

    /**
     * 动态规划
     *
     * dp[i]表示字符串s前i个字符组成的字符串能否拆分
     *
     * dp[i] = dp[j] && check(s[j..i−1])  , 0<=j<i
     * check(s[j..i−1]) => map.getOrDefault(suffix, false)
     * 其中 check(s[j..i−1]) 表示子串s[j..i−1]是否出现在字典中
     *
     * @param s
     * @param dic
     * @return
     */
    private String[] solution1(String s, String[] dic){
        int n = s.length();
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        int len;
        HashMap<String, Boolean> map = new HashMap<>();
        for(String word: dic){
            len = word.length();
            min = Math.min(min, len);
            max = Math.max(max, len);
            map.put(word, true);
        }

        boolean[] dp = new boolean[n+1];
        dp[0] = true;
        ArrayList<String>[] list = new ArrayList[n+1];
        for(int i=1; i<=n; i++){
            int gap;
            String suffix;
            for(int j=i-1; j>=0; j--){
                gap = i-j;
                if(gap < min){
                    continue;
                }
                if(max < gap){
                    break;
                }
                suffix = s.substring(j, i);
                if(dp[j] && map.getOrDefault(suffix, false)){
                    dp[i] = true;
                    if(list[i] == null){
                        list[i] = new ArrayList<String>();
                    }
                    if(list[j]!=null && list[j].size() > 0){
                        for(String part: list[j]){
                            list[i].add(part + " " + suffix);
                        }
                    }else{
                        list[i].add(suffix);
                    }
                }
            }
        }

        int size = 0;
        if(list[n] != null){
            size = list[n].size();
        }

        String[] result = new String[size];
        for(int i=0; i<size; i++){
            result[i] = list[n].get(i);
        }

        return result;
    }



    /**
     * 动态规划: 简化
     *
     * dp[i]表示字符串s前i个字符组成的字符串的所有拆分方案
     *
     * 判断是否可拆分
     * dp[j]!=null && map.getOrDefault(suffix, false)  , 0<=j<i
     * check(s[j..i−1]) => map.getOrDefault(suffix, false)
     * 其中 check(s[j..i−1]) 表示子串s[j..i−1]是否出现在字典中
     *
     * @param s
     * @param dic
     * @return
     */
    private String[] solution2(String s, String[] dic){
        int n = s.length();
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        int len;
        HashMap<String, Boolean> map = new HashMap<>();
        for(String word: dic){
            len = word.length();
            min = Math.min(min, len);
            max = Math.max(max, len);
            map.put(word, true);
        }

        ArrayList<String>[] dp = new ArrayList[n+1];
        dp[0] = new ArrayList<>();
        for(int i=1; i<=n; i++){
            int gap;
            String suffix;
            for(int j=i-1; j>=0; j--){
                gap = i-j;
                if(gap < min){
                    continue;
                }
                if(max < gap){
                    break;
                }
                suffix = s.substring(j, i);
                if(dp[j]!=null && map.getOrDefault(suffix, false)){
                    if(dp[i] == null){
                        dp[i] = new ArrayList<>();
                    }
                    if(dp[j]!=null && dp[j].size() > 0){
                        for(String part: dp[j]){
                            dp[i].add(part + " " + suffix);
                        }
                    }else{
                        dp[i].add(suffix);
                    }
                }
            }
        }

        int size = 0;
        if(dp[n] != null){
            size = dp[n].size();
        }

        String[] result = new String[size];
        for(int i=0; i<size; i++){
            result[i] = dp[n].get(i);
        }

        return result;
    }



    /**
     * dfs: 字典树Trie
     * @param s
     * @param dic
     * @return
     */
    private String[] solution3(String s, String[] dic){
        Trie root = new Trie();
        for(String word: dic){
            root.insert(word);
        }

        len = s.length();
        for(int i=1; i<=len; i++){
            dfs(s, root, 0, i, "");
        }

        String[] result = new String[list.size()];
        for(int i=0; i<list.size(); i++){
            result[i] = list.get(i);
        }

        return result;
    }

    /**
     * 递归
     * @param s
     * @param root
     * @param i
     * @param j
     * @param result
     */
    private void dfs(String s, Trie root, int i, int j, String result){
        String sub = s.substring(i, j);
        if(root.search(sub)){
            if(j == len){
                list.add(result+sub);
            }else{
                String pre = s.substring(j, j+1);
                if(root.prefixNumber(pre) > 0){
                    for(int k=j+1; k<=len; k++){
                        dfs(s, root, j, k, result+sub+" ");
                    }
                }
            }
        }
    }

    /**
     * 字典树Trie
     */
    private class Trie {
        private Trie[] children;
        boolean isEnd;
        private int count;

        public Trie(){
            children = new Trie[75];
            isEnd = false;
            count = 0;
        }

        public void insert(String word){
            Trie curr = this;
            int index;
            for(char ch: word.toCharArray()){
                index = ch - '0';
                if(curr.children[index] == null){
                    curr.children[index] = new Trie();
                }
                curr = curr.children[index];
                curr.count++;
            }
            curr.isEnd = true;
        }

        public void delete(String word){
            Trie curr = this;
            int index;
            for(char ch: word.toCharArray()){
                index = ch - '0';
                if(curr.children[index] != null){
                    curr = curr.children[index];
                    curr.count--;
                }
            }
            if(curr.count == 0){
                curr.isEnd = false;
            }
        }

        public boolean search(String word){
            Trie curr = this;
            int index;
            for(char ch: word.toCharArray()){
                index = ch - '0';
                if(curr.children[index] == null){
                    return false;
                }
                curr = curr.children[index];
            }
            if(!curr.isEnd){
                return false;
            }

            return true;
        }

        public int prefixNumber(String pre){
            Trie curr = this;
            int index;
            for(char ch: pre.toCharArray()){
                index = ch - '0';
                if(curr.children[index] == null){
                    return 0;
                }
                curr = curr.children[index];
            }

            return curr.count;
        }
    }



    /**
     * dfs: HashSet
     * @param s
     * @param dic
     * @return
     */
    private String[] solution4(String s, String[] dic){
        len = s.length();
        for(String word: dic){
            set.add(word);
        }

        dfs(s, 0, "");

        String[] result = new String[list.size()];
        for(int i=0; i<list.size(); i++){
            result[i] = list.get(i).trim();
        }

        return result;
    }

    /**
     * 递归
     * @param s
     * @param i
     * @param result
     */
    private void dfs(String s, int i, String result){
        if(i == len){
            list.add(result);
        }

        String sub = "";
        // for(int j=i; j<len; j++){
        //     sub += s.charAt(j);
        //     if(set.contains(sub)){
        //         dfs(s, j+1, result+sub+" ");
        //     }
        // }
        for(int j=i+1; j<=len; j++){
            sub = s.substring(i, j);
            if(set.contains(sub)){
                dfs(s, j, result+sub+" ");
            }
        }
    }
}
```
