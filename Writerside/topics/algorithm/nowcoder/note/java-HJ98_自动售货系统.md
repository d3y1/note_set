# java-HJ98 自动售货系统

```java
import java.util.ArrayList;
import java.util.Map;
import java.util.HashMap;
import java.util.List;
import java.util.Scanner;
import java.util.TreeMap;

public class Main {
    // 商品价格
    private static final HashMap<String, Integer> priceMap = new HashMap<String, Integer>(){{
        put("A1", 2);
        put("A2", 3);
        put("A3", 4);
        put("A4", 5);
        put("A5", 8);
        put("A6", 6);
    }};

    // 商品数量
    private static HashMap<String, Integer> productMap = new HashMap<>();

    // 存钱盒
    private static TreeMap<Integer, Integer> moneyMap = new TreeMap<>();

    // 投币余额
    private static int balance = 0;

    public static void main(String[] args){
        Scanner in = new Scanner(System.in);

        while(in.hasNext()){
            solution(in);
        }
    }

    /**
     * 模拟法
     * @param in
     */
    private static void solution(Scanner in){
        String[] commands = in.nextLine().split(";");
        for(String command: commands){
            String[] parts = command.split(" ");
            String kind = parts[0];

            switch(kind.charAt(0)){
                case 'r': reboot(command); break;
                case 'p': pay(command); break;
                case 'b': buy(command); break;
                case 'c': change(); break;
                case 'q': query(command); break;
            }
        }
    }

    /**
     * 系统初始化
     * 设置自动售货机中商品数量和存钱盒各种面额的钱币张数
     * 命令格式: r A1 数量 -A2 数量 -A3 数量 -A4 数量 -A5 数量 -A6 数量 1 元张数 -2 元张数 -5 元张数 -10 元张数
     * @param command
     */
    private static void reboot(String command){
        String[] parts = command.split(" ");

        // 各种产品数量
        String[] quantities = parts[1].split("-");
        for(int i=1; i<=quantities.length; i++){
            productMap.put("A"+i, Integer.parseInt(quantities[i-1]));
        }

        // 各种面额张数
        String[] numbers = parts[2].split("-");
        moneyMap.put(1, Integer.parseInt(numbers[0]));
        moneyMap.put(2, Integer.parseInt(numbers[1]));
        moneyMap.put(5, Integer.parseInt(numbers[2]));
        moneyMap.put(10, Integer.parseInt(numbers[3]));

        System.out.println("S001:Initialization is successful");
    }

    /**
     * 投币
     * 命令格式: p 钱币面额
     * @param command
     */
    private static void pay(String command){
        String[] parts = command.split(" ");
        int amount = Integer.parseInt(parts[1]);

        switch(amount){
            case 1:
            case 2:{
                if(isAllGoodsSoldOut()){
                    System.out.println("E005:All the goods sold out");
                }else{
                    balance += amount;
                    moneyMap.put(amount, moneyMap.getOrDefault(amount, 0)+1);
                    System.out.println("S002:Pay success,balance="+balance);
                }
                break;
            }
            case 5:
            case 10:{
                if(isChangeNotEnough(amount)){
                    System.out.println("E003:Change is not enough, pay fail");
                }else if(isAllGoodsSoldOut()){
                    System.out.println("E005:All the goods sold out");
                }else{
                    balance += amount;
                    moneyMap.put(amount, moneyMap.getOrDefault(amount, 0)+1);
                    System.out.println("S002:Pay success,balance="+balance);
                }
                break;
            }
            default: System.out.println("E002:Denomination error"); break;
        }
    }

    /**
     * 是否 存钱盒中1元和2元面额钱币总额小于本次投入的钱币面额
     * @param amount
     * @return
     */
    private static boolean isChangeNotEnough(int amount){
        int moneyBox = moneyMap.get(1) + 2*moneyMap.get(2);
        return moneyBox<amount;
    }

    /**
     * 是否 自动售货机中商品全部销售完毕
     * @return
     */
    private static boolean isAllGoodsSoldOut(){
        int total = 0;
        for(Integer quantity: productMap.values()){
            total += quantity;
        }

        return total==0;
    }

    /**
     * 购买商品
     * 命令格式: b 商品名称
     * @param command
     */
    private static void buy(String command){
        String[] parts = command.split(" ");
        String product = parts[1];

        Integer quantity = productMap.get(product);
        Integer price = priceMap.get(product);
        // 购买的商品不在商品列表中
        if(quantity == null){
            System.out.println("E006:Goods does not exist");
        }
        // 所购买的商品的数量为0
        else if(quantity == 0){
            System.out.println("E007:The goods sold out");
        }
        // 投币余额小于待购买商品价格
        else if(balance < price){
            System.out.println("E008:Lack of balance");
        }else{
            balance -= price;
            productMap.put(product, quantity-1);
            System.out.println("S003:Buy success,balance="+balance);
        }
    }

    /**
     * 退币
     * 命令格式: c
     * @param
     */
    private static void change(){
        // 投币余额等于0
        if(balance == 0){
            System.out.println("E009:Work failure");
        }else{
            StringBuilder sb = new StringBuilder();

            sb = change(sb, 10);
            sb = change(sb, 5);
            sb = change(sb, 2);
            sb = change(sb, 1);

            // 投币余额清零
            balance = 0;

            System.out.print(sb);
        }
    }

    /**
     * 按面额退币
     * @param sb
     * @param amount
     * @return
     */
    private static StringBuilder change(StringBuilder sb, int amount){
        int number = 0;
        while(balance>=amount && moneyMap.get(amount)>0){
            balance -= amount;
            moneyMap.put(amount, moneyMap.get(amount)-1);
            number++;
        }
        sb.insert(0, amount+" yuan coin number="+number+"\n");

        return sb;
    }

    /**
     * 查询
     * 命令格式: q 查询类别
     * @param command
     */
    private static void query(String command){
        String[] parts = command.split(" ");
        if(parts[0].length()>1 || parts.length!=2){
            System.out.println("E010:Parameter error");
        }else{
            int category = Integer.parseInt(parts[1]);
            // 查询商品信息
            if(category == 0){
                List<Map.Entry<String, Integer>> productList = new ArrayList<>(productMap.entrySet());
                productList.sort((o1, o2) -> {
                    if(o1.getValue().equals(o2.getValue())){
                        return o1.getKey().charAt(1)-o2.getKey().charAt(1);
                    }else{
                        return o2.getValue()-o1.getValue();
                    }
                });

                for(Map.Entry<String, Integer> entry: productList){
                    System.out.println(entry.getKey()+" "+priceMap.get(entry.getKey())+" "+entry.getValue());
                }
            }
            // 查询存钱盒信息
            else if(category == 1){
                for(Map.Entry<Integer, Integer> entry: moneyMap.entrySet()){
                    System.out.println(entry.getKey()+" yuan coin number="+entry.getValue());
                }
            }else{
                System.out.println("E010:Parameter error");
            }
        }
    }
}
```
