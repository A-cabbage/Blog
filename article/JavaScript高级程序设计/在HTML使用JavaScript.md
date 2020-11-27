### 如何在HTML中使用JavaScript？
***
向HTML页面中插入JavaScript的主要方法就是使用<script>元素  

#### 使用方式  

使用<script>元素的方式有两种：  

1.直接在页面中嵌入JavaScript代码  
```
<script type="text/javascript">
  document.write('hello!我是内部嵌入的JavaScript代码')
</script>
```
2.引入外部JavaScript文件，通过src属性指向外部JavaScript文件的链接
```
<script type="text/javascript" src="example.js"></script>
```
使用src属性的<script>元素不应该在标签内部之前再编写额外的JavaScript代码，如果包含了嵌入的代码，则只会下载并执行外部脚本，嵌入的代码会被忽略。  
```
<script type="text/javascript" src="example.js">
  //此代码不会执行，会被浏览器忽略，此处加载的是外部引入的example.js文件
  documnet.write('hello!我是内部嵌入的JavaScript')
</script>
```

通过<script>元素的src属性还可以加载不同域的JavaScript文件，这里也可以通过<script>标签来实现跨域请求  

#### 加载过程

在浏览器对JavaScript代码进行解析的过程中，页面中的其余内容都不会被浏览器加载或显示，也就是说解析JavaScript代码会阻塞页面渲染HTML以及CSS样式。如果我们不想让JavaScript代码阻塞浏览器渲染页面，这时候就要说一下它的async和defer这两个属性了。  

**async: 可选，表示应该下载脚本但不妨碍页面中的其他操作，即异步下载脚本并且立即执行脚本，只对外部引入脚本文件有效**  
  
**defer: 可选，表示脚本可以延迟到文档完全被解析和显示之后再执行，即异步下载脚本并且等待文档完全被解析完成后执行脚本，只对外部引入脚本文件有效**  

带有async属性的<script>元素解析顺序并不能确保一致，defer属性的<script>在整个文档加载完成后会依次执行

如果<script>元素中不包含async和defer属性，则浏览器会按照<script>元素在页面中的出现顺序对它们进行依次解析。所以对于有很多外部引入的JavaScript文件建议放在<body>元素中页面的内容后面  

