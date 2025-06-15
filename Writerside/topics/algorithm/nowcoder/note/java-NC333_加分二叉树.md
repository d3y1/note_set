# java-NC333 加分二叉树

```java
import java.util.*;

/**
 * NC333 加分二叉树
 * @author d3y1
 */
public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     *
     * @param scores int整型ArrayList
     * @return int整型ArrayList<ArrayList<>>
     */
    public ArrayList<ArrayList<Integer>> scoreTree (ArrayList<Integer> scores) {
        return solution1(scores);
        // return solution2(scores);
    }

    /**
     * 动态规划 + 滑动窗口
     *
     * dp[i][j]表示节点区间[i,j]所能获得的最高加分
     * root[i][j]表示节点区间[i,j]获得最高加分时的根节点编号
     *
     *            { scores.get(i-1)                       , i=j
     * dp[i][j] = {     { dp[k][k]+dp[k+1][j]             , i<j && k=i
     *            { max { dp[k][k]+dp[i][k-1]             , i<j && k=j
     *            {     { dp[k][k]+dp[i][k-1]*dp[k+1][j]  , i<j && i<k<j
     *
     * @param scores
     * @return
     */
    private ArrayList<ArrayList<Integer>> solution1(ArrayList<Integer> scores){
        int n = scores.size();

        int[][] root = new int[n+1][n+1];
        int[][] dp = new int[n+1][n+1];

        int score;
        // 滑动窗口
        for(int gap=0; gap<n; gap++){
            for(int i=1,j=i+gap; j<=n; i++,j++){
                if(gap == 0){
                    dp[i][j] = scores.get(i-1);
                    root[i][j] = i;
                }else{
                    for(int k=i; k<=j; k++){
                        if(k == i){
                            score = dp[k][k]+dp[k+1][j];
                            if(score > dp[i][j]){
                                dp[i][j] = score;
                                root[i][j] = k;
                            }
                        }else if(k == j){
                            score = dp[k][k]+dp[i][k-1];
                            if(score > dp[i][j]){
                                dp[i][j] = score;
                                root[i][j] = k;
                            }
                        }else{
                            score = dp[k][k]+dp[i][k-1]*dp[k+1][j];
                            if(score > dp[i][j]){
                                dp[i][j] = score;
                                root[i][j] = k;
                            }
                        }
                    }
                }
            }
        }

        ArrayList<ArrayList<Integer>> result = new ArrayList<>();
        ArrayList<Integer> maxScore = new ArrayList<>();
        ArrayList<Integer> seq;

        maxScore.add(dp[1][n]);
        result.add(maxScore);

        seq = preOrder(root, 1, n, new ArrayList<>());
        result.add(seq);

        return result;
    }

    /**
     * 前序遍历
     * @param range
     * @param left
     * @param right
     * @param seq
     * @return
     */
    private ArrayList<Integer> preOrder(int[][] range, int left, int right, ArrayList<Integer> seq){
        if(left > right){
            return new ArrayList<>();
        }
        int root = range[left][right];
        seq.add(root);
        preOrder(range, left, root-1, seq);
        preOrder(range, root+1, right, seq);

        return seq;
    }

    /**
     * 动态规划 + 滑动窗口
     *
     * dp[i][j]表示节点区间[i,j]所能获得的最高加分
     *
     * map.put(key, value)
     *   key: i+","+j -> 表示节点区间[i,j]
     * value: seq     -> 表示节点区间[i,j]获得最高加分时的前序遍历顺序
     *
     *            { scores.get(i-1)                       , i=j
     * dp[i][j] = {     { dp[k][k]+dp[k+1][j]             , i<j && k=i
     *            { max { dp[k][k]+dp[i][k-1]             , i<j && k=j
     *            {     { dp[k][k]+dp[i][k-1]*dp[k+1][j]  , i<j && i<k<j
     *
     * @param scores
     * @return
     */
    private ArrayList<ArrayList<Integer>> solution2(ArrayList<Integer> scores){
        int n = scores.size();

        HashMap<String, ArrayList<Integer>> map = new HashMap<>();
        int[][] dp = new int[n+1][n+1];

        int score;
        String key;
        ArrayList<Integer> seq;
        // 滑动窗口
        for(int gap=0; gap<n; gap++){
            for(int i=1,j=i+gap; j<=n; i++,j++){
                key = i+","+j;
                if(gap == 0){
                    dp[i][j] = scores.get(i-1);
                    seq = new ArrayList<>();
                    seq.add(i);
                    map.put(key, seq);
                }else{
                    for(int k=i; k<=j; k++){
                        if(k == i){
                            score = dp[k][k]+dp[k+1][j];
                            if(score > dp[i][j]){
                                dp[i][j] = score;
                                seq = new ArrayList<>();
                                seq.addAll(map.get(k+","+k));
                                seq.addAll(map.get((k+1)+","+j));
                                map.put(key, seq);
                            }
                        }else if(k == j){
                            score = dp[k][k]+dp[i][k-1];
                            if(score > dp[i][j]){
                                dp[i][j] = score;
                                seq = new ArrayList<>();
                                seq.addAll(map.get(k+","+k));
                                seq.addAll(map.get(i+","+(k-1)));
                                map.put(key, seq);
                            }
                        }else{
                            score = dp[k][k]+dp[i][k-1]*dp[k+1][j];
                            if(score > dp[i][j]){
                                dp[i][j] = score;
                                seq = new ArrayList<>();
                                seq.addAll(map.get(k+","+k));
                                seq.addAll(map.get(i+","+(k-1)));
                                seq.addAll(map.get((k+1)+","+j));
                                map.put(key, seq);
                            }
                        }
                    }
                }
            }
        }

        ArrayList<ArrayList<Integer>> result = new ArrayList<>();
        ArrayList<Integer> maxScore = new ArrayList<>();
        maxScore.add(dp[1][n]);
        result.add(maxScore);
        result.add(map.get(1+","+n));

        return result;
    }
}
```
