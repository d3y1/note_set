# java-HJ108 求最小公倍数


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        /**
         * 递归
         * @param args
         */
        public static void main(String[] args) {
            Scanner sc = new Scanner(System.in);
            int a = sc.nextInt();
            int b = sc.nextInt();
            //存储a的原始值，递归过程中使用
            int c = a;
            System.out.println(gcb(a,b,c));
        }
        public static int gcb(int a,int b,int c){
            //a累加过程中永远可以整除自身，所以可以整除b时就是最小公倍数！
            if (a%b== 0){
                return a;
            }
            //a累加自身原始值，例如a=4。  a=4,8,12,16....
            return gcb(a+c,b,c);  
        }
        
        
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        while (in.hasNextInt()){
    //            int a = in.nextInt();
    //            int b = in.nextInt();
    //
    //            int result = a*b;
    //            int max = Math.max(a,b);
    //            int min = Math.min(a,b);
    //
    //            if(max%min == 0){
    //                result = max;
    //            }else{
    //                for(int i=max; i<=a*b; i=i+max){
    //                    if(i%min == 0){
    //                        result = i;
    //                        break;
    //                    }
    //                }
    //            }
    //
    //            System.out.print(result);
    //        }
    //    }
    }

  

