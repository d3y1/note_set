# javascript-BD17 智能提示


    <!DOCTYPE html>
    <html>
    
    <head>
        <meta charset="UTF-8">
        <style>
           .search{
        position: relative;
    }
    .js-input{
        width: 450px;
        height: 22px;
        line-height: 22px;
        font-size: 16px;
        padding: 8px;
        border: 1px solid #cccccc;
        outline: none;
    }
    .js-suggest{
        width: 466px;
        font-size: 14px;
        border: 1px solid #cccccc;
        background: #ffffff;
        position: absolute;
        left: 0;
        top: 39px;
    }
    .js-suggest.hide{
        display: none;
    }
    .js-suggest ul{
        display: block;
        list-style: none;
        padding: 0;
        margin: 0;
    }
    .js-suggest ul li{
        color: #000;
        font: 14px arial;
        line-height: 25px;
        padding: 0 8px;
        position: relative;
        cursor: default;
    }
    .js-suggest ul li:hover{
        background: #f0f0f0;
    }
        </style>
    </head>
    
    <body>
        <div class="search">
        <div><input type="text" class="js-input" value="的"></div>
        <div class="js-suggest">
            <ul>
                <li>根据输入框的值</li>
                <li>从给定字符串数组中筛选出匹配的数据，依次显示在li节点中</li>
                <li>如果没有匹配的数据，请移除所有li节点，并隐藏.js-suggest节点</li>
            </ul>
        </div>
    </div>
        <script type="text/javascript">
            function suggest(items) {
                window.items = items;
                const el = document.getElementsByClassName("js-input")[0];
                // el.addEventListener("change", onInput);
                el.addEventListener("input", onInput);
                onInput({ currentTarget: el });
            }
    
            function onInput(evt) {
                const suggests = listSuggests(evt.currentTarget.value.trim());
                const display = document.getElementsByClassName("js-suggest")[0];
                const ul = display.children[0];
                ul.innerHTML = "";
                if (!suggests.length) return display.classList.add("hide");
                display.classList.remove("hide");
                ul.innerHTML = suggests.map((i) => `<li>${i}</li>`).join("");
            }
    
            function listSuggests(value) {
                if (!value) return [];
                const regex = new RegExp(
                value
                    .replace(/([\\\/\(\)\+\*\?\:\\[\]\^\$])/g, "\\$1")
                    .replace(/(\\.)/g, "$1.*?")
                );
                const items = window.items;
                const result = items.filter((i) => regex.test(i));
                return result;
            }
        </script>
    </body>
    
    </html>

  

