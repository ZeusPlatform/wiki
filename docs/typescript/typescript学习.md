## 安装和编译
```
npm install -g typescript

tsc helloworld.ts
```

初始化
tsc --init


## 配置vscode
1. 创建 tsconfig.json 文件 tsc 
2. 点击菜单 任务-运行任务 点击 tsc:监视-tsconfig.json 然后就可以自动生成代码了

简单的配置
```json
{
    "compilerOptions": {
        "outDir": "./dist",
        "declaration": true,
        "target": "es6",
        "outFile": "./index.js", // 输出到一个文件中 
        "sourceMap": true,
        "module": "commonjs",
        "moduleResolution": "node",
        "strict": true,
        "lib": [
            "es2015",
        ],
        "typeRoots": [
            "./node_modules/@types/"
        ]
    },
    "include": [
        "./src/**/*"
    ],
    "exclude": [
        "node_modules"
    ]
}
```


## typeScript中的数据类型

typescript中为了使编写的代码更规范，更有利于维护，增加了类型校验，在typescript中主要给我们提供了以下数据类型


    布尔类型（boolean）
    数字类型（number） 
    字符串类型(string)
    数组类型（array）
    元组类型（tuple）
    枚举类型（enum）
    任意类型（any）
    null 和 undefined
    void类型
    never类型

## Promise.resolve 类型定义
```ts
<Promise<string>>Promise.resolve('') 
Promise.resolve('') as as Promise<string>
promise.resolve<string>('code')
```

## 