# java-NC270 把数组排成最小的数


    import java.util.*;
    import java.util.stream.Collectors;
    
    /**
     * NC270 把数组排成最小的数
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 相似 -> NC85 拼接所有的字符串产生字典序最小的字符串   [nowcoder]
         *
         * @param numbers int整型一维数组
         * @return string字符串
         */
        public String PrintMinNumber (int[] numbers) {
            // int[] -> Integer[]
            // return solution1(Arrays.stream(numbers).boxed().toArray(Integer[]::new));
            // int[] -> List<String>
            return solution2(Arrays.stream(numbers).mapToObj(String::valueOf).collect(Collectors.toList()));
            // int[] -> List<String>
            // return solution2(Arrays.stream(numbers).boxed().map(String::valueOf).collect(Collectors.toList()));
    
        }
    
        /**
         * 贪心+排序
         * @param numbers
         * @return
         */
        private String solution1(Integer[] numbers){
            // "32" "321"
            // 直接比较字典 32<321              => 32321
            // 连接比较字典 32>321(32321>32132) => 32132
            // 升序
            // Arrays.sort(numbers, (o1, o2) -> (String.valueOf(o1)+String.valueOf(o2)).compareTo(String.valueOf(o2)+String.valueOf(o1)));
            Arrays.sort(numbers, new Comparator<Integer>(){
                @Override
                public int compare(Integer o1, Integer o2){
                    return (String.valueOf(o1)+String.valueOf(o2)).compareTo(String.valueOf(o2)+String.valueOf(o1));
                }
            });
    
            StringBuilder sb = new StringBuilder();
            for(Integer num: numbers){
                sb.append(num);
            }
    
            return sb.toString();
        }
    
        /**
         * 贪心+排序
         * @param numbers
         * @return
         */
        private String solution2(List<String> numbers){
            // "32" "321"
            // 直接比较字典 32<321              => 32321
            // 连接比较字典 32>321(32321>32132) => 32132
            // 升序
            // Collections.sort(numbers, (o1, o2) -> (o1+o2).compareTo(o2+o1));
            numbers.sort((o1, o2) -> (o1+o2).compareTo(o2+o1));
    
            StringBuilder sb = new StringBuilder();
            for(String num: numbers){
                sb.append(num);
            }
    
            return sb.toString();
        }
    }

  

