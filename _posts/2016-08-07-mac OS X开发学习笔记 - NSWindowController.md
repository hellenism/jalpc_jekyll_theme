---
layout: post
title:  "JavaScript中if语句的几种优化代码的写法"
date:   2016-06-26
desc: "JavaScript中if语句的几种优化代码的写法"
keywords: "JavaScript,if,optimise,statement,优化"
categories: [HTML]
tags: [JavaScript]
icon: icon-javascript
---

[mac OS X开发学习笔记]NSWindowController的使用

一.新建一个窗口并弹出
二.新建一个模态窗口
三.实现appear和disappear

一.新建一个窗口并弹出
1.创建xib和 .h +.m文件，保证xib与m相关联(.xib关联.m , File ' s Owner关联Window)
 

2.重写init方法，编写相关业务<br />
<pre><code>
- (instancetype)init
{
    self = [super initWithWindowNibName:@"WindowOne"];
    if (self) {
        // do something
    }
    return self;
}
</code></pre>

3.show window (WindowController需要是一个成员变量,否则出现窗口show一下迅速消失的现象)<br />
<pre><code>
- (IBAction)btnClickOpenWindow:(id)sender 
{
    _controller = [[WindowOneController alloc]init];
    [_controller showWindow:self];
}
</code></pre>
 
二.新建一个模态窗口
1.保证xib中的Visble At Launch属性取消勾选
 

2.以模态形式弹出窗口
<pre><code>
-(IBAction)click:(id)sender
{
	_twoController = [[WindowTwoController alloc]init];
	[self.window beginSheet:_twoController.window  completionHandler:^(NSModalResponse returnCode) {
        NSLog(@"Sheet closed");
        switch (returnCode) {
            case NSModalResponseOK:
                NSLog(@"Done button tapped in Custom Sheet");
                break;
            case NSModalResponseCancel:
                NSLog(@"Cancel button tapped in Custom Sheet");
                break;
            default:
                break;
        }
        _twoController = nil;
    }];
}
</code></pre>


3.模态窗口中得ok和cancel按钮click事件，目的是return回一个code
<pre><code>
- (IBAction)didTapCancelButton:(id)sender {
   [self.window.sheetParent endSheet:self.window returnCode:NSModalResponseCancel];
}
- (IBAction)didTapDoneButton:(id)sender {
    [self.window.sheetParent endSheet:self.window returnCode:NSModalResponseOK];
}
</code></pre>

四. 实现appear和disappear
NSWindowController可能需要类型appear和disappear的方法，但是生命周期中并未提供，所以可利用NSWindow的回调进行实现
1.NSWindowController实现NSWindowDelegate

2.在NSWindowControoler的WindowDidLoad内设置Delegate
<pre><code>
- (void)windowDidLoad {
    [super windowDidLoad];
    [[self window]setDelegate:self];
}
</code></pre>


3.NSWindowController实现windowDidChangeOcclusionState方法
<pre><code>
- (void)windowDidChangeOcclusionState:(NSNotification *)notification
{
    if (self.window.occlusionState & NSWindowOcclusionStateVisible)
    {
        // Appear code here
    }
    else
    {
        // Disappear code here
    }
}
</code></pre>
