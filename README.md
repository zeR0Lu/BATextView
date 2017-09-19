# BATextView
[![BAHome Team Name](https://img.shields.io/badge/Team-BAHome-brightgreen.svg?style=flat)](https://github.com/BAHome "BAHome Team")
![](https://img.shields.io/badge/platform-iOS-red.svg) ![](https://img.shields.io/badge/language-Objective--C-orange.svg) 
![](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg) 
![](https://img.shields.io/cocoapods/v/BATextView.svg?style=flat) ![](https://img.shields.io/cocoapods/dt/BATextView.svg
)  [![](https://img.shields.io/badge/微博-博爱1616-red.svg)](http://weibo.com/538298123)

## 1、功能及简介
* 1、可以自定义 placeholder的(字体、颜色)、文字(字体、颜色) <br>
* 2、可以自定义 输入文字的(字体、颜色)、文字(字体、颜色)
* 3、可以自动布局，自适应高度，实时监测输入文字的最大高度
* 4、可以实时监测输入文字的最大个数，可以限制最大输入文字字数
* 5、用分类整理，无需改动源码即可实现各种自定义功能

## 2、图片示例
![BATextView](https://github.com/BAHome/BATextView/blob/master/Images/BATextView.gif)

## 3、安装、导入示例和源码地址
* 1、pod 导入【最新版本：![](https://img.shields.io/cocoapods/v/BATextView.svg?style=flat)】： <br>
 `pod 'BATextView'` <br>
如果发现 `pod search BATextView` 搜索出来的不是最新版本，需要在终端执行 cd 转换文件路径命令退回到 desktop，然后执行 `pod setup` 命令更新本地spec缓存（可能需要几分钟），然后再搜索就可以了。<br>
具体步骤：
  - pod setup : 初始化
  - pod repo update : 更新仓库
  - pod search BATextView
* 2、文件夹拖入：下载demo，把 BATextView 文件夹拖入项目即可，<br>
* 3、导入头文件：<br>
`  #import "BATextView.h" `<br>
* 4、项目源码地址：<br>
 OC 版 ：[https://github.com/BAHome/BATextView](https://github.com/BAHome/BATextView)<br>

## 4、BATextView 的类结构及 demo 示例
![BATextView](https://github.com/BAHome/BATextView/blob/master/Images/BATextView.png)

### UITextView+BAKit.h
```
#import <UIKit/UIKit.h>

/**
 实时监测 TextView 输入文字，并返回当前文字最大高度，以便做自适应高度

 @param current_textViewHeight 当前文字的最大高度
 */
typedef void (^BAKit_TextView_HeightDidChangedBlock)(CGFloat current_textViewHeight);

/**
 实时监测 TextView 输入文字，并返回当前文字字符个数

 @param current_wordNumber 当前文字的字符个数
 */
typedef void (^BAKit_TextView_WordDidChangedBlock)(NSInteger current_wordNumber);

@interface UITextView (BAKit)

/**
 placeholder：文字
 */
@property(nonatomic, strong) NSString *ba_placeholder;

/**
 placeholder：文字颜色
 */
@property(nonatomic, strong) UIColor *ba_placeholderColor;

/**
 placeholder：文字字体
 */
@property(nonatomic, strong) UIFont *ba_placeholderFont;

/**
 文字字体，注意：一定要用 ba_textFont 设置，用系统的 self.font 设置无效
 */
@property(nonatomic, strong) UIFont *ba_textFont;

/**
 文字颜色，注意：一定要用 ba_textColor 设置，用系统的 self.textColor 设置无效
 */
@property(nonatomic, strong) UIColor *ba_textColor;

/**
 最大高度，如果需要随文字改变高度的时候使用
 */
@property (nonatomic, assign) CGFloat ba_maxHeight;

/**
 最小高度，如果需要随文字改变高度的时候使用
 */
@property (nonatomic, assign) CGFloat ba_minHeight;

/**
 实时监测 TextView 输入文字，并返回当前文字最大高度，以便做自适应高度
 */
@property(nonatomic, copy) BAKit_TextView_HeightDidChangedBlock ba_textView_HeightDidChangedBlock;

/**
 最大字数限制
 */
@property (nonatomic, assign) NSInteger ba_maxWordLimitNumber;

/**
 实时监测 TextView 输入文字，并返回当前文字字符个数
 */
@property(nonatomic, copy) BAKit_TextView_WordDidChangedBlock ba_textView_WordDidChangedBlock;


/**
 是否为空

 @return YES，NO
 */
- (BOOL)ba_textView_isEmpty;

/**
 快速设定自动布局

 @param maxHeight 最大高度
 @param minHeight 最小高度
 @param block BAKit_TextView_HeightDidChangedBlock
 */
- (void)ba_textView_autoLayoutWithMaxHeight:(CGFloat)maxHeight
                                  minHeight:(CGFloat)minHeight
                                      block:(BAKit_TextView_HeightDidChangedBlock)block;

/**
 快速设定最大字数限制返回当前字数

 @param limitNumber 最大字数限制
 @param block BAKit_TextView_WordDidChangedBlock
 */
- (void)ba_textView_wordLimitWithMaxWordLimitNumber:(NSInteger)limitNumber
                                              block:(BAKit_TextView_WordDidChangedBlock)block;

@end
```

### demo 示例
```
// 示例1：
- (UITextView *)textView1
{
    if (!_textView1)
    {
        _textView1 = [UITextView new];
        _textView1.backgroundColor = BAKit_Color_Gray_11;
        /**
         文字字体，注意：一定要用 ba_textFont 设置，用系统的 self.font 设置无效
         */
        _textView1.ba_textFont = [UIFont systemFontOfSize:13];
        /**
         文字颜色，注意：一定要用 ba_textColor 设置，用系统的 self.textColor 设置无效
         */
        _textView1.ba_textColor = [UIColor purpleColor];
        
        _textView1.backgroundColor = BAKit_Color_Gray_11;
        // 自定义 placeholder
        _textView1.ba_placeholder = @"这里是 placeholder ！";
        // 自定义 placeholder 颜色
        _textView1.ba_placeholderColor = [UIColor greenColor];
        // 自定义 placeholder 字体
        _textView1.ba_placeholderFont = [UIFont systemFontOfSize:16];
        
        [self.view addSubview:_textView1];
    }
    return _textView1;
}
    
// 示例2：
- (UITextView *)textView
{
    if (!_textView)
    {
        _textView = [UITextView new];
        _textView.userInteractionEnabled = YES;
        /**
         文字字体，注意：一定要用 ba_textFont 设置，用系统的 self.font 设置无效
         */
        _textView.ba_textFont = [UIFont systemFontOfSize:13];
        /**
         文字颜色，注意：一定要用 ba_textColor 设置，用系统的 self.textColor 设置无效
         */
        _textView.ba_textColor = [UIColor redColor];
        
        _textView.backgroundColor = BAKit_Color_Gray_11;
        // 自定义 placeholder
        _textView.ba_placeholder = @"这里是 placeholder ！";
        // 自定义 placeholder 颜色
        _textView.ba_placeholderColor = [UIColor orangeColor];
        // 自定义 placeholder 字体
        _textView.ba_placeholderFont = [UIFont systemFontOfSize:25];
        
        /**
         快速设定自动布局
         
         @param maxHeight 最大高度
         @param minHeight 最小高度
         @param block BAKit_TextView_HeightDidChangedBlock
         */
        BAKit_WeakSelf
        [_textView ba_textView_autoLayoutWithMaxHeight:100 minHeight:60 block:^(CGFloat current_textViewHeight) {
            BAKit_StrongSelf
            self.textView_Height = current_textViewHeight;
            [self.view setNeedsLayout];
        }];
        
        /**
         快速设定最大字数限制返回当前字数
         
         @param limitNumber 最大字数限制
         @param block BAKit_TextView_WordDidChangedBlock
         */
        [_textView ba_textView_wordLimitWithMaxWordLimitNumber:60 block:^(NSInteger current_wordNumber) {
            BAKit_StrongSelf
            dispatch_async(dispatch_get_main_queue(), ^{
                self.label3.text = [NSString stringWithFormat:@"%ld/%ld", (long)current_wordNumber, (long)self.textView.ba_maxWordLimitNumber];
                [self.view setNeedsLayout];
            });
        }];
        [self.view addSubview:self.textView];
    }
    return _textView;
}

其他示例可下载demo查看源码！
```

## 5、更新记录：【倒叙】
 欢迎使用 [【BAHome】](https://github.com/BAHome) 系列开源代码 ！
 如有更多需求，请前往：[【https://github.com/BAHome】](https://github.com/BAHome) 
 
 最新更新时间：2017-09-19 【倒叙】
 最新Version：【Version：1.0.2】
 更新内容：
 1.0.2.1、优化 - (BOOL)ba_textView_isEmpty; 方法，修复 输入文字和 placeholder 文字一样时判断无效的 bug(感谢群里 [@成都-刘军  11:52:23](https://github.com/liujunliuhong ) 同学提出的 bug！) <br>
 
 最新更新时间：2017-06-01 【倒叙】<br>
 最新Version：【Version：1.0.1】<br>
 更新内容：<br>
 1.0.1.1、优化注释<br>
 
 最新更新时间：2017-05-27 【倒叙】<br>
 最新Version：【Version：1.0.0】<br>
 更新内容：<br>
 1.0.0.1、可以自定义 placeholder的(字体、颜色)、文字(字体、颜色)<br>
 1.0.0.2、可以自定义 输入文字的(字体、颜色)、文字(字体、颜色)<br>
 1.0.0.3、可以自动布局，自适应高度，实时监测输入文字的最大高度<br>
 1.0.0.4、可以实时监测输入文字的最大个数，可以限制最大输入文字字数<br>
 1.0.0.5、用分类整理，无需改动源码即可实现各种自定义功能<br>

## 6、bug 反馈
> 1、开发中遇到 bug，希望小伙伴儿们能够及时反馈与我们 BAHome 团队，我们必定会认真对待每一个问题！ <br>

> 2、以后提需求和 bug 的同学，记得把 git 或者博客链接给我们，我直接超链到你们那里！希望大家积极参与测试！<br> 

## 7、BAHome 团队成员
> 1、QQ 群 
479663605 <br> 
【注意：此群为 2 元 付费群，介意的小伙伴儿勿扰！】<br> 

> 孙博岩 <br> 
QQ：137361770 <br> 
git：[https://github.com/boai](https://github.com/boai) <br>
简书：[http://www.jianshu.com/u/95c9800fdf47](http://www.jianshu.com/u/95c9800fdf47) <br>
微博：[![](https://img.shields.io/badge/微博-博爱1616-red.svg)](http://weibo.com/538298123) <br>

> 马景丽 <br> 
QQ：1253540493 <br> 
git：[https://github.com/MaJingli](https://github.com/MaJingli) <br>

> 陆晓峰 <br> 
QQ：442171865 <br> 
git：[https://github.com/zeR0Lu](https://github.com/zeR0Lu) <br>

> 陈集 <br> 
QQ：3161182978 <br> 
git：[https://github.com/chenjipdc](https://github.com/chenjipdc) <br>
简书：[http://www.jianshu.com/u/90ae559fc21d](http://www.jianshu.com/u/90ae559fc21d)

> 任子丰 <br> 
QQ：459643690 <br> 
git：[https://github.com/renzifeng](https://github.com/renzifeng) <br>

> 吴丰收 <br> 
QQ：498121294 <br> 

> 石少庸 <br> 
QQ：363605775 <br> 
git：[https://github.com/CrazyCoderShi](https://github.com/CrazyCoderShi) <br>
简书：[http://www.jianshu.com/u/0726f4d689a3](http://www.jianshu.com/u/0726f4d689a3)

## 8、开发环境 和 支持版本
> 开发使用 最新版本 Xcode，理论上支持 iOS 8 及以上版本，如有版本适配问题，请及时反馈！多谢合作！

## 9、感谢
> 感谢 [【BAHome】](https://github.com/BAHome) 团队成员倾力合作，后期会推出一系列 常用 UI 控件的封装，大家有需求得也可以在 issue 提出，如果合理，我们会尽快推出新版本！<br>

>  [【BAHome】](https://github.com/BAHome)  的发展离不开小伙伴儿的信任与推广，再次感谢各位小伙伴儿的支持！

