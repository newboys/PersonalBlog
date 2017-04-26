## RN 基础
### FlexBox
* flexDirection
* alignItems
* justifyContent
* flexWrap

### View

### Text

### Image 


* [REACTNATIVE系列教程之二：创建自定义组件&&导入与使用示例](http://www.qingpingshan.com/rjbc/az/86442.html)
```
module.exports = MyButton;
import MyButton from './MyButton'
```

* [jike](http://wiki.jikexueyuan.com/project/react-native/)
* 获取屏幕的高度和宽度：
```
var dimensions = require('Dimensions');
var {width, height} = dimensions.get('window');
```

### 遇到的问题
* No bundle url present
```
Run "react-native run-ios"
When the error appears, run "npm install"
Then run "react-native run-ios" again.
```
[answer](https://github.com/facebook/react-native/issues/12754)