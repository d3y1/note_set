# java-QQ2 微信红包


    import java.util.*;
    
    /**
     * QQ2 微信红包
     * @author d3y1
     */
    public class Gift {
        /**
         * 程序入口
         * @param gifts
         * @param n
         * @return
         */
        public int getValue(int[] gifts, int n) {
            int result;
            result = getValue1(gifts, n);
            result = getValue2(gifts, n);
            result = getValue3(gifts, n);
            result = getValue4(gifts, n);
    
            return result;
        }
    
        /**
         * 模拟法: HashMap
         * @param gifts
         * @param n
         * @return
         */
        public int getValue1(int[] gifts, int n) {
            HashMap<Integer, Integer> map = new HashMap<>(n);
    
            int result = 0;
            int value;
            for(int i=0; i<n; i++){
                value = map.getOrDefault(gifts[i], 0)+1;
                if(value > n/2){
                    result = gifts[i];
                    break;
                }
                map.put(gifts[i], value);
            }
    
            return result;
        }
    
        /**
         * 模拟法: 排序(滑动窗口)
         * @param gifts
         * @param n
         * @return
         */
        public int getValue2(int[] gifts, int n) {
            Arrays.sort(gifts);
    
            int gap = n/2;
            int result = 0;
            for(int i=0; i+gap<n; i++){
                if(gifts[i] == gifts[i+gap]){
                    result = gifts[i];
                }
            }
    
            return result;
        }
    
        /**
         * 模拟法: 排序(统计唯一可能候选者)
         * @param gifts
         * @param n
         * @return
         */
        public int getValue3(int[] gifts, int n) {
            Arrays.sort(gifts);
    
            int mid = n/2;
            int candidate = gifts[mid];
    
            int count = 0;
            int result = 0;
            for(int i=0; i<n; i++){
                if(gifts[i] == candidate){
                    if(++count > mid){
                        result = candidate;
                        break;
                    }
                }
            }
    
            return result;
        }
    
        /**
         * 模拟法: 不排序(找到并统计唯一可能候选者)
         * @param gifts
         * @param n
         * @return
         */
        public int getValue4(int[] gifts, int n) {
            int candidate = 0;
            int flag = 0;
    
            // 找到唯一可能候选者candidate
            for(int i=0; i<n; i++){
                if(flag == 0){
                    candidate = gifts[i];
                    flag++;
                }else if(gifts[i] == candidate){
                    flag++;
                }else if(gifts[i] != candidate){
                    flag--;
                }
            }
    
            int count = 0;
            int result = 0;
            for(int i=0; i<n; i++){
                if(gifts[i] == candidate){
                    if(++count > n/2){
                        result = candidate;
                        break;
                    }
                }
            }
    
            return result;
        }
    }

  

