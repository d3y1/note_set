# java-NC348 四数之和


    import java.util.*;
    
    /**
     * NC348 四数之和
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 相似 -> NC247 最接近的三数之和 [nowcoder]
         *
         * @param nums int整型ArrayList
         * @param target int整型
         * @return int整型ArrayList<ArrayList<>>
         */
        public ArrayList<ArrayList<Integer>> fournumber (ArrayList<Integer> nums, int target) {
            // return solution1(nums, target);
            return solution2(nums, target);
            // return solution3(nums, target);
        }
    
        /**
         * 排序+四指针(固二动二)
         * @param nums
         * @param target
         * @return
         */
        private ArrayList<ArrayList<Integer>> solution1(ArrayList<Integer> nums, int target){
            int n = nums.size();
    
            // 排序
            Collections.sort(nums);
    
            ArrayList<ArrayList<Integer>> result = new ArrayList<>();
            ArrayList<Integer> list;
            HashSet<ArrayList<Integer>> set = new HashSet<>();
    
            int p,q;
            int sum;
            // 固二: i j
            for(int i=0; i<n; i++){
                for(int j=i+1; j<n; j++){
                    p = j+1;
                    q = n-1;
                    // 动二: p q
                    while(p < q){
                        sum = nums.get(i)+nums.get(j)+nums.get(p)+nums.get(q);
                        if(sum < target){
                            p++;
                        }else if(sum > target){
                            q--;
                        }else{
                            list = new ArrayList<>();
                            list.add(nums.get(i));
                            list.add(nums.get(j));
                            list.add(nums.get(p));
                            list.add(nums.get(q));
                            // 去重
                            set.add(list);
                            // 去重
                            while(++p < q){
                                if(!nums.get(p).equals(nums.get(p-1))){
                                    break;
                                }
                            }
                            // 去重
                            while(p < --q){
                                if(!nums.get(q).equals(nums.get(q+1))){
                                    break;
                                }
                            }
                        }
                    }
                }
            }
    
            result.addAll(set);
    
            return result;
        }
    
        /**
         * 排序+四指针(固二动二)
         * @param nums
         * @param target
         * @return
         */
        private ArrayList<ArrayList<Integer>> solution2(ArrayList<Integer> nums, int target){
            int n = nums.size();
    
            // 排序
            Collections.sort(nums);
    
            ArrayList<ArrayList<Integer>> result = new ArrayList<>();
            ArrayList<Integer> list;
    
            int p,q;
            int sum;
            // 固二: i j
            for(int i=0; i<n; i++){
                // 去重
                if(i>0 && nums.get(i).equals(nums.get(i-1))){
                    continue;
                }
                for(int j=i+1; j<n; j++){
                    // 去重
                    if(j>i+1 && nums.get(j).equals(nums.get(j-1))){
                        continue;
                    }
                    p = j+1;
                    q = n-1;
                    // 动二: p q
                    while(p < q){
                        sum = nums.get(i)+nums.get(j)+nums.get(p)+nums.get(q);
                        if(sum < target){
                            p++;
                        }else if(sum > target){
                            q--;
                        }else{
                            list = new ArrayList<>();
                            list.add(nums.get(i));
                            list.add(nums.get(j));
                            list.add(nums.get(p));
                            list.add(nums.get(q));
                            result.add(list);
                            // 去重
                            while(++p < q){
                                if(!nums.get(p).equals(nums.get(p-1))){
                                    break;
                                }
                            }
                            // 去重
                            while(p < --q){
                                if(!nums.get(q).equals(nums.get(q+1))){
                                    break;
                                }
                            }
                        }
                    }
                }
            }
    
            return result;
        }
    
        /**
         * 排序+四指针(固二动二)
         * @param nums
         * @param target
         * @return
         */
        private ArrayList<ArrayList<Integer>> solution3(ArrayList<Integer> nums, int target){
            int n = nums.size();
    
            // 排序
            Collections.sort(nums);
    
            ArrayList<ArrayList<Integer>> result = new ArrayList<>();
            ArrayList<Integer> list;
    
            int p,q;
            int sum;
            // 固二: i j
            for(int i=0; i<n; i++){
                // 去重
                if(i>0 && nums.get(i).equals(nums.get(i-1))){
                    continue;
                }
                for(int j=i+1; j<n; j++){
                    // 去重
                    if(j>i+1 && nums.get(j).equals(nums.get(j-1))){
                        continue;
                    }
                    p = j+1;
                    q = n-1;
                    // 动二: p q
                    while(p < q){
                        // 去重
                        while(p>j+1 && p<n && nums.get(p).equals(nums.get(p-1))){
                            p++;
                        }
                        if(p >= q){
                            break;
                        }
                        sum = nums.get(i)+nums.get(j)+nums.get(p)+nums.get(q);
                        if(sum < target){
                            p++;
                        }else if(sum > target){
                            q--;
                        }else{
                            list = new ArrayList<>();
                            list.add(nums.get(i));
                            list.add(nums.get(j));
                            list.add(nums.get(p));
                            list.add(nums.get(q));
                            result.add(list);
                            p++;
                        }
                    }
                }
            }
    
            return result;
        }
    }

  

