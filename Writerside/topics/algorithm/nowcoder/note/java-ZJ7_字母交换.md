# java-ZJ7 字母交换


    import java.util.ArrayList;
    import java.util.HashMap;
    import java.util.List;
    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 动态规划
         * 
         * dp[i][j]表示使字符串中从第i个a到第j个a(共j-i+1个a)位置连续时需要进行的最少交换次数(以a为例)
         * 为了得到最少交换次数, 应该使用的移动策略: 从两边到中间
         * dp[i][j] = dp[i+1][j-1] + (pos(j)-pos(i)) - (j-i)
         * 
         * 推导过程:
         * dp[i][j] = dp[i+1][j-1] + (pos(i+1)-pos(i)-1) + (pos(j)-pos(j-1)-1) + [(pos(j-1)-pos(i+1)+1) - (j-i-1)]
         *          = dp[i+1][j-1] + (pos(j)-pos(i)) - (j-i)
         *          
         * 示例:
         * letters    a  b  a  c  d  a  f  f  a  b
         * posList    0  1  2  3  4  5  6  7  8  9
         * i    j     0     1        2        3
         * 
         * i=0 j=3
         * dp[0][3] = dp[1][2] + (pos(1)-pos(0)-1) + (pos(3)-pos(2)-1) + [(pos(2)-pos(1)+1) - (3-0-1)]
         *          = 2 + (2-0-1) + (8-5-1) + [(5-2+1) - (3-0-1)]
         *          = 2 + 1 + 2 + 4 - 2
         *          = 7
         * dp[0][3] = dp[1][2] + (pos(3)-pos(0)) - (3-0)
         *          = 2 + (8-0) - (3-0)
         *          = 2 + 8 - 3
         *          = 7
         * 
         * @param in
         */
        private static void solution(Scanner in){
            String letters = in.next();
            int m = in.nextInt();
    
            // 记录同一字母的不同位置index
            HashMap<Character, List<Integer>> letterMap = new HashMap<>();
            for(int i=0; i<letters.length(); i++){
                char letter = letters.charAt(i);
                List<Integer> list = letterMap.getOrDefault(letter, new ArrayList<>());
                list.add(i);
                letterMap.put(letter, list);
            }
    
            int result = 1;
            for(List<Integer> posList: letterMap.values()){
                int size = posList.size();
                // 该字母总数小于等于结果
                if(size <= result){
                    continue;
                }
                
                int[][] dp = new int[size][size];
                for(int interval=1; interval<size; interval++){
                    for(int i=0; i+interval<size; i++){
                        int j = i+interval;
                        dp[i][j] = dp[i+1][j-1]+(posList.get(j)-posList.get(i))-interval;
                        if(dp[i][j] <= m){
                            result = Math.max(result, j-i+1);
                        }
                    }
                }
            }
    
            System.out.println(result);
        }
    }

  

