# java-HJ52 计算字符串的编辑距离


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            while (in.hasNext()){
                String A = in.nextLine();
                String B = in.nextLine();
    
                solution(A, B);
            }
        }
    
        /**
         * 动态规划: dp[i][j]表示字符串A的前i个字符与字符串B的前j个字符相同所需要的编辑距离
         * @param A
         * @param B
         */
        private static void solution(String A, String B){
            int ALen = A.length();
            int BLen = B.length();
    
            int[][] dp = new int[ALen+1][BLen+1];
    
            // 初始化
            for(int i=0; i<=ALen; i++){
                dp[i][0] = i;
            }
            for(int j=0; j<=BLen; j++){
                dp[0][j] = j;
            }
    
            for(int i=1; i<=ALen; i++){
                for(int j=1; j<=BLen; j++){
                    // case 1
                    if(A.charAt(i-1) == B.charAt(j-1)){
                        dp[i][j] = dp[i-1][j-1];
                    }
                    // case 2
                    else{
                        dp[i][j] = Math.min(Math.min(dp[i-1][j]+1, dp[i][j-1]+1), dp[i-1][j-1]+1);
                    }
                }
            }
    
            System.out.println(dp[ALen][BLen]);
        }
    }

  

