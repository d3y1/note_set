# java-HJ96 表示数字


    
    
    
    	
    
    
    
    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        /**
         * regex is best!
         * @param args
         */
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            String input = in.nextLine();
    
    //        System.out.print(input.replaceAll("([\\d]+)", "*$1*"));
            System.out.print(input.replaceAll("([0-9]+)", "*$1*"));
        }
    
    
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        String input = in.nextLine();
    //        char[] inputChars = input.toCharArray();
    //        int len = inputChars.length;
    //
    //        StringBuilder sb = new StringBuilder();
    //
    //        for (int i = 0; i < len;) {
    //            if (Character.isDigit(inputChars[i])) {
    //                sb.append("*");
    //                sb.append(inputChars[i++]);
    //                while (i<len && Character.isDigit(inputChars[i])){
    //                    sb.append(inputChars[i++]);
    //                }
    //                sb.append("*");
    //            } else {
    //                sb.append(inputChars[i++]);
    //            }
    //        }
    //
    //        System.out.print(sb);
    //    }
    
    
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        String input = in.nextLine();
    //        char[] inputChars = input.toCharArray();
    //        int len = inputChars.length;
    //
    //        StringBuilder sb = new StringBuilder();
    //
    //        for (int i = 0; i < len; i++) {
    //            if (Character.isDigit(inputChars[i])) {
    //                if(i == 0){
    //                    sb.append("*");
    //                }else if (!Character.isDigit(inputChars[i-1])) {
    //                    sb.append("*");
    //                }
    //                sb.append(inputChars[i]);
    //                if(i == len-1){
    //                    sb.append("*");
    //                }else if (i+1 < len && !Character.isDigit(inputChars[i+1])) {
    //                    sb.append("*");
    //                }
    //            } else {
    //                sb.append(inputChars[i]);
    //            }
    //        }
    //
    //        System.out.print(sb);
    //    }
    }

  
  

