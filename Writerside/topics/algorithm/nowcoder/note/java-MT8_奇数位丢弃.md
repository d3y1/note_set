# java-MT8 奇数位丢弃


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution1(in);
                solution2(in);
                solution3(in);
                solution4(in);
            }
        }
    
        /**
         * 数学公式法
         * @param in
         */
        private static void solution1(Scanner in){
            int n = in.nextInt();
    
            int pow = (int)Math.floor(Math.log(n)/Math.log(2));
    
            int pos = 1<<pow;
            int num = pos-1;
    
            System.out.println(num);
        }
    
        /**
         * 二进制移位法
         * @param in
         */
        private static void solution2(Scanner in){
            int n = in.nextInt();
    
            int index = 1;
            while(index <= n){
                index <<= 1;
            }
    
            int pos = index>>1;
            int num = pos-1;
    
            System.out.println(num);
        }
    
        /**
         * 数学法
         *
         * pos  1  2  3  4  5  6  7  8  9  10 11  12  13  14  15  16  17
         * num  0  1  2  3  4  5  6  7  8  9  10  11  12  13  14  15  16
         * num  1  3  5  7  9  11 13 15
         * num  3  7  11 15
         * num  7  15
         * num  15
         * 
         * 观上可知:
         * 每轮最开始的数num依次为 0 1 3 7 15, 对应的pos依次为 1 2 4 8 16, 即 2^0 2^1 2^2 2^3 2^4
         * 
         * @param in
         */
        private static void solution3(Scanner in){
            int n = in.nextInt();
    
            int index = 1;
            while(index <= n){
                index *= 2;
            }
    
            int pos = index/2;
            int num = pos-1;
    
            System.out.println(num);
        }
    
        /**
         * 数组: 删除奇数位等价于保留偶数位
         * @param in
         */
        private static void solution4(Scanner in){
            int n = in.nextInt();
    
            int[] nums = new int[n+1];
            for(int i=0; i<=n; i++){
                nums[i] = i;
            }
    
            int len = nums.length;
            while(len != 1){
                int k = 0;
                for(int i=1; i<len; i+=2){
                    nums[k++] = nums[i];
                }
                len = k;
            }
    
            System.out.println(nums[0]);
        }
    }

  

