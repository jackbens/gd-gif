# 关于此项目

在nodejs使用过程中发现nodejs对图形支持很差，要做一个简单的图形验证码需要复杂的安装，且现有的如node-canvas,node-gyp-ccap等，都需要安装对应的支持库（C或C++编写）。感觉大而臃肿。
只需要一个验证码不需要如此的复杂。
BAIDU解决方案查看到有**无须组件的BMP版本**的解决方案
https://cnodejs.org/topic/581b2502e90cfbec054d763f
，感觉非常好，没有直接用只是为了抱着以练手为目的，写了一个**无须组件的GIF版本验证码**

![enter image description here](https://github.com/pzzcn/gd-gif/blob/master/1.png?raw=true)

# 限制


现在的版本还是比较初级的，内置字库只支持0-9的数字，不支持其它字符。
如果有需要，可以通过getCanvas()方法获取画布，直接操作画布即可。
比如你想在图片第二个点加入一个蓝色，你可以使用以下代码

    let g=new gif();
    g.pushColor("0066CC");
    let c=g.getCanvas();
    g[0][1]=g.getColorIndex("0066CC");

后通过g.getImage()即可获取图片流


# 安装

    npm install gd-gif

# 使用范例

引用库

    const gif=require("gd-gif");

使用例子1

    async getVerificationCodeImage(par){
        let g=new gif();
        //设置验证码宽度
        g.setWidth(100);
        //设置验证码高度
        g.setHeight(50);
        let code="";
        //随机4位生成验证码
        for(let i=0;i<4;i++){
            code+=g.rand(0,9);
        }
        g.setVerificationCode(code);
        return g.getImage();
    }
   使用例子2

    async verificationCodeService(par){
      let g=new gif();
      g.setWidth(100);
      g.setHeight(29);
      g.pushColor("0055FF");
      g.pushColor("0066CC");
      g.pushColor("ff2100");
      g.pushColor("00a23d");
      g.drawText("0",3,3,"0055FF");
      g.drawText("1",23,3,"0066CC");
      g.drawText("2",43,5,"ff2100");
      g.drawText("9",63,5,"00a23d");
      return g.getImage();
    }

# 方法


setWidth//宽度
参数：number


setHeight//设置高度
参数：number


setBackground//设备背景颜色
参数：16进制RGB色，如0066cc


pushColor//向GIF索引中添加颜色
参数：16进制RGB色，如0066cc


drawText//添加文字到图片中
参数：单个文字,x坐标,y坐标,16进制RGB色


getCanvas//得到内部的画布，是一个二维数组，可直接操作内存对象使用
参数：无


getImage//获得最后的输出流
参数：无


setVerificationCode//生成验证码，参考示例1
参数：验证码字符


