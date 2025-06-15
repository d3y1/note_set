# java-NC37 合并区间


    import java.util.*;
    
    /*
     * public class Interval {
     *   int start;
     *   int end;
     *   public Interval(int start, int end) {
     *     this.start = start;
     *     this.end = end;
     *   }
     * }
     */
    
    /**
     * NC37 合并区间
     * @author d3y1
     */
    public class Solution {
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         *
         * @param intervals Interval类ArrayList
         * @return Interval类ArrayList
         */
        public ArrayList<Interval> merge (ArrayList<Interval> intervals) {
            // return solution1(intervals);
            // return solution2(intervals);
            return solution3(intervals);
        }
    
        /**
         * 排序(最小堆)
         * @param intervals
         * @return
         */
        private ArrayList<Interval> solution1(ArrayList<Interval> intervals){
            int n = intervals.size();
            if(n <= 1){
                return intervals;
            }
    
            PriorityQueue<Interval> minHeap = new PriorityQueue<>((o1, o2) -> (o1.start-o2.start));
            // PriorityQueue<Interval> minHeap = new PriorityQueue<>(new Comparator<Interval>(){
            //     @Override
            //     public int compare(Interval o1, Interval o2){
            //         return o1.start-o2.start;
            //     }
            // });
            for(Interval interval: intervals){
                minHeap.offer(interval);
            }
    
            ArrayList<Interval> list = new ArrayList<Interval>();
            Interval out = minHeap.poll();
            Interval top;
            while(!minHeap.isEmpty()){
                top = minHeap.poll();
                // 可简化
                // if(out.start<=top.start && top.start<=out.end){
                if(top.start <= out.end){
                    out.end = Math.max(out.end, top.end);
                }else{
                    list.add(out);
                    out = top;
                }
            }
            list.add(out);
    
            return list;
        }
    
        /**
         * 排序(数组)
         * @param intervals
         * @return
         */
        private ArrayList<Interval> solution2(ArrayList<Interval> intervals){
            int n = intervals.size();
            if(n <= 1){
                return intervals;
            }
    
            Collections.sort(intervals, (o1, o2) -> (o1.start-o2.start));
    
            ArrayList<Interval> list = new ArrayList<Interval>();
    
            Interval out = intervals.get(0);
            Interval cur;
            for(int i=1; i<n; i++){
                cur = intervals.get(i);
                // 可简化
                // if(out.start<=cur.start && cur.start<=out.end){
                if(cur.start <= out.end){
                    out.end = Math.max(out.end, cur.end);
                }else{
                    list.add(out);
                    out = cur;
                }
            }
            list.add(out);
    
            return list;
        }
    
        /**
         * 排序(TreeMap)
         * @param intervals
         * @return
         */
        private ArrayList<Interval> solution3(ArrayList<Interval> intervals){
            int n = intervals.size();
            if(n <= 1){
                return intervals;
            }
    
            TreeMap<Integer, Integer> startEndMap = new TreeMap<>();
            for(Interval interval: intervals){
                if(startEndMap.containsKey(interval.start)){
                    startEndMap.put(interval.start, Math.max(startEndMap.get(interval.start), interval.end));
                }else{
                    startEndMap.put(interval.start, interval.end);
                }
            }
    
            ArrayList<Interval> list = new ArrayList<Interval>();
    
            Interval cur,out=null;
            for(int start: startEndMap.keySet()){
                cur = new Interval(start, startEndMap.get(start));
                if(out == null){
                    out = cur;
                }else if(cur.start <= out.end){
                    out.end = Math.max(out.end, cur.end);
                }else{
                    list.add(out);
                    out = cur;
                }
            }
            list.add(out);
    
            return list;
        }
    }

  

