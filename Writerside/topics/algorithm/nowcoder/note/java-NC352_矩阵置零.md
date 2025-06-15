# java-NC352 矩阵置零

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
        return solution1(matrix);
        // return solution2(matrix);
        // return solution3(matrix);
        // return solution4(matrix);
        // return solution44(matrix);
        // return solution5(matrix);
        // return solution55(matrix);
        // return solution555(matrix);
    }

    /**
     * 哈希: HashSet
     *
     * 时间复杂度: O(nm)
     * 空间复杂度: O(n+m)
     *
     * @param matrix
     * @return
     */
    private ArrayList<ArrayList<Integer>> solution1(ArrayList<ArrayList<Integer>> matrix){
        int n = matrix.size();
        int m = matrix.get(0).size();

        HashSet<Integer> rowSet = new HashSet<>();
        HashSet<Integer> colSet = new HashSet<>();
        for(int row=0; row<n; row++){
            for(int col=0; col<m; col++){
                if(matrix.get(row).get(col) == 0){
                    rowSet.add(row);
                    colSet.add(col);
                }
            }
        }

        // 行列置0
        for(int row=0; row<n; row++){
            for(int col=0; col<m; col++){
                if(rowSet.contains(row) || colSet.contains(col)){
                    matrix.get(row).set(col, 0);
                }
            }
        }

        return matrix;
    }

    /**
     * 哈希: 标记数组
     *
     * 时间复杂度: O(nm)
     * 空间复杂度: O(n+m)
     *
     * @param matrix
     * @return
     */
    private ArrayList<ArrayList<Integer>> solution2(ArrayList<ArrayList<Integer>> matrix){
        int n = matrix.size();
        int m = matrix.get(0).size();

        boolean[] rows = new boolean[n];
        boolean[] cols = new boolean[m];
        for(int row=0; row<n; row++){
            for(int col=0; col<m; col++){
                if(matrix.get(row).get(col) == 0){
                    rows[row] = true;
                    cols[col] = true;
                }
            }
        }

        // 行列置0
        for(int row=0; row<n; row++){
            for(int col=0; col<m; col++){
                if(rows[row] || cols[col]){
                    matrix.get(row).set(col, 0);
                }
            }
        }

        return matrix;
    }

    /**
     * 哈希: 两个标记变量
     *
     * 时间复杂度: O(nm)
     * 空间复杂度: O(1)
     *
     * @param matrix
     * @return
     */
    private ArrayList<ArrayList<Integer>> solution3(ArrayList<ArrayList<Integer>> matrix){
        int n = matrix.size();
        int m = matrix.get(0).size();

        // 标记第一行(row 0) 原来是否有0
        boolean flagRow0 = false;
        // 标记第一列(col 0) 原来是否有0
        boolean flagCol0 = false;

        for(int col=0; col<m; col++){
            if(matrix.get(0).get(col) == 0){
                flagRow0 = true;
                break;
            }
        }
        for(int row=0; row<n; row++){
            if(matrix.get(row).get(0) == 0){
                flagCol0 = true;
                break;
            }
        }

        // 利用第一行和第一列空间 作为标记数组
        for(int row=1; row<n; row++){
            for(int col=1; col<m; col++){
                if(matrix.get(row).get(col) == 0){
                    matrix.get(row).set(0, 0);
                    matrix.get(0).set(col, 0);
                }
            }
        }

        // 根据标记数组 置0
        for(int row=1; row<n; row++){
            for(int col=1; col<m; col++){
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
        // 第一列 置0
        if(flagCol0){
            for(int row=0; row<n; row++){
                matrix.get(row).set(0, 0);
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
    private ArrayList<ArrayList<Integer>> solution4(ArrayList<ArrayList<Integer>> matrix){
        int n = matrix.size();
        int m = matrix.get(0).size();

        // 标记第一列(col 0) 原来是否有0
        boolean flagCol0 = false;
        for(int row=0; row<n; row++){
            if(matrix.get(row).get(0) == 0){
                flagCol0 = true;
                break;
            }
        }

        // 利用第一行和第一列空间 作为标记数组
        for(int row=0; row<n; row++){
            for(int col=1; col<m; col++){
                if(matrix.get(row).get(col) == 0){
                    // matrix(0,0) 标记第一行(row 0) 原来是否有0
                    matrix.get(row).set(0, 0);
                    matrix.get(0).set(col, 0);
                }
            }
        }

        // 根据标记数组 置0; 第一行(row 0)已经作为标记数组, 应该最后置0, 所以降序
        for(int row=n-1; row>=0; row--){
            for(int col=1; col<m; col++){
                if(matrix.get(row).get(0)==0 || matrix.get(0).get(col)==0){
                    matrix.get(row).set(col, 0);
                }
            }
        }

        // 第一列 置0
        if(flagCol0){
            for(int row=0; row<n; row++){
                matrix.get(row).set(0, 0);
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
    private ArrayList<ArrayList<Integer>> solution44(ArrayList<ArrayList<Integer>> matrix){
        int n = matrix.size();
        int m = matrix.get(0).size();

        // 标记第一列(col 0) 原来是否有0
        boolean flagCol0 = false;

        // 利用第一行和第一列空间 作为标记数组
        for(int row=0; row<n; row++){
            // 标记第一列(col 0) 原来是否有0
            if(matrix.get(row).get(0) == 0){
                flagCol0 = true;
            }
            for(int col=1; col<m; col++){
                if(matrix.get(row).get(col) == 0){
                    // matrix(0,0) 标记第一行(row 0) 原来是否有0
                    matrix.get(row).set(0, 0);
                    matrix.get(0).set(col, 0);
                }
            }
        }

        // 根据标记数组 置0; 第一行(row 0)已经作为标记数组, 应该最后置0, 所以降序
        for(int row=n-1; row>=0; row--){
            for(int col=1; col<m; col++){
                if(matrix.get(row).get(0)==0 || matrix.get(0).get(col)==0){
                    matrix.get(row).set(col, 0);
                }
            }
            // 第一列 置0
            if(flagCol0){
                matrix.get(row).set(0, 0);
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
