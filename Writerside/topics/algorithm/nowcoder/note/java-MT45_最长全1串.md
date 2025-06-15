# java-MT45 最长全1串


    import java.util.Scanner;
    
    public class Main {
        private static int n;
        private static int k;
        private static int[] nums;
        private static int[] sum;
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution1(in);
                solution2(in);
                solution3(in);
            }
        }
    
        /**
         * 滑动窗口 + 双指针
         * @param in
         */
        private static void solution1(Scanner in){
            n = in.nextInt();
            k = in.nextInt();
    
            nums = new int[n];
    
            int i, j, zeros=0;
            for(i=0,j=0; j<n; j++){
                nums[j] = in.nextInt();
                if(nums[j] == 0){
                    zeros++;
                }
                if(zeros>k && nums[i++]==0){
                    zeros--;
                }
            }
    
            System.out.println(j-i);
        }
    
        /**
         * 动态规划
         * f[x] = i
         * f[x]表示第x个0在字符串中的位置为i
         * @param in
         */
        private static void solution2(Scanner in){
            n = in.nextInt();
            k = in.nextInt();
    
            int num, zeros=0, result=0;
            int[] f = new int[n+1];
            for(int i=0; i<n; i++){
                num = in.nextInt();
                if(num == 0){
                    f[++zeros] = i;
                }
                if(zeros <= k){
                    result = Math.max(result, i+1);
                }else{
                    result = Math.max(result, i-f[zeros-k]);
                }
            }
    
            System.out.println(result);
        }
    
        /**
         * 二分法 + 数组
         * @param in
         */
        private static void solution3(Scanner in){
            n = in.nextInt();
            k = in.nextInt();
    
            nums = new int[n+1];
            sum = new int[n+1];
    
            for(int i=1; i<=n; i++){
                nums[i] = in.nextInt();
                sum[i] = sum[i-1]+nums[i];
            }
    
            int l = 0;
            int r = n;
            while(l <= r){
                int mid = (l+r)>>1;
                if(!isOk(mid)) {
                    r = mid-1;
                }else{
                    l = mid+1;
                }
            }
    
            System.out.println(r);
        }
    
        /**
         * 当前区间可否全为1
         * @param gap
         * @return
         */
        private static boolean isOk(int gap){
            int zeros;
            for(int j=0; j+gap<=n; j++){
                zeros = gap-(sum[j+gap]-sum[j]);
                if(k >= zeros){
                    return true;
                }
            }
    
            return false;
        }
    }

  

