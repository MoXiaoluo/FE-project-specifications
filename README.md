# 为什么需要前端规范

为什么要有前端规范?因为人多不一定就力量大，还有可能一团糟。因此为了提升团队凝聚力，统一团队代码风格，优化团队协作效率，使用来约束同一项目不同程序员的代码风格。

# 规范类型

1. Prettier 代码格式化
2. ESlint
3. Prettier 与 ESlint 的集成
4. Git 提交规范(commitlint)

## [Prettier 代码格式化](https://github.com/prettier/prettier)

1. 什么是 prettier？

2. 安装依赖：

```
yarn add --dev --exact prettier
npm install --save-dev --save-exact prettier
```

3. 创建空的配置文件，让编辑者或者其他工具知道你正在使用 Prettier。

```
echo {}> .prettierrc.json
```

[配置选项参考](https://prettier.io/docs/en/options.html) 4. 创建.prettierignore 文件，让 Prettier CLI 和其他编辑者知道那些文件不需要格式化。

```
echo {}> .prettierignore

# Ignore artifacts:
build
coverage
.git
/node_modules
```

或者在代码中添加注释

```
JS: // prettier-ignore
JSX: {/* prettier-ignore */}
HTML: <!-- prettier-ignore -->
CSS: /* prettier-ignore */
MarkDown: <!-- prettier-ignore -->
```

[其他类型](https://prettier.io/docs/en/ignore.html)

5. 基本配置已经完成，可以通过下面命令格式化代码

```
npx prettier --write options
yarn prettier --write options
```

或者配置在 package.json 中

```
"scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "prettier": "prettier --parser --write ./src/**/*.js"
}
```

6. 在代码提交到缓存区的时候进行代码格式化

```
lint-staged
npx mrm@2 lint-staged
上面命令相当于
npm install --save-dev husky lint-staged\
npx husky install\
npm set-script prepare "husky install"\
npx husky add .husky/pre-commit "npx lint-staged"

package.json增加信息
"scripts": {
  ...
  "prepare": "husky install"
}

"lint-staged": {
  "*.js": "eslint --cache --fix",
  "*.{js,css,md}": "prettier --write"
}

```

[更多配置方式](https://prettier.io/docs/en/precommit.html) 7. 11

## ESlint

1. 什么是 ESlint？
   ESLint 的目标是提供一个插件化的 JavaScript 代码检测工具。代码检查是一种静态的分析，常用于寻找有问题的模式或者代码，并且不依赖于具体的编码风格。JavaScript 是一个动态的弱类型语言，在开发过程中比较容易出错。因为没有编译程序，为了寻找 JavaScript 代码错误通常需要在执行过程中不断调试。
2. 安装 ESlint

```
npm install eslint --save-dev
yarn add eslint -D
```

3. 初始化 ESlint

```
./node_modules/.bin/eslint --init
运行 eslint --init 之后，.eslintrc 文件会在你的文件夹中自动创建。
也可以在直接在package.json中直接配置，这两种方式都是支持的。
{
  "name": "mypackage",
  "version": "0.0.1",
  "eslintConfig": {
  }
}
```

[ESLint 附带有大量的规则](http://eslint.cn/docs/rules/)。你可以使用注释或配置文件修改你项目中要使用的规则。要改变一个规则设置，你必须将规则 ID 设置为下列值之一：

"off" 或 0 - 关闭规则
"warn" 或 1 - 开启规则，使用警告级别的错误：warn (不会导致程序退出)
"error" 或 2 - 开启规则，使用错误级别的错误：error (当被触发的时候，程序会退出)

Environments - 指定脚本的运行环境。每种环境都有一组特定的预定义全局变量。
Globals - 脚本在执行期间访问的额外的全局变量。
Rules - 启用的规则及其各自的错误级别。
plugins - 第三方插件
Extends - 继承
Parser - 解析器，ESLint 默认使用 Espree 作为其解析器。
parserOptions — 常用于设置语法解析器的一些配置。

## [Prettier 与 ESlint 的集成](https://github.com/prettier/eslint-config-prettier)

1. 安装依赖

```
npm install --save-dev eslint-config-prettier
yarn add eslint-config-prettier -D
```

2. 配置
   添加'prettier'到 eslintrc.\* 文件里面去或者在 package.json 里面查找.

```
{
  "extends": [
    "some-other-config-you-use",
    "prettier"
  ]
}
```

## commitlint

- 安装插件

  ```
  # For Windows:
  npm install --save-dev @commitlint/config-conventional @commitlint/cli

  # Configure commitlint to use conventional config
  echo "module.exports = { extends: ['@commitlint/config-conventional'] };" > commitlint.config.js

  添加hook
  npx husky add .husky/commit-msg  'npx --no -- commitlint --edit ${1}'
  ```

  [配置参考](https://commitlint.js.org/#/reference-configuration)

## 辅助工具 commitizen

1. 安装

```
yarn add commitizen -D

npx commitizen init cz-conventional-changelog --save-dev --save-exact
```
