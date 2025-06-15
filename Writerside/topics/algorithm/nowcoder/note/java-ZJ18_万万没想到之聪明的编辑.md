# java-ZJ18 万万没想到之聪明的编辑


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 正则
         * @param in
         */
        private static void solution(Scanner in){
            int n = Integer.parseInt(in.nextLine());
    
            for(int i=1; i<=n; i++){
                System.out.println(in.nextLine().replaceAll("(\\w)\\1{2,}","$1$1").replaceAll("(\\w)\\1(\\w)\\2","$1$1$2"));
            }
        }
    }

  

