# java-QQ3 编码


    import java.util.Scanner;
    
    public class Main {
        private static final int N = 4;
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 数学法: 编码
         * @param in
         */
        private static void solution(Scanner in){
            char[] code = in.nextLine().toCharArray();
            int len = code.length;
    
            int gap;
            long index = 0;
            for(int i=0; i<len; i++){
                gap = code[i]-'a';
                if(gap > 0){
                    for(int j=0; j<N-i; j++){
                        index += gap * (long)Math.pow(25,j);
                    }
                }
            }
    
            index += len-1;
    
            System.out.println(index);
        }
    }

  

