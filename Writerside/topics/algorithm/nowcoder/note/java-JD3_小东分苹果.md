# java-JD3 小东分苹果


    import java.util.*;
    
    /**
     * JD3 小东分苹果
     * @author d3y1
     */
    public class Apples {
        /**
         * 程序入口
         * @param n
         * @return
         */
        public int getInitial(int n){
            int result;
            result = getInitial1(n);
            result = getInitial2(n);
            
            return result;
        }
    
        /**
         * 模拟法
         * @param n
         * @return
         */
        public int getInitial1(int n) {
            int result = -1;
            for(int i=n+1; i<Integer.MAX_VALUE; i+=n){
                int remain = i;
                boolean found = true;
                for(int j=1; j<=n; j++){
                    if((remain-1)%n != 0){
                        found = false;
                        break;
                    }else{
                        remain = (remain-1)*(n-1)/n;
                    }
                }
                if(found){
                    result = i;
                    break;
                }
            }
    
            return result;
        }
    
        /**
         * 数学法: 公式推导
         *
         * 假设最初这堆苹果有X个
         * d-decrease(减少数量t+a) t-take(熊拿走数量) a-abandon(丢弃1个)
         * r-remain(剩余数量)
         * 
         * 依次推导:
         * 熊1: 减少数量d1 = t1+a1 = (X-1)/n+1,                       剩余数量r1 = X-d1  =  X-((X-1)/n+1) = (n-1)(X-1)/n
         * 熊2: 减少数量d2 = t2+a2 = (r1-1)/n+1 = (n-1)(X+n-1)/n^2,   剩余数量r2 = r1-d2 = (n-1)((n-1)*X-2*n+1)/n^2
         * 熊3: 减少数量d3 = t3+a3 = (r2-1)/n+1 = (n-1)^2(X+n-1)/n^3, 剩余数量r3 = r2-d3 = (n-1)((n-1)^2*X-3*n^2+3*n-1)/n^3
         * 熊4: 减少数量d4 = t4+a4 = (r3-1)/n+1 = (n-1)^3(X+n-1)/n^4, ...
         * ...
         * 熊n: 减少数量dn = (n-1)^(n-1)(X+n-1)/n^n, ...
         *
         * 要想X最小, 则dn也应该最小且为整数, 因为(n-1)^(n-1)与n^n互质, 所以只能是(X+n-1)被n^n整除并且为最小值1
         * ((X+n-1)/n^n)_min = 1
         * => (X+n-1)_min = n^n
         * => X_min = n^n-n+1
         *
         * @param n
         * @return
         */
        public int getInitial2(int n) {
            int result = (int) Math.pow(n,n)-n+1;
    
            return result;
        }
    }

  

