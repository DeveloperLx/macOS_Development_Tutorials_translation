# macOS教程：在Menu Bar App中的Menu和Popover

#### [原文地址](https://www.raywenderlich.com/165853/menus-popovers-menu-bar-apps-macos) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div class="note">
        <p>
            <em>
                更新日志：
            </em>
            本教程已由Warren Burton更新至支持Xcode 9及Swift 4的版本。
            <a href="https://www.raywenderlich.com/98178/os-x-tutorial-menus-popovers-menu-bar-apps"
            sl-processed="1">
                原教材
            </a>
            由Mikael Konutgan撰写。
        </p>
    </div>
    <div id="attachment_105403" style="width: 260px" class="wp-caption alignright">
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/08/Menus-Popovers-feature.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/08/Menus-Popovers-feature.png"
            alt="Learn how to make a menu bar macOS app with a popover!" width="250"
            height="250" class="size-full wp-image-105403">
        </a>
        <p class="wp-caption-text">
            学习如何使用popover来制作一个macOS app的菜单栏！
        </p>
    </div>
    <p>
        菜单栏app长期以来都是macOS中的主打项。很多app例如
        <a href="https://agilebits.com/onepassword/mac" target="_blank" sl-processed="1">
            1Password
        </a>
        和
        <a href="http://dayoneapp.com" target="_blank" sl-processed="1">
            Day One
        </a>
        都有着相应的菜单栏app。其它app诸如
        <a href="http://flexibits.com/fantastical" target="_blank" sl-processed="1">
            Fantastical
        </a>
        甚至仅仅存在于macOS的菜单栏中。
    </p>
    <p>
        在本教程中，你将会构建一个菜单栏app，它会在一个popover中展示鼓舞人心的名言。你会在其中学到：
    </p>
    <ul>
        <li>
            如何创建一个菜单栏的图标
        </li>
        <li>
            如何让app仅仅存在于菜单栏中
        </li>
        <li>
            如何为用户添加菜单
        </li>
        <li>
            如何让popover按照需求展示和隐藏 - 也就是说事件监视
        </li>
    </ul>
    <div class="note">
        <em>
            注意：
        </em>
        本教程假定你已熟悉了Swift和macOS。如果你需要再温习一下，欢迎关注我们的
        <a href="https://www.raywenderlich.com/151741/macos-development-beginners-part-1"
        target="_blank" sl-processed="1">
            macOS Development for Beginners
        </a>
        系列教程。
    </div>
    <h2>
        入门
    </h2>
    <p>
        打开Xcode。点击
        <em>
            File/New/Project…
        </em>
        ，然后选择
        <em>
            macOS/Application/Cocoa App
        </em>
        模板并点击
        <em>
            Next
        </em>
        。
    </p>
    <p>
        在下一屏中，输入
        <em>
            Quotes
        </em>
        作为
        <em>
            Product Name
        </em>
        ，选择你的
        <em>
            Organization Name
        </em>
        和
        <em>
            Organization Identifier
        </em>
        。然后选择
        <em>
            Swift
        </em>
        编程语言，选中
        <em>
            Use Storyboards
        </em>
        。确保
        <em>
            Create Document-Based Application
        </em>
        ，
        <em>
            Use Core Data
        </em>
        ，
        <em>
            Include Unit tests
        </em>
        和
        <em>
            Include UI Tests
        </em>
        均不选中。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/configure-project.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/configure-project-442x320.png"
            alt="configure new project" width="442" height="320" class="aligncenter size-medium wp-image-167056"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/configure-project-442x320.png 442w, https://koenig-media.raywenderlich.com/uploads/2017/07/configure-project-650x471.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/07/configure-project.png 1480w"
            sizes="(max-width: 442px) 100vw, 442px">
        </a>
    </p>
    <p>
        最后，再次点击
        <em>
            Next
        </em>
        ，选择一个地方来保存项目，并点击
        <em>
            Create
        </em>
        。
    </p>
    <p>
        设置完成新项目之后，打开
        <em>
            AppDelegate.swift
        </em>
        并添加下列的property到类中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">let</span> statusItem = <span class="hljs-type">NSStatusBar</span>.system.statusItem(withLength:<span class="hljs-type">NSStatusItem</span>.squareLength)
</pre>
    <p>
        这就创建了一个
        <em>
            Status Item
        </em>
        - 也就是说app的icon - 带有一个固定的长度并放置在菜单栏中，用户能够看到并使用它。
    </p>
    <p>
        接下来，你需要为status item关联一个图像，让你的app能够在菜单栏中易于识别。
    </p>
    <p>
        在project navigator中周到
        <code>
            Assets.xcassets
        </code>
        ，下载图片
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/03/StatusBarButtonImage@2x.png"
        sl-processed="1">
            StatusBarButtonImage@2x.png
        </a>
        并将它拖拽到asset目录中。
    </p>
    <p>
        选择图片并打开attributes inspector。将
        <em>
            Render As
        </em>
        选项改变为Template Image。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/add-image-asset.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/add-image-asset-480x109.png"
            alt="" width="480" height="109" class="aligncenter size-medium wp-image-167058"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/add-image-asset-480x109.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/07/add-image-asset-650x147.png 650w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        如果你想使用自己的图片，请确保它是黑白图片，并将它配置为template image。这样Status Item才能在亮色和暗色主题下的菜单栏中都看起来比较不错。
    </p>
    <p>
        回到
        <em>
            AppDelegate.swift
        </em>
        ，添加下列的代码到
        <code>
            applicationDidFinishLaunching(\_:)
        </code>
        中
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> button = statusItem.button {
  button.image = <span class="hljs-type">NSImage</span>(named:<span class="hljs-type">NSImage</span>.<span class="hljs-type">Name</span>(<span class="hljs-string">"StatusBarButtonImage"</span>))
  button.action = #selector(printQuote(<span class="hljs-number">_</span>:))
}
</pre>
    <p>
        这会把你刚刚添加的图片作为icon配置到status item的上面，然后配置了一个当你点击这个item时会发生的动作。现在这里会出现一个错误，但你很快就会修复它。
    </p>
    <p>
        在类中添加下列的代码：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@objc</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">printQuote</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: Any?)</span></span> {
  <span class="hljs-keyword">let</span> quoteText = <span class="hljs-string">"Never put off until tomorrow what you can do the day after tomorrow."</span>
  <span class="hljs-keyword">let</span> quoteAuthor = <span class="hljs-string">"Mark Twain"</span>
  
  <span class="hljs-built_in">print</span>(<span class="hljs-string">"<span class="hljs-subst">\(quoteText)</span> — <span class="hljs-subst">\(quoteAuthor)</span>"</span>)
}
</pre>
    <p>
        这个方法将会把名言直接打印到控制台中。
    </p>
    <p>
        注意
        <code>
            @objc
        </code>
        这个标记。它会把这个方法暴露给Objective-C的运行时，来让按钮响应这里的动作。
    </p>
    <p>
        运行app，你就会看到新的菜单栏app了。你办到了！
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/menubar-light.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/menubar-light-650x10.png"
            alt="light mode menu bar" width="650" height="10" class="aligncenter size-large wp-image-167060"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/menubar-light-650x10.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/07/menubar-light-480x8.png 480w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/menubar-dark.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/menubar-dark-650x10.png"
            alt="dark mode menu bar" width="650" height="10" class="aligncenter size-large wp-image-167059"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/menubar-dark-650x10.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/07/menubar-dark-480x8.png 480w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <div class="note">
        <p>
            <em>
                注意
            </em>
            ：如果菜单栏中的app太多了，可能你会无法看到这个按钮。可以切换到一个比Xcode的菜单少的app（例如Finder），你应该就可以看到它了。
        </p>
    </div>
    <p>
        每次你点击菜单栏的icon的时候，你就会看到名言被打印到了Xcode的控制台上。
    </p>
    <h2>
        隐藏Dock中的Icon和主窗口
    </h2>
    <p>
        在你完成完整功能的菜单栏app之前，还有两件小事需要做一下。
    </p>
    <ol>
        <li>
            禁用dock中的icon。
        </li>
        <li>
            移除主窗口。
        </li>
    </ol>
    <p>
        要禁用dock icon，只需打开
        <em>
            Info.plist
        </em>
        ，添加一个新的key
        <em>
            Application is agent (UIElement)
        </em>
        并将它的值设为
        <em>
            YES
        </em>
        。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2015/03/Application-Is-Agent-YES.png"
        class="aligncenter wp-image-98940" width="650">
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        如果你是一个编辑plist editor的专家，你可以随意地使用
        <code>
            LSUIElement
        </code>
        键来进行设置。
    </div>
    <p>
        现在该来处理主窗口了。
    </p>
    <ul>
        <li>
            打开
            <code>
                Main.storyboard
            </code>
        </li>
        <li>
            选择Window Controller场景并删除它。
        </li>
        <li>
            只留下View Controller场景。你很快就会用到它。
        </li>
    </ul>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/delete-window-scene.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/delete-window-scene-480x137.png"
            alt="delete window scene" width="480" height="137" class="aligncenter size-medium wp-image-167061"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/delete-window-scene-480x137.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/07/delete-window-scene-650x185.png 650w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        运行项目。你就会看到这个app已经没有主窗口了，也没有讨厌的dock icon，只有一个简单的status item放在菜单栏中。为自己庆祝一下吧
        :]
    </p>
    <h2>
        添加一个菜单到Status Item上
    </h2>
    <p>
        通常，点击它只有可怜兮兮的一个动作，是不值得成为一个菜单栏的app的。为你的app添加更多功能，最简单的办法就是添加菜单了。因此添加下列的方法到
        <code>
            AppDelegate
        </code>
        的尾部。
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">constructMenu</span><span class="hljs-params">()</span></span> {
  <span class="hljs-keyword">let</span> menu = <span class="hljs-type">NSMenu</span>()

  menu.addItem(<span class="hljs-type">NSMenuItem</span>(title: <span class="hljs-string">"Print Quote"</span>, action: #selector(<span class="hljs-type">AppDelegate</span>.printQuote(<span class="hljs-number">_</span>:)), keyEquivalent: <span class="hljs-string">"P"</span>))
  menu.addItem(<span class="hljs-type">NSMenuItem</span>.separator())
  menu.addItem(<span class="hljs-type">NSMenuItem</span>(title: <span class="hljs-string">"Quit Quotes"</span>, action: #selector(<span class="hljs-type">NSApplication</span>.terminate(<span class="hljs-number">_</span>:)), keyEquivalent: <span class="hljs-string">"q"</span>))

  statusItem.menu = menu
}
</pre>
    <p>
        然后在
        <code>
            applicationDidFinishLaunching(\_:)
        </code>
        的尾部添加对它的调用
    </p>
    <pre lang="swift" class="language-swift hljs">
        constructMenu()
    </pre>
    <p>
        你在这里创建了一个
        <code>
            NSMenu
        </code>
        ，并添加了三个
        <code>
            NSMenuItem
        </code>
        的实例，然后把status item的菜单设置为这个新的菜单。
    </p>
    <p>
        这里有一些事值得去关注：
    </p>
    <ul>
        <li>
            menu item的title是将会出现在菜单中的文本。如果需要的话，这里是实现本地化的一个好地方。
        </li>
        <li>
            动作，类似于按钮或者其它控件的动作，是当你在点击菜单项的时候将会调用的方法。
        </li>
        <li>
            <code>
                keyEquivalent
            </code>
            是用来激活菜单项的键盘快捷键。小写的字母将使用
            <em>
                Cmd
            </em>
            作为修饰键，而大写的字母则使用
            <em>
                Cmd+Shift
            </em>
            作为修饰键。这里的键盘快捷键只有当app位于应用的最前方且被激活的时候才会work。因此，在这个case中，这个菜单或其它的窗口必须在可见的情况下，键盘快捷键才可以使用，因为我们的app没有dock的icon。
        </li>
        <li>
            <code>
                separatorItem
            </code>
            则是一个不活动的菜单项，它只会表现为其它菜单项之间的一条灰色的线。我们可以用它来对菜单中的功能进行分组。
        </li>
        <li>
            <code>
                printQuote:
            </code>
            动作是你早已定义在
            <code>
                AppDelegate
            </code>
            中的方法，而
            <code>
                terminate:
            </code>
            动作则是定义在
            <code>
                NSApplication
            </code>
            中的方法。
        </li>
    </ul>
    <p>
        运行项目，然后点击status item，你就会看到一个菜单。庆祝一下进展吧！
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/Menu-Action.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/Menu-Action.png"
            alt="status bar item menu" width="442" height="180" class="aligncenter size-full wp-image-167062">
        </a>
    </p>
    <p>
        试验一下你的选项吧 - 选择
        <em>
            Print Quote
        </em>
        会在Xcode的控制台中打出一句名言，而选择
        <em>
            Quit Quotes
        </em>
        则会退出app。
    </p>
    <h2>
        给Status Item添加一个Popover
    </h2>
    <p>
        你已经看到了，使用代码来创建菜单是多么得容易，但在Xcode的控制台中展示名言，显然是无法被大多数你的终端用户所接受的。接来下，我们就会使用一个简单的view
        controller，来替代菜单展示名言。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/Create-QuotesViewController.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/Create-QuotesViewController-442x320.png"
            alt="" width="442" height="320" class="aligncenter size-medium wp-image-167063
            " srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/Create-QuotesViewController-442x320.png
            442w, https://koenig-media.raywenderlich.com/uploads/2017/07/Create-QuotesViewController-650x470.png
            650w, https://koenig-media.raywenderlich.com/uploads/2017/07/Create-QuotesViewController.png
            1460w " sizes="(max-width: 442px) 100vw, 442px " />
        </a>
    </p>
    <p>
        点击
        <em>
            File/New/File…
        </em>
        ，选择
        <em>
            macOS/Source/Cocoa Class
        </em>
        模板并点击
        <em>
            Next
        </em>
        。
    </p>
    <ul>
        <li>
            将这个类命名为
            <code>
                QuotesViewController
            </code>
            。
        </li>
        <li>
            将它成为
            <code>
                NSViewController
            </code>
            的子类。
        </li>
        <li>
            确保
            <em>
                Also create XIB file for user interface
            </em>
            未被勾选。
        </li>
        <li>
            将语言设置为
            <em>
                Swift
            </em>
            。
        </li>
    </ul>
    <p>
        最后，再次点击
        <em>
            Next
        </em>
        ，选择一个位置来保存文件（在项目目录下的
        <em>
            Quotes
        </em>
        子目录是一个不错的地方），然后点击
        <em>
            Create
        </em>
        。
    </p>
    <p>
        现在打开
        <em>
            Main.storyboard
        </em>
        。展开
        <em>
            View Controller场景
        </em>
        并选择
        <em>
            View Controller
        </em>
        实例。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/QuotesViewController-scene.png
        " sl-processed="1 ">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/QuotesViewController-scene-480x106.png
            " alt=" " width="480 " height="106 " class="aligncenter size-medium wp-image-167064
            " srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/QuotesViewController-scene-480x106.png
            480w, https://koenig-media.raywenderlich.com/uploads/2017/07/QuotesViewController-scene-650x143.png
            650w " sizes="(max-width: 480px) 100vw, 480px ">
        </a>
    </p>
    <p>
        首选选择
        <em>
            Identity Inspector
        </em>
        并将Class修改为
        <code>
            QuotesViewController
        </code>
        ，将
        <em>
            Storyboard ID
        </em>
        设置为
        <code>
            QuotesViewController
        </code>
    </p>
    <p>
        下面添加下列的代码到
        <em>
            QuotesViewController.swift
        </em>
        的尾部
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">QuotesViewController</span> </span>{
  <span class="hljs-comment">// MARK: Storyboard instantiation</span>
  <span class="hljs-keyword">static</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">freshController</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">QuotesViewController</span> {
    <span class="hljs-comment">//1.</span>
    <span class="hljs-keyword">let</span> storyboard = <span class="hljs-type">NSStoryboard</span>(name: <span class="hljs-type">NSStoryboard</span>.<span class="hljs-type">Name</span>(rawValue: <span class="hljs-string">"Main"</span>), bundle: <span class="hljs-literal">nil</span>)
    <span class="hljs-comment">//2.</span>
    <span class="hljs-keyword">let</span> identifier = <span class="hljs-type">NSStoryboard</span>.<span class="hljs-type">SceneIdentifier</span>(rawValue: <span class="hljs-string">"QuotesViewController"</span>)
    <span class="hljs-comment">//3.</span>
    <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> viewcontroller = storyboard.instantiateController(withIdentifier: identifier) <span class="hljs-keyword">as</span>? <span class="hljs-type">QuotesViewController</span> <span class="hljs-keyword">else</span> {
      <span class="hljs-built_in">fatalError</span>(<span class="hljs-string">"Why cant i find QuotesViewController? - Check Main.storyboard"</span>)
    }
    <span class="hljs-keyword">return</span> viewcontroller
  }
}
</pre>
    <p>
        上述代码...
    </p>
    <ol>
        <li>
            获取到对
            <em>
                Main.storyboard
            </em>
            的引用。
        </li>
        <li>
            创建一个能够匹配你刚设定的identifier的
            <em>
                Scene identifier
            </em>
            。
        </li>
        <li>
            实例化
            <em>
                QuotesViewController
            </em>
            并返回。
        </li>
    </ol>
    <p>
        创建了这个方法之后，其它用到
        <code>
            QuotesViewController
        </code>
        的东西就不需要了解如何去实例化它了。直接调用它就阔以了:]
    </p>
    <p>
        注意位于
        <code>
            guard
        </code>
        语句中的
        <code>
            fatalError
        </code>
        。使用它或
        <code>
            assertionFailure
        </code>
        ，来让自己或团队其它的成员知晓这里出现了问题，是一个非常好的习惯。
    </p>
    <p>
        现在返回到
        <em>
            AppDelegate.swift
        </em>
        。添加一个新的property声明到类中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">let</span> popover = <span class="hljs-type">NSPopover</span>()
</pre>
    <p>
        现在，使用下列的方法替换
        <code>
            applicationDidFinishLaunching(\_:)
        </code>
        ：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">applicationDidFinishLaunching</span><span class="hljs-params">(<span class="hljs-number">_</span> aNotification: Notification)</span></span> {
  <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> button = statusItem.button {
    button.image = <span class="hljs-type">NSImage</span>(named:<span class="hljs-type">NSImage</span>.<span class="hljs-type">Name</span>(<span class="hljs-string">"StatusBarButtonImage"</span>))
    button.action = #selector(togglePopover(<span class="hljs-number">_</span>:))
  }
  popover.contentViewController = <span class="hljs-type">QuotesViewController</span>.freshController()
}
</pre>
    <p>
        现在你已把按钮的动作替换为
        <code>
            togglePopover(\_:)
        </code>
        ，接下来我们就会实现它，用popover去展示存在于QuotesViewController中的内容。
    </p>
    <p>
        添加下面的三个方法到
        <code>
            AppDelegate
        </code>
        中
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@objc</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">togglePopover</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: Any?)</span></span> {
  <span class="hljs-keyword">if</span> popover.isShown {
    closePopover(sender: sender)
  } <span class="hljs-keyword">else</span> {
    showPopover(sender: sender)
  }
}

<span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">showPopover</span><span class="hljs-params">(sender: Any?)</span></span> {
  <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> button = statusItem.button {
    popover.show(relativeTo: button.bounds, of: button, preferredEdge: <span class="hljs-type">NSRectEdge</span>.minY)
  }
}

<span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">closePopover</span><span class="hljs-params">(sender: Any?)</span></span> {
  popover.performClose(sender)
}
</pre>
    <p>
        <code>
            showPopover()
        </code>
        方法会向用户展示popover。你只需要提供一个源rect，macOS会基于此来展示popover和箭头，这样看起来popover就像是从菜单栏中的icon中弹出来的。
    </p>
    <p>
        <code>
            closePopover()
        </code>
        会把popover关闭掉，而
        <code>
            togglePopover()
        </code>
        则会基于当前的状态，来确定是打开还是关闭popover。
    </p>
    <p>
        运行项目，然后点击菜单栏中的icon，来查看展示空popover和关闭它的效果。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/show-QuotesViewController.png
        " sl-processed="1 ">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/show-QuotesViewController-480x292.png
            " alt=" " width="480 " height="292 " class="aligncenter size-medium wp-image-167065
            " srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/show-QuotesViewController-480x292.png
            480w, https://koenig-media.raywenderlich.com/uploads/2017/07/show-QuotesViewController-650x395.png
            650w, https://koenig-media.raywenderlich.com/uploads/2017/07/show-QuotesViewController.png
            1040w " sizes="(max-width: 480px) 100vw, 480px ">
        </a>
    </p>
    <p>
        你的popover已能够正常地工作，但那些令人鼓舞的内容在哪里？你看到的只有一个空空的view，没有名言。猜猜看接下来该做什么了？
    </p>
    <h2>
        实现Quote View Controller
    </h2>
    <p>
        首先，你需要一个model来储存名言和属性。点击
        <em>
            File/New/File…
        </em>
        并选择
        <em>
            macOS/Source/Swift File
        </em>
        模板，然后点击
        <em>
            Next
        </em>
        。将文件命名为
        <em>
            Quote
        </em>
        并点击
        <em>
            Create
        </em>
        。
    </p>
    <p>
        打开
        <em>
            Quote.swift
        </em>
        并添加下列代码到文件中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">struct</span> <span class="hljs-title">Quote</span> </span>{
  <span class="hljs-keyword">let</span> text: <span class="hljs-type">String</span>
  <span class="hljs-keyword">let</span> author: <span class="hljs-type">String</span>
  
  <span class="hljs-keyword">static</span> <span class="hljs-keyword">let</span> all: [<span class="hljs-type">Quote</span>] =  [
    <span class="hljs-type">Quote</span>(text: <span class="hljs-string">"Never put off until tomorrow what you can do the day after tomorrow."</span>, author: <span class="hljs-string">"Mark Twain"</span>),
    <span class="hljs-type">Quote</span>(text: <span class="hljs-string">"Efficiency is doing better what is already being done."</span>, author: <span class="hljs-string">"Peter Drucker"</span>),
    <span class="hljs-type">Quote</span>(text: <span class="hljs-string">"To infinity and beyond!"</span>, author: <span class="hljs-string">"Buzz Lightyear"</span>),
    <span class="hljs-type">Quote</span>(text: <span class="hljs-string">"May the Force be with you."</span>, author: <span class="hljs-string">"Han Solo"</span>),
    <span class="hljs-type">Quote</span>(text: <span class="hljs-string">"Simplicity is the ultimate sophistication"</span>, author: <span class="hljs-string">"Leonardo da Vinci"</span>),
    <span class="hljs-type">Quote</span>(text: <span class="hljs-string">"It’s not just what it looks like and feels like. Design is how it works."</span>, author: <span class="hljs-string">"Steve Jobs"</span>)
  ]
}

<span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">Quote</span>: <span class="hljs-title">CustomStringConvertible</span> </span>{
  <span class="hljs-keyword">var</span> description: <span class="hljs-type">String</span> {
    <span class="hljs-keyword">return</span> <span class="hljs-string">"\"<span class="hljs-subst">\(text)</span>\" — <span class="hljs-subst">\(author)</span>"</span>
  }
}
</pre>
    <p>
        上述代码定义了一个简单的名言结构体，其中包含一个静态的property来返回全部的名言。同时，你让
        <code>
            Quote
        </code>
        遵循
        <code>
            CustomStringConvertible
        </code>
        协议，这样你就能够很轻松地获得一个准备好的字符串。
    </p>
    <p>
        你已经取得了很大的进展，但你现在需要一些方法，来在UI中展示全部的名言。
    </p>
    <h3>
        设置View Controller的UI
    </h3>
    <p>
        打开
        <code>
            Main.storyboard
        </code>
        并拖拽三个
        <em>
            Push Button
        </em>
        ，一个
        <em>
            Multiline Label
        </em>
        到view controller中。
    </p>
    <p>
        把按钮和标签拖拽成就像下面的样子。蓝色的虚线会帮助你去定位到正确的位置去进行布局：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/layout-no-constraints.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/layout-no-constraints-480x304.png"
            alt="view controller layout" width="480" height="304" class="aligncenter size-medium wp-image-167083"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/layout-no-constraints-480x304.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/07/layout-no-constraints-650x412.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/07/layout-no-constraints.png 1118w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        你可以独自完成添加自动布局的约束，来适配用户的交互么？在查看下面的详解之前，可以首先自己进行一下尝试。如果成功的话，就可以略过下面这部分了，你可以直接奖励给自己一颗星星。
    </p>
    <h3>
        解决方案
    </h3>
    <p>
        下列是获取正确布局所需的约束：
    </p>
    <li>
        将左侧的按钮固定到距左边20，且竖直居中的位置。
    </li>
    <li>
        将右侧的按钮固定到距右边20，且竖直居中的位置。
    </li>
    <li>
        将底部的按钮固定到距底部20，且水平居中的位置。
    </li>
    <li>
        将标签固定到距离左右两边均为20，且竖直居中的位置。
    </li>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/final-layout-show-constraints.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/final-layout-show-constraints-480x292.png"
            alt="constraints for layout" width="480" height="292" class="aligncenter size-medium wp-image-167067"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/final-layout-show-constraints-480x292.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/07/final-layout-show-constraints-650x396.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/07/final-layout-show-constraints.png 1110w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        你会发现出现了一些布局的错误，因为没有足够的信息以确定布局。
    </p>
    <p>
        因此将label的
        <em>
            Horizontal Content Hugging Priority
        </em>
        设置为249，以允许label恰当地增长。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/conflict-resolution.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/conflict-resolution-480x192.png"
            alt="resolve constraint conflicts" width="480" height="192" class="aligncenter size-medium wp-image-167068"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/conflict-resolution-480x192.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/07/conflict-resolution-650x260.png 650w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        在得到满意的布局之后：
    </p>
    <ul>
        <li>
            设置左侧按钮的图片为
            <code>
                NSGoLeftTemplate
            </code>
            ，并删除title。
        </li>
        <li>
            设置右侧按钮的图片为
            <code>
                NSGoRightTemplate
            </code>
            ，并删除title。
        </li>
        <li>
            设置下侧按钮的title为
            <em>
                Quit Quotes
            </em>
            。
        </li>
        <li>
            设置label的对齐方式为居中对齐。
        </li>
        <li>
            设置label的
            <em>
                Line Break
            </em>
            模式为
            <em>
                Word Wrap
            </em>
            。
        </li>
    </ul>
    <p>
        现在，打开
        <em>
            QuotesViewController.swift
        </em>
        ，并添加下列的代码到
        <code>
            QuotesViewController
        </code>
        类的实现中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@IBOutlet</span> <span class="hljs-keyword">var</span> textLabel: <span class="hljs-type">NSTextField</span>!
</pre>
    <p>
        添加下列的extension到类的实现之后。现在在
        <em>
            QuotesViewController.swift
        </em>
        中你会有两个extension。
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-comment">// MARK: Actions</span>

<span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">QuotesViewController</span> </span>{
  <span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">previous</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: NSButton)</span></span> {
  }

  <span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">next</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: NSButton)</span></span> {
  }

  <span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">quit</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: NSButton)</span></span> {
  }
}
</pre>
    <p>
        你现在已为label添加了一个outlet，你将会用这个label来展示鼓舞人心的名言。还添加了三个动作，你将把它们分别连接到三个按钮上。
    </p>
    <h3>
        将代码连接到Interface Builder上
    </h3>
    <p>
        你会注意到源码编辑器的左侧已出现了一些小小的圆形。只要你使用
        <code>
            @IBAction
        </code>
        和
        <code>
            @IBOutlet
        </code>
        关键字，这些原型就会出现。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/IB-handles.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/IB-handles-340x320.png"
            alt="" width="340" height="320" class="aligncenter size-medium wp-image-167069"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/IB-handles-340x320.png 340w, https://koenig-media.raywenderlich.com/uploads/2017/07/IB-handles-532x500.png 532w, https://koenig-media.raywenderlich.com/uploads/2017/07/IB-handles.png 972w"
            sizes="(max-width: 340px) 100vw, 340px">
        </a>
    </p>
    <p>
        现在，你就会使用它们来将代码和UI进行连接。
    </p>
    <p>
        在project navigator中按住
        <em>
            alt
        </em>
        点击
        <em>
            Main.storyboard
        </em>
        ，就会把storyboard打开到Assistant Editor的右侧，而源码位于左侧。
    </p>
    <p>
        拖拽靠近
        <code>
            textLabel
        </code>
        的小圆形到interface builder中的label上。并用相同的方式把previous，next和quit动作连接到相应的按钮上。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/connect-outlets.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/connect-outlets-480x300.png"
            alt="" width="480" height="300" class="aligncenter size-medium wp-image-167070"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/connect-outlets-480x300.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/07/connect-outlets-650x406.png 650w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <div class="note">
        <p>
            <em>
                注意
            </em>
            ：如果你在上面的步骤中遇到了困难，请参考我们的
            <a href="https://www.raywenderlich.com/category/macos" target="_blank"
            title="macOS tutorials" sl-processed="1">
                macOS教程
            </a>
            ，你会在这里找到macOS开发的引导性的教程，涉及到其中的方方面面，包括在interface builder中添加view和约束，以及连接outlets和actions。
        </p>
    </div>
    <p>
        站起来伸一下懒腰吧，做一个胜利的手势，你已成功地完成了一堆interface builder的工作。
    </p>
    <p>
        运行项目，你的popover现在应该看起来是下面这个样子了：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/ui-completed.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/ui-completed-480x245.png"
            alt="" width="480" height="245" class="aligncenter size-medium wp-image-167071"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/ui-completed-480x245.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/07/ui-completed-650x332.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/07/ui-completed.png 1002w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        你对上面的popover采取了view controller的默认尺寸。如果你想要一个更小或更大的popover，只需在storyboard中调整view controller即可。
    </p>
    <p>
        关于交互的部分现在已完成了，但还并没有实现。这些按钮现在正等着你去实现，当你点击它们的时候，该做些什么事情 - 不要把它们挂在那里。
    </p>
    <h2>
        为按钮创建动作
    </h2>
    <p>
        如果你尚未使用
        <em>
            Cmd-Return
        </em>
        或
        <em>
            View &gt; Standard Editor &gt; Show Standard Editor
        </em>
        来关闭Assistant Editor
    </p>
    <p>
        打开
        <em>
            QuotesViewController.swift
        </em>
        并添加下列的property到类的实现中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">let</span> quotes = <span class="hljs-type">Quote</span>.all

<span class="hljs-keyword">var</span> currentQuoteIndex: <span class="hljs-type">Int</span> = <span class="hljs-number">0</span> {
  <span class="hljs-keyword">didSet</span> {
    updateQuote()
  }
}
</pre>
    <p>
        <code>
            quotes
        </code>
        property会持有所有的名言，而
        <code>
            currentQuoteIndex
        </code>
        则持有着当前的名言。
        <code>
            currentQuoteIndex
        </code>
        同时会作为一个property的观察器，他会在序号发生变化的时候，使用新的名言来更新文本标签。
    </p>
    <p>
        接下来，添加下列的方法到类中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">override</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">viewDidLoad</span><span class="hljs-params">()</span></span> {
  <span class="hljs-keyword">super</span>.viewDidLoad()
  currentQuoteIndex = <span class="hljs-number">0</span>
}

<span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">updateQuote</span><span class="hljs-params">()</span></span> {
  textLabel.stringValue = <span class="hljs-type">String</span>(describing: quotes[currentQuoteIndex])
}
</pre>
    <p>
        当这个view被加载的时候，你就会把当前名言的序号设置为0，相应地来更新UI。
        <code>
            updateQuote()
        </code>
        会根据
        <code>
            currentQuoteIndex
        </code>
        确定的当前选择的名言来更新文本的标签。
    </p>
    <p>
        要把它们到绑定到一起，更新三个方法，就像下面这样：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">previous</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: NSButton)</span></span> {
  currentQuoteIndex = (currentQuoteIndex - <span class="hljs-number">1</span> + quotes.<span class="hljs-built_in">count</span>) % quotes.<span class="hljs-built_in">count</span>
}

<span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">next</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: NSButton)</span></span> {
  currentQuoteIndex = (currentQuoteIndex + <span class="hljs-number">1</span>) % quotes.<span class="hljs-built_in">count</span>
}

<span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">quit</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: NSButton)</span></span> {
  <span class="hljs-type">NSApplication</span>.shared.terminate(sender)
}
</pre>
    <p>
        在
        <code>
            next()
        </code>
        和
        <code>
            previous()
        </code>
        中，你会循环遍历全部的名言。而
        <code>
            quit
        </code>
        则会退出当前的app。
    </p>
    <p>
        再次运行项目，
        <i>
            现在
        </i>
        你就可以循环地浏览名言及退出app了！
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/code-connected.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/code-connected-480x267.png"
            alt="final UI" width="480" height="267" class="aligncenter size-medium wp-image-167074"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/code-connected-480x267.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/07/code-connected-650x361.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/07/code-connected.png 964w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <h2>
        事件监听
    </h2>
    <p>
        你的用户会在你小小的谦逊的菜单栏app上期待一个特性，就是当你点击app之外的任何地方，让popover自动地关闭。
    </p>
    <p>
        菜单栏的app应当在点击它的时候打开UI，而当用户移动到下一个项目的时候就消失。因此，你需要一个macOS的全局事件监听器。
    </p>
    <p>
        接下来我们就会创建一个时间监听器，它可以复用到你所有的项目上，例如当展示popover的时候就可以用到它。
    </p>
    <p>
        我赌你早已变得更聪明了！
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/07/osx-triumphant-1-320x320.png"
        alt="" width="320" height="320" class="aligncenter size-medium wp-image-167085"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/07/osx-triumphant-1-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2017/07/osx-triumphant-1-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2017/07/osx-triumphant-1-500x500.png 500w, https://koenig-media.raywenderlich.com/uploads/2017/07/osx-triumphant-1-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2017/07/osx-triumphant-1-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2017/07/osx-triumphant-1-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2017/07/osx-triumphant-1-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2017/07/osx-triumphant-1-128x128.png 128w, https://koenig-media.raywenderlich.com/uploads/2017/07/osx-triumphant-1.png 1000w"
        sizes="(max-width: 320px) 100vw, 320px">
    </p>
    <p>
        创建一个Swift文件并将它命名为
        <em>
            EventMonitor
        </em>
        ，然后用下列的类定义来替换它的内容：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">import</span> Cocoa

<span class="hljs-keyword">public</span> <span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">EventMonitor</span> </span>{
  <span class="hljs-keyword">private</span> <span class="hljs-keyword">var</span> monitor: <span class="hljs-type">Any</span>?
  <span class="hljs-keyword">private</span> <span class="hljs-keyword">let</span> mask: <span class="hljs-type">NSEvent</span>.<span class="hljs-type">EventTypeMask</span>
  <span class="hljs-keyword">private</span> <span class="hljs-keyword">let</span> handler: (<span class="hljs-type">NSEvent</span>?) -&gt; <span class="hljs-type">Void</span>

  <span class="hljs-keyword">public</span> <span class="hljs-keyword">init</span>(mask: <span class="hljs-type">NSEvent</span>.<span class="hljs-type">EventTypeMask</span>, handler: @escaping (<span class="hljs-type">NSEvent</span>?) -&gt; <span class="hljs-type">Void</span>) {
    <span class="hljs-keyword">self</span>.mask = mask
    <span class="hljs-keyword">self</span>.handler = handler
  }

  <span class="hljs-keyword">deinit</span> {
    stop()
  }

  <span class="hljs-keyword">public</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">start</span><span class="hljs-params">()</span></span> {
    monitor = <span class="hljs-type">NSEvent</span>.addGlobalMonitorForEvents(matching: mask, handler: handler)
  }

  <span class="hljs-keyword">public</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">stop</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">if</span> monitor != <span class="hljs-literal">nil</span> {
      <span class="hljs-type">NSEvent</span>.removeMonitor(monitor!)
      monitor = <span class="hljs-literal">nil</span>
    }
  }
}
</pre>
    <p>
        你会通过传递一个待监听事件类型的标记来初始化这个类的实例 - 事件诸如按键，滚动鼠标，单击左键等 - 以及一个事件处理者。
    </p>
    <p>
        当你准备好开始监听的时候，
        <code>
            start()
        </code>
        就会调用
        <code>
            addGlobalMonitorForEventsMatchingMask(\_:handler:)
        </code>
        ，它会返回一个可以让你持有的对象。任何时候只有指定的事件发生，系统就会调用你的处理方法。
    </p>
    <p>
        要移除全局事件的监听器，可以调用
        <code>
            stop()
        </code>
        中的
        <code>
            removeMonitor()
        </code>
        方法，并通过将其设置为nil，删除返回的对象。
    </p>
    <p>
        现在剩下的工作，就只有在需要的时候调用
        <code>
            start()
        </code>
        和
        <code>
            stop()
        </code>
        方法了。是不是很容易？当然这个类也会在它的析构器中调用
        <code>
            stop()
        </code>
        方法来实现清理自己。
    </p>
    <h3>
        连接事件监听器
    </h3>
    <p>
        最后一次打开
        <em>
            AppDelegate.swift
        </em>
        ，并为其添加一个新的property声明：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">var</span> eventMonitor: <span class="hljs-type">EventMonitor</span>?
</pre>
    <p>
        然后，在
        <code>
            applicationDidFinishLaunching(\_:)
        </code>
        的尾部添加下列代码来配置事件监听器：
    </p>
    <pre lang="swift" class="language-swift hljs">eventMonitor = <span class="hljs-type">EventMonitor</span>(mask: [.leftMouseDown, .rightMouseDown]) { [<span class="hljs-keyword">weak</span> <span class="hljs-keyword">self</span>] event <span class="hljs-keyword">in</span>
  <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> strongSelf = <span class="hljs-keyword">self</span>, strongSelf.popover.isShown {
    strongSelf.closePopover(sender: event)
  }
}
</pre>
    <p>
        上述代码会监听系统的鼠标左键和有件按下的事件，当这些事件发生的时候，就会将popover关闭。注意，发送到你的自己app上的事件，这里是不会响应的。这就是为何当你点击popover中的内容时，它并不会消失的原因。:]
    </p>
    <p>
        你使用了一个指向self的
        <code>
            weak
        </code>
        引用以避免
        <code>
            AppDelegate
        </code>
        和
        <code>
            EventMonitor
        </code>
        之间潜在的
        <i>
            循环引用
        </i>
        。在本例中它并非是必要的，因为这里只有一次循环，但这却是一个值得在你自己的代码中关注的地方，尤其是你在两个对象之间使用block处理回调的时候。
    </p>
    <p>
        添加下列的代码到
        <code>
            showPopover(\_:)
        </code>
        的尾部：
    </p>
    <pre lang="swift" class="language-swift hljs">eventMonitor?.start()
</pre>
    <p>
        这样就会在popover出现的时候启动事件监听器。
    </p>
    <p>
        然后添加下列的代码到
        <code>
            closePopover(\_:)
        </code>
        的尾部：
    </p>
    <pre lang="swift" class="language-swift hljs">eventMonitor?.stop()
</pre>
    <p>
        这样当popover关闭的时候，就会停止事件监听器的监听。
    </p>
    <p>
        全部都搞定了！再次运行项目。点击菜单栏的icon来展示popover，然后点击外面的任意地方来关闭它。Awesome！
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
        这里是
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/07/Quotes_final-s4b3.zip"
        sl-processed="1">
            最终的项目
        </a>
        ，包含了上述教程中你所开发的所有的代码。
    </p>
    <p>
        你已经明白了如何在你菜单栏的status items上设置菜单和popovers –&nbsp;为何不尝试下使用属性字符创或多个label来美化名言，或是连接web的后端来拉群新的名言。也许你还可以找到使用键盘快捷键去循环浏览名言的方法。
    </p>
    <p>
        一个寻找其它可能性的很棒的地方，就是阅读苹果的官方文档，如
        <a href="https://developer.apple.com/documentation/appkit/nsmenu" target="_blank"
        sl-processed="1">
            <code>
                NSMenu
            </code>
        </a>
        ，
        <a href="https://developer.apple.com/documentation/appkit/nspopover" target="_blank"
        sl-processed="1">
            <code>
                NSPopover
            </code>
        </a>
        和
        <a href="https://developer.apple.com/documentation/appkit/nsstatusitem"
        target="_blank" sl-processed="1">
            <code>
                NSStatusItem
            </code>
        </a>
        。
    </p>
    <p>
        需要考虑的一件事是你希望你的用户把你的app当做一个非常珍贵的屏幕上的不动产，因此当你感觉在状态栏上有一个item很酷的时候，可能你的用户并不这么认为。很多的app会提供偏好选项来让用户确定是打开还是隐藏这个item。你可以把它作为自己的一个进阶的练习。
    </p>
    <p>
        感谢你抽出时间来学习如何为macOS打造一个很酷的popover菜单的app。它相当得简单，但可以看出来，你所学到的这些概念将会成为你开发各种app的绝佳基础。
    </p>
</div>