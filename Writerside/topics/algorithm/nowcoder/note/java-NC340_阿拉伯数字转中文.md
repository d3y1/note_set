# java-NC340 阿拉伯数字转中文


    import java.util.*;
    
    /**
     * NC340 阿拉伯数字转中文
     * @author d3y1
     */
    public class Solution {
        private HashMap<Integer, String> numMap = new HashMap<Integer, String>(){{
            put(0, "零");
            put(1, "一");
            put(2, "二");
            put(3, "三");
            put(4, "四");
            put(5, "五");
            put(6, "六");
            put(7, "七");
            put(8, "八");
            put(9, "九");
        }};
    
        private HashMap<Integer, String> map = new HashMap<Integer, String>(){{
            put(0, "");
            put(1, "十");
            put(2, "百");
            put(3, "千");
            put(4, "万");
            put(5, "亿");
        }};
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param n int整型
         * @return string字符串
         */
        public String num2cn (int n) {
            if(n == 0){
                return "零";
            }
            String numStr = String.valueOf(n);
            StringBuilder result = new StringBuilder();
    
            boolean isNegative = false;
            if(numStr.startsWith("-")){
                isNegative = true;
                if(numStr.length() > 1){
                    numStr = numStr.substring(1);
                }
            }
    
            // 按4位分隔处理
            int len = numStr.length();
            int parts = (int)Math.ceil(len/4.0);
    
            int start, end;
            String partResult = "";
            String partNum;
            for(int i=0; i<parts; i++){
                start = len-(i+1)*4;
                if(start < 0){
                    start = 0;
                }
                end = len-i*4;
                partNum = numStr.substring(start, end);
                if(partNum.equals("0000")){
                    continue;
                }
                partResult = partNum2CN(partNum);
                if(i > 0){
                    partResult += map.get(i+3);
                }
                result.insert(0, partResult);
            }
    
            if(isNegative){
                result.insert(0, "负");
            }
    
            return result.toString();
        }
    
        private String partNum2CN(String numStr){
            StringBuilder sb = new StringBuilder();
            
            // 从左到右 第一个非零索引 first non-zero index
            int FNZIndex = -1;
            // 从右到左 第一个非零索引 last non-zero index
            int LNZIndex = -1;
            if(numStr.length() > 0){
                for(int i=0; i<numStr.length(); i++){
                    if(numStr.charAt(i) != '0'){
                        FNZIndex = i;
                        break;
                    }
                }
                if(FNZIndex == -1){
                    return "";
                }
                for(int i=numStr.length()-1; i>=0; i--){
                    if(numStr.charAt(i) != '0'){
                        LNZIndex = i;
                        break;
                    }
                }
    
                char ch;
                boolean hasZero = false;
                int len = numStr.length();
                for(int i=0; i<len; i++){
                    ch = numStr.charAt(i);
                    if(ch == '0'){
                        if(FNZIndex<i && i<LNZIndex && !hasZero){
                            sb.append("零");
                            hasZero = true;
                        }
                        if(i<FNZIndex && !hasZero){
                            sb.append("零");
                            hasZero = true;
                        }
                    }else{
                        // 十位为一的情况 1011->一千零十一 1000000000->十亿
                        if(ch=='1' && len-1-i==1){
                            if(i > 0){
                                if(numStr.charAt(i-1)=='0'){
                                    sb.append(map.get(len-1-i));
                                }else{
                                    sb.append(numMap.get(ch-'0')).append(map.get(len-1-i));
                                }
                            }
                            else{
                                sb.append(map.get(len-1-i));
                            }
                        }else{
                            sb.append(numMap.get(ch-'0')).append(map.get(len-1-i));
                        }
    
                    }
                }
            }
    
            return sb.toString();
        }
    }

  

