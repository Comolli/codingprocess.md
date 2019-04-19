# go & bash demo1

```
package main

import (
	"fmt"
	"os/exec"
)

func main() {
	var (
		cmd *exec.Cmd
		err error
	)

	// cmd = exec.Command("/bin/bash", "-c", "echo 1;echo2;")

	cmd = exec.Command("C:\\Program Files\\Git\\bin\\bash.exe", "-c", "echo 1")

	err = cmd.Run()

	fmt.Println(err)
}
```
### Git
```
or create a new repository on the command line
echo "# hg" >> README.md
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/Comolli/hg.git
git push -u origin master

```
or push an existing repository from the command line
git remote add origin https://github.com/Comolli/hg.git
git push -u origin master ```

### ***解决git push远程仓库 时 Updates were rejected because the remote contains work that you do问题***

### 一般git 提交的步骤：
```
git init //初始化仓库

git add .(文件name) //添加文件到本地仓库

git commit -m “first commit” //添加文件描述信息

git remote add origin + 远程仓库地址 //链接远程仓库，创建主分支

git push -u origin master //把本地仓库的文件推送到远程仓库
```

###正确步骤：
```
git init //初始化仓库

git add .(文件name) //添加文件到本地仓库

git commit -m “first commit” //添加文件描述信息

git remote add origin + 远程仓库地址 //链接远程仓库，创建主分支

git pull origin master // 把本地仓库的变化连接到远程仓库主分支

git push -u origin master //把本地仓库的文件推送到远程仓库
```
### 如果两人同时修改了同一部分的源代码，push 时就很容易发生冲突。所以多名开发者在同一个分支中进行作业时，为减少冲突情况的发生，建议更频繁地进行 push 和 pull 操作。



