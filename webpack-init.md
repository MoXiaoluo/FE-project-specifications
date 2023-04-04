# 通过 webpack 创建 react 工程化项目

1. 使用 webpack 脚手架初始化项目

```
npx webpack init
```

命令执行后会安装 webpack,webpack-cli, 项目初始化会通过一系列问题来完成。
初始化完成后使用 yarn serve 或者 npm run serve 来打开项目 2. 添加 react 相关配置
安装 react,react-dom 为开发依赖

```
yarn add react react-dom
```

安装完成后添加 react 组件 3. 相关问题解决
Babel 解析 react 语法失败

```
npm install --save-dev @babel/preset-react
yarn add -D @babel/preset-react

{
  "plugins": [
    "@babel/syntax-dynamic-import",
    "@babel/plugin-syntax-jsx",
    "@babel/plugin-transform-react-jsx",
    "@babel/plugin-transform-react-display-name"
  ],
  "presets": [
    [
      "@babel/preset-env",
      {
        "modules": false
      },
      "@babel/preset-react"
    ]
  ]
}
```

加载组件时忽略 jsx 后缀报错

```
resolve: {
  extensions: ['.jsx','.js', '.json',],
},
```

# webpack 的特点以及优势

1. 什么是 webpack？
   本质上，webpack 是一个用于现代 JavaScript 应用程序的 静态模块打包工具。当 webpack 处理应用程序时，它会在内部从一个或多个入口点构建一个 依赖图(dependency graph)，然后将你项目中所需的每一个模块组合成一个或多个 bundles，它们均为静态资源，用于展示你的内容。
   webpack 是基于 node 的工具, 本质上 webpack 只能识别 js 和 json 文件, 并且 webpack 本身的功能也只是统一导入导出的方法，更加强大的是 loader 和 plugin.
2. 特点及优点

- webpack 的可配置度特别高，基本上都是通过配置项完成。
- webpack 的 loader 主要是用来转换文件资源,转成 webpack 可以识别的资源
- plugin 是 webpack 中核心环节, 可以实现 css 的提取,文件的压缩，以及分离相同的代码.

3. 缺点

- 当项目内的 js 文件增长到一定数量时，webpack 的打包会非常慢。
