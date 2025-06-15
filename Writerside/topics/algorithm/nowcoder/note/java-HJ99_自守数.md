# java-HJ99 自守数


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        /**
         * 取模
         * @param args
         */
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            int num = in.nextInt();
    
            int count = 0;
            int mod = 10;
            for(int i=0; i<=num; i++){
                if(i >= mod){
                    mod *= 10;
                }
                if(i%mod == i*i%mod){
                    count++;
                }
            }
    
            System.out.print(count);
        }
    
    
    
    //    /**
    //     * 字符串
    //     * @param args
    //     */
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        int num = in.nextInt();
    //
    //        int count = 0;
    //        for(int i=0; i<=num; i++){
    //            String iStr = String.valueOf(i);
    //            String powStr = String.valueOf(i*i);
    //            if(powStr.endsWith(iStr)){
    //                count++;
    //            }
    //        }
    //
    //        System.out.print(count);
    //    }
    
    
    
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        int num = in.nextInt();
    //
    //        int count = 0;
    //        for(int i=0; i<=num; i++){
    //            int pow = (int) Math.pow(i, 2);
    //            String iStr = String.valueOf(i);
    //            String powStr = String.valueOf(pow);
    //            if(iStr.equals(powStr.substring(powStr.length()-iStr.length()))){
    //                count++;
    //            }
    //        }
    //
    //        System.out.print(count);
    //    }
    }

  

