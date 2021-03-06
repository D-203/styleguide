# Java编码规范

## 内容大纲
1. [命名规范](#naming-guide)
    + 1.1 [项目目录命名规范](#project-naming)
    + 1.2 [包命名规范](#package-naming)
    + 1.3 [类命名规范](#class-naming)
    + 1.4 [方法命名规范](#method-naming)
    + 1.5 [常量命名规范](#constants-naming)
    + 1.6 [变量命名规范](#variable-naming)
2. [源代码文件结构](#source-structure)
    + 2.1 [源代码文件命名规范](#source-naming)
    + 2.2 [源代码文件编码规范](#encoding-guide)
    + 2.3 [特殊字符规范](#special-chars)
    + 2.4 [源代码文件结构规范](#structure-guide)
    + 2.5 [类内部结构规范](#class-structure)
3. [代码格式规范](#format-guide)
    + 3.1 [缩进与对齐规范](#indents-guide)
    + 3.2 [空格使用规范](#whitespace-guide)
    + 3.3 [换行规范](#linewrap-guide)
    + 3.4 [变量的声明和初始化](#var-init-guide)
    + 3.5 [修饰符的顺序](#syntax-guide)
4. [注释规范](#comments-guide)
5. [注解规范](#annotation-guide)


<a name="naming-guide"></a>
## 命名规范

<a name="project-naming"></a>
[1.1] **项目目录命名规范**
* 全小写英文
* 以项目名称命名
* 多个单词间以下划线连接

<a name="package-naming"></a>
[1.2] **包命名规范**
* 全小写英文
* 多个单词间不能使用驼峰或下划线连接
```java
// 正确
org.springframework.context
// 错误
org.springFramework.context
org.spring_framework.context
```

<a name="class-naming"></a>
[1.3] **类命名规范**
* 驼峰式命名法 UpperCamelCase
* 使用表明类功能的名词或动词短语命名
* 测试类以待测试类名加Test构成
```java
// 正确
UserDAOTest
```
* 抽象类以Abstract开头
```java
// 正确
AbstractXmlParser
```
* 类的命名能够显示的归类其所处架构层级
```java
// 正确
LoginFormBean
LoginController
LoginService
UserDAO
```
* 如果应用类设计模式，以设计模式作为后缀
```java
// 正确
RouterAdapter
LoginProxy
TransctionFactory
```
* 领域模型相关命名规范(待讨论),如：DO，DTO，BO，VO
* 枚举类的命名加后缀Enum
```java
// 正确
OrderStatusEnum
```
* 枚举成员用下划线连接的全大写单词组合
```java
// 正确
STATUS_NEW
STATUS_PAID
```

<a name="method-naming"></a>
[1.4] **方法命名规范**
* 小写开头的驼峰命名法：findById
* 一般以动词加名词的形式表达方法的职能
* 避免信息冗余，如在UserDao中方法findById而不命名为findUserById
* 方法命名约定（待讨论）
* 获取单个对象load
* 获取对象集合find
* 插入对象save
* 更新对象update
* 删除对象remove
* 统计对象count
* 聚合数值sum、avg

<a name="constants-naming"></a>
[1.5] **常量命名规范**
* 以下划线连接的全大写英文单词的组合
* 使用名词或名词性词组
* 常量进行分级维护：全局跨应用常量，应用内常量，包内常量，类内常量

<a name="variable-naming"></a>
[1.6] **变量命名规范**
* 不能以下划线和美元符号开始或结束
```java
// 错误：
private String _userName;
private String $userName;
private String userName_;
private String userName$
```
* 小写字母开头的英文单词的组合lowerCamelCase
* 使用驼峰式命名法
* 使用名词或名词性词组
* 命名准确，望文知义，避免不必要的缩写
```java
// 错误
private String kName;
```

<a name="source-structure"></a>
## 源代码文件结构

<a name="source-naming"></a>
[2.1] **源代码文件命名规范**
* 与类命名规则相同
* 与文件中公有类名相同
* 一个类文件只能存在一个顶级的类定义

<a name="encoding-guide"></a>
[2.2] **源代码文件编码规范**
* 使用UTF-8编码格式

<a name="special-chars"></a>
[2.3] **特殊字符规范**
* 源代码中不能存在硬编码字符
* 源代码文件中不能直接硬编码，所有提示信息等通过资源文件存储
```java
// 错误
private String chineseName = "中文名";
```

<a name="structure-guide"></a>
[2.4] **源代码文件结构规范**
* 版权声明和许可条款说明
* 包声明语句
* 导入语句：不允许静态导入语句
* 公有类声明
* 以上每部分之间以一个空行分隔

<a name="class-structure"></a>
[2.5] **类内部结构规范**
* 每个源代码文件只包含一个类声明即无非公有的类
* 类注释格式（待讨论）职能，作者，时间
* 类成员顺序：静态常量，静态变量，动态常量，动态变量，静态语句块，构造函数，公有方法，保护方法，私有方法
* 构造函数顺序：根据参数数量从小到大
* 重载方法顺序：根据参数数量从小到大，中间不能夹杂其他方法
* 类修改规范：新增的成员是放在此类的成员的尾部

<a name="format-guide"></a>
## 代码格式规范

<a name="indents-guide"></a>
[3.1] **缩进与对齐规范**
* 换行符使用Unix风格换行符
* 使用空格缩进而不使用Tab键缩进
* 每一级缩进4个空格
* 每行只包含一句代码语句
* 行宽120字符
* 单行代码过长时换行，换行缩进4个空格
* 花括号样式 （待讨论）
* if等的处理语句块，即使只有一行代码也要将其写在{}内

<a name="whitespace-guide"></a>
[3.2] **空格使用规范**
* 在for，if，do，while等控制语句关键词后用空格将逻辑语句块隔离
```java
// 正确
for (int i = 0; i < 10; i++) {
}
```
* 在二元运算符的左右分别用空格隔离
* 分号代表前一语句的结束，它之前不需要空格，它之后用空格将两句语句隔离
* 一元运算符与操作数之间不用空格隔离

<a name="linewrap-guide"></a>
[3.3] **换行规范**
* 运算符与下行一起换行
```java
// 正确
String str = "the 1st line "
    + "the 2nd line "
    + "the 3rd line ";
```
* 方法调用的.与下文一起换行
```java
// 正确
StringBuilder sb = new StringBuilder();
sb.append("the 1st line")
    .append("the 2nd line")
    .append("the 3rd line");
```
* 多个参数时在逗号后换行
```java
// 正确
public void methoName(String arg1, String arg2,
                        Integer arg3, Integer arg4) {
}
```
* 在括号前不换行
```java
// 错误
public void methodName
(String arg1, String arg2, String arg3 String arg4){
}
```

<a name="var-init-guide"></a>
[3.4] **变量的声明和初始化**
* 每个变量定义单独一行
```java
// 错误
private int outerIndex = 0, innerIndex = 0;
// 正确
private int outerIndex = 0;
private int innerIndex = 0;
```
* 初始化long， float和double类型时使用L，F和D后缀
```java
// 正确
private long bigRange = 1L;
private double square = 3.14D;
```
* 声明数组类型变量时[]紧跟在类型之后，在变量名之前
```java
// 正确
private String[] cities = new String[] {"BJ", "SH"};
// 错误
private String cities[] = new String[] {
                                        "BJ", 
                                        "SH"
                                        };
```
* 数组通过枚举法初始化时在同一行，过长时才进行换行
* 多行变量声明之间不纵向对齐
```java
// 正确
private Integer userAge;
private Double userWeight;
private int size;

// 错误
private Integer userAge;
private Double  userWeight;
private int     size;
```

<a name="syntax-guide"></a>
[3.5] **修饰符的顺序**
* 修饰类、方法和变量的修饰符顺序如下
[public/protected/private] [abstract] [default] [static] [final/transient/volatile] [synchronized] [native] [strictfp]

<a name="comments-guide"></a>
## 注释规范
* 类注释和方法注释使用多行注释 
```java
/**
 * comments go here
 */
```
* 变量注释和代码块注释使用单行注释 // comments
* 注释的内容项目(待讨论)

<a name="annotation-guide"></a>
## 注解规范
* 注解跟着注释之后
* 每个注解单独占一行，只有一个注解时也是
* 注解跟在注释之后
```java
// 正确
@Override
@Transactional
public void method() {
}

// 错误
@Override @Transactional 
public void method() {
}
```






 


