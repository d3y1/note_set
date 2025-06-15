# javascript-BD19 文字输出


    <!DOCTYPE html>
    <html>
    
    <head>
        <meta charset="UTF-8">
        <style>
           html, body {margin: 0;}
    .color1 {color: #E60012;}
    .color2 {color: #EB6100;}
    .color3 {color: #F39800;}
    .color4 {color: #FCC800;}
    .color5 {color: #FFF100;}
    .color6 {color: #CFDB00;}
    .color7 {color: #8FC31F;}
    .color8 {color: #22AC38;}
    .color9 {color: #009944;}
    .color10 {color: #009B6B;}
    .color11 {color: #009E96;}
    .color12 {color: #00A0C1;}
    .color13 {color: #00A0E9;}
    .color14 {color: #0086D1;}
    .color15 {color: #0068B7;}
    .color16 {color: #00479D;}
    .color17 {color: #1D2088;}
    .color18 {color: #601986;}
    .color19 {color: #920783;}
    .color20 {color: #BE0081;}
    .color21 {color: #E4007F;}
    .color22 {color: #E5006A;}
    .color23 {color: #E5004F;}
    .color24 {color: #E60033;}
    .word {font-size: 20px;}
    .content {text-align: center;font-size:0;}
    .blink {
        font-size: 20px;
        animation: fade 500ms infinite;
        -webkit-animation: fade 500ms infinite;
    }
    @keyframes fade {
        from {opacity: 1.0;}
        50% {opacity: 0;}
        to {opacity: 1.0;}
    }
        </style>
    </head>
    
    <body>
        <!-- BD19 文字输出 -->
       <div class="content">
        <span class="word color23">h</span>
        <span class="word color22">e</span>
        <span class="word color4">l</span>
        <span class="word color24">l</span>
        <span class="word color17">o</span>
        <span class="word color2">&nbsp;</span>
        <span class="word color9">w</span>
        <span class="word color3">o</span>
        <span class="word color1">r</span>
        <span class="word color23">l</span>
        <span class="word color15">d</span>
        <br>
        <span class="word color15">你</span>
        <span class="word color13">好</span>
        <span class="word color16">世</span>
        <span class="word color19">界</span>
        <span class="blink" id="jsBlink">|</span>
    </div>
        <script type="text/javascript">
            function output(str) {
                let count = 0; //用于计时器停止
                const box = document.getElementsByClassName('content')[0];
                const spans = Array.from(box.children);
                const lastSpan = document.getElementsByClassName('blink')[0];
                for(let i = 0 ; i < spans.length ; i++){
                    if(i != (spans.length - 1)){
                        box.removeChild(spans[i])
                    }
                }
    
                const time = setInterval(function () {
                    let el = '';
                    if (str[count] == '\n') {
                        el = document.createElement('br');
                    } else {
                        el = document.createElement('span');
                        el.className = 'word ' + 'color' + (Math.round(Math.random() * 23) + 1);
                        el.innerText = str[count];
                        if (str[count] == ' ') {
                            el.innerHTML = "&nbsp;"
                        }
                        if (str[count] == '<') {
                            el.innerHTML = "&lt;"
                        }
                        if (str[count] == '>') {
                            el.innerHTML = "&gt;"
                        }
                    }
                    box.insertBefore(el, lastSpan);
                    count++;
                    if (count == str.length) {
                        clearInterval(time)
                    }
                }, 200);
            }
        </script>
    </body>
    
    </html>

  

