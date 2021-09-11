# 第 5 章 - 第一个 Go 程序

![First Go Application](./images/5-first-go-app.821f797f.jpg)

## 1 您将在本章学到什么？

* 用 Go 写一个简单的程序
* 编译程序

## 2 涵盖的技术概念

* 规范
* 编译
* 二进制文件与可执行文件

## 3 介绍

在本章中，我们将编写两个 Go 应用程序。

## 4 应用程序规范

在编写任何代码之前，我们需要决定我们的应用程序将做什么。大多数项目都从这个阶段开始。这称为规范阶段。它旨在产生应用程序应满足的精确要求。这些要求是规格（或规格）。

我们的应用程序规范很简单：启动时，应用程序应该显示日期和时间，然后退出。

## 5 项目目录

Go 应用程序由文件组成。在这些文件上，我们将编写 Go 代码。我们称这些文件为**“源文件”**。应用程序存储在主目录中。这个主目录只能包含一个源文件。大多数时候，它由几个子目录组成。

我们将为我们的应用程序创建这个主目录。您可以使用命令行（或使用系统的图形界面）来执行此操作：

```shell
$ cd Documents/code
$ mkdir dateAndTime
```

## 6 IDE

我们距离编写代码只有几分钟的路程。你需要特殊的软件来编写 Go 代码吗？理论上，您可以使用标准文本编辑器编写代码。市场上有专门为开发人员开发的专用软件。它们被称为 IDE：集成开发环境。

IDE 提供以下功能：

* 保留字的自动着色（语法高亮）
* 自动补全
* 重构能力
* ...

市场上有许多 IDE。您可以在 google 搜索找到最适合您的。我使用 IntelliJ 开发的 Goland。这个软件不是免费的（它是基于订阅的），但我觉得它很容易使用。

## 7 源文件

让我们创建我们的源文件。我们将其命名为 **main.go**。

```go
// first-go-application/first/main.go
package main

import (
    "fmt"
    "time"
)

func main() {
    now := time.Now()
    fmt.Println(now)
}
```

### 7.1 代码说明

* 第一行在 Go 中是强制性的<sup>[译1](#firstline)</sup>。在所有文件中，您必须添加包声明。这种声明由关键字 `package` 和包的名称组成。
* 在第二行，你可以读到另一个关键词：**`import`**。它的后面通常是一个开放的小括号和一个程序的导入包的列表。每个包都写在一个新的行上。每个包都有一个用双引号分隔的名称。这里我们的应用程序依赖于两个包。
  - fmt
  - time
* 这些包是**标准库**的一部分。
* 然后你会发现一个名为 **`main`** 的函数的声明。稍后我们将更深入地研究函数的语法。
  - 函数声明用大括号括起来：**`{`** 和 **`}`**。
  - 在函数声明中，我们有两个语句：
    - 第一条指令是一个影响因素。我们初始化变量 **"now"**，并给它一个由 **`time`** 包的 **Now()** 函数的返回值
    - 第二条指令是调用 **`fmt`** 包中的 **`Print`** 函数

* 警告！请确保您只使用您实际导入的包。否则你的程序将无法编译... 当你导入的包未使用时，Go 程序不会编译。
  ```go
  // DO NOT COMPILE
  // first-go-application/import-issue/main.go
  package main

  import (
      "fmt"
      "time"
  )

  func main(){

  }
  ```

### 7.2 关于 main 函数

main 函数是程序的**入口点**。在每个应用程序中，您至少有一个 main 函数。程序将从该函数的第一条语句开始执行。（注意 C、C++、Java 中存在 main 函数的概念。）

## 8 编译

源文件已准备好转换为二进制文件（或可执行文件）。为此，我们将使用 Go 工具链。打开一个终端：

```shell
$ cd Documents/code/dateAndTime
$ go build main.go
```

第一条指令（cd）指示 shell 将当前目录更改为 **Documents/code/dateAndTime**。第二条命令会将程序编译为可执行文件。可执行文件名为 main（与源文件同名，不带 .go 扩展名）。让我们看看现在进入 dateAndTime 目录的文件：

```shell
$ ls -lh
total 4160
-rwxr-xr-x  1 maximilienandile  staff   2.0M Aug 16 11:27 main
-rw-r--r--  1 maximilienandile  staff    94B Aug 16 11:00 main.go
```

我们使用命令 **`ls`**。 （对于 Windows 用户，您可以使用 **`dir`** 命令）。您可以看到我们有两个文件：

* **main** 大约有 2.0M，它是可执行文件。
* **main.go** 大约只有 94 个字节（这是我们的源文件）。

现在是时候启动我们的应用程序了：

```shell
$ ./main
2019-08-16 11:45:44.435637 +0200 CEST m=+0.000263533
```

祝贺您完成了第一个 Go 应用程序！

## 9 自测

### 9.1 问题

1. 如何编译 Go 程序？
2. 编译的结果如何调用？
3. Go 应用程序的入口点函数的名称是什么？
4. `import` 语句的用途是什么？

### 9.2 答案

1. 如何编译 Go 程序？
   1. 打开终端
   2. 转到您的应用程序目录。假设有一个名为 main.go 的文件，其中包含一个 `main` 函数，执行下面的命令：
      1. `$ cd /code/myApp`
	  2. `$ go build main.go`
2. 编译的结果如何调用？
   1. 它被称为可执行文件或二进制文件。
3. Go 应用程序的入口点函数的名称是什么？
   1. `main`
4. `import` 语句的用途是什么？
   1. 它用于将包（从标准库或其他来源）导入到程序中。
   2. 然后可以在代码中使用导入的包。

## 10 练习

### 10.1 规格说明

创建一个 go 应用程序，在屏幕上显示字符串 “Hello World” 并退出。

### 10.2 解答

```go
// first-go-application/hello-world/main.go
package main

import "fmt"

func main() {
    fmt.Println("Hello World")
}
```

注意：

* 在这里你可以看到我们只使用了一个依赖项。程序的导入部分发生了变化；只导入一个包时不需要括号。
* 我们有一个 `main` 函数。里面有一个语句。
* 这里调用了函数 `Println`。这个函数是 `fmt` 包的一部分（`fmt` 代表“格式化”）。
* 包 `fmt` 是标准库的一部分。

## 11 关键要点

* 创建一个简单的程序。
  - 创建一个文件
  - 将其命名为 **`main.go`**
  - 下面是程序的基本框架（什么都不做）
    ```go
	// first-go-application/skeleton/main.go
    package main

    func main() {

    }
	```
* 此文件即表示“源文件”。
* 从这个源文件，我们可以创建一个可执行程序（可以启动）。
* 可执行文件的创建称为“编译”。
* 要编译程序，请在终端中输入以下命令：
  - `go build main.go`
* 要启动已编译的程序，请在终端中输入以下内容：
  - `./main`

<hr>

* <a name="firstline">译1</a>：从整个文件来看应该是第二行，如果不考虑注释，则可以视为第一行。