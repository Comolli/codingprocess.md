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
