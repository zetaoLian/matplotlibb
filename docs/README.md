# 第一回：Matplotlib初相识

## 一、认识matplotlib

Matplotlib是一个Python 2D绘图库，用来绘制各种静态，动态，交互式的图表。

Matplotlib是Python数据可视化库中的泰斗，它已经成为python中公认的数据可视化工具。

## 二、一个最简单的绘图例子

```python
import matplotlib.pyplot as plt
import matplotlib as mpl
import numpy as np

fig, axes = plt.subplots() #ax 是一个可以制定坐标系的组区域
axes.plot([1,2,3,4],[1,4,2,3])
plt.show()
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220116233714400.png" alt="image-20220116233714400" style="zoom:50%;" />

## 三、Figure的组成

- `Figure`：顶层级，用来容纳所有绘图元素
- `Axes`：matplotlib宇宙的核心，容纳了大量元素用来构造一幅幅子图，一个figure可以由一个或多个子图组成
- `Axis`：axes的下属层级，用于处理所有和坐标轴，网格有关的元素
- `Tick`：axis的下属层级，用来处理所有和刻度有关的元素
- <img src="C:\Users\Williams\Desktop\matplotlib\image-20220116233733154.png" alt="image-20220116233733154" style="zoom: 50%;" />

## 四、两种绘图接口

第二种更常用（简洁）一点，即依赖plt自动创建figure 和 axes 

```python
x = np.linspace(0, 2, 100)

plt.plot(x, x, label='linear') 
plt.plot(x, x**2, label='quadratic')  
plt.plot(x, x**3, label='cubic')
plt.xlabel('x label')
plt.ylabel('y label')
plt.title("Simple Plot")
plt.legend()
plt.show()
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220116233752656.png" alt="image-20220116233752656" style="zoom: 67%;" />

## 五、通用绘图模板

```python
import matplotlib.pyplot as plt
import matplotlib as mpl
import numpy as np

#step 1 数据
x = np.linspace(0,2,100)
y = x**3
#step 2 设置绘图样式
mpl.rc('lines', linewidth=4, linestyle='-.')
#step 3 定于一布局
fig, ax = plt.subplots() #可以无？
#step 4 绘制图像
plt.plot(x,y,label='linear')
#step 5 x,y label title and 图例
plt.xlabel('x label')
plt.ylabel('y label')
plt.title("Simple Plot")
plt.legend()
plt.show()
```

(这个是思考题2)

# 第二回：艺术画笔见乾坤

## 一、 matplotlib的三层api

1. 绘图区  `Figure Canvas`

2. 渲染器  `Renderer`

3. `Artist` 分类：

- 1. `primitives `基本要素，包含一些标准图形对象，如**曲线Line2D，文字text，矩形Rectangle，图像image**等。
- 2. `container`是容器，即用来装基本要素的地方，包括**图形figure、坐标系Axes和坐标轴Axis**。

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220116233607119.png" alt="image-20220116233607119" style="zoom:50%;" />

## 二、基本元素 - primitives

### 1. 2DLines 二维曲线

#### a. 如何设置Line2D的属性

```python
# 1) 直接在plot()函数中设置
x = range(0,5)
y = [2,5,7,8,10]
plt.plot(x,y, linewidth=10); # 设置线的粗细参数为10
```

#### b. 如何绘制lines

**2) errorbar绘制误差折线图**

绘制errorbar

```python
fig = plt.figure()
x = np.arange(10)
y = 2.5 * np.sin(x / 20 * np.pi)
yerr = np.linspace(0.05, 0.2, 10)  # yerr：指定y轴水平的误差
plt.errorbar(x, y + 3, yerr=yerr, label='both limits (default)');
```

### 2. patches  二维图形类

#### a. Rectangle-矩形

**1) hist-直方图**

```python
x=np.random.randint(0,100,100) #生成[0-100)之间的100个数据,即 数据集 
bins=np.arange(0,101,10) #设置连续的边界值，即直方图的分布区间[0,10),[10,20)... 
plt.hist(x,bins,color='fuchsia',alpha=0.5)#alpha设置透明度，0为完全透明 
plt.xlabel('scores') 
plt.ylabel('count') 
plt.xlim(0,100); #设置x轴分布范围 plt.show()
```

ss

**2) bar-柱状图**

```python
# bar绘制柱状图
y = range(1,17)
plt.bar(np.arange(16), y, alpha=0.5, width=0.5, color='yellow', edgecolor='red', label='The First Bar', lw=3);
# x y 透明度
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220117000010763.png" alt="image-20220117000010763" style="zoom: 67%;" />

#### b. Polygon-多边形

常用的是**fill**类，它是基于xy绘制一个填充的多边形，它的定义：

matplotlib.pyplot.fill(*args, data=None, **kwargs)

```python
# 用fill来绘制图形
x = np.linspace(0, 5 * np.pi, 1000) 
y1 = np.sin(x)
y2 = np.sin(2 * x) 
plt.fill(x, y1, color = "g", alpha = 0.3);
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220117000139723.png" alt="image-20220117000139723" style="zoom: 67%;" />

#### c. Wedge-契形

wedge中比较常见的是绘制饼状图  **pie**

```python
# pie绘制饼状图
labels = 'Frogs', 'Hogs', 'Dogs', 'Logs'
sizes = [15, 30, 45, 10] 
explode = (0, 0.1, 0, 0) #偏移量
fig1, ax1 = plt.subplots() 
ax1.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%', shadow=True, startangle=90) 
# 大小 偏移 标签 数字格式  startangle：饼状图开始的绘制的角度。
ax1.axis('equal'); # Equal aspect ratio ensures that pie is drawn as a circle. 
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220117000300044.png" alt="image-20220117000300044" style="zoom: 67%;" />

### 3. collections 收集

包括了scatter 画散点图

```python
# 用scatter绘制散点图
x = [0,2,4,6,8,10] 
y = [10]*len(x) 
s = [20*2**n for n in range(len(x))] 
plt.scatter(x,y,s=s) ;
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220117000546659.png" alt="image-20220117000546659" style="zoom:67%;" />

### 4. images 图像

略

## 三、对象容器 - Object container

略

## 思考题

- primitives 和 container的区别和联系是什么，分别用于控制可视化图表中的哪些要素

  primitives是基本元素，containers是容器。

  区别：

  primitives 是基本元素，包括的是一些标准图像，如曲线、图形、图像、散点等。

  containers是容器，包括的是图形figure、坐标系Axes、坐标轴Axis和Tick等。

  联系： 

  容器会包含一些primitives，容器还有它自身的属性。



- 分别用一组长方形柱和填充面积的方式模仿画出下图，函数 y = -1 * (x - 2) * (x - 8) +10 在区间[2,9]的积分面积

```python
    # bar绘制柱状图
    x = np.linspace(0, 10, 100) 
    y = -1 * (x - 2) * (x - 8) +10 
    x2 = np.linspace(2, 9, 40) 
    y2 = -1 * (x2 - 2) * (x2 - 8) +10 
    plt.ylim((0, 20))
    plt.plot(x,y,color='red')
    plt.bar(x2, y2, alpha=0.5, width=0.1, color='gray', label='The First Bar', lw=3); #alpha 透明度
    # plt.fill_between(x2,0,y2,facecolor='gray',alpha=0.5)
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220117003945992.png" alt="image-20220117003945992" style="zoom:50%;" />

```python
# bar绘制柱状图
x = np.linspace(0, 10, 100) 
y = -1 * (x - 2) * (x - 8) +10 
x2 = np.linspace(2, 9, 40) 
y2 = -1 * (x2 - 2) * (x2 - 8) +10 
plt.ylim((0, 20))
plt.plot(x,y,color='red')
plt.bar(x2, y2, alpha=0.5, width=0.1, color='gray', label='The First Bar', lw=3); #alpha 透明度
```

<img src="C:\Users\Williams\Desktop\matplotlib\image-20220117004021648.png" alt="image-20220117004021648" style="zoom:50%;" />

