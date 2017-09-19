# OS X NSTask教程

#### [原文地址](https://www.raywenderlich.com/125071/nstask-tutorial-os-x) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)


<div class="content-wrapper">
    <div id="attachment_129761" style="width: 260px" class="wp-caption alignright">
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/NSTask-for-mac-feature.png"
        rel="attachment wp-att-129761" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/NSTask-for-mac-feature-250x250.png"
            alt="See a practical example of using NSTask!" width="250" height="250"
            class="size-thumbnail wp-image-129761 bordered" srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/NSTask-for-mac-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/03/NSTask-for-mac-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/03/NSTask-for-mac-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/03/NSTask-for-mac-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/03/NSTask-for-mac-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/03/NSTask-for-mac-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/03/NSTask-for-mac-feature-128x128.png 128w"
            sizes="(max-width: 250px) 100vw, 250px">
        </a>
        <p class="wp-caption-text">
            查看一个使用NSTask的特别的例子！
        </p>
    </div>
    <div class="note">
        <em>
            更新笔记：
        </em>
        这个OS X的NSTask教程，已由
        <a href="https://www.raywenderlich.com/u/warrenburton" sl-processed="1">
            Warren Burton
        </a>
        更新为Swift版的了。原教程是由
        <a href="https://www.raywenderlich.com/u/macandyp" sl-processed="1">
            Andy Pereira
        </a>
        撰写的。
    </div>
    <p>
        你的Mac是由一个成熟版本的UNIX作为操作系统的，这意味着它含有大量预装的命令行工具和脚本语言。Swift、Perl、Python、Bash、Ruby以及任何你可以安装的。使用这个来创建awesome的app，难道不是很棒么？
    </p>
    <p>
        <code>
            NSTask
        </code>
        让你可以在你的机器上执行另一个程序，作为一个子进程，并在你的主程序运行的时候，监视它的执行状态。例如，你可以运行
        <code>
            ls
        </code>
        命令来展示一个目录的列表 - 就是从你的app中！
    </p>
    <p>
        一个
        <code>
            NSTask
        </code>
        的很好的类比是父母和孩子的关系。一个父母可以创建一个孩子，并告诉它去做确定的事情，（理论上）孩子必须服从。
        <code>
            NSTask
        </code>
        表现为类似的方式；你启动一个“孩子”程序，给它指示，并告诉它在哪里报告任何的输出或错误。但会更好 - 它会比你一般的学步小孩更顺从 :]
    </p>
    <p>
        <code>
            NSTask
        </code>
        的一个很棒的用途，是用来提供命令行程序的前端GUI。命令行的程序是很有用的，但它们要求你准确地记住。它们在你机器上的什么地方，怎么来调用它们，以及你可以为它们提供什么选项或参数。在前端添加一个GUI，可以提供给用户大量的控制能力 - 无需成为一个命令行的专家（gurn）！
    </p>
    <p>
        本教程包含一个
        <code>
            NSTask
        </code>
        示例，它会展示给你如何执行一个简单的，带有参数的命名行程序，并在它允许时，展示它的标准输出到一个text field中。最后，你就可以在你的自己的app中使用NSTask了！
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            这个教程假定你对Mac OS X开发和终端已有一些基本的熟悉度。如果你对于Mac编程是纯小白，请查看我们的
            <a href="https://www.raywenderlich.com/17811/how-to-make-a-simple-mac-app-on-os-x-10-7-tutorial-part-13" sl-processed="1">
                初学者Mac OS X开发教程系列
            </a>
            。
        </p>
    </div>
    <h2>
        入门
    </h2>
    <p>
        为了把注意力直接集中在NSTask上，我已经为你创建了一个启动项目，它包含了基本的用户界面。
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/TasksProject-starter_s3.zip"
        sl-processed="1">
            下载这个项目
        </a>
        ，并在Xcode中打开，运行项目。
    </p>
    <p>
        这个启动的app有一个window，就像下面这样：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/02/initial_view-562x500.png"
        alt="initial_view" width="562" height="500" class="aligncenter size-large wp-image-126818"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/02/initial_view-562x500.png 562w, https://koenig-media.raywenderlich.com/uploads/2016/02/initial_view-360x320.png 360w, https://koenig-media.raywenderlich.com/uploads/2016/02/initial_view-768x683.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/02/initial_view.png 956w"
        sizes="(max-width: 562px) 100vw, 562px">
    </p>
    <p>
        这个window有一个标题“TasksProject”。它包含一个简单的GUI，它将通过调用shell脚本，来让你构建一个iOS项目，创建一个
        <code>
            ipa
        </code>
        并观察正在发生什么。
    </p>
    <h2>
        创建你的第一个NSTask
    </h2>
    <p>
        <code>
            NSTask
        </code>
        的示例，将通过
        <code>
            NSTask
        </code>
        在后台运行一些命令程序，来build并打包一个iOS app到
        <code>
            ipa
        </code>
        文件。大多数基本的UI功能都已到位 - 你的工作的重点都在
        <code>
            NSTask
        </code>
        上。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            建议你要有一个苹果iOS开发者的账号，因为你需要合适的证书和provisioning profile来创建一个
            <code>
                ipa
            </code>
            文件，它可以安装到你的一个设备上。如果你没有也不要担心，你同样可以在没有这个账号的情况下，follow整个教程。
        </p>
    </div>
    <p>
        现在你将在嵌入的，标题为“Tasks View Controller”的View Controller中工作。在这个window中的第一部分，会请求用户选择一个Xcode项目的目录。为了节省时间，你将硬编码为一个你自己的Xcode项目目录，而不是在每次测试运行你的app时，手动选择一个目录。
    </p>
    <p>
        要这么做，回到Xcode并打开
        <em>
            TasksViewController.swift
        </em>
        。看一下注释“Window Outlets“下的property和方法：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #008312;">//View Controller Outlets</span>
<span style="color: #B833A1;">@IBOutlet</span> <span style="color: #B833A1;">var</span> outputText<span style="color: black;">:</span><span style="color: #6F41A7;">NSTextView</span><span style="color: black;">!</span>
<span style="color: #B833A1;">@IBOutlet</span> <span style="color: #B833A1;">var</span> spinner<span style="color: black;">:</span><span style="color: #6F41A7;">NSProgressIndicator</span><span style="color: black;">!</span>
<span style="color: #B833A1;">@IBOutlet</span> <span style="color: #B833A1;">var</span> projectPath<span style="color: black;">:</span><span style="color: #6F41A7;">NSPathControl</span><span style="color: black;">!</span>
<span style="color: #B833A1;">@IBOutlet</span> <span style="color: #B833A1;">var</span> repoPath<span style="color: black;">:</span><span style="color: #6F41A7;">NSPathControl</span><span style="color: black;">!</span>
<span style="color: #B833A1;">@IBOutlet</span> <span style="color: #B833A1;">var</span> buildButton<span style="color: black;">:</span><span style="color: #6F41A7;">NSButton</span><span style="color: black;">!</span>
<span style="color: #B833A1;">@IBOutlet</span> <span style="color: #B833A1;">var</span> targetName<span style="color: black;">:</span><span style="color: #6F41A7;">NSTextField</span><span style="color: black;">!</span></pre>
    <p>
        所有的这些property都对应于
        <em>
            Main.storyboard
        </em>
        中的
        <em>
            Tasks View Controller Scene
        </em>
        。注意
        <code>
            projectPath
        </code>
        property — 这是你想要改变的那一个。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        并单击
        <em>
            Project Location
        </em>
        这项。你会发现在对象的层级上位于第四层；它是
        <em>
            Stack View
        </em>
        的一个“孩子”。在
        <code>
            Attributes Inspector
        </code>
        中，
        <em>
            Path Control
        </em>
        下，找到
        <em>
            Path
        </em>
        元素：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/set_path_1b-700x385.png"
        alt="set_path_1b" width="700" height="385" class="aligncenter size-large wp-image-128235"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/set_path_1b-700x385.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/set_path_1b-480x264.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/set_path_1b-768x423.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        设置
        <em>
            Path
        </em>
        为一个你的机器上包含iOS项目的目录。确保你使用的是项目的
        <i>
            parent
        </i>
        目录，而不是
        <code>
            .xcodeproj
        </code>
        文件它本身。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            如果在你的你机器上没有任何的iOS项目，
            <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/SuperDuperApp_s3.zip"
            sl-processed="1">
                就在这里下载一个简单的项目
            </a>
            ，并将其解压到你机器上。然后使用前面的说明来设置你应用中的
            <code>
                Path
            </code>
            property。例如，如果你把这个包解压到了桌面上，你就应该设置 
            <code>
                Path
            </code>
            为
            <code>
                <br>
                /Users/YOUR_USERNAME_HERE/Desktop/SuperDuperApp
            </code>
            。
        </p>
    </div>
    <p>
        既然你在app中，有了一个默认的源项目路径来协助测试，你也需要使用一个默认的目的地路径。打开
        <em>
            Main.storyboard
        </em>
        并单击
        <em>
            Build Repository
        </em>
        项。
    </p>
    <p>
        在Attributes Inspector，在
        <em>
            Path Control
        </em>
        下找到
        <em>
            Path
        </em>
        项：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/set_path_2b-700x385.png"
        alt="set_path_2b" width="700" height="385" class="aligncenter size-large wp-image-128236"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/set_path_2b-700x385.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/set_path_2b-480x264.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/set_path_2b-768x423.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        将
        <em>
            Path
        </em>
        设置成一个容易在你的机器上被找到的目录，例如Desktop。它会是这个应用所创建的
        <code>
            .ipa
        </code>
        文件将要放置的地方。
    </p>
    <p>
        这两个
        <code>
            Tasks View Controller Scene
        </code>
        中额外的地方，你需要了解：
        <em>
            Target Name
        </em>
        和一个关联的text field。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/02/initial_view_2-562x500.png"
        alt="initial_view_2" width="562" height="500" class="aligncenter size-large wp-image-126819"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/02/initial_view_2-562x500.png 562w, https://koenig-media.raywenderlich.com/uploads/2016/02/initial_view_2-360x320.png 360w, https://koenig-media.raywenderlich.com/uploads/2016/02/initial_view_2-768x683.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/02/initial_view_2.png 956w"
        sizes="(max-width: 562px) 100vw, 562px">
    </p>
    <ol>
        <li>
            <em>
                Target Name
            </em>
            为你想要build的
            <code>
                Target
            </code>
            的名称。
        </li>
        <li>
            在Target Name下展示的文本域，将在你的项目运行时，展示
            <code>
                NSTask
            </code>
            对象的输出。
        </li>
    </ol>
    <p>
        不知道你iOS项目target的名称？要找到它，在Xcode的project navigator中选择你的项目，并在
        <em>
            Info
        </em>
        tab下查看
        <em>
            TARGETS
        </em>
        。下面的屏幕截图展示了，在哪里可以找到一个叫做“SuperDuperApp”的简单项目。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/02/target_name-700x429.png"
        alt="target_name" width="700" height="429" class="aligncenter size-large wp-image-126825"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/02/target_name-700x429.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/02/target_name-480x294.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/02/target_name-768x471.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/02/target_name.png 1282w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        记住target的名称 - 你将在后面当app运行时输入它。
    </p>
    <p>
        让我们来填充（flesh out）当按下“Build”按钮时，将要运行的代码。
    </p>
    <h2>
        准备Spinner
    </h2>
    <p>
        打开
        <em>
            TasksViewController.swift
        </em>
        并添加下列的代码到
        <code>
            startTask(\_:)
        </code>
        中：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #008312;">//1.</span>
outputText.<span style="color: #508187;">string</span> = <span style="color: #C41A16;">""</span>
&nbsp;
<span style="color: #B833A1;">if</span> <span style="color: #B833A1;">let</span> projectURL = projectPath.<span style="color: #508187;">url</span><span style="color: black;">,</span> <span style="color: #B833A1;">let</span> repositoryURL = repoPath.<span style="color: #508187;">url</span> <span style="color: black;">{</span>
&nbsp;
  <span style="color: #008312;">//2.</span>
  <span style="color: #B833A1;">let</span> projectLocation = projectURL.<span style="color: #508187;">path</span>
  <span style="color: #B833A1;">let</span> finalLocation = repositoryURL.<span style="color: #508187;">path</span>
&nbsp;
  <span style="color: #008312;">//3.</span>
  <span style="color: #B833A1;">let</span> projectName = projectURL.<span style="color: #508187;">lastPathComponent</span>
  <span style="color: #B833A1;">let</span> xcodeProjectFile = projectLocation <span style="color: black;">+</span> <span style="color: #C41A16;">"/<span style="color: #C41A16;">\(</span>projectName).xcodeproj"</span>
&nbsp;
  <span style="color: #008312;">//4.</span>
  <span style="color: #B833A1;">let</span> buildLocation = projectLocation <span style="color: black;">+</span> <span style="color: #C41A16;">"/build"</span>
&nbsp;
  <span style="color: #008312;">//5.</span>
  <span style="color: #B833A1;">var</span> arguments<span style="color: black;">:</span><span style="color: black;">[</span><span style="color: #6F41A7;">String</span><span style="color: black;">]</span> = <span style="color: black;">[</span><span style="color: black;">]</span>
  arguments.<span style="color: #508187;">append</span><span style="color: black;">(</span>xcodeProjectFile<span style="color: black;">)</span>
  arguments.<span style="color: #508187;">append</span><span style="color: black;">(</span>targetName.<span style="color: #508187;">stringValue</span><span style="color: black;">)</span>
  arguments.<span style="color: #508187;">append</span><span style="color: black;">(</span>buildLocation<span style="color: black;">)</span>
  arguments.<span style="color: #508187;">append</span><span style="color: black;">(</span>projectName<span style="color: black;">)</span>
  arguments.<span style="color: #508187;">append</span><span style="color: black;">(</span>finalLocation<span style="color: black;">)</span>
&nbsp;
  <span style="color: #008312;">//6.</span>
  buildButton.<span style="color: #508187;">isEnabled</span> = <span style="color: #B833A1;">false</span>
  spinner.<span style="color: #508187;">startAnimation</span><span style="color: black;">(</span><span style="color: #B833A1;">self</span><span style="color: black;">)</span>
&nbsp;
<span style="color: black;">}</span></pre>
    <p>
        以下是对上述代码一步一步的解释：
    </p>
    <ol>
        <li>
            <code>
                outputText
            </code>
            是window中的大文本框；它会包含所有来自你将要运行的脚本的输出。如果你运行这个脚本多次，你会想在每次运行前清空它，因此第一行会设置
            <code>
                string
            </code>
            property（text框的内容）为一个空字符串。
        </li>
        <li>
            <code>
                projectURL
            </code>
            和
            <code>
                repositoryURL
            </code>
            都是
            <code>
                NSURL
            </code>
            的对象，为了将它们作为参数传你给你的
            <code>
                NSTask
            </code>
            ，代码获取了这些对象的字符串的表示。
        </li>
        <li>
            一般地，目录的名称和项目文件的名称是相同的。在包含于
            <code>
                projectURL
            </code>
            的项目目录，获取
            <code>
                lastPathComponent
            </code>
            property，并添加一个“.xcodeproj”的扩展，来获取项目文件的路径。
        </li>
        <li>
            定义当创建
            <code>
                ipa
            </code>
            文件作为
            <code>
                build
            </code>
            时，产生的中间的build文件，所将要保存在的子目录。
        </li>
        <li>
            将参数保存到一个数组中。这个数组将传递给
            <code>
                NSTask
            </code>
            ，用来在运行命令行工具时，构建
            <code>
                .ipa
            </code>
            文件。
        </li>
        <li>
            禁用“Build”按钮，并启动一个spinner动画。
        </li>
    </ol>
    <p>
        为什么要禁用“Build”按钮？
        <code>
            NSTask
        </code>
        将在每次按下按钮时运行，因此app将在执行
        <code>
            NSTask
        </code>
        的时间内非常忙碌，用户会无耐心地多次点击它 - 每次都会产生一个新的build过程。这个动作避免了用户在app非常忙碌的时候创建按钮的点击事件。
    </p>
    <p>
        运行项目，然后点击
        <em>
            Build
        </em>
        按钮。你应当看到“Build”按钮被禁用，并启动了spinner的动画：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/02/busy1-536x500.png"
        alt="busy1" width="536" height="500" class="aligncenter size-large wp-image-126816"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/02/busy1-536x500.png 536w, https://koenig-media.raywenderlich.com/uploads/2016/02/busy1-343x320.png 343w, https://koenig-media.raywenderlich.com/uploads/2016/02/busy1-768x717.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/02/busy1.png 870w"
        sizes="(max-width: 536px) 100vw, 536px">
    </p>
    <p>
        你的app
        <i>
            看起来
        </i>
        非常得忙碌，但你知道现在实际上，它是没有做任何事的。是时候去添加
        <code>
            NSTask
        </code>
        的魔法了。
    </p>
    <h2>
        添加NSTask到TasksProject
    </h2>
    <p>
        打开
        <em>
            TasksViewController.swift
        </em>
        并添加下面的方法：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #B833A1;">func</span> runScript<span style="color: black;">(</span>_ arguments<span style="color: black;">:</span><span style="color: black;">[</span><span style="color: #6F41A7;">String</span><span style="color: black;">]</span><span style="color: black;">)</span> <span style="color: black;">{</span>
&nbsp;
  <span style="color: #008312;">//1.</span>
  isRunning = <span style="color: #B833A1;">true</span>
&nbsp;
  <span style="color: #008312;">//2.</span>
  <span style="color: #B833A1;">let</span> taskQueue = DispatchQueue.<span style="color: #508187;">global</span><span style="color: black;">(</span>qos<span style="color: black;">:</span> DispatchQoS.<span style="color: #508187;">QoSClass</span>.<span style="color: #508187;">background</span><span style="color: black;">)</span>
&nbsp;
  <span style="color: #008312;">//3.</span>
  taskQueue.<span style="color: #508187;">async</span> <span style="color: black;">{</span>
&nbsp;
   <span style="color: #008312;">//TESTING CODE</span>
&nbsp;
   <span style="color: #008312;">//4.</span>
   Thread.<span style="color: #508187;">sleep</span><span style="color: black;">(</span>forTimeInterval<span style="color: black;">:</span> <span style="color: #1C00CF;">2.0</span><span style="color: black;">)</span>
&nbsp;
   <span style="color: #008312;">//5.  </span>
	DispatchQueue.<span style="color: #508187;">main</span>.<span style="color: #508187;">async</span><span style="color: black;">(</span>execute<span style="color: black;">:</span> <span style="color: black;">{</span>
	  <span style="color: #B833A1;">self</span>.<span style="color: #508187;">buildButton</span>.<span style="color: #508187;">isEnabled</span> = <span style="color: #B833A1;">true</span>
	  <span style="color: #B833A1;">self</span>.<span style="color: #508187;">spinner</span>.<span style="color: #508187;">stopAnimation</span><span style="color: black;">(</span><span style="color: #B833A1;">self</span><span style="color: black;">)</span>
	  <span style="color: #B833A1;">self</span>.<span style="color: #508187;">isRunning</span> = <span style="color: #B833A1;">false</span>
	<span style="color: black;">}</span><span style="color: black;">)</span>
&nbsp;
	<span style="color: #008312;">//TESTING CODE</span>
  <span style="color: black;">}</span>
&nbsp;
<span style="color: black;">}</span></pre>
    <p>
        如果你一步步地看方法，你会看到代码做了下列的事情：
    </p>
    <ol>
        <li>
            设置
            <code>
                isRunning
            </code>
            为
            <code>
                true
            </code>
            。这会允许
            <code>
                Stop
            </code>
            按钮的使用，因为它通过
            <a href="/?p=21752" sl-processed="1">
                Cocoa Bindings
            </a>
            被绑定到了
            <code>
                TasksViewController
            </code>
            的
            <code>
                isRunning
            </code>
            property。你想要让这发生在主线程。
        </li>
        <li>
            创建一个
            <code>
                DispatchQueue
            </code>
            来在后台的线程运行繁重的任务。
        </li>
        <li>
            在
            <code>
                DispatchQueue
            </code>
            中使用
            <code>
                async
            </code>
            。应用将会在主线程继续处理例如按钮点击的时间，但
            <code>
                NSTask
            </code>
            将运行在后台线程直到它完成为止。
        </li>
        <li>
            这是一行临时的代码，让当前的线程睡眠2秒钟，来模拟一个长时间运行的task。
        </li>
        <li>
            当完工时，重新启用
            <code>
                Build
            </code>
            按钮，停止spinner动画，并设置
            <code>
                isRunning
            </code>
            为
            <code>
                false
            </code>
            ，也就禁用了“Stop”按钮。这需要在主线程完成，因为你是在操纵UI元素。
        </li>
    </ol>
    <p>
        既然你已有了一个，可以运行你的task在单独的线程中的方法，你需要在你的app 中的某个地方调用它。
    </p>
    <p>
        仍然在
        <em>
            TasksViewController.swift
        </em>
        中，添加下列的代码到
        <code>
            startTask
        </code>
        的末尾，就在
        <code>
            spinner.startAnimation(self)
        </code>
        的后面：
    </p>
    <pre class="swift" style="font-family:monospace;">runScript<span style="color: black;">(</span>arguments<span style="color: black;">)</span></pre>
    <p>
        上面用你在
        <code>
            startTask
        </code>
        中构建的参数的数组，调用了
        <code>
            runScript
        </code>
        方法。
    </p>
    <p>
        运行项目，点击
        <em>
            Build
        </em>
        按钮。你会注意到，
        <em>
            Build
        </em>
        按钮变成了不可用的状态，
        <code>
            Stop
        </code>
        按钮变成了可用的状态，spinner将开始动画：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/02/busy2-536x500.png"
        alt="busy2" width="536" height="500" class="aligncenter size-large wp-image-126817"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/02/busy2-536x500.png 536w, https://koenig-media.raywenderlich.com/uploads/2016/02/busy2-343x320.png 343w, https://koenig-media.raywenderlich.com/uploads/2016/02/busy2-768x717.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/02/busy2.png 870w"
        sizes="(max-width: 536px) 100vw, 536px">
    </p>
    <p>
        当spinner的动画正在进行时，你仍然可以和应用进行交互。自己试一下 - 例如，你应当可以在spinner活动的时候，在
        <em>
            Target Name
        </em>
        框中进行输入。
    </p>
    <p>
        过了两秒之后，spinner将会消失，
        <em>
            Stop
        </em>
        按钮将会被禁用，
        <em>
            Build
        </em>
        按钮则会变为可用。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            如果你在应用完成睡眠之前，遇到了问题，请增加调用
            <code>
                sleep(forTimeInterval:)
            </code>
            时所传的秒数。
        </p>
    </div>
    <p>
        既然你已经解决了UI响应的问题，你就可以最终实现你对NSTask的调用了。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            Swift使用
            <code>
                Process
            </code>
            这个名字来调用
            <code>
                NSTask
            </code>
            ，因为
            <em>
                Foundation
            </em>
            的framework在Swift 3中去掉了
            <em>
                NS
            </em>
            的前缀。然而，你在本教程中读到的会是NSTask，因为如果你想学到更多的话，它会成为最有用的搜索术语。
        </p>
    </div>
    <p>
        在
        <em>
            TasksViewController.swift
        </em>
        中，找到
        <code>
            runScript
        </code>
        这行，被括号括起来的
        <code>
            //TESTING CODE
        </code>
        注释这里。用下面的代码替换
        <code>
            taskQueue.async
        </code>
        块中的全部内容：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #008312;">//1.</span>
guard <span style="color: #B833A1;">let</span> path = Bundle.<span style="color: #508187;">main</span>.<span style="color: #508187;">path</span><span style="color: black;">(</span>forResource<span style="color: black;">:</span> <span style="color: #C41A16;">"BuildScript"</span><span style="color: black;">,</span>ofType<span style="color: black;">:</span><span style="color: #C41A16;">"command"</span><span style="color: black;">)</span> <span style="color: #B833A1;">else</span> <span style="color: black;">{</span>
  <span style="color: #508187;">print</span><span style="color: black;">(</span><span style="color: #C41A16;">"Unable to locate BuildScript.command"</span><span style="color: black;">)</span>
  <span style="color: #B833A1;">return</span>
<span style="color: black;">}</span>
&nbsp;
<span style="color: #008312;">//2.</span>
<span style="color: #B833A1;">self</span>.<span style="color: #508187;">buildTask</span> = <span style="color: #6F41A7;">Process</span><span style="color: black;">(</span><span style="color: black;">)</span>
<span style="color: #B833A1;">self</span>.<span style="color: #508187;">buildTask</span>.<span style="color: #508187;">launchPath</span> = path
<span style="color: #B833A1;">self</span>.<span style="color: #508187;">buildTask</span>.<span style="color: #508187;">arguments</span> = arguments
&nbsp;
<span style="color: #008312;">//3.</span>
<span style="color: #B833A1;">self</span>.<span style="color: #508187;">buildTask</span>.<span style="color: #508187;">terminationHandler</span> = <span style="color: black;">{</span>
&nbsp;
  task <span style="color: #B833A1;">in</span>
  DispatchQueue.<span style="color: #508187;">main</span>.<span style="color: #508187;">async</span><span style="color: black;">(</span>execute<span style="color: black;">:</span> <span style="color: black;">{</span>
    <span style="color: #B833A1;">self</span>.<span style="color: #508187;">buildButton</span>.<span style="color: #508187;">isEnabled</span> = <span style="color: #B833A1;">true</span>
    <span style="color: #B833A1;">self</span>.<span style="color: #508187;">spinner</span>.<span style="color: #508187;">stopAnimation</span><span style="color: black;">(</span><span style="color: #B833A1;">self</span><span style="color: black;">)</span>
    <span style="color: #B833A1;">self</span>.<span style="color: #508187;">isRunning</span> = <span style="color: #B833A1;">false</span>
  <span style="color: black;">}</span><span style="color: black;">)</span>
&nbsp;
<span style="color: black;">}</span>
&nbsp;
<span style="color: #008312;">//TODO - Output Handling</span>
&nbsp;
<span style="color: #008312;">//4.</span>
<span style="color: #B833A1;">self</span>.<span style="color: #508187;">buildTask</span>.<span style="color: #508187;">launch</span><span style="color: black;">(</span><span style="color: black;">)</span>
&nbsp;
<span style="color: #008312;">//5.</span>
<span style="color: #B833A1;">self</span>.<span style="color: #508187;">buildTask</span>.<span style="color: #508187;">waitUntilExit</span><span style="color: black;">(</span><span style="color: black;">)</span></pre>
    <p>
        上面的代码：
    </p>
    <ol>
        <li>
            获取了
            <code>
                BuildScript.command
            </code>
            脚本的路径，它包含在你的应用的bundle中。这个脚本现在还不存在 - 你将在稍后添加它。
        </li>
        <li>
            创建一个新的
            <code>
                Process
            </code>
            对象，并把它赋给
            <code>
                TasksViewController
            </code>
            的
            <code>
                buildTask
            </code>
            property。
            <code>
                launchPath
            </code>
            property是你想要运行的可执行文件的路径。将
            <code>
                BuildScript.command
            </code>
            的
            <code>
                path
            </code>
            赋值给
            <code>
                Process
            </code>
            的
            <code>
                launchPath
            </code>
            ，然后将传递给
            <code>
                runScript:
            </code>
            的参数赋给
            <code>
                Process
            </code>
            的
            <code>
                arguments
            </code>
            property。
            <code>
                Process
            </code>
            将把参数传递给可执行文件，就像你在终端中输入它们一样。
        </li>
        <li>
            <code>
                Process
            </code>
            有一个
            <code>
                terminationHandler
            </code>
            的property，它包含一个会在任务完成时被执行的block。它会更新UI来反映完成的状态，就像你之前做得一样。
        </li>
        <li>
            为了运行task并执行脚本，调用
            <code>
                Process
            </code>
            对象的
            <code>
                launch
            </code>
            方法。这里同样有终止，打断，挂起或继续一个
            <code>
                Process
            </code>
            的方法。
        </li>
        <li>
            调用
            <code>
                waitUntilExit
            </code>
            ，它告诉
            <code>
                Process
            </code>
            对象block住当前线程的其它活动，直到这个task完成为止。记住，这个代码运行在后台的线程。你的UI，则运行在主线程，将始终响用户的输入。
        </li>
    </ol>
    <p>
        运行你的项目；你不会看到任何
        <i>
            看起来
        </i>
        不同的事，但点击
        <em>
            Build
        </em>
        按钮并查看输出控制台。你会看到像下面这样的错误：
    </p>
    <pre class="swift" style="font-family:monospace;">Unable to locate BuildScript.<span style="color: #508187;">command</span></pre>
    <p>
        这是你刚刚添加到代码开头的guard语句中的日志。由于你至今尚未添加任何的脚本，于是就触发了
        <code>
            guard
        </code>
        。
    </p>
    <p>
        看起来到了写脚本的时候了！:]
    </p>
    <h2>
        撰写一个Build Shell的脚本
    </h2>
    <p>
        在Xcode中，选择
        <em>
            File\New\File…
        </em>
        ，并在
        <em>
            OS X
        </em>
        下选择
        <em>
            Other
        </em>
        的category。选择
        <em>
            Shell Script
        </em>
        并点击
        <em>
            Next
        </em>
        ：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/add-script-1-650x463.png"
        alt="add script to project" width="650" height="463" class="aligncenter size-large wp-image-145431"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/add-script-1-650x463.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/04/add-script-1-449x320.png 449w, https://koenig-media.raywenderlich.com/uploads/2016/04/add-script-1.png 737w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        将文件命名为
        <em>
            BuildScript.command
        </em>
        。在你点击
        <em>
            Create
        </em>
        之前，确保
        <em>
            Targets
        </em>
        下的
        <em>
            TasksProject
        </em>
        已被选中，就像下面这样：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/02/target_choice-647x500.png"
        alt="target_choice" width="647" height="500" class="aligncenter size-large wp-image-126824"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/02/target_choice-647x500.png 647w, https://koenig-media.raywenderlich.com/uploads/2016/02/target_choice-414x320.png 414w, https://koenig-media.raywenderlich.com/uploads/2016/02/target_choice-768x593.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/02/target_choice.png 852w"
        sizes="(max-width: 647px) 100vw, 647px">
    </p>
    <p>
        打开
        <em>
            BuildScript.command
        </em>
        ，并添加下列的命令到文件末尾：
    </p>
    <pre class="objc" style="font-family:monospace;">echo <span style="color: #bf1d1a;">"*********************************"</span>
echo <span style="color: #bf1d1a;">"Build Started"</span>
echo <span style="color: #bf1d1a;">"*********************************"</span>
&nbsp;
echo <span style="color: #bf1d1a;">"*********************************"</span>
echo <span style="color: #bf1d1a;">"Beginning Build Process"</span>
echo <span style="color: #bf1d1a;">"*********************************"</span>
&nbsp;
xcodebuild <span style="color: #002200;">-</span>project <span style="color: #bf1d1a;">"${1}"</span> <span style="color: #002200;">-</span>target <span style="color: #bf1d1a;">"${2}"</span> <span style="color: #002200;">-</span>sdk iphoneos <span style="color: #002200;">-</span>verbose CONFIGURATION_BUILD_DIR<span style="color: #002200;">=</span><span style="color: #bf1d1a;">"${3}"</span>
&nbsp;
echo <span style="color: #bf1d1a;">"*********************************"</span>
echo <span style="color: #bf1d1a;">"Creating IPA"</span>
echo <span style="color: #bf1d1a;">"*********************************"</span>
&nbsp;
<span style="color: #002200;">/</span>usr<span style="color: #002200;">/</span>bin<span style="color: #002200;">/</span>xcrun <span style="color: #002200;">-</span>verbose <span style="color: #002200;">-</span>sdk iphoneos PackageApplication <span style="color: #002200;">-</span>v <span style="color: #bf1d1a;">"${3}/${4}.app"</span> <span style="color: #002200;">-</span>o <span style="color: #bf1d1a;">"${5}/app.ipa"</span></pre>
    <p>
        这就是你的
        <code>
            NSTask
        </code>
        将会调用的全部的build脚本。
    </p>
    <p>
        你所看到的贯穿你的脚本的
        <code>
            echo
        </code>
        命令，将把任何传给它的文本发送到
        <em>
            标准输出
        </em>
        中，你会捕获它作为你的
        <code>
            NSTask
        </code>
        对象的一部分的返回值，并展示到你的
        <code>
            outputText
        </code>
        框中。
        <code>
            echo
        </code>
        语句可以方便地让你知道你的脚本正在做什么，因为很多命令在命令行运行时，并不会提供很多的输出。
    </p>
    <p>
        你会注意到，除了所有的
        <code>
            echo
        </code>
        命令外，还有两个命令：
        <code>
            xcodebuild
        </code>
        和
        <code>
            xcrun
        </code>
        。
    </p>
    <p>
        <em>
            xcodebuild
        </em>
        build你的应用，创建一个
        <code>
            .app
        </code>
        文件，并将其放到子目录
        <em>
            /build
        </em>
        中。回忆一下，你已在
        <code>
            startTask
        </code>
        中创建过一个引用这个目录的参数，因为你需要一个在build和打包的时候，存放中间build文件的地方。
    </p>
    <p>
        <em>
            xcrun
        </em>
        在命令行中运行开发者工具。这里你使用它来调用
        <code>
            PackageApplication
        </code>
        ，它会把
        <code>
            .app
        </code>
        文件打包成一个
        <code>
            .ipa
        </code>
        文件。通过设置
        <code>
            verbose
        </code>
        标记，你将在标准输出中获取大量的细节信息，它们会展示在你的
        <code>
            outputText
        </code>
        框中。
    </p>
    <p>
        在
        <code>
            xcodebuild
        </code>
        和
        <code>
            xcrun
        </code>
        命令中，你会注意到所有的参数被写作了
        <code>
            “${1}”
        </code>
        而不是
        <code>
            $1
        </code>
        。这是因为你的项目的路径可能包含空格。为了处理这种情况，得到正确的路径，你必须把你的文件路径用双引号引起来。通过双引号和花括号，脚本就会恰当地解析全路径，包含空格。
    </p>
    <p>
        这个脚本的其它地方，就是Xcode自动为你添加的那些呢？它们是什么意思？、
    </p>
    <p>
        脚本的第一行如下所示：
    </p>
    <pre class="objc" style="font-family:monospace;"><span style="color: #6e371a;">#!/bin/sh</span></pre>
    <p>
        尽管它看起来像一条评论，因为那个前缀
        <code>
            #
        </code>
        。实际上这行是告诉操作系统，当执行脚本剩余的部分时，使用一个指定的
        <em>
            shell
        </em>
        。它被称作        
        <em>
            shebang
        </em>
        。这个shell就是运行你的命令的解释器，无论是在脚本文件或是从命令行的界面上。
    </p>
    <p>
        有大量不同的shell可以使用，但是它们中的大多数依附在变化的Bourne shell或C shell语法上。你的脚本指明了应当使用
        <em>
            sh
        </em>
        ，它是包含在OS X中的shell之一。
    </p>
    <p>
        如果你想要指定另一个shell来执行你的脚本，就像
        <code>
            bash
        </code>
        ，你就得将第一行改变为恰当的shell的可执行文件的全路径，就像：
    </p>
    <pre class="objc" style="font-family:monospace;"><span style="color: #6e371a;">#!/bin/bash</span></pre>
    <p>
        在脚本中，任何你传递的参数，都是通过一个
        <code>
            $
        </code>
        和一个数字来访问的。
        <code>
            $0
        </code>
        代表你调用的程序的名称，后面跟着的参数依次通过
        <code>
            $1
        </code>
        ，
        <code>
            $2
        </code>
        等等来进行引用。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            Shell脚本存在的时间，就如同计算机一样地长，因此你可以在网上找到更多关于它的信息。例如一个简单（且相关）的开启的地方，可以访问苹果的
            <a href="https://developer.apple.com/library/mac/#documentation/opensource/conceptual/shellscripting/Introduction/Introduction.html"
            alt="Apple Shell Scripting Primer" sl-processed="1">
                Shell脚本入门
            </a>
            。
        </p>
    </div>
    <p>
        现在你已经准备好从
        <code>
            NSTask
        </code>
        去调用你的脚本了，对么？
    </p>
    <p>
        不完全是。此刻，你的脚本文件还没有
        <em>
            执行
        </em>
        的权限。你可以读和写文件，但你并不能执行它。
    </p>
    <p>
        这意味着如果你现在运行app，当你点击Build按钮时，app就会crash。如果你想，就可以尝试一下。这在开发时并没什么大不了，你会在你的Xcode控制台中看到“launch path not accessible”的异常。
    </p>
    <p>
        为了让它可执行，在终端中前往你的项目目录。终端默认位于你的家目录中，因此如果项目是在你的
        <code>
            Documents
        </code>
        目录下，你应该输入命令：
    </p>
    <pre class="command" style="font-family:monospace;">cd Documents/TasksProject</pre>
    <p>
        如果你的项目在除“Documents/TasksProject”目录的另一个目录下，你需要输入正确的项目目录的路径。为了快速地完成，从Finder中点击并拖拽项目目录到终端中。你项目的路径，将魔术般地出现在终端的窗口上！现在简单地将你的光标移动到路径的前边，输入
        <code>
            cd
        </code>
        ，后跟一个空格，并点击enter。
    </p>
    <p>
        为了确保你位于正确的地方，输入下列的命令到终端上：
    </p>
    <pre class="command" style="font-family:monospace;">ls</pre>
    <p>
        在生成的文件列表中，检查
        <code>
            BuildScript.command
        </code>
        。如果你并非位于正确的位置，检查你是否在终端中输入了正确的项目目录。
    </p>
    <p>
        当确保你在正确的目录下之后，输入下列的命令到终端中：
    </p>
    <pre class="command" style="font-family:monospace;">chmod +x BuildScript.command</pre>
    <p>
        <code>
            chmod
        </code>
        命令会改变脚本的权限，使它可以被你的
        <code>
            NSTask
        </code>
        对象执行。如果你尝试，在没有这些恰当权限的条件下，运行你的应用，你将看到“Launch path not accessible”的错误，就像之前一样。你只需要为每个你新添加到项目中的脚本执行一次该操作。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            如果你是为自己开发，或在Mac App Store（MAS）外运送你的app，像这样地使用脚本是很简单的。然而在为MAS开发时，应用到你的app的沙盒规则将由你的脚本继承，你需要使用更复杂的技术来使用命令行程序。这些技术超出了本教程的范围。关于更多的详情，请参考末尾的链接。
        </p>
    </div>
    <p>
        清理并运行你的项目；清理的操作是必须的，因为Xcode不能获得文件权限的变化，因此也就不能将它拷贝到build仓库中。当应用打开时，输入你的测试app的target的名称，确保“Project Location”和“Build Repository”的值被正确地设置，最后点击
        <em>
            Build
        </em>
        。
    </p>
    <p>
        当spinner消失的时候，你应当在期望的位置上得到了一个新的
        <code>
            .ipa
        </code>
        文件。成功！
    </p>
    <h2>
        使用输出
    </h2>
    <p>
        OK，你已经相当地熟练向命令行程序传递参数了，但对于处理命令行程序的输出呢？
    </p>
    <p>
        为了实际地查看这个，输入下列命令到终端中，并点击Enter：
    </p>
    <pre class="command" style="font-family:monospace;">date</pre>
    <p>
        你应当看到生成的信息，就像这样：
    </p>
    <pre class="command" style="font-family:monospace;">Fri 19 Feb 2016 17:48:15 GMT</pre>
    <p>
        <code>
            date
        </code>
        告诉你当前的日期和时间。尽管不是很明显，它的结果是被发送到了一个名叫
        <em>
            standard output
        </em>
        的频道中。
    </p>
    <p>
        进程通常有三个用来输入和输出的频道：
    </p>
    <ul>
        <li>
            <em>
                standard input
            </em>
            ，从调用者这里接受输入；
        </li>
        <li>
            <em>
                standard output
            </em>
            ，从进程中将输出发回到调用者这里；
        </li>
        <li>
            <em>
                standard error
            </em>
            ，从进程中将错误发回到调用者这里；
        </li>
    </ul>
    <p>
        专业提示：你会看到这些通常被简写为
        <em>
            stdin
        </em>
        ，
        <em>
            stdout
        </em>
        ，和
        <em>
            stderr
        </em>
        。
    </p>
    <p>
        还有一个
        <code>
            pipe
        </code>
        ，可以让你重定向输出到另一个进程的输入上。你将创建一个pipe来让你的应用看到
        <code>
            NSTask
        </code>
        运行时，进程的标准输出。
    </p>
    <p>
        为了看到pipe在运转，确保你的电脑已打开了音量，然后在终端中输入下列命令：
    </p>
    <pre class="command" style="font-family:monospace;">date | say</pre>
    <p>
        点击enter，你会听到你的电脑告诉了你时间。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            你的键盘上的pipe字符“|”，通常位于
            <code>
                \
            </code>
            键这里，就在
            <code>
                enter/return
            </code>
            键的上面。
        </p>
    </div>
    <p>
        刚刚发生了：你创建了一个pipe，它将
        <code>
            date
        </code>
        的标准输出重定向到了
        <code>
            say
        </code>
        的标准输入中。你也可以向命令提供选项来和pipe交互，因此如果你想听到澳大利亚口音的日期，输入下面的命令来代替：
    </p>
    <pre class="command" style="font-family:monospace;">date | say -v karen</pre>
    <p>
        是的日期，宝贝！
    </p>
    <p>
        你可以使用pipe构建一些相当长的命令链，重定向一条命令的标准输出到另一条命令的标准输入中。一旦你适应了stdin，stdout，以及管道重定向，你就可以在命令行中，使用pipe这样的工具，做一些相当复杂的事情。
    </p>
    <p>
        到了在你的app中实现管道的时候了。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            <code>
                NSPipe
            </code>
            是一个
            <em>
                Foundation
            </em>
            中的类，它在Swift 3中被称为
            <code>
                Pipe
            </code>
            。大多数文档将引用
            <code>
                NSPipe
            </code>
            。
        </p>
    </div>
    <p>
        打开
        <em>
            TasksViewController.swift
        </em>
        并在
        <code>
            runScript(\_:)
        </code>
        中将评论
        <code>
            // TODO: Output Handling
        </code>
        替换为下面的代码：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #B833A1;">self</span>.<span style="color: #508187;">captureStandardOutputAndRouteToTextView</span><span style="color: black;">(</span><span style="color: #B833A1;">self</span>.<span style="color: #508187;">buildTask</span><span style="color: black;">)</span></pre>
    <p>
        现在，将这个方法添加到
        <em>
            TasksViewController.swift
        </em>
        中：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #B833A1;">func</span> captureStandardOutputAndRouteToTextView<span style="color: black;">(</span>_ task<span style="color: black;">:</span><span style="color: #6F41A7;">Process</span><span style="color: black;">)</span> <span style="color: black;">{</span>
&nbsp;
  <span style="color: #008312;">//1.</span>
  outputPipe = Pipe<span style="color: black;">(</span><span style="color: black;">)</span>
  task.<span style="color: #508187;">standardOutput</span> = outputPipe
&nbsp;
  <span style="color: #008312;">//2.</span>
  outputPipe.<span style="color: #508187;">fileHandleForReading</span>.<span style="color: #508187;">waitForDataInBackgroundAndNotify</span><span style="color: black;">(</span><span style="color: black;">)</span>
&nbsp;
  <span style="color: #008312;">//3.</span>
  NotificationCenter.<span style="color: #B833A1;">default</span>.<span style="color: #508187;">addObserver</span><span style="color: black;">(</span>forName<span style="color: black;">:</span> <span style="color: #6F41A7;">NSNotification</span>.<span style="color: #508187;">Name</span>.<span style="color: #508187;">NSFileHandleDataAvailable</span><span style="color: black;">,</span> object<span style="color: black;">:</span> outputPipe.<span style="color: #508187;">fileHandleForReading</span> <span style="color: black;">,</span> queue<span style="color: black;">:</span> <span style="color: #B833A1;">nil</span><span style="color: black;">)</span> <span style="color: black;">{</span>
    notification <span style="color: #B833A1;">in</span>
&nbsp;
    <span style="color: #008312;">//4.</span>
    <span style="color: #B833A1;">let</span> output = <span style="color: #B833A1;">self</span>.<span style="color: #508187;">outputPipe</span>.<span style="color: #508187;">fileHandleForReading</span>.<span style="color: #508187;">availableData</span>
    <span style="color: #B833A1;">let</span> outputString = <span style="color: #6F41A7;">String</span><span style="color: black;">(</span>data<span style="color: black;">:</span> output<span style="color: black;">,</span> encoding<span style="color: black;">:</span> <span style="color: #6F41A7;">String</span>.<span style="color: #508187;">Encoding</span>.<span style="color: #508187;">utf8</span><span style="color: black;">)</span> <span style="color: black;">??</span> <span style="color: #C41A16;">""</span>
&nbsp;
    <span style="color: #008312;">//5.</span>
    DispatchQueue.<span style="color: #508187;">main</span>.<span style="color: #508187;">async</span><span style="color: black;">(</span>execute<span style="color: black;">:</span> <span style="color: black;">{</span>
      <span style="color: #B833A1;">let</span> previousOutput = <span style="color: #B833A1;">self</span>.<span style="color: #508187;">outputText</span>.<span style="color: #508187;">string</span> <span style="color: black;">??</span> <span style="color: #C41A16;">""</span>
      <span style="color: #B833A1;">let</span> nextOutput = previousOutput <span style="color: black;">+</span> <span style="color: #C41A16;">"<span style="color: #C41A16;">\n</span>"</span> <span style="color: black;">+</span> outputString
      <span style="color: #B833A1;">self</span>.<span style="color: #508187;">outputText</span>.<span style="color: #508187;">string</span> = nextOutput
&nbsp;
      <span style="color: #B833A1;">let</span> range = NSRange<span style="color: black;">(</span>location<span style="color: black;">:</span>nextOutput.<span style="color: #508187;">characters</span>.<span style="color: #508187;">count</span><span style="color: black;">,</span>length<span style="color: black;">:</span><span style="color: #1C00CF;">0</span><span style="color: black;">)</span>
      <span style="color: #B833A1;">self</span>.<span style="color: #508187;">outputText</span>.<span style="color: #508187;">scrollRangeToVisible</span><span style="color: black;">(</span>range<span style="color: black;">)</span>
&nbsp;
    <span style="color: black;">}</span><span style="color: black;">)</span>
&nbsp;
    <span style="color: #008312;">//6.</span>
    <span style="color: #B833A1;">self</span>.<span style="color: #508187;">outputPipe</span>.<span style="color: #508187;">fileHandleForReading</span>.<span style="color: #508187;">waitForDataInBackgroundAndNotify</span><span style="color: black;">(</span><span style="color: black;">)</span>
  <span style="color: black;">}</span>
&nbsp;
<span style="color: black;">}</span></pre>
    <p>
        这个函数从外部的进程中采集了输出，并将它添加到了GUI的
        <code>
            outputText
        </code>
        框中。它就像下面这样地工作：
    </p>
    <ol>
        <li>
            创建了一个
            <code>
                Pipe
            </code>
            并将它连接到
            <code>
                buildTask
            </code>
            的标准输出上。
            <code>
                Pipe
            </code>
            代表了你在
            <code>
                终端
            </code>
            中创建的pipe的等效的类。任何写入到
            <code>
                buildTask
            </code>
            的
            <code>
                stdout
            </code>
            的内容，将被提供到
            <code>
                Pipe
            </code>
            对象上。
        </li>
        <li>
            <code>
                Pipe
            </code>
            有两个property：
            <code>
                fileHandleForReading
            </code>
            和
            <code>
                fileHandleForWriting
            </code>
            ，它们都是
            <code>
                NSFileHandle
            </code>
            对象。
            <code>
                NSFileHandle
            </code>
            的相关知识已经超出了这个教程的范围，但
            <code>
                fileHandleForReading
            </code>
            是用来在pipe中读取数据的。你可以调用它的
            <code>
                waitForDataInBackgroundAndNotify
            </code>
            方法，来使用一个单独的后台线程来获取有用的数据。
        </li>
        <li>
            任何当数据可用的时候，
            <code>
                waitForDataInBackgroundAndNotify
            </code>
            就会通过调用你注册在
            <code>
                NSNotificationCenter
            </code>
            中的代码块，来通知你处理
            <code>
                NSFileHandleDataAvailableNotification
            </code>
            。
        </li>
        <li>
            在你的通知处理中，获取
            <code>
                NSData
            </code>
            对象形式的数据，并将它转变为一个字符串。
        </li>
        <li>
            在主线程中，添加从上一步获取的字符串到
            <code>
                outputText
            </code>
            文本的末尾，并将文本区域滚动到 用户可以看到刚刚给出的输出的地方。这个
            <i>
                must
                必须
            </i>
            在主线程执行，就想所有的UI和用户交互一样。
        </li>
        <li>
            最后，再次调用在后台等待数据的方法。这就创造了一个循环，它将持续等待有用的数据，处理数据，再次等待有用的数据，等等。
        </li>
    </ol>
    <p>
        再次运行你的应用；确保
        <code>
            Project Location
        </code>
        和
        <code>
            Build Repository
        </code>
        是正确的，输入你的target的名称，并单击
        <em>
            Build
        </em>
        。
    </p>
    <p>
        你应当在
        <code>
            outputText
        </code>
        中看到来自build进程的输出：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/final-window-490x500.png"
        alt="final window view" width="490" height="500" class="aligncenter size-large wp-image-145429"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/final-window-490x500.png 490w, https://koenig-media.raywenderlich.com/uploads/2016/04/final-window-314x320.png 314w, https://koenig-media.raywenderlich.com/uploads/2016/04/final-window-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/04/final-window-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2016/04/final-window-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/04/final-window.png 513w"
        sizes="(max-width: 490px) 100vw, 490px">
    </p>
    <h2>
        停止NSTask
    </h2>
    <p>
        如果你开始了一个build，然后改变主意了，会发生什么？如果它花费了太长的时间，或一些其它的事看起来出错了，或只是在这儿挂起了，导致无法继续？这些都是你想要停下你的后台task的时刻。幸运的是，这些都很容易办到。
    </p>
    <p>
        在
        <em>
            TasksViewController.swift
        </em>
        中，添加下列的代码到
        <code>
            stopTask(\_:)
        </code>
        中
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #B833A1;">if</span> isRunning <span style="color: black;">{</span>
  buildTask.<span style="color: #508187;">terminate</span><span style="color: black;">(</span><span style="color: black;">)</span>
<span style="color: black;">}</span></pre>
    <p>
        上面的代码检查了是否
        <code>
            NSTask
        </code>
        正在运行，如果是的话，调用
        <code>
            terminate
        </code>
        方法。这将停止
        <code>
            NSTask
        </code>
        在它的执行中。
    </p>
    <p>
        运行你的app，确保全部的field配置正确，并单击
        <em>
            Build
        </em>
        按钮。然后在build完成前单击
        <em>
            Stop
        </em>
        按钮。你将看到每个事都停下了，且在你的输出目录下，没有创建新的
        <code>
            .ipa
        </code>
        文件。
    </p>
    <h2>
        从这儿去向哪里？
    </h2>
    <div class="inline-video-ad" id="sub-banner-inline">
        <div class="inline-video-ad-wrapper">
            <a href="https://videos.raywenderlich.com/courses" sl-processed="1">
                <div class="col-wrapper">
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
        这里是从上面的教程中完成的
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/TasksProject-completed_s3.zip"
        sl-processed="1">
            NSTask示例项目
        </a>
        。
    </p>
    <p>
        恭喜，你已经开始变成
        <code>
            NSTask
        </code>
        “忍者”（ninja）了！
    </p>
    <p>
        在一篇简短的教程中，你学到了：
    </p>
    <ul>
        <li>
            怎样创建带有参数和输出pipe的
            <code>
                NSTasks
            </code>
            ；以及
        </li>
        <li>
            怎样创建一个shell脚本，并从你的app中调用它！
        </li>
    </ul>
    <p>
        要了解关于
        <code>
            NSTask
        </code>
        的更多信息，请访问苹果的官方文档
        <a href="https://developer.apple.com/library/mac/#documentation/cocoa/Reference/Foundation/Classes/NSTask_Class/Reference/Reference.html"
        sl-processed="1">
            NSTask类参考文档
        </a>
        。
    </p>
    <p>
        为了了解在沙盒app中，使用命令行程序的相关内容，请参考
        <a href="https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/Introduction.html#//apple_ref/doc/uid/10000172i"
        sl-processed="1">
            守护进程和服务的编程向导
        </a>
        和
        <a href="https://developer.apple.com/library/mac/documentation/System/Reference/XPCServicesFW/index.html#//apple_ref/doc/uid/TP40010357"
        sl-processed="1">
            XPC服务API参考文档
        </a>
        。
    </p>
    <p>
        这个教程仅处理了NSTask的stdout，但你也可以同样地使用
        <a href="http://en.wikipedia.org/wiki/Standard_streams" sl-processed="1">
            stdin和stderr
        </a>
        ！为了实践你的新技能，尝试使用它们。
    </p>
    <p>
        我希望你可以喜欢这个
        <code>
            NSTask
        </code>
        教程，你会发现它在你将来的Mac OS X app中是非常有用的。如果你有任何的问题或评论，请参与我们下面的讨论！
    </p>
</div>
