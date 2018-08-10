- hello world!

		package main
		
		import "fmt"
		
		func main() {
			fmt.Printf("Hello, world or 你好，世界 or καλημ ́ρα κóσμ or こんにちはせかい\n")
		}

	输出如下：

		Hello, world or 你好，世界 or καλημ ́ρα κóσμ or こんにちはせかい

- 详解

	首先我们要了解一个概念，Go程序是通过package来组织的

	package <pkgName>（在我们的例子中是package main）这一行告诉我们当前文件属于哪个包，而包名main则告诉我们它是一个可独立运行的包，它在编译后会产生可执行文件。除了main包之外，其它的包最后都会生成*.a文件（也就是包文件）并放置在$GOPATH/pkg/$GOOS_$GOARCH中（以Mac为例就是$GOPATH/pkg/darwin_amd64）。

	每一个可独立运行的Go程序，必定包含一个package main，在这个main包中必定包含一个入口函数main，而这个函数既没有参数，也没有返回值。

	为了打印Hello, world...，我们调用了一个函数Printf，这个函数来自于fmt包，所以我们在第三行中导入了系统级别的fmt包：import "fmt"。

	包的概念和Python中的package类似，它们都有一些特别的好处：模块化（能够把你的程序分成多个模块)和可重用性（每个模块都能被其它应用程序反复使用）。我们在这里只是先了解一下包的概念，后面我们将会编写自己的包。

	在第五行中，我们通过关键字func定义了一个main函数，函数体被放在{}（大括号）中，就像我们平时写C、C++或Java时一样。

	大家可以看到main函数是没有任何的参数的，我们接下来就学习如何编写带参数的、返回0个或多个值的函数。

	第六行，我们调用了fmt包里面定义的函数Printf。大家可以看到，这个函数是通过<pkgName>.<funcName>的方式调用的，这一点和Python十分相似。

	前面提到过，包名和包所在的文件夹名可以是不同的，此处的<pkgName>即为通过package <pkgName>声明的包名，而非文件夹名。

	最后大家可以看到我们输出的内容里面包含了很多非ASCII码字符。实际上，Go是天生支持UTF-8的，任何字符都可以直接输出，你甚至可以用UTF-8中的任何字符作为标识符。