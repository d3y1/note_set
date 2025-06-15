# java-NC224 从下到上打印二叉树


    import java.util.*;
    
    /*
     * public class TreeNode {
     *   int val = 0;
     *   TreeNode left = null;
     *   TreeNode right = null;
     *   public TreeNode(int val) {
     *     this.val = val;
     *   }
     * }
     */
    
    /**
     * NC224 从下到上打印二叉树
     * @author d3y1
     */
    public class Solution {
        private int[][] results;
    
        /**
         * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
         *
         * 程序入口
         *
         * @param root TreeNode类
         * @return int整型二维数组
         */
        public int[][] levelOrderBottom (TreeNode root) {
            // return solution1(root);
            // return solution2(root);
            // return solution3(root);
            // return solution4(root);
            return solution44(root);
        }
    
        ///////////////////////////////////////////////////////////////////////////////////
    
        private ArrayList<QueueNode> levelNodes = new ArrayList<>();
    
        private class QueueNode {
            TreeNode node;
            int level;
            int seq;
    
            public QueueNode(TreeNode node, int level, int seq){
                this.node = node;
                this.level = level;
                this.seq = seq;
            }
        }
    
        /**
         * bfs + sort
         * @param root
         * @return
         */
        private int[][] solution1(TreeNode root){
            Queue<QueueNode> queue = new LinkedList<>();
            int level = 0;
            int seq = 1;
            queue.offer(new QueueNode(root, level, seq));
    
            QueueNode queueNode;
            int size = 0;
            int[] width = new int[1000];
            while(!queue.isEmpty()){
                size = queue.size();
                // width = Math.max(width, size);
                width[level] = size;
                level++;
                while(size-- > 0){
                    queueNode = queue.poll();
                    levelNodes.add(queueNode);
                    if(queueNode.node.left != null){
                        queue.offer(new QueueNode(queueNode.node.left, level, seq++));
                    }
                    if(queueNode.node.right != null){
                        queue.offer(new QueueNode(queueNode.node.right, level, seq++));
                    }
                }
            }
    
            Collections.sort(levelNodes, (o1, o2) -> {
                if(o1.level == o2.level){
                    return o1.seq-o2.seq;
                }else{
                    return o2.level-o1.level;
                }
            });
    
            results = new int[level][];
            for(int i=0; i<level; i++){
                results[i] = new int[width[level-i-1]];
            }
    
            int lastLevel = -1;
            int currLevel;
            int index = 0;
            for(QueueNode qNode: levelNodes){
                currLevel = qNode.level;
                if(currLevel != lastLevel){
                    index = 0;
                }
                results[level-currLevel-1][index++] = qNode.node.val;
                lastLevel = currLevel;
            }
    
            return results;
        }
    
        ///////////////////////////////////////////////////////////////////////////////////
    
        /**
         * bfs
         * @param root
         * @return
         */
        private int[][] solution2(TreeNode root){
            LinkedList<int[]> list = new LinkedList<>();
            Queue<TreeNode> queue = new LinkedList<>();
            queue.offer(root);
    
            int[] level;
            TreeNode currNode;
            while (!queue.isEmpty()) {
                int levelSize = queue.size();
                level = new int[levelSize];
                for (int i = 0; i < levelSize; i++) {
                    currNode = queue.poll();
                    if (currNode.left != null){
                        queue.offer(currNode.left);
                    }
                    if (currNode.right != null){
                        queue.offer(currNode.right);
                    }
                    level[i] = currNode.val;
                }
                list.add(level);
            }
    
            Iterator<int[]> dIterator = list.descendingIterator();
            results = new int[list.size()][];
            int i = 0;
            while (dIterator.hasNext()) {
                results[i++] = dIterator.next();
            }
            return results;
        }
    
        ///////////////////////////////////////////////////////////////////////////////////
    
        private class Node {
            TreeNode treeNode;
            int level;
            public Node(TreeNode treeNode, int level){
                this.treeNode = treeNode;
                this.level = level;
            }
        }
    
        /**
         * bfs
         * @param root
         * @return
         */
        private int[][] solution3(TreeNode root){
            if(root == null){
                return new int[][]{};
            }
    
            ArrayList<ArrayList<Integer>> list = new ArrayList<ArrayList<Integer>>();
    
            Queue<Node> queue = new LinkedList<>();
            queue.offer(new Node(root, 0));
            Node node;
            int preLevel = 0;
            ArrayList<Integer> levelList = new ArrayList<>();
            while(!queue.isEmpty()){
                node = queue.poll();
                if(node.treeNode.left != null){
                    queue.offer(new Node(node.treeNode.left, node.level+1));
                }
                if(node.treeNode.right != null){
                    queue.offer(new Node(node.treeNode.right, node.level+1));
                }
                if(node.level != preLevel){
                    list.add(levelList);
                    levelList = new ArrayList<>();
                }
                levelList.add(node.treeNode.val);
                preLevel = node.level;
            }
            list.add(levelList);
    
            results = new int[list.size()][];
            int width;
            for(int i=0; i<list.size(); i++){
                width = list.get(list.size()-i-1).size();
                results[i] = new int[width];
                for(int j=0; j<width; j++){
                    results[i][j] = list.get(list.size()-i-1).get(j);
                }
            }
    
            return results;
        }
    
        ///////////////////////////////////////////////////////////////////////////////////
    
        /**
         * bfs
         * @param root
         * @return
         */
        private int[][] solution4(TreeNode root){
            if(root == null){
                return new int[][]{};
            }
    
            ArrayList<int[]> list = new ArrayList<int[]>();
            Queue<TreeNode> queue = new LinkedList<>();
            queue.offer(root);
    
            int size;
            int[] level;
            TreeNode node;
            while(!queue.isEmpty()){
                size = queue.size();
                level = new int[size];
                for(int i=0; i<size; i++){
                    node = queue.poll();
                    if(node.left != null){
                        queue.offer(node.left);
                    }
                    if(node.right != null){
                        queue.offer(node.right);
                    }
                    level[i] = node.val;
                }
                list.add(level);
            }
    
            results = new int[list.size()][];
            int width;
            for(int i=0; i<list.size(); i++){
                width = list.get(list.size()-i-1).length;
                results[i] = new int[width];
                for(int j=0; j<width; j++){
                    results[i][j] = list.get(list.size()-i-1)[j];
                }
            }
    
            return results;
        }
    
        ///////////////////////////////////////////////////////////////////////////////////
    
        /**
         * bfs
         * @param root
         * @return
         */
        private int[][] solution44(TreeNode root){
            if(root == null){
                return new int[][]{};
            }
    
            ArrayList<int[]> list = new ArrayList<int[]>();
            Queue<TreeNode> queue = new LinkedList<>();
            queue.offer(root);
    
            int size;
            int[] level;
            TreeNode node;
            while(!queue.isEmpty()){
                size = queue.size();
                level = new int[size];
                for(int i=0; i<size; i++){
                    node = queue.poll();
                    if(node.left != null){
                        queue.offer(node.left);
                    }
                    if(node.right != null){
                        queue.offer(node.right);
                    }
                    level[i] = node.val;
                }
                list.add(0, level);
            }
    
            results = new int[list.size()][];
            for(int i=0; i<list.size(); i++){
                results[i] = list.get(i);
            }
    
            return results;
        }
    }

  

