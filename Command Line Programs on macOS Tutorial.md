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
        的命令行工具。它会根据传入的选项，来检测给定的是否是回文或相同字母的异序词。它可以由预定义的参数启动，也可以运行在交互模式下，用户将会被提示输入要求的值。
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
        So far, you’ve learned what a command-line tool is, where the execution
        starts, how to send messages to
        <code>
            stdout
        </code>
        and
        <code>
            stderr
        </code>
        and how you can split your code into logical units to keep
        <em>
            main.swift
        </em>
        organized.
    </p>
    <p>
        In the next section, you’ll handle command-line arguments and complete
        the static mode of Panagram.
    </p>
    <h2>
        Command-Line Arguments
    </h2>
    <p>
        When you start a command-line program, everything you type after the name
        is passed as an argument to the program. Arguments can be separated with
        whitespace characters. Usually, you’ll run into two kind of arguments:
        <em>
            options
        </em>
        and
        <em>
            strings
        </em>
        .
    </p>
    <p>
        Options start with a dash followed by a character, or two dashes followed
        by a word. For example, many programs have the option
        <code>
            -h
        </code>
        or
        <code>
            --help
        </code>
        , the first being simply a shortcut for the second. To keep things simple,
        Panagram will only support the short version of options.
    </p>
    <p>
        Open
        <em>
            Panagram.swift
        </em>
        and add the following enum at the top of the file, outside the scope of
        the
        <code>
            Panagram
        </code>
        class:
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">let</span> panagram = <span class="hljs-type">Panagram</span>()
panagram.staticMode()
</pre>
    <p>
        This defines an
        <code>
            enum
        </code>
        with
        <code>
            String
        </code>
        as its base type so you can pass the option argument directly to
        <code>
            init(_:)
        </code>
        . Panagram has three options:
        <code>
            -p
        </code>
        to detect palindromes,
        <code>
            -a
        </code>
        for anagrams and
        <code>
            -h
        </code>
        to show the usage information. Everything else will be handled as an error.
    </p>
    <p>
        Next, add the following method to the
        <code>
            Panagram
        </code>
        class:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                getOption
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                option: String)
            </span>
        </span>
        -&gt; (option:
        <span class="hljs-type">
            OptionType
        </span>
        , value:
        <span class="hljs-type">
            String
        </span>
        ) {
        <span class="hljs-keyword">
            return
        </span>
        (
        <span class="hljs-type">
            OptionType
        </span>
        (value: option), option) }
    </pre>
    <p>
        The above method accepts an option argument as a
        <code>
            String
        </code>
        and returns a tuple of
        <code>
            OptionType
        </code>
        and
        <code>
            String
        </code>
        .
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        If you’re not yet familiar with Tuples in Swift, check out our video series
        on
        <em>
            Beginning Swift 3
        </em>
        , specifically
        <a href="https://videos.raywenderlich.com/courses/51-beginning-swift-3/lessons/5"
        target="_blank" sl-processed="1">
            PART 5: Tuples
        </a>
        .
    </div>
    <p>
        In the
        <code>
            Panagram
        </code>
        , class replace the contents of
        <code>
            staticMode()
        </code>
        with the following:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-comment">
            //1
        </span>
        <span class="hljs-keyword">
            let
        </span>
        argCount =
        <span class="hljs-type">
            CommandLine
        </span>
        .argc
        <span class="hljs-comment">
            //2
        </span>
        <span class="hljs-keyword">
            let
        </span>
        argument =
        <span class="hljs-type">
            CommandLine
        </span>
        .arguments[
        <span class="hljs-number">
            1
        </span>
        ]
        <span class="hljs-comment">
            //3
        </span>
        <span class="hljs-keyword">
            let
        </span>
        (option, value) = getOption(argument.substring(from: argument.index(argument.startIndex,
        offsetBy:
        <span class="hljs-number">
            1
        </span>
        )))
        <span class="hljs-comment">
            //4
        </span>
        consoleIO.writeMessage(
        <span class="hljs-string">
            "Argument count:
            <span class="hljs-subst">
                \(argCount)
            </span>
            Option:
            <span class="hljs-subst">
                \(option)
            </span>
            value:
            <span class="hljs-subst">
                \(value)
            </span>
            "
        </span>
        )
    </pre>
    <p>
        Here’s what’s going on in the code above:
    </p>
    <ol>
        <li>
            You first get the number of arguments passed to the program. Since the
            executable path is always passed in (as
            <code>
                CommandLine.arguments[0]
            </code>
            ), the count value will always be greater than or equal to 1.
        </li>
        <li>
            Next, take the first “real” argument (the option argument) from the
            <code>
                arguments
            </code>
            array.
        </li>
        <li>
            Then you parse the argument and convert it to an
            <code>
                OptionType
            </code>
            . The
            <code>
                index(_:offsetBy:)
            </code>
            method is simply skipping the first character in the argument’s string,
            which in this case is the hyphen (`-`) character before the option.
        </li>
        <li>
            Finally, you log the parsing results to the Console.
        </li>
    </ol>
    <p>
        In
        <em>
            main.swift
        </em>
        , replace the line
        <code>
            panagram.staticMode()
        </code>
        with the following:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            if
        </span>
        <span class="hljs-type">
            CommandLine
        </span>
        .argc &lt;
        <span class="hljs-number">
            2
        </span>
        {
        <span class="hljs-comment">
            //
            <span class="hljs-doctag">
                TODO:
            </span>
            Handle interactive mode
        </span>
        }
        <span class="hljs-keyword">
            else
        </span>
        { panagram.staticMode() }
    </pre>
    <p>
        If your program is invoked with fewer than 2 arguments, then you're going
        to start interactive mode - you'll do this part later. Otherwise, you use
        the non-interactive static mode.
    </p>
    <p>
        You now need to figure out how to pass arguments to your command-line
        tool from within Xcode. To do this, click on the
        <em>
            Scheme
        </em>
        named
        <em>
            Panagram
        </em>
        in the
        <em>
            Toolbar
        </em>
        :
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/Scheme.png"
        rel="attachment wp-att-128043" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Scheme.png"
            alt="Scheme" width="316" height="46" class="aligncenter size-full wp-image-128043">
        </a>
    </p>
    <p>
        Select
        <em>
            Edit Scheme...
        </em>
        from the menu that appears:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/Edit_Scheme.png"
        rel="attachment wp-att-128044" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Edit_Scheme.png"
            alt="Edit_Scheme" width="310" height="172" class="aligncenter size-full wp-image-128044">
        </a>
    </p>
    <p>
        Ensure
        <em>
            Run
        </em>
        is selected in the left pane, click the
        <em>
            Arguments
        </em>
        tab, then click the
        <em>
            +
        </em>
        sign under
        <em>
            Arguments Passed On Launch
        </em>
        . Add
        <code>
            -p
        </code>
        as argument and click
        <em>
            Close
        </em>
        :
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Scheme_Settings-700x394.png"
        alt="Scheme_Settings" width="700" height="394" class="aligncenter size-large wp-image-128046"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Scheme_Settings-700x394.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Scheme_Settings-480x270.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Scheme_Settings-768x432.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/Scheme_Settings-266x151.png 266w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Now build and run, and you'll see the following output in the Console:
    </p>
    <pre lang="" class="hljs bash">
        Argument count: 2 Option: Palindrome value: p Program ended with
        <span class="hljs-built_in">
            exit
        </span>
        code: 0
    </pre>
    <p>
        So far, you've added a basic option system to your tool, learned how to
        handle command-line arguments and how to pass arguments from within Xcode.
    </p>
    <p>
        Next up, you'll build the main functionality of Panagram.
    </p>
    <h2>
        Anagrams and Palindromes
    </h2>
    <p>
        Before you can write any code to detect palindromes or anagrams, you should
        be clear on what they are!
    </p>
    <p>
        <a href="https://en.wikipedia.org/wiki/Palindrome" sl-processed="1">
            Palindromes
        </a>
        are words or sentences that read the same backwards and forwards. Here
        are some examples:
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
        As you can see, capitalization and punctuation are often ignored. To keep
        things simple, Panagram will ignore capitalization and white spaces, but
        will not handle punctuation.
    </p>
    <p>
        <a href="https://en.wikipedia.org/wiki/Anagram" sl-processed="1">
            Anagrams
        </a>
        are words or sentences that are built using the characters of other words
        or sentences. Some examples are:
    </p>
    <ul>
        <li>
            silent &lt;-&gt; listen
        </li>
        <li>
            Bolivia &lt;-&gt; Lobivia (it's a cactus from Bolivia)
        </li>
    </ul>
    <p>
        You'll encapsulate the detection logic inside a small extension to
        <code>
            String
        </code>
        .
    </p>
    <p>
        Create a new file named
        <em>
            StringExtension.swift
        </em>
        and add the following code to it:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-class">
            <span class="hljs-keyword">
                extension
            </span>
            <span class="hljs-title">
                String
            </span>
        </span>
        { }
    </pre>
    <p>
        Time for a bit of design work. First, how to detect an anagram:
    </p>
    <ol>
        <li>
            Ignore capitalization and whitespace for both strings.
        </li>
        <li>
            Check that both strings contain the same characters, and that all characters
            appear the same number of times.
        </li>
    </ol>
    <p>
        Add the following method to
        <em>
            StringExtension.swift
        </em>
        :
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                isAnagramOf
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                s: String)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            Bool
        </span>
        {
        <span class="hljs-comment">
            //1
        </span>
        <span class="hljs-keyword">
            let
        </span>
        lowerSelf =
        <span class="hljs-keyword">
            self
        </span>
        .lowercased().replacingOccurrences(of:
        <span class="hljs-string">
            " "
        </span>
        , with:
        <span class="hljs-string">
            ""
        </span>
        )
        <span class="hljs-keyword">
            let
        </span>
        lowerOther = s.lowercased().replacingOccurrences(of:
        <span class="hljs-string">
            " "
        </span>
        , with:
        <span class="hljs-string">
            ""
        </span>
        )
        <span class="hljs-comment">
            //2
        </span>
        <span class="hljs-keyword">
            return
        </span>
        lowerSelf.sorted() == lowerOther.sorted() }
    </pre>
    <p>
        Taking a closer look at the algorithm above:
    </p>
    <ol>
        <li>
            First, you remove capitalization and whitespace from both Strings.
        </li>
        <li>
            Then you sort and compare the characters.
        </li>
    </ol>
    <p>
        Detecting palindromes is simple as well:
    </p>
    <ol>
        <li>
            Ignore all capitalization and whitespace.
        </li>
        <li>
            Reverse the string and compare; if it's the same, then you have a palindrome.
        </li>
    </ol>
    <p>
        Add the following method to detect palindromes:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                isPalindrome
            </span>
            <span class="hljs-params">
                ()
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            Bool
        </span>
        {
        <span class="hljs-comment">
            //1
        </span>
        <span class="hljs-keyword">
            let
        </span>
        f =
        <span class="hljs-keyword">
            self
        </span>
        .lowercased().replacingOccurrences(of:
        <span class="hljs-string">
            " "
        </span>
        , with:
        <span class="hljs-string">
            ""
        </span>
        )
        <span class="hljs-comment">
            //2
        </span>
        <span class="hljs-keyword">
            let
        </span>
        s =
        <span class="hljs-type">
            String
        </span>
        (f.reversed())
        <span class="hljs-comment">
            //3
        </span>
        <span class="hljs-keyword">
            return
        </span>
        f == s }
    </pre>
    <p>
        The logic here is quite straightforward:
    </p>
    <ol>
        <li>
            Remove capitalization and whitespace.
        </li>
        <li>
            Create a second string with the reversed characters.
        </li>
        <li>
            If they are equal, it is a palindrome.
        </li>
    </ol>
    <p>
        Time to pull this all together and help Panagram do its job.
    </p>
    <p>
        Open
        <em>
            Panagram.swift
        </em>
        and replace the call to
        <code>
            writeMessage(_:to:)
        </code>
        in
        <code>
            staticMode()
        </code>
        with the following:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-comment">
            //1
        </span>
        <span class="hljs-keyword">
            switch
        </span>
        option {
        <span class="hljs-keyword">
            case
        </span>
        .anagram:
        <span class="hljs-comment">
            //2
        </span>
        <span class="hljs-keyword">
            if
        </span>
        argCount !=
        <span class="hljs-number">
            4
        </span>
        {
        <span class="hljs-keyword">
            if
        </span>
        argCount &gt;
        <span class="hljs-number">
            4
        </span>
        { consoleIO.writeMessage(
        <span class="hljs-string">
            "Too many arguments for option
            <span class="hljs-subst">
                \(option.rawValue)
            </span>
            "
        </span>
        , to: .error) }
        <span class="hljs-keyword">
            else
        </span>
        { consoleIO.writeMessage(
        <span class="hljs-string">
            "Too few arguments for option
            <span class="hljs-subst">
                \(option.rawValue)
            </span>
            "
        </span>
        , to: .error) } consoleIO.printUsage() }
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-comment">
            //3
        </span>
        <span class="hljs-keyword">
            let
        </span>
        first =
        <span class="hljs-type">
            CommandLine
        </span>
        .arguments[
        <span class="hljs-number">
            2
        </span>
        ]
        <span class="hljs-keyword">
            let
        </span>
        second =
        <span class="hljs-type">
            CommandLine
        </span>
        .arguments[
        <span class="hljs-number">
            3
        </span>
        ]
        <span class="hljs-keyword">
            if
        </span>
        first.isAnagramOf(second) { consoleIO.writeMessage(
        <span class="hljs-string">
            "
            <span class="hljs-subst">
                \(second)
            </span>
            is an anagram of
            <span class="hljs-subst">
                \(first)
            </span>
            "
        </span>
        ) }
        <span class="hljs-keyword">
            else
        </span>
        { consoleIO.writeMessage(
        <span class="hljs-string">
            "
            <span class="hljs-subst">
                \(second)
            </span>
            is not an anagram of
            <span class="hljs-subst">
                \(first)
            </span>
            "
        </span>
        ) } }
        <span class="hljs-keyword">
            case
        </span>
        .palindrome:
        <span class="hljs-comment">
            //4
        </span>
        <span class="hljs-keyword">
            if
        </span>
        argCount !=
        <span class="hljs-number">
            3
        </span>
        {
        <span class="hljs-keyword">
            if
        </span>
        argCount &gt;
        <span class="hljs-number">
            3
        </span>
        { consoleIO.writeMessage(
        <span class="hljs-string">
            "Too many arguments for option
            <span class="hljs-subst">
                \(option.rawValue)
            </span>
            "
        </span>
        , to: .error) }
        <span class="hljs-keyword">
            else
        </span>
        { consoleIO.writeMessage(
        <span class="hljs-string">
            "Too few arguments for option
            <span class="hljs-subst">
                \(option.rawValue)
            </span>
            "
        </span>
        , to: .error) } consoleIO.printUsage() }
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-comment">
            //5
        </span>
        <span class="hljs-keyword">
            let
        </span>
        s =
        <span class="hljs-type">
            CommandLine
        </span>
        .arguments[
        <span class="hljs-number">
            2
        </span>
        ]
        <span class="hljs-keyword">
            let
        </span>
        isPalindrome = s.isPalindrome() consoleIO.writeMessage(
        <span class="hljs-string">
            "
            <span class="hljs-subst">
                \(s)
            </span>
            is
            <span class="hljs-subst">
                \(isPalindrome ? "" : "not ")
            </span>
            a palindrome"
        </span>
        ) }
        <span class="hljs-comment">
            //6
        </span>
        <span class="hljs-keyword">
            case
        </span>
        .help: consoleIO.printUsage()
        <span class="hljs-keyword">
            case
        </span>
        .unknown:
        <span class="hljs-comment">
            //7
        </span>
        consoleIO.writeMessage(
        <span class="hljs-string">
            "Unknown option
            <span class="hljs-subst">
                \(value)
            </span>
            "
        </span>
        ) consoleIO.printUsage() }
    </pre>
    <p>
        Going through the above code step-by-step:
    </p>
    <ol>
        <li>
            First, switch based on what argument you were passed, to determine what
            operation will be performed.
        </li>
        <li>
            In the case of an anagram, there must be four command-line arguments passed
            in. The first is the executable path, the second the
            <code>
                -a
            </code>
            option and finally the two strings to check. If you don't have four arguments,
            then print an error message.
        </li>
        <li>
            If the argument count is good, store the two strings in local variables,
            check them to see if they are anagrams of each other, and print the result.
        </li>
        <li>
            In the case of a palindrome, you must have three arguments. The first
            is the executable path, the second is the
            <code>
                -p
            </code>
            option and finally the string to check. If you don't have three arguments,
            then print an error message.
        </li>
        <li>
            Check the string to see if it is a palindrome and print the result.
        </li>
        <li>
            If the
            <code>
                -h
            </code>
            option was passed in, then print the usage information.
        </li>
        <li>
            If an unknown option is passed, print the usage information.
        </li>
    </ol>
    <p>
        Now, modify the arguments inside the scheme. For example, to use the
        <code>
            -p
        </code>
        option you must pass two arguments (in addition to the first argument,
        the executable's path, which is always passed implicitly).
    </p>
    <p>
        Select
        <em>
            Edit Scheme...
        </em>
        from the Set Active Scheme toolbar item, and add a second argument with
        the value "
        <em>
            level
        </em>
        " as shown below:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Bildschirmfoto-2016-03-05-um-13.25.10-700x393.png"
        alt="p-option-settings" width="700" height="393" class="aligncenter size-large wp-image-128047"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Bildschirmfoto-2016-03-05-um-13.25.10-700x393.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Bildschirmfoto-2016-03-05-um-13.25.10-480x270.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Bildschirmfoto-2016-03-05-um-13.25.10-768x431.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Build and run, and you'll see the following output in the console:
    </p>
    <pre lang="" class="hljs bash">
        level is a palindrome Program ended with
        <span class="hljs-built_in">
            exit
        </span>
        code: 0
    </pre>
    <h2>
        Handle Input Interactively
    </h2>
    <p>
        Now that you have a basic version of Panagram working, you can make it
        even more useful by adding the ability to type in the arguments interactively
        via the input stream.
    </p>
    <p>
        In this section, you will add code so when Panagram is started without
        arguments, it will open in interactive mode and prompt the user for the
        input it needs.
    </p>
    <p>
        First, you need a way to get input from the keyboard.
        <code>
            stdin
        </code>
        is attached to the keyboard and is therefore a way for you to collect
        input from users interactively.
    </p>
    <p>
        Open
        <em>
            ConsoleIO.swift
        </em>
        and add the following method to the class:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                getInput
            </span>
            <span class="hljs-params">
                ()
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            String
        </span>
        {
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-keyword">
            let
        </span>
        keyboard =
        <span class="hljs-type">
            FileHandle
        </span>
        .standardInput
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-keyword">
            let
        </span>
        inputData = keyboard.availableData
        <span class="hljs-comment">
            // 3
        </span>
        <span class="hljs-keyword">
            let
        </span>
        strData =
        <span class="hljs-type">
            String
        </span>
        (data: inputData, encoding:
        <span class="hljs-type">
            String
        </span>
        .
        <span class="hljs-type">
            Encoding
        </span>
        .utf8)!
        <span class="hljs-comment">
            // 4
        </span>
        <span class="hljs-keyword">
            return
        </span>
        strData.trimmingCharacters(
        <span class="hljs-keyword">
            in
        </span>
        :
        <span class="hljs-type">
            CharacterSet
        </span>
        .newlines) }
    </pre>
    <p>
        Taking each numbered section in turn:
    </p>
    <ol>
        <li>
            First, grab a handle to
            <code>
                stdin
            </code>
            .
        </li>
        <li>
            Next, read any data on the stream.
        </li>
        <li>
            Convert the data to a string.
        </li>
        <li>
            Finally, remove any newline characters and return the string.
        </li>
    </ol>
    <p>
        Next, open
        <em>
            Panagram.swift
        </em>
        and add the following method to the class:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                interactiveMode
            </span>
            <span class="hljs-params">
                ()
            </span>
        </span>
        {
        <span class="hljs-comment">
            //1
        </span>
        consoleIO.writeMessage(
        <span class="hljs-string">
            "Welcome to Panagram. This program checks if an input string is an anagram
            or palindrome."
        </span>
        )
        <span class="hljs-comment">
            //2
        </span>
        <span class="hljs-keyword">
            var
        </span>
        shouldQuit =
        <span class="hljs-literal">
            false
        </span>
        <span class="hljs-keyword">
            while
        </span>
        !shouldQuit {
        <span class="hljs-comment">
            //3
        </span>
        consoleIO.writeMessage(
        <span class="hljs-string">
            "Type 'a' to check for anagrams or 'p' for palindromes type 'q' to quit."
        </span>
        )
        <span class="hljs-keyword">
            let
        </span>
        (option, value) = getOption(consoleIO.getInput())
        <span class="hljs-keyword">
            switch
        </span>
        option {
        <span class="hljs-keyword">
            case
        </span>
        .anagram:
        <span class="hljs-comment">
            //4
        </span>
        consoleIO.writeMessage(
        <span class="hljs-string">
            "Type the first string:"
        </span>
        )
        <span class="hljs-keyword">
            let
        </span>
        first = consoleIO.getInput() consoleIO.writeMessage(
        <span class="hljs-string">
            "Type the second string:"
        </span>
        )
        <span class="hljs-keyword">
            let
        </span>
        second = consoleIO.getInput()
        <span class="hljs-comment">
            //5
        </span>
        <span class="hljs-keyword">
            if
        </span>
        first.isAnagramOf(second) { consoleIO.writeMessage(
        <span class="hljs-string">
            "
            <span class="hljs-subst">
                \(second)
            </span>
            is an anagram of
            <span class="hljs-subst">
                \(first)
            </span>
            "
        </span>
        ) }
        <span class="hljs-keyword">
            else
        </span>
        { consoleIO.writeMessage(
        <span class="hljs-string">
            "
            <span class="hljs-subst">
                \(second)
            </span>
            is not an anagram of
            <span class="hljs-subst">
                \(first)
            </span>
            "
        </span>
        ) }
        <span class="hljs-keyword">
            case
        </span>
        .palindrome: consoleIO.writeMessage(
        <span class="hljs-string">
            "Type a word or sentence:"
        </span>
        )
        <span class="hljs-keyword">
            let
        </span>
        s = consoleIO.getInput()
        <span class="hljs-keyword">
            let
        </span>
        isPalindrome = s.isPalindrome() consoleIO.writeMessage(
        <span class="hljs-string">
            "
            <span class="hljs-subst">
                \(s)
            </span>
            is
            <span class="hljs-subst">
                \(isPalindrome ? "" : "not ")
            </span>
            a palindrome"
        </span>
        )
        <span class="hljs-keyword">
            default
        </span>
        :
        <span class="hljs-comment">
            //6
        </span>
        consoleIO.writeMessage(
        <span class="hljs-string">
            "Unknown option
            <span class="hljs-subst">
                \(value)
            </span>
            "
        </span>
        , to: .error) } } }
    </pre>
    <p>
        Taking a look at what's going on above:
    </p>
    <ol>
        <li>
            First, print a welcome message.
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
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            case
        </span>
        quit =
        <span class="hljs-string">
            "q"
        </span>
    </pre>
    <p>
        Next, add the following line to the enum's
        <code>
            init(_:)
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            case
        </span>
        <span class="hljs-string">
            "q"
        </span>
        :
        <span class="hljs-keyword">
            self
        </span>
        = .quit
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
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            case
        </span>
        .quit: shouldQuit =
        <span class="hljs-literal">
            true
        </span>
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
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            case
        </span>
        .unknown, .quit:
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
    <pre lang="swift" class="language-swift hljs">
        panagram.interactiveMode()
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
    <pre lang="" class="hljs cs">
        Welcome to Panagram. This program checks
        <span class="hljs-keyword">
            if
        </span>
        an input
        <span class="hljs-keyword">
            string
        </span>
        <span class="hljs-keyword">
            is
        </span>
        an anagram or palindrome. Type
        <span class="hljs-string">
            'a'
        </span>
        to check
        <span class="hljs-keyword">
            for
        </span>
        anagrams or
        <span class="hljs-string">
            'p'
        </span>
        <span class="hljs-keyword">
            for
        </span>
        palindromes type
        <span class="hljs-string">
            'q'
        </span>
        to quit.
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
    <pre lang="" class="hljs bash">
        a Type the first string: silent Type the second string: listen listen
        is an anagram of silent Type
        <span class="hljs-string">
            'a'
        </span>
        to check
        <span class="hljs-keyword">
            for
        </span>
        anagrams or
        <span class="hljs-string">
            'p'
        </span>
        <span class="hljs-keyword">
            for
        </span>
        palindromes
        <span class="hljs-built_in">
            type
        </span>
        <span class="hljs-string">
            'q'
        </span>
        to quit. p Type a word or sentence: level level is a palindrome Type
        <span class="hljs-string">
            'a'
        </span>
        to check
        <span class="hljs-keyword">
            for
        </span>
        anagrams or
        <span class="hljs-string">
            'p'
        </span>
        <span class="hljs-keyword">
            for
        </span>
        palindromes
        <span class="hljs-built_in">
            type
        </span>
        <span class="hljs-string">
            'q'
        </span>
        to quit. f Error: Unknown option f Type
        <span class="hljs-string">
            'a'
        </span>
        to check
        <span class="hljs-keyword">
            for
        </span>
        anagrams or
        <span class="hljs-string">
            'p'
        </span>
        <span class="hljs-keyword">
            for
        </span>
        palindromes
        <span class="hljs-built_in">
            type
        </span>
        <span class="hljs-string">
            'q'
        </span>
        to quit. q Program ended with
        <span class="hljs-built_in">
            exit
        </span>
        code: 0
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
    <p>
        I hope you enjoyed this Command Line Programs on macOS tutorial; if you
        have any questions or comments, feel free to join the forum discussion
        below!
    </p>
</div>