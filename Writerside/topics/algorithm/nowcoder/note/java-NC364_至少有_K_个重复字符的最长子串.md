# java-NC364 至少有 K 个重复字符的最长子串

```java
import java.util.*;

/**
 * NC364 至少有 K 个重复字符的最长子串
 * @author d3y1
 */
public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     *
     * @param s string字符串
     * @param k int整型
     * @return int整型
     */
    public int longestSubstring (String s, int k) {
        // return solution1(s, k);
        // return solution2(s, k);
        // return solution22(s, k);
        // return solution3(s, k);
        return solution33(s, k);
    }

    /**
     * 滑动窗口
     * @param s
     * @param k
     * @return
     */
    private int solution1(String s, int k){
        int len = s.length();
        if(k == 1){
            return len;
        }
        if(len < k){
            return 0;
        }

        // 可能的最大窗口
        int max = 0;
        int[] cnt = new int[26];
        for(char ch: s.toCharArray()){
            cnt[ch-'a']++;
        }
        for(int i=0; i<26; i++){
            if(cnt[i] >= k){
                max += cnt[i];
            }
        }

        // 滑动窗口
        for(int gap=max; gap>=k; gap--){
            for(int i=0; i+gap<=len; i++){
                if(isValid(s.substring(i, i+gap), k)){
                    return gap;
                }
            }
        }

        return 0;
    }

    /**
     * 子串是否合法
     * @param sub
     * @param k
     * @return
     */
    private boolean isValid(String sub, int k){
        int[] cnt = new int[26];
        for(char ch: sub.toCharArray()){
            cnt[ch-'a']++;
        }

        for(int i=0; i<26; i++){
            if(0<cnt[i] && cnt[i]<k){
                return false;
            }
        }

        return true;
    }

    /**
     * 分治法
     * @param s
     * @param k
     * @return
     */
    private int solution2(String s, int k){
        return divide(s, k);
    }

    /**
     * 递归
     * @param s
     * @param k
     * @return
     */
    private int divide(String s, int k){
        int len = s.length();
        if(k == 1){
            return len;
        }
        if(len < k){
            return 0;
        }

        // 哈希
        HashMap<Character, Integer> map = new HashMap<>();
        for(char ch: s.toCharArray()){
            map.put(ch, map.getOrDefault(ch, 0)+1);
        }

        for(char ch: s.toCharArray()){
            if(map.get(ch) < k){
                int maxLen = 0;
                for(String part: s.split(String.valueOf(ch))){
                    maxLen = Math.max(maxLen, divide(part, k));
                }
                return maxLen;
            }
        }

        return s.length();
    }

    /**
     * 分治法
     * @param s
     * @param k
     * @return
     */
    private int solution22(String s, int k){
        return dfs(s, k);
    }

    /**
     * 递归
     * @param s
     * @param k
     * @return
     */
    private int dfs(String s, int k){
        int len = s.length();
        if(k == 1){
            return len;
        }
        if(len < k){
            return 0;
        }

        // 哈希
        int[] cnt = new int[26];
        for(char ch: s.toCharArray()){
            cnt[ch-'a']++;
        }

        for(char ch: s.toCharArray()){
            if(cnt[ch-'a'] < k){
                int maxLen = 0;
                for(String part: s.split(String.valueOf(ch))){
                    maxLen = Math.max(maxLen, divide(part, k));
                }
                return maxLen;
            }
        }

        return s.length();
    }

    /**
     * 双指针
     *
     * 相似 -> NC402 包含不超过两种字符的最长子串 [nowcoder]
     * 相似 -> NC41 最长无重复子数组            [nowcoder]
     * 相似 -> NC170 最长不含重复字符的子字符串   [nowcoder]
     * 相似 -> NC356 至多包含K种字符的子串       [nowcoder]
     * 相似 -> NC387 找到字符串中的异位词        [nowcoder]
     *
     * @param s
     * @param k
     * @return
     */
    private int solution3(String s, int k){
        int n = s.length();
        int result = 0;

        // 枚举最长子串的字符种数
        for(int kind=1; kind<=26; kind++){
            // 双指针 毛毛虫
            int left=0, right=0;
            // 滑动窗口内每种字符出现的次数统计
            int[] cnt = new int[26];
            // 滑动窗口内的字符种数
            int total = 0;
            // 滑动窗口内出现次数小于k的字符种数
            int remain = 0;
            char chL,chR;
            while(right < n){
                chR = s.charAt(right);
                cnt[chR-'a']++;
                if(cnt[chR-'a'] == 1){
                    total++;
                    remain++;
                }
                if(cnt[chR-'a'] == k){
                    remain--;
                }

                while(total > kind){
                    chL = s.charAt(left);
                    cnt[chL-'a']--;
                    if(cnt[chL-'a'] == k-1){
                        remain++;
                    }
                    if(cnt[chL-'a'] == 0){
                        total--;
                        remain--;
                    }
                    left++;
                }

                if(remain == 0){
                    result = Math.max(result, right-left+1);
                }

                right++;
            }
        }

        return result;
    }

    /**
     * 双指针
     *
     * 相似 -> NC402 包含不超过两种字符的最长子串 [nowcoder]
     * 相似 -> NC41 最长无重复子数组            [nowcoder]
     * 相似 -> NC170 最长不含重复字符的子字符串   [nowcoder]
     * 相似 -> NC356 至多包含K种字符的子串       [nowcoder]
     * 相似 -> NC387 找到字符串中的异位词        [nowcoder]
     *
     * @param s
     * @param k
     * @return
     */
    private int solution33(String s, int k){
        int n = s.length();
        int result = 0;

        HashSet<Character> set = new HashSet<>();
        for(char ch: s.toCharArray()){
            set.add(ch);
        }

        // 枚举最长子串的字符种数
        for(int kind=1; kind<=set.size(); kind++){
            // 双指针 毛毛虫
            int left=0, right=0;
            // 滑动窗口内每种字符出现的次数统计
            int[] cnt = new int[26];
            // 滑动窗口内的字符种数
            int total = 0;
            // 滑动窗口内出现次数小于k的字符种数
            int remain = 0;
            char chL,chR;
            while(right < n){
                chR = s.charAt(right);
                cnt[chR-'a']++;
                if(cnt[chR-'a'] == 1){
                    total++;
                    remain++;
                }
                if(cnt[chR-'a'] == k){
                    remain--;
                }

                while(total > kind){
                    chL = s.charAt(left);
                    cnt[chL-'a']--;
                    if(cnt[chL-'a'] == k-1){
                        remain++;
                    }
                    if(cnt[chL-'a'] == 0){
                        total--;
                        remain--;
                    }
                    left++;
                }

                if(remain == 0){
                    result = Math.max(result, right-left+1);
                }

                right++;
            }
        }

        return result;
    }
}
```
