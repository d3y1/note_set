# java-HJ62 查找输入整数二进制中1的个数


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            int num = 0;
            // 注意 hasNext 和 hasNextLine 的区别
            while (in.hasNextInt()) { // 注意 while 处理多个 case
                num = in.nextInt();
                int count = 0;
                while (num !=0){
                    if(num%2 == 1){
                        count++;
                    }
                    num = num>>1;
                }
    
                System.out.println(count);
            }
        }
    
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        int num = 0;
    //        // 注意 hasNext 和 hasNextLine 的区别
    //        while (in.hasNextInt()) { // 注意 while 处理多个 case
    //            num = in.nextInt();
    //            String strNumBit = Integer.toBinaryString(num);
    //            String strNumBitShort = strNumBit.replaceAll("1", "");
    //
    //            System.out.println(strNumBit.length()-strNumBitShort.length());
    //        }
    //    }
    
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        int num = 0;
    //        // 注意 hasNext 和 hasNextLine 的区别
    //        while (in.hasNextInt()) { // 注意 while 处理多个 case
    //            num = in.nextInt();
    //            String strNumBit = Integer.toBinaryString(num);
    //            int count = 0;
    //            for (int i = 0; i < strNumBit.length(); i++) {
    //                if(strNumBit.charAt(i) == '1'){
    //                    count++;
    //                }
    //            }
    //
    //            System.out.println(count);
    //        }
    //    }
    }

  

