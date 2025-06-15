# java-NC324 下一个更大的数(三)


    import java.util.*;
    
    /**
     * NC324 下一个更大的数(三)
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 相似 -> NC194 下一个排列 [nowcoder]
         *
         * @param n int整型
         * @return int整型
         */
        public int nextGreaterElement (int n) {
            // return solution1(n);
            // return solution2(n);
            // return solution3(n);
            // return solution4(n);
            return solution5(n);
        }
    
        /**
         * 双指针
         * @param n
         * @return
         */
        private int solution1(int n){
            char[] digits = String.valueOf(n).toCharArray();
            int len = digits.length;
    
            for(int i=len-1; i>=0; i--){
                for(int j=len-1; j>i; j--){
                    if(digits[i] < digits[j]){
                        swap(digits, i, j);
                        // 区间排序 [from,to): [i+1,len)
                        Arrays.sort(digits, i+1, len);
                        return Integer.parseInt(String.valueOf(digits));
                    }
                }
            }
    
            return -1;
        }
    
        /**
         * 双指针
         * @param n
         * @return
         */
        private int solution2(int n){
            char[] digits = String.valueOf(n).toCharArray();
            int len = digits.length;
    
            // 找到待交换位置
            int i;
            for(i=len-2; i>=0; i--){
                if(digits[i] < digits[i+1]){
                    break;
                }
            }
            if(i < 0){
                return -1;
            }
            // 双指针
            for(int j=len-1; j>i; j--){
                // i右边已经降序 找到第一个大于digits[i]的数(从右向左)
                if(digits[i] < digits[j]){
                    swap(digits, i, j);
                    break;
                }
            }
    
            // 区间排序 [from,to): [i+1,len)
            Arrays.sort(digits, i+1, len);
    
            return Integer.parseInt(String.valueOf(digits));
        }
    
        /**
         * 二分
         * @param n
         * @return
         */
        private int solution3(int n){
            char[] digits = String.valueOf(n).toCharArray();
            int len = digits.length;
    
            // 找到待交换位置
            int i;
            for(i=len-2; i>=0; i--){
                if(digits[i] < digits[i+1]){
                    break;
                }
            }
            if(i < 0){
                return -1;
            }
    
            // 二分 i右边已经降序
            int left = i+1;
            int right = len-1;
            int mid;
            while(left <= right){
                mid = left+((right-left)>>1);
                // right最终指向第一个大于target(digits[i])的数(从右向左)
                if(digits[mid] <= digits[i]){
                    right = mid-1;
                }else{
                    left = mid+1;
                }
            }
            swap(digits, i, right);
    
            // 区间排序 [from,to): [i+1,len)
            Arrays.sort(digits, i+1, len);
    
            return Integer.parseInt(String.valueOf(digits));
        }
    
        /**
         * 二分
         * @param n
         * @return
         */
        private int solution4(int n){
            char[] digits = String.valueOf(n).toCharArray();
            int len = digits.length;
    
            // 找到待交换位置
            int i;
            for(i=len-2; i>=0; i--){
                if(digits[i] < digits[i+1]){
                    break;
                }
            }
            if(i < 0){
                return -1;
            }
    
            // 二分 i右边已经降序
            int left = i+1;
            int right = len-1;
            int mid;
            while(left <= right){
                mid = left+((right-left)>>1);
                // right最终指向第一个大于target(digits[i])的数(从右向左)
                if(digits[mid] <= digits[i]){
                    right = mid-1;
                }else{
                    left = mid+1;
                }
            }
            swap(digits, i, right);
            
            String pre = String.valueOf(digits).substring(0,i+1);
            // 区间反转reverse
            String last = new StringBuilder(String.valueOf(digits).substring(i+1)).reverse().toString();
            
            return Integer.parseInt(pre+last);
        }
    
        /**
         * 二分
         * @param n
         * @return
         */
        private int solution5(int n){
            char[] digits = String.valueOf(n).toCharArray();
            int len = digits.length;
    
            // 找到待交换位置
            int i;
            for(i=len-2; i>=0; i--){
                if(digits[i] < digits[i+1]){
                    break;
                }
            }
            if(i < 0){
                return -1;
            }
    
            // 二分 i右边已经降序
            int left = i+1;
            int right = len-1;
            int mid;
            while(left <= right){
                mid = left+((right-left)>>1);
                // right最终指向第一个大于target(digits[i])的数(从右向左)
                if(digits[mid] <= digits[i]){
                    right = mid-1;
                }else{
                    left = mid+1;
                }
            }
            swap(digits, i, right);
    
            // 区间反转reverse
            reverse(digits, i+1, len-1);
    
            return Integer.parseInt(String.valueOf(digits));
        }
    
        /**
         * 区间反转
         * @param digits
         * @param i
         * @param j
         */
        private void reverse(char[] digits, int i, int j){
            while(i < j){
                swap(digits, i++, j--);
            }
        }
    
        /**
         * 交换
         * @param digits
         * @param i
         * @param j
         */
        private void swap(char[] digits, int i, int j){
            char tmp = digits[i];
            digits[i] = digits[j];
            digits[j] = tmp;
        }
    }

  

