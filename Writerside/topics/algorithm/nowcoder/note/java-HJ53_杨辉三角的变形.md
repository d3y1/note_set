# java-HJ53 杨辉三角的变形


    import java.util.Scanner;
    
    // 看前4列就可以
    // 第1列 奇 奇 奇 奇 奇 奇 奇 奇 奇 奇 奇 奇 -> 都是奇
    // 第2列 偶 奇 偶 奇 偶 奇 偶 奇 偶 奇 偶 奇 -> 偶奇 循环
    // 第3列 偶 奇 奇 偶 偶 奇 奇 偶 偶 奇 奇 偶 -> 奇奇偶偶 循环
    // 第4列 偶 偶 偶 奇 偶 偶 偶 奇 偶 偶 偶 奇 -> 偶偶偶奇 循环
    // 于是我们会发现，只有num为1，2时，没有出现偶数，剩下的按照2 3 2 4的规律每四行循环一次。
    public class Main {
    
        public static void main(String[] args) {
            Scanner in = new Scanner(System.in);
    
            int num = in.nextInt();
        
            if(num==1 || num==2){
                System.out.print(-1);
            }else if(num%2 == 1){
                System.out.print(2);
            }else if(num%4 == 0){
                System.out.print(3);
            }else{
                System.out.print(4);
            }
        }
    
    
    
        // private static int NUM = 0;
    
        // public static void main(String[] args) {
        //     Scanner in = new Scanner(System.in);
    
        //     int num = in.nextInt();
        //     NUM = num;
    
        //     boolean flag = false;
        //     for(int j=1; j<2*num; j++){
        //         int result =  getResult(num, j);
    
        //         if(result%2 == 0){
        //             flag = true;
        //             System.out.print(j);
        //             break;
        //         }
        //     }
    
        //     if(!flag){
        //         System.out.print(-1);
        //     }
        // }
    
        // private static int getResult(int i, int j){
        //     if(i == 1){
        //         if(j == NUM){
        //             return 1;
        //         }else{
        //             return 0;
        //         }
        //     }
        //     return getResult(i-1, j-1) +getResult(i-1, j) + getResult(i-1, j+1);
        // }
    
    
        // public static void main(String[] args) {
        //     Scanner in = new Scanner(System.in);
    
        //     int num = in.nextInt();
        //     int[][] array = new int[num+1][2*num+1];
        //     array[1][num] = 1;
    
        //     if (num > 1) {
        //         for (int i = 2; i <= num; i++) {
        //             for (int j = num - i + 1; j < num+i; j++) {
        //                 array[i][j] = array[i-1][j-1] + array[i-1][j] + array[i-1][j+1];
        //             }
        //         }
        //     }
    
        //     boolean flag = false;
        //     for(int j=1; j<2*num; j++){
        //         if(array[num][j]%2 == 0){
        //             flag = true;
        //             System.out.print(j);
        //             break;
        //         }
        //     }
    
        //     if(!flag){
        //         System.out.print(-1);
        //     }
        // }
    }

  

