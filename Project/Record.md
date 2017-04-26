## 项目记录

### 搭建pch文件
* [iOS开发之Xcode8下新建pch文件](http://www.jianshu.com/p/337b92c28a86)

### Question
* [iOS导航控制器push/pop出现黑色阴影问题](http://www.jianshu.com/p/6e75a5fa9760)

### 导航栏

#### 修改导航栏颜色
```
navigationBar.barTintColor = UIColor.colorWithHexString("5bc4e7")
```

#### 隐藏导航栏下1px黑线 [Answer](http://blog.it985.com/9808.html)
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

### 重写cell frame

```
override var frame: CGRect {
        didSet {
            var newFrame = frame
            newFrame.size.height -= 10
            super.frame = newFrame
        }
    }
```

### Swift
* Alafire
* Kingfisher