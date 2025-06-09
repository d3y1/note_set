# 字典序第K小
https://www.nowcoder.com/practice/670c2bda374241d7ae06ade60de33e8b

    import java.util.*;
    
    /**
     * NC334 字典序第K小
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 类似 -> NC362 字典序排列 [nowcoder]
         *
         * @param n int整型
         * @param k int整型
         * @return int整型
         */
        public int findKth(int n, int k){
            // return solution1(n, k);
            return solution2(n, k);
        }
    
        private int seq = 0;
        private int ans = 0;
    
        /**
         * Trie(字典树/前缀树) - 超时!
         * @param n
         * @param k
         * @return
         */
        private int solution1(int n, int k){
            Trie trie = new Trie();
            for(int num=1; num<=n; num++){
                trie.insert(String.valueOf(num));
            }
    
            preorder(trie, "", k);
    
            return ans;
        }
    
        /**
         * 树的前序遍历
         * @param trie
         * @param num
         * @param k
         */
        private void preorder(Trie trie, String num, int k){
            if(seq >= k){
                return;
            }
            if(trie == null){
                return;
            }
    
            if(trie.isEnd){
                if(++seq == k){
                    ans = Integer.parseInt(num);
                    return;
                }
            }
    
            for(int i=0; i<=9; i++){
                preorder(trie.children[i], num+i, k);
            }
        }
    
        /**
         * Trie类
         */
        private class Trie {
            Trie[] children;
            boolean isEnd;
    
            public Trie(){
                children = new Trie[10];
                isEnd = false;
            }
    
            public void insert(String num){
                Trie cur = this;
                int idx;
                for(char digit: num.toCharArray()){
                    idx = digit-'0';
                    if(cur.children[idx] == null){
                        cur.children[idx] = new Trie();
                    }
                    cur = cur.children[idx];
                }
                cur.isEnd = true;
            }
        }
    
        /**
         * 模拟Trie(无需实际构造)
         * @param n
         * @param k
         * @return
         */
        private int solution2(int n, int k){
            // 当前数指针
            int cur = 1;
            k--;
    
            int cnt;
            while(k > 0){
                // 获取以当前数cur为根的树的所有节点数(包括当前数)
                cnt = cntNodes(cur, n);
                // 不在tree(cur)[以cur为根的树]中
                if(cnt <= k){
                    // 当前数指针 右移
                    cur++;
                    k -= cnt;
                }
                // 必在tree(cur)[以cur为根的树]中
                else{
                    // 当前数指针 下移
                    cur *= 10;
                    k--;
                }
            }
    
            return cur;
        }
    
        /**
         * 获取以当前数cur为根的树的所有节点数(包括当前数)
         * @param root
         * @param n
         * @return
         */
        private int cntNodes(int root, int n){
            int cnt = 0;
            long left = root;
            long right = root;
    
            while(left <= n){
                // 当前层的数目
                cnt += Math.min(right,n)-left+1;
                left = left*10;
                right = right*10+9;
            }
    
            return cnt;
        }
    }
    

