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

### 正确步骤：
```
git init //初始化仓库

git add .(文件name) //添加文件到本地仓库

git commit -m “first commit” //添加文件描述信息

git remote add origin + 远程仓库地址 //链接远程仓库，创建主分支

git pull origin master // 把本地仓库的变化连接到远程仓库主分支

git push -u origin master //把本地仓库的文件推送到远程仓库
```
### 如果两人同时修改了同一部分的源代码，push 时就很容易发生冲突。所以多名开发者在同一个分支中进行作业时，为减少冲突情况的发生，建议更频繁地进行 push 和 pull 操作。

### demo bash2
```
package main

import (
	"fmt"
	"os/exec"
)

func main() {
	var (
		cmd    *exec.Cmd
		output []byte
		err    error
	)

	// 生成Cmd
	cmd = exec.Command("C:\\Program Files\\Git\\bin\\bash.exe", "-c", "ls")

	// 执行了命令, 捕获了子进程的输出( pipe )
	if output, err = cmd.CombinedOutput(); err != nil {
		fmt.Println(err)
		return
	}

	// 打印子进程的输出
	fmt.Println(string(output))
}
```
### demo bash3

```
package main

import (
	"os/exec"
	"context"
	"time"
	"fmt"
)

type result struct {
	err error
	output []byte
}

func main() {
	//  执行1个cmd, 让它在一个协程里去执行, 让它执行2秒: sleep 2; echo hello;
	// 1秒的时候, 我们杀死cmd
	var (
		ctx context.Context
		cancelFunc context.CancelFunc
		cmd *exec.Cmd
		resultChan chan *result
		res *result
	)

	// 创建了一个结果队列
	resultChan = make(chan *result, 1000)

	// context:   chan byte
	// cancelFunc:  close(chan byte)

	ctx, cancelFunc = context.WithCancel(context.TODO())

	go func() {
		var (
			output []byte
			err error
		)
		cmd = exec.CommandContext(ctx, "C:\\Program Files\\Git\\bin\\bash.exe", "-c", "sleep 2;echo hello;")

		// 执行任务, 捕获输出
		output, err = cmd.CombinedOutput()

		// 把任务输出结果, 传给main协程
		resultChan <- &result{
			err: err,
			output: output,
		}
	}()

	// 继续往下走
	time.Sleep(1 * time.Second)

	// 取消上下文
	cancelFunc()

	// 在main协程里, 等待子协程的退出，并打印任务执行结果
	res = <- resultChan

	// 打印任务执行结果
	fmt.Println(res.err, string(res.output))
}

```
