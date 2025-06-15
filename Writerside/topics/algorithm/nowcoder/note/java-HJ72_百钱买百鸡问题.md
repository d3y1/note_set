# java-HJ72 百钱买百鸡问题


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        /**
         * 分析
         * 一只鸡翁价值5，100最多买20只鸡，假设可以买x只鸡翁。
         * 一只鸡母价值3，100最多买33只鸡，假设可以买y只鸡母。
         * 三只鸡雏价值1，100最多买300只鸡雏，假设可以买z只鸡雏。
         * 并且是100块钱买一百只鸡。
         * 则有以下表达式成立。
         * 鸡的价值为100
         * 5x + 3y + z/3 = 100;
         * 鸡的只数
         * x + y + z = 100;
         * ==>>> 第一个方程式乘以3
         * 15x + 9y + z = 300;
         * x + y + z = 100;
         * ===>>>两个方程式相减，消除z
         * 14x + 8y = 200 ;
         * ===>
         * 7x + 4y = 100;
         * 因为又满足价值小于 100，假设全部买鸡翁。则最多买 100/7 = 14只。所以  0<=x<=14
         * 根据x求带入方程式7x + 4y = 100;计算出y。根据x ,y带入方程式x + y + z = 100;计算出z;
         * @param args
         */
        public static void main(String[] args) {
            // 鸡翁值5， 一百块最多买20只  鸡翁买x只
            // 鸡母值3， 一百块最多买33只  鸡母买y只
            // 鸡雏三值1， 一百块最多买300只 鸡雏买z只
            Scanner in = new Scanner(System.in);
            // 买x鸡翁，y只鸡母，z只鸡雏
            //5x+3y+z/3=100  ==>  15x + 9y + z = 300
            //x+y+z==100确定         // ==>   14x + 8y = 200  ==> 7x + 4y = 100  ==>  y = (100 - 7x)/4
            while (in.hasNextInt()){
                int n = in.nextInt();
                for (int x = 0; x <= 14; x++) {
                    if ((100 - 7* x) % 4 == 0){
                        int y = (100-7*x) / 4;
                        int z = 100 - x - y;
                        System.out.println(x + " " + y + " " + z);
                    }
                }
            }
        }
    
    //    private static final int PRICE_F = 15;
    //    private static final int PRICE_M = 9;
    //    private static final int PRICE_C = 1;
    //    private static final int MONEY = 300;
    //    private static final int COUNT = 100;
    //
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        int start = in.nextInt();
    //
    //        for(int i=0; i<=MONEY/PRICE_F; i++){
    //            for(int j=0; j<=MONEY/PRICE_M; j++){
    //                if(i*PRICE_F + j*PRICE_M > MONEY){
    //                    break;
    //                }
    //                for(int k=0; k<=MONEY/PRICE_C; k++){
    //                    int spend = i*PRICE_F + j*PRICE_M + k*PRICE_C;
    //                    if(spend > MONEY){
    //                        break;
    //                    }
    //                    if(spend==MONEY && i+j+k==COUNT){
    //                        System.out.println(i+" "+j+" "+k);
    //                    }
    //                }
    //            }
    //        }
    //    }
    }

  

