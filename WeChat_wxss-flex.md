# Flex弹性盒子布局学习笔记

### flex12个“迷人的”布局属性
#### 容器属性
* flex-flow
* flex-direcion
* flex-wrap
* justify-content
* align-items
* align-content
#### 元素属性
* order
* flex-grow
* flex-shrink
* flex-basis
* flex
* align-self

### 一、Flex弹性盒子模型

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/Flex%E5%BC%B9%E6%80%A7%E7%9B%92%E5%AD%90%E6%A8%A1%E5%9E%8B.jpeg" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>


对于某个元素只要声明了` display:flex; `，那么这个元素就成为了弹性容器，具有了flex弹性布局的特性。

&ensp;&ensp;&ensp; 1.每个弹性容器都有两根轴：**主轴和交叉轴**，两轴之间成90°的关系。注意：**水平的不一定是主轴**。

&ensp;&ensp;&ensp; 2.每根轴都有**起点和终点**，这对于元素对齐是非常重要的。

&ensp;&ensp;&ensp; 3.弹性容器中的所有子元素成为`弹性元素`，**弹性元素永远沿主轴排列**。

&ensp;&ensp;&ensp; 4.弹性元素也可以通过`display:flex`设置为另一个弹性容器，形成嵌套关系。因此**一个元素既可以是弹性容器也可以是弹性元素**。

所以说弹性容器的两根轴都非常的重要，**所有属性都是作用于轴的**。下面从轴入手，将所有的flex布局属性串起来。

### 二、主轴

&ensp;&ensp;&ensp; Flex布局是一种**一维布局模型**，一次只能处理一个维度（一行或者一列）上的元素布局，作为对比的是二维布局[CSS Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout),可以同时处理行、列两个方向的布局。

#### 1.主轴的方向

&ensp;&ensp;&ensp; 我们可以在弹性容器上通过`flex-direction`修改主轴的方向。如果主轴方向修改了，那么：

&ensp;&ensp;&ensp; 1.价差周就会相应地旋转90°。

&ensp;&ensp;&ensp; 2.弹性元素的排列方式也会发生改变，因为**弹性元素永远沿主轴排列**。

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/flex-direction-row.gif" alt="Sample"  width="500" height="320">
	<p align="center">
	<em>flex-direction:row</em>
	</p>
</p>

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/flex-direction-column.gif" alt="Sample"  width="500" height="320">
	<p align="center">
	<em>flex-direction:column</em>	
	</p>
</p>

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/flex-direction-row-reverse.gif" alt="Sample"  width="500" height="320">
	<p align="center">
	<em>flex-direction:row-reverse</em>		
	</p>
</p>

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/flex-direction-column-reverse.gif" alt="Sample"  width="500" height="320">
	<p align="center">
	<em>flex-direction:column-reverse</em>	
	</p>
</p>

#### 2.沿主轴的排列处理
&ensp;&ensp;&ensp; 弹性元素永远沿主轴排列，那么如果主轴排不下，该如何处理？

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E4%B8%BB%E8%BD%B4%E6%8E%92%E5%88%97%E5%A4%84%E7%90%86.jpeg" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

&ensp;&ensp;&ensp; 通过设置`flex-wrap: nowrap | wrap | wrap-reverse`可使得主轴上的元素不折行、折列、反向折行。

&ensp;&ensp;&ensp; 默认是`nowrap`不折行，难道任由元素直接溢出容器吗？当然不会，那么这里就设计到了元素的弹性伸缩应对。

&ensp;&ensp;&ensp; `wrap`折行，顾名思义就是另起一行，那么折行之后行与行之间的间距（对齐）怎么调整？这里又设计到了交叉轴上的多行对齐。

&ensp;&ensp;&ensp; `wrap-reverse`反向折行，是从容器底部开始的折行，单每个元素之间的排列仍保留正向。

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E4%B8%BB%E8%BD%B4%E6%8E%92%E5%88%97%E5%A4%84%E7%90%861.jpeg" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

#### 3.一个复合属性
&ensp;&ensp;&ensp; `flex-flow = flex - direction + flex-wrap`

&ensp;&ensp;&ensp; `flex-flow`相当于规定了flex布局的“工作流（flow）”

&ensp;&ensp;&ensp; `flex-flow : row nowrap;`

### 三、元素如何弹性伸缩应对
&ensp;&ensp;&ensp; `flex-wrap:nowrap;`不折行时，容器宽度有剩余/不够分，弹性元素们该怎么“弹性”地伸缩应对？这里针对上面的两种场景，引入两个属性（徐应用在弹性元素上）

&ensp;&ensp;&ensp; 1.`flex-shrink`：缩小比例（容器宽度<元素总宽度时如何收缩）

&ensp;&ensp;&ensp; 2.`flex-grow`：放大比例（容器宽度>元素总宽度时如何伸展）

#### 1.flex-shrink:缩小比例
&ensp;&ensp;&ensp; 来看以下场景，弹性容器`#container`的宽度是200px，一共有三个弹性元素，宽度分别是50px,100px,120px。在不折行的情况下，此时容器宽度是明显不够分配的。

&ensp;&ensp;&ensp; 实际上，`flex-shrink`默认为1，也就是当不够分配时，元素豆浆等比例缩小，沾满整个宽度，如下图。


<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/Flex%E7%BC%A9%E5%B0%8F%E6%AF%94%E4%BE%8B.jpeg" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

```
#container{
&ensp;&ensp; display:flex;
&ensp;&ensp; flex-wrap:nowrap;
}
```

##### 元素收缩计算法

&ensp;&ensp;&ensp; 真的是等比缩小（每个元素各减去70/3的宽度）吗？这里稍微深究一下他的收缩计算方法。

&ensp;&ensp;&ensp; 1.弹性元素1:50px→37.03px

&ensp;&ensp;&ensp; 2.弹性元素2:100px→74.08px

&ensp;&ensp;&ensp; 2.弹性元素2:200px→88.89px

先抛结论：`flex-shrink:1`并非严格等比例缩小，**它还会考虑弹性元素本身的大小**

 * 容器剩余宽度：-70px
 * 缩小因子的分母：`1*50+1*100+1*120=270`(1为个元素flex-shrink的值)
 * 元素1的缩小因子：`1*50/270`
 * 元素1的缩小宽度为缩小因子乘以容器的剩余宽度：`1*50/270*(-70)`
 * 元素1最后则缩小为：`50px+(1*50/270*(-70))=37.03px`

&ensp;&ensp;&ensp; 加入弹性元素本身大小作为计算方法的考虑因素，主要是为了避免将一些本身宽度较小的元素在收缩之后宽度变为0的情况出现。

#### 2.flex-grow:放大比例
&ensp;&ensp;&ensp; 同样，弹性容器`#container`宽度是200px，但此时只有两个弹性元素，宽度分别是50px、100px。此时容器宽度是有剩余的。

&ensp;&ensp;&ensp; 那么剩余的宽度该怎样分配？而`flex-grow`则决定了要不要分配以及各个分配多少。

&ensp;&ensp;&ensp; （1）在flex布局中，容器剩余宽度默认是不进行分配的，也就是所有弹性元素的`flex-grow`都为0。

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/Flex-%E6%94%BE%E5%A4%A7%E6%AF%94%E4%BE%8B.jpeg" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

&ensp;&ensp;&ensp; （2）通过指定`flex-grow`为大于零的值，实现容器剩余宽度的分配比例设置。

##### 元素放大的计算方法
&ensp;&ensp;&ensp; 放大的计算方法并没有与缩小一样，将元素大小纳入考虑。

&ensp;&ensp;&ensp; 仅仅按`flex-grow`声明的份数算出每个需分配多少，叠加到原来的尺寸上。

* 容器剩余宽度：`50px`
* 分成每份：`50px / (3+2) = 10px`
* 元素1放大为：`50px + 3 * 10 = 80px`

##### 无多余宽度时，flex-grow无效

&ensp;&ensp;&ensp; 下图中，弹性容器的宽度正好等于元素宽度总和，无多余宽度，此时无论`flex-grow`是什么值都不会生效。

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/Flex-%E6%94%BE%E5%A4%A7%E6%AF%94%E4%BE%8B.jpeg" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

### 四、弹性处理与刚性尺寸
&ensp;&ensp;&ensp; 在进行弹性处理之余，其实有些场景我们更希望元素尺寸固定，不需要进行弹性调整。设置元素尺寸除了width和height以外，flex还提供了一个`flex-basis`属性。

`flex-basis`设置的是元素在主轴上的初始尺寸，所谓的初始尺寸就是元素在`flex-grow`和`flex-shrink`生效前的尺寸。

#### 1.与width/height的区别
&ensp;&ensp;&ensp; 首先以width为例进行比较。看下下面的例子。`#container {display:flex;}`。

```
<div id="container">
  <div>11111</div>
  <div>22222</div>
</div>
```
#### (1)两者都为0

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/width-height_0.jpeg" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

* width: 0 —— 完全没显示

* flex-basis: 0 —— 根据内容撑开宽度

#### (2)两者非0
<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/width-height-!0.jpeg" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

* width: 非0;

* flex-basis: 非0

—— 数值相同时两者等效

—— 同时设置，flex-basis优先级高

#### (3)flex-basis为auto
<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/Flex-basis-auto.jpeg" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

&ensp;&ensp;&ensp; flex-basis为auto时，如设置了width则元素尺寸由width决定；没有设置则由内容决定

#### (4)flex-basis == 主轴上的尺寸 != width
<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/flex-basis!%3Dwidth.jpeg" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

* 将主轴方向改为：上→下
* 此时主轴上的尺寸是元素的height
* flex-basis == height

#### 2.常用的复合属性flex
&ensp;&ensp;&ensp; 这个属性应该是最容易迷糊的一个，下面揭开它的真面目。

&ensp;&ensp;&ensp; flex = flex-grow + flex-shrink + flex-basis

&ensp;&ensp;&ensp; 复合属性，前面说的三个属性的简写。

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/flex%E5%A4%8D%E5%90%88%E5%B1%9E%E6%80%A7.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

##### 一些简写
* flex: 1 = flex: 1 1 0%
* flex: 2 = flex: 2 1 0%
* flex: auto = flex: 1 1 auto;
* flex: none = flex: 0 0 auto; // 常用于固定尺寸 不伸缩

##### flex:1 和 flex:auto 的区别

其实可以归结于`flex-basis:0`和`flex-basis:auto`的区别。

`flex-basis`是指定初始尺寸，当设置为0时（绝对弹性元素），此时相当于告诉`flex-grow`和`flex-shrink`在伸缩的时候不需要考虑我的尺寸；相反当设置为`auto`时（相对弹性元素），此时则需要在伸缩时将元素尺寸纳入考虑。

因此从下图（转自W3C）可以看到绝对弹性元素如果`flex-grow`值是一样的话，那么他们的尺寸一定是一样的。

### 五、容器内如何对齐
&ensp;&ensp;&ensp; 前面讲完了元素大小关系之后，下面是另外一个重要议题——**如何对齐**。可以发现上面的所有属性都是围绕主轴进行设置的，但在对齐方面则不得不加入作用于交叉轴上。需要注意的是这些对齐属性都是作用于容器上。

#### 1.主轴上的对齐方式
##### justify-content

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E4%B8%BB%E8%BD%B4%E5%AF%B9%E9%BD%90%E6%96%B9%E5%BC%8F.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

#### 2.交叉轴上的对齐方式

&ensp;&ensp;&ensp; 主轴上比较好理解，重点是交叉轴上。因为交叉轴上存在单行和多行两种情况。

##### 交叉轴上的单行对齐
###### align-items
&ensp;&ensp;&ensp; 默认值是`stretch`，当元素没有设置具体尺寸时会将容器在交叉轴方向撑满。

&ensp;&ensp;&ensp; 当`align-items`不为`stretch`时，此时除了对齐方式会改变之外，元素在交叉轴方向上的尺寸将由内容或自身尺寸（宽高）决定。

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E4%BA%A4%E5%8F%89%E8%BD%B4%E5%AF%B9%E9%BD%900.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E4%BA%A4%E5%8F%89%E8%BD%B4%E5%AF%B9%E9%BD%901.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E4%BA%A4%E5%8F%89%E8%BD%B4%E5%AF%B9%E9%BD%902.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E4%BA%A4%E5%8F%89%E8%BD%B4%E5%AF%B9%E9%BD%903.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E4%BA%A4%E5%8F%89%E8%BD%B4%E5%AF%B9%E9%BD%904.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

&ensp;&ensp;&ensp; 注意：交叉轴不一定是从上往下，这点再次强调也不为过。

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E4%BA%A4%E5%8F%89%E8%BD%B4%E5%AF%B9%E9%BD%905.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

#### 交叉轴上的多行对齐
&ensp;&ensp;&ensp; 还记得可以通过`flex-wrap: wrap`使得元素在一行放不下时进行换行。在这种场景下就会在交叉轴上出现多行，多行情况下，flex布局提供了`align-content`属性设置对齐。

&ensp;&ensp;&ensp; `align-content`与`align-items`比较类似，同时也比较容易迷糊。下面会将两者对比着来看它们的异同。

&ensp;&ensp;&ensp; 首先明确一点：`align-content`只对多行元素有效，**会以多行作为整体进行对齐**，容器必须开启换行。

```
align-content: stretch | flex-start | flex-end | center | space-between | space-around

align-items: stretch | flex-start | flex-end | center | baseline
```
&ensp;&ensp;&ensp; 在属性值上，`align-content`比`align-items`多了两个值：`space-between`和`space-around`。

##### align-content与align-items异同对比
&ensp;&ensp;&ensp; 与`align-items`一样，`align-content`:默认值也是`stretch`。两者同时都为`stretch`时，毫无悬念所有元素都是撑满交叉轴。

```
#container {
  align-items: stretch;
  align-content: stretch;
}
```
<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E4%BA%A4%E5%8F%89%E8%BD%B4%E5%A4%9A%E8%A1%8C%E5%AF%B9%E9%BD%90.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

&ensp;&ensp;&ensp; 当我们将align-items改为`flex-start`或者给弹性元素设置一个具体高度，此时效果是行与行之间形成了间距。

```
#container {
  align-items: flex-start;
  align-content: stretch;
}

/*或者*/
#container {
  align-content: stretch;
}
#container > div {
  height: 30px;
}
```
&ensp;&ensp;&ensp; 为什么？因为`align-content`会以整行为单位，此时会将整行进行拉伸占满交叉轴；而`align-items`设置了高度或者顶对齐，在不能用高度进行拉伸的情况下，选择了用间距。

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E4%BA%A4%E5%8F%89%E8%BD%B4align-items.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

&ensp;&ensp;&ensp; 尝试把`align-content`设置为顶对齐，此时以行为单位，整体高度通过内容撑开。

&ensp;&ensp;&ensp; 而`align-items`仅仅管一行，因此在只有第一个元素设置了高度的情况下，第一行的其他元素遵循`align-items: stretch`也被拉伸到了50px。而第二行则保持高度不变。

```
#container {
  align-items: stretch;
  align-content: flex-start;
}
#container > div:first-child {
    height: 50px;
}
```
<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E4%BA%A4%E5%8F%89%E8%BD%B4%E4%B8%A4%E8%80%85%E4%B8%8D%E6%98%8E%E6%98%BE.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

&ensp;&ensp;&ensp; 两者的区别还是不明显？来看下面这个例子。

&ensp;&ensp;&ensp; 这里仅对第二个元素的高度进行设置，其他元素高度则仍保持内容撑开。

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E5%85%83%E7%B4%A0%E9%AB%98%E5%BA%A6%E8%AE%BE%E7%BD%AE.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

&ensp;&ensp;&ensp; 以第一个图为例，会发现`align-content`会将所有行进行顶对齐，然后第一行由于第二个元素设置了较高的高度，因此体现出了底对齐。

##### 两者差异总结：

* 两者“作用域”不同

* align-content管全局(所有行视为整体)

* align-items管单行

##### 能否更灵活地设置交叉轴对齐

&ensp;&ensp;&ensp; 除了在容器上设置交叉轴对齐，还可以通过align-self单独对某个元素设置交叉轴对齐方式。

* 值与align-items相同

* 可覆盖容器的align-items属性

* 默认值为auto，表示继承父元素的align-items属性

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E5%85%83%E7%B4%A0%E9%AB%98%E5%BA%A6%E8%AE%BE%E7%BD%AE.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

```
#container {
  display: flex;
  align-items: flex-start;
}

#container > div:first-child {
  align-self: stretch;
}

#container > div:nth-child(3) {
  align-self: center;
}

#container > div:nth-child(4) {
  align-self: flex-end;
}
```

### 六、其他
#### order：更优雅地调整元素顺序
<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E5%85%B6%E4%BB%96.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

```
#container > div:first-child {
  order: 2;
}
#container > div:nth-child(2) {
  order: 4;
}
#container > div:nth-child(3) {
  order: 1;
}
#container > div:nth-child(4) {
  order: 3;
}
```
&ensp;&ensp;&ensp; order：可设置元素之间的排列顺序

* 数值越小，越靠前，默认为0
* 值相同时，以dom中元素排列为准

### 七、总结

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E6%80%BB%E7%BB%930.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E6%80%BB%E7%BB%931.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

<p align="center">
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/%E6%80%BB%E7%BB%932.jpeg
" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>

### 附
#### Thank：感谢网络中的各路大神，原博客地址：[Click me to see origin Blog](https://www.cnblogs.com/qcloud1001/p/9848619.html)







