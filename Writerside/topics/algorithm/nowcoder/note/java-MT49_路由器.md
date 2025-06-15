# java-MT49 路由器


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 差分数组
         *
         * 原数组[a1, a2, a3, a4, ...]
         * 差分数组[a1, a2-a1, a3-a2, a4-a3, ...]
         * 原数组第i项的值等于差分数组前i项的和
         *
         * 假如需要在区间[i,j]范围内都进行+1操作
         * 对于原数组, 需要遍历第i到j项都进行+1, 时间复杂度大
         * 对于差分数组, 只需在第i项+1, 第j+1项-1就行, 时间复杂度小
         *
         * @param in
         */
        private static void solution(Scanner in){
            int n = in.nextInt();
            int k = in.nextInt();
    
            int[] routers = new int[n];
            for(int i=0; i<n; i++){
                routers[i] = in.nextInt();
            }
    
            // 差分数组
            int[] diff = new int[n+1];
            int left,right;
            for(int i=0; i<n; i++){
                left = Math.max(0, i-routers[i]);
                right = Math.min(n, i+routers[i]+1);
                diff[left]++;
                diff[right]--;
            }
    
            int result = 0;
            int[] sum = new int[n];
            for(int i=0; i<n; i++){
                if(i > 0){
                    sum[i] = sum[i-1] + diff[i];
                }else{
                    sum[i] = diff[0];
                }
                if(sum[i] >= k){
                    result++;
                }
            }
    
            System.out.println(result);
        }
    }

  

