# javascript-BD9 倒计时


    <!DOCTYPE html>
    <html>
    
    <head>
        <meta charset="UTF-8">
        <style>
           /* 填写样式 */
            .hide{
    	display: none;
    }
        </style>
    </head>
    
    <body>
        <!-- BD9 倒计时 -->
        <div id="jsCountdown">
        <span>01天</span>
        <span>02:</span>
        <span>03:</span>
        <span>04</span>
    </div>
        <script type="text/javascript">
            function second(second) {
                let day = Math.floor(second/(60*60*24)),
                    hour = Math.floor((second%(60*60*24))/(60*60)),
                    min = Math.floor(second%(60*60)/60),
                    sec = second%60;
                return {
                    day,
                    hour,
                    min,
                    second:sec,
                }
            }
    
            function render(data) {
                let format = val=>val.toString().length>1?val:`0${val}`;
                let node = document.getElementById('jsCountdown');
                
                data.day===0?node.children[0].classList.add('hide'):node.children[0].innerHTML=`${format(data.day)}天`;
                node.children[1].innerHTML=`${format(data.hour)}:`;
                node.children[2].innerHTML=`${format(data.min)}:`;
                node.children[3].innerHTML=format(data.second);
            }
        </script>
    </body>
    
    </html>

  

