# javascript-JD12 购物车


    <!DOCTYPE html>
    <html>
    
    <head>
        <meta charset="UTF-8">
        <style>
           /* 填写样式 */
            body,html{
        padding: 0;
        margin: 0;
        font-size: 14px;
        color: #000000;
    }
    table{
        border-collapse: collapse;
        width: 100%;
        table-layout: fixed;
    }
    thead{
        background: #3d444c;
        color: #ffffff;
    }
    td,th{
        border: 1px solid #e1e1e1;
        padding: 0;
        height: 30px;
        line-height: 30px;
        text-align: center;
    }
        </style>
    </head>
    
    <body>
        <!-- JD12 购物车 -->
        <table id="jsTrolley">
        <thead><tr><th>名称</th><th>价格</th><th>操作</th></tr></thead>
        <tbody>
            <tr><td>产品1</td><td>10.00</td><td><a href="javascript:void(0);">删除</a></td></tr>
            <tr><td>产品2</td><td>30.20</td><td><a href="javascript:void(0);">删除</a></td></tr>
            <tr><td>产品3</td><td>20.50</td><td><a href="javascript:void(0);">删除</a></td></tr>
        </tbody>
        <tfoot><tr><th>总计</th><td colspan="2">60.70(3件商品)</td></tr></tfoot>
    </table>
    <script type="text/javascript">
        function add(items) {
            let table = document.querySelector("tbody");
            let str = "";
            for (let i = 0; i < items.length; ++i) {
                let item = items[i];
                str += `
                    <tr>
                        <td>${item.name}</td>
                        <td>${item.price.toFixed(2)}</td>
                        <td><a href="javascript:void(0);">删除</a></td>
                    </tr>
                `;
            }
            table.innerHTML += str;
            // 更新视图
            this.refresh();
        }
    
        function bind() {
            let table = document.querySelectorAll("tbody > tr");
            // 遍历tr项
            for (let i = 0; i < table.length; ++i) {
                let that = this
                // 得到删除按钮元素
                let deldom = table[i].querySelectorAll("td")[2];
                deldom.addEventListener('click', function (e) {
                    table[i].remove()
                    // 更新视图
                    that.refresh();
                });
            }
        }
    
        function refresh() {
            let table = document.querySelectorAll("tbody > tr");
            let sum = 0;
            for (let i = 0; i < table.length; ++i) {
                // 获取物品的价格
                let cur = table[i].querySelectorAll("td")[1].innerText;
                sum += +cur;
            }
            let count = document.querySelector("tfoot td");
            count.innerText = `${sum.toFixed(2)}(${table.length}件商品)`
            // 坑点，因为会新增元素，所以需要刷新监听列表
            this.bind()
        }
    </script>
    </body>
    
    </html>

  

