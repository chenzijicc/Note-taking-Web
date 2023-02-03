#### js二维码生成

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>position sticky</title>
    <script src="../js/jquery-3.6.1.min.js"></script>
    <script src="../js/jquery.qrcode.min.js"></script>
<!--http://t.zoukankan.com/songyz-p-7490562.html-->
</head>
<style>
    /*div:first-of-type {*/
        /*width: 100%;*/
        /*background: #f6d565;*/
        /*padding: 25px 0;*/
        /*position: sticky;*/
        /*top: 0;*/
    /*}*/
    /*div:last-of-type {*/
        /*width: 100%;*/
        /*background: yellow;*/
        /*padding: 25px 0;*/
        /*position: sticky;*/
        /*bottom: 0;*/
    /*}*/
</style>

<body>
<!--<div style="height: 300px;">上面内容</div>-->
<!--<div class="header" style="height: 1200px">浮动内容</div>-->
<!--<div style="height: 200px;">下面内容</div>-->
<div id="myTarget" style="float: left;">
    <div>
        <button id='btn_showimg' onclick="ShowQRCode()">显示二维码</button>
    </div>
    <div style="margin-top: 10px;">
        <textarea rows="20" cols="30" placeholder="请输入二维码的内容"></textarea>
    </div>
</div>
<div id="QRCode" ></div>
<div id="img"></div>
<script>
    $(function(){
        //$('#QRCode').qrcode("www.baidu.com");
        //名片格式定义
        var vcard = "BEGIN:VCARD" + '\n'
            + "VERSION:2.1" + '\n'
            + "N:" + '\n'
            + "FN:a digger" + '\n'
            + "ORG:自由职业公司公司" + '\n'
            + "TITLE:" + '\n'
            + "TEL;WORK;VOICE:10010001000" + '\n'
            + "TEL;HOME;VOICE:" + '\n'
            + "TEL;CELL;VOICE:10010001000" + '\n'
            + "ADR;WORK:;;地址;城市;省份;;国际" + '\n'
            + "LABEL;WORK;ENCODING=QUOTED-PRINTABLE:" + '\n'
            + "ADR;HOME:" + '\n'
            + "LABEL;HOME;ENCODING=QUOTED-PRINTABLE:" + '\n'
            + "EMAIL;PREF;INTERNET:mrwu-web@space.cn" + '\n'
            + "REV:" + '\n'
            + "END:VCARD;"
    })

    //从 canvas 提取图片 image
    function convertCanvasToImage(canvas) {
        //新Image对象，可以理解为DOM
        var image = new Image();
        // canvas.toDataURL 返回的是一串Base64编码的URL
        // 指定格式 PNG
        image.src = canvas.toDataURL("image/png");
        return image;
    }

    function utf16to8(str) {
        var out, i, len, c;
        out = "";
        len = str.length;
        for(i = 0; i < len; i++) {
            c = str.charCodeAt(i);
            if ((c >= 0x0001) && (c <= 0x007F)) {
                out += str.charAt(i);
            } else if (c > 0x07FF) {
                out += String.fromCharCode(0xE0 | ((c >> 12) & 0x0F));
                out += String.fromCharCode(0x80 | ((c >> 6) & 0x3F));
                out += String.fromCharCode(0x80 | ((c >> 0) & 0x3F));
            } else {
                out += String.fromCharCode(0xC0 | ((c >> 6) & 0x1F));
                out += String.fromCharCode(0x80 | ((c >> 0) & 0x3F));
            }
        }
        return out;
    }

    function ShowQRCode(){
        var data = $('textarea').val();
        var module = 3;
        if (data.length < 250){
            module = 8;
        }
        $('#QRCode').qrcode({
            //render: 'table',
            text: data,			//二维码扫码返回值
            background:"#ffddff",		//二维码背景颜色
            render:"canvas",    	//二维码显示方式
            foreground:?"#C00",//二维码前景色(条纹色)
            width: "196",                      //二维码的宽度
            height: "196",                    //二维码的高度
            moduleSize:module,   		//二维码大小
            margin:4,				//二维码外边距
            src:"../image/icon/scanIcon.png"	//二维码logo
        });

        //获取网页中的canvas对象
        var mycans=$('canvas')[0];
//调用convertCanvasToImage函数将canvas转化为img形式
        var img=convertCanvasToImage(mycans);
//将img插入容器
        console.log(img)
        $('#img').append(img);
    }
</script>
</body>

</html>

```