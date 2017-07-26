## 项目记录

### 搭建pch文件
* [iOS开发之Xcode8下新建pch文件](http://www.jianshu.com/p/337b92c28a86)

### Question
* [iOS导航控制器push/pop出现黑色阴影问题](http://www.jianshu.com/p/6e75a5fa9760)
* 生成APPicon1024*1024 [AppIcon](https://github.com/Nonchalant/AppIcon)

### 导航栏

#### 修改导航栏颜色
```
navigationBar.barTintColor = UIColor.colorWithHexString("5bc4e7")
```

#### 隐藏导航栏下1px黑线     [Link](http://blog.it985.com/9808.html)
```
var navigationBarBottomLine = UIImageView()
    
override func viewDidLoad() {
        super.viewDidLoad()
        navigationBarBottomLine = findNavigationBarBottomLine(view: navigationController?.navigationBar)!
    }
override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        navigationBarBottomLine.isHidden = true
    }
    
    override func viewWillDisappear(_ animated: Bool) {
        super.viewWillDisappear(animated)
        navigationBarBottomLine.isHidden = false
    }
func findNavigationBarBottomLine(view: UIView?) -> UIImageView? {
    if view is UIImageView && (view?.bounds.size.height)! <= 1.0 {
        return view as? UIImageView
    }
    
    for subView in (view?.subviews)! {
        let imageView = findNavigationBarBottomLine(view: subView)
        if imageView != nil {
            return imageView
        }
    }
    return nil
}
```

* 修改navigationBar title颜色
[Link](http://stackoverflow.com/questions/24402000/uinavigationbar-text-color-in-swift)
```
navigationBar.titleTextAttributes = [NSForegroundColorAttributeName : UIColor.white]
```

* 修改navigationitem的返回按钮 [Line](http://www.jianshu.com/p/457c80cbb487)
```
viewController.navigationItem.backBarButtonItem = UIBarButtonItem(title: " ", style: .done, target: nil, action: nil)
            viewController.navigationItem.leftBarButtonItem = UIBarButtonItem(image: #imageLiteral(resourceName: "back"), style: .done, target: self, action: #selector(back))

```


* tintColor/barTintColor
## UIButton
* 取消高亮
[Link](http://www.cnblogs.com/tinych/p/6520593.html)
```
objc可以用通过重写setHighlighted方法来达到当按钮选中时的高亮状态

-(void)setHighlighted:(BOOL)highlighted{
}
swift中取消高亮状态

    override var isHighlighted: Bool {
        set{
            
        }
        get {
            return false
        }
    }
```

* popToViewController 的使用 [Link](http://blog.csdn.net/C_calary/article/details/52968745)
```
for vc in (navigationController?.viewControllers)! {
            if vc is YourVC {
                navigationController?.popToViewController(vc, animated: true)
            }
        }
```

* 设置button title和image的位置 [link](http://www.hangge.com/blog/cache/detail_960.html)
* 隐藏navigationItem返回按钮
```
navigationItem.hidesBackButton = true
```
* 设置button某个圆角 [Link](http://www.jianshu.com/p/4c6efff3f3d7)
```
CAShapeLayer *shapeLayer = [CAShapeLayer layer];
shapeLayer.path = [UIBezierPath bezierPathWithRoundedRect:CGRectMake(0, 0, 100, 100) byRoundingCorners:UIRectCornerBottomLeft | UIRectCornerBottomRight cornerRadii:CGSizeMake(6, 6)].CGPath;
btn.layer.mask = shapeLayer;
```

## UITableView

* 取消tableview顶部空白
```
self.automaticallyAdjustsScrollViewInsets = false
```
* [Link](https://github.com/Lucifer0103/LinkageMenu)
* [Link](http://www.jianshu.com/p/180b1e2bcf7b)

* 设置section间距     [Link](http://blog.csdn.net/gx_wqm/article/details/51866356)

```
tableView.sectionHeaderHeight = 5
tableView.sectionFooterHeight = 5
```

* 重写cell frame

```
override var frame: CGRect {
        didSet {
            var newFrame = frame
            newFrame.size.height -= 10
            super.frame = newFrame
        }
    }
```

* cell 中model赋值
```
var model:MineWLCollectionModel! {
        didSet {
            userNameLabel.text = model.wlUserName
            timeLabel.text = model.wlTime
            personNumLabel.text = model.wlpersons
        }
    }
```

* 隐藏tableview多余cell
```
self.tableView.tableFooterView = [[UIView alloc] initWithFrame:CGRectZero];
```

* tableview section不置顶 [Link](http://blog.csdn.net/csdn2314/article/details/50478052)
* tableview cell 自适应高度 ---手动调用  layoutsubviews
* IndexSet [Link](https://stackoverflow.com/questions/37977404/create-nsindexset-from-integer-array-in-swift)
* reload row section
```
    tableView.beginUpdates()
    tableView.reloadSections(section, with: .automatic)
    tableView.endUpdates()
```

* `does not contain bitcode. You must rebuild it with bitcode enabled (Xcode setting ENABLE_BITCODE), obtain an updated library from the vendor, or disable bitcode for this target. for architecture arm64`  [Link](http://www.cocoachina.com/ios/20150818/13078.html)

## 展示word格式文档

* [Link](https://github.com/zhengwenming/OpenFile)
* webView 适配手机屏幕大小
```
webView.scalesPageToFit = true
```

## 绘制画布

## 录屏

## enumerateObjectsUsingBlock
[enumerateObjectsUsingBlock in swift](http://stackoverflow.com/questions/24120115/enumerateobjectsusingblock-in-swift)

## 手势
```
iOS开发中手势识别有六种：
轻击手势（TapGestureRecognizer）,
轻扫手势 （SwipeGestureRecognizer）,
长按手势（LongPressGestureRecognizer）,
拖动手势（PanGestureRecognizer）,
捏合手势（PinchGestureRecognizer）,
旋转手势（RotationGestureRecognizer）
```

* [iOS图标问题](http://liumh.com/2015/10/21/ios-image-related-matching/)
* [iOS GestureRecognizer](http://www.open-open.com/lib/view/open1435284827732.html)
* [限制UItextfield位数 in swift](http://stackoverflow.com/questions/31363216/set-the-maximum-character-length-of-a-uitextfield-in-swift)

```
func textField(_ textField: UITextField, shouldChangeCharactersIn range: NSRange, replacementString string: String) -> Bool {
        let maxLength = 11
        let currentString: NSString = textField.text! as NSString
        let newString: NSString =
            currentString.replacingCharacters(in: range, with: string) as NSString
        return newString.length <= maxLength
    }
```

* block 反向传值 [Link](http://www.jianshu.com/p/ac77c3416c59)
```
1. 在B中声明一个block
  typealias TestBlock = (String)->()
2. 持有一个block变量
  var blo: TestBlock?  
3. 调用
  self.blo?("It is block test")
4. 在`A`中需要接受值的地方
 let b = B()
 b.blo = {str in 
    print("test block---\\(str)")
 }
```

### TabBar

* 自定义Tabbar重叠问题 [Link](http://www.jianshu.com/p/ed9dcf87086f)
```
public func navigationController(_ navigationController: UINavigationController, willShow viewController: UIViewController, animated: Bool) {
        for tabBar in (tabBarController?.tabBar.subviews)! {
            if tabBar.isKind(of: NSClassFromString("UITabBarButton")!) {
                tabBar.removeFromSuperview()
            }
        }
    }
```

*  创建桥接文件 [Link](http://blog.csdn.net/kangli_1990/article/details/51718459)
*  swift中的MBProgressHUD [Link](http://www.jianshu.com/p/cd81bcdef64f)

### UILabel
* 居上对齐

### 上传图片
* [Data to UIImage](http://stackoverflow.com/questions/29415808/how-to-convert-a-nsdata-object-to-a-uiimage-using-swift)
* [String to URL](http://stackoverflow.com/questions/28514622/convert-string-to-nsurl-is-return-nil-in-swift)
* [Ala 上传图片加参数](http://stackoverflow.com/questions/26121827/uploading-file-with-parameters-using-alamofire?rq=1)
* [Swift - PHP](http://www.jianshu.com/p/cdbad52fd340)
* 图片压缩
* [UIImage] 圆角(http://www.jianshu.com/p/e97348f42276)

### Array
* 删除指定对象
```
var array = ["mac","iPhone","iPad"]
array = array.filter() { $0 != "mac" }
print(array) // will print ["iPhone", "iPad"]
```


* dyld: Library not loaded [Link](https://segmentfault.com/a/1190000000657902)
`把相应的framework由require改为optional`

* 获取本地视频  `picker.mediaTypes = [kUTTypeMovie as String]`
 1. [http://www.hangge.com/blog/cache/detail_1192.html] 2.[https://stackoverflow.com/questions/24262990/how-to-capture-camera-with-uiimagepickercontroller-in-swift]
* throw (使用都do-catch)
```
do {
        let videoData = try Data.init(contentsOf: URL(string: videoPath)!)
        multipartFormData.append(videoData, withName: "mrecord")
    } catch {
        print(error)
            }
```

* swift 视频格式转换
```
/**mov转mp4格式*/
    func convertMovSourceURL(sourceURL: URL) {
        let avAsset = AVURLAsset(url: sourceURL)
        let compatiblePresets = AVAssetExportSession.exportPresets(compatibleWith: avAsset)
        if compatiblePresets.contains(AVAssetExportPresetHighestQuality) {
            let exportSession = AVAssetExportSession(asset: avAsset, presetName: AVAssetExportPresetHighestQuality)
            let formater = DateFormatter()
            formater.dateFormat = "yyyyMMddHHmmss"
            let resultPath = NSSearchPathForDirectoriesInDomains(.libraryDirectory, .userDomainMask, true)[0].appendingFormat("/output-%@.mp4", formater.string(from: Date()))
            
            exportSession?.outputURL = URL(fileURLWithPath: resultPath)
            exportSession?.outputFileType = AVFileTypeMPEG4
            exportSession?.shouldOptimizeForNetworkUse = true
            exportSession?.exportAsynchronously(completionHandler: { 
                switch exportSession!.status {
                case AVAssetExportSessionStatus.cancelled:
                    print("cancel")
                case AVAssetExportSessionStatus.unknown:
                    print("unknown")
                case AVAssetExportSessionStatus.waiting:
                    print("waiting")
                case AVAssetExportSessionStatus.exporting:
                    print("exporting")
                case AVAssetExportSessionStatus.completed:
                    print("dd")
                default:
                    print("failed")
                }
            })
            
        }
    }
```

* cell 背景色 [Link](http://blog.csdn.net/hopedark/article/details/40895505)
* UIPickview 修改字体 [Link](http://blog.csdn.net/tianyou_code/article/details/53231650)
* 多个按钮单选
* Label 富文本
```
let str = NSMutableAttributedString(string: explainLabel.text!)
        str.addAttribute(NSForegroundColorAttributeName, value: systemThemeColor, range: NSMakeRange(0, 5))
        explainLabel.attributedText = str
```
* 饼状图 - PNCharts
* Convert String to CGFloat in Swift[Link](https://stackoverflow.com/questions/27595799/convert-string-to-cgfloat-in-swift)

#  短秀
* UISearchBar [Link](http://www.jianshu.com/p/57ba04b7e389
* )
* TableView section
* `self.automaticallyAdjustsScrollViewInsets = NO;`
* afn Request failed: unacceptable content-type: text/html
```
对应到自己的项目里面，我用的是AFNetworking这套网络请求包，需要改的是：
AFURLResponseSerialization.m文件
223行：
添加 @"text/html"
self.acceptableContentTypes = [NSSetsetWithObjects:@"application/json", @"text/html",@"text/json",@"text/JavaScript", nil];
```
* .ds_store 文件
* git 忽略文件
* 视频播放框架[ZFPlayer](https://github.com/renzifeng/ZFPlayer)
* 刷新某一个section [Link](http://blog.csdn.net/sophia_xiaoma/article/details/50475081)
```
NSIndexSet *indexSet = [[NSIndexSet alloc] initWithIndex:1];
        [self.tableView reloadSections:indexSet withRowAnimation:UITableViewRowAnimationAutomatic];
```

* button user sdwebimage [button user sdwebimage](https://stackoverflow.com/questions/36277472/set-image-from-sdwebimage-to-background-of-button)
* [获取当前跟视图](http://www.jianshu.com/p/949fd3dd720b)
* tableview滑动至顶部 `[tableView setContentOffset:CGPointMake(0, -64) animated:NO];`
* 删除代码块 [sk](https://stackoverflow.com/questions/5923513/delete-a-user-code-snippet-in-xcode)
* 设置button位置 [Link](https://github.com/Phelthas/Demo_ButtonImageTitleEdgeInsets)
* 设置UITextView [Link](https://cnbin.github.io/blog/2015/10/13/ios-zhong-uitextview-yu-dao-de-wen-ti-zong-jie/)
* image 处理[Link](https://github.com/lisongrc/UIImage-Categories) [Link2](http://blog.wangruofeng007.com/blog/2016/01/13/you-ya-chu-li-uiimagetu-pian-xuan-zhuan/)
* 设置cell左划删除

```
- (BOOL)tableView:(UITableView *)tableView canEditRowAtIndexPath:(NSIndexPath *)indexPath {
    return YES;
}

- (UITableViewCellEditingStyle)tableView:(UITableView *)tableView editingStyleForRowAtIndexPath:(NSIndexPath *)indexPath{
    return UITableViewCellEditingStyleDelete;
}

- (NSString *)tableView:(UITableView *)tableView titleForDeleteConfirmationButtonForRowAtIndexPath:(NSIndexPath *)indexPath {//修改删除button title
    return  @"删除";
}

- (void)tableView:(UITableView *)tableView commitEditingStyle:(UITableViewCellEditingStyle)editingStyle forRowAtIndexPath:(NSIndexPath *)indexPath {
    if (editingStyle ==UITableViewCellEditingStyleDelete) {//如果编辑样式为删除样式
        [self callDeleteActivityAPIWithActivityModel:_dataArray[indexPath.row]];
    }
}
```

* Launch Image [Set](http://www.jianshu.com/p/2e6756c4c7be)   [size](http://www.jianshu.com/p/8242b501b223)

[Link](http://blog.csdn.net/riven_wn/article/details/49275157)
* Launch Image 模拟器显示，真机不显示 

```
LaunchImage 在模拟器上显示但在真机上不显示,可能是给你图片的人直接把jpg文件改后缀为png然后给你了，但本质上它还是一张jpg图片，真机根据你给的png信息无法解析，解决办法是，再找美工要一张真的的png图片，要不就把图片后缀改为jpg，然后自己用ps改格式。
```
