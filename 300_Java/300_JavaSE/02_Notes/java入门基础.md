## 一、注释

>注释不会被执行，Java中有三种类型注释
1. 单行注释
	+ " // "开头，之后内容
2. 多行注释
	+ 以" /\* " 开头，以" \*/ "结尾
	+ 不可嵌套（无意义）
	+ 可做行内注释
3. 文档注释
	+ 以" /\*\* "开头，以" \*/ "结尾
	+ 可生成项目的API  

案例：
```java
	/**
	*这里是文档注释
	*/
	public class Welcome{
		public static void main/*这里是行内注释*/(String[] args){
		
			//下面是打印语句。输出双引号中的内容
			System.out.println("我是videjin！");
			System.out.println("你好！");
			/*
			前进！
			无所畏惧
			*/
			System.out.println("加油！");
		}
	}
```
## 二、标识符

>给变量、类、方法以及包进行命名
1. 遵守规则
    + 开头: 
      + 字母 
      + 下划线\_ 
      + 美元符号$
    + 其他不部分:
      +  字母 
      + 下划线\_ 
      + 美元符号$ 
      + 数字 （不能作为开头）的任意组合
    + Java标识符大小写敏感、长度无限制
    + 不可以是Java的关键字

>Java采用Unicode标准国际字符集(2个字节表示一个符号,2¹⁶=65536,中文一万多,英文26个字母,其他语言等等都可包含),而不是ASCII字符集(1个字节,1个字节2⁸=256)。故字母不仅仅包含英文,还包含汉字等等。但是不建议使用汉字。

2. 关键词  
   
   | abstract   | assert  | boolean   | break     | byte       | case         |
   | :---------- | :------- | :--------- | :--------- | :---------- | :------------ |
   | catch      | char    | class     | const     | continue   | default      |
   | do         | double  | else      | extends   | final      | finally      |
   | float      | for     | goto      | if        | implements | import       |
   | imstanceof | int     | interface | long      | native     | new          |
   | null       | package | private   | protected | public     | return       |
   | short      | static  | strictfp  | super     | switch     | synchronized |
   | this       | throw   | throws    | transient | try        | void         |
   | volatile   | while   |           |           |            |              |
   
>关键词不需要背，实战中自然熟悉  

3. 使用规范
   + 驼峰规则
   + 类：每个单词首字母大写，如Man
   + 方法或变量：第一个单词小写，从第二个字母开始首字母大写，如eat()，eatFood()  

## 三、变量

1. 变量本质
   
