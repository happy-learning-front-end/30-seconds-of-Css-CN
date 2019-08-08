#### 01|Layout(布局)

##### 01|Box-sizing rest(盒子模型重置)

重置框模型，使宽度和高度不受其边框或填充的影响

```html
<div class="box">border-box</div>
<div class="box content-box">content-box</div>
```

```css
html {
  box-sizing: border-box;
}
*,
*::before,
*::after {
  box-sizing: inherit;
}
.box {
  display: inline-block;
  width: 150px;
  height: 150px;
  padding: 10px;
  background: tomato;
  color: white;
  border: 10px solid red;
}
.content-box {
  box-sizing: content-box;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a3y0u15lj30ml05n74c.jpg)

**Explanation**

box-sizing：border-box使填充或边框的添加不会影响元素的宽度或高度。

box-sizing：inherit使元素继承其父级的box-sizing规则。

**Browser support  99.9%**



##### 02|ClearFix(清除浮动)

确保元素自我清除子元素

注意:这仅仅在您仍使用float构建布局时才有用,请考虑使用Flexbox布局或者是网格布局的现代方法!

```html
<div class="clearfix">
  <div class="floated">float a</div>
  <div class="floated">float b</div>
  <div class="floated">float c</div>
</div>
```

```css
.clearfix::after {
  content: '';
  display: block;
  clear: both;
}
.floated {
  float: left;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a489bwwhj30gg01c0sj.jpg)

**Explanation**

.clearfix ::之后定义了一个伪元素

content：''允许伪元素影响布局。

clear：both表示元素的左侧，右侧或两侧不能与同一块格式化上下文中较早浮动的元素相邻。

**Brower support 100%**

**注意:**

要使此代码段正常工作，您需要确保容器中没有非浮动子项，并且在clearfixed容器之前没有高浮点数，但是在相同的格式化上下文中（例如浮动列）。



##### 03|Constant width to height ratio(恒定宽高比)

给定宽度可变的元素，它将确保其高度以响应方式保持成比例（即，其宽高比保持不变）。

```html
<div class="constant-width-to-height-ratio"></div>
```

```css
.constant-width-to-height-ratio {
  background: #333;
  width: 50%;
}
.constant-width-to-height-ratio::before {
  content: '';
  padding-top: 100%;
  float: left;
}
.constant-width-to-height-ratio::after {
  content: '';
  display: block;
  clear: both;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a4fyx1rlj30me0ba3yi.jpg)

**Explanation**

:: before伪元素上的padding-top导致元素的高度等于其宽度的百分比。因此，100％表示元素的高度始终为宽度的100％，从而创建响应方块。

 此方法还允许将内容正常放置在元素内。

**Brower support 100%**



##### 04|Display table centering(显示表格居中)

使用display：table（作为flexbox的替代）在其父元素中垂直和水平居中子元素。

```html
<div class="container">
  <div class="center"><span>Centered content</span></div>
</div>
```

```css
.container {
  border: 1px solid #333;
  height: 250px;
  width: 250px;
}
.center {
  display: table;
  height: 100%;
  width: 100%;
}
.center > span {
  display: table-cell;
  text-align: center;
  vertical-align: middle;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a4k8g58sj30mk07mdfs.jpg)

**Explanation**

display：'oncenter'上的表允许元素的行为类似于<table> HTML元素。

 '.center'上的100％高度和宽度允许元素填充其父元素中的可用空间。

 display：'。centter> span'上的table-cell允许元素表现得像HTML元素。

 text-align：center on'.center> span'水平居中子元素。 

vertical-align：'。centter> span'中间'垂直居中子元素。 

外部父项（在这种情况下为“.container”）必须具有固定的高度和宽度。

**Browser support 100%**



##### 05|Evenly distributed children (分散均匀的子元素)

均匀地在父元素中分配子元素。

```html
<div class="evenly-distributed-children">
  <p>Item1</p>
  <p>Item2</p>
  <p>Item3</p>
</div>
```

```css
.evenly-distributed-children {
  display: flex;
  justify-content: space-between;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a4pizgi0j30mh02ga9x.jpg)

**Explanation**

display：flex启用flexbox。 

justify-content：space-between在水平方向均匀分布子元素。第一个项目位于左边缘，而最后一个项目位于右边缘。 

或者，使用justify-content：space-around来分配子节点周围的空间，而不是它们之间。

**Browser support 99.5%**

**需要前缀才能获得全面支持**



##### 06|Fit image in container(适合容器中的图像)

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

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a4t5796kj30mo06dt8w.jpg)

**Explanation**

object-fit：包含适合容器内的整个图像，同时保留其纵横比。 

object-fit:cover：盖子用图像填充容器，同时保持其纵横比。

object-position：[x] [y]将图像定位在容器内。

**Browser support 95.5%** 



##### 07|FlexBox centering (弹性盒子居中)

使用flexbox水平和垂直居中父元素中的子元素。

```html
<div class="flexbox-centering"><div class="child">Centered content.</div></div>
```

```css
.flexbox-centering {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a4w37z0vj30mh03fq2s.jpg)

**Explanation**

display：flex启用flexbox。

 justify-content：center将子元素水平居中。 

align-items：center将子元素垂直居中。

**Browser support 99.5  需要追加前缀才能全面支持**



##### 08|Ghost trick(鬼技巧)

将元素垂直居中于另一个元素。

```html
<div class="ghost-trick">
  <div class="ghosting"><p>Vertically centered without changing the position property.</p></div>
</div>
```

```css
.ghosting {
  height: 300px;
  background: #0ff;
}
.ghosting:before {
  content: '';
  display: inline-block;
  height: 100%;
  vertical-align: middle;
}
p {
  display: inline-block;
  vertical-align: middle;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a4zv0o8mj30mb090dg3.jpg)

**Explanation**

使用a：before伪元素的样式垂直对齐内联元素而不更改其position属性。

**Browser support 99.9%**



##### 09|Grid centering(网格居中)

使用网格水平和垂直居中父元素中的子元素。

```html
<div class="grid-centering"><div class="child">Centered content.</div></div>
```

```css
.grid-centering {
  display: grid;
  justify-content: center;
  align-items: center;
  height: 100px;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a5257shuj30mv03p0sm.jpg)

**Explanation**

display:grid：启用网格。

 justify-content：center将孩子水平居中。

 align-items：center将孩子垂直居中。

**Browser support 92.3%**



##### 10|Last item with remaining available height(剩余可用高度的最后一项)

通过为最后一个元素提供当前视口中剩余的可用空间，即使在调整窗口大小时，也可以利用可用的视口空间。

```html
<div class="container">
  <div>Div 1</div>
  <div>Div 2</div>
  <div>Div 3</div>
</div>
```

```css
html,body {
  height: 100%;
  margin: 0;
}
.container {
  height: 100%;
  display: flex;
  flex-direction: column;
}
.container > div:last-child {
  background-color: tomato;
  flex: 1;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a59jtikbj30mi02w0sp.jpg)

**Explanation**

height：100％将容器的高度设置为视口高度。 

display：flex启用flexbox。 

flex-direction：列设置flex项目从上到下的顺序。 

flex-grow：1 flexbox将容器的剩余可用空间应用于last子元素。 

父级必须具有视口高度。 flex-grow：1可以应用于第一个或第二个元素，它将具有所有可用空间。

**Browser support 99.5%**



##### 11|Offscreen(屏外)

一种防弹方式，可以在DOM中以可视方式和位置方式完全隐藏元素，同时仍允许通过JavaScript访问元素并可由屏幕阅读器读取。当视障用户需要更多上下文时，此方法对于可访问性（ADA）开发非常有用。作为display的替代方法：none，屏幕阅读器无法读取或者可见性：隐藏，占用DOM中的物理空间。

```html
<a class="button" href="http://pantswebsite.com">
  Learn More <span class="offscreen"> about pants</span>
</a>
```

```css
.offscreen {
  border: 0;
  clip: rect(0 0 0 0);
  height: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
  width: 1px;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a5e1rv84j30mn01gjr7.jpg)

**Explanation**

删除所有边框。 

使用剪辑指示不应显示元素的任何部分。

使元素的高度和宽度为1px。

使用margin：-1px取消元素的高度和宽度。 

隐藏元素的溢出。

删除所有填充。 

绝对定位元素，使其不占用DOM中的空间。

**Browser support 100%** 

**（虽然技术上剪辑已被折旧，但较新的剪辑路径目前对浏览器的支持非常有限。）**



##### 12|Transform centering(变换居中)

使用position：absolute和transform：translate（）（作为flexbox或display：table的替代），在其父元素中垂直和水平居中子元素。与flexbox类似，此方法不需要您知道父级或子级的高度或宽度，因此它非常适合响应式应用程序。

```html
<div class="parent"><div class="child">Centered content</div></div>
```

```css
.parent {
  border: 1px solid #333;
  height: 250px;
  position: relative;
  width: 250px;
}
.child {
  left: 50%;
  position: absolute;
  top: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a5j7wrflj30mh07rweh.jpg)

position：子元素上的absolute允许它根据其包含块进行定位。

 left：50％和top：50％将孩子从其包含块的左边和上边缘偏移50％。 

transform：translate（-50％， - 50％）允许否定子元素的高度和宽度，使其垂直和水平居中。

 注意：父元素的固定高度和宽度仅适用于演示。

**Browser support 97.7%**

**必须加前缀才能够全面支持**



##### 13|Truncate text multiline(截断文本多行)

如果文本长于一行，则将截断n行，并以渐变渐变结束。

```html
<p class="truncate-text-multiline">
  Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut
  labore et.
</p>
```

```css
.truncate-text-multiline {
  overflow: hidden;
  display: block;
  height: 109.2px;
  margin: 0 auto;
  font-size: 26px;
  line-height: 1.4;
  width: 400px;
  position: relative;
}
.truncate-text-multiline:after {
  content: '';
  position: absolute;
  bottom: 0;
  right: 0;
  width: 150px;
  height: 36.4px;
  background: linear-gradient(to right, rgba(0, 0, 0, 0), #f5f6f9 50%);
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a5ltxzxaj30ms03xq36.jpg)

**Explanation**

溢出：隐藏可防止文本溢出其尺寸（对于块，100％宽度和自动高度）。

 width：400px确保元素具有尺寸。

 **height：109.2px等于font-size * line-height * numberOfLines（在这种情况下为26 * 1.4 * 3 = 109.2）**

**height：36.4px计算值，它等于font-size * line-height（在这种情况下为26 * 1.4 = 36.4）** 

background：linear-gradient（right，rgba（0,0,0,0），＃f5f6f9 50％）渐变从transparent 到＃f5f6f9

**Browser support 97.5%**



##### 14|Truncate text(截断文字)

如果文本长于一行，它将被截断并以省略号结尾

```html
<p class="truncate-text">If I exceed one line's width, I will be truncated.</p>
```

```css
.truncate-text {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  width: 200px;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a5rydehej30md028t8j.jpg)

**Explanation**

overflow:hidden 可防止文本溢出其尺寸（对于块，100％宽度和自动高度）。

 white-space：nowrap可防止文本高度超过一行。

 text-overflow：省略号使得如果文本超出其维度，它将以省略号结束。

width：200px;确保元素具有维度，以了解何时获得省略号

**Browser support 99.8 仅适用于单行元素**