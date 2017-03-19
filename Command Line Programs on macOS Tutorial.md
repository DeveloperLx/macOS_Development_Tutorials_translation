# macOS教程：命令行程序

#### [原文地址](https://www.raywenderlich.com/128039/command-line-programs-macos-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div class="note">
        <p>
            <em>
                Update 9/22/16:
            </em>
            This tutorial has been updated for Xcode 8 and Swift 3.
        </p>
    </div>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/CommandLinePrograms-feature-250x250.png"
        alt="CommandLinePrograms-feature" width="250" height="250" class="alignright size-thumbnail wp-image-129951"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/CommandLinePrograms-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/03/CommandLinePrograms-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/03/CommandLinePrograms-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/03/CommandLinePrograms-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/03/CommandLinePrograms-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/03/CommandLinePrograms-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/03/CommandLinePrograms-feature-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
        Not so long ago, before the advent of graphical user interfaces, command-line
        programs were the primary method for interacting with computers. Despite
        the prevalence of GUIs, command-line programs still have an important role
        in today’s computing world. Command-line programs such as
        <a href="http://www.imagemagick.org/script/command-line-processing.php"
        target="_blank" sl-processed="1">
            ImageMagick
        </a>
        or
        <a href="https://www.ffmpeg.org/" target="_blank" sl-processed="1">
            ffmpeg
        </a>
        are important in the server world. In fact, the majority of the servers
        that form the Internet run only command-line programs.
    </p>
    <p>
        Even Xcode uses command-line programs! When Xcode builds your project,
        it calls
        <em>
            <a href="https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/xcodebuild.1.html"
            target="_blank" sl-processed="1">
                xcodebuild
            </a>
        </em>
        , which does the actual building. If the building process was baked-in
        to the Xcode product, continuous integration solutions would be hard to
        achieve — if not impossible!
    </p>
    <p>
        In this command line programs on macOS tutorial you will write a command-line
        utilty named
        <em>
            Panagram
        </em>
        . Depending on the options passed in, it will detect if a given input
        is a palindrome or anagram. It can be started with arguments or run in
        interactive mode without arguments.
    </p>
    <h2>
        Getting Started
    </h2>
    <p>
        Swift seems like an odd choice for creating a command-line program, as
        languages like C, Perl, Ruby or Java are a more traditional choice. But
        there are some great reasons to choose Swift for your command-line needs:
    </p>
    <ul>
        <li>
            Swift can be used as an interpreted scripting language, as well as a compiled
            language. This gives you the advantages of scripting languages, such as
            zero compile times and ease of maintenance, along with the choice of compiling
            your app to improve execution time or to bundle it for sale to the public.
        </li>
        <li>
            You don’t need to switch languages. Many people say that a programmer
            should learn one new language every year. This is not a bad idea, but if
            you are already used to Swift and its standard library, you can reduce
            the time investment by sticking with Swift.
        </li>
    </ul>
    <p>
        In this command line programs for macOS tutorial, you’ll create a classic
        compiled project.
    </p>
    <p>
        Open Xcode and go to
        <em>
            File\New\Project
        </em>
        . Find the macOS group, select
        <em>
            Application\Command Line Tool
        </em>
        and click
        <em>
            Next
        </em>
        :
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/05/Bildschirmfoto-2016-09-22-um-11.53.38.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/05/Bildschirmfoto-2016-09-22-um-11.53.38-452x320.png"
            alt="Create_command_line_tool" width="452" height="320" class="aligncenter size-medium wp-image-144371"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/05/Bildschirmfoto-2016-09-22-um-11.53.38-452x320.png 452w, https://koenig-media.raywenderlich.com/uploads/2016/05/Bildschirmfoto-2016-09-22-um-11.53.38-650x460.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/05/Bildschirmfoto-2016-09-22-um-11.53.38.png 1458w"
            sizes="(max-width: 452px) 100vw, 452px">
        </a>
    </p>
    <p>
        For
        <em>
            Product Name
        </em>
        , enter
        <em>
            Panagram
        </em>
        . Make sure that
        <em>
            Language
        </em>
        is set to
        <em>
            Swift
        </em>
        , then click
        <em>
            Next
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/Project_Settings.png"
        rel="attachment wp-att-128041" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Project_Settings-450x320.png"
            alt="Project_Settings" width="450" height="320" class="aligncenter size-medium wp-image-128041"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Project_Settings-450x320.png 450w, https://koenig-media.raywenderlich.com/uploads/2016/03/Project_Settings-768x546.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/Project_Settings-700x498.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Project_Settings.png 1462w"
            sizes="(max-width: 450px) 100vw, 450px">
        </a>
    </p>
    <p>
        Choose a location on your disk to save your project and click
        <em>
            Create
        </em>
        .
    </p>
    <p>
        Many C-like languages have a
        <code>
            main
        </code>
        function that serves as the entry point — i.e. the code that the operating
        system will call when the program is executed. This means the program execution
        starts with the first line of this function. Swift doesn’t have a
        <code>
            main
        </code>
        function; instead, it has a
        <em>
            main file
        </em>
        .
    </p>
    <p>
        When you run your project, the first line inside that file that isn’t
        a method or class declaration is the first one to execute. It’s a good
        idea to keep your
        <em>
            main.swift
        </em>
        file as clean as possible and put all your classes and structs in their
        own files. This keeps things streamlined and helps you to understand the
        <em>
            main execution path
        </em>
        .
    </p>
    <p>
        Press
        <em>
            Cmd + N
        </em>
        to create a new file. Under
        <em>
            macOS
        </em>
        , select
        <em>
            Source\Swift File
        </em>
        and press
        <em>
            Next
        </em>
        :
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/05/Bildschirmfoto-2016-09-22-um-11.55.53.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/05/Bildschirmfoto-2016-09-22-um-11.55.53-454x320.png"
            alt="File_selection" width="454" height="320" class="aligncenter size-medium wp-image-144372"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/05/Bildschirmfoto-2016-09-22-um-11.55.53-454x320.png 454w, https://koenig-media.raywenderlich.com/uploads/2016/05/Bildschirmfoto-2016-09-22-um-11.55.53-650x459.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/05/Bildschirmfoto-2016-09-22-um-11.55.53.png 730w"
            sizes="(max-width: 454px) 100vw, 454px">
        </a>
    </p>
    <p>
        Save the file as
        <em>
            ConsoleIO.swift
        </em>
        and open it. You’ll wrap all the input and output elements in a small,
        handy class.
    </p>
    <p>
        Add the following code to
        <em>
            ConsoleIO.swift
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1280391">
                    <td class="code" id="p128039code1">
                        <pre class="swift" style="font-family:monospace;">
                            class ConsoleIO { class func printUsage() { let executableName = (CommandLine.arguments[0]
                            as NSString).lastPathComponent &nbsp; print("usage:") print("\(executableName)
                            -a string1 string2") print("or") print("\(executableName) -p string") print("or")
                            print("\(executableName) -h to show usage information") print("Type \(executableName)
                            without an option to enter interactive mode.") } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This code creates a class
        <code>
            ConsoleIO
        </code>
        and a class method that prints usage information to the console. Every
        time you run a program, the path to the executable is implicitly passed
        as argument [0] and accessible through the global
        <code>
            CommandLine
        </code>
        enum.
        <code>
            CommandLine
        </code>
        is a small wrapper around the
        <code>
            argc
        </code>
        and
        <code>
            argv
        </code>
        arguments you may know from C-like languages.
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        It is common practice to print a usage statement to the console when the
        user tries to start a command-line program with incorrect arguments.
    </div>
    <p>
        Create another new Swift file named
        <em>
            Panagram.swift
        </em>
        and add the following code to it:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1280392">
                    <td class="code" id="p128039code2">
                        <pre class="swift" style="font-family:monospace;">
                            class Panagram { func staticMode() { ConsoleIO.printUsage() } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This creates a class
        <code>
            Panagram
        </code>
        that has one method. The class will handle the program logic, with
        <code>
            staticMode()
        </code>
        representing non-interactive mode — i.e. when you provide all data through
        command line arguments. For now, it simply prints the usage information.
    </p>
    <p>
        Now open
        <em>
            main.swift
        </em>
        and replace the
        <code>
            print
        </code>
        statement with the following code:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1280393">
                    <td class="code" id="p128039code3">
                        <pre class="swift" style="font-family:monospace;">
                            let panagram = Panagram() panagram.staticMode()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run your project; you’ll see the following output in Xcode’s
        console:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1280394">
                    <td class="code" id="p128039code4">
                        <pre class="text" style="font-family:monospace;">
                            usage: Panagram -a string1 string2 or Panagram -p string or Panagram -h
                            to show usage information Type Panagram without an option to enter interactive
                            mode. Program ended with exit code: 0
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        So far, you’ve learned what a command-line tool is, where the execution
        starts and how you can split your code into logical units to keep
        <em>
            main.swift
        </em>
        organized.
    </p>
    <p>
        In the next section, you’ll handle command-line arguments and complete
        the static mode of
        <em>
            Panagram
        </em>
        .
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
        <em>
            Panagram
        </em>
        will only support the short version of options.
    </p>
    <p>
        Open
        <em>
            ConsoleIO.swift
        </em>
        and add the following enum above the
        <code>
            ConsoleIO
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1280395">
                    <td class="code" id="p128039code5">
                        <pre class="swift" style="font-family:monospace;">
                            enum OptionType: String { case palindrome = "p" case anagram = "a" case
                            help = "h" case unknown &nbsp; init(value: String) { switch value { case
                            "a": self = .anagram case "p": self = .palindrome case "h": self = .help
                            default: self = .unknown } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This creates an
        <code>
            enum
        </code>
        with
        <code>
            String
        </code>
        as its base type so you can pass the command-line arguments directly to
        <code>
            init(_:)
        </code>
        .
        <em>
            Panagram
        </em>
        has three options:
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
            ConsoleIO
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1280396">
                    <td class="code" id="p128039code6">
                        <pre class="swift" style="font-family:monospace;">
                            func getOption(- option: String) -&gt; (option:OptionType, value: String)
                            { return (OptionType(value: option), option) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The above method accepts a
        <code>
            String
        </code>
        as its argument and returns a tuple of
        <code>
            OptionType
        </code>
        and
        <code>
            String
        </code>
        .
    </p>
    <p>
        Open
        <em>
            Panagram.swift
        </em>
        and add the following property to the class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1280397">
                    <td class="code" id="p128039code7">
                        <pre class="swift" style="font-family:monospace;">
                            let consoleIO = ConsoleIO()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Then replace the content of
        <code>
            staticMode()
        </code>
        with the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1280398">
                    <td class="code" id="p128039code8">
                        <pre class="swift" style="font-family:monospace;">
                            //1 let argCount = CommandLine.argc //2 let argument = CommandLine.arguments[1]
                            //3 let (option, value) = consoleIO.getOption(argument.substring(from:
                            argument.characters.index(argument.startIndex, offsetBy: 1))) //4 print("Argument
                            count: \(argCount) Option: \(option) value: \(value)")
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s what’s going on in the code above:
    </p>
    <ol>
        <li>
            You first get the number of arguments passed to the program. Since the
            executable path is always passed in, this value will always be greater
            than or equal to 1.
        </li>
        <li>
            Next, take the first “real” argument from the
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
            .
        </li>
        <li>
            Finally, you log the parsing results to the console.
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1280399">
                    <td class="code" id="p128039code9">
                        <pre class="swift" style="font-family:monospace;">
                            if CommandLine.argc &lt; 2 { //Handle interactive mode } else { panagram.staticMode()
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        If your program is invoked with fewer than 2 arguments, then you’re going
        to start interactive mode. Otherwise you use the non-interactive static
        mode.
    </p>
    <p>
        You now need to figure out how to pass
        <em>
            arguments
        </em>
        to your command-line tool from within
        <em>
            Xcode
        </em>
        . To do this, click on the
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
            Edit Scheme…
        </em>
        in the popover that appears:
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
        is selected, click the
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
        <em>
            -p
        </em>
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
        Now run your project, and you’ll see the following output in the console:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803910">
                    <td class="code" id="p128039code10">
                        <pre class="text" style="font-family:monospace;">
                            Argument count: 2 Option: Palindrome value: p Program ended with exit
                            code: 0
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        So far, you’ve added a basic option system to your tool, learned how to
        handle command-line arguments and how to pass arguments from within Xcode.
    </p>
    <p>
        Next up, you’ll build up the main functionality of Panagram.
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
            A man, a plan, a canal – Panama!
        </li>
    </ul>
    <p>
        As you can see, capitalization and punctuation are often ignored.
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
            Bolivia &lt;-&gt; Lobivia (it’s a cactus from Bolivia)
        </li>
    </ul>
    <p>
        You’ll encapsulate the detection logic inside a small extension to
        <code>
            String
        </code>
        .
    </p>
    <p>
        Create a new file
        <em>
            StringExtension.swift
        </em>
        and add the following code to it:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803911">
                    <td class="code" id="p128039code11">
                        <pre class="swift" style="font-family:monospace;">
                            extension String { }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
        Add the following method to the String extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803912">
                    <td class="code" id="p128039code12">
                        <pre class="swift" style="font-family:monospace;">
                            func isAnagramOfString(- s: String) -&gt; Bool { //1 let lowerSelf = self.lowercased().replacingOccurrences(of:
                            " ", with: "") let lowerOther = s.lowercased().replacingOccurrences(of:
                            " ", with: "") //2 return lowerSelf.characters.sorted() == lowerOther.characters.sorted()
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
            Reverse the string and compare; if it’s the same, then you have a palindrome.
        </li>
    </ol>
    <p>
        Add the following method to detect palindromes:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803913">
                    <td class="code" id="p128039code13">
                        <pre class="swift" style="font-family:monospace;">
                            func isPalindrome() -&gt; Bool { //1 let f = self.lowercased().replacingOccurrences(of:
                            " ", with: "") //2 let s = String(f.characters.reversed()) //3 return f
                            == s }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
        and replace the
        <code>
            print(_:)
        </code>
        statement inside
        <code>
            staticMode()
        </code>
        with the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803914">
                    <td class="code" id="p128039code14">
                        <pre class="swift" style="font-family:monospace;">
                            //1 switch option { case .anagram: //2 if argCount != 4 { if argCount
                            &gt; 4 { print("Too many arguments for option \(option.rawValue)") } else
                            { print("Too few arguments for option \(option.rawValue)") } &nbsp; ConsoleIO.printUsage()
                            } else { //3 let first = CommandLine.arguments[2] let second = CommandLine.arguments[3]
                            &nbsp; if first.isAnagramOfString(second) { print("\(second) is an anagram
                            of \(first)") } else { print("\(second) is not an anagram of \(first)")
                            } } case .palindrome: //4 if argCount != 3 { if argCount &gt; 3 { print("Too
                            many arguments for option \(option.rawValue)") } else { print("Too few
                            arguments for option \(option.rawValue)") } } else { //5 let s = CommandLine.arguments[2]
                            let isPalindrome = s.isPalindrome() print("\(s) is \(isPalindrome ? ""
                            : "not ")a palindrome") } //6 case .help: ConsoleIO.printUsage() case .unknown:
                            //7 print("Unknown option \(value)") ConsoleIO.printUsage() }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Going through this step-by-step:
    </p>
    <ol>
        <li>
            First, switch to see what should be detected.
        </li>
        <li>
            In the case of an anagram, there must be four command-line arguments passed
            in. The first is the executable path, the second the
            <em>
                a
            </em>
            option and finally the two strings to check. If you don’t have four arguments,
            then print an error message.
        </li>
        <li>
            If the argument count is good, store the two strings in local variables,
            check the strings and print the result.
        </li>
        <li>
            In the case of a palindrome, you must have three arguments.
        </li>
        <li>
            Check for the palindrome and print the result.
        </li>
        <li>
            If the
            <em>
                -h
            </em>
            option was passed in, then print the usage information.
        </li>
        <li>
            If an unknown option is passed, print the usage to the console.
        </li>
    </ol>
    <p>
        Run your project with some modified arguments inside the
        <em>
            Scheme
        </em>
        . For example, you could use the
        <em>
            -p
        </em>
        option as shown below:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Bildschirmfoto-2016-03-05-um-13.25.10-700x393.png"
        alt="p-option-settings" width="700" height="393" class="aligncenter size-large wp-image-128047"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Bildschirmfoto-2016-03-05-um-13.25.10-700x393.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Bildschirmfoto-2016-03-05-um-13.25.10-480x270.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Bildschirmfoto-2016-03-05-um-13.25.10-768x431.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        You have a basic version of Panagram working, but you can make it even
        more useful by tying in to the input and output streams.
    </p>
    <h2>
        Input and Output
    </h2>
    <p>
        In most command-line programs, you’d like to print some messages for the
        user. For example, a program that converts video files into different formats
        could print the current progess or some error messages if something goes
        wrong.
    </p>
    <p>
        Unix-based systems such as
        <em>
            macOS
        </em>
        define two different output streams:
    </p>
    <ul>
        <li>
            The
            <em>
                standard output
            </em>
            stream (or
            <em>
                stdout
            </em>
            ) is normally attached to the display and should be used to display messages
            to the user.
        </li>
        <li>
            The
            <em>
                standard error
            </em>
            stream (or
            <em>
                stderr
            </em>
            ) is normally used to display status and error messages. This is normally
            attached to the display, but can be redirected to a file.
        </li>
    </ul>
    <p>
        <em>
            stderr
        </em>
        can be used to log error messages, the internal program state, or any
        other information the user doesn’t need to see. This can make debugging
        of a shipped application much easier.
    </p>
    <p>
        Your next task is to change
        <em>
            Panagram
        </em>
        to use these different output streams.
    </p>
    <p>
        First, open
        <em>
            ConsoleIO.swift
        </em>
        and add the following enum to the top of the file, outside the scope of
        the Panagram class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803915">
                    <td class="code" id="p128039code15">
                        <pre class="swift" style="font-family:monospace;">
                            enum OutputType { case error case standard }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This defines the output method to use when writing messages.
    </p>
    <p>
        Next add the following function to the
        <code>
            ConsoleIO
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803916">
                    <td class="code" id="p128039code16">
                        <pre class="swift" style="font-family:monospace;">
                            func writeMessage(_ message: String, to: OutputType = .standard) { switch
                            to { case .standard: print("\u{001B}[;m\(message)") case .error: fputs("\u{001B}[0;31m\(message)\n",
                            stderr) } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This function has two parameters; the first is the actual message to print,
        and the second is where to write it. This defaults to
        <code>
            .standard
        </code>
        .
    </p>
    <p>
        The code for the
        <code>
            .standard
        </code>
        option uses
        <code>
            print
        </code>
        , which by default writes to
        <em>
            stdout
        </em>
        . The
        <code>
            .error
        </code>
        case uses the C function
        <code>
            fputs
        </code>
        to write to stderr, which is a global variable and points to the standard
        error stream.
    </p>
    <p>
        What are those cryptic strings, though? These are
        <em>
            control characters
        </em>
        that cause Terminal to change the color of the following string. In this
        case you’ll print error messages in red (
        <code>
            \u{001B}[0;31m
        </code>
        ). The sequence
        <code>
            \u{001B}[;m
        </code>
        used in the standard case resets the terminal color back to the default.
    </p>
    <p>
        To use this new function, open
        <em>
            Panagram.swift
        </em>
        and change the
        <code>
            print
        </code>
        lines in
        <code>
            staticMode()
        </code>
        to use the new
        <code>
            writeMessage(_:to:)
        </code>
        method.
    </p>
    <p>
        The
        <code>
            switch
        </code>
        statement should now look like the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803917">
                    <td class="code" id="p128039code17">
                        <pre class="swift" style="font-family:monospace;">
                            case .anagram: if argCount != 4 { if argCount &gt; 4 { consoleIO.writeMessage("Too
                            many arguments for option \(option.rawValue)", to: .error) } else { consoleIO.writeMessage("too
                            few arguments for option \(option.rawValue)", to: .error) } ConsoleIO.printUsage()
                            } else { let first = CommandLine.arguments[2] let second = CommandLine.arguments[3]
                            &nbsp; if first.isAnagramOfString(second) { consoleIO.writeMessage("\(second)
                            is an anagram of \(first)") } else { consoleIO.writeMessage("\(second)
                            is not an anagram of \(first)") } } case .palindrome: if argCount != 3
                            { if argCount &gt; 3 { consoleIO.writeMessage("Too many arguments for option
                            \(option.rawValue)", to: .error) } else { consoleIO.writeMessage("too few
                            arguments for option \(option.rawValue)", to: .error) } } else { let s
                            = CommandLine.arguments[2] let isPalindrome = s.isPalindrome() consoleIO.writeMessage("\(s)
                            is \(isPalindrome ? "" : "not ")a palindrome") } case .help: ConsoleIO.printUsage()
                            case .unknown: consoleIO.writeMessage("Unkonwn option \(value)", to: .error)
                            ConsoleIO.printUsage() }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        As you see, only error messages need the
        <em>
            to:
        </em>
        parameter. That’s one of the benefits of Swift’s
        <em>
            default values
        </em>
        for parameters.
    </p>
    <p>
        Run your project; you should see something similar to this in the Xcode
        console. For example, using the arguments
        <em>
            a, listen
        </em>
        and
        <em>
            silent
        </em>
        you’ll see the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803918">
                    <td class="code" id="p128039code18">
                        <pre class="text" style="font-family:monospace;">
                            [;mlisten is an anagram of silent
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The
        <code>
            [;m
        </code>
        at the beginning of the output looks a bit awkward. That’s because the
        Xcode console doesn’t support using control characters to colorize the
        output. To see this in action, you’ll have to launch Panagram in Terminal:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Colored_Output-e1458912975895-700x216.png"
        alt="Colored_Output" width="700" height="216" class="aligncenter size-large wp-image-128048"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Colored_Output-e1458912975895-700x216.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Colored_Output-e1458912975895-480x148.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Colored_Output-e1458912975895-768x237.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/Colored_Output-e1458912975895.png 1145w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        The following section walks you how to launch your app in Terminal directly
        from Xcode. The downside is that you can’t debug your app in Xcode this
        way; therefore, the next section is optional and you can skip directly
        to the
        <em>
            Handle Input
        </em>
        section if you wish.
    </div>
    <h2>
        Launching Outside Xcode
    </h2>
    <p>
        There are different ways to launch your program from inside Terminal.
        You could find the build product using the Finder and start it directly
        via Terminal, or you could be lazy and tell
        <em>
            Xcode
        </em>
        to do this for you. In this section you’ll discover the lazy way.
    </p>
    <p>
        First, edit your current
        <em>
            Scheme
        </em>
        and uncheck
        <em>
            Debug executable
        </em>
        . Now click on the
        <em>
            Executable
        </em>
        drop down and select
        <em>
            Other
        </em>
        :
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/Executable_setting.png"
        rel="attachment wp-att-128049" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Executable_setting-480x270.png"
            alt="Executable_setting" width="480" height="270" class="aligncenter size-medium wp-image-128049"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Executable_setting-480x270.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Executable_setting-768x432.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/Executable_setting-700x394.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Executable_setting-266x151.png 266w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        In the window that appears, go to
        <em>
            Applications/Utilities
        </em>
        , select
        <em>
            Terminal.app
        </em>
        , then click
        <em>
            Choose
        </em>
        :
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/Choose_Terminal.png"
        rel="attachment wp-att-128050" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Choose_Terminal-412x320.png"
            alt="Choose_Terminal" width="412" height="320" class="aligncenter size-medium wp-image-128050"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Choose_Terminal-412x320.png 412w, https://koenig-media.raywenderlich.com/uploads/2016/03/Choose_Terminal-768x597.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/Choose_Terminal-643x500.png 643w, https://koenig-media.raywenderlich.com/uploads/2016/03/Choose_Terminal.png 1412w"
            sizes="(max-width: 412px) 100vw, 412px">
        </a>
    </p>
    <p>
        Now select the
        <em>
            Arguments
        </em>
        tab, remove all entries under
        <em>
            Arguments Passed On Launch
        </em>
        , then add one new entry in that section:
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
        This instructs Xcode to open Terminal when you run your project and pass
        through the path to your program. Terminal will then launch your program
        as you’d expect.
    </p>
    <h2>
        Handle Input
    </h2>
    <p>
        <code>
            stdin
        </code>
        is attached to the keyboard and is therefore a way for you to collect
        input from users interactively. When
        <em>
            Panagram
        </em>
        is started without arguments, it will open in interactive mode and prompt
        the user for the options it would otherwise have collected from its arguments.
    </p>
    <p>
        First, you need a way to get input from the keyboard.
    </p>
    <p>
        Open
        <em>
            ConsoleIO.swift
        </em>
        and add the following method to the
        <code>
            ConsoleIO
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803919">
                    <td class="code" id="p128039code19">
                        <pre class="swift" style="font-family:monospace;">
                            func getInput() -&gt; String { &nbsp; // 1 let keyboard = FileHandle.standardInput
                            &nbsp; // 2 let inputData = keyboard.availableData &nbsp; // 3 let strData
                            = String(data: inputData, encoding: String.Encoding.utf8)! &nbsp; // 4
                            return strData.trimmingCharacters(in: CharacterSet.newlines) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
        and create a function
        <code>
            interactiveMode()
        </code>
        as follows:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803920">
                    <td class="code" id="p128039code20">
                        <pre class="swift" style="font-family:monospace;">
                            func interactiveMode() { //1 consoleIO.writeMessage("Welcome to Panagram.
                            This program checks if an input string is an anagram or palindrome.") //2
                            var shouldQuit = false while !shouldQuit { //3 consoleIO.writeMessage("Type
                            'a' to check for anagrams or 'p' for palindromes type 'q' to quit.") let
                            (option, value) = consoleIO.getOption(consoleIO.getInput()) &nbsp; switch
                            option { case .anagram: //4 consoleIO.writeMessage("Type the first string:")
                            let first = consoleIO.getInput() consoleIO.writeMessage("Type the second
                            string:") let second = consoleIO.getInput() &nbsp; //5 if first.isAnagramOfString(second)
                            { consoleIO.writeMessage("\(second) is an anagram of \(first)") } else
                            { consoleIO.writeMessage("\(second) is not an anagram of \(first)") } case
                            .palindrome: consoleIO.writeMessage("Type a word or sentence:") let s =
                            consoleIO.getInput() let isPalindrome = s.isPalindrome() consoleIO.writeMessage("\(s)
                            is \(isPalindrome ? "" : "not ")a palindrome") default: //6 consoleIO.writeMessage("Unknown
                            option \(value)", to: .error) } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Taking a look at what’s going on above:
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
            Prompt the user for input and convert it to one of the two options if
            possible.
        </li>
        <li>
            Prompt the user for the two strings to compare.
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
        loop. To do this, open
        <em>
            ConsoleIO.swift
        </em>
        again and add the following line to
        <code>
            OptionType
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803921">
                    <td class="code" id="p128039code21">
                        <pre class="swift" style="font-family:monospace;">
                            case quit = "q"
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Next, add the following line to to
        <code>
            init(_:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803922">
                    <td class="code" id="p128039code22">
                        <pre class="swift" style="font-family:monospace;">
                            case "q": self = .quit
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now go back to
        <em>
            Panagram.swift
        </em>
        and add a
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803923">
                    <td class="code" id="p128039code23">
                        <pre class="swift" style="font-family:monospace;">
                            case .quit: shouldQuit = true
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Then change the
        <code>
            .unknown
        </code>
        case definition inside
        <code>
            staticMode()
        </code>
        as follows:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803924">
                    <td class="code" id="p128039code24">
                        <pre class="swift" style="font-family:monospace;">
                            case .unknown, .quit:
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Finally, open
        <em>
            main.swift
        </em>
        and replace the comment
        <code>
            //Handle interactive mode
        </code>
        with the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12803925">
                    <td class="code" id="p128039code25">
                        <pre class="swift" style="font-family:monospace;">
                            panagram.interactiveMode()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Run your project and enjoy your finished command-line program!
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Finished_Program-e1458913657510-700x267.png"
        alt="Finished_Program" width="700" height="267" class="aligncenter size-large wp-image-128052"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Finished_Program-e1458913657510-700x267.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Finished_Program-e1458913657510-480x183.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Finished_Program-e1458913657510-768x292.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/Finished_Program-e1458913657510.png 1145w"
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
        You can download the final project for this command line programs on macOS
        tutorial
        <br>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/05/Panagram_Final.zip"
        sl-processed="1">
            here
        </a>
    </p>
    <p>
        If you want to write more command-line programs in the future, take a
        look at how to redirect stderr to a log file and also look at
        <a href="http://www.gnu.org/software/ncurses/" sl-processed="1">
            ncurses
        </a>
        , which is a C library for writing “GUI-style” programs for the terminal.
    </p>
    <p>
        You can also check out
        <a href="http://krakendev.io/blog/scripting-in-swift" target="_blank"
        sl-processed="1">
            this great article
        </a>
        on scripting with Swift.
    </p>
    <p>
        I hope you enjoyed this command line programs on macOS tutorial; if you
        have any questions or comments, feel free to join the forum discussion
        below!
    </p>
</div>