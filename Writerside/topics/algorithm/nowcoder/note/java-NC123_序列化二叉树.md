# java-NC123 序列化二叉树

```java
import java.util.*;
/*
public class TreeNode {
    int val = 0;
    TreeNode left = null;
    TreeNode right = null;

    public TreeNode(int val) {
        this.val = val;
    }
}
*/

/**
 * NC123 序列化二叉树
 * @author d3y1
 */
public class Solution {
    private StringBuilder sb = new StringBuilder();

    private String strSE;
    private int idx = 0;

    /**
     * 序列化
     * @param root
     * @return
     */
    String Serialize(TreeNode root) {
        // 层序遍历
        return Serialize1(root);

        // 前序遍历
        // return Serialize2(root);
    }

    /**
     * 层序遍历
     * @param root
     * @return
     */
    String Serialize1(TreeNode root) {
        if(root == null){
            return "{}";
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        sb.append("{");
        sb.append(root.val);

        int size;
        TreeNode node;
        while(!queue.isEmpty()){
            size = queue.size();
            while(size-- > 0){
                node = queue.poll();

                if(node.left != null){
                    queue.offer(node.left);
                    sb.append(",").append(node.left.val);
                }else{
                    sb.append(",").append("#");
                }

                if(node.right != null){
                    queue.offer(node.right);
                    sb.append(",").append(node.right.val);
                }else{
                    sb.append(",").append("#");
                }
            }
        }

        // 删除 #后缀
        while(sb.length()>0 && sb.charAt(sb.length()-1)=='#') {
            sb.deleteCharAt(sb.length()-1);
            sb.deleteCharAt(sb.length()-1);
        }

        sb.append("}");

        return sb.toString();
    }

    /**
     * 前序遍历
     * @param root
     * @return
     */
    String Serialize2(TreeNode root) {
        if(root == null){
            return "{}";
        }

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        sb.append("{");
        preOrderSE(root);
        sb.append("}");

        return sb.toString();
    }

    /**
     * 前序遍历: 递归
     * @param root
     */
    private void preOrderSE(TreeNode root){
        if(root == null){
            sb.append("#");
            return;
        }

        sb.append(root.val).append("^");

        preOrderSE(root.left);
        preOrderSE(root.right);
    }



    /**
     * 反序列化
     * @param str
     * @return
     */
    TreeNode Deserialize(String str) {
        // 层序遍历
        // return Deserialize1(str);
        return Deserialize11(str);

        // 前序遍历
        // return Deserialize2(str);
    }

    /**
     * 哈希法
     * @param str
     * @return
     */
    TreeNode Deserialize1(String str) {
        if(str.equals("{}")){
            return null;
        }

        String[] values = str.substring(1,str.length()-1).split(",");
        int len = values.length;

        HashMap<String,TreeNode> nodeMap = new HashMap<>();
        HashMap<Integer,Integer> cntMap = new HashMap<>();

        int idx = 0;
        int level = 1;
        int cnt = 1;
        int seq = cnt-1;
        TreeNode root = new TreeNode(Integer.parseInt(values[0]));

        nodeMap.put(level+"-"+seq, root);
        cntMap.put(level, cnt);

        int start,end,offset;
        int parentLevel,parentSeq,parentDirect;
        TreeNode node,parentNode;
        idx++;
        while(idx < len){
            level++;
            cnt = 0;
            start = idx;
            end = Math.min(start+cntMap.get(level-1)*2, len);
            offset = 0;
            for(int i=start; i<end; i++){
                if(!values[i].equals("#")){
                    cnt++;
                    seq = cnt-1;
                    node = new TreeNode(Integer.parseInt(values[i]));
                    nodeMap.put(level+"-"+seq, node);
                    parentLevel = level-1;
                    parentSeq = offset/2;
                    parentNode = nodeMap.get(parentLevel+"-"+parentSeq);
                    parentDirect = offset%2;
                    if(parentDirect == 0){
                        parentNode.left = node;
                    }else{
                        parentNode.right = node;
                    }
                }
                offset++;
            }
            cntMap.put(level, cnt);
            idx = end;
        }

        return root;
    }

    /**
     * 层序遍历
     * @param str
     * @return
     */
    TreeNode Deserialize11(String str) {
        if(str.equals("{}")){
            return null;
        }

        String[] values = str.substring(1,str.length()-1).split(",");
        int len = values.length;

        Queue<TreeNode> queue = new LinkedList<>();

        int idx = 0;
        TreeNode root = new TreeNode(Integer.parseInt(values[idx]));
        queue.offer(root);

        TreeNode node,leftNode,rightNode;
        int size;
        String left,right;
        while(!queue.isEmpty()){
            size = queue.size();
            while(size-- > 0){
                node = queue.poll();

                ++idx;
                if(idx >= len){
                    return root;
                }
                left = values[idx];
                if(!left.equals("#")){
                    leftNode = new TreeNode(Integer.parseInt(left));
                    queue.offer(leftNode);
                    node.left = leftNode;
                }

                ++idx;
                if(idx >= len){
                    return root;
                }
                right = values[idx];
                if(!right.equals("#")){
                    rightNode = new TreeNode(Integer.parseInt(right));
                    queue.offer(rightNode);
                    node.right = rightNode;
                }
            }
        }

        return root;
    }

    /**
     * 前序遍历
     * @param str
     * @return
     */
    TreeNode Deserialize2(String str) {
        if(str.equals("{}")){
            return null;
        }

        strSE = str.substring(1,str.length()-1);

        return preOrderDE();
    }

    /**
     * 前序遍历: 递归
     * @return
     */
    private TreeNode preOrderDE(){
        char ch = strSE.charAt(idx);
        if(ch == '#'){
            idx++;
            return null;
        }
        int val = -1;
        if(Character.isDigit(ch)){
            val = getValue();
        }

        TreeNode root = new TreeNode(val);

        root.left = preOrderDE();
        root.right = preOrderDE();

        return root;
    }

    /**
     * 获取节点的值
     * @return
     */
    private int getValue(){
        int val = 0;
        char ch;
        while(idx < strSE.length()){
            ch = strSE.charAt(idx);
            idx++;
            if(ch == '^'){
                return val;
            }
            if(Character.isDigit(ch)){
                val = val*10+(ch-'0');
            }
        }

        return val;
    }
}
```
