
## 以下6个属性设置在容器上
### flex-direction
flex-direction属性决定主轴的方向，即项目的排列方向
```css
.box{
    flex-direction: row|row-reverse|column|column-reverse;
}
```
值说明：
- row（default）：主轴为水平方向，起点在左侧。
- row-reverse：主轴在水平方向，起点在右侧。
- column：主轴在垂直方向，起点在顶部。
- column-reverse：主轴在垂直方向，起点在底部。
### flex-wrap
默认情况下，项目都排在一条线（又称“轴线”）上，flex-wrap属性定义，如果一条轴线排不下，如何换行。
```css
.box{
    flex-wrap: nowrap|wrap|wrap-reverse;
}
```
值说明：
- nowrap（default）：不换行。
- wrap：往下方换行。
- wrap-reverse：往上方换行。
### flex-flow
flex-flow 属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap
```css
.box{
    flex-flow: <flex-direction> || <flex-wrap>;
}
```
值说明：
此属性为简写，可以形式为：row nowrap或者flex-flow: row-reverse wrap-reverse
### justify-content
justify-content属性定义了项目在主轴上的对齐方式
```css
.box{
    justify-content: flex-start|flex-end|center|space-between|space-around;
}
```
具体对齐方式与轴的方向有关。
值说明：
- flex-start（default）：左对齐。
- flex-end：右对齐。
- center：居中。
- space-between：两端对齐，子项目之间的间隔都相等。
- space-around：每个项目之间的间隔相等，所以项目之间的间隔是项目与边框的间隔的两倍。
### align-items
align-items属性定义项目在交叉轴（也就是垂直方向的轴）上如何对齐。
```css
.box{
    align-items: flex-start|flex-end|center|baseline|stretch;
}
```
具体对齐方式与轴的方向有关。
值说明：
- flex-start：交叉轴的起点对齐。
- flex-end：交叉轴的终点对齐。
- center：交叉轴的中点对齐（可以设置垂直居中）
- baseline：项目的第一行文字的基线对齐。
- stretch（default）：如果项目未设置高度或者设为auto，将占满整个容器的高度。
### align-content
align-content属性定义了多根轴线的对齐方式，如果项目只有一根轴线，该属性不起作用。
多根轴线的理解：父容器中包含多个子容器，且子容器中包含多个items
```css
.box{
    align-content: flex-start|flex-end|center|space-between|space-around|stretch;
}
```
值说明：
- flex-start：与交叉轴的起点对齐。
- flex-end：与交叉轴的终点对齐。
- center：与交叉轴的中点对齐。
- space-between：与交叉轴的两端对齐，轴线之间间隔平均分布。
- space-around：每根轴线两侧的距离都相等，所以轴线之间的间隔比轴线与边框的间隔大一倍。
- stretch：轴线占满整个交叉轴。
## 以下6个属性设置在项目上
### order
order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。
```css
.item{
    order: <integer>;
}
```
值说明：整数。
### flex-grow
flex-grow（grow:长大，变大）属性定义项目的放大比列，默认值为0，即如果存在剩余空间，也不放大，默认为0。
```css
.item{
    flex-grow: <number>;
}
```
值说明：数字。
如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性值为2，其他项目为1，则前者的剩余空间将比其他项目多一倍。
### flex-shrink
flex-shrink属性定义了项目的缩小比列，默认为1，即如果空间不足，该项目将缩小
```css
.item{
    flex-shrink: <number>;
}
```
如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。
值说明：负值对该属性无效。
### flex-basis
flex-basis属性定义了在分配多余空间之前，项目占据主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
```css
.item{
    flex-basis: <length> | auto;
}
```
值说明：它可以设为跟width或height属性一样的值（如：100px），项目将占据固定空间。
### flex
flex属性是flex-grow、flex-shrink和flex-basis的简写，默认值为0 1 auto。后两个属性可选。
```css
.item{
    flex:none | [<'flex-grow'> <'flex-shrink'>? || <'flex-basis'>]
}
```
值说明：该属性有两个快捷值：auto （1 1 auto）和none （0 0 auto）。建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。
### align-self
align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。
```css
.item{
    align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```
值说明：该属性可能取6个值，除了auto，其他都与align-items属性完全一致。