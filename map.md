
## map

map是关联性容器，内部自建红黑树（非严格意义的红黑树），具有自动排序功能。建立Key-value对应关系，key值需唯一，如果key是结构体，需重载operator <，让其可排序。
否则会出错。

### map的插入
  * insert： map.insert(std::make_pair(key, value))
  * 数组方式: map[key] = value
  
### map的查找
  * count: 存在返回1，不存在返回0
  * find: map.find(key), 返回迭代器的位置
  
  
### map的删除
  * map.erase(Itr++); 注意Itr++不是erase之后迭代器++, 而表达是使用删除前迭代器来定位下一元素；
  
  
### map的排序

```
struct SComp
{
  bool operator()(const std::string& vKey1, const std::string& vKey2)
  {
    return vKey.length() < vKey2.length();
  }
};

std::map<std::string, int, SComp> map; //自定义string长度排序；
```

### map的原理

* TODO
