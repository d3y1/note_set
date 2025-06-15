# java-NC327 取数游戏


    import java.util.*;
    
    /**
     * NC327 取数游戏
     * @author d3y1
     */
    public class Solution {
        private int result;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param A int整型ArrayList
         * @param B int整型ArrayList
         * @return int整型
         */
        public int numbergame (ArrayList<Integer> A, ArrayList<Integer> B) {
            // return solution1(A, B);
            return solution2(A, B);
        }
    
        /**
         * dfs: 遍历空间: 超时
         * @param A
         * @param B
         * @return
         */
        private int solution1(ArrayList<Integer> A, ArrayList<Integer> B){
            int n = A.size();
    
            dfs(A, B, 0, n-1, 0, 0, 0);
    
            return result;
        }
    
        /**
         * dfs: 递归
         * @param A
         * @param B
         * @param left
         * @param right
         * @param direction
         * @param sum
         * @param index
         */
        private void dfs(ArrayList<Integer> A, ArrayList<Integer> B, int left, int right, int direction, int sum, int index){
            if(direction == 1){
                sum += A.get(left) * B.get(index);
                left++;
                index++;
                if(left > right){
                    result = Math.max(result, sum);
                    return;
                }
            }
            if(direction == -1){
                sum += A.get(right) * B.get(index);
                right--;
                index++;
                if(left > right){
                    result = Math.max(result, sum);
                    return;
                }
            }
    
            dfs(A, B, left, right, 1, sum, index);
            dfs(A, B, left, right, -1, sum, index);
        }
    
        /**
         * 动态规划
         *
         * dp[i][j]表示区间[i,j]可以取得的最大价值
         *
         * len表示区间[i,j]长度, 亦即剩余取数次数(总共n次)
         * len = j-i+1
         *
         * n-len表示下次取数时对应的价值索引(0到n-1, 递增)
         * 
         *            { A.get(i)*B.get(n-len)                                                         , i=j
         * dp[i][j] = {
         *            { Math.max(dp[i+1][j]+A.get(i)*B.get(n-len), dp[i][j-1]+A.get(j)*B.get(n-len))  , i<j
         *
         * @param A
         * @param B
         * @return
         */
        private int solution2(ArrayList<Integer> A, ArrayList<Integer> B){
            int n = A.size();
    
            int[][] dp = new int[n][n];
    
            int len;
            // 左边界i 降序
            for(int i=n-1; i>=0; i--){
                // 右边界j 升序
                for(int j=i; j<n; j++){
                    len = j-i+1;
                    if(i == j){
                        dp[i][j] = A.get(i)*B.get(n-len);
                    }else{
                        // dp[i+1][j]+A.get(i)*B.get(n-len) 左边界i依赖于后面i+1(i<-i+1) 所以i应降序
                        // dp[i][j-1]+A.get(j)*B.get(n-len) 右边界j依赖于前面j-1(j-1->j) 所以j应升序
                        dp[i][j] = Math.max(dp[i+1][j]+A.get(i)*B.get(n-len), dp[i][j-1]+A.get(j)*B.get(n-len));
                    }
                }
            }
    
            return dp[0][n-1];
        }
    }

  

