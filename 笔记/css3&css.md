[TOC]

##CSS3###

### CSS3边框###

`css:Cascading Style Sheets`

`媒体查询@media 设备类型 and (设备特性) `

```
圆角边框:border-radius
边框阴影：box-shadow  
	h-shadow--水平位置
	v-shadow--垂直位置
	blur--模糊值
	color--阴影颜色
	inset--外部阴影改为内部阴影
图片边框：border-image 属性 
	border-image-source--图片路径
	border-image-slice--图片边框向内偏移
	border-image-width--图片边框的宽度
	border-image-repeat--是否平铺  (repeated平铺 rounded铺满 stretched拉伸)
```

### CSS3背景###

```
background-size   属性规定背景图片的尺寸
	cover--把背景图像扩展至足够大，以使背景图像完全覆盖背景区域
	contain--把图像图像扩展至最大尺寸，以使其宽度和高度完全适应内容区域
background-origin  属性规定背景图片的定位区域
	padding-box--背景图像相对于内边距框来定位
	border-box--背景图像相对于边框盒来定位
	content-box--背景图像相对于内容框来定位
background-clip 属性规定背景的绘制区域
	border-box--背景被裁剪到边框盒
	padding-box--背景被裁剪到内边距框
	content-box--背景被裁剪到内容框
```

### 文本效果###

```
text-shadow 参数 水平阴影、垂直阴影、模糊距离，以及阴影的颜色
word-wrap 允许对长单词进行拆分，并换行到下一行
```

### CSS3字体###

```
@font-face
{
font-family: myFirstFont;
src: url('Sansation_Bold.ttf'),
     url('Sansation_Bold.eot'); /* IE9+ */
font-weight:bold;
}
```

### CSS3 转换###

```
transform 向元素应用 2D 或 3D 转换
translate()  从其当前位置移动，根据给定的 left（x 坐标） 和 top（y 坐标）
 rotate()  元素顺时针旋转给定的角度。允许负值，元素将逆时针旋转
 scale() 定义 2D 缩放转换，根据给定的宽度（X 轴）和高度（Y 轴）
 skew() 元素倾斜转换，根据给定的水平线（X 轴）和垂直线（Y 轴）
 perspective 规定3D元素的透视效果
```

### CSS3过渡动画###

```
transition  简写属性，用于在一个属性中设置四个过渡属性
transition-property 规定应用过渡的 CSS 属性的名称
transition-duration 定义过渡效果花费的时间。默认是 0
transition-timing-function 规定过渡效果的时间曲线。默认是 "ease"
transition-delay 规定过渡效果何时开始。默认是 0
```

### CSS3动画###

```
@keyframes 规定动画
{
from {background: red;}
to {background: yellow;}
}
animation 所有动画属性的简写属性  动画完成所花费的时间，动画的速度曲线，动画何时开始，动画被播放的次数，
动画是否在下一周期逆向地播放
```

### CSS3多列###

```
column-count 属性规定元素应该被分隔的列数
column-gap 属性规定列之间的间隔
column-rule 属性设置列之间的宽度、样式和颜色规则
```

###CSS3用户界面###

```
resize 属性规定是否可由用户调整元素尺寸
box-sizing 属性允许您以确切的方式定义适应某个区域的具体内容
```

## HTML5##

###新特性###

```
用于绘画的 canvas 元素
用于媒介回放的 video 和 audio 元素
对本地离线存储的更好的支持
新的特殊内容元素，比如 article、footer、header、nav、section
新的表单控件，比如 calendar、date、time、email、url、search
```

### 视频###

```
标签video 支持Ogg、MPEG4、WebM
control 属性供添加播放、暂停和音量控件
loop 则当媒介文件完成播放后再次开始播放
方法：
	play()、pause()、load()
属性：	paused、error、width	
```

### 音频###

```
标签audio 支持Ogg Vorbis、MP3、Wav
control 属性供添加播放、暂停和音量控件
autoplay 音频在就绪后马上播放
loop 循环播放
```

### 拖放###

```
draggable 属性设置为 true 可以拖放
ondragstart()
dataTransfer.setData() 方法设置被拖数据的数据类型和值
ondragover 事件规定在何处放置被拖动的数据
调用 preventDefault() 来避免浏览器对数据的默认处
```

### 画布###

```
标签canvas
canvas 元素本身是没有绘图能力的。所有的绘制工作必须在 JavaScript 内部完成
1.var c=document.getElementById("myCanvas")
2.var cxt=c.getContext("2d") 创建对象
fillStyle 方法设置颜色，fillRect 方法规定了形状、位置和尺寸

```

### 地理定位###

```
getCurrentPosition() 方法来获得用户的位置
coords.latitude 十进制数的纬度
coords.longitude 十进制数的经度
coords.accuracy 位置精度
```

### Web存储###

```
localStorage 方法存储的数据没有时间限制
sessionStorage 方法针对一个 session 进行数据存储
```

### 应用缓存###

```
manifest 文件是简单的文本文件，它告知浏览器被缓存的内容
manifest 文件可分为三个部分：
	CACHE MANIFEST - 在此标题下列出的文件将在首次下载后进行缓存
	NETWORK - 在此标题下列出的文件需要与服务器的连接，且不会被缓存
	FALLBACK - 在此标题下列出的文件规定当页面无法访问时的回退页面（比如 404 页面）
```

### Input类型###

```
email、url、number、range(类型显示为滑动条)、Date (date, month, week, time, datetime, datetime-local)、search、color、image
```

### 表单元素###

```
datalist 元素规定输入域的选项列表
Webpage: <input type="url" list="url_list" name="link" />
<datalist id="url_list">
<option label="W3School" value="http://www.W3School.com.cn" />
<option label="Google" value="http://www.google.com" />
<option label="Microsoft" value="http://www.microsoft.com" />
</datalist>
```

### 表单属性###

```
autocomplete 属性规定 form 或 input 域应该拥有自动完成功能 on/off 开启/关闭
autofocus 属性规定在页面加载时，域自动地获得焦点
form 属性规定输入域所属的一个或多个表单，form 属性必须引用所属表单的 id
height 和 width 属性规定用于 image 类型的 input 标签的图像高度和宽度
max 属性规定输入域所允许的最大值
min 属性规定输入域所允许的最小值
step 属性为输入域规定合法的数字间隔
multiple 属性规定输入域中可选择多个值
novalidate 属性规定在提交表单时不应该验证 form 或 input 域
pattern 属性规定用于验证 input 域的模式
placeholder 属性提供一种提示
required 属性规定必须在提交之前填写输入域（不能为空）
```

