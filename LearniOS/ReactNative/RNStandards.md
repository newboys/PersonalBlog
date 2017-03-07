## React-Native Standards
### 项目结构

以下目录结构示例中只展示js与静态资源，不包含原生代码。

```
.
├── index.ios.js
├── index.android.js
└── js
    ├── component           可复用的组件（非完整页面）
    ├── page                完整页面
    ├── config              配置项（常量、接口地址、路由、多语言化等预置数据）
    ├── util                工具类（非UI组件)
    ├── style               全局样式
    └── image               图片
```

在component和page目录中，可能还有一些内聚度较高的模块再建目录

```
page/component
├── HomeView.component.js
├── HomeView.style.js
└── MovieView
    ├── MovieList.component.js          
    ├── MovieList.style.js          
    ├── MovieCell.component.js          
    ├── MovieCell.style.js              
    ├── MovieView.component.js          
    └── MovieView.style.js              
```

### 其他
* 命名采用驼峰

### 参考
* [ReactNative编码规范](https://github.com/cnsnake11/blog/blob/master/ReactNative%E5%BC%80%E5%8F%91%E8%A7%84%E8%8C%83/%E7%BC%96%E7%A0%81%E8%A7%84%E8%8C%83.md)
* [React Native项目结构规范](https://github.com/sunnylqm/react-native-project-structure-guide)