[【无废话30分钟】Lua快速入门教程 - 4K超清](https://www.bilibili.com/video/BV1vf4y1L7Rb)

# 入门

+ 运行环境

  + [在线模拟](https://wiki.luatos.com/_static/luatos-emulator/lua.html)

  + 打印

    ```lua
    print("hello world")
    ```

+ 变量声明

  ```lua
  local a = 1 // 局部变量
  b = 2 // 全局变量
  print(c) //没有声明的变量都是nil
  ```

+ 多重赋值

  ```lua
  a,b = 1,2
  print(a,b)
  a,b,c = 1,2
  print(c)
  [11:52:10] 1	2
  [11:52:10] nil
  ```

+ 数值型

  ```lua
  a = 1 // a是number类型
  a = 0x11
  b = 2e10
  print(a,b)
  print(10^5)
  print(1<<3,102>>1)
  [11:56:06] 17	20000000000.0
  [11:56:06] 100000.0
  [11:56:06] 8	51
  ```

