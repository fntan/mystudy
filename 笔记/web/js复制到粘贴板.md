### 常见方法

+ 第三方库：clipboard.js
+ 原生方法：document.execCommand()

### clipboard.js

clipboard的官网：[clipboardjs.com/](https://link.juejin.im/?target=https%3A%2F%2Fclipboardjs.com%2F)。

### 原生方法

document.execCommand()，它只能操作**可编辑区域**，也就是意味着除了 `<input>`、`<textarea>` 这样的输入域以外，是无法使用这个方法的。使用时需要动态创建input标签

```javascript
<button id="btn">点我复制</button>

const btn = document.querySelector('#btn');
btn.addEventListener('click',() => {
	const input = document.createElement('input');
	document.body.appendChild(input);
 	input.setAttribute('value', '要复制的内容');
	input.select();
	if (document.execCommand('copy')) {
		document.execCommand('copy');
		console.log('复制成功');
	}
    document.body.removeChild(input);
})
```

