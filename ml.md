
## Tensorflow 

Tensorflow是深度学习框架，使用**有向无环图**来表示计算任务，其中图的节点为**OP(operation)**。每个OP可对应多个**张量(tensor)**，tensor表示类型化的多维数据。

图的计算过程必须在**会话（Session）**中启动，会话把图的op分发到CPU或GPU的的**设备**上，同时执行op的方法，最后把计算的tensor返回。

* python: 返回tensor是numpy的ndarray的数组
* c++:    返回tensorflow::Tensor实例

![][1]

---
### 计算图

### 边

* 数据依赖：实现边表示数据依赖，代表数据(张量)。任意维度的数据称为张量，张量在数据流图中从前往后流动一遍为完成一次**前向传播(forward propagation)**，而残差从后往前流动一遍为**反向传播(backword propagation)**
* 控制依赖：虚线边用于控制操作的运行，确保happen-before关系，虚线边没有数据流过

### 节点

图中节点称为算子，代表操作(operation, OP),用来表示施加的数学运算，可以表示数据输入(feed in)的起点以及输出(push out)的终点,或者是**读取/写入持久变量(pesistent variable)**的终点。

#### 会话

会话（session）提供在图中执行操作的一些方法，模式为建立会话形成空图，在会话中添加节点和边，形成图然后执行。 会话可以对应多个图，可以修改图的结构，也可以注入数据进行科学计算。

* run:运行图，传入Tensor，即为**填充(feed)**过程；返回结果类型根据输入类型而定，为**取回(fetch)**过程
* Extend:在Graph中添加节点

### 设备

用来运算并且拥有自己地址的硬件，如CPU和GPU

### 变量

变量(variable)是特殊的数据结构，在图中有确定的位置，不可流动。创建方式为tf.Variable()构造函数，构造函数需要初始值，初始值的类型和形状确定变量的形状和类型。

* 填充机制：构件图时使用tf.placeholder()临时代替任意操作的张量，调用Session对象的run()执行图时，使用填充数据作为调用参数。

### 内核

操作是对抽象操作如add的一个统称，而内核是真正运行在特定设备上对操作的实现。所以，同一个操作可能对应多个内核。定义操作，需要把新操作和内核注册到系统中。



[1]:https://www.tensorflow.org/images/tensors_flowing.gif