# java-HJ27 查找兄弟单词


    import java.util.ArrayList;
    import java.util.Arrays;
    import java.util.Collections;
    import java.util.HashSet;
    import java.util.List;
    import java.util.Scanner;
    import java.util.TreeSet;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        /**
         * 单独判断
         * @param args
         */
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
    
            while (scanner.hasNext()){
                String[] ss = scanner.nextLine().split(" ");
                Integer a = Integer.parseInt(ss[0]);
                String x = ss[ss.length-2];
                Integer k = Integer.parseInt(ss[ss.length-1]);
                List<String> list = new ArrayList<>();
    
                for (int i = 1; i <=a ; i++) {
                    if (isBrother(x,ss[i])){
                        list.add(ss[i]);
                    }
                }
                int size = list.size();
                System.out.println(size);
                if (size>=k){
                    Collections.sort(list);
                    System.out.println(list.get(k-1));
                }
            }
        }
        
        public static boolean isBrother(String x,String y){
            if (x.length()!=y.length()||y.equals(x)){
                return false;
            }
            char[] s = x.toCharArray();
            char[] j= y.toCharArray();
            Arrays.sort(s);
            Arrays.sort(j);
            return new String(s).equals(new String(j));
        }
        
        
    
    //    /**
    //     * set 子序列
    //     */
    //    private static HashSet<String> diffWords = new HashSet<>();
    //
    //    public static void main(String[] args) {
    //        Scanner in = new Scanner(System.in);
    //
    //        while (in.hasNext()){
    //            String input = in.nextLine();
    //            String[] strList = input.split(" ");
    //
    //
    //
    //            int total = Integer.parseInt(strList[0]);
    //            String[] words = new String[total];
    //            for(int i=0; i<total; i++){
    //                words[i] = strList[i+1];
    //            }
    //
    //            String xWord = strList[total+1];
    //            int index = Integer.parseInt(strList[total+2]);
    //
    //            generateWord(xWord, 0);
    //
    //            int count = 0;
    //            List<String> sortSibWords = new ArrayList<>();
    //            for(String word: words){
    //                if(!word.equals(xWord) && diffWords.contains(word)){
    //                    count++;
    //                    sortSibWords.add(word);
    //                }
    //            }
    //
    //            Collections.sort(sortSibWords);
    //
    //            System.out.println(count);
    //            if(index <= count){
    //                // Object[] sibWords = sortSibWords.toArray();
    //                System.out.println(sortSibWords.get(index-1));
    //            }
    //
    //            diffWords = new HashSet<>();
    //        }
    //    }
    //
    //    private static void generateWord(String word, int i){
    //        diffWords.add(word);
    //        char[] chars = word.toCharArray();
    //        for(int j=i; j<chars.length; j++){
    //            swap(chars, i, j);
    //            generateWord(String.valueOf(chars), i+1);
    //            swap(chars, j, i);
    //        }
    //    }
    //
    //    private static void swap(char[] chars, int i, int j){
    //        char tmp = chars[i];
    //        chars[i] = chars[j];
    //        chars[j] = tmp;
    //    }
    }

  

