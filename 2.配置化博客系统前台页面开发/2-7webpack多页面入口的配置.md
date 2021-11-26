# webpack多页面入口配置
一个工程里面既想有一个前台页面，又想有一个后台管理页面，需要通过webpack配置，把一个单页应用变成多页应用。既有给用户看的展示页面，又有一个给后台管理员看的页面。为了能配置webpack，首先要将隐藏的配置暴露出来。传统使用`npm run eject`，但是eject操作是不可逆的。
1. 打开path.js文件，在module.exports中添加
   ```javascript
   adminHtml: resolveApp('public/admin.html'),
   adminIndexJs: resolveModule(resolveApp, 'src/admin'),
   ```
2. 打开webpack.config.js文件，找到entry入口
   ```javascript
   entry: {
      index: isEnvDevelopment && !shouldUseReactRefresh
        ? [
            webpackDevClientEntry,
            paths.appIndexJs,
          ]
        : paths.appIndexJs,
      admin: isEnvDevelopment && !shouldUseReactRefresh
      ? [
          webpackDevClientEntry,
          paths.adminIndexJs,
        ]
      : paths.adminIndexJs
    },
   ```
3. 对打包出来的文件内容进行区分，修改output中的filename，在bundle.js前面加上`[name]`。比如入口是index.js，那么对应的打包文件就是index.bundle.js，好处是如果只访问前台页面，那么只会加载前台页面对应的index.bundle.js；如果访问的是anmin页面，那么只会加载admin.bundle.js
   ```javascript
   filename: isEnvProduction
        ? 'static/js/[name].[contenthash:8].js'
        : isEnvDevelopment && 'static/js/[name].bundle.js',
   ```

4. 修改`HtmlWebpackPlugin`插件
把js打包完成之后index页面对应的index.js文件插入到index.html模板里面，然后生成一个新的html，放到打包出来的dist目录下面名字叫做index.html这个文件里面。
```javascript
new HtmlWebpackPlugin(
  Object.assign(
    {},
    {
      inject: true,
      chunks: ['index'],
      template: paths.appHtml,
      filename: 'index.html'
    },
    isEnvProduction
      ? {
          minify: {
            removeComments: true,
            collapseWhitespace: true,
            removeRedundantAttributes: true,
            useShortDoctype: true,
            removeEmptyAttributes: true,
            removeStyleLinkTypeAttributes: true,
            keepClosingSlash: true,
            minifyJS: true,
            minifyCSS: true,
            minifyURLs: true,
          },
        }
      : undefined
  )
),
new HtmlWebpackPlugin(
  Object.assign(
    {},
    {
      inject: true,
      chunks: ['admin'],
      template: paths.admainHtml,
      filename: 'admin.html'
    },
    isEnvProduction
      ? {
          minify: {
            removeComments: true,
            collapseWhitespace: true,
            removeRedundantAttributes: true,
            useShortDoctype: true,
            removeEmptyAttributes: true,
            removeStyleLinkTypeAttributes: true,
            keepClosingSlash: true,
            minifyJS: true,
            minifyCSS: true,
            minifyURLs: true,
          },
        }
      : undefined
  )
),
```
5. 删除ManifestPlugin
6. scripts目录下start.js, build.js增加`paths.adminHtml, paths.adminIndexJs`
```javascript
if (!checkRequiredFiles([paths.appHtml, paths.appIndexJs, paths.adminHtml, paths.adminIndexJs])) {
  process.exit(1);
}
```
## 优化
7. 将public目录下admin.html与index.html统一为template.html模板，上述位置也要做出相应修改。