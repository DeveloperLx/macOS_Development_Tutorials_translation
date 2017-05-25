# macOS上的Cocoa Bindings

#### [原文地址](https://www.raywenderlich.com/141297/cocoa-bindings-macos) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div class="note">
        <p>
            <em>
                更新笔记：
            </em>
            这个macOS的教程Cocoa Bindings，已由Andy Pereira更新到Xcode 8和 Swift 3的版本。
            <a href="https://www.raywenderlich.com/124490/cocoa-bindings-os-x-tutorial">
                原教程
            </a>
            撰写自Jake Gundersen。
        </p>
    </div>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-250x250.png"
        alt="Cocoa-Bindings-on-macOS" width="250" height="250" class="alignright size-thumbnail wp-image-129292"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
        Cocoa bindings，或简单的
        <em>
            bindings
        </em>
        ，使你从花费大量时间撰写
        <i>
            粘合代码
        </i>
        中解放出来；那就是，当使用Model-View-Controller(MVC)模式时，在controller中创建model和view之间的连接。
    </p>
    <p>
        Cocoa bindings有一个简单的目标：写更少的代码。你会发现，真的可以通过这么做来达到这个目的。
    </p>
    <p>
        在这个macOS教程Cocoa Bindings中，你将创建一个app，来展示从App Store中通过iTunes API获取的搜索结果，借此你会学到如何使用Cocoa bindings来完成如下的事：
    </p>
    <ul>
        <li>
            在Interface Builder设置一个数据模型的property和一个UI元素（例如label或button）之间的关系
        </li>
        <li>
            设置默认值
        </li>
        <li>
            应用格式化，例如货币或日期格式
        </li>
        <li>
            改变数据结构，例如当转化数值为代表的相应颜色时
        </li>
    </ul>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/cb-rageface1-e1445168631127.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/10/cb-rageface1-e1445168631127-435x320.png"
            alt="cb-rageface1" width="435" height="320" class="aligncenter size-medium wp-image-118691"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/10/cb-rageface1-e1445168631127-435x320.png 435w, https://koenig-media.raywenderlich.com/uploads/2015/10/cb-rageface1-e1445168631127.png 644w"
            sizes="(max-width: 435px) 100vw, 435px">
        </a>
    </p>
    <h2>
        入门
    </h2>
    <p>
        尽管你无须花费接下来的几个小时进行编码，这里仍然有相当的在
        <a href="http://www.raywenderlich.com/?s=Interface+Builder&amp;cof=FORID%3A10"
        target="_blank" title="Interface Builder">
            Interface Builder
        </a>
        中使用
        <a href="http://www.raywenderlich.com/?s=Auto+Layout&amp;cof=FORID%3A10"
        target="_blank" title="Auto Layout">
            Auto Layout
        </a>
        的工作，因此熟悉这些工具是首要的条件。
    </p>
    <p>        
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/09/AppResearchBindings-Starter.zip"
        title="here">
            在这里
        </a>
        下载初始项目。
    </p>
    <p>
        Build并运行项目，你将看到它有一个很棒的界面 - 但是没有数据。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.01.30-PM-700x463.png"
        alt="First run" width="700" height="463" class="aligncenter size-large wp-image-125398"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.01.30-PM-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.01.30-PM-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.01.30-PM-768x508.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.01.30-PM.png 1133w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        你也会看到有一些文件是对你有帮助的。
        <em>
            iTunesRequestManager.swift
        </em>
        包含一个带有两个静态方法的结构体。第一个方法为提供的搜索字符串向iTunes的API发送查询，并下载包含iOS App结果的JSON；而第二个方法则是用来异步下载图片的助手方法。
    </p>
    <p>
        第二个文件，
        <em>
            iTunesResults.swift
        </em>
        ，定义了一个可以匹配从iTunes搜索方法下载到的数据的数据模型类。
    </p>
    <div class="note">
        <p>
            <em>
                注意
            </em>
            ：所有在
            <code>
                Result
            </code>
            类中的变量都被定义为
            <em>
                dynamic
            </em>
            型。这是因为bindings是依赖于键值编码的，因此要求了Objective-C的运行时特性。添加
            <code>
                dynamic
            </code>
            关键字确保了访问那些属性总是通过使用Objective-C的运行时特性动态分配的。
        </p>
        <p>
            这个类是继承自
            <em>
                NSObject
            </em>
            的；这同样是由bindings要求的。你将在后面当添加一个变量到你的视图控制器类中时，了解到它的原因。
        </p>
    </div>
    <h2>
        通过iTunes搜索
    </h2>
    <p>
        首先，你将通过iTunes的API获取搜索的结果，并将它们添加到一个
        <code>
            NSArrayController
        </code>
        中。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        并查看
        <em>
            View Controller Scene
        </em>
        中的对象。注意到那些你将设置binding的对象，它们都包含标签
        <em>
            ‘(Bind)’
        </em>
        。
    </p>
    <h3>
        设置NSArrayController
    </h3>
    <p>
        <code>
            NSArrayController
        </code>
        对象管理
        <code>
            NSTableView
        </code>
        的内容。这个内容通常表现为一个模型对象数组的形式。
    </p>
    <div class="note">
        <p>
            <em>
                注意
            </em>
            ：
            <code>
                NSArrayController
            </code>
            提供的不仅仅是一个数组，还包括管理对象的选取、排序、和过滤。Cocoa Bindings会重度地使用这些功能。
        </p>
    </div>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        。并在
        <em>
            Object Library
        </em>
        中找到
        <code>
            NSArrayController
        </code>
        对象，并把它拖拽到document outline中的
        <em>
            View Controller Scene
        </em>
        组的对象列表的下面：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/02/add-array-controller-430x500.png"
        alt="add array controller" width="430" height="500" class="aligncenter size-large wp-image-126104"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/02/add-array-controller-430x500.png 430w, https://koenig-media.raywenderlich.com/uploads/2016/02/add-array-controller-275x320.png 275w, https://koenig-media.raywenderlich.com/uploads/2016/02/add-array-controller.png 692w"
        sizes="(max-width: 430px) 100vw, 430px">
    </p>
    <p>
        接下来，打开assistant editor，并确保你工作在文件
        <em>
            ViewController.swift
        </em>
        上。按住Control从
        <em>
            Storyboard
        </em>
        拖拽到
        <em>
            ViewController.swift
        </em>
        中的
        <em>
            Array Controller
        </em>
        对象上，并将其命名为
        <em>
            searchResultsController
        </em>
        ：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.39.36-PM-700x221.png"
        alt="add outlet" width="700" height="221" class="aligncenter size-large wp-image-125400"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.39.36-PM-700x221.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.39.36-PM-480x152.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.39.36-PM.png 721w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h3>
        添加搜索框和按钮
    </h3>
    <p>
        现在你已准备好了使用搜索框和按钮来获取一个搜索结果的列表，并添加它们到
        <code>
            searchResultsController
        </code>
        对象上。
    </p>
    <p>
        按住Control，将storyboard中的
        <em>
            search button
        </em>
        拖拽到
        <em>
            ViewController.swift
        </em>
        的源码中来创建一个动作方法。选择来创建一个
        <em>
            Action
        </em>
        的连接并命名为
        <em>
            searchClicked
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/09/addConnectionMethod.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/09/addConnectionMethod-650x195.png"
            alt="addConnectionMethod" width="650" height="195" class="aligncenter size-large wp-image-143260"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/09/addConnectionMethod-650x195.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/09/addConnectionMethod-480x144.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/09/addConnectionMethod.png 826w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        现在，添加下面的代码到
        <code>
            searchClicked(:_)
        </code>
        方法中：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-comment">//1</span>
<span class="hljs-keyword">if</span> (searchTextField.stringValue == <span class="hljs-string">""</span>) {
  <span class="hljs-keyword">return</span>
}
<span class="hljs-comment">//2</span>
<span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> resultsNumber = <span class="hljs-type">Int</span>(numberResultsComboBox.stringValue) <span class="hljs-keyword">else</span> { <span class="hljs-keyword">return</span> }
<span class="hljs-comment">//3</span>
iTunesRequestManager.getSearchResults(searchTextField.stringValue,
  results: resultsNumber, langString: <span class="hljs-string">"en_us"</span>) { 
      results, error <span class="hljs-keyword">in</span>
    <span class="hljs-comment">//4</span>
    <span class="hljs-keyword">let</span> itunesResults = results.<span class="hljs-built_in">map</span> { 
        <span class="hljs-keyword">return</span> <span class="hljs-type">Result</span>(dictionary: $<span class="hljs-number">0</span>) 
    } <span class="hljs-comment">//Deal with rank here later  </span>
    <span class="hljs-comment">//5</span>
    <span class="hljs-type">DispatchQueue</span>.main.async {
    <span class="hljs-comment">//6</span>
        <span class="hljs-keyword">self</span>.searchResultsController.content = itunesResults
        <span class="hljs-built_in">print</span>(<span class="hljs-keyword">self</span>.searchResultsController.content)
    }
}
</pre>
    <p>
        回顾一下每行代码：
    </p>
    <ol>
        <li>
            检查文本输入框；如果它是空的，就不会发送查询到iTunes的搜索API。
        </li>
        <li>
            获取下拉菜单中的值。这个数字被传递给API，并控制返回多少个结果。在下拉菜单中有一些预先配置的选项，但你也可以输入其它的数字 - 200是最大的值。
        </li>
        <li>
            调用
            <code>
                getSearchResults(_:results:langString:completionHandler:)
            </code>
            方法。它传递来自组合框的结果的数字，和你输入到文本输入框中的查询字符串。并通过完成的句柄，来返回一个
            <code>
                Dictionary
            </code>
            的数组的对象，或当完成查询的时候出现了问题时，返回一个
            <code>
                NSError
            </code>
            的对象。
        </li>
        <li>
            这里你使用了一些Swift风格的数组进行映射，来传递字典到初始化方法，来创建
            <code>
                Result
            </code>
            对象。当完成后，
            <code>
                itunesResults
            </code>
            变量就包含了一个
            <code>
                Result
            </code>
            对象的数组。
        </li>
        <li>
            在你设置新的数据到
            <code>
                searchResultsController
            </code>
            上前，你需要确保你正在主线程上。因此你使用
            <code>
                DispatchQueue.main.async
            </code>
            来获取主线程。你尚未设置任何bindings，但一旦你有了，变更            
            <code>
                searchResultsController
            </code>
            上的content property将更新
            <code>
                NSTableView
            </code>
            （以及潜在的其它的UI元素）在主线程上。在后台线程更新UI永远都是禁忌。
        </li>
        <li>
            最后，设置
            <code>
                NSArrayController
            </code>
            中的content property。这个array controller有一些不同的方法来添加或删除它所管理的对象。每次当你搜索时，你想要清除之前的结果，并使用最新的查询的结果。此时，打印
            <code>
                searchResultsController
            </code>
            的内容到控制台上，来验证每件事都如同计划中一般进行。
        </li>
    </ol>
    <p>
        现在，添加下列的
        <code>
            ViewController
        </code>
        extension：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">ViewController</span>: <span class="hljs-title">NSTextFieldDelegate</span> </span>{
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">control</span><span class="hljs-params">(<span class="hljs-number">_</span> control: NSControl, textView: NSTextView, doCommandBy commandSelector: Selector)</span></span> -&gt; <span class="hljs-type">Bool</span> {
    <span class="hljs-keyword">if</span> commandSelector == #selector(insertNewline(<span class="hljs-number">_</span>:)) {
      searchClicked(searchTextField)
    }
    <span class="hljs-keyword">return</span> <span class="hljs-literal">false</span>
  }
}
</pre>
    <p>
        当用户在文本输入框中点击Enter时，就会调用
        <code>
            searchClicked(_:)
        </code>
        ，就如同你点击搜索按钮一样。这使得使用键盘搜索更加得快速和容易。
    </p>
    <p>
        Build并运行，输入
        Build and run, type
        <em>
            flappy
        </em>
        到搜索栏中并点击Enter按钮或单击搜索按钮。你应该会在控制台中看到一些类似下面所示的内容：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.04.46-PM-650x82.png"
        alt="Search result" width="650" height="82" class="alignnone size-large wp-image-142721"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.04.46-PM-650x82.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.04.46-PM-480x60.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.04.46-PM.png 1192w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <h2>
        你的第一个Bindings
    </h2>
    <p>
        是时候来获取这个教程的精要了！
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/allthethings1.jpg">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/10/allthethings1.jpg"
            alt="allthethings1" width="400" height="300" class="aligncenter size-full wp-image-118939">
        </a>
    </p>
    <p>
        第一步是将array controller绑定到table view上。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        并选择标题为
        <em>
            Search Results Table View (Bind)
        </em>
        的列表。打开
        <em>
            Bindings Inspector
        </em>
        ：它是右侧窗格中的倒数第二个，就位于
        <em>
            View Effects Inspector
        </em>
        之前。
    </p>
    <p>
        展开
        <em>
            Table Contents
        </em>
        头下的
        <em>
            Content
        </em>
        选项。勾选靠近        
        <em>
            ‘Bind to ‘
        </em>
        的选框并确保
        <em>
            Search Results Controller
        </em>
        展示在下拉菜单中。最后，确保
        <em>
            Controller Key
        </em>
        被设置为
        <em>
            arrangedObjects
        </em>
        ，就像：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/TableViewBinding-170x320.png"
        alt="TableViewBinding" width="170" height="320" class="aligncenter size-medium wp-image-126033"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/TableViewBinding-170x320.png 170w, https://koenig-media.raywenderlich.com/uploads/2016/01/TableViewBinding-265x500.png 265w, https://koenig-media.raywenderlich.com/uploads/2016/01/TableViewBinding.png 520w"
        sizes="(max-width: 170px) 100vw, 170px">
    </p>
    <p>
        build并运行，并搜索一些你知道的事，将返回大量的结果。你会看到至少5个结果，除非你改变下拉菜单中的数字。由于bindings，这个array controller就自动地代表了table view中的内容。然后，他们都叫“Table View Cell”。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/arrayboundnotitlesintable-700x463.png"
        alt="arrayboundnotitlesintable" width="700" height="463" class="aligncenter size-large wp-image-126034"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/arrayboundnotitlesintable-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/arrayboundnotitlesintable-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/arrayboundnotitlesintable-768x508.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        你会得到一堆重复的匹配，因为cell中的text field不清楚它们应当读取在data model中哪个的property。
    </p>
    <h3>
        绑定Text Field到它们的Property
    </h3>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        并前往
        <em>
            View Controller Scene
        </em>
        。展开table view中的对象知道你发现名为
        <em>
            Title TextField (Bind)
        </em>
        的文本输入框。选择这个对象并打开
        <em>
            Bindings Inspector
        </em>
        。
    </p>
    <p>
        展开
        <em>
            Value
        </em>
        选项并绑定到
        <em>
            Table Cell View
        </em>
        对象上。确保
        <em>
            Model Key Path
        </em>
        为
        <em>
            objectValue.trackName
        </em>
        。
    </p>
    <p>
        <code>
            objectValue
        </code>
        是一个在table cell view上的property，它从
        <code>
            NSTableView
        </code>
        上的每个cell view对象的到table的binding中获取相应的值。
    </p>
    <p>
        在这个case中，
        <code>
            objectValue
        </code>
        等于这行的
        <code>
            Result
        </code>
        模型对象。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/trackName.png"
        alt="trackName" width="248" height="215" class="aligncenter size-full wp-image-126070">
    </p>
    <p>
        通过将其值绑定到
        <em>
            objectValue.artistName
        </em>
        上，为
        <em>
            Publisher TextField (Bind)
        </em>
        重复上面的过程。
    </p>
    <p>
        Build并运行，然后再次搜索。这次，标题和publisher会展示如：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/title-and-publisher-700x463.png"
        alt="title and publisher" width="700" height="463" class="aligncenter size-large wp-image-126071"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/title-and-publisher-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/title-and-publisher-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/title-and-publisher-768x508.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/title-and-publisher.png 1133w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h3>
        添加在Rank中
    </h3>
    <p>
        对于缺失的rank列呢？Rank并不设置在你从iTunes获取的数据模型的对象上。然而，从iTunes得到的结果的顺序，确实告诉了你当搜索iTunes时展示在设备上的顺序。
    </p>
    <p>
        只需再多做一点工作，你就可以设置排名的值了。
    </p>
    <p>
        在
        <code>
            ViewController
        </code>
        中
        <code>
            //Deal with rank here later
        </code>
        评论的下面，添加下列的代码：
    </p>
    <pre lang="swift" class="hljs kotlin">.enumerated()
.map({ index, element -&gt; Result <span class="hljs-keyword">in</span>
  element.rank = index + <span class="hljs-number">1</span>
  <span class="hljs-keyword">return</span> element
})
</pre>
    <p>
        这个代码调用了
        <code>
            enumerated()
        </code>
        已获取序号和相应这个序号的对象。然后调用
        <code>
            map(:_)
        </code>
        来为每个对象设置排名的值，并返回结果的数组。
    </p>
    <p>
        现在，回到
        <em>
            Main.storyboard
        </em>
        ，选择
        <em>
            Rank TextField (Bind)
        </em>
        并打开
        <em>
            Bindings Inspector
        </em>
        。在
        <em>
            Value
        </em>
        区，绑定到
        <em>
            Table Cell View
        </em>
        。确保
        <em>
            Controller Key
        </em>
        是空的，并设置
        <em>
            Model Key Path
        </em>
        为
        <code>
            objectValue.rank
        </code>
        。
    </p>
    <p>
        Build并运行，app会在table view的第一列中展示排名：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/ranktitlepublisher-700x463.png"
        alt="ranktitlepublisher" width="700" height="463" class="aligncenter size-large wp-image-126072"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/ranktitlepublisher-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/ranktitlepublisher-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/ranktitlepublisher-768x508.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/ranktitlepublisher.png 1133w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        现在，你需要将用户选择的
        <code>
            Result
        </code>
        选项绑定到UI的剩余的部分。
    </p>
    <h2>
        绑定Table View的选择
    </h2>
    <p>
        在table中绑定选择包含两步：
    </p>
    <ol>
        <li>
            首先绑定
            <code>
                NSArrayController
            </code>
            到table的选择上。
        </li>
        <li>
            然后，你可以绑定NSArrayController中
            <code>
                selection
            </code>
            对象的property到各自的label和其它的property。
        </li>
    </ol>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        。选择
        <em>
            Search Results Table View (Bind)
        </em>
        并打开
        <em>
            Bindings Inspector
        </em>
        。
    </p>
    <p>
        在
        <em>
            Table Content
        </em>
        区展开
        <em>
            Selection Indexes
        </em>
        选项。查看
        <em>
            绑定到
        </em>
        <em>
            Search Results Controller
        </em>
        对象。
    </p>
    <p>
        在
        <em>
            Controller Key
        </em>
        框中输入
        <em>
            selectionIndexes
        </em>
        。这个table有一个
        <code>
            selectionIndexes
        </code>
        property，它包含一个序号的集合，这些序号代表了用户在table中选择的内容。
    </p>
    <p>
        在这个case中，我已设定了这个table view同时只能允许一行被选中。当然如果app需要的话，你可以允许同时选择多行，就如同Finder允许你同时选择多个文件。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/selectionIndexes.png"
        alt="selectionIndexes" width="248" height="262" class="aligncenter size-full wp-image-126073">
    </p>
    <p>
        <code>
            NSArrayController
        </code>
        对象有一个
        <code>
            selection
        </code>
        property，它会返回一个对象的数组。当你把table view的
        <code>
            selectionIndexes
        </code>
        property绑定到array controller时，array controller中的
        <code>
            selection
        </code>
        property就会被相应的在table中选择的序号构成的对象所填充。
    </p>
    <p>
        下面一步是吧label和其它的UI元素绑定到选择的对象上。
    </p>
    <p>
        找到并选择
        <em>
            App Name Label (Bind)
        </em>
        。将他的value绑定到
        <em>
            Search Results Controller
        </em>  
        上。
        <em>
            Controller Key
        </em>
        为
        <em>
            selection
        </em>
        , and
        <em>
            Model Key Path
        </em>
        为
        <em>
            trackName
        </em>
        。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/mainTrackName.png"
        alt="mainTrackName" width="247" height="193" class="aligncenter size-full wp-image-126075">
    </p>
    <p>
        Build并运行，选择在table view中的任一app，它的title就会出现在文本输入框中：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Main-Title-700x463.png"
        alt="Main Title" width="700" height="463" class="aligncenter size-large wp-image-126076"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Main-Title-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/Main-Title-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Main-Title-768x508.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/Main-Title.png 1133w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        你以及看到了，从你的模型获取数据，再放入到UI中是多么得容易。不过，如果数据需要以某种方式进行一下格式化，例如货币或日期，该怎么做呢？
    </p>
    <p>
        幸运的是，有一系列內建的对象，使得改变指定数据展示到label上的形式变得非常得容易。
    </p>
    <h2>
        格式化被绑定的数据
    </h2>
    <p>
        找到title为
        <em>
            Price Label (Bind)
        </em>
        的label。将它绑定到
        <em>
            Search Results Controller
        </em>
        对象上，并确保
        <em>
            Controller Key
        </em>
        为
        <em>
            selection
        </em>
        。
    </p>
    <p>
        设置
        <em>
            Model Key Path
        </em>
        为
        <em>
            price
        </em>
        ，然后，在Object Library中找到
        <em>
            Number Formatter
        </em>
        ，将它拖拽到名为
        <em>
            Label
        </em>
        的
        <code>
            NSTextFieldCell
        </code>
        上，就在
        <em>
            Price
        </em>
        文本输入框的下面。
    </p>
    <p>
        最后，选择
        <em>
            Number Formatter
        </em>
        ，打开
        <em>
            Attributes Inspector
        </em>
        并改变
        <em>
            Style
        </em>
        为
        <em>
            Currency
        </em>
        。
    </p>
    <p>
        当以上都完成后，你的storyboard和inspector应当看起来像下面这样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/09/currencyFormatter-1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/09/currencyFormatter-1-650x321.png"
            alt="currencyFormatter" width="650" height="321" class="aligncenter size-large wp-image-143266"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/09/currencyFormatter-1-650x321.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/09/currencyFormatter-1-480x237.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/09/currencyFormatter-1.png 1259w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Build并运行，从列表中选择任一app，现在货币应当全部展示的是正确的：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/priceformatted-700x463.png"
        alt="priceformatted" width="700" height="463" class="aligncenter size-large wp-image-126078"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/priceformatted-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/priceformatted-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/priceformatted-768x508.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/priceformatted.png 1133w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <div class="note">
        <p>
            <em>
                注意
            </em>
            ：数字格式化器是非常强大的。除了货币外，你也可以控制小数点后有几位数字，或者用单词拼写出数字。
        </p>
        <p>
            已有的格式化器对象有日期，字节计数，和其它几个不太常见的情况。如果它们都满足不了你，你甚至可以定制你自己的格式化器。
        </p>
    </div>
    <h3>
        格式化为字节
    </h3>
    <p>
        接下来你将使用
        <em>
            Byte Count Formatter
        </em>
        来显示文件的大小。
    </p>
    <p>
        找到并选择
        <em>
            File Size Label (Bind)
        </em>
        ，打开
        <em>
            Bindings Inspector
        </em>
        并绑定到
        <em>
            Search Results Controller
        </em>
        上。设置
        <em>
            Controller Key
        </em>
        为
        <em>
            selection
        </em>
        以及
        <em>
            Model Key Path
        </em>
        为
        <em>
            fileSizeInBytes
        </em>
        。
    </p>
    <p>
        然后在
        <em>
            Object Library
        </em>
        中找到
        <em>
            Byte Count Formatter
        </em>
        并附加到
        <em>
            NSTextFieldCell
        </em>
        上。这里无需进行任何的配置，字节格式化器的默认设置就可以工作得很好。
    </p>
    <p>
        你应当在document outline看到你的字节技术格式化器就像下面这样：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-formatter.png"
        alt="byte count formatter" width="349" height="124" class="aligncenter size-full wp-image-126083">
    </p>
    <p>
        Build并运行，在列表中选择一个app，你就会看到使用合适单位的文件的大小，例如KB，MB和GB：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-final-700x463.png"
        alt="byte count final" width="700" height="463" class="aligncenter size-large wp-image-126084"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-final-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-final-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-final-768x508.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-final.png 1133w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        你现在已经绑定了一些东西，所以这里有一个剩余的你需要去绑定的键的短表：
    </p>
    <ul>
        <li>
            绑定
            <em>
                Artist Label (Bind)
            </em>
            到
            <em>
                artistName
            </em>
            。
        </li>
        <li>
            绑定
            <em>
                Publication Date (Bind)
            </em>
            到
            <em>
                releaseDate
            </em>
            。
        </li>
        <li>
            添加一个
            <em>
                Date Formatter
            </em>
            ；默认的设置就很棒。
        </li>
        <li>
            绑定
            <em>
                All Ratings Count (Bind)
            </em>
            到
            <em>
                userRatingCount
            </em>
            。
        </li>
        <li>
            绑定
            <em>
                All Ratings (Bind)
            </em>
            到
            <em>
                averageUserRating
            </em>
            。
        </li>
        <li>
            绑定
            <em>
                Genre Label (Bind)
            </em>
            到
            <em>
                primaryGenre
            </em>
            。
        </li>
    </ul>
    <p>
        全部的这些label应当被绑定到
        <em>
            Search Results Controller
        </em>
        并设置
        <em>
            selection
        </em>
        的controller key。
    </p>
    <p>
        为了让你的UI更加精确，你也可以绑定
        <em>
            Description Text View (Bind)
        </em>
        ，
        <em>
            Attributed String
        </em>
        binding到
        <em>
            itemDescription
        </em>
        Model Key Path上。确保你绑定的是
        <code>
            NSTextView
        </code>
        ，它在层级中有一些深。
        <i>
            并不是
        </i>
        <code>
            NSScrollView
        </code>
        ，它在顶层。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/09/selecttextView.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/09/selecttextView-412x320.png"
            alt="selecttextView" width="360" height="280" class="aligncenter size-medium wp-image-143267"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/09/selecttextView-412x320.png 412w, https://koenig-media.raywenderlich.com/uploads/2016/09/selecttextView.png 602w"
            sizes="(max-width: 360px) 100vw, 360px">
        </a>
    </p>
    <p>
        Build并运行，你会看到大部分的UI已被填充：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/mostly-populated-700x421.png"
        alt="mostly populated" width="700" height="421" class="aligncenter size-large wp-image-126085"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/mostly-populated-700x421.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/mostly-populated-480x289.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/mostly-populated-768x462.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/mostly-populated.png 1200w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        绑定图像
    </h2>
    <p>
        下面一步是为icon绑定其图像到
        <em>
            Icon Image View
        </em>
        上。这个有一点trick，因为JSON并不包含事实上的图像，而是用一个图片的URL来代替。
    </p>
    <p>
        <code>
            Result
        </code>
        包含了一个方法来下载图片文件，并让它成为
        <code>
            artworkImage
        </code>
        property的可用
        <code>
            NSImage
        </code>
        对象。
    </p>
    <h3>
        即时的下载
    </h3>
    <p>
        你并不想一次下载全部的图标 - 而是只需下载那个当前在table中选择的那个。你将在选择发生变化的时候下载一个新的icon。
    </p>
    <p>
        添加下列的方法到
        <em>
            ViewController
        </em>
        中：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-comment">//1</span>
<span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">tableViewSelectionDidChange</span><span class="hljs-params">(<span class="hljs-number">_</span> notification: NSNotification)</span></span> {
  <span class="hljs-comment">//2</span>
  <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> result = searchResultsController.selectedObjects.first <span class="hljs-keyword">as</span>? <span class="hljs-type">Result</span> <span class="hljs-keyword">else</span> { <span class="hljs-keyword">return</span> }
  <span class="hljs-comment">//3</span>
  result.loadIcon()
}
</pre>
    <p>
        这里是详情：
    </p>
    <ol>
        <li>
            <code>
                tableViewSelectionDidChange(_:)
            </code>
            会在用户每次table选择不同的行时被触发。
        </li>
        <li>
            array controller的property
            <code>
                selectedObjects
            </code>
            返回了一个数组，它包含了全部的在table中选择的行的序号。在这个case中，这个table只允许单选行，因此这个数组总是只包含一个对象。你用
            <code>
                result
            </code>
            对象的形式来储存它。
        </li>
        <li>
            最后，你调用了
            Finally, you call
            <code>
                loadIcon()
            </code>
            。这个方法会在后台线程下载图像，然后下载完后在主线程更新
            <code>
                Result
            </code>
            对象的
            <code>
                artworkImage
            </code>
            property。
        </li>
    </ol>
    <h3>
        绑定Image View
    </h3>
    <p>
        Now that your code is in place, you’re ready to bind the image view.
    </p>
    <p>
        Head back to
        <em>
            Main.storyboard
        </em>
        , select the
        <em>
            Icon Image View (Bind)
        </em>
        object and open the
        <em>
            Bindings Inspector
        </em>
        .
    </p>
    <p>
        Go to the
        <em>
            Value
        </em>
        section and bind to the
        <em>
            Search Results Controller
        </em>
        , set
        <em>
            Controller Key
        </em>
        to
        <em>
            selection
        </em>
        and
        <em>
            Model Key Path
        </em>
        to
        <em>
            artworkImage
        </em>
        .
    </p>
    <p>
        Did you notice the
        <em>
            Value Path
        </em>
        and a
        <em>
            Value URL
        </em>
        sections? Both of these bindings are intended for local resources only.
        You
        <i>
            can
        </i>
        connect them to a network resource, but that will block the UI thread
        until the resource has finished downloading.
    </p>
    <p>
        Build and run, search for
        <em>
            fruit
        </em>
        and then select a row. You’ll see the icon image appear once it has downloaded:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/icon-populated-700x421.png"
        alt="icon populated" width="700" height="421" class="aligncenter size-large wp-image-126088"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/icon-populated-700x421.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/icon-populated-480x289.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/icon-populated-768x462.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/icon-populated.png 1200w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        The collection view beneath the description text view is currently looking
        a little bare. Time to populate that with some screenshots.
    </p>
    <h3>
        Populating the Collection View
    </h3>
    <p>
        First you’ll bind the collection view to the
        <code>
            screenShots
        </code>
        property and then ensure the
        <code>
            screenShots
        </code>
        array populated correctly.
    </p>
    <p>
        Select the
        <em>
            Screen Shot Collection View (Bind)
        </em>
        . Open the
        <em>
            Bindings Inspector
        </em>
        and expand the
        <em>
            Content
        </em>
        binding in the
        <em>
            Content
        </em>
        group.
    </p>
    <p>
        Bind to the
        <em>
            Search Results Controller
        </em>
        , set
        <em>
            Controller Key
        </em>
        to
        <em>
            selection
        </em>
        and
        <em>
            Model Key Path
        </em>
        to
        <em>
            screenShots
        </em>
        .
    </p>
    <p>
        The
        <code>
            screenShots
        </code>
        array starts out empty.
        <code>
            loadScreenShots()
        </code>
        downloads the image files and populates the
        <code>
            screenShots
        </code>
        array with
        <code>
            NSImage
        </code>
        objects.
    </p>
    <p>
        Add the following line to
        <em>
            ViewController.swift
        </em>
        , in
        <code>
            tableViewSelectionDidChange(_:)
        </code>
        , right after
        <code>
            result.loadIcon()
        </code>
        :
    </p>
    <pre lang="swift" class="hljs">result.loadScreenShots()
</pre>
    <p>
        This populates the screenshot images and creates the right number of views.
    </p>
    <p>
        The next thing you need to do is set the right collection view item prototype.
        Although the collection view item scene is present in the storyboard, it’s
        not connected to the collection view. You’ll have to create this connection
        in code.
    </p>
    <p>
        Add the following code to the end of
        <code>
            viewDidLoad()
        </code>
        in
        <em>
            ViewController.swift
        </em>
        :
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-keyword">let</span> itemPrototype = <span class="hljs-keyword">self</span>.storyboard?.instantiateController(withIdentifier:
  <span class="hljs-string">"collectionViewItem"</span>) <span class="hljs-keyword">as</span>! <span class="hljs-type">NSCollectionViewItem</span>
collectionView.itemPrototype = itemPrototype
</pre>
    <p>
        Now that the collection view knows how to create each item via the prototype,
        you need to provide the content for each item via a binding.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and select
        <em>
            Screen Shot Image View (Bind)
        </em>
        inside the
        <em>
            Collection View Item Scene
        </em>
        . You’ll find this floating next to the main view controller.
    </p>
    <p>
        Bind the
        <em>
            Value
        </em>
        option to the
        <em>
            Collection View Item
        </em>
        object. The controller key should be blank, and
        <em>
            Model Key Path
        </em>
        should be
        <em>
            representedObject
        </em>
        .
    </p>
    <p>
        The
        <code>
            representedObject
        </code>
        property represents the object in the collection view array for that item;
        in this case, it’s an
        <code>
            NSImage
        </code>
        object.
    </p>
    <p>
        Build and run, and you’ll see see the screenshots appearing below the
        description text:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/screenshots-700x421.png"
        alt="screenshots" width="700" height="421" class="aligncenter size-large wp-image-126089"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/screenshots-700x421.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/screenshots-480x289.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/screenshots-768x462.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/screenshots.png 1200w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Great work! There’s just a few more features of Cocoa Bindings to cover
        before wrapping up.
    </p>
    <h2>
        Binding Other Properties
    </h2>
    <p>
        Your UI could use a bit of feedback. Users don’t like to stare at static
        screens when something is loading, and they’ll assume the worst when nothing
        happens in response to a user action.
    </p>
    <p>
        Instead of leaving a static screen, you’ll show a spinner to the user
        while the image downloads.
    </p>
    <h3>
        Seting Up a Progress Spinner
    </h3>
    <p>
        You can easily bind a progress spinner to a new property in the
        <code>
            ViewController
        </code>
        . Add the following property to
        <code>
            ViewController
        </code>
        :
    </p>
    <pre lang="swift" class="hljs cs"><span class="hljs-keyword">dynamic</span> <span class="hljs-keyword">var</span> loading = <span class="hljs-literal">false</span>
</pre>
    <p>
        Loading requires two things in order to work correctly: the
        <code>
            dynamic
        </code>
        keyword, and the parent class to be a subclass of
        <code>
            NSObject
        </code>
        . Bindings relies on KVO (Key Value Observing), and a Swift class that
        doesn’t inherit from NSObject wouldn’t be able to use KVO.
    </p>
    <p>
        Add the following line of code inside
        <code>
            searchClicked(:_)
        </code>
        , right before the line that executes the call to
        <code>
            getSearchResults(_:results:langString:completionHandler:)
        </code>
        :
    </p>
    <pre lang="swift" class="hljs javascript">loading = <span class="hljs-literal">true</span>
</pre>
    <p>
        Locate the line in the same method that sets the
        <code>
            content
        </code>
        property on
        <code>
            searchResultsController
        </code>
        . Add the following code immediately before that line:
    </p>
    <pre lang="swift" class="hljs objectivec"><span class="hljs-keyword">self</span>.loading = <span class="hljs-literal">false</span>
</pre>
    <p>
        Next, open
        <em>
            Main.storyboard
        </em>
        and select
        <em>
            Search Progress Indicator (Bind)
        </em>
        . You’re going to bind two properties of the progress spinner:
        <code>
            hidden
        </code>
        and
        <code>
            animate
        </code>
        .
    </p>
    <p>
        First, expand the
        <em>
            Hidden
        </em>
        group, and bind to the
        <em>
            View Controller
        </em>
        .
        <em>
            Controller Key
        </em>
        should be blank, and
        <em>
            Model Key Path
        </em>
        should be
        <em>
            self.loading
        </em>
        .
    </p>
    <p>
        In this case, you want
        <code>
            hidden
        </code>
        to be false when
        <code>
            loading
        </code>
        is
        <code>
            true
        </code>
        , and vice versa. There’s an easy way to do that: use
        <code>
            NSValueTransformer
        </code>
        to flip the value of the boolean.
    </p>
    <div class="note">
        <p>
            <code>
                NSValueTransformer
            </code>
            is a class that helps you convert the form or value of data when moving
            between UI and data model.
        </p>
        <p>
            You can subclass this object in order to do much more complex conversions,
            you can learn more about NSValueTransformers in this tutorial:
            <a href="http://www.raywenderlich.com/21752/how-to-use-cocoa-bindings-and-core-data-in-a-mac-app"
            target="_blank" title="How to Use Cocoa Bindings and Core Data in a Mac App">
                How to Use Cocoa Bindings and Core Data in a Mac App
            </a>
            .
        </p>
    </div>
    <p>
        Choose
        <em>
            NSNegateBoolean
        </em>
        from the
        <em>
            Value Transformer
        </em>
        dropdown list.
    </p>
    <p>
        Bind the
        <em>
            Animate
        </em>
        value to the
        <em>
            View Controller
        </em>
        object. Set
        <em>
            Controller Key
        </em>
        as blank, and set
        <em>
            Model Key Path
        </em>
        as
        <em>
            self.loading
        </em>
        .
    </p>
    <p>
        This Boolean doesn’t need to be negated. The bindings look like this:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Binding-animating.png"
        alt="Binding animating" width="248" height="700" class="aligncenter size-full wp-image-126093"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Binding-animating.png 248w, https://koenig-media.raywenderlich.com/uploads/2016/01/Binding-animating-113x320.png 113w, https://koenig-media.raywenderlich.com/uploads/2016/01/Binding-animating-177x500.png 177w"
        sizes="(max-width: 248px) 100vw, 248px">
    </p>
    <p>
        Build and run; search for something that will return a large number of
        results so you have time to watch the spinner do its thing:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Spinner-animating-700x421.png"
        alt="Spinner animating" width="700" height="421" class="aligncenter size-large wp-image-126092"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Spinner-animating-700x421.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/Spinner-animating-480x289.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Spinner-animating-768x462.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/Spinner-animating.png 1200w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        Adding a Little More Detail
    </h2>
    <p>
        Cocoa Bindings can do more than what you’ve learned so far: you can bind
        colors and fonts to labels, enable and disable controls, and even set different
        values for labels depending on their state.
    </p>
    <p>
        Build and run your app, and you’ll notice that you see
        <em>
            No Selection
        </em>
        on all your labels before. This isn’t very nice for a user to see when
        they start your app.
    </p>
    <p>
        Find the label titled
        <em>
            Price Label (Bind)
        </em>
        , and expand
        <em>
            Value
        </em>
        . Under
        <em>
            No Selection Placeholder
        </em>
        , put
        <code>
            --
        </code>
        as shown below:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.37.50-PM.png"
        alt="Screen Shot 2016-08-30 at 12.37.50 PM" width="261" height="492" class="alignnone size-full wp-image-142725"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.37.50-PM.png 261w, https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.37.50-PM-170x320.png 170w"
        sizes="(max-width: 261px) 100vw, 261px">
    </p>
    <p>
        Build and run your app, and you’ll see that the
        <em>
            Price
        </em>
        label now has a nice placeholder value:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.38.00-PM.png"
        alt="Screen Shot 2016-08-30 at 12.38.00 PM" width="212" height="191" class="alignnone size-large wp-image-142726">
    </p>
    <p>
        Set all labels that say
        <em>
            No Selection
        </em>
        to have a placeholder of your choice.
    </p>
    <div class="note">
        <p>
            <em>
                Note
            </em>
            : If you want the label to be blank, you can set the
            <em>
                No Selection Placeholder
            </em>
            to a
            <em>
                space
            </em>
            .
        </p>
    </div>
    <h2>
        Where to Go From Here?
    </h2>
    <div class="inline-video-ad" id="sub-banner-inline">
        <div class="inline-video-ad-wrapper">
            <a href="https://videos.raywenderlich.com/courses">
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
        That’s the basics of Cocoa Bindings on macOS. You’ve seen how easy it
        can be to connect data and UI.
    </p>
    <p>
        In this tutorial, you learned the following:
    </p>
    <ol>
        <li>
            How to use Interface Builder to quickly and easily bind objects to data.
        </li>
        <li>
            How to keep models and views in sync with the user’s current selection.
        </li>
        <li>
            How to use methods and bindings together to control behaviors and organize
            data.
        </li>
        <li>
            How to quickly build out UI features like progress spinners.
        </li>
    </ol>
    <p>
        You can download the final project
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/09/AppResearchBindings-Final.zip"
        target="_blank" title="">
            here
        </a>
        . Hopefully, you can save a lot of time (and code!) by adopting this technology.
    </p>
    <p>
        Each binding has a lot of little settings and options, many of which you
        didn’t explore in this tutorial. Check out
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/CocoaBindingsRef/Concepts/BindingsOptions.html"
        target="_blank" title="">
            this resource on Cocoa bindings
        </a>
        provided by Apple. It covers a lot of the details about what the options
        in the bindings windows do.
    </p>
    <p>
        I hope you enjoyed this Cocoa Bindings on macOS tutorial and picked up
        some new techniques to use to accelerate your development process. You’ve
        just opened up a whole new universe!
    </p>
</div>