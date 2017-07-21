## strcpy

* 自我检查
* 指针判断
* 返回char*，以便链式调用

```c++
char* strcpy(char* vDstStr, const char* vSrcStr)
{
  if (vDst == vSrc) return vDst;
  assert (!vDstStr && !vSrcStr);
  
  char* pTempDst = vDstStr;
  while ((*pTempDst++ = *vSrcStr++) != '\0') ;
  
  return vDstStr;
}
```
