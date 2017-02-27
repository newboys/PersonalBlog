## Network

### URLSession/NSURLSession

#### 创建GET请求

```
    let userTel = "13231852031"
    let userPassword = "123456"
    let defaultConfiguration = URLSessionConfiguration.default
    let sessionWithoutADelegate = URLSession(configuration: defaultConfiguration)
    if let url = URL(string: "http://127.0.0.1:8080/v1/login?usertel=\(userTel)&userpassword=\(userPassword)") {
        (sessionWithoutADelegate.dataTask(with: url) { (data, response, error) in
            if let error = error {
                print("Error: \(error)")
            } else if let response = response,
                let data = data,
                let string = String(data: data, encoding: .utf8) {
                print("Response: \(response)")
                print("DATA:\n\(string)\nEND DATA\n")
            }
        }).resume()
    }
```

#### 创建POST请求

```
    let defaultConfiguration = URLSessionConfiguration.default
    let sessionWithoutADelegate = URLSession(configuration: defaultConfiguration)
    let paramer: [String: String] = ["userTel":"13231852031","userPassword":"123456"]
    
    if let url = URL(string: "http://127.0.0.1:8080/v1/register") {
        var request = URLRequest.init(url: url)
        request.httpMethod = "POST"
        request.httpBody = try? JSONSerialization.data(withJSONObject: paramer, options: JSONSerialization.WritingOptions.prettyPrinted)
        
        sessionWithoutADelegate.dataTask(with: request, completionHandler: { (data, response, error) in
            if let error = error {
                print("Error:\(error)")
            }else if let response = response,
                let data = data,
                let string = String(data: data,encoding: .utf8){
                print("Response: \(response)\n")
                print("DATA:\(string)\n")
            }
        }).resume()
    }
```

### 根据Alamofire的README读其源码

#### Swift版本和Alamofire版本

* Swift:3.0
* Alamofire:4.4.0

#### Making a Request

```
Alamofire.request("https://httpbin.org/get")
```

首先，文档中给出上面的一个例子，我们可以看到很简单就发送了一个请求。接下来我们可以看一下Alamofire是如何实现的request，通过跳转我们可以看到该方法是实现在Alamofire.swift文件中:

```
@discardableResult
public func request(
    _ url: URLConvertible,
    method: HTTPMethod = .get,
    parameters: Parameters? = nil,
    encoding: ParameterEncoding = URLEncoding.default,
    headers: HTTPHeaders? = nil)
    -> DataRequest
{
    return SessionManager.default.request(
        url,
        method: method,
        parameters: parameters,
        encoding: encoding,
        headers: headers
    )
}
```

首先该方法通过`URLConvertible`协议来判断URL的有效性(如未无效URL会抛出Error)，然后方法默认为GET，parameters参数默认为空，参数编码默认为URLEncoding.default，header默认为空。在该方法中又调用了`SessionManager`，接下来我们再跳转到SessionManager，在SessionManager中的request方法实现如下(由于方法较长下面代码只贴关键部分):

```

    do {
        originalRequest = try URLRequest(url: url, method: method, headers: headers)
        let encodedURLRequest = try encoding.encode(originalRequest!, with: parameters)
        return request(encodedURLRequest)
    } catch {
        return request(originalRequest, failedWith: error)
    }

```

在上述实现中
```
    do {
        originalRequest = try urlRequest.asURLRequest()
        let originalTask = DataRequest.Requestable(urlRequest: originalRequest!)
        let task = try originalTask.task(session: session, adapter: adapter, queue: queue)
        let request = DataRequest(session: session, requestTask: .data(originalTask, task))
        delegate[task] = request
        if startRequestsImmediately { request.resume() }
        return request
    } catch {
        return request(originalRequest, failedWith: error)
    }
```









#### 代码中的关键字解释
* `@discardableResult`:此关键字表示修饰的方法不必接受返回值Swift 3.0 中方法的返回值必须有接收否则会报警告，当然其实主要目的是为了避免开发人员忘记接收返回值的情况，但是有些情况下确实不需要使用返回值可以使用"_"接收来忽略返回值。当然你也可以增加@discardableResult声明，告诉编译器此方法可以不用接收返回值
* `open`:open 一个元素在其他module中还是可以被override
* `static`:在方法的func关键字之前加上关键字static或者class都可以用于指定类方法.不同的是用class关键字指定的类方法可以被子类重写
* `@escaping`



### 参考
* [GET/Post Request](http://ios.jobbole.com/85378/)
* [Apple Document](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/URLLoadingSystem/CookiesandCustomProtocols/CookiesandCustomProtocols.html#//apple_ref/doc/uid/10000165i-CH10-SW3)
* [译-URL-Session编程指南](http://www.wenghengcong.com/2016/09/%E8%AF%91-URL-Session%E7%BC%96%E7%A8%8B%E6%8C%87%E5%8D%97/)
* [iOS开发系列--Swift 3.0](http://www.cnblogs.com/kenshincui/p/5594951.html)
* [Swift 3必看：新的访问控制fileprivate和open](http://www.jianshu.com/p/604305a61e57)
* [Swift_关键字static和class的区别](http://www.jianshu.com/p/a9c9e7313438)