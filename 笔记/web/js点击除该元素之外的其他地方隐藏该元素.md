**判断点击事件发生在区域外的条件是：**

1. 点击事件的对象不是目标区域本身
2. 事件对象同时也不是目标区域的子元素

**方法一:**

`首先点击document任意位置隐藏该元素，然后给该元素绑定click事件，阻止冒泡到该元素，则可以顺利实现需求。`

**方法二:**

```javascript
 $(document).on('click', null, function(event) {
        if(($('.element').has($(event.target)).length === 0) && 			       !$(event.target).hasClass('element')) {
          	//隐藏操作
        }
    });
```

