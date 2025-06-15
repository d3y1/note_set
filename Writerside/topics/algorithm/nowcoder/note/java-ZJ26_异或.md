# java-ZJ26 异或


    import java.util.Scanner;
    
    public class Main {
        private static int n;
        private static int m;
    
        public static void main(String[] args){
            Scanner in = new Scanner(System.in);
            while(in.hasNext()){
                solution(in);
            }
        }
    
        /**
         * 字典树(前缀树) Trie
         * @param in
         */
        private static void solution(Scanner in){
            n = in.nextInt();
            m = in.nextInt();
    
            int[] A = new int[n];
            for(int i=0; i<n; i++){
                A[i] = in.nextInt();
            }
    
            Trie trie = buildTrie(A);
    
            long result = 0;
            for(int i=0; i<n; i++){
                result += queryTrie(trie, A[i], 31);
            }
    
            System.out.println(result/2);
        }
        
        private static long queryTrie(Trie trie, int a, int index){
            if(trie == null){
                return 0;
            }
    
            Trie curr = trie;
            for(int i=index; i>=0; i--){
                int aBit =(a >> i) & 1;
                int mBit =(m >> i) & 1;
                // 1. aBit=1, mBit=1时
                // 字典中第k位为0, 异或结果为1, 需要继续搜索更低位;
                // 字典中第k位为1, 异或结果为0, 小于mBit, 不用理会;
                if(aBit==1 && mBit==1){
                    if(curr.child[0] == null){
                        return 0;
                    }
    //                curr = curr.child[0];
                    return queryTrie(curr.child[0], a, i-1);
                }
                // 2. aBit=0, mBit=1时
                // 字典中第k位为1, 异或结果为1, 需要继续搜索更低位;
                // 字典中第k位为0, 异或结果为0, 小于mBit, 不用理会;
                else if(aBit==0 && mBit==1){
                    if(curr.child[1] == null){
                        return 0;
                    }
    //                curr = curr.child[1];
                    return queryTrie(curr.child[1], a, i-1);
                }
                // 3. aBit=1, mBit=0时
                // 字典中第k位为0, 异或结果为1, 与对应分支所有数异或, 结果都会大于m;
                // 字典中第k位为1, 异或结果为0, 递归获得结果;
                else if(aBit==1 && mBit==0){
                    long p = queryTrie(curr.child[1], a, i-1);
                    long q = curr.child[0]==null ? 0:curr.child[0].count;
                    return p+q;
                }
                // 4. aBit=0, mBit=0时
                // 字典中第k位为1, 异或结果为1, 与对应分支所有数异或, 结果都会大于m;
                // 字典中第k位为0, 异或结果为0, 递归获得结果;
                else if(aBit==0 && mBit==0){
                    long p = queryTrie(curr.child[0], a, i-1);
                    long q = curr.child[1]==null ? 0:curr.child[1].count;
                    return p+q;
                }
            }
            return 0;
        }
    
        private static Trie buildTrie(int[] A){
            Trie trie = new Trie();
            for(int i=0; i<n; i++){
                Trie curr = trie;
                for(int j=31; j>=0; j--){
                    int bit =(A[i] >> j) & 1;
                    if(curr.child[bit] == null){
                        curr.child[bit] = new Trie();
                    }else{
                        curr.child[bit].count++;
                    }
                    curr = curr.child[bit];
                }
            }
            return trie;
        }
    
        private static class Trie{
            Trie[] child = new Trie[2];
            int count = 1;
        }
    }

  

