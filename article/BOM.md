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
 
 
