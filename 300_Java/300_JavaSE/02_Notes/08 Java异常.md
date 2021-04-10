## 09 Java异常

#### 1. 数组异常

1. java.lang.NullPointrException 未开辟空间使用数组
2. java.lang.ArrayIndexOutOfBoundsException索引超出合法空间
3. 长度[0，+∞)
   1. java.lang.ArryIndexOutOfBoundsException（0表示空数组，确定了存放的数据类型，但未真正意义上开辟空间，不能直接使用）
   2. java.lang.NegativeArraySizeException（-1编译通过，运行错误）