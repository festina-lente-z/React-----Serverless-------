## ref用于父组件从子组件中取数据
父组件中`<PageSetting ref={pageSettingRef}/>`
那么在PageSetting这个组件里就可以接收到一个对应的ref。第一个参数接收到的是`props`,第二个参数接收到外部传入的`ref`参数。
```javascript
const PageSetting = (props, ref) => {
  return (
    <div>PageSetting组件</div>
  )
}
```
> 注意：直接给一个function组件传递ref会报错，因为function component本身自己没有实例。如果要用ref，需要在子组件中再引入一个`forwardRef`，然后在结尾export组件中用`forwardRef`对`PageSetting`进行包裹 -> `export default forwardRef(PageSetting)`

## antd form表单坑
`<Form.Item>`内部诸如`<Input/>`等初始值不是写在`defaultValue`中的，而是写在
```javascript
<Form.Item
  label="请输入页面标题"
  name="title"
  initialValue={title}
>
```

## 配置网页标题
`npm install react-helmet`