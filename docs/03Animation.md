#### 03|Animation(动画)

##### 01|Bouncing loader(弹簧加载动画)

创建一个弹簧动画

```html
<div class="bouncing-loader">
  <div></div>
  <div></div>
  <div></div>
</div>
```

```css
@keyframes bouncing-loader {
  to {
    opacity: 0.1;
    transform: translate3d(0, -1rem, 0);
  }
}
.bouncing-loader {
  display: flex;
  justify-content: center;
}
.bouncing-loader > div {
  width: 1rem;
  height: 1rem;
  margin: 3rem 0.2rem;
  background: #8385aa;
  border-radius: 50%;
  animation: bouncing-loader 0.6s infinite alternate;
}
.bouncing-loader > div:nth-child(2) {
  animation-delay: 0.2s;
}
.bouncing-loader > div:nth-child(3) {
  animation-delay: 0.4s;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3aa8lhn2ag30kf0413zg.gif)

**Explanation**

注意：1rem通常是16px。 

@keyframes定义了一个具有两种状态的动画，其中元素改变不透明度，并使用transform：translate3d（）在2D平面上转换。在transform上使用单轴转换：translate3d（）可提高动画的性能。 

.bouncing-loader是弹跳圆的父容器，使用display：flex和justify-content：center将它们放在中心。 

.bouncing-loader> div，定位要设置样式的父级的三个子div。 div的宽度和高度为1rem，使用border-radius：50％将它们从正方形转换为圆形。 

margin：3rem 0.2rem指定每个圆圈的顶部/底部边缘为3rem，左/右边距为0.2rem，这样它们就不会直接相互接触，从而为它们提供一些喘息空间。

animation是各种动画属性的简写属性：animation-name,animation-duration,animation-iteration-count,animation-direction

nth-child（n）定位其父元素的第n个子元素。 

animation-delay分别用于第二个和第三个div，因此每个元素不会同时启动动画。

**Browser support 97.4%**



##### 02|Button border animation(按钮边框动画)

创建一个按钮边框动画!

```html
<div class="button-border"><button class="button">Submit</button></div>
```

```css
.button {
  background-color: #c47135;
  border: none;
  color: #ffffff;
  outline: none;
  padding: 12px 40px 10px;
  position: relative;
}
.button:before,
.button:after {
  border: 0 solid transparent;
  transition: all 0.25s;
  content: '';
  height: 24px;
  position: absolute;
  width: 24px;
}
.button:before {
  border-top: 2px solid #c47135;
  left: 0px;
  top: -5px;
}
.button:after {
  border-bottom: 2px solid #c47135;
  bottom: -5px;
  right: 0px;
}
.button:hover {
  background-color: #c47135;
}
.button:hover:before,
.button:hover:after {
  height: 100%;
  width: 100%;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3aaf9lk79g30kf025wfb.gif)

**Explanation**

使用：before和：在pseduo-elements之后作为在悬停时设置动画的边框。

**Browser support 100%**



##### 03|Donut spinner(甜甜圈旋转器)

创建一个甜甜圈微调器，可用于指示内容的加载。

```html
<div class="donut"></div>
```

```css
@keyframes donut-spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
.donut {
  display: inline-block;
  border: 4px solid rgba(0, 0, 0, 0.1);
  border-left-color: #7983ff;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  animation: donut-spin 1.2s linear infinite;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3aaia0uf4g30kf021js2.gif)

**Explanation**

对于整个元素使用半透明边框，除了将用作甜甜圈的加载指示符的一侧。使用动画旋转元素。

**Browser support 97.4%**



##### 04|Height transition(高度过渡)

当元素的高度未知时，将元素的高度从0转换为自动。

```html
<div class="trigger">
  Hover me to see a height transition.
  <div class="el">content</div>
</div>
```

```css
.el {
  transition: max-height 0.5s;
  overflow: hidden;
  max-height: 0;
}
.trigger:hover > .el {
  max-height: var(--max-height);
}
```

```js
var el = document.querySelector('.el')
var height = el.scrollHeight
el.style.setProperty('--max-height', height + 'px')
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3aalfss9cg30kf02n763.gif)

**Explanation**

**CSS**

transition：max-height：0.5s cubic-bezier（...）指定使用ease-out-quint计时功能，应该在0.5秒内转换为max-height的更改。 

overflow：hidden可以防止隐藏元素的内容溢出其容器。

max-height：0指定元素最初没有高度。 

.target：hover> .el指定当父项悬停时，在其中定位子.el并使用由JavaScript定义的--max-height变量。

**JavaScript**

el.scrollHeight是元素的高度，包括溢出，它将根据元素的内容动态变化。 

el.style.setProperty（...）设置--max-height CSS变量，该变量用于指定目标悬停的元素的最大高度，允许它从0平滑过渡到auto。

**Browser support 91.6%  导致每个动画帧重排，如果元素下方有大量元素在高度过渡，则会出现滞后现象。**



##### 05|Hover underline animation(悬停下划线动画)

当文本悬停时，创建动画下划线效果。

```html
<p class="hover-underline-animation">Hover this text to see the effect!</p>
```

```css
.hover-underline-animation {
  display: inline-block;
  position: relative;
  color: #0087ca;
}
.hover-underline-animation::after {
  content: '';
  position: absolute;
  width: 100%;
  transform: scaleX(0);
  height: 2px;
  bottom: 0;
  left: 0;
  background-color: #0087ca;
  transform-origin: bottom right;
  transition: transform 0.25s ease-out;
}
.hover-underline-animation:hover::after {
  transform: scaleX(1);
  transform-origin: bottom left;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3aar0lpxsg30kf02nwfh.gif)

**Explanation**

display：inline-block使块p成为内联块，以防止下划线跨越整个父宽度而不仅仅是内容（文本）。 

position：元素上的相对为伪元素建立笛卡尔定位上下文。 

::after定义一个伪元素。 

position：absolute将伪元素从文档流中取出，并将其相对于父文档定位。 

width：100％确保伪元素跨越文本块的整个宽度。 

transform：scaleX（0）最初将伪元素缩放为0，因此它没有宽度且不可见。 

bottom：0和left：0将其定位到块的左下角。 

transition: transform 0.25s ease-out意味着transform的变化将通过缓出计时功能在0.25秒内转换。 

transform-origin：右下角表示变换锚点位于块的右下角。 

：hover :: after然后使用scaleX（1）将宽度转换为100％，然后将transform-origin更改为左下角，以便锚点反转，允许它在悬停时从另一个方向转换出来。

**Browser support 97.5%**