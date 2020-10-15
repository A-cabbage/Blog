## window对象
在浏览器中，window既是通过JavaScript访问浏览器窗口的一个接口，又是ECMAScript规定的Global对象。在网页中定义任何对象、变量、函数，window都有权去访问它。  

由于window作为浏览器中的Global对象，因此在全局作用域中声明的所有变量、函数都会变成window的属性和方法。
  
 ```
 var age = 22
 function sayAge() {
    console.log(this.age)
 }
 
 console.log(window.age)         //22
 sayAge()                        //22
 window.sayAge()                 //22
 ```
 window对象的其他属性：  
 
  使用var声明的属性有一个[[Configurable]]的特性，这个特性的值为false，不能使用delete操作符来删除这个属性。  
  
  访问未声明的变量会报错，但是通过查询window对象，可以知道这个对象是否存在，若不存在返回undefined。  
  ```
  var name = 'tom'
  delete window.name;           //false
  
  name = 'jerry'
  delete window.name;           //true
  
  console.log(window.name)      //'tom'
  console.log(age)              //error
  console.log(window.age)       //undefined
  ```
 ## 窗口位置
 ```
 //窗口相对于屏幕左边的位置(IE,Safari,Opera,Chrome支持screen,Firefox支持screen)
 var leftPos = (typeof window.screenLeft == 'number') ? window.screenLeft : window.screenX;
 
 //窗口相对于屏幕上边的位置
 var topPos = (typeof window.screenTop == 'number') ? window.screenTop : window.screenY;
 ```
 ## 窗口大小
 ```
 window.innerWidth            //返回浏览器视口大小Chrome
 
 window.outerWidth            //返回浏览器窗口本身尺寸Firefox,IE9+,Safari
 
 document.documentElement.clientWidth      //返回浏览器视口大小IE,Chrome,Safari,Opera(标准模式)
 
 document.body.clientWidth      //返回浏览器视口大小(混杂模式)
 
 //获取浏览器视口大小
 var pageWidth = window.innerWidth,
     pageHeight = window.innerHeight;
 if(typeof pageWidth != 'number') {
    if(document.compatMode == 'CSS1Compat') {
        pageWidth = document.documentElement.clientWidth
        pageHeight = document.documentElement.clientHeight 
    } else {
        pageWidth = document.body.clientWidth
        pageHeight = document.body.clientHeight
    }
 }
 
 ```
 
 ## location对象
 
 https://github.com/A-cabbage/JavaScript/edit/master/article/BOM.md?q=javascript#testHash
 
 | 属性名 | 值 | 说明 |
 | --- | --- | --- |
 | hash | #testHash | 返回URL中#后面的字符串 |
 | host | github.com | 返回服务器名称和端口号 |
 | hostname | github.com | 返回不带端口号的服务器名称 | 
 | href | http://github.com/A-cabbage/JavaScript/edit/master/article/BOM.md?q=javascript#testHash | 返回当前页面完整的URL |
 | pathname | /A-cabbage/JavaScript/edit/master/article/BOM.md | 返回URL中的目录或文件名 |
 | port | "" | 返回URL中指定的端口号，如果不含端口号则返回空字符串 |
 | protocol | https | 返回页面使用的协议 |
 | search | ?q=javascript | 返回URL中查询字符串，这个字符串以问号开头 |
 
 我们可以通过字面量访问对象的形式来重新为location对象的属性赋值，并且除了hash外，改变其他属性值都会导致页面的重载。  
 
 ## history对象
 history对象保存着用户上网的历史记录，借助history可以实现页面前进和后退。  
 
 histroy.length属性表示历史记录的数量。  
 
 使用history.go()方法可以在用户的历史记录中任意跳转。go()方法接受一个参数，表示向前或向后跳转的页面数的一个整数值。如果这个整数值大于histroy.length值或小于histroy.length值的相反数，则go()方法什么也不做  
 ```
 history.go(-1)          //后退一页
 
 histroy.go(-100)         //不做任何处理
 
 history.go(2)           //前进两页
 
 history.go(100)         //不做任何处理
 ```
 也可以给go()方法传递一个字符串参数，此时会跳转到包含该字符串最近的一个位置，可能是后退也可能是前进。如果不包含这个字符串，则go()方法什么也不做  
 
 history提供了back()和forward()方法用来模仿浏览器的后退和前进。
 ```
 history.back()    //后退一页
 
 history.forward()  //前进一页
 ```
 
 
