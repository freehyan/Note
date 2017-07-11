
## vector

vector是线性容器，内部实现方式是动态数组，元素存储在连续的内存空间，重载了操作符operator[]，所以支持数组的随机访问。也可以使用迭代器访问。

* 容器大小：元素个数
* 容器容量: 分配的内存大小可容纳的元素个数

### 基本用法

//构造函数
vector();
vector( size_type num, const TYPE &val ); //n个相同值的vector
vector( const vector &from );             //拷贝构造函数
vector( input_iterator start, input_iterator end ); //迭代器构造函数

//迭代器
iterator begin(); //vector第一个元素的迭代器
iterator end(); //vector末尾的迭代器，注意这里实际是最后一个元素向后移动一个单位的迭代器

//分配函数
void assign( input_iterator start, input_iterator end );
void assign( size_type num, const TYPE &val );

//首尾元素的引用
TYPE front();
TYPE back();

size_type size();      //当前vector元素数目
size_type capacity(); //返回当前vector在重新进行内存分配以前所能容纳的元素数量

//删作指定位置loc的元素,要么删除区间[start, end)的所有元素.返回值是指向删除的最后一个元素的下一位置的迭代器.如果不以左值得方式赋值，那么当前的迭代器就是一个野指针。
iterator erase( iterator loc );
iterator erase( iterator start, iterator end );

//get_allocator() 函数返回当前vector的内存分配器.在STL里面一般不会调用new或者alloc来分配内存,而且通过一个allocator对象的相关方法来分配.
allocator_type get_allocator();

//reserve()函数为当前vector预留至少共容纳size个元素的空间.(译注:实际空间可能大于size)
void reserve( size_type size );

### 知识点

* reserve()容器预留空间，并没有实际元素创建对象；
* resize()是改变容器大小，并且创建对象，可以初始元素的默认值。
* <algorithm>的sort函数可对vector容器排序，前提是自定义结构体重载了比较符，operator <;或者在结构体外定义比较函数

### vector 排序
  * std::sort(vec.begin(), vec.end(), comp)

### vector 查找
  * auto t = std::find(vec.begin(), vec.end(), value)
 
### vector 删除
  * 注意迭代器指针失效的情况,因为vec.erease(Itr)执行后，Itr是野指针: 1) 连续存在相同元素 2）元素在容器末尾
  
  ```
  for (auto Itr = vec.begin(); Itr!=vec.end();)
    {
    if (*Itr == value)
      Itr = vec.erase(Itr);
    else
      Itr++;
      }
  ```
 
  * 删除区间元素: vec.erase(vec.begin() + i vec.begin() + j)
  
  ---
  
  ## vector的内存管理与效率
  * 剩余容量不能放入新元素时，重新分配当前内存空间大小1.5~2倍新内存区，再把原数组内容拷贝过去；
  * 使用reserve函数提前设定容量大小: vec.resever(10000)
  * 使用“交换技巧”修整vector过剩空间/内存: std::vector<int>(vec).swap(vec), 因为vector<int>(vec)只是一个临时vector，vector拷贝构造函数只分配拷贝元素的内存。
  * 使用swap强行释放vector所占内存：vec.swap(std::vector<int>())
  
  ## vector的简单实现
  
  
  
  
  
