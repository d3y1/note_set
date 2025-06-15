# java-MT34 数字构造


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
         * 模拟法: 找规律
         * 简化
         * @param in
         */
        private static void solution1(Scanner in){
            int s = in.nextInt();
    
            int multi = s/3;
            int mod = s%3;
            StringBuilder sb = new StringBuilder();
            if(mod == 1){
                sb.append(1);
            }
            for(int i=1; i<=multi; i++){
                sb.append("21");
            }
            if(mod == 2){
                sb.append(2);
            }
    
            System.out.println(sb);
        }
    
        /**
         * 模拟法: 找规律
         * @param in
         */
        private static void solution2(Scanner in){
            int s = in.nextInt();
    
            int multi = s/3;
            int mod = s%3;
            StringBuilder sb = new StringBuilder();
            if(mod == 0){
                for(int i=1; i<=multi; i++){
                    sb.append("21");
                }
            }else if(mod == 1){
                for(int i=1; i<=multi; i++){
                    sb.append("12");
                }
                sb.append(1);
            }else if(mod == 2){
                for(int i=1; i<=multi; i++){
                    sb.append("21");
                }
                sb.append(2);
            }
    
            System.out.println(sb);
        }
    }

  

