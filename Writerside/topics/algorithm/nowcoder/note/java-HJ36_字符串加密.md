# java-HJ36 字符串加密


    import java.util.HashMap;
    import java.util.HashSet;
    import java.util.HashSet;
    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        private static final Integer SIZE = 26;
        private static final Integer LOWER_START = 97;
        private static final Integer UPPER_START = 65;
    
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            while (in.hasNext()){
                String key = in.nextLine();
                String word = in.nextLine();
    
                char[] keyChars = key.toCharArray();
                char[] wordChars = word.toCharArray();
                HashSet<Character> lowerKeyCharSet = new HashSet<>();
                HashSet<Character> upperKeyCharSet = new HashSet<>();
                HashMap<Character, Character> lowerKeyMap = new HashMap<>();
                HashMap<Character, Character> upperKeyMap = new HashMap<>();
    
    
                int lowerStart = LOWER_START;
                int upperStart = UPPER_START;
                for(char aChar: keyChars){
                    if(Character.isUpperCase(aChar) && !upperKeyCharSet.contains(aChar)){
                        upperKeyCharSet.add(aChar);
                        upperKeyMap.put((char) upperStart++, aChar);
                    }else if(Character.isLowerCase(aChar) && !lowerKeyCharSet.contains(aChar)){
                        lowerKeyCharSet.add(aChar);
                        lowerKeyMap.put((char) lowerStart++, aChar);
                    }
                }
    
                for(int i=0; i<SIZE && upperStart<UPPER_START+SIZE; i++){
                    Character upperChar = (char) (UPPER_START+i);
    
                    if(!upperKeyCharSet.contains(upperChar)){
                        upperKeyCharSet.add(upperChar);
                        upperKeyMap.put((char) upperStart++, upperChar);
                    }
                }
    
                for(int i=0; i<SIZE && lowerStart<LOWER_START+SIZE; i++){
                    Character lowerChar = (char) (LOWER_START+i);
    
                    if(!lowerKeyCharSet.contains(lowerChar)){
                        lowerKeyCharSet.add(lowerChar);
                        lowerKeyMap.put((char) lowerStart++, lowerChar);
                    }
                }
    
    
                StringBuilder sb = new StringBuilder();
                for(char aChar: wordChars){
                    if(Character.isUpperCase(aChar)){
                        sb.append(upperKeyMap.get(aChar));
                    }else if(Character.isLowerCase(aChar)){
                        sb.append(lowerKeyMap.get(aChar));
                    }
                }
    
                System.out.println(sb);
             }
        }
    }

  

