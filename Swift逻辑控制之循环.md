## Swift逻辑控制之循环

### for in循环结构
　　计算 `[ -99 , 99 ]` 相乘，如 `-99 * -99` 或 `-98 * -98` 。
```
for i in -99 ... 99 {
    i*i
}
```
#### 计算 2 的 10 次方
```
var result = 1
var base = 2
var power = 10
for _ in 1...power {
    result *= base
}
result // 1024
```


































