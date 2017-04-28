---
title: iOS 编码规范
date: 2017-04-27 15:40:16
tags: iOS
---


## 通用规范
- 含义清楚有意义，尽量做到不需要注释也能了解其作用，若做不到，就加注释
- 使用全称，不使用缩写，一些约定俗成的除外
- 尽量使用英语单词，避免使用拼音

## 命名规则
### 类的命名
- 大驼峰式命名：每个单词的首字母都采用大写字母（前缀用大写字母），如：EPHomePageViewController，OrderDetailViewController
- 针对Controller ，View的命名，要添加相应的后缀即XxxController，YyView；UITableCell，使用Cell做后缀
- 其他UI控件，遵循类似上面的规则
- Protocol，使用Delegate或者DataSource作为后缀
- 对于一些内部使用的工具类尽量添加前缀，避免和其他第三方库命名冲突

### 方法的命名
- 参数名以小写字母开始，之后的单词首字母大写，避免使用缩写
- 私有方法可以加前缀（可选） ，前缀与当前类的前缀保持一致，使用小写
- 在所有参数之前使用关键字即别名
```objective-c
- (instancetype)initWithNibName:(NSString *)nibNameOrNil bundle:(NSBundle *)nibBundleOrNil; ✅

- (instancetype)initWithNibName:(NSString *)nibNameOrNil 
:(NSBundle *)nibBundleOrNil; ❌
```


### 变量的命名
- 小驼峰式命名：第一个单词以小写字母开始，后面的单词的首字母全部大写，如：lastName
- 私有变量放在.m文件中

### 宏的命名
- 全部大写，单词间用 _ 分隔 [不带参数]，如：THIS_IS_MACRO @"this is macro"
- 以字母 k 开头，后面遵循大驼峰命名 [不带参数]，如：kButtonWidth  40
- 小驼峰命名 [带参数]，如：defaultFont(s)   [UIFont fontWithName:@"ArialMT" size:s]

### 枚举的命名
- Enum类型的命名与类的命名规则一致
- Enum中枚举内容的命名需要以该Enum类型名称开头，如：
```objective-c
typedef NS_ENUM(NSInteger, AFOperationState) {
    AFOperationPausedState      = -1,
    AFOperationReadyState       = 1,
    AFOperationExecutingState   = 2,
    AFOperationFinishedState    = 3,
};
```

## 注释
- 最好的代码是不需要注释的 ，尽量通过合理的命名，如果做不到命名尽量的见名知意的话，就可以适当的添加一些注释或者mark
- 注释需要与代码同步更新
- 对于一些变量或者注释内容简短的可以使用单行注释，对于注释内容多或者复杂方法使用多行注释，如：


```objective-c
/**
 * Init a new cache store with a specific namespace and directory
 * @param ns        The namespace to use for this cache store
 * @param directory Directory to cache disk images in
 */
- (id)initWithNamespace:(NSString *)ns diskCacheDirectory:(NSString *)directory;

/**
 * The maximum number of objects the cache should hold.
 */
@property (assign, nonatomic) NSUInteger maxMemoryCountLimit;

@property(nonatomic, strong) NSString *dishesCode;//菜品编号
```

## 格式化
- 属性的声明，@property和类型与括弧之间保留一个空格，属性修饰符之间逗号隔开，并保留一个空格
```objective-c
@property (nonatomic, copy) NSString *lastSelectedString; ✅

@property(nonatomic,strong)NSString *name; ❌
```
- 方法的声明， - 、+ 和 返回值 之间留一个空格，如果参数过多，可考虑每个参数单独换行，参数类型与`*`之间保留空格，如：
```objective-c
- (NSURLSessionDataTask *)HEAD:(NSString *)URLString
                    parameters:(id)parameters
                       success:(void (^)(NSURLSessionDataTask *task))success
                       failure:(void (^)(NSURLSessionDataTask *task, NSError *error))failure;
```
- 方法之间间隔一行，方法体内部不要多余的空行，方法体使用一个tab的缩进

- 使用 #pragma mark - 方式对类的方法进行分组，分组按照一定的功能关联性或者流程性划分

- 方法的左括号，放在方法结尾，右括号单独另起一行；对于其他情况的左括号放在行尾

- 对于一些流程控制语句即使语法上有可以不使用括号的，也需要加上括号，括号和判断条件之间保留一个空格，如：
```objective-c
if (error) {
    if (failure) {
        NSLog(@"this is wrong!!!");
     }
 } else {
     if (success) {
         NSLog(@"this is success!!!");
       }
 }
```
- 对于缩进，使用 xcode 默认缩进，即一个tab (4空格)
- 方法嵌套调用的时候，保留一个空格，如：
```objective-c
[[NSURLConnection alloc] initWithRequest:self.request delegate:self startImmediately:NO]; ✅

[[NSNotificationCenter defaultCenter]postNotificationName:AFNetworkingOperationDidStartNotification object:self]; ❌
```
- 在书写字典的key-value的时候，冒号要紧跟在key后面并与value之间保留一个空格，如：
```objective-c
@[
     @{ @"title": @"英",
        @"languageType": kSearchWordLanguageTypeEnglish },
                
     @{ @"title": @"日",
        @"languageType": kSearchWordLanguageTypeJapanese }
];
```