# java-HJ45 名字的漂亮度


    import java.util.ArrayList;
    import java.util.Arrays;
    import java.util.Collections;
    import java.util.HashMap;
    import java.util.Map;
    import java.util.List;
    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            while (in.hasNext()){
                Integer num = in.nextInt();
                for(int i=1; i<=num; i++){
                    // solutionList(in.next());
                   solutionMap(in.next());
                }
            }
        }
    
    
        /**
         * list sort()
         * @param word
         */
        private static void solutionList(String word){
            char[] wordChars = word.toCharArray();
    
            int[] charCount = new int[26];
            for(char aChar: wordChars){
                if(Character.isLetter(aChar)){
                    char lowerChar = Character.toLowerCase(aChar);
                    charCount[lowerChar-'a']++;
                }
            }
    
            Arrays.sort(charCount);
    
            int result = 0;
            int pretty = 26;
            for(int j=25; j>=0; j--){
                if(charCount[j] == 0){
                    break;
                }
                result += charCount[j]*(pretty--);
            }
    
            System.out.println(result);
        }
        
    
        /**
         * map sort()
         * @param word
         */
        private static void solutionMap(String word){
            char[] wordChars = word.toCharArray();
    
            HashMap<Character, Integer> charMap = new HashMap<>();
            for(char aChar: wordChars){
                if(Character.isLetter(aChar)){
                    char lowerChar = Character.toLowerCase(aChar);
                    charMap.put(lowerChar, charMap.getOrDefault(lowerChar, 0)+1);
                }
            }
    
           // map排序
           List<Map.Entry<Character, Integer>> entryList = new ArrayList<>(charMap.entrySet());
           Collections.sort(entryList, (o1, o2) -> o2.getValue()-o1.getValue());
    
           int result = 0;
           int pretty = 26;
           for(Map.Entry<Character, Integer> entry: entryList){
               result += entry.getValue()*(pretty--);
           }
    
            // // 仅需要的value排序
            // int[] mapValues = new int[charMap.size()];
            // int index = 0;
            // for(Character key: charMap.keySet()){
            //     mapValues[index++] = charMap.get(key);
            // }
            // Arrays.sort(mapValues);
    
            // int result = 0;
            // int pretty = 26;
            // for(int j= mapValues.length-1; j>=0; j--){
            //     result += mapValues[j]*(pretty--);
            // }
    
    
            System.out.println(result);
        }
    }

  

