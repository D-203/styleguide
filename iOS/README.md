
# 赛维集团 移动团队 iOS Coding Style Objective-C 规范指南 

这份规范指南概括了赛维集团 iOS 团队的代码约定。

## 目录

* [点语法](#点语法)
* [间距](#间距)
* [条件判断](#条件判断)
* [三目运算符](#三目运算符)
* [错误处理](#错误处理)
* [方法](#方法)
* [变量](#变量)
* [命名](#命名)
* [注释](#注释)
* [Init 和 Dealloc](#init-和-dealloc)
* [字面量](#字面量)
* [CGRect 函数](#CGRect-函数)
* [常量](#常量)
* [枚举类型](#枚举类型)
* [位掩码](#位掩码)
* [私有属性](#私有属性)
* [图片命名](#图片命名)
* [布尔](#布尔)
* [单例](#单例)
* [导入](#导入)
* [Xcode 工程](#Xcode-工程)

## 点语法

应该 **始终** 使用点语法来访问或者修改属性，访问其他实例时首选括号。

**推荐：**
```objc
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```

**反对：**
```objc
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```

## 间距

* 一个缩进使用 4 个空格，永远不要使用制表符（tab）缩进。请确保在 Xcode 中设置了此偏好。
* 方法的大括号和其他的大括号（`if`/`else`/`switch`/`while` 等等）始终和声明在同一行开始，在新的一行结束。
* [强制]  应尽量控制每行代码的长度在120个字符以内。
* [强制] 用逗号分隔多项时，每个逗号后使用1个空格进行分隔。
* 左大括号位置
* [强制] 左大括号 { 不单独占据一行，放置在上一行的末尾，可以在 { 前增加一个空格。
* [强制] -，+ 与返回类型之间必须有一个空格，在参数列表中，除了参数之间不要有任何间距。
* [强制] * 号前面必须要加空格，增加可读性。
**推荐：**
```实例
- (void)doSomethingWithString:(NSString *)theString { 
    ...
}

///objc
if (user.isHappy) {
    // Do something
}
else {
    // Do something else
}
```
* 方法之间应该正好空一行，这有助于视觉清晰度和代码组织性。在方法中的功能块之间应该使用空白分开，但往往可能应该创建一个新的方法。
* `@synthesize` 和 `@dynamic` 在实现中每个都应该占一个新行。

**因为具体block长度的不同，可以有以下几种风格：**

*（1）如果block一行就能放下，就不需要换行。

*（2）如果必须要换行，那么 } 需要和block所在行的第一个字符对齐。

*（3）block中的代码块应该缩进4个空格。

*（4）如果block很大，比如超过20行，建议单独拿出来赋给一个本地变量

*（5）如果block没有参数，那字符 ^{ 之间就不应有空格。如果有参数，字符 ^{ 之间同样没有空格，但是字符 ) { 之间需要有一个空格。

*（6）包含内联block的函数调用可以在缩进4个空格的基础上左对齐，尤其是调用中包含多个内联block。

```

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
```

## 条件判断

条件判断主体部分应该始终使用大括号括住来防止[出错][Condiationals_1]，即使它可以不用大括号（例如它只需要一行）。这些错误包括添加第二行（代码）并希望它是 if 语句的一部分时。还有另外一种[更危险的][Condiationals_2]，当 if 语句里面的一行被注释掉，下一行就会在不经意间成为了这个 if 语句的一部分。此外，这种风格也更符合所有其他的条件判断，因此也更容易检查。

**推荐：**
```objc
if (!error) {
    return success;
}
```

**反对：**
```objc
if (!error)
    return success;
```

或

```objc
if (!error) return success;
```


[Condiationals_1]:(https://github.com/NYTimes/objective-c-style-guide/issues/26#issuecomment-22074256)
[Condiationals_2]:http://programmers.stackexchange.com/a/16530

### 三目运算符

三目运算符，? ，只有当它可以增加代码清晰度或整洁时才使用。单一的条件都应该优先考虑使用。多条件时通常使用 if 语句会更易懂，或者重构为实例变量。

**推荐：**
```objc
result = a > b ? x : y;
```

**反对：**
```objc
result = a > b ? x = c > d ? c : d : y;
```

## 错误处理

当引用一个返回错误参数（error parameter）的方法时，应该针对返回值，而非错误变量。

**推荐：**
```objc
NSError *error;
if (![self trySomethingWithError:&error]) {
    // 处理错误
}
```

**反对：**
```objc
NSError *error;
[self trySomethingWithError:&error];
if (error) {
    // 处理错误
}
```
一些苹果的 API 在成功的情况下会写一些垃圾值给错误参数（如果非空），所以针对错误变量可能会造成虚假结果（以及接下来的崩溃）。

## 方法

在方法签名中，在 -/+ 符号后应该有一个空格。方法片段之间也应该有一个空格。

**推荐：**
```objc
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
```

## 变量

变量名应该尽可能命名为描述性的。除了 `for()` 循环外，其他情况都应该避免使用单字母的变量名。
星号表示指针属于变量，例如：`NSString *text` 不要写成 `NSString* text` 或者 `NSString * text` ，常量除外。
尽量定义属性来代替直接使用实例变量。除了初始化方法（`init`， `initWithCoder:`，等）， `dealloc` 方法和自定义的 setters 和 getters 内部，应避免直接访问实例变量。更多有关在初始化方法和 dealloc 方法中使用访问器方法的信息，参见[这里][Variables_1]。

* [强制] 实现Category的文件名需包含类名，如 NSString+Utils.h 或 NSTextView+Autocomplete.h。

* 大驼峰式命名:每个单词的首字母都采用大写字母   

例子:
```
	MFHomePageViewController
	```
后缀要求
```
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
```
**推荐：**

```objc
@interface NYTSection: NSObject

@property (nonatomic) NSString *headline;

@end
```

**反对：**

```objc
@interface NYTSection : NSObject {
    NSString *headline;
}
```

类成员变量的命名是在普通变量的名字前，添加一个下划线做前缀，
``比如_usernameTextField。
``
小驼峰式命名:第一个单词以小写字母开始，后面的单词的首字母全部大写  
``例子:firstName、lastName``
以 _ 开头，第一个单词首字母小写 
``例子:NSString * _somePrivateVariable``

[Variables_1]:https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/mmPractical.html#//apple_ref/doc/uid/TP40004447-SW6

#### 变量限定符

当涉及到[在 ARC 中被引入][Variable_Qualifiers_1]变量限定符时，
限定符 (`__strong`, `__weak`, `__unsafe_unretained`, `__autoreleasing`) 应该位于星号和变量名之间，如：`NSString * __weak text`。

[Variable_Qualifiers_1]:(https://developer.apple.com/library/ios/releasenotes/objectivec/rn-transitioningtoarc/Introduction/Introduction.html#//apple_ref/doc/uid/TP40011226-CH1-SW4)

## 命名

尽可能遵守苹果的命名约定，尤其那些涉及到[内存管理规则][Naming_1]，（[NARC][Naming_2]）的。

长的和描述性的方法名和变量名都不错。

**推荐：**

```objc
UIButton *settingsButton;
```

**反对：**

```objc
UIButton *setBut;
```
类名和常量应该始终使用三个字母的前缀（例如 `NYT`），但 Core Data 实体名称可以省略。为了代码清晰，常量应该使用相关类的名字作为前缀并使用驼峰命名法。

**推荐：**

```objc
static const NSTimeInterval NYTArticleViewControllerNavigationFadeAnimationDuration = 0.3;
```

**反对：**

```objc
static const NSTimeInterval fadetime = 1.7;
```

属性和局部变量应该使用驼峰命名法并且首字母小写。

为了保持一致，实例变量应该使用驼峰命名法命名，并且首字母小写，以下划线为前缀。这与 LLVM 自动合成的实例变量相一致。
**如果 LLVM 可以自动合成变量，那就让它自动合成。**

**推荐：**

```objc
@synthesize descriptiveVariableName = _descriptiveVariableName;
```

**反对：**

```objc
id varnm;
```

[Naming_1]:https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/MemoryMgmt/Articles/MemoryMgmt.html

[Naming_2]:http://stackoverflow.com/a/2865194/340508

## 注释

当需要的时候，注释应该被用来解释 **为什么** 特定代码做了某些事情。所使用的任何注释必须保持最新否则就删除掉。

通常应该避免一大块注释，代码就应该尽量作为自身的文档，只需要隔几行写几句说明。这并不适用于那些用来生成文档的注释。


## init 和 dealloc

`dealloc` 方法应该放在实现文件的最上面，并且刚好在 `@synthesize` 和 `@dynamic` 语句的后面。在任何类中，`init` 都应该直接放在 `dealloc` 方法的下面。

`init` 方法的结构应该像这样：

```objc
- (instancetype)init {
    self = [super init]; // 或者调用指定的初始化方法
    if (self) {
        // Custom initialization
    }

    return self;
}
```

## 字面量

每当创建 `NSString`， `NSDictionary`， `NSArray`，和 `NSNumber` 类的不可变实例时，都应该使用字面量。要注意 `nil` 值不能传给 `NSArray` 和 `NSDictionary` 字面量，这样做会导致崩溃。

**推荐：**

```objc
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone" : @"Kate", @"iPad" : @"Kamal", @"Mobile Web" : @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingZIPCode = @10018;
```

**反对：**

```objc
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingZIPCode = [NSNumber numberWithInteger:10018];
```

## CGRect 函数

当访问一个 `CGRect` 的 `x`， `y`， `width`， `height` 时，应该使用[`CGGeometry` 函数][CGRect-Functions_1]代替直接访问结构体成员。苹果的 `CGGeometry` 参考中说到：

> All functions described in this reference that take CGRect data structures as inputs implicitly standardize those rectangles before calculating their results. For this reason, your applications should avoid directly reading and writing the data stored in the CGRect data structure. Instead, use the functions described here to manipulate rectangles and to retrieve their characteristics.

**推荐：**

```objc
CGRect frame = self.view.frame;

CGFloat x = CGRectGetMinX(frame);
CGFloat y = CGRectGetMinY(frame);
CGFloat width = CGRectGetWidth(frame);
CGFloat height = CGRectGetHeight(frame);
```

**反对：**

```objc
CGRect frame = self.view.frame;

CGFloat x = frame.origin.x;
CGFloat y = frame.origin.y;
CGFloat width = frame.size.width;
CGFloat height = frame.size.height;
```

[CGRect-Functions_1]:http://developer.apple.com/library/ios/#documentation/graphicsimaging/reference/CGGeometry/Reference/reference.html

## 常量

常量首选内联字符串字面量或数字，因为常量可以轻易重用并且可以快速改变而不需要查找和替换。常量应该声明为 `static` 常量而不是 `#define` ，除非非常明确地要当做宏来使用。

**推荐：**

```objc
static NSString * const NYTAboutViewControllerCompanyName = @"The New York Times Company";

static const CGFloat NYTImageThumbnailHeight = 50.0;
```

**反对：**

```objc
#define CompanyName @"The New York Times Company"

#define thumbnailHeight 2
```

## 枚举类型

当使用 `enum` 时，建议使用新的基础类型规范，因为它具有更强的类型检查和代码补全功能。现在 SDK 包含了一个宏来鼓励使用使用新的基础类型 - `NS_ENUM()`

**推荐：**

```objc
typedef NS_ENUM(NSInteger, NYTAdRequestState) {
    NYTAdRequestStateInactive,
    NYTAdRequestStateLoading
};
```

## 位掩码

当用到位掩码时，使用 `NS_OPTIONS` 宏。

**举例：**

```objc
typedef NS_OPTIONS(NSUInteger, NYTAdCategory) {
    NYTAdCategoryAutos      = 1 << 0,
    NYTAdCategoryJobs       = 1 << 1,
    NYTAdCategoryRealState  = 1 << 2,
    NYTAdCategoryTechnology = 1 << 3
};
```


## 私有属性

私有属性应该声明在类实现文件的延展（匿名的类目）中。

**推荐：**

```objc
@interface NYTAdvertisement ()

@property (nonatomic, strong) GADBannerView *googleAdView;
@property (nonatomic, strong) ADBannerView *iAdView;
@property (nonatomic, strong) UIWebView *adXWebView;

@end
```

## 图片命名

图片名称应该被统一命名以保持组织的完整。它们应该被命名为一个说明它们用途的驼峰式字符串，其次是自定义类或属性的无前缀名字（如果有的话），然后进一步说明颜色 和/或 展示位置，最后是它们的状态。

**推荐：**

* `RefreshBarButtonItem` / `RefreshBarButtonItem@2x` 和 `RefreshBarButtonItemSelected` / `RefreshBarButtonItemSelected@2x`
* `ArticleNavigationBarWhite` / `ArticleNavigationBarWhite@2x` 和 `ArticleNavigationBarBlackSelected` / `ArticleNavigationBarBlackSelected@2x`.

图片目录中被用于类似目的的图片应归入各自的组中。


## 布尔

因为 `nil` 解析为 `NO`，所以没有必要在条件中与它进行比较。永远不要直接和 `YES` 进行比较，因为 `YES` 被定义为 1，而 `BOOL` 可以多达 8 位。

这使得整个文件有更多的一致性和更大的视觉清晰度。

**推荐：**

```objc
if (!someObject) {
}
```

**反对：**

```objc
if (someObject == nil) {
}
```

-----

**对于 `BOOL` 来说, 这有两种用法:**

```objc
if (isAwesome)
if (![someObject boolValue])
```

**反对：**

```objc
if ([someObject boolValue] == NO)
if (isAwesome == YES) // 永远别这么做
```

-----

如果一个 `BOOL` 属性名称是一个形容词，属性可以省略 “is” 前缀，但为 get 访问器指定一个惯用的名字，例如：

```objc
@property (assign, getter=isEditable) BOOL editable;
```

内容和例子来自 [Cocoa 命名指南][Booleans_1] 。

[Booleans_1]:https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingIvarsAndTypes.html#//apple_ref/doc/uid/20001284-BAJGIIJE


## 单例

单例对象应该使用线程安全的模式创建共享的实例。

```objc
+ (instancetype)sharedInstance {
    static id sharedInstance = nil;

    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        sharedInstance = [[self alloc] init];
    });

    return sharedInstance;
}
```
这将会预防[有时可能产生的许多崩溃][Singletons_1]。

[Singletons_1]:http://cocoasamurai.blogspot.com/2011/04/singletons-your-doing-them-wrong.html

## 导入   

如果有一个以上的 import 语句，就对这些语句进行[分组][Import_1]。每个分组的注释是可选的。   
注：对于模块使用 [@import][Import_2] 语法。   

```objc   
// Frameworks
@import QuartzCore;

// Models
#import "NYTUser.h"

// Views
#import "NYTButton.h"
#import "NYTUserView.h"
```   


