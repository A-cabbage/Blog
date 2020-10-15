注： 不同浏览器之间可能会存在差异

## 1.偏移量

元素的可见大小由其高度、宽度决定，包括所有的内边距，滚动条和边框大小（不包括外边框大小）。  

通过这四个属性可取得元素的偏移量。  

**offsetHeight： 元素在垂直方向上占用空间的大小。包括元素的高度、上边距高度和下边距高度、上边框高度和下边框高度。**  
**offsetWeight： 元素在水平方向上占用空间的大小。包括元素的宽度、左边距宽度和右边距宽度、左边框宽度和右边框宽度。**  
**offsetTop： 元素在上边框外至包含元素的上内边距之间的像素距离。**  
**offsetLeft： 元素在左边框外至包含元素的左内边距之间的像素距离。**  

其中offsetTop和offsetLeft属性与包含元素有关，包含元素的引用保存在offsetParent中。offsetParent不一定与parentNode值相等。

![元素的位置大小偏移量关系图](../image/1602732448(1).jpg)

知道这些关系，我们就可以计算出元素的左和上偏移量。

```
//计算元素的左偏移量
function getElementLeft(element) {
  var actualLeft = element.offsetLeft;
  var current = element.offsetParent;
  
  while(current !== null) {
    actualLeft += current.offsetLeft;
    current = current.offsetParent;
  }
  
  return acturalLeft;
}


//计算元素的上偏移量
function getElementTop(element) {
  var actualTop = element.offsetTop;
  var current = element.offsetParent;
  
  while(current !== null) {
    actualTop += current.offsetTop;
    current = current.offsetParent;
  }
  
  return actualTop;
}
```

## 2.客户区大小

元素的客户区大小指的是元素的内容及其内边距占据的空间大小。  

**clientWeight： 元素内容区宽度加左右内边距宽度。**  
**clientHeight： 元素内容区域高度加上下内边距高度。**

获取元素的客户区大小
```
function getViewport(element) {
  //检查浏览器是否运行在混杂模式中
  if(document.compatMode == 'BackCompat') {
    return {
      width: document.body.clientWeight,
      height: document.body.clientHeight
    }
  } else {
    return {
      width: document.documentElement.clientWeight,
      height: document.documentElement.clientHeight 
    }
  }
}
```

## 3.滚动大小

滚动大小指的是包含滚动内容的元素的大小。  

**scrollHeight： 在没有滚动条的情况下，元素内容的总高度。**  
**scrollWeight： 在没有滚动条的情况下，元素内容的总宽度。**  
**scrollTop： 被隐藏在内容区域上方的像素值（即出现滚动条时，被隐藏的内容高度）。**  
**scrollLeft： 被隐藏在内容区域左侧的像素值。**

## 4.确定元素大小

浏览器为元素提供了getBoundingClientRect()方法。这个方法返回一个矩形对象，包含当前元素的大小及相对视口的位置。  

我们定义一个这样的元素
```
var el = document.createElement('div');
el.style.cssText = "width: 100px; height: 100px; border: 1px solid #2D8CF0; padding: 10px;"
document.body.appendChild(el)

var rect = el.getBoundingClientRect();
console.log(rect)       //{bottom: 130, left: 8, top: 8, right: 130, height: 122, width: 122, x: 8, y: 8}   (这里body有8px外边距)

```

