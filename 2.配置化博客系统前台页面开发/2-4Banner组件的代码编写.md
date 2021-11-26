## 箭头函数简写return
如果要返回一个对象，就要注意，如果是单表达式，这么写的话会报错：
```javascript
// SyntaxError:
x => { foo: x }
```
因为和函数体的`{ ... }`有语法冲突，所以要改为：
```javascript
// ok:
x => ({ foo: x })
```
## 步骤
在container目录下创建Home文件夹
在Home文件夹中创建index.jsx(首页的入口文件)，并在其中写Home组件。                                                                          在Home文件夹中创建component文件夹
在component文件夹下面创建Bannner文件夹
在Bannner下创建index.jsx和style.module.scss
## `background-size`用法
`background-size`设置背景图片大小。图片可以保有其原有的尺寸，或者拉伸到新的尺寸，或者在保持其原有比例的同时缩放到元素的可用空间的尺寸。
`background-size: contain;`缩放背景图片以完全装入背景区，可能背景区部分空白。contain 尽可能的缩放背景并保持图像的宽高比例（图像不会被压缩）。该背景图会填充所在的容器。当背景图和容器的大小的不同时，容器的空白区域（上/下或者左/右）会显示由 background-color 设置的背景颜色。
