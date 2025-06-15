# java-MT39 被 7 整除


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 数学法: 拆分
         * 127 和 12
         * 12712 = 12700+12
         * @param in
         */
        private static void solution(Scanner in){
            int n = in.nextInt();
    
            int[] nums = new int[n];
            // 统计个数
            int[][] count = new int[11][7];
            for(int i=0; i<n; i++) {
                nums[i] = in.nextInt();
                count[String.valueOf(nums[i]).length()][nums[i]%7]++;
            }
    
            long result = 0L;
            for(int i=0; i<n; i++) {
                int bits = String.valueOf(nums[i]).length();
                int mod = nums[i]%7;
                // 排除当前数
                count[bits][mod]--;
                long num = nums[i];
                for(int j=1; j<=10; j++){
                    num *= 10;
                    int currMod = (int)(num%7);
                    result += count[j][(7-currMod)%7];
                }
                // 恢复当前数
                count[bits][mod]++;
            }
    
            System.out.println(result);
        }
    }

  

