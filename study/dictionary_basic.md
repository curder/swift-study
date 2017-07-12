## Swift 字典之基本操作
假如有如下字典变量，下面对如下字典进行基本操作。
```
var user = ["name":"luo","password":"passwd","occupation":"programmer"]
```

### 修改
```
user["occupation"] = "freelancer"

user.updateValue("password", forKey: "password") // 返回字典修改前的旧值 例如这里返回`passwd`

// 简单的解包判断
let oldPassword = user.updateValue("passwd", forKey: "password")
if let oldPassword = oldPassword, let newPassword = user["password"], oldPassword == newPassword {
    print("修改前的密码和修改后的密码一致！")
}
```

### 添加
```
user["email"] = "curder@foxmail.com"
user.updateValue("webfsd.com", forKey: "website")
```
> 字典不用像数组那样担心会有越界的问题。

`updateValue()` 方法如果操作的key在字典中存在则会修改字典对应的value，否则会在字典内新增这个key。

### 删除
```
user["website"] = nil
user.removeValue(forKey: "email") // 返回删除掉的字典的旧值

user.removeAll() // 清空字典
```

### 获取字典中单元个数
```
dict.count
```

### 判断字典是否为空
```
dict.isEmpty
```

### 获取字典的key

```
Array( dict.keys)
```

### 获取字典的value
```
Array(dict.values)
```

### 字典键值的遍历
```
for (key,value) in dict{
    print(key , value)
}
```