#### 02|Visual(视觉)

##### 01|Circle(圆)

通过纯CSS创建圆

```html
<div class="circle"></div>
```

```css
.circle {
  border-radius: 50%;
  width: 2rem;
  height: 2rem;
  background: #333;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a8r3ad9oj30k601kjr6.jpg)

**Explanation**

border-radius：50％曲线元素的边框以创建圆。 由于圆在任何给定点具有相同的半径，因此width和height必须相同。不同的值将创建一个椭圆。

**Browser support 97.7%**



##### 02|Counter(计数器)

计数器本质上是由CSS维护的变量，其值可以通过CSS规则递增以跟踪它们被使用的次数。

```html
<ul>
  <li>List item</li>
  <li>List item</li>
  <li>
    List item
    <ul>
      <li>List item</li>
      <li>List item</li>
      <li>List item</li>
    </ul>
  </li>
</ul>
```

```css
ul {
  counter-reset: counter;
}
li::before {
  counter-increment: counter;
  content: counters(counter, '.') ' ';
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a8su78nsj30k805z3yk.jpg)

**Explanation**

您可以使用任何类型的HTML创建有序列表。

 counter-reset初始化计数器，该值是计数器的名称。默认情况下，计数器从0开始。此属性还可用于将其值更改为任何特定数字。 

counter-increment用于可计数的元素。一旦counter-reset初始化，计数器的值可以增加或减少。

 counter（name，style）显示节计数器的值。通常用于content属性。此函数可以接收两个参数，第一个作为计数器的名称，第二个参数可以是decimal或上upper-roman（默认为decimal）。 

counter（counter，string，style）显示节计数器的值。通常用于内容属性。此函数可以接收三个参数，第一个作为计数器的名称，第二个可以包含一个字符串，它位于计数器之后，第三个可以是十进制或上罗马（默认为十进制）。

 CSS计数器对于制作轮廓列表特别有用，因为计数器的新实例是在子元素中自动创建的。使用counters（）函数，可以在不同级别的嵌套计数器之间插入分隔文本。

**Browser support 99.9%**



##### 03|Custom scrollbar (自定义滚动栏)

在WebKit平台上自定义具有可滚动溢出的文档和元素的滚动条样式。

```html
<div class="custom-scrollbar">
  <p>
    Lorem ipsum dolor sit amet consectetur adipisicing elit.<br />
    Iure id exercitationem nulla qui repellat laborum vitae, <br />
    molestias tempora velit natus. Quas, assumenda nisi. <br />
    Quisquam enim qui iure, consequatur velit sit?
  </p>
</div>
```

```css
.custom-scrollbar {
  height: 70px;
  overflow-y: scroll;
}
/* To style the document scrollbar, remove `.custom-scrollbar` */
.custom-scrollbar::-webkit-scrollbar {
  width: 8px;
}
.custom-scrollbar::-webkit-scrollbar-track {
  box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
  border-radius: 10px;
}
.custom-scrollbar::-webkit-scrollbar-thumb {
  border-radius: 10px;
  box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.5);
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a8xlr7hhg30kf02qdic.gif)

**Explanation**

:: - webkit-scrollbar以整个滚动条元素为目标。 

:: - webkit-scrollbar-track仅定位滚动条轨道。

:: - webkit-scrollbar-thumb以滚动条拇指为目标。

 还有许多其他伪元素可用于设置滚动条的样式。有关更多信息，请访问WebKit博客。

**Browser support 90.7% 滚动条样式似乎不在任何标准轨道上。**



##### 04|Custom text selection(更改文本选择的样式)

更改文本选择的样式

```html
<p class="custom-text-selection">Select some of this text.</p>
```

```css
::selection {
  background: aquamarine;
  color: black;
}
.custom-text-selection::selection {
  background: deeppink;
  color: white;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a932wjwog30kf02kabd.gif)

**Explanation**

:: selection在元素上定义一个伪选择器，以便在选中时为其中的文本设置样式。请注意，如果您未将任何其他选择器组合在一起，则您的样式将应用于文档根级别，并应用于任何可选元素。

**Browser support 86.5% 需要前缀以获得完全支持，并且实际上并不在任何规范中。**



##### 05|Dynamic shadow(动态阴影)

创建类似于box-shadow的阴影，但基于元素本身的颜色。

```html
<div class="dynamic-shadow"></div>
```

```css
.dynamic-shadow {
  position: relative;
  width: 10rem;
  height: 10rem;
  background: linear-gradient(75deg, #6d78ff, #00ffb8);
  z-index: 1;
}
.dynamic-shadow::after {
  content: '';
  width: 100%;
  height: 100%;
  position: absolute;
  background: inherit;
  top: 0.5rem;
  filter: blur(0.4rem);
  opacity: 0.7;
  z-index: -1;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a96wharsg30kf05caak.gif)

**Explanation**

position：元素上的relative为psuedo-elements建立一个Cartesian定位上下文.

z-index：1建立新的堆叠上下文。 ::之后定义一个伪元素。 

position：absolute将伪元素从文档流中取出，并将其相对于父文档定位。 

width：100％和height：100％调整伪元素的大小以填充其父元素的尺寸，使其大小相等。

background：inherit导致伪元素继承元素上指定的线性渐变。 

top：0.5rem将伪元素从其父元素略微偏移。 

filter：blur（0.4rem）将模糊伪元素以创建下方阴影的外观。

opacity：0.7使伪元素部分透明。 

z-index：-1将伪元素定位在父元素后面但位于背景前面。

**Browser support 94.2% 必须写前缀才能完全支持**



##### 06|Etched text(蚀刻文字)

创建一种效果，其中文本看起来“蚀刻”或雕刻在背景中。

```html
<p class="etched-text">I appear etched into the background.</p>
```

```css
.etched-text {
  text-shadow: 0 2px white;
  font-size: 1.5rem;
  font-weight: bold;
  color: #b8bec5;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a9coq2lhg30kf03940p.gif)

**Explanation**

text-shadow：0 2px white在原点位置创建一个水平偏移0px和垂直偏移2px的白色阴影。

 背景必须比阴影更暗，以使效果起作用。 

文字颜色应略微褪色，使其看起来像是在背景上雕刻/雕刻。

**Browser support 99.5%** 



##### 07|Fit image in container(适合容器中的图像)

更改图像在其容器内的适合度和位置，同时保留其纵横比。以前只能使用背景图像和background-size属性。

```html
<img class="image image-contain" src="https://picsum.photos/600/200" />
<img class="image image-cover" src="https://picsum.photos/600/200" />
```

```css
.image {
  background: #34495e;
  border: 1px solid #34495e;
  width: 200px;
  height: 200px;
}
.image-contain {
  object-fit: contain;
  object-position: center;
}
.image-cover {
  object-fit: cover;
  object-position: right top;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a9fdspqzj30k906fdga.jpg)

**Explanation**

object-fit：包含适合容器内的整个图像，同时保留其纵横比。 

物体贴合：盖子用图像填充容器，同时保持其纵横比。 

object-position：[x] [y]将图像定位在容器内。

**Browser support 95.5%**



##### 08|Fullscreen

全屏CSS伪类表示浏览器处于全屏模式时显示的元素。

```html
<div class="container">
  <p><em>Click the button below to enter the element into fullscreen mode. </em></p>
  <div class="element" id="element"><p>I change color in fullscreen mode!</p></div>
  <br />
  <button onclick="var el = document.getElementById('element'); el.requestFullscreen();">
    Go Full Screen!
  </button>
</div>
```

```css
.container {
  margin: 40px auto;
  max-width: 700px;
}
.element {
  padding: 20px;
  height: 300px;
  width: 100%;
  background-color: skyblue;
}
.element p {
  text-align: center;
  color: white;
  font-size: 3em;
}
.element:-ms-fullscreen p {
  visibility: visible;
}
.element:fullscreen {
  background-color: #e4708a;
  width: 100vw;
  height: 100vh;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a9ol9cm7g31h00s3n49.gif)

**Explanation**

`fullscreen` CSS伪类选择器用于选择和设置以全屏模式显示的元素。

**Browser support 85.6%**



##### 09|Gradient text(渐变文字)

为文本提供渐变颜色

```html
<p class="gradient-text">Gradient text</p>
```

```css
.gradient-text {
  background: -webkit-linear-gradient(pink, red);
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a9szazf2j30k402aq2q.jpg)

**Explanation**

background：-webkit-linear-gradient（...）为文本元素提供渐变背景。 

webkit-text-fill-color：透明用透明颜色填充文本。 

webkit-background-clip：文本使用文本剪切背景，使用渐变背景填充文本作为颜色。

**Browser support 94.1% 使用非标准属性**



##### 10|Overflow scroll gradient(溢出滚动渐变)

向溢出元素添加渐变渐变以更好地指示要滚动的内容更多。

```html
<div class="overflow-scroll-gradient">
  <div class="overflow-scroll-gradient__scroller">
    Lorem ipsum dolor sit amet consectetur adipisicing elit. <br />
    Iure id exercitationem nulla qui repellat laborum vitae, <br />
    molestias tempora velit natus. Quas, assumenda nisi. <br />
    Quisquam enim qui iure, consequatur velit sit? <br />
    Lorem ipsum dolor sit amet consectetur adipisicing elit.<br />
    Iure id exercitationem nulla qui repellat laborum vitae, <br />
    molestias tempora velit natus. Quas, assumenda nisi. <br />
    Quisquam enim qui iure, consequatur velit sit?
  </div>
</div>
```

```css
.overflow-scroll-gradient {
  position: relative;
}
.overflow-scroll-gradient::after {
  content: '';
  position: absolute;
  bottom: 0;
  width: 240px;
  height: 25px;
  background: linear-gradient(
    rgba(255, 255, 255, 0.001),
    white
  ); /* transparent keyword is broken in Safari */
  pointer-events: none;
}
.overflow-scroll-gradient__scroller {
  overflow-y: scroll;
  background: white;
  width: 240px;
  height: 200px;
  padding: 15px;
  line-height: 1.2;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3aa0qt1v2g30kf06hqb8.gif)

**Explanation**

position：父级的相对为伪元素建立笛卡尔定位上下文。 

::之后定义一个伪元素。 

background-image：线性渐变（...）添加一个从透明变为白色（从上到下）的线性渐变。 

position：absolute将伪元素从文档流中取出，并将其相对于父文档定位。 

width：240px匹配滚动元素的大小（它是具有伪元素的父元素的子元素）。 

height：25px是渐变渐变伪元素的高度，应该保持相对较小。 

bottom：0将伪元素定位在父元素的底部。 

pointer-events：none指定伪元素不能是鼠标事件的目标，允许其后面的文本仍然是可选择/交互的。

**Browser support 97.5%**