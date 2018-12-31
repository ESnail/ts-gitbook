# Typescript 介绍、安装、编译
 
> 中文网：[https://www.tslang.cn/](https://www.tslang.cn/)
> 
> 官网：[http://www.typescriptlang.org/](http://www.typescriptlang.org/)

## 一、 Typescript  介绍

1. TypeScript 是由微软开发的一款开源的编程语言。
2. TypeScript 是 Javascript 的超集，遵循最新的 ES6、Es5 规范。TypeScript 扩展了 JavaScript 的语法。
3. TypeScript 更像后端 java、C# 这样的面向对象语言，可以让 js 开发大型企业项目。
4. 谷歌也在大力支持 Typescript 的推广，谷歌的 angular2.x+ 就是基于 Typescript 语法。
5. 最新的 Vue 、React 也可以集成 TypeScript。

## 二、 Typescript 安装及编译

1. 全局安装，前提是安装了 node。
```
npm install -g typescript
```
2. 编译
    - 书写一个 `.ts` 文件，比如：test.ts，内容如下：
    ```
    let str:string = 'test';
    ```
    - `tsc test.ts` 
    - 默认会在和 test.ts 同级目录下生成一个同名的 `.js` 文件。而这个 .js 文件是编译生成的 ES5 语法的 js 文件。

## 三、 Typescript 开发工具语法高亮、校验、自动编译

使用开发工具，对编写的 TypeScript 代码能进行语法高亮(便于阅读)、语法校验(减少错误)、保存后立即编译，提高开发效率节省工作量。能用工具做的事，就不要浪费人力。

- vscode 编辑器
    -  `tsc --init`，生成配置文件 tsconfig.json。可修改 "outDir": "./js"，指定编译后的文件放置目录。
    - 任务 --> 运行任务，监视 tsconfig.json
    - 默认带语法高亮及语法校验

- sublime 编辑器v
    - 快捷键 `ctrl + shift + p`，调出命令窗口
    - 输入 `paci`，找到 Package Control install
    - 输入 `Typescript`，语法高亮、语法校验
    -  `tsc --init`，生成配置文件 tsconfig.json。可修改 "outDir": "./
    - 输入 `TypescriptCompletion`，自动编译
