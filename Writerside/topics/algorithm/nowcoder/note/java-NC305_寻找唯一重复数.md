# java-NC305 寻找唯一重复数

```java
import java.util.*;

/**
 * NC305 寻找唯一重复数
 * @author d3y1
 */
public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 相似 -> NC3 链表中环的入口结点 [nowcoder]
     *
     * @param nums int整型ArrayList
     * @return int整型
     */
    public int findRepeatNum (ArrayList<Integer> nums) {
        // return solution1(nums);
        // return solution2(nums);
        // return solution3(nums);
        // return solution4(nums);
        // return solution44(nums);
        return solution5(nums);
        // return solution6(nums);
    }

    /**
     * 遍历统计
     * @param nums
     * @return
     */
    private int solution1(ArrayList<Integer> nums){
        int n = nums.size();

        int[] cnt = new int[n+1];

        int result = 0;
        for(int num: nums){
            if(cnt[num] == 0){
                cnt[num]++;
            }else{
                result = num;
                break;
            }
        }

        return result;
    }

    /**
     * 二分: 需要先排序(升序)
     *
     * 测试用例9 数据有问题! -> 此时n=100000, 数组中所有数字都应在区间[1,n-1]内(即最大值为99999), 提供的数据中有100000!
     *
     *      i  0 1 2 3 4
     * nums[i] 4 2 1 3 3
     *
     * l: left
     * m: mid
     * r: right
     *                l   m   r
     *             i  0 1 2 3 4
     * sorted nums[i] 1 2 3 3 4
     *
     * @param nums
     * @return
     */
    private int solution2(ArrayList<Integer> nums){
        int n = nums.size();

        Collections.sort(nums);

        int left = 0;
        int right = n-1;
        int mid;
        while(left <= right){
            // mid = (left+right)/2;
            mid = left+(right-left)/2;
            if(nums.get(mid) > mid){
                left = mid+1;
            }else{
                right = mid-1;
            }
        }

        return nums.get(left);
    }

    /**
     * 二分
     *
     * 测试用例9 数据有问题! -> 此时n=100000, 数组中所有数字都应在区间[1,n-1]内(即最大值为99999), 提供的数据中有100000!
     *
     * cnt[i]表示nums数组中小于等于i的数的个数
     *
     * 假设重复的数是target, 那么[1,target)里的所有数满足cnt[i]≤i, [target,n-1]里的所有数满足cnt[i]>i, 具有单调性
     *
     *      i  0 1 2 3 4
     * nums[i] 4 2 1 3 3
     *
     * l: left
     * m: mid
     * r: right
     *     l m   r
     * num 1 2 3 4
     * cnt 1 2 4 5
     *
     * @param nums
     * @return
     */
    private int solution3(ArrayList<Integer> nums){
        int n = nums.size();

        int result = -1;
        int left = 1;
        int right = n-1;
        int mid;
        while(left <= right){
            // mid = (left+right)>>1;
            mid = left+((right-left)>>1);
            int cnt = 0;
            for(int num: nums){
                if(num <= mid){
                    cnt++;
                }
            }
            if(cnt <= mid){
                left = mid+1;
            }else{
                result = mid;
                right = mid-1;
            }
        }

        return result;
    }

    /**
     * 二进制: 位运算
     *
     * 测试用例9 数据有问题! -> 此时n=100000, 数组中所有数字都应在区间[1,n-1]内(即最大值为99999), 提供的数据中有100000!
     *
     * 错误用例! -> n=10 最大值只能9
     * input: [1, 2, 2, 2, 4, 6, 7, 8, 9, 10]
     * output: 10
     *
     * 正确用例
     * input:[1, 2, 2, 2, 4, 5, 6, 7, 8, 9]
     * output: 2
     *
     * -----------------------------------------------------------
     *
     * 考虑第i位
     * x: nums数组中所有数二进制展开后第i位为1的个数
     * y: 区间[1,n-1]中n-1个数二进制展开后第i位为1的个数
     * 那么重复的数target第i位为1 当且仅当 x>y
     *
     * 考虑重复2次情况:
     *      i  0  1  2  3  4
     * nums[i] 4  2  1  3  3  x  y  target(011)=3
     *   第0位  0  0  1  1  1  3  2  1 (x>y)
     *   第1位  0  1  0  1  1  3  2  1 (x>y)
     *   第2位  1  0  0  0  0  1  1  0 (x=y)
     *
     * 容易理解, 重复的数target第i位为1 当且仅当 x>y
     *
     *
     * 考虑重复多次情况(>=3次): 重复2次 + 替换剩余次数(替换成target)
     * target第i位为1时
     * 每次替换后只会使x不变或增大
     * target第i位为0时
     * 每次替换后只会使x不变或减小
     *      i  0  1  2  3  4
     * nums[i] 3  2  1  3  3  x  y  target(011)=3
     *   第0位  1  0  1  1  1  4  2  1 (x>y)
     *   第1位  1  1  0  1  1  4  2  1 (x>y)
     *   第2位  0  0  0  0  0  0  1  0 (x<y)
     *
     * 可见, 重复的数target第i位为1 当且仅当 x>y
     * 因此我们只要按位还原这个重复的数即可
     *
     * @param nums
     * @return
     */
    private int solution4(ArrayList<Integer> nums){
        int n = nums.size();
        int result = 0;

        int maxBits = 31;
        // 确定所需最终位数 最大数n-1
        while(((n-1)>>maxBits) == 0){
            maxBits -= 1;
        }

        for(int bit=0; bit<=maxBits; bit++){
            int x=0, y=0;
            for(int i=0; i<n; ++i){
                if((nums.get(i)&(1<<bit)) != 0){
                    x += 1;
                }
                if(i>=1 && ((i&(1<<bit))!=0)){
                    y += 1;
                }
            }
            if(x > y){
                result |= 1<<bit;
            }
        }

        return result;
    }

    /**
     * 二进制: 位运算
     *
     * 测试用例9 数据有问题! -> 此时n=100000, 数组中所有数字都应在区间[1,n-1]内(即最大值为99999), 提供的数据中有100000!
     *
     * @param nums
     * @return
     */
    private int solution44(ArrayList<Integer> nums){
        int n = nums.size();
        int result = 0;

        int maxBits = 31;
        // 确定所需最终位数 最大数n-1
        while(((n-1)>>maxBits) == 0){
            maxBits -= 1;
        }

        for(int bit=0; bit<=maxBits; bit++){
            int x=0, y=0;
            for(int i=0; i<n; ++i){
                if(((nums.get(i)>>bit)&1) == 1){
                    x += 1;
                }
                if(i>=1 && (((i>>bit)&1)==1)){
                    y += 1;
                }
            }
            if(x > y){
                result |= 1<<bit;
            }
        }

        return result;
    }

    /**
     * 双指针: 快慢指针
     *
     * 转化为有向环图, 更容易理解!
     *
     * Floyd判圈算法(又称龟兔赛跑算法): 检测链表是否有环的算法
     *
     * 对nums数组建图, 每个位置i连一条i→nums[i]的边;
     * 由于存在的重复的数字target, 因此target这个位置一定有起码两条指向它的边, 因此整张图一定存在环, 且我们要找到的target就是这个环的入口
     *
     * 先设置慢指针slow和快指针fast, 慢指针每次走一步, 快指针每次走两步
     * 根据Floyd判圈算法, 两个指针在有环的情况下一定会相遇,
     * 此时我们再将slow放置起点0, 两个指针每次同时移动一步, 相遇的点就是答案
     *
     * @param nums
     * @return
     */
    private int solution5(ArrayList<Integer> nums){
        int slow = 0;
        int fast = 0;
        do{
            slow = nums.get(slow);
            fast = nums.get(nums.get(fast));
        }while(slow != fast);

        slow = 0;
        while(slow != fast){
            slow = nums.get(slow);
            fast = nums.get(fast);
        }

        return slow;
    }

    /**
     * 原地哈希
     * @param nums
     * @return
     */
    private int solution6(ArrayList<Integer> nums){
        for(int num: nums){
            // 若第二次进入(根据|num|), 必为负值 -> 此时该|num|重复, 返回|num|即可
            if(nums.get(Math.abs(num)) < 0){
                return Math.abs(num);
            }
            nums.set(Math.abs(num), -nums.get(Math.abs(num)));
        }

        return -1;
    }
}
```
