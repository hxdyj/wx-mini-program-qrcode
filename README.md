# Document

## 1.outputQRCodeBase64: function (text, options)

描述:

-   以 base64 图片格式输出二维码

参数:

-   text：必须，二维码内容，比如 url

options：

```
{
	ecc: 'H',               // 可选，容错级别，可选值L、M、Q和H（默认）
	size: 256,              // 可选，二维码尺寸，必须为整数。默认为256
	padding: 0,             // 可选，单侧空白边宽度，默认为0
	color: '#000000',       // 可选，二维码颜色，必须是16进制，默认为'#000000'
	background: '#ffffff'   // 可选，二维码背景色，必须是16进制，默认为'#ffffff'
}
```

返回值:

-   二维码图片的 base64 数据

## 2.drawQRCodeToCanvas: function (text, options)

    描述
    绘制二维码到 canvas

参数
text：必须，二维码内容，比如 url

options：参数对象

```
{
	x: 0,                   // 可选，二维码左上角点横坐标
	y: 0,                   // 可选，二维码左上角点纵坐标
	ctx: null,              // 必须，canvas绘制上下文或者canvasID
	ecc: 'H',               // 可选，容错级别，可选值L、M、Q和H（默认）
	size: 200,              // 可选，二维码尺寸，必须为整数。默认为200
	padding: 0,             // 可选，单侧空白边宽度，默认为0
	color: '#000000',       // 可选，二维码颜色，必须是16进制，默认为'#000000'
	background: '#ffffff'   // 可选，二维码背景色，必须是16进制，默认为'#ffffff'
}
```

返回值
无返回值

# Demo

-   wxml:

```
<view class="qrcode0">
    <image mode="widthFix" src="{{qrcode0}}"></image>
</view>
<view class="qrcode1">
    <canvas canvas-id="qrcode1"></canvas>
</view>
<view class="qrcodd2">
    <canvas canvas-id="qrcode2"></canvas>
</view>
```

-   wxjs:

```
const qrcode = require('../../lib/qrcode/index');

Page({
    data: {
        qrcode0: ''
    },
    onReady(){
        let text = 'https://m.baidu.com';

        // qrcode0
        let qrcode0 = qrcode.outputQRCodeBase64(text, {
            size: 400,
            color: '#CC6600',
            padding: 16,
            background: '#FFCC99'
        });

        this.setData({
            qrcode0
        })

        // qrcode1
        qrcode.drawQRCodeToCanvas(text, {
            ctx: 'qrcode1',
            size: 200,
            color: '#CC6600',
            padding: 16,
            background: '#FFCC99'
        });

        // qrcode2
        let qrcode2 = wx.createCanvasContext('qrcode2');
        qrcode.drawQRCodeToCanvas(text, {
            ctx: qrcode2,
            size: 200,
            color: '#CC6600',
            padding: 16,
            background: '#FFCC99'
        });
        qrcode2.draw();
    }
});
```
