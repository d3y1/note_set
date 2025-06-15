# java-MT28 手机号


    import java.util.HashSet;
    import java.util.Scanner;
    
    public class Main {
        // 中国电信: 133,153,180,181,189
        private static final HashSet<String> telecomSet = new HashSet<String>(){{
            add("133");
            add("153");
            add("180");
            add("181");
            add("189");
        }};
        // 中国联通: 130,131,155,185,186
        private static final HashSet<String> unicomSet = new HashSet<String>(){{
            add("130");
            add("131");
            add("155");
            add("185");
            add("186");
        }};
        // 中国移动: 135,136,150,182,188
        private static final HashSet<String> mobilecomSet = new HashSet<String>(){{
            add("135");
            add("136");
            add("150");
            add("182");
            add("188");
        }};
    
        private static final int LEN = 11;
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution1(in);
                solution2(in);
            }
        }
    
        /**
         * 字符串: 正则
         * @param in
         */
        private static void solution1(Scanner in){
            int N = Integer.parseInt(in.nextLine());
    
            String number,prefix;
            for(int i=1; i<=N; i++){
                number = in.nextLine();
                if(number.matches("(133|153|180|181|189)\\d{8}")){
                    System.out.println("China Telecom");
                }else if(number.matches("(130|131|155|185|186)\\d{8}")){
                    System.out.println("China Unicom");
                }else if(number.matches("(135|136|150|182|188)\\d{8}")){
                    System.out.println("China Mobile Communications");
                }else{
                    System.out.println(-1);
                }
            }
        }
        
        /**
         * 字符串: Set
         * @param in
         */
        private static void solution2(Scanner in){
            int N = Integer.parseInt(in.nextLine());
    
            String number,prefix;
            for(int i=1; i<=N; i++){
                number = in.nextLine();
                if(number.length() != LEN){
                    System.out.println(-1);
                }else{
                    prefix = number.substring(0, 3);
                    if(telecomSet.contains(prefix)){
                        System.out.println("China Telecom");
                    }else if(unicomSet.contains(prefix)){
                        System.out.println("China Unicom");
                    }else if(mobilecomSet.contains(prefix)){
                        System.out.println("China Mobile Communications");
                    }else{
                        System.out.println(-1);
                    }
                }
            }
        }
    }

  

