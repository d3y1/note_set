# java-HJ95 人民币转换


    import java.util.Scanner;
    import java.util.HashMap;
    
    public class Main {
        private static final HashMap<Integer, String> numMap = new HashMap<Integer, String>(){{
            put(1, "壹");
            put(2, "贰");
            put(3, "叁");
            put(4, "肆");
            put(5, "伍");
            put(6, "陆");
            put(7, "柒");
            put(8, "捌");
            put(9, "玖");
            put(10, "拾");
            put(100, "佰");
            put(1000, "仟");
        }};
        private static final String[] units = new String[]{"", "万", "亿"};
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
    
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 模拟法
         * @param in
         */
        private static void solution(Scanner in){
            String[] money = in.nextLine().split("\\.");
    
            // 整数
            String number = money[0];
            // 小数
            String fraction = money[1];
    
            int numLen = number.length();
            int times = numLen / 4;
            int remainder = numLen % 4;
    
            StringBuilder result = new StringBuilder();
    
            // 整数部分 从右到左 每4位数转换一次
            for(int i=1; i<=times; i++){
                result.insert(0, transfer(Integer.parseInt(number.substring(numLen-i*4, numLen-(i-1)*4)))+units[i-1]);
            }
            if(remainder > 0){
                if(times == 0){
                    result.insert(0, transfer(Integer.parseInt(number.substring(0, remainder))));
                }else{
                    result.insert(0, transfer(Integer.parseInt(number.substring(0, remainder)))+units[times]);
                }
            }
            if(Integer.parseInt(number) > 0){
                result.append("元");
            }
    
            // 小数部分
            if("00".equals(fraction)){
                result.append("整");
            }else{
                // 角
                if(fraction.charAt(0) != '0'){
                    result.append(numMap.get(Integer.parseInt(String.valueOf(fraction.charAt(0))))).append("角");
                }
                // 分
                if(fraction.charAt(1) != '0'){
                    result.append(numMap.get(Integer.parseInt(String.valueOf(fraction.charAt(1))))).append("分");
                }
            }
    
            result.insert(0, "人民币");
            System.out.println(result);
        }
    
        /**
         * 四位数 转 中文
         * @param num
         * @return
         */
        private static String transfer(int num){
            StringBuilder sb = new StringBuilder();
    
            // 千位
            int thousandthDigit = num / 1000;
            int thousandthRemainder = num % 1000;
            if(thousandthDigit > 0){
                sb.append(numMap.get(thousandthDigit)).append(numMap.get(1000));
                if(0<thousandthRemainder && thousandthRemainder<100){
                    sb.append("零");
                }
            }
    
            // 百位
            int hundredthDigit = thousandthRemainder / 100;
            int hundredthRemainder = thousandthRemainder % 100;
            if(thousandthRemainder >= 100){
                sb.append(numMap.get(hundredthDigit)).append(numMap.get(100));
                if(0<hundredthRemainder && hundredthRemainder<10){
                    sb.append("零");
                }
            }
    
            // 十位
            int tenthDigit = hundredthRemainder / 10;
            int tenthRemainder = hundredthRemainder % 10;
            if(hundredthRemainder >= 10){
                if(tenthDigit == 1){
                    sb.append(numMap.get(10));
                }else{
                    sb.append(numMap.get(tenthDigit)).append(numMap.get(10));
                }
            }
    
            // 个位
            if(tenthRemainder > 0){
                sb.append(numMap.get(tenthRemainder));
            }
    
            return sb.toString();
        }
    }

  

