# java-HJ57 高精度整数加法


    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            while (in.hasNext()) {
                String numAStr = in.nextLine();
                String numBStr = in.nextLine();
    
                // solution(numAStr, numBStr);
                solutionSimplify(numAStr, numBStr);
            }
        }
    
    
        /**
         * 模拟法 简化
         * @param numAStr
         * @param numBStr
         */
        private static void solutionSimplify (String numAStr, String numBStr){
            int lenA = numAStr.length();
            int lenB = numBStr.length();
    
            int carry = 0;
            StringBuilder numsStr = new StringBuilder();
            for(int i=lenA-1,j=lenB-1; i>=0||j>=0; i--,j--){
                char charA = i>=0 ? numAStr.charAt(i) : '0';
                char charB = j>=0 ? numBStr.charAt(j) : '0';
                int lastSum = (charA-'0') + (charB-'0') + carry;
                numsStr.append(lastSum % 10);
                carry = lastSum / 10;
            }
    
            if(carry == 1){
                numsStr.append(carry);
            }
    
            System.out.println(numsStr.reverse());
        }
    
    
        /**
         * 模拟法
         * @param numAStr
         * @param numBStr
         */
        private static void solution (String numAStr, String numBStr){
            int lenA = numAStr.length();
            int lenB = numBStr.length();
            int lenMax = Math.max(lenA, lenB);
    
            // 初始化 对齐
            StringBuilder prefix = new StringBuilder();
            if (lenA != lenB) {
                for (int i = 1; i <= Math.abs(lenA - lenB); i++) {
                    prefix.append("0");
                }
                if (lenA > lenB) {
                    numBStr = prefix + numBStr;
                } else {
                    numAStr = prefix + numAStr;
                }
            }
    
            // 模拟 进位运算
            int upper = 0;
            int[] nums = new int[lenMax + 1];
            int k = 0;
            for (int i = lenMax - 1; i >= 0; i--) {
                int lastSum = upper + Integer.parseInt(String.valueOf(numAStr.charAt(i))) + Integer.parseInt(String.valueOf(numBStr.charAt(i)));
                int lastDigit = lastSum % 10;
                nums[k++] = lastDigit;
                upper = lastSum / 10;
            }
            nums[k] = upper;
    
            // 打印
            StringBuilder numsStr = new StringBuilder();
            for (int i = lenMax; i >= 0; i--) {
                numsStr.append(nums[i]);
            }
            if (numsStr.indexOf("0") == 0) {
                String result = numsStr.toString().replaceFirst("0+", "");
                if ("".equals(result)) {
                    System.out.println(0);
                } else {
                    System.out.println(result);
                }
            } else {
                System.out.println(numsStr);
            }
        }
    }

  

