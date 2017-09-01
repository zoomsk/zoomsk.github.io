### 1. 获取一组元素的最大宽度或高度
```js
var getMaxHeight = function ($elms) {
  var maxHeight = 0;
  $elms.each(function () {
    // In some cases you may want to use outerHeight() instead
    var height = $(this).height();
    if (height > maxHeight) {
      maxHeight = height;
    }
  });
  return maxHeight;
};
// 使用方法
$(elements).height( getMaxHeight($(elements)) );
```
### 限制文本字数
下面这端脚本允许你根据给定的字符长度截取文本，如果文本被截取，那么它的后面会自动带上省略号。
```js
    function excerpt(str, nwords) {
      var words = str.split(' ');
      words.splice(nwords, words.length-1);
      return words.join(' ') +
        (words.length !== str.split(' ').length ? '…' : '');
    }
```
[更多js片段](http://www.jianshu.com/p/3ef822ec5a63)
