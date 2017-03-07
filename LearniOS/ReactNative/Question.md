## Question

* 错误描述
`xcrun: error: unable to find utility "instruments", not a developer   
tool or in PATH`
[解决](http://stackoverflow.com/questions/39778607/error-running-react-native-app-from-terminal-ios)
* error: 

```
`Yoga (= 0.42.0.React)` required by `React/Core (0.42.0)`
None of your spec sources contain a spec satisfying the dependency: `Yoga (= 0.42.0.React)`.
````

修改podfile文件如下:

```
# In Podfile
react_native_path = "node_modules/react-native"
pod "React", :path => react_native_path
pod "Yoga", :path => "#{react_native_path}/ReactCommon/yoga"
```
[解决](https://github.com/facebook/react-native/issues/12670)