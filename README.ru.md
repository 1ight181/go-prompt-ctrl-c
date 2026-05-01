[Английская версия](README.ru.md)

Это форк **[go-prompt](https://github.com/elk-language/go-prompt)**. В оригинальной библиотеке была проблема, которая была унаследована и другими форками - отсутствие возможности контролировать обработку сигналов прерывания. Этот форк решает эту задачу, добавляя дополнительную опцию `WithInterruptCallback` для передачи кастомного обработчика в конструктор `go-promt`. 

Подойдет, если вы используете REPL как один из модулей программы, после завершение которого должно произойти еще что-то. Например, освобождение ресурсов, переход в другое состояние, смена типа интерфейса. 

## Поддерживаемые сигналы

- `SIGINT`
- `SIGTERM`
- `SIGQUIT`

## Пример использования

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
  
// Кастомная обработка Ctrl+C  
func interruptCallback(code int) {  
	fmt.Println("\nCtrl+C pressed, but we handle it ourselves")  
	// os.Exit(code) // поведение по умолчанию 
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
## Сообщество 

Email: [danil.odinzov181@gmail.com](mailto:danil.odinzov181@gmail.com)