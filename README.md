# Dom-->Cavans-->Img下载
### 一、适用场景

H5页面，用户需要对Dom元素截图，比如：1、进入H5页面后做了一些测试题，答题完毕会生成测试结果，用户可以把测试结果或者题生成一张图片，从而可以保存图片到本地或者分享出去。2、用户进入某个名片页面，需要对名片进行保存到本地。

### 二、效果图

**H5名片页面：**(第一张：H5页面；第二张：生成的图片。)

<div style="display: fex;">
<img src="https://github.com/liuerwa/DOM-Canvas-Download/raw/master/images/1.png" width="200">
    <img src="https://github.com/liuerwa/DOM-Canvas-Download/raw/master/images/2.png" width="200">
</div>

### 三、关键代码

**需要引入的js：**html2canvas.js（此仓库js文件夹里面有这个js）

html对应的具体css请看此仓库css文件夹

**需要生成的Dom节点：**

```html
<div id="app">
    <div class="title title1">
        <span class="span1">姓名：</span>
        <span class="span2">刘大王</span>
    </div>
    <div class="title">
        <span class="span1">QQ：</span>
        <span class="span2">826557140</span>
    </div>
    <div class="title">
        <span class="span1">Email：</span>
        <span class="span2">1996@liuerwa.cn</span>
    </div>
    <div class="title">
        <span class="span1">Github：</span>
        <span class="span2">https://github.com/liuerwa</span>
    </div>
</div>
```

**用户点击按钮后页面的变化：**

```html
//存放生成的Img标签
<div id="img"></div>
//点击生成图片按钮
<div class="btn" onclick="generateImage()">生成图片</div>
//生成图片成功后显示的提示文字
<div class="tip">图片已生成，请长按屏幕保存！</div>
```

**生成图片操作：**

```javascript
//生成图片
  function generateImage() {
    // 获取想要转换的dom节点
    var dom = document.querySelector("#app");
    var box = window.getComputedStyle(dom);
    // dom节点计算后宽高
    var width = parseValue(box.width);
    var height = parseValue(box.height);
    // 获取像素比
    var scaleBy = getDpr();
    // 创建自定义的canvas元素
    var canvas = document.createElement('canvas');
    // 设置canvas元素属性宽高为 DOM 节点宽高
    canvas.width = width;
    canvas.height = height;
    // 设置canvas css 宽高为DOM节点宽高
    canvas.style.width = width + 'px';
    canvas.style.height = height + 'px';
    // 获取画笔
    var context = canvas.getContext('2d');
    // 将所有绘制内容放大像素比倍
    context.scale(scaleBy, scaleBy);
    var w = width;
    var h = height;
	//生成canvas并渲染（关键）
    html2canvas(dom, {
      allowTaint: true,
      width: w,
      height: h,
      useCORS: true
    }).then(function (canvas) {
      // 将canvas转换成图片渲染到页面上
      var url = canvas.toDataURL('image/png');// base64数据
      var image = new Image();
      image.src = url;
      image.width = w;
      image.height = h;
      document.getElementById('img').appendChild(image);
      document.getElementsByClassName("btn")[0].style.display = 'none'
      document.getElementsByClassName("tip")[0].style.display = 'block'
    });
  }
```

### 四、说明

这只是最简单的H5转换DOM对象保存图片，还有PC端转换DOM调用浏览器下载图片、使用Vue来完成相应操作等，后续会整理出来。

欢迎大家相互探讨指教，有什么问题请留言，谢谢！





