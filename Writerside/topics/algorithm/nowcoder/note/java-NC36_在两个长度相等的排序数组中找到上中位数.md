# java-NC36 在两个长度相等的排序数组中找到上中位数


    import java.util.*;
    
    /**
     * NC36 在两个长度相等的排序数组中找到上中位数
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定,请勿修改,直接返回方法规定的值即可
         *
         * 相似 -> 4. 寻找两个正序数组的中位数[<a href="https://***********************************************************n/">...</a>]
         *
         * find median in two sorted array
         * @param arr1 int整型一维数组 the array1
         * @param arr2 int整型一维数组 the array2
         * @return int整型
         */
        public int findMedianinTwoSortedAray (int[] arr1, int[] arr2) {
            // return solution1(arr1, arr2);
            return solution2(arr1, arr2);
            // return solution3(arr1, arr2);
        }
    
        /**
         * 双指针
         * @param arr1
         * @param arr2
         * @return
         */
        private int solution1(int[] arr1, int[] arr2){
            int n = arr1.length;
    
            if(arr1[n-1] <= arr2[0]){
                return arr1[n-1];
            }
            if(arr2[n-1] <= arr1[0]){
                return arr2[n-1];
            }
    
            int count = 0;
            int result = 0;
            int min;
            for(int i=0,j=0; i<n&&j<n;){
                if(arr1[i] < arr2[j]){
                    min = arr1[i];
                    i++;
                }else{
                    min = arr2[j];
                    j++;
                }
                count++;
                if(count == n){
                    result = min;
                    break;
                }
            }
    
            return result;
        }
    
        /**
         * 二分
         *
         * 思路:
         * 要找到第k(k>1)小的元素, 那么就取 mid1=arr1[k/2-1] 和 mid2=arr2[k/2-1] 进行比较
         * arr1 中小于等于 mid1 的元素有 arr1[0 .. k/2-2] 共计 k/2-1 个
         * arr2 中小于等于 mid2 的元素有 arr2[0 .. k/2-2] 共计 k/2-1 个
         * 取 pivot = min(mid1, mid2),两个数组中小于等于 pivot 的元素共计不会超过 (k/2-1) + (k/2-1) <= k-2 个
         * 这样 pivot 本身最大也只能是第 k-1 小的元素
         * 如果 pivot = mid1, 那么 arr1[0 .. k/2-1] 都不可能是第 k 小的元素。把这些元素全部 "删除", 剩下的作为新的 arr1 数组
         * 如果 pivot = mid2, 那么 arr2[0 .. k/2-1] 都不可能是第 k 小的元素。把这些元素全部 "删除", 剩下的作为新的 arr2 数组
         * 由于我们 "删除" 了一些元素（这些元素都比第 k 小的元素要小）, 因此需要修改 k 的值, 减去删除的数的个数
         *
         * @param arr1
         * @param arr2
         * @return
         */
        private int solution2(int[] arr1, int[] arr2){
            int n1 = arr1.length;
            int n2 = arr2.length;
    
            // 第k个数 (第k小的数)
            int k = (n1+n2+1)/2;
            int left1 = 0;
            int left2 = 0;
            int half;
            while(true){
                if(left1 == n1){
                    return arr2[left2+k-1];
                }
                if(left2 == n2){
                    return arr1[left1+k-1];
                }
                if(k == 1){
                    return Math.min(arr1[left1], arr2[left2]);
                }
    
                half = k/2;
                int mid1 = Math.min(left1+half, n1)-1;
                int mid2 = Math.min(left2+half, n2)-1;
                if(arr1[mid1] <= arr2[mid2]){
                    k -= (mid1-left1+1);
                    left1 = mid1+1;
                }else{
                    k -= (mid2-left2+1);
                    left2 = mid2+1;
                }
            }
        }
    
        /**
         * 二分: 划分数组
         *
         * len(pre_part):  前一部分的元素个数
         * len(post_part): 后一部分的元素个数
         *
         * n1+n2为偶数时:
         * 确保
         * (1). len(pre_part)=len(post_part)
         * (2). max(pre_part)≤min(post_part)
         * 则有 上中位数median=max(pre_part)
         *
         * 此时由(1)推得:
         * => i+j=n1−i+n2−j
         * => i+j=(n1+n2)/2
         *
         * n1+n2为奇数时:
         * 确保
         * (1). len(pre_part)=len(post_part)+1
         * (2). max(pre_part)≤min(post_part)
         * 则有 上中位数median=max(pre_part)
         *
         * 此时由(1)推得:
         * => i+j=n1−i+n2−j+1
         * => i+j=(n1+n2+1)/2
         *
         * 可见: 无论(n1+n2)为奇为偶
         * i+j = (n1+n2+1)/2
         * => j= (n1+n2+1)/2 - i  (0<=i<=n1 0<=j<=n2 n1<=n2)
         *
         * @param arr1
         * @param arr2
         * @return
         */
        private int solution3(int[] arr1, int[] arr2){
            // 注意 n1<=n2 -> 确保j>=0
            int n1 = arr1.length;
            int n2 = arr2.length;
            int left = 0, right = n1;
            // preMax:  前一部分的最大值
            // postMin: 后一部分的最小值
            int preMax = 0, postMin = 0;
    
            // 二分
            while (left <= right) {
                // 前一部分包含 arr1[0 .. i-1] 和 arr2[0 .. j-1]
                // 后一部分包含 arr1[i .. n1-1] 和 arr2[j .. n2-1]
                int i = (left+right)/2;
                int j = (n1 + n2 + 1) / 2 - i;
    
                // arr1_i_1, arr1_i, arr2_j_1, arr2_j 分别表示 arr1[i-1], arr1[i], arr2[j-1], arr2[j]
                int arr1_i_1 = (i==0?Integer.MIN_VALUE:arr1[i-1]);
                int arr1_i = (i==n1?Integer.MAX_VALUE:arr1[i]);
                int arr2_j_1 = (j==0?Integer.MIN_VALUE:arr2[j-1]);
                int arr2_j = (j==n2?Integer.MAX_VALUE:arr2[j]);
    
                if (arr1_i_1 <= arr2_j) {
                    preMax = Math.max(arr1_i_1, arr2_j_1);
                    postMin = Math.min(arr1_i, arr2_j);
                    left = i + 1;
                } else {
                    right = i - 1;
                }
            }
    
            return preMax;
        }
    }

  

