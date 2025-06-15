# java-ZJ2 编程题1


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution1(in);
                solution2(in);
            }
        }
    
        /**
         * 数学法: 分4种情况解方程组
         *
         * 最终情况只能是每队得分: n/3
         * s1: 球队1当前得分 s2: 球队2当前得分 s3: 球队3当前得分
         * |s1-s2| = d1
         * |s2-s3| = d2
         * s1+s2+s3 = k
         *
         * @param in
         */
        private static void solution1(Scanner in){
            int lines = in.nextInt();
            for(int i=1; i<=lines; i++){
                long n = in.nextLong();
                long k = in.nextLong();
                long d1 = in.nextLong();
                long d2 = in.nextLong();
    
                // 比赛场数不为3的倍数
                if(n%3 != 0){
                    System.out.println("no");
                }
                // 比分差额大于n/3
                else if(d1>n/3 || d2>n/3){
                    System.out.println("no");
                }else if(check(n, k, d1, d2) || check(n, k, -d1, d2) || check(n, k, d1, -d2) || check(n, k, -d1, -d2)){
                    System.out.println("yes");
                }else{
                    System.out.println("no");
                }
            }
        }
    
        /**
         * check: 4种情况代码相同 通用简化
         *
         * |s1-s2| = d1
         * |s3-s2| = d2
         * s1+s2+s3 = k
         *
         * @param n
         * @param k
         * @param d1
         * @param d2
         * @return
         */
        private static boolean check(long n, long k, long d1, long d2){
            if((k-d1-d2)%3 != 0){
                return false;
            }
    
            long s2 = (k-d1-d2)/3;
            long s1 = s2+d1;
            long s3 = s2+d2;
    
            if((0<=s1&&s1<=n/3) && (0<=s2&&s2<=n/3) && (0<=s3&&s3<=n/3)){
                return true;
            }else{
                return false;
            }
        }
    
        /**
         * 数学法: 分4种情况解方程组
         *
         * 最终情况只能是每队得分: n/3
         * s1: 球队1当前得分 s2: 球队2当前得分 s3: 球队3当前得分
         * |s1-s2| = d1
         * |s2-s3| = d2
         * s1+s2+s3 = k
         *
         * @param in
         */
        private static void solution2(Scanner in){
            int lines = in.nextInt();
            for(int i=1; i<=lines; i++){
                long n = in.nextLong();
                long k = in.nextLong();
                long d1 = in.nextLong();
                long d2 = in.nextLong();
    
                // 比赛场数不为3的倍数
                if(n%3 != 0){
                    System.out.println("no");
                }
                // 比分差额大于n/3
                else if(d1>n/3 || d2>n/3){
                    System.out.println("no");
                }else if(case1(n, k, d1, d2) || case2(n, k, d1, d2) || case3(n, k, d1, d2) || case4(n, k, d1, d2)){
                    System.out.println("yes");
                }else{
                    System.out.println("no");
                }
            }
        }
    
        /**
         * case1
         *
         * s1-s2 = d1
         * s3-s2 = d2
         * s1+s2+s3 = k
         *
         * @param n
         * @param k
         * @param d1
         * @param d2
         * @return
         */
        private static boolean case1(long n, long k, long d1, long d2){
            if((k-d1-d2)%3 != 0){
                return false;
            }
    
            long s2 = (k-d1-d2)/3;
            long s1 = s2+d1;
            long s3 = s2+d2;
    
            if((0<=s1&&s1<=n/3) && (0<=s2&&s2<=n/3) && (0<=s3&&s3<=n/3)){
                return true;
            }else{
                return false;
            }
        }
    
        /**
         * case2
         *
         * s1-s2 = d1
         * s2-s3 = d2
         * s1+s2+s3 = k
         *
         * @param n
         * @param k
         * @param d1
         * @param d2
         * @return
         */
        private static boolean case2(long n, long k, long d1, long d2){
            if((k-d1+d2)%3 != 0){
                return false;
            }
    
            long s2 = (k-d1+d2)/3;
            long s1 = s2+d1;
            long s3 = s2-d2;
    
            if((0<=s1&&s1<=n/3) && (0<=s2&&s2<=n/3) && (0<=s3&&s3<=n/3)){
                return true;
            }else{
                return false;
            }
        }
    
        /**
         * case3
         *
         * s2-s1 = d1
         * s3-s2 = d2
         * s1+s2+s3 = k
         *
         * @param n
         * @param k
         * @param d1
         * @param d2
         * @return
         */
        private static boolean case3(long n, long k, long d1, long d2){
            if((k+d1-d2)%3 != 0){
                return false;
            }
    
            long s2 = (k+d1-d2)/3;
            long s1 = s2-d1;
            long s3 = s2+d2;
    
            if((0<=s1&&s1<=n/3) && (0<=s2&&s2<=n/3) && (0<=s3&&s3<=n/3)){
                return true;
            }else{
                return false;
            }
        }
    
        /**
         * case4
         *
         * s2-s1 = d1
         * s2-s3 = d2
         * s1+s2+s3 = k
         *
         * @param n
         * @param k
         * @param d1
         * @param d2
         * @return
         */
        private static boolean case4(long n, long k, long d1, long d2){
            if((k+d1+d2)%3 != 0){
                return false;
            }
    
            long s2 = (k+d1+d2)/3;
            long s1 = s2-d1;
            long s3 = s2-d2;
    
            if((0<=s1&&s1<=n/3) && (0<=s2&&s2<=n/3) && (0<=s3&&s3<=n/3)){
                return true;
            }else{
                return false;
            }
        }
    }

  

