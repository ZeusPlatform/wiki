## remote
git remote -h


## 获取帮助
参考： https://git-scm.com/book/en/v2/Getting-Started-Getting-Help
```
$ git help <verb>
$ git <verb> --help
$ man git-<verb>
git add -h
```

## tag
### 删除tag
`git tag -d <tag-naem>`

## 修改已commit的版本
`git add <file-name | .>`
`git commit --amend --no-edit`
每个commit内容显示在一行
git log --oneline

## 之前是使用https clone下来的项目改成ssh
修改 ./git 目录下的 config文件
cd .git && vim config
修改其中url 为 git@XXXX

使用命令行 
git remote set-url origin git@github.com:AccountName/Project-name.git
