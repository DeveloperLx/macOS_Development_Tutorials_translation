# macOS X 初学者开发教程 第一部分 Xcode介绍

#### [原文地址](https://www.raywenderlich.com/110170/mac-os-x-development-tutorial-for-beginners-part-1-intro-to-xcode) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
    	想要学习怎么使用Swift为你的Mac开发App？
        <img class="alignright size-full wp-image-110249 bordered" src="https://koenig-media.raywenderlich.com/uploads/2015/07/250x250.png"
        alt="250x250" width="250" height="250" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2015/07/250x250-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/07/250x250-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2015/07/250x250-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2015/07/250x250-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
        
    </p>
    <p>
        好消息 - 苹果让为OS X开发难以置信得容易 - 我们将在这个教程中展示给你。你讲学到怎么创建你的第一个OS X app - 即使你完全就是个初学者。
    </p>
    <ol>
        <li>在第一部分，你将首次怎么获取你需要的OS X开发的工具。然后，使用你下载的app作为例子，你将进行一次Xcode的旅行，发现怎么运行一个App，编辑代码，设计UI，debug程序。
        </li>
        <li>在<a href="http://www.raywenderlich.com/110267/mac-os-x-development-tutorial-for-beginners-part-2-os-x-app-anatomy"
            sl-processed="1">第二部分</a>，你将从Xcode挪步到了解构成一个OS X app的组成部分。从一个app怎么启动，到UI怎么构建，再到怎么控制交互。
        </li>
        <li>在<a href="http://www.raywenderlich.com/110269/mac-os-x-development-tutorial-for-beginners-part-3-your-first-os-x-app"
            sl-processed="1">最后一部分</a>， 你将亲自动手（get your hands dirty）- 构建你史无前例的第一个OS X app。从一无所有开始，你将很快地拥有一个简单的app，并运行在你的mac上！
        </li>
    </ol>
    <p>
        所以你还在等什么？桌面app的世界等着你！
    </p>
    <div class="note">
        <p>
            <em>
            	注意：
            </em>
            这里有一些从哪里开始这个系列的指导：
        </p>
        <ul>
            <li>
                <em>
                	如果你是Swift的新手
                </em>
                ，这个系列要求Swift的知识，所以首先点击我们的
                <a href="http://www.raywenderlich.com/category/swift" sl-processed="1">
                	Swift教程
                </a>
                ，来获取一个不错的介绍。
            </li>
            <li>
                <em>
                	如果你早就有了iOS的经验
                    If you already have iOS experience
                </em>
                ，这个系列的第一部分将是回顾。快速地浏览主题来确认你已掌握，然后直接跳到这个系列的<a href="http://www.raywenderlich.com/110267/mac-os-x-development-tutorial-for-beginners-part-2-os-x-app-anatomy"
                sl-processed="1">下一部分</a>。
            </li>
            <li>
                <em>
                    否则
                </em>
                ，保持继续阅读 - 这个系列是面对完全的初学者 - 不要求有过开发iOS或OS X经验。
            </li>
        </ul>
    </div>
    <h2>
    	预备条件
    </h2>
    <p>
    	要变成一个OS X的开发者，你需要这些东西：
    </p>
    <ul>
        <li>
            <em>
            	运行OS X的Mac。
            </em>
            OS X操作系统只能在苹果电脑上运行，因此你需要一个Mac来开发和运行OS X app。如果你困惑该买哪个Mac，我们推荐Mac mini搭配额外的内存和固态或融合的驱动；这是对于费用和性能的最佳平衡。
        </li>
        <li>
            <em>
                一个AppleID。
            </em>
            为了从App Store下载开发工具，你需要有一个AppleID。
        </li>
        <li>
            <em>
                Xcode。
            </em>
            它是用来创建OS X app的集成开发环境和工具链。你会在下一个部分学到如何安装它。
        </li>
    </ul>
    <p>
    	一旦你构建好了你的app，你想把它上传到App Store并发布，你就需要去买一个苹果开发者账号。但在你准备发送你的app到全世界前，这都不是必须的。
    </p>
    <h2>
        获取工具
    </h2>
    <p>
        不像一些其它的平台，开发OS X只要求安装一个工具-就是我们所知的Xcode。Xcode是一个包含所有开发iOS，watchOS和OS X app所需的集成开发环境。
    </p>
    <p>
        如果你还没有Xcode，点击你菜单栏左上角的Apple icon图标，选择
        <em>
            App Store
        </em>
        来打开Mac App商店。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/AppStore21.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-112234 bordered" src="https://koenig-media.raywenderlich.com/uploads/2015/08/AppStore21.png"
            alt="AppStore2" width="263" height="261" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/AppStore21.png 263w, https://koenig-media.raywenderlich.com/uploads/2015/08/AppStore21-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/08/AppStore21-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2015/08/AppStore21-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2015/08/AppStore21-128x128.png 128w"
            sizes="(max-width: 263px) 100vw, 263px">
        </a>
    </p>
    <p>
        搜索Xcode，然后下载它：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110235 bordered" src="https://koenig-media.raywenderlich.com/uploads/2015/07/xcode_mas-679x500.png"
        alt="xcode_mas" width="679" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/xcode_mas-679x500.png 679w, https://koenig-media.raywenderlich.com/uploads/2015/07/xcode_mas-435x320.png 435w"
        sizes="(max-width: 679px) 100vw, 679px">
    </p>
    <p>
        下载和安装好它之后，从你的Applications目录下打开Xcode。第一次打开Xcode时，它会请求你安装一些额外的组件。让它安装，并输入你的密码如果它要求的话。
    </p>
    <p>
       接下来你会看到Xcode的欢迎界面：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110236" src="https://koenig-media.raywenderlich.com/uploads/2015/07/xocde_welcome-480x289.png"
        alt="xocde_welcome" width="480" height="289" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/xocde_welcome-480x289.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/xocde_welcome-700x422.png 700w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        恭喜你成功地安装了Xcode！继续阅读，学习它可以做什么。
    </p>
    <h3>
    	Beta版本的Xcode
    </h3>
    <p>
    	在继续描述Xcode的强大之前，值得花几分钟了解一下Beta版本的Xcode。
    </p>
    <p>
    	当苹果发布Xcode新的更新时（常常支持新的OS X，iOS和watchOS特性），会通过发布一轮激进（agressive）的beta版本。这些发布包括新的特性，但因而也会有很多bug。如果你感兴趣于开发利用这些新特性的app，你需要从苹果下载最新beta版的Xcode。
    </p>
    <p>
        This tutorial requires Xcode 7, since the sample project used in this
        tutorial has been updated to the Swift 2.0 programming language. There
        are two cases:
    </p>
    <ul>
        <li>
            <em>
                If the App Store version of Xcode is Xcode 7 at the time of reading this
                tutorial
            </em>
            , you are all set!
        </li>
        <li>
            <em>
                If the App Store version of Xcode is Xcode 6 at the time of reading this
                tutorial
            </em>
            , you’ll need to install a beta version of Xcode 7 – keep reading to learn
            how.
        </li>
    </ul>
    <p>
        To get the latest beta version of Xcode, visit
        <a href="https://developer.apple.com/" sl-processed="1">
            developer.apple.com
        </a>
        , click on
        <em>
            Resources
        </em>
        ,
        <em>
            Xcode
        </em>
        , and then
        <em>
            Download
        </em>
        . Follow the link to download the latest version of Xcode beta there.
    </p>
    <p>
        Note you can install a beta version of Xcode alongside the stable version,
        so there’s no problem with continuing work on projects that aren’t ready
        for upgrade.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/XcodeBeta.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112238 bordered" src="https://koenig-media.raywenderlich.com/uploads/2015/08/XcodeBeta-700x356.png"
            alt="XcodeBeta" width="700" height="356" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/XcodeBeta-700x356.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/XcodeBeta-480x244.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/XcodeBeta.png 1099w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        The download is a DMG, so you can install by dragging the Xcode app across
        into
        <em>
            Applications
        </em>
        in the usual way. You’ll then have two versions of Xcode in your applications
        folder:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/2Xcode.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-112242" src="https://koenig-media.raywenderlich.com/uploads/2015/08/2Xcode.png"
            alt="2Xcode" width="256" height="124">
        </a>
    </p>
    <p>
        Run
        <em>
            Xcode-beta
        </em>
        and then you’re ready to continue on!
    </p>
    <h2>
        Hello World!
    </h2>
    <p>
        Xcode is an Integrated Development Environment (IDE) which means that
        it is a collection of all the tools you need, from source code editing,
        compilation through to debugging and UI design.
    </p>
    <p>
        When you open Xcode it allows you to create a new project, or open an
        existing one. You can also open an existing project by double clicking
        on an Xcode project or workspace in Finder:
    </p>
    <p>
        <img class="aligncenter wp-image-110225 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/07/open_finder-480x269.png"
        alt="open_finder" width="480" height="269" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/open_finder-480x269.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/open_finder-700x393.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/open_finder.png 1052w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <h3>
        Creating a new app
    </h3>
    <p>
        For most of this tutorial you’ll tour Xcode via a sample app, but first
        things first – you can’t start learning about a new platform without first
        creating a “Hello World” app!
    </p>
    <p>
        To do this, select
        <em>
            Create a new Xcode project
        </em>
        from the Xcode welcome screen:
    </p>
    <p>
        <img class="aligncenter wp-image-110236 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/07/xocde_welcome-480x289.png"
        alt="xocde_welcome" width="480" height="289" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/xocde_welcome-480x289.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/xocde_welcome-700x422.png 700w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        The template chooser allows you to decide how Xcode will configure your
        new project. In the
        <em>
            OS X
        </em>
        <em>
            \
        </em>
        <em>
            Application
        </em>
        section you can see the three different core OS X app types:
    </p>
    <p>
        <img class="aligncenter wp-image-110224 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/07/new_project-451x320.png"
        alt="new_project" width="451" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/new_project-451x320.png 451w, https://koenig-media.raywenderlich.com/uploads/2015/07/new_project-700x496.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/new_project.png 1464w"
        sizes="(max-width: 451px) 100vw, 451px">
    </p>
    <p>
        The three different app types are as follows:
    </p>
    <ul>
        <li>
            <em>
                Cocoa Application
            </em>
            : An OS X desktop app – with a window-based UI. Cocoa is the name of the
            framework upon which all OS X applications are built.
        </li>
        <li>
            <em>
                Game
            </em>
            : Games built using Apple’s SpriteKit or SceneKit frameworks.
        </li>
        <li>
            <em>
                Command Line Tool
            </em>
            : A utility that runs in a shell, and has a text-based UI.
        </li>
    </ul>
    <p>
        Select
        <em>
            Cocoa Application
        </em>
        , and click
        <em>
            Next
        </em>
        . On the screen that follows, set the
        <em>
            Product Name
        </em>
        to
        <em>
            HelloWorld
        </em>
        , check the language is set to
        <em>
            Swift
        </em>
        and that
        <em>
            Use Storyboards
        </em>
        is checked:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110277" src="https://koenig-media.raywenderlich.com/uploads/2015/07/new_project1-450x320.png"
        alt="new_project" width="450" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/new_project1-450x320.png 450w, https://koenig-media.raywenderlich.com/uploads/2015/07/new_project1-700x497.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/new_project1.png 1464w"
        sizes="(max-width: 450px) 100vw, 450px">
    </p>
    <p>
        Click
        <em>
            Next
        </em>
        , and choose a location on disk to save your project.
    </p>
    <p>
        This creates a new, empty project ready for you to craft into your amazing
        app. The first thing you’ll want to do is build and run it to check that
        it’s all working.
    </p>
    <h3>
        Running your app
    </h3>
    <p>
        Whether you’ve opened an existing app or created a new one, the most important
        thing you’ll want to do is to build and run it.
    </p>
    <p>
        This involves compiling all of the code you’ve written into machine code,
        bundling up the resources required by the app and then executing it. This
        process is complex, but luckily Xcode has your back. To build and run your
        project simply press the
        <em>
            play
        </em>
        button on the toolbar:
    </p>
    <p>
        <img class="aligncenter wp-image-110281 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/07/play_button1-480x124.png"
        alt="" width="480" height="124" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/play_button1-480x124.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/play_button1.png 534w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        You can also build and run your app with the
        <em>
            ⌘R
        </em>
        keyboard shortcut.
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110284" src="https://koenig-media.raywenderlich.com/uploads/2015/07/bar_empty-480x292.png"
        alt="bar_empty" width="480" height="292" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/bar_empty-480x292.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/bar_empty-700x426.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/bar_empty.png 962w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        The first time you ever build and run an app in Xcode, you might well
        be asked whether you want to
        <em>
            Enable Developer Mode on this Mac?
        </em>
        . You’re safe to select
        <em>
            Enable
        </em>
        , at which point you may have to enter your password. Developer mode allows
        Xcode to attach a debugger to running processes – which will be extremely
        useful when building your application!
    </div>
    <p>
        Your
        <em>
            HelloWorld
        </em>
        app is currently looking a bit empty – and doesn’t even say hello! You’re
        going to fix that now.
    </p>
    <h3>
        Adding Text
    </h3>
    <p>
        You’re going to update the user interface (UI) of your app to make it
        into a true “Hello World” app, and to do this you’re going to use a tool
        called Interface Builder (IB). You’ll learn much more about Interface Builder
        later in this tutorial – for now, you&nbsp;just need to know enough to
        add some text to the layout.
    </p>
    <p>
        Find the
        <em>
            Main.storyboard
        </em>
        file in the
        <em>
            Project Navigator
        </em>
        , and click on it:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110287" src="https://koenig-media.raywenderlich.com/uploads/2015/07/open_storyboard-294x320.png"
        alt="open_storyboard" width="294" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/open_storyboard-294x320.png 294w, https://koenig-media.raywenderlich.com/uploads/2015/07/open_storyboard-459x500.png 459w, https://koenig-media.raywenderlich.com/uploads/2015/07/open_storyboard.png 518w"
        sizes="(max-width: 294px) 100vw, 294px">
    </p>
    <p>
        This opens the storyboard file in Interface Builder – you can see an outline
        of your entire app:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110288" src="https://koenig-media.raywenderlich.com/uploads/2015/07/hello_world_storyboard-343x500.png"
        alt="hello_world_storyboard" width="343" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/hello_world_storyboard-343x500.png 343w, https://koenig-media.raywenderlich.com/uploads/2015/07/hello_world_storyboard-219x320.png 219w, https://koenig-media.raywenderlich.com/uploads/2015/07/hello_world_storyboard.png 602w"
        sizes="(max-width: 343px) 100vw, 343px">
    </p>
    <p>
        The lower component (entitled “View Controller”) represents the visual
        appearance of your app. You’re going to add a text label to this to create
        your “Hello World” app.
    </p>
    <p>
        Find the
        <em>
            Object Library
        </em>
        in the lower right part of the Xcode window. Type
        <em>
            label
        </em>
        into the search box and locate the
        <em>
            Label
        </em>
        entry:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110291" src="https://koenig-media.raywenderlich.com/uploads/2015/07/object_library-330x320.png"
        alt="object_library" width="330" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/object_library-330x320.png 330w, https://koenig-media.raywenderlich.com/uploads/2015/07/object_library-516x500.png 516w, https://koenig-media.raywenderlich.com/uploads/2015/07/object_library-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/07/object_library.png 520w"
        sizes="(max-width: 330px) 100vw, 330px">
    </p>
    <p>
        <em>
            Drag
        </em>
        a label from the
        <em>
            Object Library
        </em>
        onto the empty
        <em>
            View Controller
        </em>
        scene canvas:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110292" src="https://koenig-media.raywenderlich.com/uploads/2015/07/drag_label-480x312.png"
        alt="drag_label" width="480" height="312" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/drag_label-480x312.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/drag_label-700x455.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/drag_label.png 1022w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        A label represents a static piece of text – with no user interaction –
        perfect for your Hello World app. You don’t want it to say “label” though
        – you’re going to update that next.
    </p>
    <p>
        To configure the label, select it and then open the
        <em>
            Attributes Inspector
        </em>
        (the 4th tab) on the right hand side of the Xcode window. Set the
        <em>
            title
        </em>
        to
        <em>
            “Hello OS X!”
        </em>
        , and update the
        <em>
            font
        </em>
        to be
        <em>
            size 40
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110294" src="https://koenig-media.raywenderlich.com/uploads/2015/07/label_config-296x320.png"
        alt="label_config" width="296" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/label_config-296x320.png 296w, https://koenig-media.raywenderlich.com/uploads/2015/07/label_config-462x500.png 462w, https://koenig-media.raywenderlich.com/uploads/2015/07/label_config.png 516w"
        sizes="(max-width: 296px) 100vw, 296px">
    </p>
    <p>
        You may see that the label is no longer sized correctly – next you’ll
        fix that and set it to the correct position.
    </p>
    <p>
        You position UI elements in OS X using a system called Auto Layout – which
        allows you to specify positions and sizes of UI elements in terms of their
        relationships. You want to put your “Hello OS X!” label in the center of
        the window – so you’re going to add constraints to achieve this.
    </p>
    <p>
        Select the label once again, and click the
        <em>
            Align
        </em>
        button in the bottom bar (the second from the left). Check both the
        <em>
            Horizontally in Container
        </em>
        and the
        <em>
            Vertically in Container
        </em>
        boxes, and ensure that they are both
        <em>
            set to 0
        </em>
        . Select
        <em>
            Items of New Constraints
        </em>
        in the
        <em>
            Update Frames
        </em>
        selection box before finally clicking the
        <em>
            Add 2 Constraints button
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110297" src="https://koenig-media.raywenderlich.com/uploads/2015/07/constraints-413x320.png"
        alt="constraints" width="413" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/constraints-413x320.png 413w, https://koenig-media.raywenderlich.com/uploads/2015/07/constraints-645x500.png 645w, https://koenig-media.raywenderlich.com/uploads/2015/07/constraints.png 1016w"
        sizes="(max-width: 413px) 100vw, 413px">
    </p>
    <p>
        This will update the storyboard to position and size your label correctly.
    </p>
    <p>
        Build and run your app (either by clicking the play button, or using the&nbsp;
        <em>
            ⌘R
        </em>
        keyboard shortcut) to see your “Hello World!” Mac OS X app:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110300" src="https://koenig-media.raywenderlich.com/uploads/2015/07/hello_osx-480x293.png"
        alt="hello_osx" width="480" height="293" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/hello_osx-480x293.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/hello_osx-700x428.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/hello_osx.png 962w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <h2>
        Introducing HubEvent
    </h2>
    <p>
        You’ll continue learning how to make projects from scratch and code OS
        X apps in later parts of this series, but for the rest of this tutorial
        you’ll focus on learning more about Xcode itself.
    </p>
    <p>
        To help with that, I’ve created a sample project for you called
        <em>
            HubEvent
        </em>
        that you’ll work with for the rest of this tutorial. This way you can
        get a tour of Xcode with a real-world project.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/HubEvent_7.1.zip"
        sl-processed="1">
            Download
        </a>
        the
        <em>
            HubEvent
        </em>
        &nbsp;starter project, unzip it and
        <em>
            double click
        </em>
        on
        <em>
            HubEvent\HubEvent.xcodeproj
        </em>
        in Finder to open it in Xcode.
    </p>
    <p>
        Build and run
        <em>
            HubEvent
        </em>
        sample project and you’ll see it compile and then launch:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110220" src="https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent-613x500.png"
        alt="hubevent" width="613" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent-613x500.png 613w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent-392x320.png 392w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent.png 1071w"
        sizes="(max-width: 613px) 100vw, 613px">
    </p>
    <p>
        HubEvent uses the public GitHub API to pull down all the events for a
        user, and displays a summary of them in a table. As you select each row
        of the table, the raw JSON associated with that event is displayed in the
        panel below.
    </p>
    <h2>
        Xcode Core Functionality
    </h2>
    <p>
        HubEvent&nbsp;is a fairly simple app, but is complex enough to demonstrate
        the core functionality of Xcode. The remainder of this tutorial will cover
        the following:
    </p>
    <ul>
        <li>
            <em>
                Code Editor.
            </em>
            All OS X apps have a code component, and HubEvent is no different. The
            code in HubEvent is responsible for downloading the data from the GitHub
            API, and wiring it up to the user interface.
        </li>
        <li>
            <em>
                Interface Builder.
            </em>
            You’ve already used Interface Builder when you build your “Hello World!”
            app. You’ll learn more about how this powerful tool allows you to build
            up the split-window UI used in
            <em>
                HubEvent
            </em>
            .
        </li>
        <li>
            <em>
                Asset Catalog.
            </em>
            All image assets are stored inside asset catalogs – you’ll discover how
            to replace the standard app icon with something more interesting.
        </li>
        <li>
            <em>
                Debugging.
            </em>
            Everybody makes mistakes when writing code and building apps and Xocde’s
            debugger makes identifying and fixing bugs a whole lot easier.
        </li>
        <li>
            <em>
                Documentation.
            </em>
            OS X apps are build on top of some extremely advanced system frameworks,
            and nobody can remember exactly how to use each and every one of them.
            Luckily Apple creates high-quality documentation and has integrated it
            with Xcode to make it easy to find answers to your questions.
        </li>
    </ul>
    <h3>
        Code Editor
    </h3>
    <p>
        Apps are built primarily from code, written in the Swift programming language.
        You can also use Objective-C to write apps for OS X, but Apple introduced
        Swift in 2014, and was very clear that it is the langauge of the future.
        <em>
            HubEvent
        </em>
        is written in Swift.
    </p>
    <p>
        One of the views available in Xcode is the
        <em>
            Code Editor
        </em>
        , which is activated whenever you open a source code file. To see it,
        select
        <em>
            WindowController.swift
        </em>
        from the
        <em>
            Controllers
        </em>
        group in the
        <em>
            Project navigator
        </em>
        .
    </p>
    <p>
        <img class="aligncenter wp-image-110238 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/07/source_editor-700x368.png"
        alt="" width="700" height="368" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/source_editor-700x368.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/source_editor-480x252.png 480w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        You might need to show the
        <em>
            Navigator pane
        </em>
        on the left hand side using the buttons in the toolbar, and choose the
        <em>
            Project navigator
        </em>
        within the navigator pane. The buttons are shown in the above screenshot.
    </div>
    <p>
        In the main section of the Xcode window, you can now see the source code
        associated with the Window Controller. Find the following line:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1101701">
                    <td class="code" id="p110170code1">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #11740a; font-style: italic;">
                                // The shared data model
                            </span>
                            <span style="color: #a61390;">
                                let
                            </span>
                            sharedDataStore
                            <span style="color: #002200;">
                                =
                            </span>
                            DataStore
                            <span style="color: #002200;">
                                (
                            </span>
                            username
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #bf1d1a;">
                                "rwenderlich"
                            </span>
                            , type
                            <span style="color: #002200;">
                                :
                            </span>
                            .Network
                            <span style="color: #002200;">
                                )
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This line is selecting the source of the GitHub event data – here choosing
        Ray’s username (
        <code>
            rwenderlich
        </code>
        ).
    </p>
    <p>
        Try changing
        <code>
            rwenderlich
        </code>
        to a different GitHub username – for example
        <code>
            sammyd
        </code>
        . Then, build and run your app as you did before. You’ll see the new user’s
        events listed in the app:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110221" src="https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_sammyd-629x500.png"
        alt="hubevent_sammyd" width="629" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_sammyd-629x500.png 629w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_sammyd-403x320.png 403w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_sammyd.png 979w"
        sizes="(max-width: 629px) 100vw, 629px">
    </p>
    <p>
        Well done! You’ve changed your first code in an OS X app!
    </p>
    <p>
        The code editor includes many powerful features to assist you as your
        write code, including autocompletion and QuickLook documentation.
    </p>
    <h3>
        Interface Builder
    </h3>
    <p>
        Although it is possible to build the user interface of an OS X app entirely
        in code, since UI is inherently visual, proceeding in this manner isn’t
        very intuitive.
    </p>
    <p>
        Xcode includes a tool called Interface Builder (IB), which is a fully-featured
        visual design tool that allows you to build your UI from reusable components.
    </p>
    <p>
        The files which make up these visual interfaces are called Storyboards
        – a name inspired by the film industry. In the same way that a storyboard
        is used to depict scenes in a film, and the progression through it, a storyboard
        in an app depicts the scenes and the flow between them.
    </p>
    <p>
        To see a storyboard in Interface Builder, select
        <em>
            Main.storyboard
        </em>
        in the
        <em>
            Project navigator
        </em>
        :
    </p>
    <p>
        <img class="aligncenter wp-image-110239 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/07/storyboard-700x492.png"
        alt="" width="700" height="492" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/storyboard-700x492.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/storyboard-456x320.png 456w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        This storyboard includes the layout for the entire app. You can see how
        the table at the top of the app is split out as a separate entity from
        the JSON viewer at the bottom.
    </p>
    <p>
        To get a really quick feel for interface builder, you’re going to change
        the color of the icon in the left hand column.
    </p>
    <p>
        Although being zoomed out allows you to get a good view of the entire
        storyboard, you can’t edit a zoomed out storyboard. Zoom in to the
        <em>
            EventList VC
        </em>
        scene using
        <em>
            ⌘+
        </em>
        . This is the scene that contains the table:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110218" src="https://koenig-media.raywenderlich.com/uploads/2015/07/eventlist-700x320.png"
        alt="eventlist" width="700" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/eventlist-700x320.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/eventlist-480x219.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/eventlist.png 946w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Use the button in the bottom left corner to
        <em>
            Show Document Outline
        </em>
        . This is a panel along the left hand side of Interface Builder which
        shows you the hierarchy of components that make up the current scene.
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110228" src="https://koenig-media.raywenderlich.com/uploads/2015/07/select_icon-345x500.png"
        alt="select_icon" width="345" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/select_icon-345x500.png 345w, https://koenig-media.raywenderlich.com/uploads/2015/07/select_icon-221x320.png 221w, https://koenig-media.raywenderlich.com/uploads/2015/07/select_icon.png 782w"
        sizes="(max-width: 345px) 100vw, 345px">
    </p>
    <p>
        If you click on the purple
        <em>
            ⌘
        </em>
        symbol in the table view, you’ll highlight the corresponding
        <em>
            Table Cell View
        </em>
        row in the
        <em>
            Document Outline
        </em>
        . Since you want to access the text field
        <i>
            inside
        </i>
        this cell, click on the
        <em>
            ⌘
        </em>
        again. Now you’ll have the row selected as in the previous image.
    </p>
    <p>
        Once you’ve selected this text field, you can configure various attributes
        associated with it, which determine its appearance.
    </p>
    <p>
        If the
        <em>
            Utilities
        </em>
        panel is not visible down the right hand side of Xcode, use the button
        in the toolbar to show it:
    </p>
    <p>
        <img class="aligncenter size-full wp-image-110233" src="https://koenig-media.raywenderlich.com/uploads/2015/07/utilities_button.png"
        alt="utilities_button" width="220" height="66">
    </p>
    <p>
        This panel can display many different inspectors, but the one you want
        now is the
        <em>
            Atrributes Inspector
        </em>
        . Select it now and you’ll find the
        <em>
            Text Color
        </em>
        attribute:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110210" src="https://koenig-media.raywenderlich.com/uploads/2015/07/attributes_inspector-337x500.png"
        alt="attributes_inspector" width="337" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/attributes_inspector-337x500.png 337w, https://koenig-media.raywenderlich.com/uploads/2015/07/attributes_inspector-216x320.png 216w, https://koenig-media.raywenderlich.com/uploads/2015/07/attributes_inspector.png 520w"
        sizes="(max-width: 337px) 100vw, 337px">
    </p>
    <p>
        Tap on the purple color bar, and you’ll see a colors panel. Use this to
        select a different color – e.g. yellow:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110212" src="https://koenig-media.raywenderlich.com/uploads/2015/07/color_panel-290x500.png"
        alt="color_panel" width="290" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/color_panel-290x500.png 290w, https://koenig-media.raywenderlich.com/uploads/2015/07/color_panel-186x320.png 186w, https://koenig-media.raywenderlich.com/uploads/2015/07/color_panel.png 460w"
        sizes="(max-width: 290px) 100vw, 290px">
    </p>
    <p>
        Now you can build and run
        <em>
            HubEvent
        </em>
        again to see the effect your change has had:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110222" src="https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_yellow-700x438.png"
        alt="hubevent_yellow" width="700" height="438" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_yellow-700x438.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_yellow-480x300.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_yellow.png 1078w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h3>
        Asset Catalog
    </h3>
    <p>
        In addition to code and user interfaces, your app will also need some
        assets such as artwork. Due to the different screen types (e.g. retina
        and non-retina), you often need to provide multiple versions of each asset.
        To simplify this process, Xcode uses
        <em>
            Asset Libraries
        </em>
        to store and organize the assets that accompany the app.
    </p>
    <p>
        <em>
            HubEvent
        </em>
        already has the default asset library, called
        <em>
            Images.xcassets
        </em>
        . Select it in the
        <em>
            Project navigator
        </em>
        to reveal its content:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110208" src="https://koenig-media.raywenderlich.com/uploads/2015/07/asset_library-700x247.png"
        alt="asset_library" width="700" height="247" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/asset_library-700x247.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/asset_library-480x170.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/asset_library.png 1126w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        When you create a new app, the template includes an asset library, with
        just one entry – the app logo. This is exactly the state of the asset library
        in
        <em>
            HubEvent
        </em>
        . You can see the different asset types you can create by right clicking
        in the left pane of the library:
    </p>
    <p>
        <img class="aligncenter wp-image-110209 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/07/asset_types-285x320.png"
        alt="asset_types" width="285" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/asset_types-285x320.png 285w, https://koenig-media.raywenderlich.com/uploads/2015/07/asset_types-445x500.png 445w, https://koenig-media.raywenderlich.com/uploads/2015/07/asset_types.png 532w"
        sizes="(max-width: 285px) 100vw, 285px">
    </p>
    <p>
        Currently the app icon for
        <em>
            HubEvent
        </em>
        is the default OS X icon:
    </p>
    <p>
        <img class="aligncenter size-full wp-image-110226" src="https://koenig-media.raywenderlich.com/uploads/2015/07/original_icon.png"
        alt="original_icon" width="126" height="144">
    </p>
    <p>
        Since the app icon is provided by the asset catalog, you’re going to replace
        it with something more appropriate. Click on the
        <em>
            AppIcon
        </em>
        asset:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110206" src="https://koenig-media.raywenderlich.com/uploads/2015/07/appicon-700x328.png"
        alt="appicon" width="700" height="328" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/appicon-700x328.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/appicon-480x225.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/appicon.png 1444w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        When you provide an app icon for an app, you have to provide it in many
        different sizes and densities for use around the system. As a demonstration,
        you’re going to add one of these sizes to see the app icon change.
    </p>
    <p>
        Use Finder to locate
        <em>
            rw
        </em>
        <em>
            _
        </em>
        <em>
            icon.png
        </em>
        in the unzipped directory you downloaded. Then drag this from Finder into
        the
        <em>
            Mac 512pt 2x
        </em>
        cell in the
        <em>
            AppIcon
        </em>
        asset:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110207" src="https://koenig-media.raywenderlich.com/uploads/2015/07/appicon_updated-700x320.png"
        alt="appicon_updated" width="700" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/appicon_updated-700x320.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/appicon_updated-480x219.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/appicon_updated.png 1444w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        Providing a single image in this manner is not generally appropriate.
        In a real application you should provide all ten versions of the icon.
    </div>
    <p>
        Now build and run the app again and you’ll see the updated icon in the
        dock:
    </p>
    <p>
        <img class="aligncenter size-full wp-image-110223" src="https://koenig-media.raywenderlich.com/uploads/2015/07/new_icon.png"
        alt="new_icon" width="140" height="138" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/new_icon.png 140w, https://koenig-media.raywenderlich.com/uploads/2015/07/new_icon-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/07/new_icon-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2015/07/new_icon-96x96.png 96w"
        sizes="(max-width: 140px) 100vw, 140px">
    </p>
    <h2>
        Debugging
    </h2>
    <p>
        Nobody is capable of writing code that works perfectly every time, and
        therefore you’re likely to spend time trying to fix problems in your code.
        You’ll soon find that it’d be really helpful to be able to stop your app
        at a particular line of code and investigate the values of variables. This
        is precisely the functionality provided by a debugger.
    </p>
    <p>
        Once again, Xcode is here to help. It has an integrated debugger that
        makes runtime investigation of your code really easy. To demonstrate some
        of its functionality, you’re going to use it.
    </p>
    <p>
        Open
        <em>
            Value Transformers\CodeStringFormattingTransformer.swift
        </em>
        by selecting it in the
        <em>
            Project navigator
        </em>
        .
    </p>
    <p>
        Find the following line in the code:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1101702">
                    <td class="code" id="p110170code2">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #a61390;">
                                return
                            </span>
                            <span style="color: #400080;">
                                NSAttributedString
                            </span>
                            <span style="color: #002200;">
                                (
                            </span>
                            string
                            <span style="color: #002200;">
                                :
                            </span>
                            unescaped, attributes
                            <span style="color: #002200;">
                                :
                            </span>
                            attributes
                            <span style="color: #002200;">
                                )
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        <em>
            Click
        </em>
        in the gutter to the left of this line to insert a
        <em>
            breakpoint
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-full wp-image-110211" src="https://koenig-media.raywenderlich.com/uploads/2015/07/breakpoint.png"
        alt="breakpoint" width="672" height="64" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/breakpoint.png 672w, https://koenig-media.raywenderlich.com/uploads/2015/07/breakpoint-480x46.png 480w"
        sizes="(max-width: 672px) 100vw, 672px">
    </p>
    <p>
        A breakpoint marks the line in your code at which point execution will
        stop. Your app will pause at this point to allow you to investigate the
        state.
    </p>
    <p>
        <em>
            Build and run
        </em>
        the app. You’ll see the app start, before Xcode comes back to the foreground.
        You’ll see the line you added the breakpoint to highlighted:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110219" src="https://koenig-media.raywenderlich.com/uploads/2015/07/highlighted_line-700x39.png"
        alt="highlighted_line" width="700" height="39" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/highlighted_line-700x39.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/highlighted_line-480x27.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/highlighted_line.png 1082w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        This means that your app has started running, and then reached this line
        of code. It has paused here to allow you to investigate.
    </p>
    <p>
        The bottom pane in Xcode shows you the state of the variables at the current
        point of execution, including their variables.
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110214" src="https://koenig-media.raywenderlich.com/uploads/2015/07/debug_pane-700x186.png"
        alt="debug_pane" width="700" height="186" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/debug_pane-700x186.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/debug_pane-480x127.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/debug_pane.png 1296w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        This particular method is removing escaped characters from the JSON downloaded
        from the GitHub API. You can see the input string
        <code>
            s
        </code>
        and the resultant string
        <code>
            unescaped
        </code>
        .
    </p>
    <p>
        You can progress to the next line of execution with the
        <em>
            stepover
        </em>
        button:
    </p>
    <p>
        <img class="aligncenter size-full wp-image-110230" src="https://koenig-media.raywenderlich.com/uploads/2015/07/stepover.png"
        alt="stepover" width="56" height="52">
    </p>
    <p>
        Or to continue the program execution, use the
        <em>
            continue
        </em>
        button:
    </p>
    <p>
        <img class="aligncenter size-full wp-image-110213" src="https://koenig-media.raywenderlich.com/uploads/2015/07/continue.png"
        alt="continue" width="52" height="50" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/continue.png 52w, https://koenig-media.raywenderlich.com/uploads/2015/07/continue-32x32.png 32w"
        sizes="(max-width: 52px) 100vw, 52px">
    </p>
    <p>
        Note that continuing will then run the program until it comes across another
        breakpoint.
    </p>
    <p>
        To remove a breakpoint, you can drag it out of the gutter until the pointer
        changes to a
        <em>
            x
        </em>
        .
    </p>
    <h3>
        Fixing a bug with the debugger
    </h3>
    <p>
        To see how debugging works, you’re going to fix a real-world bug! You’ve
        had reports that if you change HubEvent to use a disk-based data source
        instead of network then it ignores your choice – and still queries the
        network. Your job is to find this bug and fix it.
    </p>
    <p>
        First, to change the app into disk-mode instead of network-mode, open
        <em>
            WindowController.swift
        </em>
        , locate the line that creates the
        <code>
            sharedDataStore
        </code>
        , and update it to match the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1101703">
                    <td class="code" id="p110170code3">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #a61390;">
                                let
                            </span>
                            sharedDataStore
                            <span style="color: #002200;">
                                =
                            </span>
                            DataStore
                            <span style="color: #002200;">
                                (
                            </span>
                            username
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #bf1d1a;">
                                "rwenderlich"
                            </span>
                            , type
                            <span style="color: #002200;">
                                :
                            </span>
                            .Disk
                            <span style="color: #002200;">
                                )
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now run up the app, and confirm that the data is indeed still being pulled
        from the network (the on-disk data was acquired in April 2015).
    </p>
    <p>
        To debug this problem, you’re going to add a break point at the point
        the data store is created to find out what’s happening. Open
        <em>
            DataStore.swift
        </em>
        , and add a breakpoint on the line that contains
        <code>
            super.init()
        </code>
        .
    </p>
    <p>
        Run the app and wait for it to pause at the break point. Use the debug
        browser to locate the
        <code>
            dataProvider
        </code>
        property within
        <code>
            self
        </code>
        :
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110313" src="https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_dataprovider-480x254.png"
        alt="debugging_dataprovider" width="480" height="254" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_dataprovider-480x254.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_dataprovider-700x370.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_dataprovider.png 960w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        Notice that the type next to it is
        <code>
            GitHubData.GitHubDataNetworkProvider
        </code>
        . This doesn’t sound right – why would it be using an object called network
        when it’s reading off disk.
    </p>
    <p>
        Now take a look further up the file, and you’ll find where this
        <code>
            dataProvider
        </code>
        object is created:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1101704">
                    <td class="code" id="p110170code4">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #a61390;">
                                switch
                            </span>
                            type
                            <span style="color: #002200;">
                                {
                            </span>
                            <span style="color: #a61390;">
                                case
                            </span>
                            .Network
                            <span style="color: #002200;">
                                :
                            </span>
                            dataProvider
                            <span style="color: #002200;">
                                =
                            </span>
                            GitHubDataNetworkProvider
                            <span style="color: #002200;">
                                (
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #a61390;">
                                case
                            </span>
                            .Disk
                            <span style="color: #002200;">
                                :
                            </span>
                            dataProvider
                            <span style="color: #002200;">
                                =
                            </span>
                            GitHubDataNetworkProvider
                            <span style="color: #002200;">
                                (
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                }
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This is a switch statement that decides what kind of provider it needs
        to create – why does it create a
        <code>
            GitHubDataNetworkProvider
        </code>
        for the
        <code>
            .Disk
        </code>
        type? This is the bug!
    </p>
    <p>
        Replace the
        <code>
            .Disk
        </code>
        case to match the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1101705">
                    <td class="code" id="p110170code5">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #a61390;">
                                case
                            </span>
                            .Disk
                            <span style="color: #002200;">
                                :
                            </span>
                            dataProvider
                            <span style="color: #002200;">
                                =
                            </span>
                            GitHubDataFileProvider
                            <span style="color: #002200;">
                                (
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now re-run the app, and it’ll pause on the same breakpoint. Check the
        type of the
        <code>
            dataProvider
        </code>
        property once again:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110314" src="https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_fixed-480x166.png"
        alt="debugging_fixed" width="480" height="166" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_fixed-480x166.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_fixed-700x242.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_fixed.png 960w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        The type now looks correct – use the
        <em>
            Continue program execution
        </em>
        button to run the app:
    </p>
    <p>
        <img class="aligncenter wp-image-110315 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_disk-479x500.png"
        alt="hubevent_disk" width="479" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_disk-479x500.png 479w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_disk-307x320.png 307w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_disk-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_disk.png 1002w"
        sizes="(max-width: 479px) 100vw, 479px">
    </p>
    <p>
        Yay! The app is now reading from the disk-based store, rather than over
        the network. Well done – you’ve fixed your first OS X bug!
    </p>
    <h2>
        Documentation
    </h2>
    <p>
        Xcode has a couple of integrated ways to get access to documentation for
        system frameworks. The first is the ability to show a tooltip containing
        the most salient information about a class or method.
    </p>
    <p>
        As an example, open
        <em>
            Controllers\WindowController.swift
        </em>
        and inside the
        <code>
            transformedValueClass()
        </code>
        method,
        <em>
            Option-Click
        </em>
        on
        <code>
            NSString
        </code>
        :
    </p>
    <p>
        <img class="aligncenter wp-image-110232 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/07/tooltip-480x194.png"
        alt="tooltip" width="480" height="194" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/tooltip-480x194.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/tooltip-700x282.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/tooltip.png 1022w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        The second method of accessing documentation shows you the full documentation
        in a dedicated browser. To access this, either click on the
        <em>
            Reference
        </em>
        link at the bottom of the tooltip, or click the
        <em>
            Window
        </em>
        <em>
            \
        </em>
        <em>
            Documentation and Reference
        </em>
        menu. Then search for
        <code>
            NSString
        </code>
        to pull up the documentation:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110216" src="https://koenig-media.raywenderlich.com/uploads/2015/07/doc_browser-700x339.png"
        alt="doc_browser" width="700" height="339" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/doc_browser-700x339.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/doc_browser-480x233.png 480w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        Fixing a bug with documentation
    </h2>
    <p>
        Let’s see how you can use Xcode’s documentation to fix another bug.
    </p>
    <p>
        When HubEvent first loads, you’ll notice that the divider between the
        table and the JSON view is positioned very high:
    </p>
    <p>
        <img class="aligncenter wp-image-110310 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/07/divider_initial-479x500.png"
        alt="divider_initial" width="479" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/divider_initial-479x500.png 479w, https://koenig-media.raywenderlich.com/uploads/2015/07/divider_initial-306x320.png 306w, https://koenig-media.raywenderlich.com/uploads/2015/07/divider_initial-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/07/divider_initial.png 1002w"
        sizes="(max-width: 479px) 100vw, 479px">
    </p>
    <p>
        If you try to drag the divider down, you’ll see that it snaps to the middle
        of the window, and is then immovable. This is the behavior you’d like,
        but the divider should be in the correct position when the app starts.
    </p>
    <p>
        You can achieve this by adding a single line to the
        <code>
            viewWillAppear()
        </code>
        method inside the
        <em>
            SplitViewController.swift
        </em>
        file. Use the documentation browser to search for
        <code>
            NSSplitView
        </code>
        , and read about the
        <code>
            setPosition(_:, ofDividerAtIndex:)
        </code>
        method. Then use this method on the
        <code>
            splitView
        </code>
        property in the aforementioned method, passing in
        <code>
            view.bounds.height / 2.0
        </code>
        for the position.
    </p>
    <div class="easySpoilerWrapper" style="">
        <table class="easySpoilerTable" border="0" style="text-align:center;"
        align="center" bgcolor="FFFFFF">
            <tbody>
                <tr style="white-space:normal;">
                    <th class="easySpoilerTitleA" style="white-space:normal;font-weight:normal;text-align:left;vertical-align:middle;font-size:120%;color:#000000;">
                        Solution Inside: Divider Position
                    </th>
                    <th class="easySpoilerTitleB" style="text-align:right;vertical-align:middle;font-size:100%; white-space:nowrap;">
                        <a href="" onclick="wpSpoilerSelect(&quot;spoilerDiv14998001&quot;); return false;"
                        class="easySpoilerButtonOther" style="font-size:100%;color:#000000;background-color:#fcfcfc;background-image:none;border: 1px inset;border-style:solid;border-color:#cccccc; margin: 3px 0px 3px; padding: 4px; "
                        align="right" sl-processed="1">
                            Select
                        </a>
                        <a href="" onclick="wpSpoilerToggle(&quot;spoilerDiv14998001&quot;,true,&quot;Show&quot;,&quot;Hide&quot;,&quot;fast&quot;,false); return false;"
                        id="spoilerDiv14998001_action" class="easySpoilerButton" value="Show" align="right"
                        style="font-size:100%;color:#000000;background-color:#fcfcfc;background-image:none;border: 1px inset;border-style:solid;border-color:#cccccc; margin: 3px 0px 3px 5px; padding: 4px;"
                        sl-processed="1">
                            Show
                        </a>
                    </th>
                </tr>
                <tr>
                    <td class="easySpoilerRow" colspan="2" style="">
                        <div id="spoilerDiv14998001" class="easySpoilerSpoils" style="display:none; white-space:wrap; overflow:auto; vertical-align:middle;">
                            <p>
                            </p>
                            <div class="wp_codebox">
                                <table>
                                    <tbody>
                                        <tr id="p1101706">
                                            <td class="code" id="p110170code6">
                                                <pre class="swift" style="font-family:monospace;">
                                                    splitView.setPosition
                                                    <span style="color: #002200;">
                                                        (
                                                    </span>
                                                    view.bounds.height
                                                    <span style="color: #002200;">
                                                        /
                                                    </span>
                                                    <span style="color: #2400d9;">
                                                        2.0
                                                    </span>
                                                    , ofDividerAtIndex
                                                    <span style="color: #002200;">
                                                        :
                                                    </span>
                                                    <span style="color: #2400d9;">
                                                        0
                                                    </span>
                                                    <span style="color: #002200;">
                                                        )
                                                    </span>
                                                </pre>
                                            </td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                            <p>
                            </p>
                        </div>
                    </td>
                </tr>
            </tbody>
        </table>
        <div class="easySpoilerConclude" style="">
            <table class="easySpoilerTable" border="0" style="text-align:center;"
            frame="box" align="center" bgcolor="FFFFFF">
                <tbody>
                    <tr>
                        <th class="easySpoilerEnd" style="width:100%;">
                        </th>
                        <td class="easySpoilerEnd" style="white-space:nowrap;" colspan="2">
                        </td>
                    </tr>
                    <tr>
                        <td class="easySpoilerGroupWrapperLastRow" colspan="2" style="">
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
    <p>
        &nbsp;
    </p>
    <h2>
        Where To Go From Here?
    </h2>
    <div class="inline-video-ad" id="sub-banner-inline">
        <div class="inline-video-ad-wrapper">
            <a href="https://videos.raywenderlich.com/courses" sl-processed="1">
                <div class="col-wrapper">
                    <div class="col">
                        <img src="https://cdn3.raywenderlich.com/wp-content/themes/raywenderlich/images/global/video-yeti@2x.png"
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
        Here’s the
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/HubEvent_7.1.zip"
        sl-processed="1">
            finished project
        </a>
        &nbsp;for this Max OS X development tutorial.
    </p>
    <p>
        At this point, you have a birds-eye overview of the most important aspects
        of Xcode. In the
        <a href="http://www.raywenderlich.com/110267/mac-os-x-development-tutorial-for-beginners-part-2-os-x-app-anatomy"
        sl-processed="1">
            next article
        </a>
        you’ll learn about the anatomy of an app, and finally move on to creating
        your first OS X app.
    </p>
    <p>
        Apple has a huge amount of documentation for OS X – all available on the
        <a href="https://developer.apple.com/library/mac/navigation/" sl-processed="1">
            Developer Portal
        </a>
        .
    </p>
    <p>
        If you have any questions or comments then please join in below or on
        the forums.
    </p>
</div>
