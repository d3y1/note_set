# java-MT35 字符串距离


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution1(in);
            }
        }
    
        /**
         * 模拟法: 前缀和
         * 
         * pre[i]表示字符串S前i个字符中a的个数
         * 
         * @param in
         */
        private static void solution1(Scanner in){
            String S = in.nextLine();
            String T = in.nextLine();
    
            int sLen = S.length();
            int tLen = T.length();
    
            int[] pre = new int[sLen+1];
            for(int i=1; i<=sLen; i++){
                if(S.charAt(i-1) == 'a'){
                    pre[i] = pre[i-1]+1;
                }else{
                    pre[i] = pre[i-1];
                }
            }
    
            int gap = sLen-tLen+1;
            long result = 0;
            char tChar;
            int aCount;
            for(int i=0; i<tLen; i++){
                tChar = T.charAt(i);
                aCount = pre[i+gap]-pre[i];
                if(tChar == 'b'){
                    result += aCount;
                }else{
                    result += gap-aCount;
                }
            }
    
            System.out.println(result);
        }
    }

  

