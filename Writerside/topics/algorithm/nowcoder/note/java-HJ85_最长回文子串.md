# java-HJ85 最长回文子串


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            String input = in.nextLine();
    
            int len = input.length();
            int result = 1;
            
            for(int i=0; i<len; i++){
                for(int j=len; j>i; j--){
                    if(isReverse(input.substring(i,j))){
                        result = Math.max(result, j-i);
                    }
                }
            }
    
            System.out.print(result);
        }
    
        private static boolean isReverse(String str){
            
            return str.equals(new StringBuilder(str).reverse().toString());
        }
        
        
        
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        String input = in.nextLine();
    //
    //        int len = input.length();
    //
    //        int result = 1;
    //        int interval = 0;
    //
    //        if(len%2 == 0){
    //            interval = len/2;
    //        }else{
    //            interval = len/2+1;
    //        }
    //
    //        for(int i=interval; i>0; i--){
    //            boolean flag = false;
    //            for(int j=0,k=j+2*i-1; k<=len; j++,k++){
    //                if(isReverse(input.substring(j,k))){
    //                    flag = true;
    //                    result = Math.max(result,k-j);
    //                }
    //                if(k+1<=len){
    //                    if(isReverse(input.substring(j,k+1))){
    //                        flag = true;
    //                        result = Math.max(result, k+1-j);
    //                    }
    //                }
    //            }
    //            if(flag){
    //                break;
    //            }
    //        }
    //
    //        System.out.print(result);
    //    }
    //
    //    private static boolean isReverse(String str){
    //
    //        for(int i=0,j=str.length()-1; i<j; i++,j--){
    //            if(str.charAt(i) != str.charAt(j)){
    //                return false;
    //            }
    //        }
    //
    //        return true;
    //    }
    }

  

