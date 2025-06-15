# java-HJ102 字符统计


    import java.util.ArrayList;
    import java.util.Collections;
    import java.util.Comparator;
    import java.util.HashMap;
    import java.util.List;
    import java.util.Map;
    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            String input = in.nextLine();
            char[] chars = input.toCharArray();
            HashMap<Character, Integer> hashMap = new HashMap<>(input.length());
    
            for(char aChar: chars){
                if(hashMap.containsKey(aChar)){
                    hashMap.put(aChar, hashMap.get(aChar)+1);
                }else{
                    hashMap.put(aChar, 1);
                }
            }
    
            List<Map.Entry<Character, Integer>> list = new ArrayList<>(hashMap.entrySet());
    
    //        Collections.sort(list, (e1, e2)->{
    //            if(e1.getValue() < e2.getValue()){
    //                return 1;
    //            }else{
    //                if(e1.getValue().equals(e2.getValue())){
    //                    if(e1.getKey() < e2.getKey()){
    //                        return -1;
    //                    }else{
    //                        return 1;
    //                    }
    //
    //                }else{
    //                    return -1;
    //                }
    //            }
    //        });
    
    //        Collections.sort(list, (e1, e2)->{
    //            if(e1.getValue() < e2.getValue()){
    //                return 1;
    //            }else if(e1.getValue().equals(e2.getValue())){
    //                if(e1.getKey() < e2.getKey()){
    //                    return -1;
    //                }else if(e1.getKey().equals(e2.getKey())){
    //                    return 0;
    //                }else{
    //                    return 1;
    //                }
    //            }else{
    //                return -1;
    //            }
    //        });
    
            Collections.sort(list, (o1, o2) -> {
                if(!o1.getValue().equals(o2.getValue())){//如果字符出现次数不同 按照出现次数从高到底
                    return o2.getValue()-o1.getValue();
                }else{//若次数相同则对比ASCII的大小 按照升序排列
                    return o1.getKey()-o2.getKey();
                }
            });
    
            for(Map.Entry entry: list){
                System.out.print(entry.getKey());
            }
        }
    }

  

