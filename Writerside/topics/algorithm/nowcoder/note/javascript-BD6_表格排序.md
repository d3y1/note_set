# javascript-BD6 表格排序


    <!DOCTYPE html>
    <html>
    
    <head>
        <meta charset="UTF-8">
        <style>
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
        <!-- 填写标签 -->
        <table>
        <thead>
            <tr><th>id</th><th>price</th><th>sales</th></tr>
        </thead>
        <tbody id="jsList">
            <tr><td>1</td><td>10.0</td><td>800</td></tr>
            <tr><td>2</td><td>30.0</td><td>600</td></tr>
            <tr><td>3</td><td>20.5</td><td>700</td></tr>
            <tr><td>4</td><td>40.5</td><td>500</td></tr>
            <tr><td>5</td><td>60.5</td><td>300</td></tr>
            <tr><td>6</td><td>50.0</td><td>400</td></tr>
            <tr><td>7</td><td>70.0</td><td>200</td></tr>
            <tr><td>8</td><td>80.5</td><td>100</td></tr>
        </tbody>
    </table>
        <script type="text/javascript">
            // 填写JavaScript
            function sort(type, order) {
                const table = document.getElementById("jsList");
                const rows = Array.from(table.rows);
                
                let col;
                switch(type){
                    case 'id':
                        col = 0;
                        break;
                    case 'price':
                        col = 1;
                        break;
                    case 'sales':
                        col = 2;
                        break;
                    default:
                        col = 0;
                        break;
                }
    
                const comparator = order == 'asc'
                    ? (a, b) => getVal(a, col) - getVal(b, col)
                    : (a, b) =>getVal(b, col) - getVal(a, col);
    
                rows.sort(comparator);
    
                // 更新表格内容
                for(let i=1; i<rows.length; i++) {
                    table.appendChild(rows[i]);
                }
            }
    
            function getVal(target, col) {
                return parseFloat(target.cells[col].innerHTML);
            }
        </script>
    </body>
    
    </html>

  

