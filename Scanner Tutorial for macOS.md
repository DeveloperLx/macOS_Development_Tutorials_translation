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
            本教程已由Hai Nguyen更新至Swift版。原教程由Vincent Ngo撰写。
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
        时代，数据是以多种格式保存的，这就使得处理它成为了一项挑战。如果你幸运的话，数据会是有组织和层次的格式，就像
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
        这样。否则，你就会挣扎在无尽的if/case语句之间。另一方面，手动地摘取数据也是非常无聊的。
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
        。它们各自都有各自的优势，但到目前为止，
        <code>
            Scanner
        </code>
        是最容易使用的，不仅功能强大，而且非常灵活。在本教程中，你将会学习如何使用它，来从电子邮件的信息中抽取信息，去构建一个macOS应用。它工作起来，就像如下所示的苹果的Mail界面这样。
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
            对象，并将它的
            <code>
                charactersToBeSkipped
            </code>
            默认值（空格和换行符）修改为
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
            </code>
            ，因此为了将他们传给scanner的方法，你不得不将这些变量声明为可选的
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
        。
    </div>
    <p>
        运行项目来在实际中查看它。
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
        在深入解析之前，理解你要实现的，是一个什么样的效果是非常重要的。以下是样本文件中的一个，你将重点检索的数据项。
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
                scanDecimal(\_:)
            </li>
            <li>
                scanFloat(\_:)
            </li>
            <li>
                scanHexDouble(\_:)
            </li>
            <li>
                scanHexFloat(\_:)
            </li>
            <li>
                scanHexInt32(\_:)
            </li>
            <li>
                scanHexInt64(\_:)
            </li>
            <li>
                scanInt(\_:)
            </li>
            <li>
                scanInt32(\_:)
            </li>
            <li>
                scanInt64(\_:)
            </li>
        </ul>
    </div>
    <p>
        很简单，不是么？现在返回主项目并开始进行解析吧！
    </p>
    <h2>
        创建数据结构
    </h2>
    <p>
        找到
        <em>
            File\New\File…
        </em>
        （或只需按下
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
            HardwarePost.swift
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
            HardwarePost.swift
        </em>
        并添加下列的结构体：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">struct</span> <span class="hljs-title">HardwarePost</span> </span>{
  <span class="hljs-comment">// MARK: Properties</span>
  
  <span class="hljs-comment">// the fields' values once extracted placed in the properties</span>
  <span class="hljs-keyword">let</span> email: <span class="hljs-type">String</span>
  <span class="hljs-keyword">let</span> sender: <span class="hljs-type">String</span>
  <span class="hljs-keyword">let</span> subject: <span class="hljs-type">String</span>
  <span class="hljs-keyword">let</span> date: <span class="hljs-type">String</span>
  <span class="hljs-keyword">let</span> organization: <span class="hljs-type">String</span>
  <span class="hljs-keyword">let</span> numberOfLines: <span class="hljs-type">Int</span>
  <span class="hljs-keyword">let</span> message: <span class="hljs-type">String</span>
  
  <span class="hljs-keyword">let</span> costs: [<span class="hljs-type">Double</span>]         <span class="hljs-comment">// cost related information</span>
  <span class="hljs-keyword">let</span> keywords: <span class="hljs-type">Set</span>&lt;<span class="hljs-type">String</span>&gt;   <span class="hljs-comment">// set of distinct keywords</span>
}
</pre>
    <p>
        以上代码定义了
        <code>
            HardwarePost
        </code>
        结构体，它可以用来储存解析到的数据。默认情况下，
        <em>
            Swift
        </em>
        基于结构体的property，向你提供了一个默认的构造方法，但你会在之后回到这里，来实现你自己的初始化方法。
    </p>
    <p>
        准备好用
        <code>
            Scanner
        </code>
        解析数据了么？动手吧。
    </p>
    <h2>
        创建数据解析器
    </h2>
    <p>
        找到
        <em>
            File\New\File…
        </em>
        （或只需按下
        <em>
            Command+N
        </em>
        键），选择
        <em>
            macOS &gt; Source &gt; Swift File
        </em>
        并点击
        <em>
            Next
        </em>
        。设置文件的名称为
        <em>
            ParserEngine.swift
        </em>
        ，然后点击
        <em>
            Create
        </em>
        。
    </p>
    <p>
        打开
        <em>
            ParserEngine.swift
        </em>
        并添加下列代码，创建
        <code>
            ParserEngine
        </code>
        类：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">final</span> <span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">ParserEngine</span> </span>{

}
</pre>
    <h3>
        提取元数据字段
    </h3>
    <p>
        考虑下列示例的元数据段：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Metadata-Segment-700x211.png"
        alt="Metadata-Segment" width="700" height="211" class="aligncenter size-large wp-image-129689"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Metadata-Segment-700x211.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Metadata-Segment-480x144.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Metadata-Segment-768x231.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        这里是
        <code>
            Scanner
        </code>
        进入并分割字段和它的值的地方。下面的图给出了你这个结构体的一般的视觉上的表示。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Field-Structure-Illustraion-700x75.png"
        alt="Field-Structure-Illustraion" width="700" height="75" class="aligncenter size-large wp-image-129685"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Field-Structure-Illustraion-700x75.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Field-Structure-Illustraion-480x51.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Field-Structure-Illustraion-768x82.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        打开
        <em>
            ParserEngine.swift
        </em>
        并在
        <code>
            ParserEngine
        </code>
        类中添加下列的代码：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-comment">// 1.</span>
<span class="hljs-keyword">typealias</span> <span class="hljs-type">Fields</span> = (sender: <span class="hljs-type">String</span>, email: <span class="hljs-type">String</span>, subject: <span class="hljs-type">String</span>, date: <span class="hljs-type">String</span>, organization: <span class="hljs-type">String</span>, lines: <span class="hljs-type">Int</span>)

<span class="hljs-comment">/// Returns a collection of predefined fields' extracted values</span>
<span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">fieldsByExtractingFrom</span><span class="hljs-params">(<span class="hljs-number">_</span> string: String)</span></span> -&gt; <span class="hljs-type">Fields</span> {
  <span class="hljs-comment">// 2.</span>
  <span class="hljs-keyword">var</span> (sender, email, subject, date, organization, lines) = (<span class="hljs-string">""</span>, <span class="hljs-string">""</span>, <span class="hljs-string">""</span>, <span class="hljs-string">""</span>, <span class="hljs-string">""</span>, <span class="hljs-number">0</span>)
  
  <span class="hljs-comment">// 3.</span>
  <span class="hljs-keyword">let</span> scanner = <span class="hljs-type">Scanner</span>(string: string)
  scanner.charactersToBeSkipped = <span class="hljs-type">CharacterSet</span>(charactersIn: <span class="hljs-string">" :\n"</span>)
  
  <span class="hljs-comment">// 4.</span>
  <span class="hljs-keyword">while</span> !scanner.isAtEnd {                  <span class="hljs-comment">// A</span>
    <span class="hljs-keyword">let</span> field = scanner.scanUpTo(<span class="hljs-string">":"</span>) ?? <span class="hljs-string">""</span> <span class="hljs-comment">// B</span>
    <span class="hljs-keyword">let</span> info = scanner.scanUpTo(<span class="hljs-string">"\n"</span>) ?? <span class="hljs-string">""</span> <span class="hljs-comment">// C</span>
    
    <span class="hljs-comment">// D</span>
    <span class="hljs-keyword">switch</span> field {
    <span class="hljs-keyword">case</span> <span class="hljs-string">"From"</span>: (email, sender) = fromInfoByExtractingFrom(info) <span class="hljs-comment">// E</span>
    <span class="hljs-keyword">case</span> <span class="hljs-string">"Subject"</span>: subject = info
    <span class="hljs-keyword">case</span> <span class="hljs-string">"Date"</span>: date = info
    <span class="hljs-keyword">case</span> <span class="hljs-string">"Organization"</span>: organization = info
    <span class="hljs-keyword">case</span> <span class="hljs-string">"Lines"</span>: lines = <span class="hljs-type">Int</span>(info) ?? <span class="hljs-number">0</span>
    <span class="hljs-keyword">default</span>: <span class="hljs-keyword">break</span>
    }
  }
  
  <span class="hljs-keyword">return</span> (sender, email, subject, date, organization, lines)
}
</pre>
    <p>
        不要惊慌！
        <em>
            Xcode
        </em>
        上的未解决的标识符的错误，将会在下一部分中消失。
    </p>
    <p>
        这里是以上代码所做的事：
    </p>
    <ol>
        <li>
            为解析到的字段的元组定义一个
            <code>
                Fields
            </code>
            类型的别名。
        </li>
        <li>
            创建用来持有返回值的变量
        </li>
        <li>
            初始化一个
            <code>
                Scanner
            </code>
            示例，并将它的
            <code>
                charactersToBeSkipped
            </code>
            property改变为除了它的默认值（空格和换行符）外，还包含一个冒号。
        </li>
        <li>
            通过重复下列的过程，获取全部想要的字段的值：
            <ol>
                <li>
                    使用
                    <code>
                        while
                    </code>
                    来循环访问
                    <code>
                        string
                    </code>
                    的内容，直到它的结尾处。
                </li>
                <li>
                    调用你之前创建的工具方法之一，来获取
                    <code>
                        field
                    </code>
                    位于
                    <code>
                        :
                    </code>
                    之前的标题。
                </li>
                <li>
                    继续扫描至行尾
                    <code>
                        \n
                    </code>
                    处，并将结果赋值给
                    <code>
                        info
                    </code>
                    。
                </li>
                <li>
                    使用
                    <code>
                        switch
                    </code>
                    来找到匹配的字段，并将它的
                    <code>
                        info
                    </code>
                    property的值储存到合适的变量中。                    
                </li>
                <li>
                    调用
                    <code>
                        fromInfoByExtractingFrom(\_:)
                    </code>
                    分析
                    <i>
                        From
                    </i>
                    字段。你将在这部分之后实现这个方法。
                </li>
            </ol>
        </li>
    </ol>
    <p>
        还记得
        <i>
            From
        </i>
        字段这个tricky的部分么？挺住，你将在正则表达式的帮助下克服这个挑战。
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        正则表达式是处理模式字符串的好工具，这篇
        <a href="https://www.raywenderlich.com/30288/nsregularexpression-tutorial-and-cheat-sheet" sl-processed="1">
            NSRegularExpression教程
        </a>
        会给你一个很好的关于如何使用它的概览。
    </div>
    <p>
        在
        <em>
            ParserEngine.swift
        </em>
        的末尾，添加下列的
        <code>
            String
        </code>
        的extension：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">private</span> <span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">String</span> </span>{
  
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">isMatched</span><span class="hljs-params">(<span class="hljs-number">_</span> pattern: String)</span></span> -&gt; <span class="hljs-type">Bool</span> {
    <span class="hljs-keyword">return</span> <span class="hljs-type">NSPredicate</span>(format: <span class="hljs-string">"SELF MATCHES %@"</span>, pattern).evaluate(with: <span class="hljs-keyword">self</span>)
  }
}
</pre>
    <p>
        这个extension定义了一个私有的助手方法，来得出给到的字符串是否匹配给到的正则表达式。
    </p>
    <p>
        它用
        <code>
            NSPredicate
        </code>
        操作符，使用正则表达式创建了一个
        <code>
            NSPredicate
        </code>
        对象。然后调用
        <code>
            evaluate(with:)
        </code>
        来检查字符串是否与之匹配。
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        你可以在
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/Foundation/Classes/NSPredicate_Class/index.html"
        sl-processed="1">
            the official Apple documentation
        </a>
        中读到更多的关于
        <code>
            NSPredicate
        </code>
        的内容。
    </div>
    <p>
        现在添加下列的方法到
        <code>
            ParserEngine
        </code>
        实现的内部，就在
        <code>
            fieldsByExtractingFrom(\_:)
        </code>
        方法之后：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">fileprivate</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">fromInfoByExtractingFrom</span><span class="hljs-params">(<span class="hljs-number">_</span> string: String)</span></span> -&gt; (email: <span class="hljs-type">String</span>, sender: <span class="hljs-type">String</span>) {
  <span class="hljs-keyword">let</span> scanner = <span class="hljs-type">Scanner</span>(string: string)
  
  <span class="hljs-comment">// 1.</span>
  <span class="hljs-comment">/*
   \* ROGOSCHP@MAX.CC.Uregina.CA (Are we having Fun yet ???)
   \* oelt0002@student.tc.umn.edu (Bret Oeltjen)
   \* (iisi owner)
   \* mbuntan@staff.tc.umn.edu ()
   \* barry.davis@hal9k.ann-arbor.mi.us (Barry Davis)
   \*/
   </span>
  <span class="hljs-keyword">if</span> string.isMatched(<span class="hljs-string">".*[\\s]*\\({1}(.*)"</span>) { <span class="hljs-comment">// A</span>
    scanner.charactersToBeSkipped = <span class="hljs-type">CharacterSet</span>(charactersIn: <span class="hljs-string">"() "</span>) <span class="hljs-comment">// B</span>
    <span class="hljs-keyword">let</span> email = scanner.scanUpTo(<span class="hljs-string">"("</span>)  <span class="hljs-comment">// C</span>
    <span class="hljs-keyword">let</span> sender = scanner.scanUpTo(<span class="hljs-string">")"</span>) <span class="hljs-comment">// D</span>
    <span class="hljs-keyword">return</span> (email ?? <span class="hljs-string">""</span>, sender ?? <span class="hljs-string">""</span>)
  }
  
  <span class="hljs-comment">// 2.</span>
  <span class="hljs-comment">/*
   \* "Jonathan L. Hutchison" &lt;jh6r+@andrew.cmu.edu&gt;
   \* &lt;BR4416A@auvm.american.edu&gt;
   \* Thomas Kephart &lt;kephart@snowhite.eeap.cwru.edu&gt;
   \* Alexander Samuel McDiarmid &lt;am2o+@andrew.cmu.edu&gt;
   \*/</span>
  <span class="hljs-keyword">if</span> string.isMatched(<span class="hljs-string">".*[\\s]*&lt;{1}(.*)"</span>) {
    scanner.charactersToBeSkipped = <span class="hljs-type">CharacterSet</span>(charactersIn: <span class="hljs-string">"&lt;&gt; "</span>)
    <span class="hljs-keyword">let</span> sender = scanner.scanUpTo(<span class="hljs-string">"&lt;"</span>)
    <span class="hljs-keyword">let</span> email = scanner.scanUpTo(<span class="hljs-string">"&gt;"</span>)
    <span class="hljs-keyword">return</span> (email ?? <span class="hljs-string">""</span>, sender ?? <span class="hljs-string">""</span>)
  }
  
  <span class="hljs-comment">// 3.</span>
  <span class="hljs-keyword">return</span> (<span class="hljs-string">"unknown"</span>, string)
}
</pre>
    <p>
        在检查了49个数据集之后，最后考虑以下三种case：
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
            没有名称的
            <em>
                email
            </em>
        </li>
    </ul>
    <p>
        以上代码完成了：
    </p>
    <ol>
        <li>
            用第一个模式 - 
            <i>
                email (name)
            </i>
            匹配
            <code>
                string
            </code>
            。如果不匹配的话，执行到下一个case。
            <ol>
                <li>
                    <code>
                        .*
                    </code>
                    可以用来查找零个或多个任意的字符，后跟零个或多个的空格 - 
                    <code>
                        [\\s]*
                    </code>
                    ，后跟一个开发的括号 - 
                    <code>
                        \\({1}
                    </code>
                    ，最后则是一个或多个的字符串 - 
                    <code>
                        (.*)
                    </code>
                    。
                </li>
                <li>
                    设置
                    <code>
                        Scanner
                    </code>
                    对象的
                    <code>
                        charactersToBeSkipped
                    </code>
                    包含“(”,“)”和空格。
                </li>
                <li>
                    扫描到
                    <code>
                        (
                    </code>
                    来获取
                    <code>
                        email
                    </code>
                    的值。
                </li>
                <li>
                    扫描到
                    <code>
                        )
                    </code>
                    ，这会给到你
                    <code>
                        sender
                    </code>
                    的名称。这就提取了在
                    <code>
                        (
                    </code>
                    和
                    <code>
                        )
                    </code>
                    之间的任何内容。
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
            检查给到的字符创是否匹配模式 -
            <i>
                name &lt;email&gt;
            </i>
            。
            <i>
                if
            </i>
            语句体和第一个场景中几乎是相同的，除了你对尖括号的处理。
        </li>
        <li>
            最终，如果两种模式都不匹配，那么就只有一份电子邮件。你只需返回email的字符串，sender则返回“unknown”。
        </li>
    </ol>
    <p>
        现在，你可以build你的项目了。之前的编译错误消失了。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Starter-Initial-Screen-683x500.png"
        alt="Starter-Initial-Screen" width="683" height="500" class="aligncenter size-large wp-image-129690"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Starter-Initial-Screen-683x500.png 683w, https://koenig-media.raywenderlich.com/uploads/2016/03/Starter-Initial-Screen-437x320.png 437w, https://koenig-media.raywenderlich.com/uploads/2016/03/Starter-Initial-Screen-768x563.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/Starter-Initial-Screen.png 804w"
        sizes="(max-width: 683px) 100vw, 683px">
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        <code>
            NSDataDetector
        </code>
        对类似于电话号码，地址，邮箱这样的已知的数据类型来讲，是一个更好的解决方案。你可以访问
        <a href="https://www.cocoanetics.com/2014/06/e-mail-validation/" sl-processed="1">
            这篇
        </a>
        关于使用
        <code>
            NSDataDetector
        </code>
        验证电子邮箱的博客。
    </div>
    <p>
        你已经使用了
        <code>
            Scanner
        </code>
        来分析和检索来自于模式字符串的信息。在接下来的两节中，你将了解到如何去解析非结构化的数据。
    </p>
    <h3>
        提取成本相关的信息
    </h3>
    <p>
        解析非结构化数据的一个很好的例子，就是确定电子邮件的正文中是否包含成本相关的信息。为了实现这点，你将使用
        <code>
            Scanner
        </code>
        来搜索一个美元字符：
        <em>
            $
        </em>
        的出现。
    </p>
    <p>
        仍然在
        <em>
            ParserEngine.swift
        </em>
        中，添加下列的实现到
        <code>
            ParserEngine
        </code>
        类中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">costInfoByExtractingFrom</span><span class="hljs-params">(<span class="hljs-number">_</span> string: String)</span></span> -&gt; [<span class="hljs-type">Double</span>] {
  <span class="hljs-comment">// 1.</span>
  <span class="hljs-keyword">var</span> results = [<span class="hljs-type">Double</span>]()
  
  <span class="hljs-comment">// 2.</span>
  <span class="hljs-keyword">let</span> dollar = <span class="hljs-type">CharacterSet</span>(charactersIn: <span class="hljs-string">"$"</span>)
  
  <span class="hljs-comment">// 3.</span>
  <span class="hljs-keyword">let</span> scanner = <span class="hljs-type">Scanner</span>(string: string)
  scanner.charactersToBeSkipped = dollar
  
  <span class="hljs-comment">// 4.</span>
  <span class="hljs-keyword">while</span> !scanner.isAtEnd &amp;&amp; scanner.scanUpToCharacters(from: dollar, into: <span class="hljs-literal">nil</span>) {
    results += [scanner.scanDouble()].flatMap { $<span class="hljs-number">0</span> }
  }
  
  <span class="hljs-keyword">return</span> results
}
</pre>
    <p>
        这个代码相当地直接：
    </p>
    <ol>
        <li>
            定义一个空数组来保存费用的值。
        </li>
        <li>
            使用
            <code>
                $
            </code>
            字符创建一个
            <code>
                CharacterSet
            </code>
            对象。
        </li>
        <li>
            初始化一个
            <code>
                Scanner
            </code>
            实例，并配置它忽略
            <em>
                $
            </em>
            字符。
        </li>
        <li>
            遍历
            <code>
                string
            </code>
            的内容，当
            <code>
                $
            </code>
            字符被找到时，使用你的助手方法抓取
            <code>
                $
            </code>
            字符后的数字，并将它添加到
            <code>
                results
            </code>
            数组中。
        </li>
    </ol>
    <h3>
        解析消息
    </h3>
    <p>
        解析非结构化数据的另一个例子，是在给到的文本内容中找到关键字。你的搜索策略，是查找每一个单词，并检查一组关键字，看它是否匹配。你将使用
        <em>
            空格
        </em>
        和
        <em>
            换行符
        </em>
        来将消息中的单词进行扫描。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/Keywords-Parser-Illustration-700x102.png"
        alt="Keywords-Parser-Illustration" width="700" height="102" class="aligncenter size-large wp-image-129687"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/Keywords-Parser-Illustration-700x102.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/Keywords-Parser-Illustration-480x70.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/Keywords-Parser-Illustration-768x112.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        在
        <code>
            ParserEngine
        </code>
        类的尾部添加下列代码：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-comment">// 1.</span>
<span class="hljs-keyword">let</span> keywords: <span class="hljs-type">Set</span>&lt;<span class="hljs-type">String</span>&gt; = [<span class="hljs-string">"apple"</span>, <span class="hljs-string">"macs"</span>, <span class="hljs-string">"software"</span>, <span class="hljs-string">"keyboard"</span>,
                             <span class="hljs-string">"printers"</span>, <span class="hljs-string">"printer"</span>, <span class="hljs-string">"video"</span>, <span class="hljs-string">"monitor"</span>,
                             <span class="hljs-string">"laser"</span>, <span class="hljs-string">"scanner"</span>, <span class="hljs-string">"disks"</span>, <span class="hljs-string">"cost"</span>, <span class="hljs-string">"price"</span>,
                             <span class="hljs-string">"floppy"</span>, <span class="hljs-string">"card"</span>, <span class="hljs-string">"phone"</span>]

<span class="hljs-comment">/// Return a set of keywords extracted from</span>
<span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">keywordsByExtractingFrom</span><span class="hljs-params">(<span class="hljs-number">_</span> string: String)</span></span> -&gt; <span class="hljs-type">Set</span>&lt;<span class="hljs-type">String</span>&gt; {
  <span class="hljs-comment">// 2.</span>
  <span class="hljs-keyword">var</span> results: <span class="hljs-type">Set</span>&lt;<span class="hljs-type">String</span>&gt; = []
  
  <span class="hljs-comment">// 3.</span>
  <span class="hljs-keyword">let</span> scanner = <span class="hljs-type">Scanner</span>(string: string)
  
  <span class="hljs-comment">// 4.</span>
  <span class="hljs-keyword">while</span> !scanner.isAtEnd, <span class="hljs-keyword">let</span> word = scanner.scanUpTo(<span class="hljs-string">" "</span>)?.lowercased()  {
    <span class="hljs-keyword">if</span> keywords.<span class="hljs-built_in">contains</span>(word) {
      results.insert(word)
    }
  }
  
  <span class="hljs-keyword">return</span> results
}
</pre>
    <p>
        以上代码：
    </p>
    <ol>
        <li>
            定义了你将匹配的关键字的集合。
        </li>
        <li>
            创建一个
            <code>
                String
            </code>
            的
            <code>
                Set
            </code>
            来保存找到的关键字。
        </li>
        <li>
            初始化一个
            <code>
                Scanner
            </code>
            的实例。你将采用默认的
            <code>
                charactersToBeSkipped
            </code>
            值，即空格和换行符。
        </li>
        <li>
            对于每个发现的单词，检查其是否是预定义的
            <code>
                keywords
            </code>
            之一。如果是的话，添加它到
            <code>
                results
            </code>
            中。
        </li>
    </ol>
    <p>
        在这里，你已经有了获取所需信息的所有必须的方法。是时候投入实用，为49个数据文件创建
        <code>
            HardwarePost
        </code>
        实例。
    </p>
    <h2>
        使用数据样本连接解析器
    </h2>
    <p>
        打开
        <em>
            HardwarePost.swift
        </em>
        并添加下面的初始化器到
        <code>
            HardWarePost
        </code>
        结构体中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">init</span>(fromData data: <span class="hljs-type">Data</span>) {
  <span class="hljs-comment">// 1.</span>
  <span class="hljs-keyword">let</span> parser = <span class="hljs-type">ParserEngine</span>()
  
  <span class="hljs-comment">// 2.</span>
  <span class="hljs-keyword">let</span> string = <span class="hljs-type">String</span>(data: data, encoding: <span class="hljs-type">String</span>.<span class="hljs-type">Encoding</span>.utf8) ?? <span class="hljs-string">""</span>
  
  <span class="hljs-comment">// 3.</span>
  <span class="hljs-keyword">let</span> scanner = <span class="hljs-type">Scanner</span>(string: string)
  
  <span class="hljs-comment">// 4.</span>
  <span class="hljs-keyword">let</span> metadata = scanner.scanUpTo(<span class="hljs-string">"\n\n"</span>) ?? <span class="hljs-string">""</span>
  <span class="hljs-keyword">let</span> (sender, email, subject, date, organization, lines) = parser.fieldsByExtractingFrom(metadata)
  
  <span class="hljs-comment">// 5.</span>
  <span class="hljs-keyword">self</span>.sender = sender
  <span class="hljs-keyword">self</span>.email = email
  <span class="hljs-keyword">self</span>.subject = subject
  <span class="hljs-keyword">self</span>.date = date
  <span class="hljs-keyword">self</span>.organization = organization
  <span class="hljs-keyword">self</span>.numberOfLines = lines
  
  <span class="hljs-comment">// 6.</span>
  <span class="hljs-keyword">let</span> startIndex = string.characters.index(string.startIndex, offsetBy: scanner.scanLocation)                                               <span class="hljs-comment">// A</span>
  <span class="hljs-keyword">let</span> message = string[startIndex..&lt;string.endIndex]                      <span class="hljs-comment">// B</span>
  <span class="hljs-keyword">self</span>.message = message.trimmingCharacters(<span class="hljs-keyword">in</span>: .whitespacesAndNewlines ) <span class="hljs-comment">// C</span>
  
  <span class="hljs-comment">// 7.</span>
  costs = parser.costInfoByExtractingFrom(message)
  keywords = parser.keywordsByExtractingFrom(message)
}
</pre>
    <p>        
        <code>
            HardwarePost
        </code>
        如何初始化它的property：
    </p>
    <ol>
        <li>
            创建名为
            <code>
                parser
            </code>
            的
            <code>
                ParserEngine
            </code>
            对象。
        </li>
        <li>
            将
            <code>
                data
            </code>
            转化为
            <code>
                String
            </code>
            。
        </li>
        <li>
            初始化一个
            <code>
                Scanner
            </code>
            的实例，来解析由“\n\n”分隔的元数据和消息段。
        </li>
        <li>
            扫描到第一个
            <code>
                \n\n
            </code>
            来抓取元数据的字符串，然后调用
            <code>
                parser
            </code>
            的
            <code>
                fieldsByExtractingFrom(\_:)
            </code>
            方法，来获取全部的元数据字段。
        </li>
        <li>
            将解析的结果赋值到
            <code>
                HardwarePost
            </code>
            的property中。
        </li>
        <li>
            准备消息内容：
            <ol>
                <li>
                    使用
                    <code>
                        scanLocation
                    </code>
                    获取
                    <code>
                        scanner
                    </code>
                    当前的读取指针，并将它转化为 
                    <code>
                        String.CharacterView.Index
                    </code>
                    ，这样你就可以通过range来替代
                    <code>
                        string
                    </code>
                    。
                </li>
                <li>
                    将
                    <code>
                        scanner
                    </code>
                    剩余还未读取的字符串赋给新的
                    <code>
                        message
                    </code>
                    变量。
                </li>
                <li>
                    由于
                    <code>
                        message
                    </code>
                    的值仍然包含
                    <code>
                        \n\n
                    </code>
                    ，也就是
                    <code>
                        scanner
                    </code>
                    从之前的读取停止的地方，你需要trim它，并将新的值给回到
                    <code>
                        HardwarePost
                    </code>
                    实例的
                    <code>
                        message
                    </code>
                    property中。
                </li>
            </ol>
        </li>
        <li>
            用
            <code>
                message
            </code>
            调用
            <code>
                parser
            </code>
            的方法，来检索
            <code>
                cost
            </code>
            和
            <code>
                keywords
            </code>
            property的值。
        </li>
    </ol>
    <p>
        现在，你就可以由文件的数据直接创建
        <code>
            HardwarePost
        </code>
        实例。你距离展现出最后的产品已只剩几步之遥了！
    </p>
    <h2>
        展示解析出的数据
    </h2>
    <p>
        打开
        <em>
            PostCell.swift
        </em>
        并添加下列的方法到
        <code>
            PostCell
        </code>
        类的实现中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">configure</span><span class="hljs-params">(<span class="hljs-number">_</span> post: HardwarePost)</span></span> {
  
  senderLabel.stringValue = post.sender
  emailLabel.stringValue = post.email
  dateLabel.stringValue = post.date
  subjectLabel.stringValue = post.subject
  organizationLabel.stringValue = post.organization
  numberOfLinesLabel.stringValue = <span class="hljs-string">"<span class="hljs-subst">\(post.numberOfLines)</span>"</span>
  
  <span class="hljs-comment">// 1.</span>
  costLabel.stringValue = post.costs.isEmpty ? <span class="hljs-string">"NO"</span> : 
                                               post.costs.<span class="hljs-built_in">map</span> { <span class="hljs-string">"<span class="hljs-subst">\($<span class="hljs-number">0</span>)</span>"</span> }.<span class="hljs-built_in">lazy</span>.joined(separator: <span class="hljs-string">"; "</span>)
  
  <span class="hljs-comment">// 2.</span>
  keywordsLabel.stringValue = post.keywords.isEmpty ? <span class="hljs-string">"No keywords found"</span> : 
                                                      post.keywords.joined(separator: <span class="hljs-string">"; "</span>)
}
</pre>
    <p>
        上面的代码将post的值分配给了cell label。
        <code>
            costLabel
        </code>
        和
        <code>
            keywordsLabel
        </code>
        需要特殊的处理，因为它们可以为空。这里是会发生的事：
    </p>
    <ol>
        <li>
            如果
            <code>
                costs
            </code>
            数组为空，就设置
            <code>
                costLabel
            </code>
            的string值为
            <em>
                NO
            </em>
            ；否则，就用“;”这个操作符连接cost的值。
        </li>
        <li>
            类似的，当
            <code>
                post.keywords
            </code>
            是一个空集合时，设置
            <code>
                keywordsLabel
            </code>
            的string值为
            <code>
                No words found
            </code>
            。
        </li>
    </ol>
    <p>
        你几乎已要搞定了！打开
        <em>
            DataSource.swift
        </em>
        。删除
        <code>
            DataSource
        </code>
        初始化器
        <code>
            init()
        </code>
        并添加下列的代码到这个类中：
    </p>
    <pre lang="swift">let hardwarePosts: [HardwarePost] // 1.

override init() {
  self.hardwarePosts = Bundle.main                                                // 2.
    .urls(forResourcesWithExtension: nil, subdirectory: "comp.sys.mac.hardware")? // 3.
    .flatMap( { try? Data(contentsOf: $0) }).lazy                                 // 4.                                                                    
    .map(HardwarePost.init) ?? []                                                 // 5.
  
  super.init()
}
</pre>
    <p>
        上述代码：
    </p>
    <ol>
        <li>
            储存
            <code>
                HardwarePost
            </code>
            实例。
        </li>
        <li>
            获取指向app主Bundle的引用。
        </li>
        <li>
            检索在
            <em>
                comp.sys.mac.hardware
            </em>
            目录中的示例文件的url。
        </li>
        <li>
            通过使用
            <code>
                Data
            </code>
            的可是白初始化器和
            <code>
                flatMap(\_:)
            </code>
            读取文件内容，惰性获取
            <code>
                Data
            </code>
            实例的数组。使用
            <code>
                flatMap(\_:)
            </code>
            是要获取元素不为
            <code>
                nil
            </code>
            的子数组。
        </li>
        <li>
            最后，将
            <code>
                Data
            </code>
            的结果转换为
            <code>
                HardwarePost
            </code>
            对象，并将它们赋给
            <code>
                DataSource
            </code>
            的
            <code>
                hardwarePosts
            </code>
            property。
        </li>
    </ol>
    <p>
        现在你需要配置table view的data source和delegate，让app可以展示你的工作成果。
    </p>
    <p>
        打开
        <em>
            DataSource.swift
        </em>
        。找到
        <code>
            numberOfRows(in:)
        </code>
        ，并使用下列代码来替换它：
    </p>
    <pre lang="swift">func numberOfRows(in tableView: NSTableView) -&gt; Int {
    return hardwarePosts.count
}
</pre>
    <p>
        <code>
            numberOfRows(in:)
        </code>
        是table view的data source协议的一部分；它设置了table view的行数。
    </p>
    <p>
        接下来，找到
        <code>
            tableView(\_:viewForTableColumn:row:)
        </code>
        ，并使用下列代码替换注释
        <code>
            //TODO: Set up cell view
        </code>
        ：
    </p>
    <pre lang="swift">cell.configure(hardwarePosts[row])
</pre>
    <p>
        table view会调用代理方法
        <code>
            tableView(\_:viewForTableColumn:row:)
        </code>
        来设置每个cell。它为相应的行获取post的引用，并调用
        <code>
            PostCell
        </code>
        的
        <code>
            configure(\_:)
        </code>
        方法来展示数据。
    </p>
    <p>
        现在你需要当在table view中选择一个post时，在text view上展示它。使用下列代码替换
        <code>
            tableViewSelectionDidChange(\_:)
        </code>
        的实现：
    </p>
    <pre lang="swift">func tableViewSelectionDidChange(_ notification: Notification) {
  guard let tableView = notification.object as? NSTableView else {
    return
  }
  textView.string = hardwarePosts[tableView.selectedRow].message
}
</pre>
    <p>
        <code>
            tableViewSelectionDidChange(\_:)
        </code>
        方法会在table view的选择发生变化时被调用。当调用发生时，这个代码就会获取选择的行的硬件post，并在text view中展示
        <code>
            message
        </code>
        。
    </p>
    <p>
        运行你的项目。
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
        所有被解析的字段现在都已经很好地展示在table上了。选择一个左侧的cell，你就会在右侧看到相应的信息。Good Job！
    </p>
    <h2>
        从这儿去向哪里？
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
                            想要学习得更快？通过我们的
                            <span>
                                视频课程
                            </span>
                            来节约时间吧
                        </span>
                    </div>
                </div>
            </a>
        </div>
    </div>
    <p>
        这里是完整项目的
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/09/EmailParser-final-project.zip"
        sl-processed="1">
            源码
        </a>
        。
        <br>
        有很多你可以基于解析到的数据去做的事。你可以写一个格式转换器，将
        <code>
            HardwarePost
        </code>
        对象转换为JSON，XML，CSV或其它格式。你可以通过新发现的灵活性，来以不同的格式展示数据，你可以在不同的平台上分享数据。
    </p>
    <p>
        如果你感兴趣于学习计算机语言，已经它们是如何实现的，可以参加
        If you’re interested in the study of computer languages and how they are
        implemented, take a class in
        <i>
            comparative
        </i>
        语言的课程。你的课程将可能覆盖正式的语言，和BNF（巴科斯-诺尔范式）语法的有关设计和实现解析器的重要的概念。
    </p>
    <p>
        有关
        <code>
            Scanner
        </code>
        和其它解析理论的更多信息，请访问下列资源：
    </p>
    <ul>
        <li>
            <a href="https://www.raywenderlich.com/150322/swift-json-tutorial-2" sl-processed="1">
                Swift教程：使用JSON
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/mac/documentation/cocoa/reference/foundation/classes/NSScanner_Class/Reference/Reference.html"
            sl-processed="1">
                Apple：Scanner参考指南
            </a>
        </li>
        <li>
            <a href="https://www.raywenderlich.com/553/xml-tutorial-for-ios-how-to-choose-the-best-xml-parser-for-your-iphone-project" sl-processed="1">
                iOS的XML教程 - 如果为你的iPhone项目选择最好的XML解析器
            </a>
            （Objective-C）
        </li>
        <li>
            <a href="http://www.cocoawithlove.com/2009/11/writing-parser-using-nsscanner-csv.html"
            sl-processed="1">
                使用NSScanner写一个解析器（一个CSV的解析例子）
            </a>
            - Matt Gallagher（Objective-C）
        </li>
        <li>
            <a href="http://prezi.com/jlstnqcytmvz/ios-sharing-session/" sl-processed="1">
                NSScanner的简短介绍
            </a>
            - Lorex Antiono（Objective-C）
        </li>
    </ul>
</div>