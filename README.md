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

<img src="C:\Users\Williams\AppData\Roaming\Typora\typora-user-images\image-20220111220836690.png" alt="image-20220111220836690" style="zoom:67%;" />

## 三、Figure的组成

- `Figure`：顶层级，用来容纳所有绘图元素
- `Axes`：matplotlib宇宙的核心，容纳了大量元素用来构造一幅幅子图，一个figure可以由一个或多个子图组成
- `Axis`：axes的下属层级，用于处理所有和坐标轴，网格有关的元素
- `Tick`：axis的下属层级，用来处理所有和刻度有关的元素<img src="C:\Users\Williams\AppData\Roaming\Typora\typora-user-images\image-20220111221915508.png" alt="image-20220111221915508" style="zoom:67%;" />

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

<img src="C:\Users\Williams\AppData\Roaming\Typora\typora-user-images\image-20220111221402137.png" alt="image-20220111221402137" style="zoom: 67%;" />

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

