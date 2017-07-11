
### decltype

**decltype** 也是在编译时期推导变量类型，不同于auto的是，auto须明确定义变量类型的值。

  `decltype(exp)`
  
exp是表达式；


### 基本用法

```C++
int x = 0;
decltype(x) y = 1; // y-> int

const int& i = x;
decltype(i) j = y; // j-> const int&
```

### decltype 推导规则



### 与auto不同处
* 不需要变量定义就可以推导变量的类型；
* 推导规则会保留住表达式的引用和cv限定符；
