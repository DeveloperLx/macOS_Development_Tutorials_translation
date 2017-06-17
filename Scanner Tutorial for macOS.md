# macOS的Scanner教程

#### [原文地址](https://www.raywenderlich.com/128792/nsscanner-tutorial-for-os-x) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div class="note">
        <p>
            <em>
                2016年9月25日更新：
            </em>
            本教程已更新至Xcode 8及Swift 3。
        </p>
        <p>
            <em>
                更新笔记：
            </em>
            本教程已由Hai Nguyen更新至Swift版。原教程是由Vincent Ngo所撰写的。
        </p>
    </div>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/05/OSX-NSScanner-feature-250x250.png"
        alt="NSScannerFeatureImage" width="250" height="250" class="alignright size-full wp-image-61878 bordered">
    </p>
    <p>
        在
        <i>
            大数据
        </i>
        时代，数据是以多种格式保存的，这就使得搞懂它变成了一项挑战。如果你很幸运，数据会是有组织的，层次的格式，就像
        <a href="http://www.json.org" sl-processed="1">
            JSON
        </a>
        ,
        <a href="https://en.wikipedia.org/wiki/XML" sl-processed="1">
            XML
        </a>
        ，
        <a href="https://en.wikipedia.org/wiki/Comma-separated_values" sl-processed="1">
            CSV
        </a>
        这样。否则，你就可能会挣扎在无穷的if/case语句之间。另一方面，手动地抽取数据是非常无聊的。
    </p>
    <p>
        谢天谢地，苹果提供了一系列用来分析在任何形式下的字符串数据的工具，从自然的到电脑的语言，诸如
        <code>
            NSRegularExpression
        </code>
        ，
        <code>
            NSDataDetector
        </code>
        或
        <code>
            Scanner
        </code>
        。它们每种都有各自的有时，但
        <code>
            Scanner
        </code>
        是到目前为止最容易使用的，不仅功能强大，而且非常灵活。在本教程中，你会学习如何使用它的方法从电子邮件的信息中抽取信息，来构建一个macOS应用，它工作起来就像下面苹果的Mail的界面这样。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Completed-Final-Screen-700x422.png"
        alt="Completed-Final-Screen" width="700" height="422" class="aligncenter size-large wp-image-129683"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Completed-Final-Screen-700x422.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Completed-Final-Screen-480x289.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Completed-Final-Screen-768x463.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/Completed-Final-Screen.png 810w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        尽管你是为Mac构建app，但
        <code>
            Scanner
        </code>
        同样也可以用在iOS上。在这个教程的结尾，你将可以在任一平台上解析文本。
    </p>
    <p>
        在开始之前，让我们来看一看
        <code>
            Scanner
        </code>
        有哪些功能！
    </p>
    <h2>
        Scanner概述
    </h2>
    <p>
        <code>
            Scanner
        </code>
        的主要功能是检索和解释子字符串和数值。
    </p>
    <p>
        例如，
        <code>
            Scanner
        </code>
        可以分析一个电话号码，并将其拆分成像下面这样的几个部分：
    </p>
    <pre lang="swift" class="hljs cs"><span class="hljs-comment">// 1.</span>
<span class="hljs-keyword">let</span> hyphen = CharacterSet(charactersIn: <span class="hljs-string">"-"</span>)

<span class="hljs-comment">// 2.</span>
<span class="hljs-keyword">let</span> scanner = Scanner(<span class="hljs-keyword">string</span>: <span class="hljs-string">"123-456-7890"</span>)
scanner.charactersToBeSkipped = hyphen

<span class="hljs-comment">// 3.</span>
<span class="hljs-keyword">var</span> areaCode, firstThreeDigits, lastFourDigits: NSString?

scanner.scanUpToCharacters(<span class="hljs-keyword">from</span>: hyphen, <span class="hljs-keyword">into</span>: &amp;areaCode)          <span class="hljs-comment">// A</span>
scanner.scanUpToCharacters(<span class="hljs-keyword">from</span>: hyphen, <span class="hljs-keyword">into</span>: &amp;firstThreeDigits)  <span class="hljs-comment">// B</span>
scanner.scanUpToCharacters(<span class="hljs-keyword">from</span>: hyphen, <span class="hljs-keyword">into</span>: &amp;lastFourDigits)    <span class="hljs-comment">// C</span>

print(areaCode!, firstThreeDigits!, lastFourDigits!)<span class="hljs-comment">// 123 - area code</span>
<span class="hljs-comment">// 456 - first three digits</span>
<span class="hljs-comment">// 7890 - last four digits</span>
</pre>
    <p>
        以上代码做的事有：
    </p>
    <ol>
        <li>
            创建的一个名为
            <code>
                hyphen
            </code>
            的
            <code>
                CharacterSet
            </code>
            的实例。这将会作为字符串成分之间的分隔符。
        </li>
        <li>
            初始化一个
            <code>
                Scanner
            </code>
            对象并改为
            <code>
                charactersToBeSkipped
            </code>
            的默认值（空格和换行符）为
            <code>
                hyphen
            </code>
            ，因此返回的字符串将不包含任何连字符。
        </li>
        <li>
            <code>
                areaCode
            </code>
            ，
            <code>
                firstThreeDigits
            </code>
            和
            <code>
                lastFourDigits
            </code>
            将会储存你从scanner返回的解析过的值。由于你无法将
            <em>
                Swift
            </em>
            本身的
            <code>
                String
            </code>
            直接作为
            <code>
                AutoreleasingUnsafeMutablePointer
                <nsstring?>
                </nsstring?>
            </code>
            ，因此为了将他们传递给scanner的方法，你不得不将这些变量声明为可选的
            <code>
                NSString
            </code>
            对象。
            <ol>
                <li>
                    扫描至第一个
                    <em>
                        –
                    </em>
                    字符并将连字符前的值分配到
                    <code>
                        areaCode
                    </code>
                    中。
                </li>
                <li>
                    继续扫描到第二个
                    <em>
                        –
                    </em>
                    并抓取下面的三个数字到
                    <code>
                        firstThreeDigits
                    </code>
                    中。在调用
                    <code>
                        scanUpToCharactersFromSet(from:into:)
                    </code>
                    之前，scanner的读取光标位于首次发现
                    <code>
                        -
                    </code>
                    的位置。在忽略掉连字符之后，你就获得了电话号码的第二个成分。
                </li>
                <li>
                    寻找下一个
                    <code>
                        -
                    </code>
                    。scanner结束了字符串的剩余部分，并返回一个成功的状态。之后就没有连字符了，scanner会将剩余的子字符串装到
                    <code>
                        lastFourDigits
                    </code>
                    中。
                </li>
            </ol>
        </li>
    </ol>
    <p>
        这就是
        <code>
            Scanner
        </code>
        所作的全部的事。容易吧！现在，是时候来搞个app了！
    </p>
    <h2>
        入门
    </h2>
    <p>
        下载
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/09/EmailParser-starter-project.zip"
        sl-processed="1">
            起始项目
        </a>
        并提取出ZIP文件的内容。在Xcode中打开
        <em>
            EmailParser.xcodeproj
        </em>
        。
    </p>
    <p>
        你将发现下列的内容：
    </p>
    <ul>
        <li>
            <em>
                DataSource.swift
            </em>
            包含一个预制的结构，它可以配置
            <em>
                data source/delegate
            </em>
            来填充一个
            <em>
                table view
            </em>
            。
        </li>
        <li>
            <em>
                PostCell.swift
            </em>
            包含所有你需要展示的每个独立数据项目的property。
        </li>
        <li>
            <em>
                Support/Main.storyboard
            </em>
            包含一个带有定制的cell的
            <em>
                TableView
            </em>
            ，位于左侧，以及在另一侧的
            <em>
                TextView
            </em>
            。
        </li>
    </ul>
    <p>
        你将解析在
        <em>
            comp.sys.mac.hardware
        </em>
        中的49个样本文件中的数据。让我们来花一些时间来浏览它们的结构吧。你将会收集诸如
        <em>
            Name
        </em>
        ，
        <em>
            Email
        </em>
        等项目到一个table中，以便一眼把它们看懂。
    </p>
    <div class="note">
        <em>
            注意
        </em>
        ：起始的项目使用了table view来展示数据，因此如果你不熟悉table view，请访问我们的
        <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/macOS%20NSTableView%20Tutorial.md" sl-processed="1">
            macOS NSTableView教程
        </a>
        .
    </div>
    <p>
        Build并运行项目来在实际中查看它。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Starter-Initial-Screen-683x500.png"
        alt="Starter-Initial-Screen" width="683" height="500" class="aligncenter size-large wp-image-129690"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Starter-Initial-Screen-683x500.png 683w, https://koenig-media.raywenderlich.com/uploads/2016/03/Starter-Initial-Screen-437x320.png 437w, https://koenig-media.raywenderlich.com/uploads/2016/03/Starter-Initial-Screen-768x563.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/Starter-Initial-Screen.png 804w"
        sizes="(max-width: 683px) 100vw, 683px">
    </p>
    <p>
        table view当前使用
        <em>
            [Field]Value
        </em>
        前缀展示占位的label。在这篇教程的最后，它们将会被解析过的数据来替换。
    </p>
    <h2>
        理解原始样本的结构
    </h2>
    <p>
        在深入解析之前，理解你要尝试实现什么结果是非常重要的。以下是样本文件中的一个，你将重点检索的数据项。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Data-Structure-Illustration-547x500.png"
        alt="Data-Structure-Illustration" width="547" height="500" class="aligncenter size-large wp-image-129684"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Data-Structure-Illustration-547x500.png 547w, https://koenig-media.raywenderlich.com/uploads/2016/03/Data-Structure-Illustration-350x320.png 350w, https://koenig-media.raywenderlich.com/uploads/2016/03/Data-Structure-Illustration-768x702.png 768w"
        sizes="(max-width: 547px) 100vw, 547px">
    </p>
    <p>
        总的来说，这些数据项目就是：
    </p>
    <ul>
        <li>
            <em>
                <i>
                    From
                </i>
                域
            </em>
            ：它包含了sender的名称和email。解析它是非常tricky的，因为名称可能会在email之前出现，反之亦然；它可能甚至只包含一个却不包含另一个。
        </li>
        <li>
            <em>
                <i>
                    Subject
                </i>
            </em>
            ，
            <em>
                <i>
                    Date
                </i>
            </em>
            ，
            <em>
                <i>
                    Organization
                </i>
            </em>
            和
            <em>
                <i>
                    Lines
                </i>
            </em>
            <em>
                fields
            </em>
            ：这些包含了由冒号分隔的值。
        </li>
        <li>
            <em>
                <i>
                    Message
                </i>
                部分
            </em>
            ：包含了成本信息以及一些下面的关键字：
            <i>
                apple
            </i>
            ，
            <i>
                macs
            </i>
            ，
            <i>
                software
            </i>
            ，
            <i>
                keyboard
            </i>
            ，
            <i>
                printer
            </i>
            ，
            <i>
                video
            </i>
            ，
            <i>
                monitor
            </i>
            ，
            <i>
                laser
            </i>
            ，
            <i>
                scanner
            </i>
            ，
            <i>
                disks
            </i>
            ，
            <i>
                cost
            </i>
            ，
            <i>
                price
            </i>
            ，
            <i>
                floppy
            </i>
            ，
            <i>
                card
            </i>
            ，以及
            <i>
                phone
            </i>
            。
        </li>
    </ul>
    <p>
        <code>
            Scanner
        </code>
        是超赞的；然而，我们使用它的时候会感到有一些笨重，并且不那么的swift，因此你会转换內建的方法，就像上面那个电话号码的例子中一样，返回可选类型的值。
    </p>
    <p>
        点击
        <em>
            File\New\File…
        </em>
        （或只需按
        <em>
            Command+N
        </em>
        键）。选择
        <em>
            macOS &gt; Source &gt; Swift File
        </em>
        并单击
        <em>
            Next
        </em>
        。设置文件的名称为
        <em>
            Scanner+.swift
        </em>
        ，然后单击
        <em>
            Create
        </em>
        。
    </p>
    <p>
        打开
        <em>
            Scanner+.swift
        </em>
        并添加下列的extension：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">Scanner</span> </span>{
  
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">scanUpToCharactersFrom</span><span class="hljs-params">(<span class="hljs-number">_</span> <span class="hljs-keyword">set</span>: CharacterSet)</span></span> -&gt; <span class="hljs-type">String</span>? {
    <span class="hljs-keyword">var</span> result: <span class="hljs-type">NSString</span>?                                                           <span class="hljs-comment">// 1.</span>
    <span class="hljs-keyword">return</span> scanUpToCharacters(from: <span class="hljs-keyword">set</span>, into: &amp;result) ? (result <span class="hljs-keyword">as</span>? <span class="hljs-type">String</span>) : <span class="hljs-literal">nil</span> <span class="hljs-comment">// 2.</span>
  }
  
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">scanUpTo</span><span class="hljs-params">(<span class="hljs-number">_</span> string: String)</span></span> -&gt; <span class="hljs-type">String</span>? {
    <span class="hljs-keyword">var</span> result: <span class="hljs-type">NSString</span>?
    <span class="hljs-keyword">return</span> <span class="hljs-keyword">self</span>.scanUpTo(string, into: &amp;result) ? (result <span class="hljs-keyword">as</span>? <span class="hljs-type">String</span>) : <span class="hljs-literal">nil</span>
  }
  
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">scanDouble</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">Double</span>? {
    <span class="hljs-keyword">var</span> double: <span class="hljs-type">Double</span> = <span class="hljs-number">0</span>
    <span class="hljs-keyword">return</span> scanDouble(&amp;double) ? double : <span class="hljs-literal">nil</span>
  }
}
</pre>
    <p>
        这些助手方法封装了一些你在这篇教程中用到的
        <code>
            Scanner
        </code>
        的方法，它们会返回
        <code>
            String
        </code>
        的可选类型。这三个方法有着相同的结构：
    </p>
    <ol>
        <li>
            定义一个
            <code>
                result
            </code>
            变量来持有scanner返回的结果。
        </li>
        <li>
            使用一个三元操作符来检查扫描是否成功。如果成功的话，将
            <code>
                result
            </code>
            转化为
            <code>
                String
            </code>
            并返回它；否则就返回
            <code>
                nil
            </code>
            。
        </li>
    </ol>
    <div class="note">
        <em>
            注意：
        </em>
        就像上面这样，你可以用相同的方式来实现其它的
        <code>
            Scanner
        </code>
        方法，并将它们保存到你的武器库中：
        <p>
        </p>
        <ul>
            <li>
                scanDecimal(_:)
            </li>
            <li>
                scanFloat(_:)
            </li>
            <li>
                scanHexDouble(_:)
            </li>
            <li>
                scanHexFloat(_:)
            </li>
            <li>
                scanHexInt32(_:)
            </li>
            <li>
                scanHexInt64(_:)
            </li>
            <li>
                scanInt(_:)
            </li>
            <li>
                scanInt32(_:)
            </li>
            <li>
                scanInt64(_:)
            </li>
        </ul>
    </div>
    <p>
        Simple, right? Now go back to the main project and start parsing!
    </p>
    <h2>
        Creating the Data Structure
    </h2>
    <p>
        Navigate to
        <em>
            File\New\File…
        </em>
        (or simply press
        <em>
            Command+N
        </em>
        ). Select
        <em>
            macOS &gt; Source &gt; Swift File
        </em>
        and click
        <em>
            Next
        </em>
        . Set the file’s name to
        <em>
            HardwarePost.swift
        </em>
        , then click
        <em>
            Create
        </em>
        .
    </p>
    <p>
        Open
        <em>
            HardwarePost.swift
        </em>
        and add the following structure:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1287923">
                    <td class="code" id="p128792code3">
                        <pre class="swift" style="font-family:monospace;">
                            struct HardwarePost { // MARK: Properties &nbsp; // the fields' values
                            once extracted placed in the properties let email: String let sender: String
                            let subject: String let date: String let organization: String let numberOfLines:
                            Int let message: String &nbsp; let costs: [Double] // cost related information
                            let keywords: Set&lt;String&gt; // set of distinct keywords }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This code defines
        <code>
            HardwarePost
        </code>
        structure that stores the parsed data. By default,
        <em>
            Swift
        </em>
        provides you a default constructor based on its properties, but you’ll
        come back to this later to implement your own custom initializer.
    </p>
    <p>
        Are you ready for parsing in action with
        <code>
            Scanner
        </code>
        ? Let’s do this.
    </p>
    <h2>
        Creating the Data Parser
    </h2>
    <p>
        Navigate to
        <em>
            File\New\File…
        </em>
        (or simply press
        <em>
            Command+N
        </em>
        ), select
        <em>
            macOS &gt; Source &gt; Swift File
        </em>
        and click
        <em>
            Next
        </em>
        . Set the file’s name to
        <em>
            ParserEngine.swift
        </em>
        , then click
        <em>
            Create
        </em>
        .
    </p>
    <p>
        Open
        <em>
            ParserEngine.swift
        </em>
        and create
        <code>
            ParserEngine
        </code>
        class by adding the following code:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1287924">
                    <td class="code" id="p128792code4">
                        <pre class="swift" style="font-family:monospace;">
                            final class ParserEngine { &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <h3>
        Extracting Metadata Fields
    </h3>
    <p>
        Consider the following sample metadata segment:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Metadata-Segment-700x211.png"
        alt="Metadata-Segment" width="700" height="211" class="aligncenter size-large wp-image-129689"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Metadata-Segment-700x211.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Metadata-Segment-480x144.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Metadata-Segment-768x231.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Here’s where
        <code>
            Scanner
        </code>
        comes in and separates the fields and their values. The image below gives
        you a general visual representation of this structure.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Field-Structure-Illustraion-700x75.png"
        alt="Field-Structure-Illustraion" width="700" height="75" class="aligncenter size-large wp-image-129685"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Field-Structure-Illustraion-700x75.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Field-Structure-Illustraion-480x51.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Field-Structure-Illustraion-768x82.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Open
        <em>
            ParserEngine.swift
        </em>
        and implement this code inside
        <code>
            ParserEngine
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1287925">
                    <td class="code" id="p128792code5">
                        <pre class="swift" style="font-family:monospace;">
                            // 1. typealias Fields = (sender: String, email: String, subject: String,
                            date: String, organization: String, lines: Int) &nbsp; /// Returns a collection
                            of predefined fields' extracted values func fieldsByExtractingFrom(_ string:
                            String) -&gt; Fields { // 2. var (sender, email, subject, date, organization,
                            lines) = ("", "", "", "", "", 0) &nbsp; // 3. let scanner = Scanner(string:
                            string) scanner.charactersToBeSkipped = CharacterSet(charactersIn: " :\n")
                            &nbsp; // 4. while !scanner.isAtEnd { // A let field = scanner.scanUpTo(":")
                            ?? "" // B let info = scanner.scanUpTo("\n") ?? "" // C &nbsp; // D switch
                            field { case "From": (email, sender) = fromInfoByExtractingFrom(info) //
                            E case "Subject": subject = info case "Date": date = info case "Organization":
                            organization = info case "Lines": lines = Int(info) ?? 0 default: break
                            } } &nbsp; return (sender, email, subject, date, organization, lines) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Don’t panic! The
        <em>
            Xcode
        </em>
        error of an unresolved identifier will go away right in the next section.
    </p>
    <p>
        Here’s what the above code does:
    </p>
    <ol>
        <li>
            Defines a
            <code>
                Fields
            </code>
            type alias for the tuple of parsed fields.
        </li>
        <li>
            Creates variables that will hold the returning values.
        </li>
        <li>
            Initializes a
            <code>
                Scanner
            </code>
            instance and changes its
            <code>
                charactersToBeSkipped
            </code>
            property to also include a colon beside the default values – whitespace
            and linefeed.
        </li>
        <li>
            Obtains values of all the wanted fields by repeating the process below:
            <ol>
                <li>
                    Uses
                    <code>
                        while
                    </code>
                    to loop through
                    <code>
                        string
                    </code>
                    ‘s content until it reaches the end.
                </li>
                <li>
                    Invokes one of the helper functions you created earlier to get
                    <code>
                        field
                    </code>
                    ‘s title before
                    <code>
                        :
                    </code>
                    .
                </li>
                <li>
                    Continues scanning up to the end of the line where the linefeed character
                    <code>
                        \n
                    </code>
                    is located and assigns the result to
                    <code>
                        info
                    </code>
                    .
                </li>
                <li>
                    Uses
                    <code>
                        switch
                    </code>
                    to find the matching field and stores its
                    <code>
                        info
                    </code>
                    property value into the proper variable.
                </li>
                <li>
                    Analyzes
                    <i>
                        From
                    </i>
                    field by calling
                    <code>
                        fromInfoByExtractingFrom(_:)
                    </code>
                    . You’ll implement the method after this section.
                </li>
            </ol>
        </li>
    </ol>
    <p>
        Remember the tricky part of
        <i>
            From
        </i>
        field? Hang tight because you’re going to need help from regular expression
        to overcome this challenge.
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        Regular expressions are a great tool to manipulate strings with patterns,
        and this
        <a href="/?p=30288" sl-processed="1">
            NSRegularExpression Tutorial
        </a>
        gives a good overview of how to use them.
    </div>
    <p>
        At the end of
        <em>
            ParserEngine.swift
        </em>
        , add the following
        <code>
            String
        </code>
        extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1287926">
                    <td class="code" id="p128792code6">
                        <pre class="swift" style="font-family:monospace;">
                            private extension String { &nbsp; func isMatched(_ pattern: String) -&gt;
                            Bool { return NSPredicate(format: "SELF MATCHES %@", pattern).evaluate(with:
                            self) } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This extension defines a private helper method to find whether the string
        matches a given pattern using regular expressions.
    </p>
    <p>
        It creates a
        <code>
            NSPredicate
        </code>
        object with a
        <code>
            MATCHES
        </code>
        operator using the regular expression pattern. Then it invokes
        <code>
            evaluate(with:)
        </code>
        to check if the string matches the conditions of the pattern.
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        You can read more about
        <code>
            NSPredicate
        </code>
        in
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/Foundation/Classes/NSPredicate_Class/index.html"
        sl-processed="1">
            the official Apple documentation
        </a>
        .
    </div>
    <p>
        Now add the following method inside the
        <code>
            ParserEngine
        </code>
        implementation, just after
        <code>
            fieldsByExtractingFrom(_:)
        </code>
        method:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1287927">
                    <td class="code" id="p128792code7">
                        <pre class="swift" style="font-family:monospace;">
                            fileprivate func fromInfoByExtractingFrom(_ string: String) -&gt; (email:
                            String, sender: String) { let scanner = Scanner(string: string) &nbsp;
                            // 1. /* * ROGOSCHP@MAX.CC.Uregina.CA (Are we having Fun yet ???) * oelt0002@student.tc.umn.edu
                            (Bret Oeltjen) * (iisi owner) * mbuntan@staff.tc.umn.edu () * barry.davis@hal9k.ann-arbor.mi.us
                            (Barry Davis) */ if string.isMatched(".*[\\s]*\\({1}(.*)") { // A scanner.charactersToBeSkipped
                            = CharacterSet(charactersIn: "() ") // B &nbsp; let email = scanner.scanUpTo("(")
                            // C let sender = scanner.scanUpTo(")") // D &nbsp; return (email ?? "",
                            sender ?? "") } &nbsp; // 2. /* * "Jonathan L. Hutchison" &lt;jh6r+@andrew.cmu.edu&gt;
                            * &lt;BR4416A@auvm.american.edu&gt; * Thomas Kephart &lt;kephart@snowhite.eeap.cwru.edu&gt;
                            * Alexander Samuel McDiarmid &lt;am2o+@andrew.cmu.edu&gt; */ if string.isMatched(".*[\\s]*&lt;{1}(.*)")
                            { scanner.charactersToBeSkipped = CharacterSet(charactersIn: "&lt;&gt;
                            ") &nbsp; let sender = scanner.scanUpTo("&lt;") let email = scanner.scanUpTo("&gt;")
                            &nbsp; return (email ?? "", sender ?? "") } &nbsp; // 3. return ("unknown",
                            string) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        After examining the 49 data sets, you end up with three cases to consider:
    </p>
    <ul>
        <li>
            <em>
                email (name)
            </em>
        </li>
        <li>
            <em>
                name &lt;email&gt;
            </em>
        </li>
        <li>
            <em>
                email
            </em>
            with no name
        </li>
    </ul>
    <p>
        Here’s what the code does:
    </p>
    <ol>
        <li>
            Matches
            <code>
                string
            </code>
            with the first pattern –
            <i>
                email (name)
            </i>
            . If not, continues to the next case.
            <ol>
                <li>
                    Looks for zero or more occurrences of any character –
                    <code>
                        .*
                    </code>
                    , followed by zero or more occurrence of a space –
                    <code>
                        [\\s]*
                    </code>
                    , followed by one open parenthesis –
                    <code>
                        \\({1}
                    </code>
                    and finally zero or more occurrences of a string –
                    <code>
                        (.*)
                    </code>
                    .
                </li>
                <li>
                    Sets the
                    <code>
                        Scanner
                    </code>
                    object’s
                    <code>
                        charactersToBeSkipped
                    </code>
                    to include: “(“, “)” and whitespace.
                </li>
                <li>
                    Scans up to
                    <code>
                        (
                    </code>
                    to get the
                    <code>
                        email
                    </code>
                    value.
                </li>
                <li>
                    Scans up to
                    <code>
                        )
                    </code>
                    , which gives you the
                    <code>
                        sender
                    </code>
                    name. This extracts everything before
                    <code>
                        (
                    </code>
                    and after
                    <code>
                        )
                    </code>
                    .
                </li>
            </ol>
        </li>
        <p>
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Field-Value-Illustration-700x81.png"
            alt="Field-Value-Illustration" width="700" height="81" class="aligncenter size-large wp-image-129686"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Field-Value-Illustration-700x81.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Field-Value-Illustration-480x56.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Field-Value-Illustration-768x89.png 768w"
            sizes="(max-width: 700px) 100vw, 700px">
        </p>
        <li>
            Checks whether the given string matches the pattern –
            <i>
                name &lt;email&gt;
            </i>
            . The
            <i>
                if
            </i>
            body is practically the same as the first scenario, except that you deal
            with angle brackets.
        </li>
        <li>
            Finally, if neither of the two patterns is matched, this is the case where
            you only have an email. You’ll simply return the string for the email and
            “unknown” for sender.
        </li>
    </ol>
    <p>
        At this point, you can build the project. The previous compile error is
        gone.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Starter-Initial-Screen-683x500.png"
        alt="Starter-Initial-Screen" width="683" height="500" class="aligncenter size-large wp-image-129690"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Starter-Initial-Screen-683x500.png 683w, https://koenig-media.raywenderlich.com/uploads/2016/03/Starter-Initial-Screen-437x320.png 437w, https://koenig-media.raywenderlich.com/uploads/2016/03/Starter-Initial-Screen-768x563.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/Starter-Initial-Screen.png 804w"
        sizes="(max-width: 683px) 100vw, 683px">
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        <code>
            NSDataDetector
        </code>
        would be a better solution for known-data types like phone number, address,
        and email. You can check out
        <a href="https://www.cocoanetics.com/2014/06/e-mail-validation/" sl-processed="1">
            this blog
        </a>
        about email validation with
        <code>
            NSDataDetector
        </code>
        .
    </div>
    <p>
        You’ve been working with
        <code>
            Scanner
        </code>
        to analyze and retrieve information from a patterned string. In the next
        two sections, you’ll learn how to parse unstructured data.
    </p>
    <h3>
        Extracting Cost-Related Information
    </h3>
    <p>
        A good example of parsing unstructured data is to determine whether the
        email’s body contains cost-related information. To do this, you’ll use
        <code>
            Scanner
        </code>
        to search for an occurrence of a dollar character:
        <em>
            $
        </em>
        .
    </p>
    <p>
        Still working on
        <em>
            ParserEngine.swift
        </em>
        , add the following implementation inside
        <code>
            ParserEngine
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1287928">
                    <td class="code" id="p128792code8">
                        <pre class="swift" style="font-family:monospace;">
                            func costInfoByExtractingFrom(_ string: String) -&gt; [Double] { // 1.
                            var results = [Double]() &nbsp; // 2. let dollar = CharacterSet(charactersIn:
                            "$") &nbsp; // 3. let scanner = Scanner(string: string) scanner.charactersToBeSkipped
                            = dollar &nbsp; // 4. while !scanner.isAtEnd &amp;&amp; scanner.scanUpToCharacters(from:
                            dollar, into: nil) { results += [scanner.scanDouble()].flatMap { $0 } }
                            &nbsp; return results }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The code is fairly straightforward:
    </p>
    <ol>
        <li>
            Defines an empty array to store the cost values.
        </li>
        <li>
            Creates a
            <code>
                CharacterSet
            </code>
            object with a
            <code>
                $
            </code>
            character.
        </li>
        <li>
            Initializes a
            <code>
                Scanner
            </code>
            instance and configures it to ignore the
            <em>
                $
            </em>
            character.
        </li>
        <li>
            Loops through
            <code>
                string
            </code>
            ‘s content and when a
            <code>
                $
            </code>
            is found, grabs the number after
            <code>
                $
            </code>
            with your helper method and appends it to
            <code>
                results
            </code>
            array.
        </li>
    </ol>
    <h3>
        Parsing the Message
    </h3>
    <p>
        Another example of parsing unstructured data is finding keywords in a
        given body of text. Your search strategy is to look at every word and check
        it against a set of keywords to see if it matches. You’ll use the
        <em>
            whitespace
        </em>
        and
        <em>
            newline
        </em>
        characters to take the words in the message as scanning.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Keywords-Parser-Illustration-700x102.png"
        alt="Keywords-Parser-Illustration" width="700" height="102" class="aligncenter size-large wp-image-129687"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Keywords-Parser-Illustration-700x102.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Keywords-Parser-Illustration-480x70.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Keywords-Parser-Illustration-768x112.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Add the following code at the end of
        <code>
            ParserEngine
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1287929">
                    <td class="code" id="p128792code9">
                        <pre class="swift" style="font-family:monospace;">
                            // 1. let keywords: Set&lt;String&gt; = ["apple", "macs", "software",
                            "keyboard", "printers", "printer", "video", "monitor", "laser", "scanner",
                            "disks", "cost", "price", "floppy", "card", "phone"] &nbsp; /// Return
                            a set of keywords extracted from func keywordsByExtractingFrom(_ string:
                            String) -&gt; Set&lt;String&gt; { // 2. var results: Set&lt;String&gt;
                            = [] &nbsp; // 3. let scanner = Scanner(string: string) &nbsp; // 4. while
                            !scanner.isAtEnd, let word = scanner.scanUpTo(" ")?.lowercased() { if keywords.contains(word)
                            { results.insert(word) } } &nbsp; return results }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s what this code does:
    </p>
    <ol>
        <li>
            Defines the keywords set that you’ll match against.
        </li>
        <li>
            Creates a
            <code>
                Set
            </code>
            of
            <code>
                String
            </code>
            to store the found keywords.
        </li>
        <li>
            Initializes a
            <code>
                Scanner
            </code>
            instance. You’ll use the default
            <code>
                charactersToBeSkipped
            </code>
            , which are the whitespace and newline characters.
        </li>
        <li>
            For every word found, checks whether it’s one of the predefined
            <code>
                keywords
            </code>
            . If it is, appends it into
            <code>
                results
            </code>
            .
        </li>
    </ol>
    <p>
        There — you have all of the necessary methods to acquire the desired information.
        Time to put them to good use and create
        <code>
            HardwarePost
        </code>
        instances for the 49 data files.
    </p>
    <h2>
        Connecting the Parser With Data Samples
    </h2>
    <p>
        Open
        <em>
            HardwarePost.swift
        </em>
        and add this initializer into
        <code>
            HardWarePost
        </code>
        structure:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12879210">
                    <td class="code" id="p128792code10">
                        <pre class="swift" style="font-family:monospace;">
                            init(fromData data: Data) { // 1. let parser = ParserEngine() &nbsp; //
                            2. let string = String(data: data, encoding: String.Encoding.utf8) ?? ""
                            &nbsp; // 3. let scanner = Scanner(string: string) &nbsp; // 4. let metadata
                            = scanner.scanUpTo("\n\n") ?? "" let (sender, email, subject, date, organization,
                            lines) = parser.fieldsByExtractingFrom(metadata) &nbsp; // 5. self.sender
                            = sender self.email = email self.subject = subject self.date = date self.organization
                            = organization self.numberOfLines = lines &nbsp; // 6. let startIndex =
                            string.characters.index(string.startIndex, offsetBy: scanner.scanLocation)
                            // A let message = string[startIndex..&lt;string.endIndex] // B self.message
                            = message.trimmingCharacters(in: .whitespacesAndNewlines ) // C &nbsp;
                            // 7. costs = parser.costInfoByExtractingFrom(message) keywords = parser.keywordsByExtractingFrom(message)
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s how
        <code>
            HardwarePost
        </code>
        initializes its properties:
    </p>
    <ol>
        <li>
            Simply creates a
            <code>
                ParserEngine
            </code>
            object named
            <code>
                parser
            </code>
            .
        </li>
        <li>
            Converts
            <code>
                data
            </code>
            into a
            <code>
                String
            </code>
            .
        </li>
        <li>
            Initializes an instance of
            <code>
                Scanner
            </code>
            to parse the Metadata and Message segments, which are separated by “\n\n”.
        </li>
        <li>
            Scans up to the first
            <code>
                \n\n
            </code>
            to grab the metadata string, then invokes the
            <code>
                parser
            </code>
            ‘s
            <code>
                fieldsByExtractingFrom(_:)
            </code>
            method to obtain all of the metadata fields.
        </li>
        <li>
            Assigns the parsing results to the
            <code>
                HardwarePost
            </code>
            properties.
        </li>
        <li>
            Prepares the message content:
            <ol>
                <li>
                    Gets the current reading cursor from
                    <code>
                        scanner
                    </code>
                    with
                    <code>
                        scanLocation
                    </code>
                    and converts it to
                    <code>
                        String.CharacterView.Index
                    </code>
                    , so you can substitute
                    <code>
                        string
                    </code>
                    by range.
                </li>
                <li>
                    Assigns the remaining string that
                    <code>
                        scanner
                    </code>
                    has yet to read into the new
                    <code>
                        message
                    </code>
                    variable.
                </li>
                <li>
                    Since
                    <code>
                        message
                    </code>
                    value still contains
                    <code>
                        \n\n
                    </code>
                    where the
                    <code>
                        scanner
                    </code>
                    left off from the previous reading, you need to trim it and give the new
                    value back to the
                    <code>
                        HardwarePost
                    </code>
                    instance’s
                    <code>
                        message
                    </code>
                    property.
                </li>
            </ol>
        </li>
        <li>
            Invokes the
            <code>
                parser
            </code>
            ‘s methods with
            <code>
                message
            </code>
            to retrieve values for
            <code>
                cost
            </code>
            and
            <code>
                keywords
            </code>
            properties.
        </li>
    </ol>
    <p>
        At this point, you can create
        <code>
            HardwarePost
        </code>
        instances directly from the files’ data. You are only few more steps from
        displaying the final product!
    </p>
    <h2>
        Displaying Parsed Data
    </h2>
    <p>
        Open
        <em>
            PostCell.swift
        </em>
        and add the following method inside the
        <code>
            PostCell
        </code>
        class implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12879211">
                    <td class="code" id="p128792code11">
                        <pre class="swift" style="font-family:monospace;">
                            func configure(_ post: HardwarePost) { &nbsp; senderLabel.stringValue
                            = post.sender emailLabel.stringValue = post.email dateLabel.stringValue
                            = post.date subjectLabel.stringValue = post.subject organizationLabel.stringValue
                            = post.organization numberOfLinesLabel.stringValue = "\(post.numberOfLines)"
                            &nbsp; // 1. costLabel.stringValue = post.costs.isEmpty ? "NO" : post.costs.map
                            { "\($0)" }.lazy.joined(separator: "; ") &nbsp; // 2. keywordsLabel.stringValue
                            = post.keywords.isEmpty ? "No keywords found" : post.keywords.joined(separator:
                            "; ") }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This code assigns the post values to the cell labels.
        <code>
            costLabel
        </code>
        and
        <code>
            keywordsLabel
        </code>
        require special treatment because they can be empty. Here’s what happens:
    </p>
    <ol>
        <li>
            If the
            <code>
                costs
            </code>
            array is empty, it sets the
            <code>
                costLabel
            </code>
            string value to
            <em>
                NO
            </em>
            ; otherwise, it concatenates the cost values with “; ” as a separator.
        </li>
        <li>
            Similarly, sets
            <code>
                keywordsLabel
            </code>
            string value to
            <code>
                No words found
            </code>
            for an empty set of
            <code>
                post.keywords
            </code>
            .
        </li>
    </ol>
    <p>
        You’re almost there! Open
        <em>
            DataSource.swift
        </em>
        . Delete the
        <code>
            DataSource
        </code>
        initializer
        <code>
            init()
        </code>
        and add the following code into the class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12879212">
                    <td class="code" id="p128792code12">
                        <pre class="swift" style="font-family:monospace;">
                            let hardwarePosts: [HardwarePost] // 1. &nbsp; override init() { self.hardwarePosts
                            = Bundle.main // 2. .urls(forResourcesWithExtension: nil, subdirectory:
                            "comp.sys.mac.hardware")? // 3. .flatMap( { try? Data(contentsOf: $0) }).lazy
                            // 4. .map(HardwarePost.init) ?? [] // 5. &nbsp; super.init() }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This is what the code does:
    </p>
    <ol>
        <li>
            Stores the
            <code>
                HardwarePost
            </code>
            instances.
        </li>
        <li>
            Obtains a reference to the application’s main Bundle.
        </li>
        <li>
            Retrieves urls of the sample files inside the
            <em>
                comp.sys.mac.hardware
            </em>
            directory.
        </li>
        <li>
            Lazily acquires an array of
            <code>
                Data
            </code>
            instances by reading file contents with
            <code>
                Data
            </code>
            failable initializer and
            <code>
                flatMap(_:)
            </code>
            . The idea of using
            <code>
                flatMap(_:)
            </code>
            is to get back a subarray containing only elements that are not
            <code>
                nil
            </code>
            .
        </li>
        <li>
            Finally, transforms the
            <code>
                Data
            </code>
            results to a
            <code>
                HardwarePost
            </code>
            object and assigns them to the
            <code>
                DataSource
            </code>
            <code>
                hardwarePosts
            </code>
            property.
        </li>
    </ol>
    <p>
        Now you need to set up the table view’s data source and delegate so that
        your app can show your hard work.
    </p>
    <p>
        Open
        <em>
            DataSource.swift
        </em>
        . Find
        <code>
            numberOfRows(in:)
        </code>
        and replace it with the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12879213">
                    <td class="code" id="p128792code13">
                        <pre class="swift" style="font-family:monospace;">
                            func numberOfRows(in tableView: NSTableView) -&gt; Int { return hardwarePosts.count
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        <code>
            numberOfRows(in:)
        </code>
        is part of the table view’s data source protocol; it sets the number of
        rows of the table view.
    </p>
    <p>
        Next, find
        <code>
            tableView(_:viewForTableColumn:row:)
        </code>
        and replace the comment that says:
        <code>
            //TODO: Set up cell view
        </code>
        with the code below:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12879214">
                    <td class="code" id="p128792code14">
                        <pre class="swift" style="font-family:monospace;">
                            cell.configure(hardwarePosts[row])
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The table view invokes its delegate
        <code>
            tableView(_:viewForTableColumn:row:)
        </code>
        method to set up every individual cell. It gets a reference to the post
        for that row and invokes
        <code>
            PostCell
        </code>
        ‘s
        <code>
            configure(_:)
        </code>
        method to display the data.
    </p>
    <p>
        Now you need to show the post in the text view when you select a post
        on the table view. Replace the initial implementation of
        <code>
            tableViewSelectionDidChange(_:)
        </code>
        with the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12879215">
                    <td class="code" id="p128792code15">
                        <pre class="swift" style="font-family:monospace;">
                            func tableViewSelectionDidChange(_ notification: Notification) { guard
                            let tableView = notification.object as? NSTableView else { return } textView.string
                            = hardwarePosts[tableView.selectedRow].message }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        <code>
            tableViewSelectionDidChange(_:)
        </code>
        is called when the table view’s selection has changed. When that happens,
        this code gets the hardware post for the selected row and displays the
        <code>
            message
        </code>
        in the text view.
    </p>
    <p>
        Build and run your project.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/starter-final.png"
        rel="attachment wp-att-131188" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/starter-final-480x270.png"
            alt="starter-final" width="480" height="270" class="aligncenter size-medium wp-image-131188"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/starter-final-480x270.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/starter-final-768x433.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/starter-final-700x394.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/starter-final-266x151.png 266w, https://koenig-media.raywenderlich.com/uploads/2016/04/starter-final.png 1498w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        All of the parsed fields are now neatly displayed on the table. Select
        a cell on the left, and you’ll see the corresponding message on the right.
        Good Job!
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
        Here’s the source code for the
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/09/EmailParser-final-project.zip"
        sl-processed="1">
            completed project
        </a>
        <br>
        There is so much more you can do with the data you have parsed. You could
        write a formatter that converts a
        <code>
            HardwarePost
        </code>
        object into JSON, XML, CSV or any other formats. With your new-found flexibility
        to represent data in different forms, you can share your data across different
        platforms.
    </p>
    <p>
        If you’re interested in the study of computer languages and how they are
        implemented, take a class in
        <i>
            comparative
        </i>
        languages. Your course will likely cover formal languages and BNF grammars—all
        important concepts in the design and implementation of parsers.
    </p>
    <p>
        For more information on
        <code>
            Scanner
        </code>
        and other parsing theory, check out the following resources:
    </p>
    <ul>
        <li>
            <a href="/?p=120442" sl-processed="1">
                Swift Tutorial: Working with JSON
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/mac/documentation/cocoa/reference/foundation/classes/NSScanner_Class/Reference/Reference.html"
            sl-processed="1">
                Apple: Scanner Reference Guide
            </a>
        </li>
        <li>
            <a href="/?p=553" sl-processed="1">
                XML Tutorial for iOS – How to choose the best XML parser for your iPhone-Project
            </a>
            (in Objective-C)
        </li>
        <li>
            <a href="http://www.cocoawithlove.com/2009/11/writing-parser-using-nsscanner-csv.html"
            sl-processed="1">
                Writing a parser using NSScanner (a CSV parsing example)
            </a>
            by Matt Gallagher (in Objective-C)
        </li>
        <li>
            <a href="http://prezi.com/jlstnqcytmvz/ios-sharing-session/" sl-processed="1">
                Short Presentation on NSScanner
            </a>
            by Lorex Antiono (in Objective-C)
        </li>
    </ul>
</div>