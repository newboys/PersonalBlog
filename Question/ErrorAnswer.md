Q: 打开项目显示无可用deceive

A: Deployment Target比当前xcode支持的最高版本还高，调整一下版本即可

Q:CocoaPods:--zsh: /usr/local/bin/pod: bad interpreter: /System/Library/Frameworks/Ruby.framework/Versions/2.0/usr/bin: no such file or directory

A:http://www.jianshu.com/p/3efdffc136c0

Q:如何解决collectionview 上一个button点击事件错乱问题？

Q:如何设置全屏HUD？

```
//第一种
[MBProgressHUD showHUDAddedTo:[UIApplication sharedApplication].keyWindow animated:YES];
//第二种
[MBProgressHUD showHUDAddedTo:self.view animated:YES];
[UIApplication sharedApplication].keyWindow.userInteractionEnabled = NO;
```

Q:编写和微信一样的录视频？

Q:UIButton type system和custom的区别为什么定时器system会闪？

Q:UILabel一行时居中多行时靠左

http://mingxianwei.github.io/2016/05/27/iOS%E4%B8%AD%E6%B1%82%E5%87%BAlabel%E4%B8%AD%E6%96%87%E5%AD%97%E7%9A%84%E8%A1%8C%E6%95%B0%E5%92%8C%E6%AF%8F%E4%B8%80%E8%A1%8C%E7%9A%84%E5%86%85%E5%AE%B9/

Q:Git, fatal: The remote end hung up unexpectedly
A:[stackoverflow](https://stackoverflow.com/questions/15240815/git-fatal-the-remote-end-hung-up-unexpectedly)

Q:ios 打包时遇到的问题 The binary file 'BInterestStreet.app/EmptyView.o' is not permitted. 
A:[so](https://stackoverflow.com/questions/20251252/invalid-bundle-structure-the-app-may-contain-only-one-executable-file)
删除Copy Bundle Resources相应的文件

Q:小数和整数显示问题

```
    NSString *moneyStr = [NSString stringWithFormat:@"%.2lf", money];
    moneyStr = [NSDecimalNumber decimalNumberWithString:moneyStr].stringValue;
    NSString *text = [NSString stringWithFormat:@"小计  ￥%@", moneyStr];
```

Q:控件约束不能依赖同等级固定位置的控件？
比如同一视图下，一个不固定位置的label依赖于一个固定位置的button

Q:富文本文字居中（如同一行前后字体大小不一致，他们会底部对齐）

```
NSMutableAttributedString *attribute = [[NSMutableAttributedString alloc]initWithString:[NSString stringWithFormat:@"¥%@ ", [NSString reviseString:_priceMoney]] attributes:@{NSFontAttributeName:[UIFont systemFontOfSize:21],NSForegroundColorAttributeName:[UIColor whiteColor]}];    
NSAttributedString *atr1 = [[NSAttributedString alloc]initWithString:@"确认支付" attributes:@{NSFontAttributeName:[UIFont systemFontOfSize:16],NSForegroundColorAttributeName:[UIColor whiteColor], NSBaselineOffsetAttributeName:@(1.5)}];
[attribute appendAttributedString:atr1];
```

Q:设置换行缩进

```
 NSMutableParagraphStyle *paraStyle = [[NSMutableParagraphStyle alloc] init];
 paraStyle.alignment = NSTextAlignmentLeft;  //对齐
 paraStyle.headIndent = _useCouponLabel.font.pointSize * 7.4;
 NSAttributedString *attrText;
```

Q:iOS 9 'Application tried to present modally an active controller <BIPhotoViewController: 0x7f9cf40602a0>.'


Q:tableview cell初始化方式dequeueReusableCellWithIdentifier和alloc的区别

Q:适配iPhone X Push过程中TabBar位置上移

http://blog.csdn.net/xuyang844175181/article/details/78134552

Q: 两者的区别？
Different:In a UIViewController, title and navigationItem.title are different. One example: if you have a view controller (in a NavigationController) in a UITabBarController, then if you set self.title it overrides the name of the tab as well as the top title. If you set self.navigationItem.title then it only changes the top title, leaving the tab bar name unchanged.
```
self.title = @"新动态";
self.navigationItem.title = @"新动态";
```

Q:九宫格算行数？

Q:NSURLConnection finished with error - code -1002

Q: EXC_BAD_ACCESS (code=EXC_I386_GPFLT).
The process has been returned to the state before expression evaluation
