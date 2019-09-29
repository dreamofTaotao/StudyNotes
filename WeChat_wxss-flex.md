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
<img src="https://github.com/dreamofTaotao/StudyNotes/blob/master/Photos/Flex%E5%BC%B9%E6%80%A7%E7%9B%92%E5%AD%90%E6%A8%A1%E5%9E%8B.jpeg" alt="Sample"  width="500" height="320">
	<p align="center">
	</p>
</p>





















