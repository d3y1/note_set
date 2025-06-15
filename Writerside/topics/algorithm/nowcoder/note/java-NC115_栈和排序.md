# java-NC115 栈和排序


    import java.util.*;
    
    /**
     * NC115 栈和排序
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 栈排序
         * @param a int整型一维数组 描述入栈顺序
         * @return int整型一维数组
         */
        public int[] solve (int[] a) {
            // return solution1(a);
            // return solution2(a);
            return solution3(a);
        }
    
        /**
         * 模拟法: Stack+TreeSet
         * @param a
         * @return
         */
        private int[] solution1(int[] a){
            int n = a.length;
    
            TreeSet<Integer> treeSet = new TreeSet<>((o1, o2) -> (o2-o1));
            for(int i=n-1; i>=0; i--){
                treeSet.add(a[i]);
                if(a[i] == n){
                    break;
                }
            }
    
            int max = treeSet.pollFirst();
    
            int[] result = new int[n];
            Stack<Integer> stack = new Stack<>();
            int i = 0;
            for(int num: a){
                stack.push(num);
                treeSet.remove(num);
                if(stack.peek() == max){
                    result[i++] = stack.pop();
                    while(!stack.isEmpty() && !treeSet.isEmpty() && stack.peek()>treeSet.first()){
                        result[i++] = stack.pop();
                    }
                    if(!treeSet.isEmpty()){
                        max = treeSet.pollFirst();
                    }
                }
            }
    
            while(!stack.isEmpty()){
                result[i++] = stack.pop();
            }
    
            return result;
        }
    
        /**
         * 模拟法: Stack(简化)
         * @param a
         * @return
         */
        private int[] solution2(int[] a){
            int n = a.length;
            // rMax[i]: i右侧最大值(不包括自身)
            int[] rMax = new int[n];
            int max = a[n-1];
            for(int i=n-2; i>=0; i--){
                max = Math.max(max, a[i+1]);
                rMax[i] = max;
            }
    
            int[] result = new int[n];
            Stack<Integer> stack = new Stack<>();
            for(int i=0,j=0; i<n; i++){
                stack.push(a[i]);
                if(stack.peek() == max){
                    result[j++] = stack.pop();
                    // rMax[n-1]=0 全部弹出
                    while(!stack.isEmpty() && stack.peek()>rMax[i]){
                        result[j++] = stack.pop();
                    }
                    max = rMax[i];
                }
            }
    
            return result;
        }
    
        /**
         * 模拟法: Stack(再简化)
         * @param a
         * @return
         */
        private int[] solution3(int[] a){
            int n = a.length;
            // rMax[i]: i右侧最大值(包括自身)
            int[] rMax = new int[n];
            rMax[n-1] = a[n-1];
            for(int i=n-2; i>=0; i--){
                rMax[i] = Math.max(rMax[i+1], a[i]);
            }
    
            int[] result = new int[n];
            Stack<Integer> stack = new Stack<>();
            int j = 0;
            for(int i=0; i<n; i++){
                while(!stack.isEmpty() && stack.peek()>rMax[i]){
                    result[j++] = stack.pop();
                }
                stack.push(a[i]);
            }
    
            while(!stack.isEmpty()){
                result[j++] = stack.pop();
            }
    
            return result;
        }
    }

  

