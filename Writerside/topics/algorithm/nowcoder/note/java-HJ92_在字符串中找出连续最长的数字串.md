# java-HJ92 在字符串中找出连续最长的数字串


    import java.util.ArrayList;
    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution1(in);
                // solution2(in);
            }
        }
    
    
        /**
         * 动态规划: dp[i]表示当前局部数字子串长度
         * @param in
         */
        private static void solution1(Scanner in){
            String input = in.nextLine();
    
            int len = input.length();
            int[] dp = new int[len+1];
    
            int max = 0;
            for(int i=1; i<=len; i++){
                char ch = input.charAt(i-1);
                if(Character.isDigit(ch)){
                    dp[i] = dp[i-1] + 1;
                    if(max < dp[i]){
                        max = dp[i];
                    }
                }
            }
    
            for(int i=1; i<=len; i++){
                if(dp[i] == max){
                    System.out.print(input.substring(i-max, i));
                }
            }
    
            System.out.println(","+max);
        }
    
    
        /**
         * 正则
         * @param in
         */
        private static void solution2(Scanner in){
            String input = in.nextLine();
    
            String[] digitParts = input.split("[^0-9]+");
            ArrayList<String> list = new ArrayList<>();
            int max = 0;
    
            for(String part: digitParts){
                if(max < part.length()){
                    max = part.length();
                    list.clear();
                    list.add(part);
                }else if(max == part.length()){
                    list.add(part);
                }
            }
    
            StringBuilder sb = new StringBuilder();
            for(String maxPart: list){
                sb.append(maxPart);
            }
            sb.append(","+max);
    
            System.out.println(sb);
        }
    }

  

