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

## 之前是使用https clone下来的项目改成ssh 设置git源地址
修改 ./git 目录下的 config文件
cd .git && vim config
修改其中url 为 git@XXXX

使用命令行 
git remote set-url origin git@github.com:AccountName/Project-name.git

## 添加与提交
git add < filename >
git add *

git commit -m "代码提交信息"

## 推送
在 .git/config 声明 remote，使用git-remote或者git-config或者手动修改，使用git push 的时候没有指定remote，如果省略将会默认使用配置文件中的remote
> [Named remote in configuration file
You can choose to provide the name of a remote which you had previously configured using git-remote[1], git-config[1] or even by a manual edit to the $GIT_DIR/config file. The URL of this remote will be used to access the repository. The refspec of this remote will be used by default when you do not provide a refspec on the command line. The entry in the config file would appear like this:](https://www.git-scm.com/docs/git-push#REMOTES)

	[remote "<name>"]
		url = <url>
		pushurl = <pushurl>
		push = <refspec>
		fetch = <refspec>
```
The <pushurl> is used for pushes only. It is optional and defaults to <url>.
```


git push origin master

git remote add origin < server >

这里 origin 是 < server > 的别名，取什么名字都可以，你也可以在 push 时将 < server > 替换为 origin。但为了以后 push 方便，我们第一次一般都会先 remote add。
如果你还没有 git 仓库，可以在 GitHub 等代码托管平台上创建一个空（不要自动生成 README.md）的 repository，然后将代码 push 到远端仓库。

## 新建一个空白分支
git checkout --orphan gh-pages

git rm -rf .

这个时候时无法查看到分支的

在commit 一次之后即可 使用 git branch -a 查看到分支