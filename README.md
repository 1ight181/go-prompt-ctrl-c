[Русская версия](README.ru.md)

This is a fork of **[go-prompt](https://github.com/elk-language/go-prompt)**. The original library had a limitation that was inherited by other forks as well — there was no way to control interrupt signal handling. This fork addresses that issue by introducing an additional option, `WithInterruptCallback`, which allows you to pass a custom handler to the `go-prompt` constructor.

It is useful if you use a REPL as a module within a larger program, where additional actions should be performed after the REPL exits. For example, releasing resources, transitioning to another state, or switching the interface type.
## Supported signals

- `SIGINT`
- `SIGTERM`
- `SIGQUIT`
## Usage example

```go
package main

import (
	"fmt"
	"os"

	prompt "github.com/1ight181/go-prompt-ctrl-c"
)

func executor(in string) {
	fmt.Println("input:", in)
}

// Custom Ctrl+C handling
func interruptCallback(code int) {
	fmt.Println("\nCtrl+C pressed, but we handle it ourselves")
	// os.Exit(code) // default behavior
}

func main() {
	p := prompt.New(
		executor,
		nil,
		prompt.OptionPrefix(">>> "),
		prompt.WithInterruptCallback(interruptCallback),
	)

	p.Run()
}
```
## Community

Email: [danil.odinzov181@gmail.com](mailto:danil.odinzov181@gmail.com)