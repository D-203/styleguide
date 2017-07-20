iOS Coding Style
一.缩进与格式

1、缩进符
[强制] 只用空格，用4个空格表示一个缩进。

2、每行的长度
[强制] 应尽量控制每行代码的长度在120个字符以内。

3、逗号分隔项
[强制] 用逗号分隔多项时，每个逗号后使用1个空格进行分隔。

4、左大括号位置
[强制] 左大括号 { 不单独占据一行，放置在上一行的末尾，可以在 { 前增加一个空格。

5、声明与定义
[强制] -，+ 与返回类型之间必须有一个空格，在参数列表中，除了参数之间不要有任何间距。
实例
- (void)doSomethingWithString:(NSString *)theString { 
    ...
}
[强制] * 号前面必须要加空格，增加可读性。
6、Blocks
[强制] 块内的代码应缩进4个空格
因为具体block长度的不同，可以有以下几种风格：
（1）如果block一行就能放下，就不需要换行。
（2）如果必须要换行，那么 } 需要和block所在行的第一个字符对齐。
（3）block中的代码块应该缩进4个空格。
（4）如果block很大，比如超过20行，建议单独拿出来赋给一个本地变量
（5）如果block没有参数，那字符 ^{ 之间就不应有空格。如果有参数，字符 ^{ 之间同样没有空格，但是字符 ) { 之间需要有一个空格。
（6）包含内联block的函数调用可以在缩进4个空格的基础上左对齐，尤其是调用中包含多个内联block。

///演例
//整个block放在一行的 
[operation setCompletionBlock:^{ [self onOperationDone]; }];

//多行时缩进四个空格，{要和block所在行的第一个字符对齐
[operation setCompletionBlock:^{

    [self.delegate newDataAvailable];
}]; 

//在C函数中使用block时遵循和Objective-C同样的对齐和缩进原则
dispatch_async(fileIOQueue_, ^{

    NSString *path = [self sessionFilePath];     
    if (path) {       // ...     
    } 
});

// 方法参数与block声明能放到一行时。注意比较^(SessionWindow *window) {和上面的^{。 
[[SessionService sharedService]  loadWindowWithCompletionBlock:^(SessionWindow *window) {

    if (window) {          
     [self windowDidLoad:window];        
    } else {           
        [self errorLoadingWindow];        
    }     
}]; 

//方法参数与block声明不能放到一行时。 
[[SessionService sharedService]     
    loadWindowWithCompletionBlock:^(SessionWindow *window) {  

        if (window) {              
         [self windowDidLoad:window];             
        } else {               
        [self errorLoadingWindow];             
        }         
    }];  

// 较长的Block可声明为变量。 
void (^largeBlock)(void) = ^{
     // ... 
}; 
[operationQueue_ addOperationWithBlock:largeBlock]; 

 // 一次调用中包含多个内联block。 
[myObject doSomethingWith:arg1
    firstBlock:^(Foo *a) { // ...
    }
    secondBlock:^(Bar *b){
            // ...
    }];
二.命名与规范

1.文件名
文件名应该反映其中包含的类实现的名称，按照项目中的约定且大小写相关。
[强制] 实现Category的文件名需包含类名，如 NSString+Utils.h 或 NSTextView+Autocomplete.h。
大驼峰式命名:每个单词的首字母都采用大写字母   
例子:MFHomePageViewController
后缀要求
        ViewController: 使用ViewController做后缀
 例子: 
        MFHomeViewController View: 使用View做后缀
例子: 
        MFAlertView UITableCell:使用Cell做后缀
例子: 
        MFNewsCell
Protocol: 使用Delegate或者DataSource作为后缀
例子: 
        UITableViewDelegate 
        UI控件依次类推
2.类名

[强制] 类名（包括Category、Protocol名和Block名）以大写字母开始，通过大小写而不是下划线分隔。
[建议] 在设计可跨越多个应用之间共享的代码时，推荐使用前缀，（例如，GTMSendMessage）。还有很多外部依赖库的大型应用中设计的类最好也使用前缀。
[建议] 若使用前缀，则前缀缩写要大于2个字符。

3.Category名

[强制] 类别（Category）名中需要加入被扩展的类名。
比如我们要给NSString类加一个解析的功能，我们创建一个category，命名为GTMStringParsingAdditions，并且放在名为NSString+Parsing.h的文件中。

4.Objective-C 方法名
[强制] 方法名应该以小写字母开头，混合大小写。每个命名参数也应该以小写字母开头。
[建议] 方法名称应该尽可能读起来像句子，意味着你应该选择能够搭配方法名的参数名。（比如：convertPoint:fromRect:或replaceCharactersInRange:withString:）。
[建议] getter类型的方法不加get前缀。

[强制] 变量名以小写字母开头，混合大小写以区分单词。

5.变量名
类成员变量的命名是在普通变量的名字前，添加一个下划线做前缀，比如_usernameTextField。
小驼峰式命名:第一个单词以小写字母开始，后面的单词的首字母全部大写   例子:firstName、lastName
以 _ 开头，第一个单词首字母小写   例子:NSString * _somePrivateVariable
私有变量放在 .m 文件中声明

6.宏命名
全部大写，单词间用 _ 分隔。[不带参数]
  例子: #define THIS_IS_AN_MACRO @"THIS_IS_AN_MACRO"
以字母 k 开头，后面遵循大驼峰命名。[不带参数]   例子:#define kWidth self.frame.size.width





