# java-NC352 矩阵置零_2

```java
import java.util.*;

/**
 * NC352 矩阵置零
 * @author d3y1
 */
public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     *
     * @param matrix int整型ArrayList<ArrayList<>>
     * @return int整型ArrayList<ArrayList<>>
     */
    public ArrayList<ArrayList<Integer>> setZeroMatrix (ArrayList<ArrayList<Integer>> matrix) {
        return solution5(matrix);
        // return solution55(matrix);
        // return solution555(matrix);
    }

    /**
     * 哈希: 一个标记变量
     *
     * 时间复杂度: O(nm)
     * 空间复杂度: O(1)
     *
     * @param matrix
     * @return
     */
    private ArrayList<ArrayList<Integer>> solution5(ArrayList<ArrayList<Integer>> matrix){
        int n = matrix.size();
        int m = matrix.get(0).size();

        // 标记第一行(row 0) 原来是否有0
        boolean flagRow0 = false;
        for(int col=0; col<m; col++){
            if(matrix.get(0).get(col) == 0){
                flagRow0 = true;
                break;
            }
        }

        // 利用第一行和第一列空间 作为标记数组
        for(int row=1; row<n; row++){
            for(int col=0; col<m; col++){
                if(matrix.get(row).get(col) == 0){
                    // matrix(0,0) 标记第一列(col 0) 原来是否有0
                    matrix.get(row).set(0, 0);
                    matrix.get(0).set(col, 0);
                }
            }
        }

        // 根据标记数组 置0
        for(int row=1; row<n; row++){
            // 第一列(col 0)已经作为标记数组, 应该最后置0, 所以降序
            for(int col=m-1; col>=0; col--){
                if(matrix.get(row).get(0)==0 || matrix.get(0).get(col)==0){
                    matrix.get(row).set(col, 0);
                }
            }
        }

        // 第一行 置0
        if(flagRow0){
            for(int col=0; col<m; col++){
                matrix.get(0).set(col, 0);
            }
        }

        return matrix;
    }

    /**
     * 哈希: 一个标记变量
     *
     * 时间复杂度: O(nm)
     * 空间复杂度: O(1)
     *
     * @param matrix
     * @return
     */
    private ArrayList<ArrayList<Integer>> solution55(ArrayList<ArrayList<Integer>> matrix){
        int n = matrix.size();
        int m = matrix.get(0).size();

        // 标记第一行(row 0) 原来是否有0
        boolean flagRow0 = false;
        for(int col=0; col<m; col++){
            if(matrix.get(0).get(col) == 0){
                flagRow0 = true;
                break;
            }
        }

        // 利用第一行和第一列空间 作为标记数组
        for(int col=0; col<m; col++){
            for(int row=1; row<n; row++){
                if(matrix.get(row).get(col) == 0){
                    // matrix(0,0) 标记第一列(col 0) 原来是否有0
                    matrix.get(row).set(0, 0);
                    matrix.get(0).set(col, 0);
                }
            }
        }

        // 根据标记数组 置0; 第一列(col 0)已经作为标记数组, 应该最后置0, 所以降序
        for(int col=m-1; col>=0; col--){
            for(int row=1; row<n; row++){
                if(matrix.get(row).get(0)==0 || matrix.get(0).get(col)==0){
                    matrix.get(row).set(col, 0);
                }
            }
        }

        // 第一行 置0
        if(flagRow0){
            for(int col=0; col<m; col++){
                matrix.get(0).set(col, 0);
            }
        }

        return matrix;
    }

    /**
     * 哈希: 一个标记变量
     *
     * 时间复杂度: O(nm)
     * 空间复杂度: O(1)
     *
     * @param matrix
     * @return
     */
    private ArrayList<ArrayList<Integer>> solution555(ArrayList<ArrayList<Integer>> matrix){
        int n = matrix.size();
        int m = matrix.get(0).size();

        // 标记第一行(row 0) 原来是否有0
        boolean flagRow0 = false;

        // 利用第一行和第一列空间 作为标记数组
        for(int col=0; col<m; col++){
            // 标记第一行(row 0) 原来是否有0
            if(matrix.get(0).get(col) == 0){
                flagRow0 = true;
            }
            for(int row=1; row<n; row++){
                if(matrix.get(row).get(col) == 0){
                    // matrix(0,0) 标记第一列(col 0) 原来是否有0
                    matrix.get(row).set(0, 0);
                    matrix.get(0).set(col, 0);
                }
            }
        }

        // 根据标记数组 置0; 第一列(col 0)已经作为标记数组, 应该最后置0, 所以降序
        for(int col=m-1; col>=0; col--){
            for(int row=1; row<n; row++){
                if(matrix.get(row).get(0)==0 || matrix.get(0).get(col)==0){
                    matrix.get(row).set(col, 0);
                }
            }
            // 第一行 置0
            if(flagRow0){
                matrix.get(0).set(col, 0);
            }
        }

        return matrix;
    }
}
```
