[【无废话30分钟】Lua快速入门教程 - 4K超清](https://www.bilibili.com/video/BV1vf4y1L7Rb)

# 入门

## 运行环境

  - [在线模拟](https://wiki.luatos.com/_static/luatos-emulator/lua.html)

  - 打印

    ```lua
    print("hello world")
    ```

## 变量声明

  ```lua
  local a = 1 -- 局部变量
  b = 2 -- 全局变量
  print(c) -- 没有声明的变量都是nil
  ```

## 多重赋值

  ```lua
  a,b = 1,2
  print(a,b)
  a,b,c = 1,2
  print(c)
  [11:52:10] 1	2
  [11:52:10] nil
  ```

## number

  ```lua
  a = 1 -- a是number类型
  a = 0x11
  b = 2e10
  print(a,b) -- 17	20000000000.0
  print(10^5) -- 支持幂运算
  print(1<<3,102>>1) -- 支持位运算

  [11:56:06] 17	20000000000.0
  [11:56:06] 100000.0
  [11:56:06] 8	51
  ```

## string

```lua
a = "0x\t11" -- 转义字符
b = '2e10'
c = [[
dasd
    asd\tdsa
    asdd
]] -- 多行字符串
d = tostring(10) -- 转换为字符串
n = tonumber("abc") -- 转换为数字,如果无法转换则返回nil

print(a, #a, b) -- #a返回字符串长度
print(c)
print(d, n)

[01:45:49] 0x	11	5	2e10
[01:45:49] dasd
    asd\tdsa
    asdd

[01:45:49] 10	nil
```
```lua
s = string.char(0x30, 0x00, 0x31, 0x32) -- 生成字符串
n = string.byte(s, 2) -- 返回字符串的字节值
print(s, #s, n)

[11:40:18] 012	4	0
```


## function

  ```lua
  function f(a, b, c) -- 函数声明
      print(a, b, c)
  end
  f(1, 2) -- 如果参数不够,则多余的参数为nil

  [01:56:51] 1	2	nil

  function f(a, b, c)
    return a, b
  end
  local i, j = f(1, 2) -- 多重赋值
  print(i, j)

  [01:58:37] 1	2
  ```
## table

  ```lua
  a = {1, "ac", {}, function() end}
  print(a[5]) -- 下标从1开始，如果没有则返回nil
  a[5] = 123
  table.insert(a,"d")
  table.insert(a, 2, "2")
  local s = table.remove(a, 2) -- 删除元素，返回删除的元素
  print(#a, a[2], s)

  [10:04:36] nil
  [10:04:36] 6	ac	2
  ```

### 字符串下标
  ```lua
  a = {
      a = 1,
      b = "1234",
      c = function()

      end,
      [",;"] = 123
  }
  a["abc"] = "abc"
  print(a['a'], a.b, a[",;"], a.abc, a.x)

  [10:11:48] 1	1234	123	abc	nil
  ```

### 全局表G
  ```lua
  a = 1
  print(_G, _G["a"], _G["table"]["insert"])

  [10:17:09] table: 0x3	1	function: 0x153
  ```


## bool
```lua
a = true
b = false -- nil和false为假，其他都为真，0也为真
print(1>2)
print(1<2)
print(1>=2)
print(1<=2)
print(1==2)
print(1~=2) -- 不等于
print(a and b)
print(a or b)
print(not a)

[10:25:00] false
[10:25:00] true
[10:25:00] false
[10:25:00] true
[10:25:00] false
[10:25:00] true
[10:25:00] false
[10:25:00] true
[10:25:00] false
```
```lua
a = nil -- 假
b = 0   -- 真
print(a and b)  -- 若 a 为 true，则返回 b；若a为false，则返回a。
print(a or b)   -- 若 a 为 true，则返回 a，若a为false，则返回 b。
print(not a)   -- 返回bool

print(b > 10 and "yes" or "no")

[11:23:48] nil
[11:23:48] 0
[11:23:48] true
[11:23:48] no
```

## if
```lua
if 1>10 then
    print("1>10")
elseif 1 < 10 then
    print("1<10")
else
    print("no")
end
```

## 循环
- for

  ```lua
  for i=1,10,1 do
      print(i)
      if i == 3 then break end
  end

  for i=10,1,-5 do
      print(i)
  end
  ```
- while

  ```lua
  i = 1
  while i < 10 do
      print(i)
      i = i + 1 -- 没有++和--
  end
  ```
