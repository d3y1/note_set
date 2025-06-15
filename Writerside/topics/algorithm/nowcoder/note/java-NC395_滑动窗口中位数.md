# java-NC395 滑动窗口中位数

```java
import java.util.*;

/**
 * NC395 滑动窗口中位数
 * @author d3y1
 */
public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     * <p>
     * 相似 -> NC252 多数组中位数     [nowcoder]
     * 相似 -> NC131 数据流中的中位数  [nowcoder]
     *
     * @param nums int整型ArrayList
     * @param k    int整型
     * @return double浮点型ArrayList
     */
    public ArrayList<Double> slidewindow(ArrayList<Integer> nums, int k) {
        // return solution1(nums, k);
        // return solution2(nums, k);
        return solution3(nums, k);
    }

    /**
     * 双堆+双指针: 超时!
     *
     * @param nums
     * @param k
     * @return
     */
    private ArrayList<Double> solution1(ArrayList<Integer> nums, int k) {
        int n = nums.size();
        if (n < k) {
            return new ArrayList<>();
        }

        ArrayList<Double> list = new ArrayList<>();

        // 双堆
        TwoHeap th = new TwoHeap(k);
        for (int i = 0; i < k; i++) {
            th.addToHeap(nums.get(i));
        }
        list.add(th.getMedian());

        // 双指针
        for (int i = 0, j = k; j < n; i++, j++) {
            th.addToHeap(nums.get(j));
            th.removeFromHeap(nums.get(i));
            list.add(th.getMedian());
        }

        return list;
    }

    /**
     * 双堆
     */
    private class TwoHeap {
        // 大根堆 维护较小的一半元素
        private PriorityQueue<Integer> maxHeap;
        // 小根堆 维护较大的一半元素
        private PriorityQueue<Integer> minHeap;
        // 滑动窗口大小
        private int k;

        public TwoHeap(int k) {
            this.maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
            this.minHeap = new PriorityQueue<>();
            this.k = k;
        }

        private void addToHeap(int num) {
            if (minHeap.size() == maxHeap.size()) {
                minHeap.offer(num);
                maxHeap.offer(minHeap.poll());
            } else {
                maxHeap.offer(num);
                minHeap.offer(maxHeap.poll());
            }
        }

        private void removeFromHeap(int num) {
            if (num <= maxHeap.peek()) {
                if (minHeap.size() == maxHeap.size()) {
                    maxHeap.remove(num);
                    maxHeap.offer(minHeap.poll());
                } else {
                    maxHeap.remove(num);
                }
            } else {
                if (minHeap.size() == maxHeap.size()) {
                    minHeap.remove(num);
                } else {
                    minHeap.remove(num);
                    minHeap.offer(maxHeap.poll());
                }
            }
        }

        /**
         * 获取中位数
         *
         * @return
         */
        private double getMedian() {
            // if(k%2 == 0){
            if ((k & 1) == 0) {
                return (minHeap.peek() + maxHeap.peek()) / 2.0;
            } else {
                return maxHeap.peek();
            }
        }
    }

    //////////////////////////////////////////////////////////////////////////////////////////////

    /**
     * 双堆+双指针+哈希(延迟删除)
     *
     * @param nums
     * @param k
     * @return
     */
    private ArrayList<Double> solution2(ArrayList<Integer> nums, int k) {
        int n = nums.size();
        if (n < k) {
            return new ArrayList<>();
        }

        ArrayList<Double> list = new ArrayList<>();

        // 双堆
        DualHeap dh = new DualHeap(k);
        for (int i = 0; i < k; i++) {
            dh.insert(nums.get(i));
        }
        list.add(dh.getMedian());

        // 双指针
        for (int i = 0, j = k; j < n; i++, j++) {
            dh.insert(nums.get(j));
            dh.delete(nums.get(i));
            list.add(dh.getMedian());
        }

        return list;
    }

    /**
     * 双堆
     */
    private class DualHeap {
        // 大根堆 维护较小的一半元素
        private PriorityQueue<Integer> maxHeap;
        // 小根堆 维护较大的一半元素
        private PriorityQueue<Integer> minHeap;
        // 哈希表 记录「延迟删除」的元素, key 为元素, value 为需要删除的次数
        private Map<Integer, Integer> delayed;
        // 滑动窗口大小
        private int k;
        // maxHeap 和 minHeap 当前包含的元素个数, 需要扣除被「延迟删除」的元素
        private int maxHeapSize, minHeapSize;

        public DualHeap(int k) {
            this.maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
            this.minHeap = new PriorityQueue<>();
            this.delayed = new HashMap<>();
            this.k = k;
            this.maxHeapSize = 0;
            this.minHeapSize = 0;
        }

        /**
         * 获取中位数
         *
         * @return
         */
        public double getMedian() {
            return (k & 1) == 1 ? maxHeap.peek() : (maxHeap.peek() + minHeap.peek()) / 2.0;
        }

        /**
         * 新增元素
         *
         * @param num
         */
        public void insert(int num) {
            if (minHeapSize == maxHeapSize) {
                minHeap.offer(num);
                maxHeap.offer(minHeap.poll());
                ++maxHeapSize;
                prune(minHeap);
            } else {
                maxHeap.offer(num);
                minHeap.offer(maxHeap.poll());
                ++minHeapSize;
                prune(maxHeap);
            }
        }

        /**
         * 假删元素: 哈希表实现(延迟删除)
         *
         * @param num
         */
        public void delete(int num) {
            delayed.put(num, delayed.getOrDefault(num, 0) + 1);
            if (num <= maxHeap.peek()) {
                if (minHeapSize == maxHeapSize) {
                    --maxHeapSize;
                    if (num == maxHeap.peek()) {
                        prune(maxHeap);
                    }
                    maxHeap.offer(minHeap.poll());
                    --minHeapSize;
                    ++maxHeapSize;
                    prune(minHeap);
                } else {
                    --maxHeapSize;
                    if (num == maxHeap.peek()) {
                        prune(maxHeap);
                    }
                }
            } else {
                if (minHeapSize == maxHeapSize) {
                    --minHeapSize;
                    if (num == minHeap.peek()) {
                        prune(minHeap);
                    }
                } else {
                    --minHeapSize;
                    if (num == minHeap.peek()) {
                        prune(minHeap);
                    }
                    minHeap.offer(maxHeap.poll());
                    --maxHeapSize;
                    ++minHeapSize;
                    prune(maxHeap);
                }
            }
        }

        /**
         * 修剪: 真删元素
         * 不断地弹出 heap 的堆顶元素, 并且更新哈希表
         *
         * @param heap
         */
        private void prune(PriorityQueue<Integer> heap) {
            while (!heap.isEmpty()) {
                int num = heap.peek();
                if (delayed.containsKey(num)) {
                    delayed.put(num, delayed.get(num) - 1);
                    if (delayed.get(num) == 0) {
                        delayed.remove(num);
                    }
                    heap.poll();
                } else {
                    break;
                }
            }
        }
    }

    //////////////////////////////////////////////////////////////////////////////////////////////

    /**
     * 双堆+双指针+哈希(延迟删除): 优化
     *
     * @param nums
     * @param k
     * @return
     */
    private ArrayList<Double> solution3(ArrayList<Integer> nums, int k) {
        int n = nums.size();
        if (n < k) {
            return new ArrayList<>();
        }

        ArrayList<Double> list = new ArrayList<>();

        // 双堆
        DoubleHeap dh = new DoubleHeap(k);
        for (int i = 0; i < k; i++) {
            dh.insert(nums.get(i));
        }
        list.add(dh.getMedian());

        // 双指针
        for (int i = 0, j = k; j < n; i++, j++) {
            dh.insert(nums.get(j));
            dh.delete(nums.get(i));
            list.add(dh.getMedian());
        }

        return list;
    }

    /**
     * 双堆
     */
    private class DoubleHeap {
        // 大根堆 维护较小的一半元素
        private PriorityQueue<Integer> maxHeap;
        // 小根堆 维护较大的一半元素
        private PriorityQueue<Integer> minHeap;
        // 哈希表, 记录「延迟删除」的元素, key 为元素，value 为需要删除的次数
        private Map<Integer, Integer> delayed;
        // 滑动窗口大小
        private int k;
        // maxHeap 和 minHeap 当前包含的元素个数, 需要扣除被「延迟删除」的元素
        private int maxHeapSize, minHeapSize;

        public DoubleHeap(int k) {
            this.maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
            this.minHeap = new PriorityQueue<>();
            this.delayed = new HashMap<>();
            this.k = k;
            this.maxHeapSize = 0;
            this.minHeapSize = 0;
        }

        /**
         * 获取中位数
         *
         * @return
         */
        public double getMedian() {
            return (k & 1) == 1 ? maxHeap.peek() : (maxHeap.peek() + minHeap.peek()) / 2.0;
        }

        /**
         * 新增元素
         *
         * @param num
         */
        public void insert(int num) {
            if (maxHeap.isEmpty() || num <= maxHeap.peek()) {
                maxHeap.offer(num);
                ++maxHeapSize;
            } else {
                minHeap.offer(num);
                ++minHeapSize;
            }

            balance();
        }

        /**
         * 假删元素: 哈希表实现(延迟删除)
         *
         * @param num
         */
        public void delete(int num) {
            delayed.put(num, delayed.getOrDefault(num, 0) + 1);
            if (num <= maxHeap.peek()) {
                --maxHeapSize;
                if (num == maxHeap.peek()) {
                    prune(maxHeap);
                }
            } else {
                --minHeapSize;
                if (num == minHeap.peek()) {
                    prune(minHeap);
                }
            }

            balance();
        }

        /**
         * 修剪: 真删元素
         * 不断地弹出 heap 的堆顶元素, 并且更新哈希表
         *
         * @param heap
         */
        private void prune(PriorityQueue<Integer> heap) {
            while (!heap.isEmpty()) {
                int num = heap.peek();
                if (delayed.containsKey(num)) {
                    delayed.put(num, delayed.get(num) - 1);
                    if (delayed.get(num) == 0) {
                        delayed.remove(num);
                    }
                    heap.poll();
                } else {
                    break;
                }
            }
        }

        /**
         * 平衡双堆
         * 调整 maxHeap 和 minHeap 中的元素个数, 使得二者的元素个数满足要求:
         * maxHeapSize = minHeapSize + 1
         * 或者
         * maxHeapSize = minHeapSize
         */
        private void balance() {
            if (maxHeapSize > minHeapSize + 1) {
                // maxHeap 比 minHeap 元素多 2 个
                minHeap.offer(maxHeap.poll());
                --maxHeapSize;
                ++minHeapSize;
                // 上面 maxHeap 堆顶元素被移除, 需要进行 prune
                prune(maxHeap);
            } else if (maxHeapSize < minHeapSize) {
                // minHeap 比 maxHeap 元素多 1 个
                maxHeap.offer(minHeap.poll());
                ++maxHeapSize;
                --minHeapSize;
                // 上面 minHeap 堆顶元素被移除，需要进行 prune
                prune(minHeap);
            }
        }
    }
}
```
