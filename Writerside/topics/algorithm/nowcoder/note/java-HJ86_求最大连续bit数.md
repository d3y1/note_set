# java-HJ86 求最大连续bit数


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
            while(in.hasNextInt()){
                int num = in.nextInt();
                int max = 0;
                int count = 0;
                while(num != 0){
                    if((num&1) == 1){
                        count++;
                        max = Math.max(max,count);
                    }else{
                        count = 0;
                    }
                    num >>>= 1;
                }
                System.out.println(max);
            }
        }
    
    
    
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        int input = in.nextInt();
    //        String bitStr = Integer.toBinaryString(input);
    //
    //        String[] strings = bitStr.split("0+");
    //
    //        int result = 0;
    //        for(int i=0; i<strings.length; i++){
    //            result = Math.max(result, strings[i].length());
    //        }
    //
    //        System.out.print(result);
    //    }
    }

  

