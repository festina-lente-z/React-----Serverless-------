## 文件目录
- store
  - action
  - reducer
    - homeManagement.js
  - index.js

## 步骤
1. 创建一个store目录（创建一个仓库）。store就是redux存储的数据。
2. homeManagement.js中创建协议
3. reducer起两部分作用：一部分告诉我们初始化数据要怎么存储；另一部分告诉我们当我接收到action的时候要怎么去改变数据里的内容
4. reducer内容
   {
     homeManagement: {
       name: 'Page',
       attributes: {},
       children: []
     }
   }
5. 在admin/index.jsx中引入
6. reducer要求每次都返回一个新的state，所以要引入immer。
   