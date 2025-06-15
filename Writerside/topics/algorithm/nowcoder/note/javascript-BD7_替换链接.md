# javascript-BD7 替换链接


    <!DOCTYPE html>
    <html>
    
    <head>
        <meta charset="UTF-8">
        <style>
           /* 填写样式 */
            a {
        color: #00bc9b;
    }
        </style>
    </head>
    
    <body>
        <!-- BD7 替换链接 -->
        <div id="jsContainer">
    这里会给出一段随机文本，可能包含一些链接，比如https://www.baidu.com，或者 www.baidu.com?from=onlineExam，如果出现链接文本，请给该链接文本加上链接标签，用户点击后能直接在新窗口中打开该链接。
    </div>
        <script type="text/javascript">
            // 填写JavaScript
            function link(){
                const div = document.querySelector('#jsContainer');
                let text = div.innerText;;
                // let arr = text.match(/(https:\/\/www\.\w+\.com(\.\w+)*\??(\w+=.+)*|http:\/\/www\.\w+\.com(\.\w+)*\??(\w+=.+)*|www\.\w+\.com(\.\w+)*\??(\w+=\S+)*)/g);
                let arr = text.match(/(http(s)?:\/\/www\.\w+\.com(\.\w+)*\??(\w+=.+)*|www\.\w+\.com(\.\w+)*\??(\w+=\S+)*)/g);
                if (arr) {
                    arr.forEach(item => {
                        if (/^www./.test(item)) {
                            text = text.replace(item, `<a href='http://${item}' target="_blank" >${item}</a>`)
                        } else {
                            text = text.replace(item, `<a href='${item}' target="_blank" >${item}</a>`)
                        }
                    })
                }
                div.innerHTML = text
            }
        </script>
    </body>
    
    </html>

  

