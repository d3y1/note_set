# java-NC362 字典序排列


    import java.util.*;
    
    /**
     * NC362 字典序排列
     * @author d3y1
     */
    public class Solution {
        ArrayList<Integer> list = new ArrayList<>();
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param n int整型
         * @return int整型ArrayList
         */
        public ArrayList<Integer> orderArray (int n) {
            // return solution1(n);
            // return solution2(n);
            // return solution3(n);
            // return solution33(n);
            return solution4(n);
        }
    
        /**
         * 迭代
         * @param n
         * @return
         */
        private ArrayList<Integer> solution1(int n){
            int num = 1;
            // i: 插入次数(也即正整数个数)
            for(int i=1; i<=n; i++){
                list.add(num);
                if(num*10 <= n){
                    num = num*10;
                }else{
                    // test case: 20
                    while(num%10==9 || num+1>n){
                        num = num/10;
                    }
                    num = num+1;
                }
            }
    
            return list;
        }
    
        /**
         * 小根堆
         * @param n
         * @return
         */
        private ArrayList<Integer> solution2(int n){
            PriorityQueue<Integer> minHeap = new PriorityQueue<>(Comparator.comparing(String::valueOf));
    
            // 小根堆: 按字典序排序
            for(int num=1; num<=n; num++){
                minHeap.offer(num);
            }
    
            while(!minHeap.isEmpty()){
                list.add(minHeap.poll());
            }
    
            return list;
        }
    
        /**
         * 递归
         * @param n
         * @return
         */
        private ArrayList<Integer> solution3(int n){
            for(int i=1; i<=9; i++){
                dfs(i, n);
            }
            return list;
        }
    
        private void dfs(int num, int n){
            if(num > n){
                return;
            }
    
            list.add(num);
    
            for(int i=0; i<=9; i++){
                dfs(num*10+i, n);
            }
        }
    
        /**
         * 递归: 优化
         * @param n
         * @return
         */
        private ArrayList<Integer> solution33(int n){
            for(int i=1; i<=9; i++){
                DFS(i, n);
            }
            return list;
        }
    
        private boolean DFS(int num, int n){
            if(num > n){
                return false;
            }
    
            list.add(num);
    
            for(int i=0; i<=9; i++){
                if(!DFS(num*10+i, n)){
                    break;
                }
            }
    
            return true;
        }
    
        /**
         * Trie(字典树/前缀树)
         * @param n
         * @return
         */
        private ArrayList<Integer> solution4(int n){
            Trie trie = new Trie();
            for(int num=1; num<=n; num++){
                trie.insert(String.valueOf(num));
            }
    
            preOrder(trie, "");
    
            return list;
        }
    
        /**
         * 递归: 类似树的前序遍历
         * @param trie
         * @param num
         */
        private void preOrder(Trie trie, String num){
            if(trie == null){
                return;
            }
    
            if(trie.isEnd){
                list.add(Integer.parseInt(num));
            }
    
            for(int i=0; i<=9; i++){
                preOrder(trie.children[i], num+i);
            }
        }
    
        /**
         * Trie类
         */
        private class Trie {
            private Trie[] children;
            private boolean isEnd;
    
            public Trie(){
                this.children = new Trie[10];
                this.isEnd = false;
            }
    
            public void insert(String num){
                Trie curr = this;
                int idx;
                for(char digit: num.toCharArray()){
                    idx = digit-'0';
                    if(curr.children[idx] == null){
                        curr.children[idx] = new Trie();
                    }
                    curr = curr.children[idx];
                }
                curr.isEnd = true;
            }
        }
    }

  

