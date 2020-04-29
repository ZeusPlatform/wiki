## [快速生成gitignore](https://github.com/generate/generate-gitignore#quickstart)
### Quickstart
Install

Install generate and generate-gitignore:

$ npm install --global generate generate-gitignore
Generate a .gitignore

Initiate a prompt to generate a .gitignore file in the current working directory:

$ gen gitignore
Customization

Add a custom template with the same as the .gitignore template you want to use to the ~/templates directory on your system, and this generator will automatically use it.

For example, add a Node.gitignore template to override the .gitignore template that's used when $ gen gitignore:node is run.

## [同步types](https://github.com/jeffijoe/typesync)
npx typesync

## [程序运行调用关系生成njstrace](https://www.npmjs.com/package/njstrace)


## 快速生成表单 https://github.com/dream2023/vue-ele-form-generator https://github.com/JakHuang/form-generator

## 图片懒加载 https://github.com/aFarkas/lazysizes

## 监控代码 supervisor  -i node_modules index.js
npm i supervisor

supervisor -h

## [commander简单使用](https://github.com/tj/commander.js/tree/master#installation)
```js
const { program } = require('commander')
program.version('0.0.1');


program
  .usage("[global options] command")
  .option('-d, --debug', 'output extra debugging')
  .option('-s, --small', 'small pizza size')
  .option('-p, --pizza-type <type>', 'flavour of pizza')
  .command('clone <source> [destination]')
  .description('clone a repository into a newly created directory')
  .action((source, destination) => {
    console.log('clone command called');
  });

program.parse(process.argv);
```

或者
```js
const { Command } = require('commander');
const program = new Command();
program.version('0.0.1');
```


### [promts](https://github.com/terkelg/prompts)
```js
const prompts = require('prompts');

(async () => {
  const response = await prompts({
    type: 'number',
    name: 'value',
    message: 'How old are you?',
    validate: value => value < 18 ? `Nightclub is 18+ only` : true
  });

  console.log(response); // => { value: 24 }
})();
```


### [npm-check-updates](https://www.npmjs.com/package/npm-check-updates)
检查更新npm库

