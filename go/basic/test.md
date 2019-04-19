## Go语言测试框架（testing）用法

要开始一个单元测试，需要准备一个 go 源码文件，在命名文件时需要让文件必须以_test结尾。

单元测试源码文件可以由多个测试用例组成，**每个测试用例函数需要以Test为前缀**，例如：

	func TestXXX( t *testing.T )

- 测试用例文件不会参与正常源码编译，不会被包含到可执行文件中。
- 测试用例文件使用 go test /go test -v指令来执行，没有也不需要 main() 作为函数入口。所有在以_test结尾的源码内以Test开头的函数会自动被执行。
- 测试用例可以不传入 *testing.T 参数。

- eg:

		package code11_3
		
		import "testing"
		
		func TestHelloWorld(t *testing.T) {
		    t.Log("hello world")
		}
		
>代码说明如下：

>第 5 行，单元测试文件 (*_test.go) 里的测试入口必须以 Test 开始，参数为 *testing.T 的函数。一个单元测试文件可以有多个测试入口。

>第 6 行，使用 testing 包的 T 结构提供的 Log() 方法打印字符串。



- 1) 单元测试命令行

	- 单元测试使用 go test 命令启动，例如：
	
			$ go test helloworld_test.go
			
			ok          command-line-arguments        0.003s
			$ go test -v helloworld_test.go
			=== RUN   TestHelloWorld
			--- PASS: TestHelloWorld (0.00s)
			        helloworld_test.go:8: hello world
			PASS
			ok          command-line-arguments        0.004s
			
>代码说明如下：

>第 1 行，在 go test 后跟 helloworld_test.go 文件，表示测试这个文件里的所有测试用例。

>第 2 行，显示测试结果，ok 表示测试通过，command-line-arguments 是测试用例需要用到的一个包名，0.003s 表示测试花费的时间。

>第 3 行，显示在附加参数中添加了-v，可以让测试时显示详细的流程。

>第 4 行，表示开始运行名叫 TestHelloWorld 的测试用例。

>第 5 行，表示已经运行完 TestHelloWorld 的测试用例，PASS 表示测试成功。

>第 6 行打印字符串 hello world。

- 2) 运行指定单元测试用例

go test 指定文件时默认执行文件内的所有测试用例。可以使用-run参数选择需要的测试用例单独执行，参考下面的代码。
		
	package code11_3
	
	import "testing"
	
	func TestA(t *testing.T) {
	    t.Log("A")
	}
	
	func TestAK(t *testing.T) {
	    t.Log("AK")
	}
	
	func TestB(t *testing.T) {
	    t.Log("B")
	}
	
	func TestC(t *testing.T) {
	    t.Log("C")
	}
	
这里指定 TestA 进行测试：

	$ go test -v -run TestA select_test.go
	=== RUN   TestA
	--- PASS: TestA (0.00s)
	        select_test.go:6: A
	=== RUN   TestAK
	--- PASS: TestAK (0.00s)
	        select_test.go:10: AK
	PASS
	ok          command-line-arguments        0.003s
	
>TestA 和 TestAK 的测试用例都被执行，原因是-run跟随的测试用例的名称支持正则表达式，使用-run TestA$即可只执行 TestA 测试用例。

- 3) 标记单元测试结果

当需要终止当前测试用例时，可以使用 FailNow，参考下面的代码。

	func TestFailNow(t *testing.T) {
	    t.FailNow()
	}
	
	还有一种只标记错误不终止测试的方法，代码如下：
	func TestFail(t *testing.T) {
	    fmt.Println("before fail")
	    t.Fail()
	    fmt.Println("after fail")
	}
	
	测试结果如下：
	=== RUN   TestFail
	before fail
	after fail
	--- FAIL: TestFail (0.00s)
	FAIL
	exit status 1
	FAIL        command-line-arguments        0.002s
	
>从日志中看出，第 5 行调用 Fail() 后测试结果标记为失败，但是第 7 行依然被程序执行了。

- 4) 单元测试日志

	每个测试用例可能并发执行，使用 testing.T 提供的日志输出可以保证日志跟随这个测试上下文一起打印输出。testing.T 提供了几种日志输出方法
	>Log  		打印日志，同时结束测试
	
	>Logf	 	格式化打印日志，同时结束测试
	
	>Error		打印错误日志，同时结束测试
	
	>Errorf	格式化打印错误日志，同时结束测试
	
	>Fatal		打印致命日志，同时结束测试
	
	>Fatalf	格式化打印致命日志，同时结束测试
	
**开发者可以根据实际需要选择合适的日志。**
