# macOS FileManager类教程：文件系统入门

#### [原文地址](https://www.raywenderlich.com/157986/filemanager-class-tutorial-macos-getting-started-file-system) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div id="attachment_124497" style="width: 260px" class="wp-caption alignright">
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/InteractingFileSystem-feature.png"
        alt="File Manager Case Tutorial for macOS: Getting Started with the File System"
        width="250" height="250" class="size-thumbnail wp-image-124497">
        <p class="wp-caption-text">
            macOS文件系统
        </p>
    </div>
    <p>
        在
        <em>
            macOS
        </em>
        中文件系统是每个app的基础 - 在
        <code>
            FileManager
        </code>
        类有很多来处理这个。你会在
        <em>
            Applications
        </em>
        目录下储存app，在
        <em>
            Documents
        </em>
        目录下储存文档，在
        <em>
            Library
        </em>
        目录下储存偏好和支持文件。
    </p>
    <p>
        随着文件和数据在文件系统中传播，你的app该如何查找文件和目录，使用文件和目录的路径，甚至读取及写入数据到一个文件中？
    </p>
    <p>
        那就要靠
        <code>
            FileManager
        </code>
        类了！
    </p>
    <p>
        在这个教程中，你会学到如何管理目录路径，使用URL，使用通用的文件和目录对话框，展示文件和目录信息等等！
    </p>
    <h2>
        入门
    </h2>
    <p>
        在本教程中，你会从playground开始，然后在掌握基础之后，移步到app中。
    </p>
    <p>
        <em>
            macOS
        </em>
        使用了一个分层的文件系统：目录中的文件和目录，目录内部。这意味着找到一个指定的文件是非常复杂的。每个文件都有它自己的地址，定义地址的结构被称为
        <code>
            URL
        </code>
        。
    </p>
    <p>
        打开
        <em>
            Xcode
        </em>
        并在
        <em>
            Welcome to Xcode
        </em>
        窗口中单击
        <em>
            Get started with a playground
        </em>
        ，或依次选择
        <em>
            File/New/Playground…
        </em>
        将playground的名称设为
        <em>
            Files
        </em>
        ，确保平台被设置为
        <em>
            macOS
        </em>
        并单击
        <em>
            Next
        </em>
        。
    </p>
    <p>
        选择你的
        <em>
            Desktop
        </em>
        并单击
        <em>
            Create
        </em>
        来保存playground。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/NewPlayground.png"
        alt="New Playground" width="600" height="432" class="aligncenter size-full wp-image-157988"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/NewPlayground.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/04/NewPlayground-444x320.png 444w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        在这个教程中，playground的名称必须为
        <em>
            Files
        </em>
        ，并且它必须位于你的
        <em>
            Desktop
        </em>
        目录下。如果你给它起了一个其它的名字，或把它保存到了其它地方，请在开始后续教程开始前纠正，否则下面的代码就会无法正常工作！
    </div>
    <p>
        打开开始的playground后，删除除
        <code>
            import Cocoa
        </code>
        外全部行的代码。
    </p>
    <p>
        添加下面的代码到你的playground中，但不要担心现在改变了用户名：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-keyword"><font><font>let</font></font></span><font><font> completePath = </font></font><span class="hljs-string"><font><font>“/Users/sarah/Desktop/Files.playground”</font></font></span>
</pre>
    <p>
        <code>
            completePath
        </code>
        现在包含了这个playground文件的地址或路径。由于
        now contains the address, or path, of this playground file. Since
        <em>
            macOS
        </em>
        是基于Unix系统的，而
        this is how
        <em>
            Unix
        </em>
        （以及它的所有变体）就是这么描述文件路径的。第一条斜杠表示根目录，在这个case中是你的启动磁盘。之后，每个斜杠都界定除了一个新的目录或文件。因此，
        (and all its variants) describe file paths. 
        The first slash indicates the root directory, 
        which in this case is your startup disk. 
        After that, every slash delimits a new folder or file.
        So
        <em>
            Files.playground
        </em>
        文件就位于启动驱动器的
        <em>
            Users
        </em>
        目录下的
        <em>
            sarah
        </em>
        目录下的
        <em>
            Desktop
        </em>
        目录中。
    </p>
    <p>
        尽管这个字符串描述了这个文件的全路径，但它并不是处理地址的最佳方式。相代替的，你会通过添加下列代码，将地址替换为一个
        <code>
            URL
        </code>
        ：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-keyword">let</span> completeUrl = URL(fileURLWithPath: completePath)
</pre>
    <p>
        现在，在playground的结果面板中，你会看到：
        <code>
            file:///Users/sarah/Desktop/Files.playground
        </code>
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/CreateURL.png"
        alt="Create a URL" width="700" height="103" class="aligncenter size-full wp-image-157989"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/CreateURL.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/CreateURL-480x71.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/04/CreateURL-650x96.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        “稍等！”你喊道。“我以为
        <code>
            URL
        </code>
        是一个像
        <code>
            https://www.raywenderlich.com
        </code>
        这样的网址，而不是目录的路径！”
    </p>
    <p>
        嗯，是的是的！
    </p>
    <p>
        <code>
            URL
        </code>
        代表了
        <em>
            Uniform Resource Locator
        </em>
        - 它也可以指向本地的文件和目录。并非
        <code>
            https://
        </code>
        ，而是以
        <code>
            file://
        </code>
        开头来表示本地文件。在结果面板中，它看起来有3个斜杠，但这是因为这个路径本身就是以斜杠开头的。
    </p>
    <h3>
        FileManager类
    </h3>
    <p>
        你已经使用了一个
        <code>
            字符串
        </code>
        来指定一个文件路径，并将它转换为一个
        <code>
            URL
        </code>
        。但是，虽然它是一个有效的
        <code>
            URL
        </code>
        ，但却无法工作 - 除非你的用户名也恰好就是
        <em>
            sarah
        </em>
        。因此，下面的一步就是来创建一个可以在任何人的电脑上work的
        <code>
            URL
        </code>
        了。
    </p>
    <p>
        要做到这个，你就要使用
        <code>
            FileManager
        </code>
        类，它提供了在macOS中大多数的处理文件相关行为的方法。
    </p>
    <p>
        第一个任务就是识别你的
        <em>
            Home
        </em>
        目录，并使用你自己的用户名来替换
        <em>
            sarah
        </em>
        。
    </p>
    <p>
        添加下列的代码到你的playground中：
    </p>
    <pre lang="swift" class="hljs cs"><span class="hljs-keyword">let</span> home = FileManager.<span class="hljs-keyword">default</span>.homeDirectoryForCurrentUser
</pre>
    <p>
        <code>
            default
        </code>
        返回了
        <code>
            FileManager
        </code>
        类的单例实例，而
        <code>
            homeDirectoryForCurrentUser
        </code>
        包含了当前用户的home目录的
        <code>
            URL
        </code>
        。
    </p>
    <p>
        现在你已经有了指向你的home目录的
        <code>
            URL
        </code>
        ，你就可以通过添加下列的代码来获取指向playground的路径：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-keyword">let</span> playgroundPath = <span class="hljs-string">"Desktop/Files.playground"</span>
<span class="hljs-keyword">let</span> playgroundUrl = home.appendingPathComponent(playgroundPath)
</pre>
    <p>
        现在结果面板就会展示在你的家目录下的
        <code>
            URL
        </code>
        了。
    </p>
    <p>
        添加下列的代码到playground中，来查询各种
        <code>
            URL
        </code>
        的property：
    </p>
    <pre lang="swift" class="hljs">playgroundUrl.path
playgroundUrl.absoluteString
playgroundUrl.absoluteURL
playgroundUrl.baseURL
playgroundUrl.pathComponents
playgroundUrl.lastPathComponent
playgroundUrl.pathExtension
playgroundUrl.isFileURL
playgroundUrl.hasDirectoryPath
</pre>
    <p>
        <code>
            pathComponents
        </code>
        这个property非常有趣，它会将所有的目录和文件拆成一个数组。而
        <code>
            lastPathComponent
        </code>
        和
        <code>
            pathExtension
        </code>
        property在实践中都相当地有用。
    </p>
    <p>
        下面是你应该在你的playground中有的：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/URLcomponents3.png"
        alt="URL Components" width="700" height="165" class="aligncenter size-full wp-image-158588">
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            property
            <code>
                hasDirectoryPath
            </code>
            的值被设为了
            <coee>
                true
            </coee>
            。这标记了
            <code>
                URL
            </code>
            是一个目录。但为何playground文件是被标记为一个目录？
        </p>
        <p>
            这是因为
            <em>
                .playground
            </em>
            文件是“目录bundle”，就像
            <em>
                .app
            </em>
            文件一样。右击playground文件，并选择
            <em>
                Show Package Contents
            </em>
            就可以查看它的内部了。
        </p>
    </div>
    <p>
        <code>
            URL
        </code>
        类使得编辑
        <code>
            URLs
        </code>
        非常得容易。
    </p>
    <p>
        添加下列的代码到你的playground中：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-keyword">var</span> urlForEditing = home
urlForEditing.path

urlForEditing.appendPathComponent(<span class="hljs-string">"Desktop"</span>)
urlForEditing.path

urlForEditing.appendPathComponent(<span class="hljs-string">"Test file"</span>)
urlForEditing.path

urlForEditing.appendPathExtension(<span class="hljs-string">"txt"</span>)
urlForEditing.path

urlForEditing.deletePathExtension()
urlForEditing.path

urlForEditing.deleteLastPathComponent()
urlForEditing.path
</pre>
    <p>
        注意，每次你都会展示
        <code>
            path
        </code>
        property，因此很容易就会看到改变了什么。
    </p>
    <p>
        尽管这些命令恰当地编辑
        <code>
            URL
        </code>
        ，你也可以从已存在的创建一个新的
        <code>
            URL
        </code>
        。
    </p>
    <p>
        为了了解如何操作，添加下列的命令到你的playground：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-keyword">let</span> fileUrl = home
    .appendingPathComponent(<span class="hljs-string">"Desktop"</span>)
    .appendingPathComponent(<span class="hljs-string">"Test file"</span>)
    .appendingPathExtension(<span class="hljs-string">"txt"</span>)
fileUrl.path

<span class="hljs-keyword">let</span> desktopUrl = fileUrl.deletingLastPathComponent()
desktopUrl.path
</pre>
    <p>
        这些方法会返回新的
        <code>
            URLs
        </code>
        ，因此将它们连接到一个序列中效果会更好。
    </p>
    <p>
        这三个
        <code>
            appending
        </code>
        方法实际上可以缩到一个方法中，但我在这里将它们拆分成了独立的步骤，以便清晰地展示给你。
    </p>
    <p>
        你的playground现在应当看起来像下面的样子：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/AppendURL.png"
        alt="Append Path to a URL" width="700" height="94" class="aligncenter size-full wp-image-157992"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/AppendURL.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/AppendURL-480x64.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/04/AppendURL-650x87.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        <em>
            查看文件和目录
        </em>
    </p>
    <p>
        <code>
            NSString
        </code>
        中有很多处理文件路径的方法，但在Swift的结构体
        <code>
            String
        </code>
        中则不是。相反地，随着苹果向着
        <em>
            Apple File System (APFS)
        </em>
        的转变，你应当使用
        <code>
            URLs
        </code>
        来处理文件路径。在这种方式下处理将会变得更重要，因为。
    </p>
    <p>
        然而，在下面这个情形下，你仍然需要一个字符串来代表文件
        <code>
            URL
        </code>
        ：检查是否这个文件或目录存在。获取一个
        <code>
            URL
        </code>
        的字符串版本的最近方式是通过
        <code>
            path
        </code>
        property。
    </p>
    <p>
        添加下列的代码到你的playground中：
    </p>
    <pre lang="swift" class="hljs cs"><span class="hljs-keyword">let</span> fileManager = FileManager.<span class="hljs-keyword">default</span>
fileManager.fileExists(atPath: playgroundUrl.path)

<span class="hljs-keyword">let</span> missingFile = URL(fileURLWithPath: <span class="hljs-string">"this_file_does_not_exist.missing"</span>)
fileManager.fileExists(atPath: missingFile.path)
</pre>
    <p>
        检查一个目录是否存在稍微有一点难懂，因为你必须这个
        <code>
            URL
        </code>
        既是一个有效的资源，又是一个目录。
    </p>
    <p>
        这就要求我使用一个非常非Swift的机制 - OC版本的inout的Bool值。添加下列的代码：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-keyword">var</span> isDirectory: ObjCBool = <span class="hljs-literal">false</span>
fileManager.fileExists(atPath: playgroundUrl.path, <span class="hljs-attr">isDirectory</span>: &amp;isDirectory)
isDirectory.boolValue
</pre>
    <p>
        现在，你的playground看起来应当是下面的样子：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/CheckForExistence3.png"
        alt="FileManager Class Check For File Exists" width="700" height="123"
        class="aligncenter size-full wp-image-158554" srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/CheckForExistence3.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/CheckForExistence3-480x84.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/04/CheckForExistence3-650x114.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        一个充满注释版本的
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/04/Files.playground-1.zip"
        sl-processed="1">
            playground
        </a>
        可以到这里下载。
    </p>
    <p>
        既然你已理解了如何使用
        <code>
            URL
        </code>
        来区别文件和目录，关闭playground。是时候来构建app了！
    </p>
    <h2>
        文件间谍
    </h2>
    <p>
        在教程的这一部分，你将要构建
        <em>
            文件间谍
        </em>
        app，你可以用它选择一个目录来查看其内部的每个文件和目录。选择其中任一项目，就可以看到更多的详情。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo.png"
        alt="FileManager Class File Information" width="700" height="498" class="aligncenter size-full wp-image-157994"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo-450x320.png 450w, https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo-650x462.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        下载
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/04/FileSpy-Starter.zip"
        sl-processed="1">
            起始的app项目
        </a>
        ，在
        <em>
            Xcode
        </em>
        中打开它并在toolbar单击
        <em>
            Play
        </em>
        按钮，或按
        <em>
            Command+R键
        </em>
        运行项目。它的UI已完成，但你需要添加文件管理位。
    </p>
    <p>
        你第一个任务就是让用户选择一个目录，然后展示它的内容。你会在
        <em>
            Select Folder
        </em>
        按钮上添加一些代码，并使用
        <code>
            NSOpenPanel
        </code>
        类来选择一个目录。
    </p>
    <p>
        在
        <em>
            ViewController.swift
        </em>
        中的
        <em>
            Actions
        </em>
        区，找到
        <code>
            selectFolderClicked
        </code>
        并插入下面的代码：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-comment">// 1</span>
<span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> window = view.window <span class="hljs-keyword">else</span> { <span class="hljs-keyword">return</span> }

<span class="hljs-comment">// 2</span>
<span class="hljs-keyword">let</span> panel = <span class="hljs-type">NSOpenPanel</span>()
panel.canChooseFiles = <span class="hljs-literal">false</span>
panel.canChooseDirectories = <span class="hljs-literal">true</span>
panel.allowsMultipleSelection = <span class="hljs-literal">false</span>

<span class="hljs-comment">// 3</span>
panel.beginSheetModal(<span class="hljs-keyword">for</span>: window) { (result) <span class="hljs-keyword">in</span>
  <span class="hljs-keyword">if</span> result == <span class="hljs-type">NSFileHandlingPanelOKButton</span> {
    <span class="hljs-comment">// 4</span>
    <span class="hljs-keyword">self</span>.selectedFolder = panel.urls[<span class="hljs-number">0</span>]
    <span class="hljs-built_in">print</span>(<span class="hljs-keyword">self</span>.selectedFolder)
  }
}
</pre>
    <p>
        上面的代码完成了：
    </p>
    <ol>
        <li>
            检查你可否获取window的引用，因为它是
            <code>
                NSOpenPanel
            </code>
            将要展示的地方。
        </li>
        <li>
            创建一个新的
            <code>
                NSOpenPanel
            </code>
            ，并设置一些property，使其值运行单选，且只能选择目录。
        </li>
        <li>
            模态地在window中展示
            <code>
                NSOpenPanel
            </code>
            并使用一个闭包来等待结果。
        </li>
        <li>
            如果result表明用户点击了
            <em>
                OK
            </em>
            按钮（实际看到的按钮上，将基于你的本地化带有不同的标签），获取被选择的
            <code>
                URL
            </code>
            并设置指定的
            <code>
                ViewController
            </code>
            property。为了临时快速地测试，你会把选择的
            <code>
                URL
            </code>
            输入到控制台。现在忽略这行代码上的警告。
        </li>
    </ol>
    <p>
        运行项目，单击
        <em>
            Select Folder
        </em>
        按钮并选择一个目录。确认选择的目录的
        <code>
            URL
        </code>
        已打印到控制台上。
    </p>
    <p>
        再次单击按钮来打开对话框，但这次单击
        <em>
            Cancel
        </em>
        按钮。这时就不会打印
        <code>
            URL
        </code>
        。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/FolderSelected.png"
        alt="Selecting a Folder" width="700" height="476" class="aligncenter size-full wp-image-157995"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/FolderSelected.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/FolderSelected-471x320.png 471w, https://koenig-media.raywenderlich.com/uploads/2017/04/FolderSelected-650x442.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        退出app并删除临时的
        <code>
            print
        </code>
        语句。
    </p>
    <h3>
        文件内容
    </h3>
    <p>
        既然你能够选择目录，那接下来你的工作就是找出这个目录的内容并展示出来。
    </p>
    <p>
        上一部分的代码填充了一个名为
        <code>
            selectedFolder
        </code>
        的property。滚动到
        <code>
            ViewController
        </code>
        定义的顶部，并查看
        <code>
            selectedFolder
        </code>
        的property。它使用了一个
        <code>
            didSet
        </code>
        的property观察者，它会在设置值的时候运行代码。
    </p>
    <p>
        这里的关键代码是调用
        <code>
            contentsOf(folder:)
        </code>
        。滚动到这个方法这里，它当前返回了一个空的数组。用下面的代码来替换其中的内容：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">contentsOf</span><span class="hljs-params">(folder: URL)</span></span> -&gt; [<span class="hljs-type">URL</span>] {
  <span class="hljs-comment">// 1</span>
  <span class="hljs-keyword">let</span> fileManager = <span class="hljs-type">FileManager</span>.<span class="hljs-keyword">default</span>

  <span class="hljs-comment">// 2</span>
  <span class="hljs-keyword">do</span> {
    <span class="hljs-comment">// 3</span>
    <span class="hljs-keyword">let</span> contents = <span class="hljs-keyword">try</span> fileManager.contentsOfDirectory(atPath: folder.path)

    <span class="hljs-comment">// 4</span>
    <span class="hljs-keyword">let</span> urls = contents.<span class="hljs-built_in">map</span> { <span class="hljs-keyword">return</span> folder.appendingPathComponent($<span class="hljs-number">0</span>) }
    <span class="hljs-keyword">return</span> urls
  } <span class="hljs-keyword">catch</span> {
    <span class="hljs-comment">// 5</span>
    <span class="hljs-keyword">return</span> []
  }
}
</pre>
    <p>
        一步步来看代码：
    </p>
    <ol>
        <li>
            和之前一样，获取
            <code>
                FileManager
            </code>
            类的单例。
        </li>
        <li>
            由于
            <code>
                FileManager
            </code>
            的方法可能抛出错误，因此你要使用
            <code>
                do...catch
            </code>
            代码块。
        </li>
        <li>
            尝试找到目录
            <code>
                contentsOfDirectory(atPath:)
            </code>
            的内容，并返回内部文件和目录名称的数组。
        </li>
        <li>
            使用
            <code>
                map
            </code>
            处理返回的数组，并将每个名称，用其父目录转换成一个完整的
            <code>
                URL
            </code>
            然后返回数组。
        </li>
        <li>
            如果
            <code>
                contentsOfDirectory(atPath:)
            </code>
            抛出错误的话，返回一个空的数组。
        </li>
    </ol>
    <p>
        <code>
            selectedFolder
        </code>
        property将
        <code>
            filesList
        </code>
        property设置为被选择的目录的内容，但由于你使用了一个table view来展示内容，你就需要定义如何展示每个项目。
    </p>
    <p>
        向下拖动到
        <code>
            NSTableViewDataSource
        </code>
        的extension。注意
        <code>
            numberOfRows
        </code>
        早已返回了
        <code>
            filesList
        </code>
        数组中
        <code>
            URLs
        </code>
        的数量。现在滚动到        
        <code>
            NSTableViewDelegate
        </code>
        ，并注意到
        <code>
            tableView(\_:viewFor:row:)
        </code>
        返回的是
        <code>
            nil
        </code>
        。你需要在table中出现任何事之前改变这点。
    </p>
    <p>
        使用下面的代码来替换这个方法：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">tableView</span><span class="hljs-params">(<span class="hljs-number">_</span> tableView: NSTableView, viewFor
  tableColumn: NSTableColumn?, row: Int)</span></span> -&gt; <span class="hljs-type">NSView</span>? {
  <span class="hljs-comment">// 1</span>
  <span class="hljs-keyword">let</span> item = filesList[row]

  <span class="hljs-comment">// 2</span>
  <span class="hljs-keyword">let</span> fileIcon = <span class="hljs-type">NSWorkspace</span>.shared().icon(forFile: item.path)

  <span class="hljs-comment">// 3</span>
  <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> cell = tableView.make(withIdentifier: <span class="hljs-string">"FileCell"</span>, owner: <span class="hljs-literal">nil</span>) 
  	<span class="hljs-keyword">as</span>? <span class="hljs-type">NSTableCellView</span> {
    <span class="hljs-comment">// 4</span>
    cell.textField?.stringValue = item.lastPathComponent
    cell.imageView?.image = fileIcon
    <span class="hljs-keyword">return</span> cell
  }

  <span class="hljs-comment">// 5</span>
  <span class="hljs-keyword">return</span> <span class="hljs-literal">nil</span>
}
</pre>
    <p>
        你在代码中做的事有：
    </p>
    <ol>
        <li>
            获取匹配行序号的
            <code>
                URL
            </code>
            。
        </li>
        <li>
            获取这个
            <code>
                URL
            </code>
            的icon。
            <code>
                NSWorkspace
            </code>
            是另一个非常有用的单例；这个方法对任何
            <code>
                URL
            </code>
            都返回的是Finder的icon。
        </li>
        <li>
            获取这个table中对于这个cell的引用。
            <em>
                FileCell
            </em>
            这个标识符是在
            <em>
                Storyboard
            </em>
            中被设置的。
        </li>
        <li>
            如果cell存在，就设置它的text field来展示文件名，设置它的image view来展示文件的icon。
        </li>
        <li>
            如果没有cell存在，返回
            <code>
                nil
            </code>
            。
        </li>
    </ol>
    <p>
        运行项目，选择一个目录，你应当看到一个文件和目录的列表出现了 - 欢呼吧！
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/FolderContents.png"
        alt="Show Folder Contents" width="700" height="368" class="aligncenter size-full wp-image-157996"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/FolderContents.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/FolderContents-480x252.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/04/FolderContents-650x342.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        但点击一个文件或目录现在还没有给出有用的信息，因此继续下一步。
    </p>
    <h3>
        获取文件信息
    </h3>
    <p>
        打开Finder并按
        <em>
            Command+I键
        </em>
        来打开一个关于文件信息的窗口：创建日期，修改日期，尺寸，权限等等。全部的这些信息，甚至更多，你都可以通过
        <code>
            FileManager
        </code>
        类来获取。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/FinderFileInfo-1.png"
        alt="File Information" width="238" height="700" class="aligncenter size-full wp-image-158016"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/FinderFileInfo-1.png 238w, https://koenig-media.raywenderlich.com/uploads/2017/04/FinderFileInfo-1-109x320.png 109w, https://koenig-media.raywenderlich.com/uploads/2017/04/FinderFileInfo-1-170x500.png 170w"
        sizes="(max-width: 238px) 100vw, 238px">
    </p>
    <p>
        回到app，仍然在
        <em>
            ViewController.swift
        </em>
        中，查找
        <code>
            tableViewSelectionDidChange
        </code>
        。设置
        <code>
            ViewController
        </code>
        的property：
        <code>
            selectedItem
        </code>
        。
    </p>
    <p>
        滚动回到顶部，并找到
        <code>
            selectedItem
        </code>
        被定义的地方。和
        <code>
            selectedFolder
        </code>
        一样，
        <code>
            didSet
        </code>
        观察者正在观察这个property的变化。当这个property改变时，如果新的值不为
        <code>
            nil
        </code>
        ，观察者就会调用
        <code>
            infoAbout(url:)
        </code>
        。这里将是你检索的信息用来展示的地方。
    </p>
    <p>
        找到
        <code>
            infoAbout
        </code>
        ，当前它会返回一个无聊的静态字符串，用下面的代码来替换它：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">infoAbout</span><span class="hljs-params">(url: URL)</span></span> -&gt; <span class="hljs-type">String</span> {
  <span class="hljs-comment">// 1</span>
  <span class="hljs-keyword">let</span> fileManager = <span class="hljs-type">FileManager</span>.<span class="hljs-keyword">default</span>

  <span class="hljs-comment">// 2</span>
  <span class="hljs-keyword">do</span> {
    <span class="hljs-comment">// 3</span>
    <span class="hljs-keyword">let</span> attributes = <span class="hljs-keyword">try</span> fileManager.attributesOfItem(atPath: url.path)
    <span class="hljs-keyword">var</span> report: [<span class="hljs-type">String</span>] = [<span class="hljs-string">"<span class="hljs-subst">\(url.path)</span>"</span>, <span class="hljs-string">""</span>]

    <span class="hljs-comment">// 4</span>
    <span class="hljs-keyword">for</span> (key, value) <span class="hljs-keyword">in</span> attributes {
      <span class="hljs-comment">// ignore NSFileExtendedAttributes as it is a messy dictionary</span>
      <span class="hljs-keyword">if</span> key.rawValue == <span class="hljs-string">"NSFileExtendedAttributes"</span> { <span class="hljs-keyword">continue</span> }
      report.append(<span class="hljs-string">"<span class="hljs-subst">\(key.rawValue)</span>:\t <span class="hljs-subst">\(value)</span>"</span>)
    }
    <span class="hljs-comment">// 5</span>
    <span class="hljs-keyword">return</span> report.joined(separator: <span class="hljs-string">"\n"</span>)
  } <span class="hljs-keyword">catch</span> {
    <span class="hljs-comment">// 6</span>
    <span class="hljs-keyword">return</span> <span class="hljs-string">"No information available for <span class="hljs-subst">\(url.path)</span>"</span>
  }
}
</pre>
    <p>
        这里发生了一些不同的事，因此我们一次看一个：
    </p>
    <ol>
        <li>    
            按照惯例，获取一个
            <code>
                FileManager
            </code>
            单例的引用。
        </li>
        <li>
            使用
            <code>
                do...catch
            </code>
            来捕获任何的错误。
        </li>
        <li>
            使用
            <em>
                FileManager
            </em>
            类的
            <code>
                attributesOfItem(atPath:)
            </code>
            方法来获取文件的信息。如果成功的话，它就会返回一个
            <code>
                [FileAttributeKey: Any]
            </code>
            类型的字典，
            <code>
                FileAttributeKeys
            </code>
            是一个带有字符串
            <code>
                rawValue
            </code>
            的结构体的成员。
        </li>
        <li>
            将key的名称和value的值组装成一个tab分隔符字符创的数组。但会忽略掉
            <code>
                NSFileExtendedAttributes
            </code>
            键，因为它包含了一个复杂的但并不是确实有用的字段。
        </li>
        <li>
            将整个数组组装成一个单独的字符串，返回它。
        </li>
        <li>
            如果
            <code>
                try
            </code>
            语句抛出了错误，就返回一个默认的报告。
        </li>
    </ol>
    <p>
        Build并再次运行，就像之前一样选择一个目录，然后点击列表中的任一文件或目录：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/FolderInfo.png"
        alt="Folder Information" width="700" height="447" class="aligncenter size-full wp-image-157998"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/FolderInfo.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/FolderInfo-480x307.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/04/FolderInfo-650x415.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        你现在已经获得了很多关于这个文件或目录有用的信息。但还有更多你可以做的事！
    </p>
    <h3>
        更多特征
    </h3>
    <p>
        这个app正在变得更棒，但仍然缺少一些事情：
    </p>
    <ul>
        <li>
            点击
            <em>
                Show Invisible Files
            </em>
            不会改变任何事。
        </li>
        <li>
            双击一个目录应当进入它的内容。
        </li>
        <li>
            <em>
                Move Up
            </em>
            按钮需要向上移动目录的层次结构。
        </li>
        <li>
            <em>
                Save Info
            </em>
            应当可以把被选择文件的详情到一个文件中。
        </li>
    </ul>
    <p>
        接下来你就会出来这些事情。
    </p>
    <p>
        <em>
            处理不可见的文件
        </em>
    </p>
    <p>
        在Unix系统中，名称以一个句点开头文件和目录将会不可见。你会添加代码来处理这个情况。
    </p>
    <p>
        前往
        <code>
            contentsOf(folder:)
        </code>
        ，并用下列代码替换
        <code>
            map
        </code>
        这行：
    </p>
    <pre lang="swift" class="hljs bash"><span class="hljs-built_in">let</span> urls = contents
  .filter { <span class="hljs-built_in">return</span> showInvisibles ? <span class="hljs-literal">true</span> : <span class="hljs-variable">$0</span>.characters.first != <span class="hljs-string">"."</span> }
  .map { <span class="hljs-built_in">return</span> folder.appendingPathComponent(<span class="hljs-variable">$0</span>) }
</pre>
    <p>
        上面的代码添加了一个
        <code>
            filter
        </code>
        ，当
        <code>
            showInvisibles
        </code>
        的property不为        
        <code>
            true
        </code>
        时，就会拒绝隐藏的项目；否则
        <code>
            filter
        </code>
        会返回所有的项目，包括因此的。
    </p>
    <p>
        找到
        <code>
            ViewController
        </code>
        中的
        <code>
            toggleShowInvisibles
        </code>
        方法，并插入下列代码到函数中：
    </p>
    <pre lang="swift" class="hljs objectivec"><span class="hljs-comment">// 1</span>
showInvisibles = (sender.state == <span class="hljs-built_in">NSOnState</span>)

<span class="hljs-comment">// 2</span>
<span class="hljs-keyword">if</span> let selectedFolder = selectedFolder {
  filesList = contentsOf(folder: selectedFolder)
  selectedItem = <span class="hljs-literal">nil</span>
  tableView.reloadData()
}
</pre>
    <p>
        这些代码完成了：
    </p>
    <ol>
        <li>
            根据sender的状态设置
            <code>
                showInvisibles
            </code>
            property。由于sender是
            <code>
                NSButton
            </code>
            ，所以它的state不是
            <code>
                NSOnState
            </code>
            就是
            <code>
                NSOffState
            </code>
            。由于它是一个checkbox按钮，
            <code>
                NSOnState
            </code>
            就表示勾选。
        </li>
        <li>
            如果当前有
            <code>
                selectedFolder
            </code>
            ，就重新生成
            <code>
                filesList
            </code>
            并更新UI。
        </li>
    </ol>
    <p>
        运行项目，选择一个目录，并勾选及取消
        <em>
            Show Invisible Files
        </em>
        按钮。依赖于你正在观察的目录，你有可能会在当
        <em>
            Show Invisible Files
        </em>
        被勾选时，看到以一个圆点的文件。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/Invisibles.png"
        alt="Show Invisible Files" width="700" height="340" class="aligncenter size-full wp-image-157999"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/Invisibles.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/Invisibles-480x233.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/04/Invisibles-650x316.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        <em>
            处理双击目录的情况
        </em>
    </p>
    <p>
        在storyboard中，table view已被分配了一个叫做
        <code>
            tableViewDoubleClicked
        </code>
        的
        <code>
            双击动作
        </code>
        。找到
        <code>
            tableViewDoubleClicked
        </code>
        并用以下代码替换：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">tableViewDoubleClicked</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: Any)</span></span> {
  <span class="hljs-comment">// 1</span>
  <span class="hljs-keyword">if</span> tableView.selectedRow &lt; <span class="hljs-number">0</span> { <span class="hljs-keyword">return</span> }

  <span class="hljs-comment">// 2</span>
  <span class="hljs-keyword">let</span> selectedItem = filesList[tableView.selectedRow]
  <span class="hljs-comment">// 3</span>
  <span class="hljs-keyword">if</span> selectedItem.hasDirectoryPath {
    selectedFolder = selectedItem
  }
}
</pre>
    <p>
        一步一步地回顾上面的代码：
    </p>
    <ol>
        <li>
            检查双击是否发生在一个已填充的行上。如果点击在table的空白的部分，就会将
            <code>
                tableView的
            </code>
            selectedRow设置为-1。
        </li>
        <li>
            从
            <code>
                filesList
            </code>
            中获取匹配的
            <code>
                URL
            </code>
            。
        </li>
        <li>
            <code>
                URL
            </code>
            是一个目录，设置
            <code>
                ViewController的
            </code>
            <code>
                selectedFolder
            </code>
            property。就像当你使用Select Folder按钮来选择一个目录一样，设置这个property就会触发property的观察者来读取目录的内容，并更新UI。如果
            <code>
                URL
            </code>
            不是目录，则不执行任何事。
        </li>
    </ol>
    <p>
        运行项目，选择一个包含其它目录的目录，然后双击这个列表中的目录进入它。
    </p>
    <p>
        <em>
            处理Move Up按钮
        </em>
    </p>
    <p>
        一旦你实现了双击进入目录，接下来显然就应该是移回到“树”上了。
    </p>
    <p>
        找到空的
        <code>
            moveUpClicked
        </code>
        方法并用下列的代码来替换它：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">moveUpClicked</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: Any)</span></span> {
  <span class="hljs-keyword">if</span> selectedFolder?.path == <span class="hljs-string">"/"</span> { <span class="hljs-keyword">return</span> }
  selectedFolder = selectedFolder?.deletingLastPathComponent()
}
</pre>
    <p>
        首先，检查
        <code>
            selectedFolder
        </code>
        是否是根目录。如果是的话，你就不能做任何事，如果不是的话，就使用
        <code>
            URL
        </code>
        的方法来去掉URL的最后一部分。编辑
        <code>
            selectedFolder
        </code>
        就会像之前一样触发更新。
    </p>
    <p>
        Build并再次运行；确认你可以选择一个目录，双击并移动到一个子目录上，并点击
        <em>
            Move Up
        </em>
        来回到目录的层级中。只要你不在根目录上，你甚至可以在双击目录之前向上移动。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/MoveDownUp.gif"
        alt="Move Up The Folder Tree" width="694" height="397" class="aligncenter size-full wp-image-158000">
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        正如你看到的一样，property观察器（
        <code>
            didSet
        </code>
        ）非常得有用。用来更新界面的所有代码都在一个观察者中，因此无论是UI元素或方法来改变被观察的property，更新就发生了，无需做任何其它的事。Sweet！
    </div>
    <p>
        <em>
            保存信息
        </em>
    </p>
    <p>
        保存数据主要有两个办法：用户发起的保存以及自动保存。对于用户发起的保存，你的app应答让用户选择一个保存数据的位置，来将数据写入到这个位置中。对于自动保存，app自己会决定保存数据的位置。
    </p>
    <p>
        在这一部分，你会处理当用户点击
        <em>
            Save Info
        </em>
        按钮来发起保存的case。
    </p>
    <p>
        你已使用
        <code>
            NSOpenPanel
        </code>
        来提示用户选择一个目录。这次，你会使用
        <code>
            NSSavePanel
        </code>
        。
        <code>
            NSOpenPanel
        </code>
        和
        <code>
            NSSavePanel
        </code>
        都是
        <code>
            NSPanel
        </code>
        的子类，因此它们有很多共同的地方。
    </p>
    <p>
        使用下列代码来替换空方法
        <code>
            saveInfoClicked
        </code>
        ：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">saveInfoClicked</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: Any)</span></span> {
  <span class="hljs-comment">// 1</span>
  <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> window = view.window <span class="hljs-keyword">else</span> { <span class="hljs-keyword">return</span> }
  <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> selectedItem = selectedItem <span class="hljs-keyword">else</span> { <span class="hljs-keyword">return</span> }

  <span class="hljs-comment">// 2</span>
  <span class="hljs-keyword">let</span> panel = <span class="hljs-type">NSSavePanel</span>()
  <span class="hljs-comment">// 3</span>
  panel.directoryURL = <span class="hljs-type">FileManager</span>.<span class="hljs-keyword">default</span>.homeDirectoryForCurrentUser
  <span class="hljs-comment">// 4</span>
  panel.nameFieldStringValue = selectedItem
    .deletingPathExtension()
    .appendingPathExtension(<span class="hljs-string">"fs.txt"</span>)
    .lastPathComponent

  <span class="hljs-comment">// 5</span>
  panel.beginSheetModal(<span class="hljs-keyword">for</span>: window) { (result) <span class="hljs-keyword">in</span>
    <span class="hljs-keyword">if</span> result == <span class="hljs-type">NSFileHandlingPanelOKButton</span>,
      <span class="hljs-keyword">let</span> url = panel.url {
      <span class="hljs-comment">// 6</span>
      <span class="hljs-keyword">do</span> {
        <span class="hljs-keyword">let</span> infoAsText = <span class="hljs-keyword">self</span>.infoAbout(url: selectedItem)
        <span class="hljs-keyword">try</span> infoAsText.write(to: url, atomically: <span class="hljs-literal">true</span>, encoding: .utf8)
      } <span class="hljs-keyword">catch</span> {
        <span class="hljs-keyword">self</span>.showErrorDialogIn(window: window,
                               title: <span class="hljs-string">"Unable to save file"</span>,
                               message: error.localizedDescription)
      }
    }
  }
}
</pre>
    <p>
        依次来看每个被标号的注释：
    </p>
    <ol>
        <li>
            确认每样你需要的都存在：一个用来展示面板的窗口，已经你将要保存的
            <code>
                URL
            </code>
            。
        </li>
        <li>
            创建一个
            <code>
                NSSavePanel
            </code>
            。
        </li>
        <li>
            设置
            <code>
                directoryURL
            </code>
            property，它会指定展示在面板中的发起目录。
        </li>
        <li>
            设置
            <code>
                nameFieldStringValue
            </code>
            property，来为文件设置一个默认的名称。            
        </li>
        <li>
            展示面板，并在一个闭包中来等待用户完成。
        </li>
        <li>
            如果用户选择了一个有效的数据文件的路径（一个有效的
            <code>
                URL
            </code>
            ）并点击
            <em>
                OK
            </em>
            按钮，获取文件信息并将它写入到被选择的文件中。如果出现错误，就展示一个对话框。注意如果用户在保持的对话框中点击
            <em>
                Cancel
            </em>
            ，你只需忽略操作。
        </li>
    </ol>
    <p>
        <code>
            write(to:atomically:encoding)
        </code>
        是一个字符串的方法，它会将字符串写入到被提供的
        <code>
            URL
        </code>
        中。
        <code>
            atomically
        </code>
        选项意味着字符串将会写入到一个临时的文件中，并进行重命名，确保你不会在一个坏掉的文件上结束 - 即使系统在写入过程中崩溃了。在这个文件中，文本的编码方式被设置为
        <em>
            UTF8
        </em>
        ，这是一个通用的标准。
    </p>
    <p>
        运行项目，从列表中选择一个文件或目录，点击
        <em>
            Save Info
        </em>
        。选择一个待保存的位置，并点击
        <em>
            Save
        </em>
        。你会以一个文本文件结束，看起来就像下面这样：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/SavedFile.png"
        alt="File Info" width="650" height="370" class="aligncenter size-full wp-image-158001"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/SavedFile.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/04/SavedFile-480x273.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/04/SavedFile-266x151.png 266w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        使用
        <code>
            NSSavePanel
        </code>
        的一个很好的特性，就是如果你尝试覆盖一个早已存在的文件，你的app会自动展示一个确认对话框，询问你是否想要替换文件。
    </div>
    <p>
        这已经闭环了app的特性列表，但这里还有一个很好的特性可以添加：当app重新启动时，记录被选择的目录和项目，将最后被选择的目录再展示出来。
    </p>
    <h3>
        保存App的状态
    </h3>
    <p>
        通常，我会把app状态的数据保存到
        <code>
            UserDefaults
        </code>
        中，它会为你自动保存到
        <em>
            Preferences
        </em>
        目录中。但不允许你对文件系统做任何事。相反，你会保存这个数据到
        <em>
            Application Support
        </em>
        目录中的专用的app目录中。
    </p>
    <p>
        滚动到
        <em>
            ViewController.swift
        </em>
        的尾部，你会看到一个extension，专门用来保存和恢复用户的选择。
    </p>
    <p>
        我已经提供了用来进行实际的读写的方法。写入会使用和保存info file相同的
        <code>
            write(to:atomically:encoding)
        </code>
        方法。读取则使用一个
        <code>
            String
        </code>
        构造器，从
        <code>
            URL
        </code>
        创建一个
        <code>
            String
        </code>
        。
    </p>
    <p>
        一个非常有趣的事是如何决定去哪里保存数据。你会在
        <code>
            urlForDataStorage
        </code>
        来做这件事，它现在返回的是
        <code>
            nil
        </code>
        。
    </p>
    <p>
        使用下列的代码替换
        <code>
            urlForDataStorage
        </code>
        ：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-keyword">private</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">urlForDataStorage</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">URL</span>? {
  <span class="hljs-comment">// 1</span>
  <span class="hljs-keyword">let</span> fileManager = <span class="hljs-type">FileManager</span>.<span class="hljs-keyword">default</span>

  <span class="hljs-comment">// 2</span>
  <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> folder = fileManager.urls(<span class="hljs-keyword">for</span>: .applicationSupportDirectory,
                                      <span class="hljs-keyword">in</span>: .userDomainMask).first <span class="hljs-keyword">else</span> {
                                        <span class="hljs-keyword">return</span> <span class="hljs-literal">nil</span>
  }

  <span class="hljs-comment">// 3</span>
  <span class="hljs-keyword">let</span> appFolder = folder.appendingPathComponent(<span class="hljs-string">"FileSpy"</span>)
  <span class="hljs-keyword">var</span> isDirectory: <span class="hljs-type">ObjCBool</span> = <span class="hljs-literal">false</span>
  <span class="hljs-keyword">let</span> folderExists = fileManager.fileExists(atPath: appFolder.path, 
  			                    isDirectory: &amp;isDirectory)
  <span class="hljs-keyword">if</span> !folderExists || !isDirectory.boolValue {
    <span class="hljs-keyword">do</span> {
      <span class="hljs-comment">// 4</span>
      <span class="hljs-keyword">try</span> fileManager.createDirectory(at: appFolder,
                                      withIntermediateDirectories: <span class="hljs-literal">true</span>,
                                      attributes: <span class="hljs-literal">nil</span>)
    } <span class="hljs-keyword">catch</span> {
      <span class="hljs-keyword">return</span> <span class="hljs-literal">nil</span>
    }
  }

  <span class="hljs-comment">// 5</span>
  <span class="hljs-keyword">let</span> dataFileUrl = appFolder.appendingPathComponent(<span class="hljs-string">"StoredState.txt"</span>)
  <span class="hljs-keyword">return</span> dataFileUrl
}
</pre>
    <p>
        这些代码都做了些什么？
    </p>
    <ol>
        <li>
            又是你的老朋友
            <code>
                FileManager
            </code>
            。:]
        </li>
        <li>
            <code>
                FileManager
            </code>
            有一个方法，可以返回对于指定用途的恰当的
            <code>
                URL
            </code>
            的列表。在这个case中，你会在用户当前的目录下查找
            <code>
                applicationSupportDirectory
            </code>
            。这个基本上是不大可能返回超过一个的URL的，并且你只想获取第一个元素。你可以用不同的参数来调用这个方法，来找到更多不同的目录。
        </li>
        <li>
            就像你在playground中做的一样，添加一个路径成分来创建一个app指定目录的
            <code>
                URL
            </code>
            ，并检查它是否存在。
        </li>
        <li>
            如果这个目录不存在，尝试创建它，以及任何由路径决定的中间目录。如果创建失败的话，就返回
            <code>
                nil
            </code>
            。
        </li>
        <li>
            添加另一个路径成分，来创建数据文件的完整的
            <code>
                URL
            </code>
            ，并返回它。
        </li>
    </ol>
    <div class="note">
        <em>
            注意：
        </em>
        <code>
            .applicationSupportDirectory
        </code>
        是
        <code>
            FileManager.SearchPathDirectory.applicationSupportDirectory
        </code>
        的一个简写的方式。
        <code>
            .userDomainMask
        </code>
        则指向了
        <code>
            FileManager.SearchPathDomainMask.userDomainMask
        </code>
        。虽然简写的方式会更容易输入和阅读，但完整的方式会更有用于了解这些来自于哪里，因此如果需要的话，你可以在文档中找到他们。
    </div>
    <p>
        运行项目，选择一个目录，然后点击一个目录或文件。使用
        <em>
            Quit
        </em>
        菜单项或
        <em>
            Command-Q
        </em>
        来关闭app。不要通过
        <em>
            Xcode
        </em>
        来退出，否则生命循环的方法就不会触发保存的动作。再次运行app，可以注意到它自动打开了你上次退出时正在查看的文件或目录。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo.png"
        alt="Saved App State" width="700" height="498" class="aligncenter size-full wp-image-157994"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo-450x320.png 450w, https://koenig-media.raywenderlich.com/uploads/2017/04/FileInfo-650x462.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        如果你想查看存储状态的数据文件，就按住
        <em>
            Option
        </em>
        键，然后点击
        <em>
            Finder的Go
        </em>
        菜单并选择
        <em>
            Library
        </em>
        。在新的Finder窗口中，打开
        <em>
            Application Support
        </em>
        并查找
        <em>
            FileSpy
        </em>
        目录。你应该会看到带有你选择的目录和项目的
        <em>
            StoredState.txt
        </em>
        文件。
    </div>
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
        你可以在
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/04/FileSpy-Final.zip"
        sl-processed="1">
            这里
        </a>
        下载最后的示例项目。
    </p>
    <p>
        在
        <code>
            FileManager
        </code>
        类的教程中：
    </p>
    <ol>
        <li>
            你学到了
            <code>
                URL
            </code>
            如何表示本地的文件和目录，以及展示关于文件或目录的有用的属性。
        </li>
        <li>
            你学到了如何添加和删除一个
            <code>
                URL
            </code>
            中的
            <em>
                路径成分
            </em>
            。
        </li>
        <li>
            你探究了
            <code>
                FileManager
            </code>
            类，如property
            <code>
                homeDirectoryForCurrentUser
            </code>
            ，
            <code>
                applicationSupportDirectory
            </code>
            ，甚至
            <code>
                attributesOfItem
            </code>
            ，它包含了一个文件或目录的详细信息。
        </li>
        <li>
            你学到了如何保持一个文件的相关信息。
        </li>
        <li>
            你学到了如何查看一个文件或目录是否存在。
        </li>
    </ol>
    <p>
        有关更多的信息，请访问
        <a href="https://developer.apple.com/reference/foundation/filemanager"
        sl-processed="1">
            苹果FileManager API参考文档
        </a>
        ，你可以找到更多关于
        <code>
            FileManager
        </code>
        类中可用的方法。
    </p>
    <p>
        现在，你已经可以开始在你自己的app中应用关于文件和目录的知识了。
    </p>
</div>