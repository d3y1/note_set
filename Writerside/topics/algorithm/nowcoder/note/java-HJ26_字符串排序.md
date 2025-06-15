# java-HJ26 字符串排序


    import java.util.Collections;
    import java.util.Comparator;
    import java.util.List;
    import java.util.Scanner;
    import java.util.stream.Collectors;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in  = new Scanner(System.in);
    
            while (in.hasNext()){
                String input = in.nextLine();
                String alphabet = input.replaceAll("[^a-zA-Z]", "");
                List<Character> charsList = alphabet.chars().mapToObj(c -> (char)c).collect(Collectors.toList());
    
                Collections.sort(charsList, new Comparator<Character>() {
                    @Override
                    public int compare(Character o1, Character o2) {
    //                    if(Character.toLowerCase(o1) == Character.toLowerCase(o2)){
    //                        return 0;
    //                    }else{
    //                        return Character.toLowerCase(o1)-Character.toLowerCase(o2);
    //                    }
                        return Character.toLowerCase(o1)-Character.toLowerCase(o2);
                    }
                });
    
                Object[] chars = charsList.toArray();
                int index = 0;
                StringBuilder sb = new StringBuilder();
                for(int i=0; i<input.length(); i++){
                    Character aChar = input.charAt(i);
                    if(Character.isAlphabetic(aChar)){
                        sb.append(chars[index++]);
                    }else{
                        sb.append(aChar);
                    }
                }
    
                System.out.println(sb);
            }
        }
    }

  

