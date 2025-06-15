# java-HJ21 简单密码


    import java.util.HashMap;
    import java.util.Map;
    import java.util.Scanner;
    import java.util.Set;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
    
        private static Map<String, Character> map = new HashMap<String, Character>(){
            {
                put("abc", '2');
                put("def", '3');
                put("ghi", '4');
                put("jkl", '5');
                put("mno", '6');
                put("pqrs", '7');
                put("tuv", '8');
                put("wxyz", '9');
            }
        };
    
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            String input = in.nextLine();
            StringBuffer strBuf = new StringBuffer();
    
            for(int i=0; i<input.length(); i++){
                if('a'<=input.charAt(i) && input.charAt(i)<='z'){
                    Set<String> keys = map.keySet();
                    for(String key: keys){
                        if(key.contains(String.valueOf(input.charAt(i)))){
                            strBuf.append(map.get(key));
                        }
                    }
                }else if('A'<=input.charAt(i) && input.charAt(i)<='Y'){
                    strBuf.append((char)(input.charAt(i)+32+1));
                }else if(input.charAt(i) == 'Z'){
                    strBuf.append('a');
                }else{
                    strBuf.append(input.charAt(i));
                }
            }
    
            System.out.print(strBuf);
        }
    
        // map
        // private static Map<Character, Character> map = new HashMap<Character, Character>(){
        //     {
        //         put('a', '2');
        //         put('b', '2');
        //         put('c', '2');
        //         put('d', '3');
        //         put('e', '3');
        //         put('f', '3');
        //         put('g', '4');
        //         put('h', '4');
        //         put('i', '4');
        //         put('j', '5');
        //         put('k', '5');
        //         put('l', '5');
        //         put('m', '6');
        //         put('n', '6');
        //         put('o', '6');
        //         put('p', '7');
        //         put('q', '7');
        //         put('r', '7');
        //         put('s', '7');
        //         put('t', '8');
        //         put('u', '8');
        //         put('v', '8');
        //         put('w', '9');
        //         put('x', '9');
        //         put('y', '9');
        //         put('z', '9');
    
        //         put('A', 'b');
        //         put('B', 'c');
        //         put('C', 'd');
        //         put('D', 'e');
        //         put('E', 'f');
        //         put('F', 'g');
        //         put('G', 'h');
        //         put('H', 'i');
        //         put('I', 'j');
        //         put('J', 'k');
        //         put('K', 'l');
        //         put('L', 'm');
        //         put('M', 'n');
        //         put('N', 'o');
        //         put('O', 'p');
        //         put('P', 'q');
        //         put('Q', 'r');
        //         put('R', 's');
        //         put('S', 't');
        //         put('T', 'u');
        //         put('U', 'v');
        //         put('V', 'w');
        //         put('W', 'x');
        //         put('X', 'y');
        //         put('Y', 'z');
        //         put('Z', 'a');
        //     }
        // };
    
        // public static void main(String[] args) {
        //     Scanner in = new Scanner(System.in);
    
        //     String input = in.nextLine();
        //     StringBuffer strBuf = new StringBuffer();
    
        //     for(int i=0; i<input.length(); i++){
        //         if(map.get(input.charAt(i)) == null){
        //             strBuf.append(input.charAt(i));
        //         }else{
        //             strBuf.append(map.get(input.charAt(i)));
        //         }
        //     }
    
        //     System.out.print(strBuf);
        // }
    }

  

