# java-HJ65 查找两个字符串a,b中的最长公共子串


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            while (in.hasNext()){
                String a = in.nextLine();
                String b = in.nextLine();
    
                if(a.length() <= b.length()){
                    solution1(a, b);
                    // solution2(a, b);
                }else{
                    solution1(b, a);
                    // solution2(b, a);
                }
            }
        }
    
        /**
         * 滑动窗口
         * @param shortStr
         * @param longStr
         */
        private static void solution1(String shortStr, String longStr){
    
            int window = shortStr.length();
            boolean found = false;
            for(int i=window; i>0; i--){
                if(found){
                    break;
                }
                for(int j=0; j+i<=window; j++){
                    String subStr = shortStr.substring(j, j+i);
                    if(longStr.contains(subStr)){
                        System.out.println(subStr);
                        found = true;
                        break;
                    }
                }
            }
        }
    
    
        /**
         * 动态规划 dp[i][j]表示在较短字符串shortStr中以第i个字符结尾，较长字符串longStr中以第j个字符结尾时的公共子串长度
         * @param shortStr
         * @param longStr
         */
        private static void solution2(String shortStr, String longStr){
    
            int shortLen = shortStr.length();
            int longLen = longStr.length();
            int[][] dp =  new int[shortLen+1][longLen+1];
    
            int maxSub = 0;
            int index = 0;
            for(int i=1; i<=shortLen; i++){
                for(int j=1; j<=longLen; j++){
                    if(shortStr.charAt(i-1) == longStr.charAt(j-1)){
                        dp[i][j] = dp[i-1][j-1]+1;
                        if(dp[i][j] > maxSub){
                            maxSub = dp[i][j];
                            index = i;
                        }
                    }
                }
            }
    
            System.out.println(shortStr.substring(index-maxSub, index));
        }
    }

  

