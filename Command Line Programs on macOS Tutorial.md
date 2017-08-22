# macOS教程：命令行程序

#### [原文地址](https://www.raywenderlich.com/128039/command-line-programs-macos-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div class="note">
        <em>
            2017年7月21日更新：
        </em>
        本macOS命令行程序已更新至支持Xcode 9及Swift 4。
    </div>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/CommandLinePrograms-feature.png"
        alt="CommandLinePrograms-feature" width="250" height="250" class="alignright size-thumbnail wp-image-129951">
    </p>
    <p>
        通常来说，Mac用户与他们的电脑是通过（
        <em>
            GUI
        </em>
        ）进行交互的。GUI，就像它的名字所表示的一样，是基于用户和电脑之间的可视化交互进行的，比如在屏幕上用鼠标选择或操作菜单、按钮之类的元素等。
    </p>
    <p>
        但并非过去太久，在图形用户界面出现之前，命令行界面（
        <em>
            CLI
        </em>
        ）是与电脑进行交互的重要方法。CLI是基于文本界面的，用户通过输入程序名称（可添加参数）来执行。
    </p>
    <p>
        尽管GUI非常的流行，命令行程序仍然在今天的计算机世界中扮演重要的角色。诸如
        Despite the prevalence of GUIs, command-line programs still have an important role in today’s computing world. Command-line programs such as
        <a href="http://www.imagemagick.org/script/command-line-processing.php"
        target="_blank" sl-processed="1">
            ImageMagick
        </a>
        或
        <a href="https://www.ffmpeg.org/" target="_blank" sl-processed="1">
            ffmpeg
        </a>
        的命令行程序在服务器的世界中都是非常重要的。事实上，构成英特网的大多数服务器都仅仅是在运行命令行程序。
    </p>
    <p>
        甚至Xcode也是使用的命令行程序！当Xcode build你的项目的时候，它就会调用
        <em>
            <a href="https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/xcodebuild.1.html"
            target="_blank" sl-processed="1">
                xcodebuild
            </a>
        </em>
        来进行实际上的build。因为如果build的过程被构建在了Xcode的产品中，就很难甚至是不可能实现可持续集成（CI）的！
    </p>
    <p>
        在本教程中，你将会编写一个名叫
        <em>
            Panagram
        </em>
        的命令行工具。它会根据传入的选项，来检测给定的是否是异构词或相同字母的异序词。它可以由预定义的参数启动，也可以运行在交互模式下，用户将会被提示输入要求的值。
    </p>
    <p>
        通常，在macOS中，命令行程序是通过 嵌入工具app的类似终端的shell（在macOS中是
        <em>
            bash
        </em>
        ）启动的。在本教程中，为了简易和便于学习，大多时间你都会使用Xcode来启动Panagram。在本教程结束的时候，你将会学习如何从终端中启动Panagram。
    </p>
    <h2>
        入门
    </h2>
    <p>
        Swift看起来像是一个创建命令行程序的奇特选择，因为可能像是类C，Perl，Ruby或Java才是更加传统的选择。但仍有一些很棒的理由，让你可以选择Swift来实现命令行的需求：
    </p>
    <ul>
        <li>
            Swift既可以作为解释性的脚本语言来使用，也可以当做编译型语言来使用。这就给你带来了脚本语言的好处，例如零编译时间，易于维护，以及在编译你的app以提高执行的时间和将它捆绑以销售到公众之间进行选择。
        </li>
        <li>
            你不需要切换语言。很多人说作为程序员每年都应当学习一门语言。这当然并不是一个坏主意，但如果你早已习惯使用Swift和它的标准库，你就可以继续Swift以减少学习时间的成本投入。
        </li>
    </ul>
    <p>
        在本教程中，你将创建一个典型的编译项目。
    </p>
    <p>
        打开Xcode并找到
        <em>
            File/New/Project
        </em>
        。找到
        <em>
            macOS
        </em>
        组，选择
        <em>
            Application/Command Line Tool
        </em>
        并单击
        <em>
            Next
        </em>
        ：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/New-Project.png"
        rel="attachment wp-att-165422" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/New-Project-444x320.png"
            alt="" width="444" height="320" class="aligncenter size-full wp-image-165422"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/New-Project-444x320.png 444w, https://koenig-media.raywenderlich.com/uploads/2017/06/New-Project-650x468.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/06/New-Project.png 730w"
            sizes="(max-width: 444px) 100vw, 444px">
        </a>
    </p>
    <p>
        在
        <em>
            Product Name
        </em>
        中，选择Panagram。确认
        <em>
            Language
        </em>
        被设为
        <em>
            Swift
        </em>
        ，然后单击
        <em>
            Next
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/Name-the-New-Project.png"
        rel="attachment wp-att-165423" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/Name-the-New-Project-444x320.png"
            alt="" width="444" height="320" class="aligncenter size-full wp-image-165423"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/Name-the-New-Project-444x320.png 444w, https://koenig-media.raywenderlich.com/uploads/2017/06/Name-the-New-Project-650x468.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/06/Name-the-New-Project.png 730w"
            sizes="(max-width: 444px) 100vw, 444px">
        </a>
    </p>
    <p>
        选择一个磁盘上的位置来保存你的项目，并单击
        <em>
            Create
        </em>
        。
    </p>
    <p>
        在
        <em>
            Project Navigator
        </em>
        中，你将看到模板
        <em>
            main.swift
        </em>
        文件，它是通过Xcode命令行工具模板所创建的。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/main-swift.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/main-swift.png"
            alt="" width="629" height="379" class="aligncenter size-full wp-image-165846"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/main-swift.png 629w, https://koenig-media.raywenderlich.com/uploads/2017/06/main-swift-480x289.png 480w"
            sizes="(max-width: 629px) 100vw, 629px">
        </a>
    </p>
    <p>
        很多类C语言都有
        <code>
            main
        </code>
        函数作为程序的入口 - 也就是说，当程序被执行的时候，被操作系统调用的代码。这意味着程序会从这个方法的第一行处开始被执行。与众不同的是，Swift并不包含一个
        <code>
            main
        </code>
        函数，而是只有一个
        <em>
            main文件
        </em>
        。
    </p>
    <p>
        当你运行这个项目的时候，在这个文件中的除方法和类声明之外的第一行代码就会被执行。让你的
        <em>
            main.swift
        </em>
        文件尽可能地保持整洁是一个非常好的习惯，你应当尽量保持类和结构体存放在它们自己相应的文件中。这就可以使一切保持条理化，并帮助你理解
        <em>
            main execution path
        </em>
        。
    </p>
    <h2>
        输出流
    </h2>
    <p>
        在大多数的命令行程序中，你都会为用户打印出一些信息。例如，一个将视频文件转化为不同的格式的命令行程序，就可以打印出当前的进度，或当发生错误的时候，打印出错误信息。
    </p>
    <p>
        类似macOS这样基于Unix的系统，定义了两种不同的输出流：
    </p>
    <ul>
        <li>
            <em>
                standard output
            </em>
            stream（或
            <code>
                stdout
            </code>
            ）会将信息正常地输出到屏幕上展示给用户。
        </li>
        <li>
            <em>
                standard error
            </em>
            stream（或
            <code>
                stderr
            </code>
            ）通常是用来展示状态和错误信息的。通常它会展示到屏幕上，但也可以重定向到一个文件中。
        </li>
    </ul>
    <div class="note">
        <em>
            注意：
        </em>
        当从Xcode或终端中启动一个命令行程序时，默认的，
        <code>
            stdout
        </code>
        和
        <code>
            stderr
        </code>
        是相同的，都会将信息写入到控制台。一般的实践是将
        <code>
            stderr
        </code>
        重定向到一个文件中，这样错误的信息就不会展示到屏幕上，但可以在之后进行查看。这样就可以通过隐藏用户不需要看到的信息，来使得debug一个装载好的app更加容易，但仍然保留错误的信息以便将来的查看。
    </div>
    <p>
        在Project navigator中选择Panagram组，按下
        <em>
            Cmd + N
        </em>
        来创建一个新的文件。在
        <em>
            macOS
        </em>
        下，选择
        <em>
            Source/Swift File
        </em>
        并按
        <em>
            Next
        </em>
        键：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/New-Swift-File.png"
        rel="attachment wp-att-165426" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/New-Swift-File-444x320.png"
            alt="" width="444" height="320" class="aligncenter size-full wp-image-165426"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/New-Swift-File-444x320.png 444w, https://koenig-media.raywenderlich.com/uploads/2017/06/New-Swift-File-650x468.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/06/New-Swift-File.png 730w"
            sizes="(max-width: 444px) 100vw, 444px">
        </a>
    </p>
    <p>
        将文件保存为
        <em>
            ConsoleIO.swift
        </em>
        。你将会把所有的输入和输出元素封装到一个又小又方法的名为
        <code>
            ConsoleIO
        </code>
        的类中。
    </p>
    <p>
        添加下列的代码到
        <em>
            ConsoleIO.swift
        </em>
        的尾部：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">ConsoleIO</span> </span>{
}
</pre>
    <p>
        你的下一个任务就是将Panagram改为使用两个输出流。
    </p>
    <p>
        在
        <em>
            ConsoleIO.swift
        </em>
        中，添加下列的enum到文件的顶部，就在
        <code>
            ConsoleIO
        </code>
        类的实现之上，
        <code>
            import
        </code>
        这行代码之下：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">enum</span> <span class="hljs-title">OutputType</span> </span>{
  <span class="hljs-keyword">case</span> error
  <span class="hljs-keyword">case</span> standard
}
</pre>
    <p>
        这就定义了当撰写信息时的输出流。
    </p>
    <p>
        接下来，添加下列的方法到
        <code>
            ConsoleIO
        </code>
        类中（就在类声明的花括号之中）：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">writeMessage</span><span class="hljs-params">(<span class="hljs-number">_</span> message: String, to: OutputType = .standard)</span></span> {
  <span class="hljs-keyword">switch</span> to {
  <span class="hljs-keyword">case</span> .standard:
    <span class="hljs-built_in">print</span>(<span class="hljs-string">"<span class="hljs-subst">\(message)</span>"</span>)
  <span class="hljs-keyword">case</span> .error:
    fputs(<span class="hljs-string">"Error: <span class="hljs-subst">\(message)</span>\n"</span>, stderr)
  }
}
</pre>
    <p>
        这个方法中含有两个参数；第一个就是实际要打印的信息，第二个则是要输出到的目的地。第二个参数默认为
        <code>
            .standard
        </code>
        。
    </p>
    <p>
        对于
        <code>
            .standard
        </code>
        选项的代码使用了
        <code>
            print
        </code>
        ，它会默认地将信息写入到
        <code>
            stdout
        </code>
        中。而
        <code>
            .error
        </code>
        这里，则使用C函数
        <code>
            fputs
        </code>
        写入到
        <code>
            stderr
        </code>
        中，它是一个指向到标准错误流的全局变量。
    </p>
    <p>
        添加下列的代码到
        <code>
            ConsoleIO
        </code>
        类的尾部：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">printUsage</span><span class="hljs-params">()</span></span> {

  <span class="hljs-keyword">let</span> executableName = (<span class="hljs-type">CommandLine</span>.arguments[<span class="hljs-number">0</span>] <span class="hljs-keyword">as</span> <span class="hljs-type">NSString</span>).lastPathComponent
        
  writeMessage(<span class="hljs-string">"usage:"</span>)
  writeMessage(<span class="hljs-string">"<span class="hljs-subst">\(executableName)</span> -a string1 string2"</span>)
  writeMessage(<span class="hljs-string">"or"</span>)
  writeMessage(<span class="hljs-string">"<span class="hljs-subst">\(executableName)</span> -p string"</span>)
  writeMessage(<span class="hljs-string">"or"</span>)
  writeMessage(<span class="hljs-string">"<span class="hljs-subst">\(executableName)</span> -h to show usage information"</span>)
  writeMessage(<span class="hljs-string">"Type <span class="hljs-subst">\(executableName)</span> without an option to enter interactive mode."</span>)
}
</pre>
    <p>
        这个代码定义了
        <code>
            printUsage()
        </code>
        方法，它可以将信息打印到控制台上。每次当你运行程序的时候，可执行程序的路径就会悄悄被传递到
        <code>
            argument[0]
        </code>
        中，他可以通过全局的枚举
        <code>
            CommandLine
        </code>
        访问到。
        <code>
            CommandLine
        </code>
        是在Swift标准库中对于
        <code>
            argc
        </code>
        和
        <code>
            argv
        </code>
        参数（你可能已在类C语言中了解过的）的封装。
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        通常的实践是，当用户尝试使用不正确的参数启动命令行程序时，就将使用说明打印到控制台中。
    </div>
    <p>
        创建另一个名为
        <em>
            Panagram.swift
        </em>
        的Swift文件（就和之前的步骤一样），并添加下列的代码到里面：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">Panagram</span> </span>{

  <span class="hljs-keyword">let</span> consoleIO = <span class="hljs-type">ConsoleIO</span>()

  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">staticMode</span><span class="hljs-params">()</span></span> {
    consoleIO.printUsage()
  }

}
</pre>
    <p>
        这就定义了带有一个方法的一个
        <code>
            Panagram
        </code>
        类。这个类会用来处理程序逻辑，而
        <code>
            staticMode()
        </code>
        则代表了非交互的模式 - 也就是说，当你通过命令行参数提供所有的数据的时候。现在，它只是把用法的信息打印了出来。
    </p>
    <p>
        现在，打开
        <em>
            main.swift
        </em>
        并使用下列的代码替换
        <code>
            print
        </code>
        语句：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">let</span> panagram = <span class="hljs-type">Panagram</span>()
panagram.staticMode()
</pre>
    <div class="note">
        <em>
            注意：
        </em>
        就像上面所提到的，
        <em>
            main.swift
        </em>
        中的第一行代码将在程序启动的时候被执行。
    </div>
    <p>
        Build并运行你的项目；你会在Xcode的控制台中看到下列的输出：
    </p>
    <pre lang="" class="hljs bash">usage:
Panagram -a string1 string2
or
Panagram -p string
or
Panagram -h to show usage information
Type Panagram without an option to enter interactive mode.
Program ended with <span class="hljs-built_in">exit</span> code: 0
</pre>
    <p>
        到目前为止，你已经学习了什么是命令行工具，它会从哪里开始执行，如何发送信息到
        <code>
            stdout
        </code>
        和
        <code>
            stderr
        </code>
        上，以及如何将代码拆分到不同的逻辑单元，来保持
        <em>
            main.swift
        </em>
        整洁有序。
    </p>
    <p>
        在下一部分，你将会处理命令行的参数，并完成Panagram的静态模式。
    </p>
    <h2>
        命令行的参数
    </h2>
    <p>
        当你启动一个命令行程序时，你在命令后输入的任何内容都会被当做参数传递给程序。参数之间是通过空格来区分的。通常，你会传入两种类型的参数：
        <em>
            选项
        </em>
        和
        <em>
            字符串
        </em>
        。
    </p>
    <p>
        选项是由一条横线开始，后跟一个字符；或两条横线，后跟一个单词。例如，很多程序都有选项
        <code>
            -h
        </code>
        或
        <code>
            --help
        </code>
        ，前者就是后者的简写。为了让一切保持简单，Panagram将只支持简短版本的选项。
    </p>
    <p>
        打开
        <em>
            Panagram.swift
        </em>
        并添加下列的enum到文件的顶部，要在
        <code>
            Panagram
        </code>
        类的范围之外：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">enum</span> <span class="hljs-title">OptionType</span>: <span class="hljs-title">String</span> </span>{
  <span class="hljs-keyword">case</span> palindrome = <span class="hljs-string">"p"</span>
  <span class="hljs-keyword">case</span> anagram = <span class="hljs-string">"a"</span>
  <span class="hljs-keyword">case</span> help = <span class="hljs-string">"h"</span>
  <span class="hljs-keyword">case</span> unknown
  
  <span class="hljs-keyword">init</span>(value: <span class="hljs-type">String</span>) {
    <span class="hljs-keyword">switch</span> value {
    <span class="hljs-keyword">case</span> <span class="hljs-string">"a"</span>: <span class="hljs-keyword">self</span> = .anagram
    <span class="hljs-keyword">case</span> <span class="hljs-string">"p"</span>: <span class="hljs-keyword">self</span> = .palindrome
    <span class="hljs-keyword">case</span> <span class="hljs-string">"h"</span>: <span class="hljs-keyword">self</span> = .help
    <span class="hljs-keyword">default</span>: <span class="hljs-keyword">self</span> = .unknown
    }
  }
}
</pre>
    <p>
        这就使用
        <code>
            String
        </code>
        作为基本类型，定义了一个
        <code>
            enum
        </code>
        ，这样你就可以直接将选项参数传递给
        <code>
            init(\_:)
        </code>
        。Panagram有三个选项：
        <code>
            -p
        </code>
        用来检测异构词，
        <code>
            -a
        </code>
        用来检测逆序词，
        <code>
            -h
        </code>
        则用来展示用法信息。其余的东西则被当做错误处理。
    </p>
    <p>
        接下来，添加下列的方法到
        <code>
            Panagram
        </code>
        类中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">getOption</span><span class="hljs-params">(<span class="hljs-number">_</span> option: String)</span></span> -&gt; (option:<span class="hljs-type">OptionType</span>, value: <span class="hljs-type">String</span>) {
  <span class="hljs-keyword">return</span> (<span class="hljs-type">OptionType</span>(value: option), option)
}
</pre>
    <p>
        上面的方法接受一个选项参数作为
        <code>
            String
        </code>
        ，并返回一个关于
        <code>
            OptionType
        </code>
        和
        <code>
            String
        </code>
        的元组。
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        如果你不熟悉Swift中的元组，可以访问我们在 
        <em>
            Beginning Swift 3
        </em>
        上的视频系列，特别是
        <a href="https://videos.raywenderlich.com/courses/51-beginning-swift-3/lessons/5"
        target="_blank" sl-processed="1">
            PART 5: Tuples
        </a>
        。
    </div>
    <p>
        在
        <code>
            Panagram
        </code>
        类中，使用下列代码替换
        <code>
            staticMode()
        </code>
        的内容：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-comment">//1</span>
<span class="hljs-keyword">let</span> argCount = <span class="hljs-type">CommandLine</span>.argc
<span class="hljs-comment">//2</span>
<span class="hljs-keyword">let</span> argument = <span class="hljs-type">CommandLine</span>.arguments[<span class="hljs-number">1</span>]
<span class="hljs-comment">//3</span>
<span class="hljs-keyword">let</span> (option, value) = getOption(argument.substring(from: argument.index(argument.startIndex, offsetBy: <span class="hljs-number">1</span>)))
<span class="hljs-comment">//4</span>
consoleIO.writeMessage(<span class="hljs-string">"Argument count: <span class="hljs-subst">\(argCount)</span> Option: <span class="hljs-subst">\(option)</span> value: <span class="hljs-subst">\(value)</span>"</span>)
</pre>
    <p>
        上面的代码：
    </p>
    <ol>
        <li>
            首先，你获取了传递给程序的参数的个数。由于可执行文件的路径必然会传入（
            <code>
                CommandLine.arguments[0]
            </code>
            ），count的值总是会大于等于1。
        </li>
        <li>
            下一步，从
            <code>
                arguments
            </code>
            的数组中获取“真正的”第一个参数（选项参数）。
        </li>
        <li>
            接下来，你将参数进行解析，并将它转换为一个
            <code>
                OptionType
            </code>
            。
            <code>
                index(\_:offsetBy:)
            </code>
            方法会跳过参数字符串中的第一个字符，在本例中也就是“-”这个字符。
        </li>
        <li>
            最后，把解析的结果作为log输出到控制台中。
        </li>
    </ol>
    <p>
        在
        <em>
            main.swift
        </em>
        中，使用下列代码替换
        <code>
            panagram.staticMode()
        </code>
        这行：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">if</span> <span class="hljs-type">CommandLine</span>.argc &lt; <span class="hljs-number">2</span> {
  <span class="hljs-comment">//<span class="hljs-doctag">TODO:</span> Handle interactive mode</span>
} <span class="hljs-keyword">else</span> {
  panagram.staticMode()
}
</pre>
    <p>
        如果程序收到的参数少于两个，你就会进入到交互模式 - 你将在之后完成这个部分。否则，你就会使用非交互的静态模式。
    </p>
    <p>
        现在你需要知道如何在Xcode中传递参数到你的命令行工具中。因此，在
        <em>
            Toolbar
        </em>
        中，选择名为
        <em>
            Panagram
        </em>
        的
        <em>
            Scheme
        </em>
        ：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/Scheme.png"
        rel="attachment wp-att-128043" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Scheme.png"
            alt="Scheme" width="316" height="46" class="aligncenter size-full wp-image-128043">
        </a>
    </p>
    <p>
        在出现的菜单中选择
        <em>
            Edit Scheme...
        </em>
        ：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/Edit_Scheme.png"
        rel="attachment wp-att-128044" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Edit_Scheme.png"
            alt="Edit_Scheme" width="310" height="172" class="aligncenter size-full wp-image-128044">
        </a>
    </p>
    <p>
        确定在左侧的面板中选择
        <em>
            Run
        </em>
        ，点击
        <em>
            Arguments
        </em>
        tab，然后点击
        <em>
            Arguments Passed On Launch
        </em>
        下的
        <em>
            +
        </em>
        。添加
        <code>
            -p
        </code>
        作为参数，并点击
        <em>
            Close
        </em>
        ：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Scheme_Settings-700x394.png"
        alt="Scheme_Settings" width="700" height="394" class="aligncenter size-large wp-image-128046"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Scheme_Settings-700x394.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Scheme_Settings-480x270.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Scheme_Settings-768x432.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/Scheme_Settings-266x151.png 266w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        现在，build并运行，你会在控制台中看到下面的输出：
    </p>
    <pre lang="" class="hljs bash">Argument count: 2 Option: Palindrome value: p
Program ended with <span class="hljs-built_in">exit</span> code: 0
</pre>
    <p>
        到目前为止，你已经添加了一个基本的选项系统到你的工具在，了解了如何处理命令行参数，以及如何在Xcode中传递参数。
    </p>
    <p>
        接下来，你就要构建Panagram的主要功能了。
    </p>
    <h2>
        逆序词和异构词
    </h2>
    <p>
        在你撰写代码去识别逆序词和异构词之前，你应当首先清楚它们是什么！
    </p>
    <p>
        <a href="https://en.wikipedia.org/wiki/Palindrome" sl-processed="1">
            逆序词
        </a>
        是那些从前往后读，或从后往前读完全一样的单词或句子。下面有一些例子：
    </p>
    <ul>
        <li>
            level
        </li>
        <li>
            noon
        </li>
        <li>
            A man, a plan, a canal - Panama!
        </li>
    </ul>
    <p>
        正如你所看到的，首字母大写和标点符号通常会被忽略。为了保持简单，Panagram将忽略掉首字母大写和空格，并且不会处理标点。
    </p>
    <p>
        <a href="https://en.wikipedia.org/wiki/Anagram" sl-processed="1">
            异构词
        </a>
        是那些由另一个单词或句子中的字母，所构建成的单词或句子。一些例子包括：
    </p>
    <ul>
        <li>
            silent &lt;-&gt; listen
        </li>
        <li>
            Bolivia &lt;-&gt; Lobivia （是一种来自玻利维亚的🌵）
        </li>
    </ul>
    <p>
        你会将检测的逻辑封装到一个
        <code>
            String
        </code>
        的小extension中。
    </p>
    <p>
        创建一个新的名为
        <em>
            StringExtension.swift
        </em>
        的文件，并添加下列的代码到其中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">String</span> </span>{
}
</pre>
    <p>
        需要一些时间来进行设计工作。首先，如何检测一个异构词：
    </p>
    <ol>
        <li>
            对于两个字符串，都忽略掉首字母大写和空格。
        </li>
        <li>
            检测两个字符串中所含有的是否都是相同的字符，且所有的字符出现的次数都对应相同。
        </li>
    </ol>
    <p>
        添加下列的方法到
        <em>
            StringExtension.swift
        </em>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">isAnagramOf</span><span class="hljs-params">(<span class="hljs-number">_</span> s: String)</span></span> -&gt; <span class="hljs-type">Bool</span> {
  <span class="hljs-comment">//1</span>
  <span class="hljs-keyword">let</span> lowerSelf = <span class="hljs-keyword">self</span>.lowercased().replacingOccurrences(of: <span class="hljs-string">" "</span>, with: <span class="hljs-string">""</span>)
  <span class="hljs-keyword">let</span> lowerOther = s.lowercased().replacingOccurrences(of: <span class="hljs-string">" "</span>, with: <span class="hljs-string">""</span>)
  <span class="hljs-comment">//2</span>
  <span class="hljs-keyword">return</span> lowerSelf.sorted() == lowerOther.sorted()
}
</pre>
    <p>
        仔细看上述算法：
    </p>
    <ol>
        <li>
            首先，把两个字符串中的首字母大写和空格都移除掉。
        </li>
        <li>
            然后将字符进行比较和排序。
        </li>
    </ol>
    <p>
        检测逆序词也是同样的简单：
    </p>
    <ol>
        <li>
            忽略掉字符串中的所有大写和空格。
        </li>
        <li>
            将字符串逆序并进行比较；如果相同的话，你就得到了一个逆序词。
        </li>
    </ol>
    <p>
        添加下列的代码到检测逆序词的方法中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">isPalindrome</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">Bool</span> {
  <span class="hljs-comment">//1</span>
  <span class="hljs-keyword">let</span> f = <span class="hljs-keyword">self</span>.lowercased().replacingOccurrences(of: <span class="hljs-string">" "</span>, with: <span class="hljs-string">""</span>)
  <span class="hljs-comment">//2</span>
  <span class="hljs-keyword">let</span> s = <span class="hljs-type">String</span>(f.reversed())
  <span class="hljs-comment">//3</span>
  <span class="hljs-keyword">return</span>  f == s
}
</pre>
    <p>
        这里的逻辑相当得直接：
    </p>
    <ol>
        <li>
            忽略掉字符串中的所有大写和空格。
        </li>
        <li>
            使用颠倒顺序的字符创建第二个字符串。
        </li>
        <li>
            如果它们是相同的，你就得到了一个逆序词。
        </li>
    </ol>
    <p>
        是时候将它们组合到一起，来让Panagram完成它的工作。
    </p>
    <p>
        打开
        <em>
            Panagram.swift
        </em>
        并在
        <code>
            staticMode()
        </code>
        方法中使用下列的代码替换对
        <code>
            writeMessage(_:to:)
        </code>
        的调用：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-comment">//1</span>
<span class="hljs-keyword">switch</span> option {
<span class="hljs-keyword">case</span> .anagram:
    <span class="hljs-comment">//2</span>
    <span class="hljs-keyword">if</span> argCount != <span class="hljs-number">4</span> {
        <span class="hljs-keyword">if</span> argCount &gt; <span class="hljs-number">4</span> {
            consoleIO.writeMessage(<span class="hljs-string">"Too many arguments for option <span class="hljs-subst">\(option.rawValue)</span>"</span>, to: .error)
        } <span class="hljs-keyword">else</span> {
            consoleIO.writeMessage(<span class="hljs-string">"Too few arguments for option <span class="hljs-subst">\(option.rawValue)</span>"</span>, to: .error)
        }        
        consoleIO.printUsage()
    } <span class="hljs-keyword">else</span> {
        <span class="hljs-comment">//3</span>
        <span class="hljs-keyword">let</span> first = <span class="hljs-type">CommandLine</span>.arguments[<span class="hljs-number">2</span>]
        <span class="hljs-keyword">let</span> second = <span class="hljs-type">CommandLine</span>.arguments[<span class="hljs-number">3</span>]
        <span class="hljs-keyword">if</span> first.isAnagramOf(second) {
            consoleIO.writeMessage(<span class="hljs-string">"<span class="hljs-subst">\(second)</span> is an anagram of <span class="hljs-subst">\(first)</span>"</span>)
        } <span class="hljs-keyword">else</span> {
            consoleIO.writeMessage(<span class="hljs-string">"<span class="hljs-subst">\(second)</span> is not an anagram of <span class="hljs-subst">\(first)</span>"</span>)
        }
    }
<span class="hljs-keyword">case</span> .palindrome:
    <span class="hljs-comment">//4</span>
    <span class="hljs-keyword">if</span> argCount != <span class="hljs-number">3</span> {
        <span class="hljs-keyword">if</span> argCount &gt; <span class="hljs-number">3</span> {
            consoleIO.writeMessage(<span class="hljs-string">"Too many arguments for option <span class="hljs-subst">\(option.rawValue)</span>"</span>, to: .error)
        } <span class="hljs-keyword">else</span> {
            consoleIO.writeMessage(<span class="hljs-string">"Too few arguments for option <span class="hljs-subst">\(option.rawValue)</span>"</span>, to: .error)
        }
        consoleIO.printUsage()
    } <span class="hljs-keyword">else</span> {
        <span class="hljs-comment">//5</span>
        <span class="hljs-keyword">let</span> s = <span class="hljs-type">CommandLine</span>.arguments[<span class="hljs-number">2</span>]
        <span class="hljs-keyword">let</span> isPalindrome = s.isPalindrome()
        consoleIO.writeMessage(<span class="hljs-string">"<span class="hljs-subst">\(s)</span> is <span class="hljs-subst">\(isPalindrome ? "" : "not ")</span>a palindrome"</span>)
    }
<span class="hljs-comment">//6</span>
<span class="hljs-keyword">case</span> .help:
    consoleIO.printUsage()
<span class="hljs-keyword">case</span> .unknown:
    <span class="hljs-comment">//7</span>
    consoleIO.writeMessage(<span class="hljs-string">"Unknown option <span class="hljs-subst">\(value)</span>"</span>)
    consoleIO.printUsage()
}
</pre>
    <p>
        一步一步地来查看上述代码：
    </p>
    <ol>
        <li>
            首先，根据你所传的参数，觉得来执行什么样的操作。
        </li>
        <li>
            在异构词这种case下，必须传入四个命令行参数。第一个参数是可执行文件的路径，第二个是
            <code>
                -a
            </code>
            选项，还有待判定两个字符串。当未传入四个参数的时候，就会打印出一个错误信息。
        </li>
        <li>
            在参数个数正确的前提下，保存两个字符串到本地变量中，然后确定它们是否互为异构词，并将结果打印出来。
        </li>
        <li>
            在逆序词这种case下，则必须传入三个参数。第一个参数是可执行文件的路径，第二个是
            <code>
                -p
            </code>
            选项，以及一个待判定的字符串。当未传入三个参数的时候，就会打印出一个错误信息。
        </li>
        <li>
            确定这个字符串是否为逆序词，并打印出结果。
        </li>
        <li>
            如果传入
            <code>
                -h
            </code>
            选项，就打印出用法信息。
        </li>
        <li>
            如果传入未知的选项，亦打印出用法信息。
        </li>
    </ol>
    <p>
        现在，修改scheme中的参数。例如，为使用
        <code>
            -p
        </code>
        选项，你必须传入两个参数（除第一个参数外，也就是可执行文件的路径，总是被隐式地传递）。
    </p>
    <p>
        从设置活动Scheme的工具栏项目中，选择
        <em>
            Edit Scheme...
        </em>
        ，并将第二个参数设置为“
        <em>
            level
        </em>
        ”，就像下面这样：        
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Bildschirmfoto-2016-03-05-um-13.25.10-700x393.png"
        alt="p-option-settings" width="700" height="393" class="aligncenter size-large wp-image-128047"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Bildschirmfoto-2016-03-05-um-13.25.10-700x393.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Bildschirmfoto-2016-03-05-um-13.25.10-480x270.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Bildschirmfoto-2016-03-05-um-13.25.10-768x431.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Build并运行，你就会在控制台中看到下列的输出：
    </p>
    <pre lang="" class="hljs bash">level is a palindrome
Program ended with <span class="hljs-built_in">exit</span> code: 0
</pre>
    <h2>
        处理交互性的输入
    </h2>
    <p>
        现在你已经有了可以work的基本版本的异构词工具，你可以通过增加交互式地输入参数的能力，来让它变得更加得有用。 
    </p>
    <p>
        在这个部分，你将添加异构词工具在未传入参数的情况下进行处理的代码，它将打开交互模式，来提示用户如如所需的参数。
    </p>
    <p>
        首先，你需要增加从键盘获取输入的方法。
        <code>
            stdin
        </code>
        会附加到键盘上，它提供了一个交互式收集用户输入的方式。
    </p>
    <p>
        打开
        <em>
            ConsoleIO.swift
        </em>
        ，并添加下列的方法到类中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">getInput</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">String</span> {
  <span class="hljs-comment">// 1</span>
  <span class="hljs-keyword">let</span> keyboard = <span class="hljs-type">FileHandle</span>.standardInput
  <span class="hljs-comment">// 2</span>
  <span class="hljs-keyword">let</span> inputData = keyboard.availableData
  <span class="hljs-comment">// 3</span>
  <span class="hljs-keyword">let</span> strData = <span class="hljs-type">String</span>(data: inputData, encoding: <span class="hljs-type">String</span>.<span class="hljs-type">Encoding</span>.utf8)!
  <span class="hljs-comment">// 4</span>
  <span class="hljs-keyword">return</span> strData.trimmingCharacters(<span class="hljs-keyword">in</span>: <span class="hljs-type">CharacterSet</span>.newlines)
}
</pre>
    <p>
        一步一步地看：
    </p>
    <ol>
        <li>
            首先，获取用来处理
            <code>
                stdin
            </code>
            的句柄。
        </li>
        <li>
            接下来，读取流中的全部数据。
        </li>
        <li>
            将data转换为字符串。
        </li>
        <li>
            最后，移除所有的换行符，并返回处理所得的字符串。
        </li>
    </ol>
    <p>
        接下来，打开
        <em>
            Panagram.swift
        </em>
        并添加下列方法到类中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">interactiveMode</span><span class="hljs-params">()</span></span> {
  <span class="hljs-comment">//1</span>
  consoleIO.writeMessage(<span class="hljs-string">"Welcome to Panagram. This program checks if an input string is an anagram or palindrome."</span>)
  <span class="hljs-comment">//2</span>
  <span class="hljs-keyword">var</span> shouldQuit = <span class="hljs-literal">false</span>
  <span class="hljs-keyword">while</span> !shouldQuit {
    <span class="hljs-comment">//3</span>
    consoleIO.writeMessage(<span class="hljs-string">"Type 'a' to check for anagrams or 'p' for palindromes type 'q' to quit."</span>)
    <span class="hljs-keyword">let</span> (option, value) = getOption(consoleIO.getInput())
    <span class="hljs-keyword">switch</span> option {
    <span class="hljs-keyword">case</span> .anagram:
      <span class="hljs-comment">//4</span>
      consoleIO.writeMessage(<span class="hljs-string">"Type the first string:"</span>)
      <span class="hljs-keyword">let</span> first = consoleIO.getInput()
      consoleIO.writeMessage(<span class="hljs-string">"Type the second string:"</span>)
      <span class="hljs-keyword">let</span> second = consoleIO.getInput()
      <span class="hljs-comment">//5</span>
      <span class="hljs-keyword">if</span> first.isAnagramOf(second) {
        consoleIO.writeMessage(<span class="hljs-string">"<span class="hljs-subst">\(second)</span> is an anagram of <span class="hljs-subst">\(first)</span>"</span>)
      } <span class="hljs-keyword">else</span> {
        consoleIO.writeMessage(<span class="hljs-string">"<span class="hljs-subst">\(second)</span> is not an anagram of <span class="hljs-subst">\(first)</span>"</span>)
      }
    <span class="hljs-keyword">case</span> .palindrome:
      consoleIO.writeMessage(<span class="hljs-string">"Type a word or sentence:"</span>)
      <span class="hljs-keyword">let</span> s = consoleIO.getInput()
      <span class="hljs-keyword">let</span> isPalindrome = s.isPalindrome()
      consoleIO.writeMessage(<span class="hljs-string">"<span class="hljs-subst">\(s)</span> is <span class="hljs-subst">\(isPalindrome ? "" : "not ")</span>a palindrome"</span>)
    <span class="hljs-keyword">default</span>:
      <span class="hljs-comment">//6</span>
      consoleIO.writeMessage(<span class="hljs-string">"Unknown option <span class="hljs-subst">\(value)</span>"</span>, to: .error)
    }
  }
}
</pre>
    <p>
        检查上述代码所做的事：
    </p>
    <ol>
        <li>
            首先，打印一条欢迎信息。
        </li>
        <li>
            <code>
                shouldQuit
            </code>
            breaks the infinite loop that is started in the next line.
        </li>
        <li>
            Prompt the user for input and convert it to one of the two options, if
            possible.
        </li>
        <li>
            If the option was for anagrams, prompt the user for the two strings to
            compare.
        </li>
        <li>
            Write the result out. The same logic flow applies to the palindrome option.
        </li>
        <li>
            If the user enters an unknown option, print an error and start the loop
            again.
        </li>
    </ol>
    <p>
        At the moment, you have no way to interrupt the
        <code>
            while
        </code>
        loop. In
        <em>
            Panagram.swift
        </em>
        add the following line to the
        <code>
            OptionType
        </code>
        enum:
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">case</span> quit = <span class="hljs-string">"q"</span>
</pre>
    <p>
        Next, add the following line to the enum's
        <code>
            init(_:)
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">case</span> <span class="hljs-string">"q"</span>: <span class="hljs-keyword">self</span> = .quit
</pre>
    <p>
        In the same file, add a
        <code>
            .quit
        </code>
        case to the
        <code>
            switch
        </code>
        statement inside
        <code>
            interactiveMode()
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">case</span> .quit:
  shouldQuit = <span class="hljs-literal">true</span>
</pre>
    <p>
        Then, change the
        <code>
            .unknown
        </code>
        case definition inside
        <code>
            staticMode()
        </code>
        as follows:
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">case</span> .unknown, .quit:
</pre>
    <p>
        Open
        <em>
            main.swift
        </em>
        and replace the comment
        <code>
            //TODO: Handle interactive mode
        </code>
        with the following:
    </p>
    <pre lang="swift" class="language-swift hljs">panagram.interactiveMode()
</pre>
    <p>
        To test interactive mode, you must not have any arguments defined in the
        Scheme.
    </p>
    <p>
        So, remove the two arguments you defined earlier. Select
        <em>
            Edit Scheme...
        </em>
        from the toolbar menu. Select each argument and then click the
        <em>
            -
        </em>
        sign under
        <em>
            Arguments Passed On Launch
        </em>
        . Once all arguments are deleted, click
        <em>
            Close
        </em>
        :
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/NoArguments.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/NoArguments-650x366.png"
            alt="" width="650" height="366" class="aligncenter size-large wp-image-165986"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/NoArguments-650x366.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/06/NoArguments-480x270.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/06/NoArguments-266x151.png 266w, https://koenig-media.raywenderlich.com/uploads/2017/06/NoArguments.png 898w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Build and run, and you'll see the following output in the Console:
    </p>
    <pre lang="" class="hljs cs">Welcome to Panagram. This program checks <span class="hljs-keyword">if</span> an input <span class="hljs-keyword">string</span> <span class="hljs-keyword">is</span> an anagram or palindrome.
Type <span class="hljs-string">'a'</span> to check <span class="hljs-keyword">for</span> anagrams or <span class="hljs-string">'p'</span> <span class="hljs-keyword">for</span> palindromes type <span class="hljs-string">'q'</span> to quit.
</pre>
    <p>
        Try out the different options. Type an option letter (do not prefix with
        a hyphen) followed by
        <em>
            Return
        </em>
        . You will be prompted for the arguments. Enter each value followed by
        <em>
            Return
        </em>
        . In the Console you should see something similar to this:
    </p>
    <pre lang="" class="hljs bash">a
Type the first string:
silent
Type the second string:
listen
listen is an anagram of silent
Type <span class="hljs-string">'a'</span> to check <span class="hljs-keyword">for</span> anagrams or <span class="hljs-string">'p'</span> <span class="hljs-keyword">for</span> palindromes <span class="hljs-built_in">type</span> <span class="hljs-string">'q'</span> to quit.
p
Type a word or sentence:
level
level is a palindrome
Type <span class="hljs-string">'a'</span> to check <span class="hljs-keyword">for</span> anagrams or <span class="hljs-string">'p'</span> <span class="hljs-keyword">for</span> palindromes <span class="hljs-built_in">type</span> <span class="hljs-string">'q'</span> to quit.
f
Error: Unknown option f
Type <span class="hljs-string">'a'</span> to check <span class="hljs-keyword">for</span> anagrams or <span class="hljs-string">'p'</span> <span class="hljs-keyword">for</span> palindromes <span class="hljs-built_in">type</span> <span class="hljs-string">'q'</span> to quit.
q
Program ended with <span class="hljs-built_in">exit</span> code: 0
</pre>
    <h2>
        Launching Outside Xcode
    </h2>
    <p>
        Normally, a command-line program is launched from a shell utility like
        Terminal (vs. launching it from an IDE like Xcode). The following section
        walks you through launching your app in Terminal.
    </p>
    <p>
        There are different ways to launch your program via Terminal. You could
        find the compiled binary using the Finder and start it directly via Terminal.
        Or, you could be lazy and tell Xcode to do this for you. First, you'll
        learn the lazy way.
    </p>
    <h3>
        Launch your app in Terminal from Xcode
    </h3>
    <p>
        Create a new scheme that will open Terminal and launch Panagram in the
        Terminal window. Click on the scheme named
        <em>
            Panagram
        </em>
        in the toolbar and select
        <em>
            New Scheme
        </em>
        :
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/SelectNewScheme.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/SelectNewScheme.png"
            alt="" width="152" height="88" class="aligncenter size-full wp-image-166001">
        </a>
    </p>
    <p>
        Name the new scheme
        <em>
            Panagram on Terminal
        </em>
        :
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/NameNewScheme.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/NameNewScheme.png"
            alt="" width="496" height="126" class="aligncenter size-full wp-image-166002"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/NameNewScheme.png 496w, https://koenig-media.raywenderlich.com/uploads/2017/06/NameNewScheme-480x122.png 480w"
            sizes="(max-width: 496px) 100vw, 496px">
        </a>
    </p>
    <p>
        Ensure the
        <em>
            Panagram on Terminal
        </em>
        scheme is selected as the active scheme. Click the scheme and select
        <em>
            Edit Scheme...
        </em>
        in the popover.
    </p>
    <p>
        Ensure that the
        <em>
            Info
        </em>
        tab is selected and then click on the
        <em>
            Executable
        </em>
        drop down and select
        <em>
            Other
        </em>
        . Now, find the
        <em>
            Terminal.app
        </em>
        in your
        <em>
            Applications/Utilities
        </em>
        folder and click
        <em>
            Choose
        </em>
        . Now that Terminal is your executable, uncheck
        <em>
            Debug executable
        </em>
        .
    </p>
    <p>
        Your
        <em>
            Panagram on Terminal
        </em>
        scheme's
        <em>
            Info
        </em>
        tab should look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/TerminalScheme.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/TerminalScheme-650x368.png"
            alt="" width="650" height="368" class="aligncenter size-large wp-image-166003"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/TerminalScheme-650x368.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/06/TerminalScheme-480x272.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/06/TerminalScheme-266x151.png 266w, https://koenig-media.raywenderlich.com/uploads/2017/06/TerminalScheme.png 899w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        The downside is that you can't debug your app in Xcode this way because
        now the executable that Xcode launches during a run is Terminal and not
        Panagram.
    </div>
    <p>
        Next, select the
        <em>
            Arguments
        </em>
        tab, then add one new argument:
    </p>
    <p>
        <code>
            ${BUILT_PRODUCTS_DIR}/${FULL_PRODUCT_NAME}
        </code>
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/passed_arguments2.png"
        rel="attachment wp-att-128051" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/passed_arguments2-480x118.png"
            alt="passed_arguments2" width="480" height="118" class="aligncenter size-medium wp-image-128051"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/passed_arguments2-480x118.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/passed_arguments2-768x189.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/passed_arguments2-700x172.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/passed_arguments2.png 1352w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Finally, click
        <em>
            Close
        </em>
        .
    </p>
    <p>
        Now, make sure you have the scheme
        <em>
            Panagram on Terminal
        </em>
        selected, then build and run your project. Xcode will open Terminal and
        pass through the path to your program. Terminal will then launch your program
        as you'd expect.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Finished_Program-e1458913657510-700x267.png"
        alt="Finished_Program" width="700" height="267" class="aligncenter size-large wp-image-128052"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Finished_Program-e1458913657510-700x267.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Finished_Program-e1458913657510-480x183.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Finished_Program-e1458913657510-768x292.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/Finished_Program-e1458913657510.png 1145w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h3>
        Launch your app directly from Terminal
    </h3>
    <p>
        Open Terminal from your
        <em>
            Applications/Utilities
        </em>
        folder.
    </p>
    <p>
        In the
        <em>
            Project Navigator
        </em>
        select your product under the
        <em>
            Products
        </em>
        group. Copy your debug folder's
        <em>
            Full Path
        </em>
        from Xcode's Utility area as shown below (do not include "Panagram"):
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/BuildFullPath.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/BuildFullPath-650x377.png"
            alt="" width="650" height="377" class="aligncenter size-large wp-image-166005"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/BuildFullPath-650x377.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/06/BuildFullPath-480x278.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/06/BuildFullPath.png 1044w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Open a Finder window and select the
        <em>
            Go/Go to Folder...
        </em>
        menu item and paste the full path you copied in the previous step into
        the dialog's text field:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/GoToFolder.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/GoToFolder.png"
            alt="" width="433" height="128" class="aligncenter size-full wp-image-166007">
        </a>
    </p>
    <p>
        Click
        <em>
            Go
        </em>
        and Finder navigates to the folder containing the Panagram executable:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/ExecutableInFinder.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/ExecutableInFinder-650x362.png"
            alt="" width="650" height="362" class="aligncenter size-large wp-image-166008"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/ExecutableInFinder-650x362.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/06/ExecutableInFinder-480x268.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/06/ExecutableInFinder.png 759w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Drag the Panagram executable from Finder to the Terminal window and drop
        it there. Switch to the Terminal window and hit
        <em>
            Return
        </em>
        on the keyboard. Terminal launches Panagram in interactive mode since
        no arguments were specified:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Finished_Program-e1458913657510-700x267.png"
        alt="Finished_Program" width="700" height="267" class="aligncenter size-large wp-image-128052"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Finished_Program-e1458913657510-700x267.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Finished_Program-e1458913657510-480x183.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Finished_Program-e1458913657510-768x292.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/Finished_Program-e1458913657510.png 1145w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        To run Panagram directly from Terminal in static mode, perform the same
        steps as described above for the interactive mode, but before hitting
        <em>
            Return
        </em>
        type the relevant arguments. For example:
        <em>
            -p level
        </em>
        or
        <em>
            -a silent listen
        </em>
        etc..
    </div>
    <h2>
        Displaying Errors
    </h2>
    <p>
        Finally, you will add some code to display error messages in red.
    </p>
    <p>
        Open
        <em>
            ConsoleIO.swift
        </em>
        and in
        <code>
            writeMessage(_:to:)
        </code>
        , replace the two
        <code>
            case
        </code>
        statements with the following:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            case
        </span>
        .standard:
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-built_in">
            print
        </span>
        (
        <span class="hljs-string">
            "\u{001B}[;m
            <span class="hljs-subst">
                \(message)
            </span>
            "
        </span>
        )
        <span class="hljs-keyword">
            case
        </span>
        .error:
        <span class="hljs-comment">
            // 2
        </span>
        fputs(
        <span class="hljs-string">
            "\u{001B}[0;31m
            <span class="hljs-subst">
                \(message)
            </span>
            \n"
        </span>
        , stderr)
    </pre>
    <p>
        Taking each numbered line in turn:
    </p>
    <ol>
        <li>
            The sequence
            <code>
                \u{001B}[;m
            </code>
            is used in the standard case to reset the terminal's text color back to
            the default.
        </li>
        <li>
            The sequence
            <code>
                \u{001B}[0;31m
            </code>
            are control characters that cause Terminal to change the color of the
            following text strings to red.
        </li>
    </ol>
    <div class="note">
        <em>
            Note:
        </em>
        When you run the Panagram scheme (and not the Terminal one), the
        <code>
            [;m
        </code>
        at the beginning of the output might look a bit awkward. That's because
        the Xcode Console doesn't support using control characters to colorize
        text output.
    </div>
    <p>
        Build and run, this will launch Panagram in Terminal. Type
        <em>
            f
        </em>
        for option, the
        <em>
            Unknown option f
        </em>
        error message will display in red:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Colored_Output-e1458912975895-700x216.png"
        alt="Colored_Output" width="700" height="216" class="aligncenter size-large wp-image-128048"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Colored_Output-e1458912975895-700x216.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Colored_Output-e1458912975895-480x148.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Colored_Output-e1458912975895-768x237.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/Colored_Output-e1458912975895.png 1145w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        Where to Go From Here?
    </h2>
    <div class="inline-video-ad" id="sub-banner-inline">
        <div class="inline-video-ad-wrapper">
            <a href="https://videos.raywenderlich.com/courses" sl-processed="1">
                <div class="col-wrapper">
                    <div class="col">
                        <img src="https://koenig-assets.raywenderlich.com/wp-content/themes/raywenderlich/images/global/video-yeti@2x.png"
                        alt="yeti holding videos">
                    </div>
                    <div class="col large-col">
                        <span>
                            Want to learn even faster? Save time with our
                            <span>
                                video courses
                            </span>
                        </span>
                    </div>
                </div>
            </a>
        </div>
    </div>
    <p>
        You can download the final project for this tutorial
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/Panagram_Final_170706.zip"
        sl-processed="1">
            here
        </a>
        .
    </p>
    <p>
        If you want to write more command-line programs in the future, take a
        look at how to redirect stderr to a log file and also look at
        <a href="http://www.gnu.org/software/ncurses/" sl-processed="1">
            ncurses
        </a>
        , which is a C library for writing "GUI-style" programs for the terminal.
    </p>
    <p>
        You can also check out the article
        <a href="http://krakendev.io/blog/scripting-in-swift" target="_blank"
        sl-processed="1">
            Scripting in Swift is pretty awesome
        </a>
        if you're interested in Swift for scripting.
    </p>
</div>