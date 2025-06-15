# java-HJ8 合并表记录


    import java.util.Collection;
    import java.util.HashMap;
    import java.util.LinkedHashMap;
    import java.util.Map;
    import java.util.Scanner;
    import java.util.TreeMap;
    import java.util.stream.Collectors;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
            int num = in.nextInt();
    
            // treemap
            Map<Integer, Integer> map = new TreeMap<Integer, Integer>();
    
            int key, value = 0;
            for (int i = 0; i < num; i++) {
                key = in.nextInt();
                value = in.nextInt();
                if (map.get(key) != null) {
                    map.put(key, map.get(key) + value);
                } else {
                    map.put(key, value);
                }
            }
    
            for (Integer mapKey : map.keySet()) {
                System.out.println(mapKey + " " + map.get(mapKey));
            }
    
    
    
            // hashmap + stream
            // Map<Integer, Integer> map = new HashMap<Integer, Integer>();
    
            // int key, value = 0;
            // for (int i = 0; i < num; i++) {
            //     key = in.nextInt();
            //     value = in.nextInt();
            //     if (map.get(key) != null) {
            //         map.put(key, map.get(key) + value);
            //     } else {
            //         map.put(key, value);
            //     }
            // }
    
            // Map<Integer, Integer> sortMap = map.entrySet().stream().sorted(Map.Entry.comparingByKey()).collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue, (e1, e2)->e1, LinkedHashMap::new));
    
            // for (Integer mapKey : sortMap.keySet()) {
            //     System.out.println(mapKey + " " + sortMap.get(mapKey));
            // }
        }
    }

  

