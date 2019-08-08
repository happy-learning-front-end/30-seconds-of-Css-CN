#### 04|InterActivity(交互)

##### 01|Disable selection(禁用选择)

使内容无法选择。

```html
<p>You can select me.</p>
<p class="unselectable">You can't select me!</p>
```

```css
.unselectable {
  user-select: none;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a6e8l2kkg30ew03ut9x.gif)

**Explanation**

user-select：none指定无法选择文本。

**Browser support 93.2%**

**需要前缀才能获得完全支持。 ⚠️这不是防止用户复制内容的安全方法。**



##### 02|Focus Within(专注于)

如果表单中的任何子项被聚焦，则更改表单的外观。

```html
<div class="focus-within">
  <form>
    <label for="given_name">Given Name:</label> <input id="given_name" type="text" /> <br />
    <label for="family_name">Family Name:</label> <input id="family_name" type="text" />
  </form>
</div>
```

```css
form {
  border: 3px solid #2d98da;
  color: #000000;
  padding: 4px;
}
form:focus-within {
  background: #f7b731;
  color: #000000;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a6h0pyg5g30l102n0tp.gif)

**Explanation**

psuedo类：focus-within将样式应用于父元素（如果任何子元素被聚焦）。例如，表单元素内的输入元素。

**Browser support 82.9% IE11或当前版本的Edge不支持。**



##### 03|Mouse cursor gradient tracking(鼠标光标渐变跟踪)

一种悬停效果，其中渐变跟随鼠标光标。

```html
<button class="mouse-cursor-gradient-tracking"><span>Hover me</span></button>
```

```css
.mouse-cursor-gradient-tracking {
  position: relative;
  background: #7983ff;
  padding: 0.5rem 1rem;
  font-size: 1.2rem;
  border: none;
  color: white;
  cursor: pointer;
  outline: none;
  overflow: hidden;
}
.mouse-cursor-gradient-tracking span {
  position: relative;
}
.mouse-cursor-gradient-tracking::before {
  --size: 0;
  content: '';
  position: absolute;
  left: var(--x);
  top: var(--y);
  width: var(--size);
  height: var(--size);
  background: radial-gradient(circle closest-side, pink, transparent);
  transform: translate(-50%, -50%);
  transition: width 0.2s ease, height 0.2s ease;
}
.mouse-cursor-gradient-tracking:hover::before {
  --size: 200px;
}
```

```js
var btn = document.querySelector('.mouse-cursor-gradient-tracking')
btn.onmousemove = function(e) {
  var x = e.pageX - btn.offsetLeft - btn.offsetParent.offsetLeft
  var y = e.pageY - btn.offsetTop - btn.offsetParent.offsetTop
  btn.style.setProperty('--x', x + 'px')
  btn.style.setProperty('--y', y + 'px')
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a6kqkn6hg30kf01vmz5.gif)

**Browser support 91.6% 必须需要使用到JavaScript**



##### 04|Popout Menu(弹出菜单)

在悬停和焦点上显示交互式弹出菜单。

```html
<div class="reference" tabindex="0"><div class="popout-menu">Popout menu</div></div>
```

```css
.reference {
  position: relative;
  background: tomato;
  width: 100px;
  height: 100px;
}
.popout-menu {
  position: absolute;
  visibility: hidden;
  left: 100%;
  background: #333;
  color: white;
  padding: 15px;
}
.reference:hover > .popout-menu,
.reference:focus > .popout-menu,
.reference:focus-within > .popout-menu {
  visibility: visible;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a6o5jsiqg30kf03k0te.gif)

**Explanation**

position：引用父级的相对为其子级建立笛卡尔定位上下文。 

position：absolute将弹出菜单从文档流中取出，并将其相对于父文件定位。

left：100％将弹出菜单从左侧移动100％的父级宽度。 

visibility：hidden最初隐藏弹出菜单并允许转换（与display：none不同）。 

.reference：hover> .popout-menu表示当.reference悬停在上面时，选择具有.popout-menu类的直接子项并将其可见性更改为visible，这将显示弹出窗口。 

.reference：focus> .popout-menu意味着当.reference被聚焦时，会显示弹出窗口。 

.reference：focus-within> .popout-menu确保当焦点在引用范围内时显示弹出窗口。

**Browser support 100%**



##### 05|Sibling fade(兄弟姐妹褪色)

淡化悬停物品的兄弟姐妹。

```html
<div class="sibling-fade">
  <span>Item 1</span> <span>Item 2</span> <span>Item 3</span> <span>Item 4</span>
  <span>Item 5</span> <span>Item 6</span>
</div>
```

```css
span {
  padding: 0 1rem;
  transition: opacity 0.2s;
}
.sibling-fade:hover span:not(:hover) {
  opacity: 0.5;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a6oiy6img30kf01sgn1.gif)

**Explanation**

过渡：不透明度0.2s指定对不透明度的更改将在0.2秒内过渡。

.sibling-fade：悬停span：not（：hover）指定当父项悬停时，选择当前未悬停的任何span子项并将其不透明度更改为0.5

**Browser support 97.5%**

##### 06|Toogle switch(拨动开关)

仅使用CSS创建切换开关。

```html
<input type="checkbox" id="toggle" class="offscreen" /> <label for="toggle" class="switch"></label>
```

```css
.switch {
  position: relative;
  display: inline-block;
  width: 40px;
  height: 20px;
  background-color: rgba(0, 0, 0, 0.25);
  border-radius: 20px;
  transition: all 0.3s;
}
.switch::after {
  content: '';
  position: absolute;
  width: 18px;
  height: 18px;
  border-radius: 18px;
  background-color: white;
  top: 1px;
  left: 1px;
  transition: all 0.3s;
}
input[type='checkbox']:checked + .switch::after {
  transform: translateX(20px);
}
input[type='checkbox']:checked + .switch {
  background-color: #7983ff;
}
.offscreen {
  position: absolute;
  left: -9999px;
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3a6rehp97g30kf01l3zk.gif)

**Explanation**

此效果仅将<label>元素设置为样式，以使其看起来像切换开关，并通过将其定位在屏幕外来隐藏实际的<input>复选框。单击与<input>元素关联的标签时，它会将<input>复选框设置为：checked状态。 

for属性通过其id将<label>与相应的<input>复选框元素相关联。 

.switch :: after为<label>定义一个伪元素以创建圆形旋钮。

 input[type='checkbox']:checked + .switch::after在选中复选框后定位<label>的伪元素样式。

 transform：translateX（20px）在选中复选框时将伪元素（旋钮）20px移动到右侧。 

background-color：＃7983ff;选中复选框时，将开关的背景颜色设置为不同的颜色。

 .offscreen将<input>复选框元素（不包含实际切换开关的任何部分）移出文档流，并将其远离视图定位，但不隐藏它，以便可通过键盘和屏幕访问读者。

 transition: all 0.3s指定所有属性更改将在0.3秒内转换，因此在选中复选框时转换<label>的background-color和pseudo-element的transform属性。

**Browser support 97.7% 必须加前缀才能全面支持!**