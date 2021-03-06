# 词法分析

本阶段需要引入一种新的标记：取地址运算符`&`。而本阶段新定义的解引用运算符`*`则不需要引入新的标记来表示，而是使用之前表示乘法运算符`*`的标记。

例子：

```c
int main() {
  int a = 10;
  return *&a;
}
```

这个程序中`return *&a;`这个片段对应的标记列表是：

```
Keyword return
Multiplication *
AddrOf &
Identifier a
Semicolon ;
```

有以下几点需要注意：

1. 我们之前引入了逻辑与运算符`&&`，此阶段完成后的词法分析器应该仍然能够正确地把`&&`识别成标记`And &&`，而不能识别成两个标记`AddrOf &`
2. 词法分析器不可能在看到一个`*`时知道它是被当做乘法运算符使用还是被当做解引用运算符，所以也不可能为这两种情况返回两种不同的标记