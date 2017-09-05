###tip1  常见的颜色及其心里联想
> **颜色**  心里联想  
> **红色**  力量、活力、爱、激情、进攻、危险    
> **蓝色**  信任、保守、安全、清洁、悲伤、有序   
> **绿色**  大自然、健康、嫉妒、复苏  
> **橙色**  愉快、幸福    
> **黄色**  乐观、希望、冷静、懦弱  
> **褐色**  可靠、舒适、忍耐、大地  
> **灰色/银色**  智慧、未来、谦虚、悲哀、腐朽、高雅  
> **黑色**  力量、性、完善、神秘、恐惧、忧愁、死亡  
> **白色**  纯洁、干净、精确、洁白、中性、不毛、死亡  

###tip2 css支持颜色17种  
black黑色、silver银色、gray灰色、white白色、maroon栗色、purple紫色、fuchsia紫红色、green绿色、lime鲜红色、blur蓝色、red红色、olive橄榄色、yellow换色、navy藏青色、teal枭蓝色、aqua浅蓝绿色、orange橙色 



<!-- 简体中文 -->
<html lang="zh-cmn-Hans">


# IE 兼容模式

优先使用最新版本的IE 和 Chrome 内核

<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">  
# SEO 优化

	<head>
	    <meta charset="utf-8">
	    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
	    <!-- SEO -->
	    <title>Style Guide</title>
	    <meta name="keywords" content="your keywords">
	    <meta name="description" content="your description">
	    <meta name="author" content="author,email address">
	</head>  
 
#  移动设备优先
<meta name="viewport" content="width=device-width, initial-scale=1.0">

# 链接的样式顺序：

a:link -> a:visited -> a:hover -> a:active（LoVeHAte）

#异步加载第三方内容

当你无法保证嵌入第三方内容比如 Youtube 视频或者一个 like/tweet 按钮可以正常工作的时候，你需要考虑用异步加载这些代码，避免阻塞整个页面加载。

```js
(function() {

	    var script,
	        scripts = document.getElementsByTagName('script')[0];

	    function load(url) {
	      script = document.createElement('script');
	      script.async = true;
	      script.src = url;
	      scripts.parentNode.insertBefore(script, scripts);
	    }

	    load(docsjs);
	    load(docsjs);
	    load(docsjs);

	}());(function() {

	    var script,
	        scripts = document.getElementsByTagName('script')[0];

	    function load(url) {
	      script = document.createElement('script');
	      script.async = true;
	      script.src = url;
	      scripts.parentNode.insertBefore(script, scripts);
	    }

	    load(docsjs);
	    load(docsjs);
	    load(docsjs);

	}());
```

# 电话号码识别

iOS Safari ( Android 或其他浏览器不会) 会自动识别看起来像电话号码的数字，将其处理为电话号码链接，比如：

7位数字，形如：1234567
带括号及加号的数字，形如：(+86)123456789
双连接线的数字，形如：00-00-00111
11位数字，形如：13800138000
	<!-- 关闭电话号码识别： -->
	<meta name="format-detection" content="telephone=no" />
	
	<!-- 开启电话功能： -->
	<a href="tel:123456">123456</a>
	
	<!-- 开启短信功能： -->
	<a href="sms:123456">123456</a>