- 判断滚动条到底部，需要用到DOM的三个属性值：
  - scrollTop：滚动条在Y轴上的滚动距离
  - offsetHeight：为内容可视区域的高度
  - scrollHeight：为内容可视区域的高度加上溢出（滚动）的距离

```javascript
//jquery
$('.container').scroll(function(){
    var scrollTop = $(this).scrollTop();
    var scrollHeight = $(this)[0].scrollHeight;
    var clientHeight = $(this)[0].offsetHeight;
    if(scrollTop + clientHeight == scrollHeight){
		alert("已经滑到底部了");
    }
});
//原生js
window.onscroll = function () {
    //滚动条y轴上的距离
    var scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
    //可视区域的高度
    var clientHeight = document.documentElement.clientHeight || document.body.clientHeight;
    //可视化的高度与溢出的距离（总高度）
    var scrollHeight = document.documentElement.scrollHeight || document.body.scrollHeight;
    if(scrollTop + clientHeight == scrollHeight){
             alert('已滚动到底部!')
         }
     }
```





