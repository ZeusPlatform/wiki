## webpack-dev-server
### npm script
"dev": "webpack-dev-server --config webpack.config.dev.js"
### dev 配置文件
1. 引入必要的依赖 path, webpack, html-webpack-plugin
2. 入口：entry
3. 出口：{filename,path,library,libraryTarget}
4. devServer {hot,watchOption,contentBase}
5. resolve: 别名
6. module.rules [{test,exclude,loader}]
7. plugins: new webpack.HootModuleReplacementPlugin(), new HtmlWebpackPlugin({template,inject})

### 查看dev-server文件
例子：http://localhost:8081/webpack-dev-server