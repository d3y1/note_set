# java-HJ14 字符串排序


    import java.util.ArrayList;
    import java.util.Arrays;
    import java.util.Collections;
    import java.util.LinkedList;
    import java.util.List;
    import java.util.Scanner;
    
    // Arrays sort()
    // public class Main {
    //     public static void main(String[] args) {
    //         Scanner in = new Scanner(System.in);
            
    //         int count = in.nextInt();
    
    //         String[] list = new String[count];
    
    //         for(int i=0; i<count; i++){
    //             list[i] = in.next();
    //         }
    
    //         Arrays.sort(list);
    
    //         for(String word: list){
    //             System.out.println(word);
    //         }
    //     }
    // }
    
    // Collections sort()
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
            
            int count = Integer.valueOf(in.nextLine());
    
            // List<String> list = new ArrayList<String>();
            List<String> list = new LinkedList<String>();
            while(count-- > 0){
                list.add(in.nextLine());
            }
    
            Collections.sort(list);
    
            for(String word: list){
                System.out.println(word);
            }
        }
    }

  

