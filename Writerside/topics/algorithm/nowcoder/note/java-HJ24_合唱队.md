# java-HJ24 合唱队


    import java.util.Scanner;
    
    // 注意类名必须为 Main, 不要有任何 package xxx 信息
    public class Main {
        /**
         * 动态规划
         * @param args
         */
        public static void main(String[] args) {
            Scanner sc = new Scanner(System.in);
            while (sc.hasNext()) {
                int n = sc.nextInt();
                int[] arr = new int[n];
                for (int i = 0; i < n; i++) {
                    arr[i] = sc.nextInt();
                }
    
                //存储每个数左边小于其的数的个数
                int[] left = new int[n];
                //存储每个数右边小于其的数的个数
                int[] right = new int[n];
                //最左边的数设为1
                left[0] = 1;
                //最右边的数设为1
                right[n - 1] = 1;
                //计算每个位置左侧的最长递增
                for (int i = 0; i < n; i++) {
                    left[i] = 1;
                    for (int j = 0; j < i; j++) {
                        //动态规划
                        if (arr[i] > arr[j]) {
                            left[i] = Math.max(left[j] + 1, left[i]);
                        }
                    }
                }
                //计算每个位置右侧的最长递减
                for (int i = n - 1; i >= 0; i--) {
                    right[i] = 1;
                    for (int j = n - 1; j > i; j--) {
                        //动态规划
                        if (arr[i] > arr[j]) {
                            right[i] = Math.max(right[i], right[j] + 1);
                        }
                    }
                }
                // 记录每个位置的值
                int[] result = new int[n];
                for (int i = 0; i < n; i++) {
                    //位置 i计算了两次 所以需要－1
                    //两个都包含本身
                    result[i] = left[i] + right[i] - 1;
                }
    
                //找到最大的满足要求的值
                int max = 1;
                for (int i = 0; i < n; i++) {
                    max = Math.max(result[i],max);
                }
                System.out.println(n - max);
            }
        }
    
    
    
    //    /**
    //     * 二分查找
    //     * @param args
    //     */
    //    public static void main(String[] args) {
    //        Scanner sc = new Scanner(System.in);
    //        while (sc.hasNext()) {
    //            int n = sc.nextInt();
    //            int[] arr = new int[n];
    //            for (int i = 0; i < n; i++) {
    //                arr[i] = sc.nextInt();
    //            }
    //
    //            //存储每个数左边小于其的数的个数
    //            int[] left = new int[n];
    //            //存储每个数右边小于其的数的个数
    //            int[] right = new int[n];
    //            left[0] = arr[0];
    //            right[n - 1] = arr[n - 1];
    //            //记录以i为终点的从左向右和从右向走的子序列元素个数
    //            int[] num = new int[n];
    //            //记录当前子序列的长度
    //            int index = 1;
    //            for (int i = 1; i < n; i++) {
    //                if (arr[i] > left[index - 1]) {
    //                    //直接放在尾部
    //                    //i左侧元素个数
    //                    num[i] = index;
    //                    //更新递增序列
    //                    left[index++] = arr[i];
    //                } else {
    //                    //找到当前元素应该放在的位置
    //                    int low = 0, high = index - 1;
    //                    while (low < high) {
    //                        int mid = (low + high) / 2;
    //                        if (left[mid] < arr[i]) {
    //                            low = mid + 1;
    //                        } else {
    //                            high = mid;
    //                        }
    //                    }
    //                    //将所属位置替换为当前元素
    //                    left[low] = arr[i];
    //                    //当前位置i的左侧元素个数
    //                    num[i] = low;
    //                }
    //            }
    //            index = 1;
    //            for (int i = n - 2; i >= 0; i--) {
    //                if (arr[i] > right[index - 1]) {
    //                    num[i] += index;
    //                    right[index++] = arr[i];
    //                } else {
    //                    int low = 0, high = index - 1;
    //                    while (low < high) {
    //                        int mid = (high + low) / 2;
    //                        if (right[mid] < arr[i]) {
    //                            low = mid + 1;
    //                        } else {
    //                            high = mid;
    //                        }
    //                    }
    //                    right[low] = arr[i];
    //                    num[i] += low;
    //                }
    //            }
    //            int max = 1;
    //            for (int number : num) {
    //                max = Math.max(max, number);
    //            }
    //            // max+1为最大的k
    //            System.out.println(n - max);
    //        }
    //    }
    }

  

