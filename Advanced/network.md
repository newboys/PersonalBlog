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




### 参考
* [GET/Post Request](http://ios.jobbole.com/85378/)
* [Apple Document](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/URLLoadingSystem/CookiesandCustomProtocols/CookiesandCustomProtocols.html#//apple_ref/doc/uid/10000165i-CH10-SW3)
* [译-URL-Session编程指南](http://www.wenghengcong.com/2016/09/%E8%AF%91-URL-Session%E7%BC%96%E7%A8%8B%E6%8C%87%E5%8D%97/)