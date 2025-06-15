# java-NC27 集合的所有子集(一)


    import java.util.*;
    
    /**
     * NC27 集合的所有子集(一)
     * @author d3y1
     */
    public class Solution {
        private ArrayList<Integer> list = new ArrayList<>();
        private ArrayList<ArrayList<Integer>> result = new ArrayList<>();
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         * 
         * 相似 -> NC221 集合的所有子集(二) [nowcoder]
         *
         * @param S int整型一维数组 
         * @return int整型ArrayList<ArrayList<>>
         */
        public ArrayList<ArrayList<Integer>> subsets (int[] S) {
            // return solution1(S);
            // return solution11(S);
            // return solution111(S);
            // return solution1111(S);
            return solution11111(S);
            // return solution2(S);
            // return solution22(S);
            // return solution222(S);
            // return solution3(S);
            // return solution33(S);
        }
    
        // /**
        //  * 位运算
        //  * @param S
        //  * @return
        //  */
        // private ArrayList<ArrayList<Integer>> solution1(int[] S){
        //     int n = S.length;
        //     if(n == 0){
        //         return new ArrayList<>();
        //     }
    
        //     Arrays.sort(S);
    
        //     ArrayList<Integer> list;
        //     StringBuilder binStr;
        //     for(int i=0; i<Math.pow(2,n); i++){
        //         binStr = new StringBuilder(Integer.toBinaryString(i));
        //         while(binStr.length() < n){
        //             binStr.insert(0,'0');
        //         }
        //         list = new ArrayList<>();
        //         for(int j=0; j<n; j++){
        //             if(binStr.charAt(j) == '1'){
        //                 list.add(S[j]);
        //             }
        //         }
        //         result.add(list);
        //     }
    
        //     return result;
        // }
    
        /**
         * 位运算
         * @param S
         * @return
         */
        private ArrayList<ArrayList<Integer>> solution11(int[] S){
            int n = S.length;
            if(n == 0){
                return new ArrayList<>();
            }
    
            Arrays.sort(S);
    
            ArrayList<Integer> list;
            for(int i=0; i<Math.pow(2,n); i++){
                list = new ArrayList<>();
                for(int j=0; j<n; j++){
                    if(((i>>j)&1) == 1){
                        list.add(S[j]);
                    }
                }
                result.add(list);
            }
    
            return result;
        }
    
        /**
         * 位运算
         * @param S
         * @return
         */
        private ArrayList<ArrayList<Integer>> solution111(int[] S){
            int n = S.length;
            if(n == 0){
                return new ArrayList<>();
            }
    
            Arrays.sort(S);
    
            ArrayList<Integer> list = new ArrayList<>();
            for(int i=0; i<Math.pow(2,n); i++){
                list.clear();
                for(int j=0; j<n; j++){
                    if(((i>>j)&1) == 1){
                        list.add(S[j]);
                    }
                }
                result.add(new ArrayList<>(list));
            }
    
            return result;
        }
    
        /**
         * 位运算
         * @param S
         * @return
         */
        private ArrayList<ArrayList<Integer>> solution1111(int[] S){
            int n = S.length;
            if(n == 0){
                return new ArrayList<>();
            }
    
            Arrays.sort(S);
    
            for(int mask=0; mask<(1<<n); mask++){
                list.clear();
                for(int j=0; j<n; j++){
                    if(((mask>>j)&1) == 1){
                        list.add(S[j]);
                    }
                }
                result.add(new ArrayList<>(list));
            }
    
            return result;
        }
    
        /**
         * 位运算
         * @param S
         * @return
         */
        private ArrayList<ArrayList<Integer>> solution11111(int[] S){
            int n = S.length;
            if(n == 0){
                return new ArrayList<>();
            }
    
            Arrays.sort(S);
    
            for(int mask=0; mask<(1<<n); mask++){
                list.clear();
                for(int j=0; j<n; j++){
                    if((mask&(1<<j)) != 0){
                        list.add(S[j]);
                    }
                }
                result.add(new ArrayList<>(list));
            }
    
            return result;
        }
    
        /**
         * 回溯法
         * @param S
         * @return
         */
        private ArrayList<ArrayList<Integer>> solution2(int[] S){
            int n = S.length;
            if(n == 0){
                return new ArrayList<>();
            }
    
            Arrays.sort(S);
            backtrack2(S, 0, new ArrayList<>());
    
            return result;
        }
    
        /**
         * 回溯: 递归遍历解空间
         * @param S
         * @param idx
         * @param list
         */
        private void backtrack2(int[] S, int idx, ArrayList<Integer> list){
            result.add(list);
            ArrayList<Integer> newList;
            for(int i=idx; i<S.length; i++){
                newList = new ArrayList<>(list);
                newList.add(S[i]);
                backtrack2(S, i+1, newList);
            }
        }
    
        /**
         * 回溯法
         * @param S
         * @return
         */
        private ArrayList<ArrayList<Integer>> solution22(int[] S){
            int n = S.length;
            if(n == 0){
                return new ArrayList<>();
            }
    
            Arrays.sort(S);
            backtrack22(S, 0, new ArrayList<>());
    
            return result;
        }
    
        /**
         * 回溯: 递归遍历解空间
         * @param S
         * @param idx
         * @param list
         */
        private void backtrack22(int[] S, int idx, ArrayList<Integer> list){
            result.add(new ArrayList<>(list));
            for(int i=idx; i<S.length; i++){
                list.add(S[i]);
                backtrack22(S, i+1, list);
                list.remove(list.size()-1);
            }
        }
    
        /**
         * 回溯法
         * @param S
         * @return
         */
        private ArrayList<ArrayList<Integer>> solution222(int[] S){
            int n = S.length;
            if(n == 0){
                return new ArrayList<>();
            }
    
            Arrays.sort(S);
            backtrack222(S, 0);
    
            return result;
        }
    
        /**
         * 回溯: 递归遍历解空间
         * @param S
         * @param idx
         */
        private void backtrack222(int[] S, int idx){
            result.add(new ArrayList<>(list));
            for(int i=idx; i<S.length; i++){
                list.add(S[i]);
                backtrack222(S, i+1);
                list.remove(list.size()-1);
            }
        }
    
        /**
         * 回溯法
         * @param S
         * @return
         */
        private ArrayList<ArrayList<Integer>> solution3(int[] S){
            int n = S.length;
            if(n == 0){
                return new ArrayList<>();
            }
    
            Arrays.sort(S);
            backtrack3(S, 0);
    
            return result;
        }
    
        /**
         * 回溯: 递归遍历解空间
         * @param S
         * @param idx
         */
        private void backtrack3(int[] S, int idx){
            if(idx == S.length) {
                result.add(new ArrayList<Integer>(list));
                return;
            }
    
            list.add(S[idx]);
            backtrack3(S, idx+1);
            list.remove(list.size()-1);
            backtrack3(S, idx+1);
        }
    
        /**
         * 回溯法
         * @param S
         * @return
         */
        private ArrayList<ArrayList<Integer>> solution33(int[] S){
            int n = S.length;
            if(n == 0){
                return new ArrayList<>();
            }
    
            Arrays.sort(S);
            backtrack33(S, 0);
    
            return result;
        }
    
        /**
         * 回溯: 递归遍历解空间
         * @param S
         * @param idx
         */
        private void backtrack33(int[] S, int idx){
            if(idx == S.length) {
                result.add(new ArrayList<Integer>(list));
                return;
            }
    
            backtrack33(S, idx+1);
            list.add(S[idx]);
            backtrack33(S, idx+1);
            list.remove(list.size()-1);
        }
    }

  

