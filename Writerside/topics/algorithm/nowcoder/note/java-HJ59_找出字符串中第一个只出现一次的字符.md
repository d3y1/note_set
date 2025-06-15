# java-HJ59 找出字符串中第一个只出现一次的字符


    import java.util.HashMap;
    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            while (in.hasNext()){
                String input = in.nextLine();
    
                // map
                solution1(input);
    
                // String.indexOf() && String.lastIndexOf()
                // solution2(input);
    
                // String.replaceAll()
                // solution3(input);
    
                // bitmap: char[]
                // solution4(input);
            }
        }
    
        /**
         * map
         * @param input
         */
        private static void solution1(String input){
    
            HashMap<Character, Integer> charCountMap = new HashMap<>();
            for(int i=0; i<input.length(); i++){
                char aChar = input.charAt(i);
                charCountMap.put(aChar, charCountMap.getOrDefault(aChar,0)+1);
            }
    
            boolean found = false;
            for(char aChar: input.toCharArray()){
                Integer aCharCount = charCountMap.get(aChar);
                if(aCharCount == 1){
                    System.out.println(aChar);
                    found = true;
                    break;
                }
            }
    
            if(!found){
                System.out.println(-1);
            }
        }
    
    
        /**
         * String.indexOf() && String.lastIndexOf()
         * @param input
         */
        private static void solution2(String input){
    
            boolean found = false;
            for(char aChar: input.toCharArray()){
                if(input.indexOf(aChar) == input.lastIndexOf(aChar)){
                    System.out.println(aChar);
                    found = true;
                    break;
                }
            }
    
            if(!found){
                System.out.println(-1);
            }
        }
    
    
        /**
         * String.replaceAll()
         * @param input
         */
        private static void solution3(String input){
    
            int inputLen = input.length();
    
            boolean found = false;
            for(char aChar: input.toCharArray()){
                String replacedStr = input.replaceAll(String.valueOf(aChar), "");
                int replacedStrLen = replacedStr.length();
                if(inputLen-replacedStrLen == 1){
                    System.out.println(aChar);
                    found = true;
                    break;
                }
            }
    
            if(!found){
                System.out.println(-1);
            }
        }
    
    
        /**
         * bitmap: char[]
         * @param input
         */
        private static void solution4(String input){
    
            boolean found = false;
            char[] charsCount = new char[126];
            for(char aChar: input.toCharArray()){
                charsCount[aChar-'0']++;
            }
    
            for(char aChar: input.toCharArray()){
                if(charsCount[aChar-'0'] == 1){
                    System.out.println(aChar);
                    found = true;
                    break;
                }
            }
    
            if(!found){
                System.out.println(-1);
            }
        }
    }

  

