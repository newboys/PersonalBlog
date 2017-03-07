### Tools

#### git
* [git document](https://git-scm.com/book/zh/v2)

ERROR:
* `error:src refspec master does not match any`
原因: 引起该错误的原因是，目录中没有文件，空目录是不能提交上去的

* `error: failed to push some refs to 'https://github.com/fengzhihao123/test.git'`
原因: github中的README.md文件不在本地代码目录中 pull=fetch+merge
执行: `git pull --rebase origin master`


#### Iterm
* [shortcut key](https://cnbin.github.io/blog/2015/06/20/iterm2-kuai-jie-jian-da-quan/)

#### autojump

### Cocoapods
* [Cocoapods install](http://www.jianshu.com/p/00107eb5449b)
* [pod install vs pod update](https://guides.cocoapods.org/using/pod-install-vs-update.html)
* [忽略特殊文件.gitignore](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013758404317281e54b6f5375640abbb11e67be4cd49e0000)

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