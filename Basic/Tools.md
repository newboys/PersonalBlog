### Tools

#### git
* [git document](https://git-scm.com/book/zh/v2)
* 
#### Iterm
* [shortcut key](https://cnbin.github.io/blog/2015/06/20/iterm2-kuai-jie-jian-da-quan/)

#### autojump

### Cocoapods
* [Cocoapods install](http://www.jianshu.com/p/00107eb5449b)

#### Install error 
* pod setup :error `RPC failed; curl 56 SSLRead() return error -36| 17.00 KiB/s`

解决:

```
cd ~/.cocoapods/repos
git clone https://github.com/CocoaPods/Specs.git master
```
参考 : [CocoaPods安装和使用图解](http://www.jianshu.com/p/06e6b7670a91)

### VSCode
修改快捷键
command + k + s 调出此窗口
```
[
  { "key": "cmd+1",                "command": "workbench.action.openEditorAtIndex1" },
  { "key": "cmd+2",                "command": "workbench.action.openEditorAtIndex2" },
  { "key": "cmd+3",                "command": "workbench.action.openEditorAtIndex3" },
  { "key": "cmd+4",                "command": "workbench.action.openEditorAtIndex4" },
  { "key": "cmd+5",                "command": "workbench.action.openEditorAtIndex5" },
  { "key": "cmd+6",                "command": "workbench.action.openEditorAtIndex6" },
  { "key": "cmd+7",                "command": "workbench.action.openEditorAtIndex7" },
  { "key": "cmd+8",                "command": "workbench.action.openEditorAtIndex8" },
  { "key": "cmd+9",                "command": "workbench.action.openEditorAtIndex9" }  
]
```

#### 插件
* 在插件安装的框中输入`shell`，即可在终端使用`code .`打开文件
* command k + command r :显示vscode官方快捷键