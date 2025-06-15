# java-NC175 合法的括号字符串


    import java.util.*;
    
    /**
     * NC175 合法的括号字符串
     * @author d3y1
     */
    public class Solution {
         /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param s string字符串
         * @return bool布尔型
         */
        public boolean isValidString (String s) {
            // return solution1(s);
            return solution2(s);
            // return solution3(s);
        }
    
        /**
         * 栈
         * @param s
         * @return
         */
        private boolean solution1(String s){
            Stack<Integer> leftStack = new Stack<>();
            Stack<Integer> starStack = new Stack<>();
    
            char ch;
            for(int i=0; i<s.length(); i++){
                ch = s.charAt(i);
                if(ch == '('){
                    leftStack.push(i);
                }
                else if(ch == '*'){
                    starStack.push(i);
                }
                else if(ch == ')'){
                    if(!leftStack.isEmpty()){
                        leftStack.pop();
                    }else if(!starStack.isEmpty()){
                        starStack.pop();
                    }else{
                        return false;
                    }
                }
            }
    
            while(!leftStack.isEmpty()){
                if(!starStack.isEmpty() && leftStack.peek()<starStack.peek()){
                    leftStack.pop();
                    starStack.pop();
                }else{
                    return false;
                }
            }
    
            return true;
        }
    
        /**
         * 贪心
         * @param s
         * @return
         */
        private boolean solution2(String s){
            // 待消除左括号的最小个数
            int minLeft = 0;
            // 待消除左括号的最大个数
            int maxLeft = 0;
    
            for(char ch: s.toCharArray()){
                if(ch == '('){
                    minLeft++;
                    maxLeft++;
                }
                else if(ch == '*'){
                    // * -> )
                    if(minLeft > 0){
                        minLeft--;
                    }
                    // * -> (
                    maxLeft++;
                }
                else if(ch == ')'){
                    if(minLeft > 0){
                        minLeft--;
                    }
                    // 已经没有'('或'*'与当前')'匹配
                    if(maxLeft == 0){
                        return false;
                    }
                    maxLeft--;
                }
            }
    
            return minLeft==0;
        }
    
        /**
         * 动态规划
         *
         * dp[i][j]表示子串s[i,j]是否为合法的括号字符串
         * 
         * len=1:
         * dp[i][i] = true , s.charAt(i) == '*'
         * 
         * len=2:
         * dp[i][i+1] = true , (currCh=='('||currCh=='*') && (nextCh==')'||nextCh=='*')
         * 
         * len>=3:
         * dp[i][j] = dp[i+1][j-1] , (leftCh=='('||leftCh=='*') && (rightCh==')'||rightCh=='*')
         * dp[i][j] = dp[i][k]&&dp[k+1][j] , i<=k<j&&!dp[i][j]
         * 
         * @param s
         * @return
         */
        private boolean solution3(String s){
            int n = s.length();
    
            boolean[][] dp = new boolean[n][n];
    
            // len=1 -> *
            for(int i=0; i<n; i++){
                if(s.charAt(i) == '*'){
                    dp[i][i] = true;
                }
            }
    
            // len=2 -> () (* *) **
            char currCh,nextCh;
            for(int i=0; i+1<n; i++){
                currCh = s.charAt(i);
                nextCh = s.charAt(i+1);
                if((currCh=='('||currCh=='*') && (nextCh==')'||nextCh=='*')){
                    dp[i][i+1] = true;
                }
            }
    
            // len>=3
            char leftCh,rightCh;
            for(int i=n-3; i>=0; i--){
                for(int j=i+2; j<n; j++){
                    leftCh = s.charAt(i);
                    rightCh = s.charAt(j);
                    // (())
                    if((leftCh=='('||leftCh=='*') && (rightCh==')'||rightCh=='*')){
                        dp[i][j] = dp[i+1][j-1];
                    }
                    // ()()
                    for(int k=i; k<j&&!dp[i][j]; k++){
                        dp[i][j] = dp[i][k]&&dp[k+1][j];
                    }
                }
            }
    
            return dp[0][n-1];
        }
    }

  

