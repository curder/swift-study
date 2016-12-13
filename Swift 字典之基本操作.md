## Swift 字典之基本操作
假如有如下字典变量。
```
var user = ["name":"luo","password":"passwd","occupation":"programmer"]
```

### 修改
```
user["occupation"] = "freelancer"

user.updateValue("password", forKey: "password") // 返回字典修改前的旧值 例如这里返回`passwd`
```
### 添加
```
user["email"] = "curder@foxmail.com"
user.updateValue("webfsd.com", forKey: "website")
```
> 字典不用像数组那样担心会有越界的问题。


### 删除
```
user["website"] = nil
user.removeValue(forKey: "email") // 返回删除掉的旧值

user.removeAll() // 清空字典
```























