# keydom移动端框架
keydom是一个快速构建移动端的css框架，改文章主要介绍其中的用法
### index.html
      <!doctype html>
      <html>
      <head>
          <meta charset="utf-8">
          <meta http-equiv="x-ua-compatible" content="ie=edge">
          <meta name="viewport"
                content="width=device-width, initial-scale=1.0, user-scalable=0,minimum-scale,maximum-scale=1.0">
          <title>标题</title>
          <link rel="stylesheet" href="css/mobile.css">
          <script src="js/mobile.js"></script>

      </head>
      <body>

      </body>
      </html>

### css常用类
`.flex` 布局基本类
```css
display: -webkit-flex;
display: flex;
flex-flow: wrap row;
justify-content: space-between;
```

`.flex-cc` 布局 水平垂直居中
```css
justify-content: center;
align-items: center;
```


`.flex-around` 布局 平均分配布局

```css
justify-content: space-around;
```

`.clearfix` 清除浮动

```css
.clearfix {
    display: table;
    clear: both;
}
.clearfix:before,
.clearfix:after {
    display: table;
    content: "";
    clear: both;
}
```

表单布局左右`.form-group-line`,单行`.form-group`

```html
    <!-- 左右表单布局： -->
      <div class="form-group-line">
          <label class="flex1">account：</label>
          <input type="text">
      </div>

      <!-- 单行表单布局 -->
      <div class="flex form-group">
          <label>account：</label>
          <input type="text" placeholder="account">
      </div>

```

图片宽度自适应`.pull-fill`

    width: 100%;

### mobile.js
1.把`PSD_WIDTH`设置为设计图的大小;
2.根据计算，css中1rem为设计图100px，意思就是设计图高度为60px则css中写为.6rem，即实际`css = psdcss/100(rem)`



```js
    (function () {
        var PSD_WIDTH = 1080; //.psd width
        function changeRem() {
            var width = document.documentElement.clientWidth;
            document.documentElement.style.fontSize = width * 100 / PSD_WIDTH + 'px';
        }
        changeRem();
        window.addEventListener('resize', function () {
            changeRem();
        })
    })()
     //Tip: 设置为*100是因为在浏览器中调试的时候有些浏览器支持的字体>=12px，所以直接*100然后再使用的时候再除以100
```
