# interface

- 接口定义：

利用关键字interface来定义一个接口，接口是一组方法的集合。

例如：

	type People interface {
	    Show(name string, age int) (id int, err error)  
	    Set(name string, age int)
	}
	
- 接口的实现：

跟结构体的成员方法实现是一样的。

	func (object of implement func) func_name (parameters) (return type){
	
	    ....//func body
	    
	}
	
例如：

	package main
	
	import "fmt"
	func main() {
	    fmt.Println("=================Live interface===============")
	    var live Live
	    s := &Student{People{"puyangsky", 22, 007}, 0}
	    live = s
	    live.speak("I am happy")
	    live.eat()
	    fmt.Println("================Earn interface================")
	    var earn Earn
	    earn = &Worker{People{"humeiling", 22, 002}, 0}
	    earn.eat()
	    earn.work()
	    earn.getMoney(100)
	    fmt.Println("=====================End======================")
	}
	
	
	type People struct {
	    name string
	    age int32
	    id int32
	}
	
	type Student struct{
	    People
	    grade float32
	}
	
	type Worker struct{
	    People
	    salary float32
	}
	
	type Live interface {
	    eat()
	    speak(something string)
	}
	
	type Earn interface {
	    eat()
	    work()
	    getMoney(money int32)
	}
	
	func (s *Student) eat()  {
	    fmt.Printf("%s is eating...\n", s.name)
	}
	
	func (s *Student) speak(something string) {
	    fmt.Printf("%s is speaking: %s\n", s.name, something)
	}
	
	func (w *Worker) eat()  {
	    fmt.Printf("%s is eating ...\n", w.name)
	}
	
	func (w *Worker) work()  {
	    fmt.Printf("%s is working...\n", w.name)
	}
	
	func (w *Worker) getMoney(money int32) {
	    fmt.Printf("%s earned %d money..\n", w.name, money)
	}
	
- 接口的使用：

一个结构体必须实现了一个接口的所有方法，才能被一个接口对象接受。这一点和Java语言中的接口的要求是一样的。

例如上例中的Live接口的对象live，只能接受实现了Live接口所有方法的Student结构体的对象，而不能接受其他结构体的对象。

一个接口可以被多个结构体实现，一个结构体可以实现多个接口的方法，是多对多的关系。

使用方法：先定义一个接口的对象，用实现了该接口所有方法的结构体的对象来初始化该接口对象，然后就可以通过该接口对象来访问接口的方法。