# java-NC111 最大数


    import java.util.*;
    import java.util.stream.Collectors;
    
    /**
     * NC111 最大数
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 相似 -> NC270  把数组排成最小的数                     [nowcoder]
         * 相似 -> NC85   拼接所有的字符串产生字典序最小的字符串    [nowcoder]
         *
         * 最大数
         * @param nums int整型一维数组
         * @return string字符串
         */
        public String solve (int[] nums) {
            // return solution1(Arrays.stream(nums).boxed().toArray(Integer[]::new));
            return solution2(Arrays.stream(nums).boxed().map(String::valueOf).collect(Collectors.toList()));
        }
    
        /**
         * 排序: Integer[]
         * @param nums
         * @return
         */
        private String solution1(Integer[] nums){
            Arrays.sort(nums, new Comparator<Integer>(){
                @Override
                public int compare(Integer o1, Integer o2){
                    return (String.valueOf(o2)+String.valueOf(o1)).compareTo(String.valueOf(o1)+String.valueOf(o2));
                }
            });
    
            StringBuilder sb = new StringBuilder();
            for(int num: nums){
                sb.append(num);
            }
    
            String result = sb.toString();
            // 去掉 前导0
            if(result.startsWith("0")){
                result = result.replaceFirst("^0+", "");
            }
    
            return "".equals(result)?"0":result;
        }
    
        /**
         * 排序: List<String>
         * @param nums
         * @return
         */
        private String solution2(List<String> nums){
            Collections.sort(nums, (o1, o2) -> (o2+o1).compareTo(o1+o2));
    
            StringBuilder sb = new StringBuilder();
            for(String num: nums){
                sb.append(num);
            }
    
            String result = sb.toString();
            // 去掉 前导0
            if(result.startsWith("0")){
                result = result.replaceFirst("^0+", "");
            }
    
            return "".equals(result)?"0":result;
        }
    }

  

