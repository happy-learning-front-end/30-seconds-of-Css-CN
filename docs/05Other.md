#### 05|Other(其他)

##### 01|Calc() 计算

函数calc（）允许使用数学表达式定义CSS值，属性采用的值是数学表达式的结果。

```html
<div class="box-example"></div>
```

```css
.box-example {
  height: 280px;
  background: #222 url('https://image.ibb.co/fUL9nS/wolf.png') no-repeat;
  background-position: calc(100% - 20px) calc(100% - 20px);
}
```

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3aawdcppvj30k208lq2z.jpg)

如果您想从右侧和底部对齐背景图像，则只能使用直线长度值。所以现在可以使用calc（）：

![](https://ws1.sinaimg.cn/large/0060ejA5ly1g3aawkudjaj30k408fjrj.jpg)

**Explanation**

它允许加法，减法，乘法和除法。 

可以为表达式中的每个值使用不同的单位（例如，像素和百分比）。 

允许嵌套calc（）函数。 

它可用于任何允许<length>，<frequency>，<angle>，<time>，<number>，<color>或<integer>的属性，如width，height，font-size，top，离开等

**Browser support 97.0%**