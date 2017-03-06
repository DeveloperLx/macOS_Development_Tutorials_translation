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
                <em>否则</em>，保持继续阅读 - 这个系列是面对完全的初学者 - 不要求有过开发iOS或OS X经验。
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
    	本教程需要Xcode 7的版本，因为教程中的样本工程已更新到Swift 2.0编程语言。有两种情形：
    </p>
    <ul>
        <li>
            <em>
            	当阅读本教程时，如果App Store中的Xcode 版本是Xcode 7
            </em>
            ，你就直接省心了！
        </li>
        <li>
            <em>
	            当阅读本教程时，如果App Store中的Xcode 版本是Xcode 6
            </em>
            ，你就得安装一个beta版本的Xcode 7 - 继续阅读来学习怎么做。
        </li>
    </ul>
    <p>
    	要获取Xcode的最新版本，浏览
        To get the latest beta version of Xcode, visit
        <a href="https://developer.apple.com/" sl-processed="1">
            developer.apple.com
        </a>
        ，点击
        <em>
            Resources
        </em>
        ，
        <em>
            Xcode
        </em>
        及
        <em>
            Download
        </em>
        。在这里跟随链接去下载最新版本的Xcode。
    </p>
    <p>
    	注意你可以在稳定版的Xcode旁，安装一个beta版本的Xcode。所以完全可以使没有为更新准备好的项目继续正常运行。
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
    	下载到的是一个DMG文件，因此你可以像往常一样，通过将Xcode app拖到
        <em>
            Applications
        </em>
        中。这样你就会有两个版本的Xcode在你的applications目录中：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/2Xcode.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-112242" src="https://koenig-media.raywenderlich.com/uploads/2015/08/2Xcode.png"
            alt="2Xcode" width="256" height="124">
        </a>
    </p>
    <p>
        运行
        <em>
            Xcode-beta
        </em>
        ，准备好继续下面的内容！
    </p>
    <h2>
        Hello World!
    </h2>
    <p>
    	Xcode是一个集成开发环境，这意味着它是一个你需要的所有开发工具的集合，从源码编辑，编译，到debug和UI设计。
    </p>
    <p>
    	当你大开Xcode时，它会让你创建一个新项目，或打开一个已存在的项目。你也可以通过双击目录中的Xcode project或workspace来打开一个已存在的项目：
    </p>
    <p>
        <img class="aligncenter wp-image-110225 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/07/open_finder-480x269.png"
        alt="open_finder" width="480" height="269" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/open_finder-480x269.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/open_finder-700x393.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/open_finder.png 1052w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <h3>
        创建一个新的app
    </h3>
    <p>
    	在这个教程中的大部分，你将通过一个样本项目来游览Xcode，但是首先的第一件事情 - 你必须创建一个“Hello World” app来了解新的平台！
    </p>
    <p>
    	要想这么做，从Xcode的欢迎屏幕中，选择
        <em>
            Create a new Xcode project
        </em>
		：
	</p>
    <p>
        <img class="aligncenter wp-image-110236 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/07/xocde_welcome-480x289.png"
        alt="xocde_welcome" width="480" height="289" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/xocde_welcome-480x289.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/xocde_welcome-700x422.png 700w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	模板选择器允许你决定Xcode怎么配置你的新工程。在
        <em>
            OS X
        </em>
        <em>
            \
        </em>
        <em>
            Application
        </em>
        部分，你可以看到三个不同的核心OS X app的类型：
    </p>
    <p>
        <img class="aligncenter wp-image-110224 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/07/new_project-451x320.png"
        alt="new_project" width="451" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/new_project-451x320.png 451w, https://koenig-media.raywenderlich.com/uploads/2015/07/new_project-700x496.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/new_project.png 1464w"
        sizes="(max-width: 451px) 100vw, 451px">
    </p>
    <p>
    	三个不同的app类型如下：
    </p>
    <ul>
        <li>
            <em>
                Cocoa Application
            </em>
            ：OS X桌面app，基于窗口的UI。全部的OS X应用构建在名为Cocoa的framework上。
        </li>
        <li>
            <em>
                Game
            </em>
            ：使用苹果的SpriteKit或SceneKit frameworks构建的游戏。
        </li>
        <li>
            <em>
                Command Line Tool
            </em>
            ：运行在shell上的工具，有基于文本的UI。
        </li>
    </ul>
    <p>
        选择
        <em>
            Cocoa Application
        </em>
        ，点击
        <em>
            Next
        </em>
        。在接下来的屏幕中，设置
        <em>
            Product Name
        </em>
        为
        <em>
            HelloWorld
        </em>
        ，检查language被设置为
        <em>
            Swift
        </em>
        和
        <em>
            Use Storyboards
        </em>
		已被勾选：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110277" src="https://koenig-media.raywenderlich.com/uploads/2015/07/new_project1-450x320.png"
        alt="new_project" width="450" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/new_project1-450x320.png 450w, https://koenig-media.raywenderlich.com/uploads/2015/07/new_project1-700x497.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/new_project1.png 1464w"
        sizes="(max-width: 450px) 100vw, 450px">
    </p>
    <p>
        点击
        <em>
            Next
        </em>
        ，选择一个磁盘中的位置来保存你的项目。
    </p>
    <p>
    	这将创建一个新的空项目，准备好为你打造令人惊叹的app。第一件你想做的事，是build和运行来检查它是否工作正常。
    </p>
    <h3>
        运行你的app
    </h3>
    <p>
    	不管你是打开一个已存在的app，还是创建一个新的，最重要的事都是你想build和运行它。
    </p>
    <p>
    	这会将所有你写的code编译成机器码，打包所有app需求的资源，然后执行。这个过程是复杂的，但幸运的时Xcode会帮你搞定。要想build和执行你的项目，只需点击工具栏上的
        <em>
            play
        </em>
        按钮：
    </p>
    <p>
        <img class="aligncenter wp-image-110281 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/07/play_button1-480x124.png"
        alt="" width="480" height="124" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/play_button1-480x124.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/play_button1.png 534w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	你也可以使用快捷键
        <em>
            ⌘R
        </em>
        来build和运行你的app。
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110284" src="https://koenig-media.raywenderlich.com/uploads/2015/07/bar_empty-480x292.png"
        alt="bar_empty" width="480" height="292" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/bar_empty-480x292.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/bar_empty-700x426.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/bar_empty.png 962w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <div class="note">
        <em>
        	注意：
        </em>
        当你第一次用Xcode build和执行app时，你可能被询问是否想要
        <em>
        	在这台电脑上打开开发者模式？
        </em>
        你可以安全地选择
        <em>
        	打开
        </em>
        ，并可能会遇到要求输入你的密码的时候。开发者模式允许附加一个调试者 - 这在当你build你的应用时将会非常得有用！
    </div>
    <p>
        当前，你的
        <em>
            HelloWorld
        </em>
        app看起来有一点空 - 甚至连hello都没有说！现在，你将要修复它。
    </p>
    <h3>
    	添加文本
    </h3>
    <p>
    	现在你要更新你的app的用户界面（UI），让它变成一真正的“Hello World” app，因此你要使用一个名叫Interface Builder (IB)的工具来实现。在这个教程后面，你会学到很多关于Interface Builder的 - 对于现在，你只需要知道怎么添加一些文本到布局中就够了。
    </p>
    <p>
    	在
    	<em>
            Project Navigator
        </em>
        中，找到
        <em>
            Main.storyboard
        </em>
        文件，点击它：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110287" src="https://koenig-media.raywenderlich.com/uploads/2015/07/open_storyboard-294x320.png"
        alt="open_storyboard" width="294" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/open_storyboard-294x320.png 294w, https://koenig-media.raywenderlich.com/uploads/2015/07/open_storyboard-459x500.png 459w, https://koenig-media.raywenderlich.com/uploads/2015/07/open_storyboard.png 518w"
        sizes="(max-width: 294px) 100vw, 294px">
    </p>
    <p>
    	这会在Interface Builder中打开storyboard文件 - 你会看到你全部app的轮廓：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110288" src="https://koenig-media.raywenderlich.com/uploads/2015/07/hello_world_storyboard-343x500.png"
        alt="hello_world_storyboard" width="343" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/hello_world_storyboard-343x500.png 343w, https://koenig-media.raywenderlich.com/uploads/2015/07/hello_world_storyboard-219x320.png 219w, https://koenig-media.raywenderlich.com/uploads/2015/07/hello_world_storyboard.png 602w"
        sizes="(max-width: 343px) 100vw, 343px">
    </p>
    <p>
        下方的组件（被标为“View Controller”）的，代表着你app的可见的外观。你要添加一个text label到这里来创建你的“Hello World”app。
    </p>
    <p>
        在Xcode窗口的右下部分，找到
        <em>
            Object Library
        </em>
        。在搜索框中输入
        <em>
            label
        </em>
        并定位到
        <em>
            Label
        </em>
        入口：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110291" src="https://koenig-media.raywenderlich.com/uploads/2015/07/object_library-330x320.png"
        alt="object_library" width="330" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/object_library-330x320.png 330w, https://koenig-media.raywenderlich.com/uploads/2015/07/object_library-516x500.png 516w, https://koenig-media.raywenderlich.com/uploads/2015/07/object_library-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/07/object_library.png 520w"
        sizes="(max-width: 330px) 100vw, 330px">
    </p>
    <p>
    	从
   	    <em>
            Object Library
        </em>
        中
        <em>
    		拖拽
    	</em>
    	一个label到
 	    <em>
            View Controller
        </em>
    	的空的场景画布上：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110292" src="https://koenig-media.raywenderlich.com/uploads/2015/07/drag_label-480x312.png"
        alt="drag_label" width="480" height="312" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/drag_label-480x312.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/drag_label-700x455.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/drag_label.png 1022w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	一个label代表一块静态的文本 - 没有用户交互 - 对于你的Hello World app来说是完美的。你并不想让它说出“label”来直到你下次要升级的时候。
    </p>
    <p>
        要配置这个label，选择它，然后在Xcode窗口右侧打开
        <em>
            Attributes Inspector
        </em>
        （第四个标签）。设置
        <em>
            title
        </em>
        为
        <em>
            “Hello OS X!”
        </em>
        ，把
        <em>
            font
        </em>
        修改为
        <em>
            40号
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110294" src="https://koenig-media.raywenderlich.com/uploads/2015/07/label_config-296x320.png"
        alt="label_config" width="296" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/label_config-296x320.png 296w, https://koenig-media.raywenderlich.com/uploads/2015/07/label_config-462x500.png 462w, https://koenig-media.raywenderlich.com/uploads/2015/07/label_config.png 516w"
        sizes="(max-width: 296px) 100vw, 296px">
    </p>
    <p>
    	你可能会看到label的尺寸不再合适 - 下一步你会修复，并把它设到正确的位置上。
    </p>
    <p>
    	在OS X中，你安置UI原件是使用一个名叫Auto Layout的系统 - 它允许你根据它们之间的关系，指定UI原件的位置和大小。你想要摆放你的“Hello OS X!” label在窗口中央 - 因此你需要添加约束（constraints）来实现。
    </p>
    <p>
    	再次选择label，在底栏点击
        <em>
            Align
        </em>
        按钮（从左往右数第二个）。勾选
        <em>
            Horizontally in Container
        </em>
        和        
        <em>
            Vertically in Container
        </em>
        勾选框，并确保它们都被
        <em>
        	设为0
        </em>
        。在最后点击
        <em>
            Add 2 Constraints
        </em>
        按钮前，在
        <em>
            Update Frames
        </em>        
        中选择
        <em>
            Items of New Constraints
        </em>
		选择框：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110297" src="https://koenig-media.raywenderlich.com/uploads/2015/07/constraints-413x320.png"
        alt="constraints" width="413" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/constraints-413x320.png 413w, https://koenig-media.raywenderlich.com/uploads/2015/07/constraints-645x500.png 645w, https://koenig-media.raywenderlich.com/uploads/2015/07/constraints.png 1016w"
        sizes="(max-width: 413px) 100vw, 413px">
    </p>
    <p>
    	这会更新storyboard让你的label的位置和大小正确。
    </p>
    <p>
    	Build并执行的你的app（点击play按钮或使用
    	<em>
            ⌘R
        </em>
        快捷键均可），来查看你的“Hello World!” Mac OS X app：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110300" src="https://koenig-media.raywenderlich.com/uploads/2015/07/hello_osx-480x293.png"
        alt="hello_osx" width="480" height="293" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/hello_osx-480x293.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/hello_osx-700x428.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/hello_osx.png 962w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <h2>
        介绍HubEvent
    </h2>
    <p>
    	在这个系列之后的部分，你将学习怎么通过从涂画（scratch）和编码OS X app来制作项目，但在这个教程的剩余部分，你将关注更多Xcode本身的东西。
    </p>
    <p>
    	为了有所帮助，我为你创建了一个名叫
    	<em>
            HubEvent
        </em>
    	的简单的项目，在这个教程接下来，你将与之一起工作。这样你就可以得到一个真实世界项目中的Xcode的旅程。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/HubEvent_7.1.zip"
        sl-processed="1">
            下载
        </a>
        <em>
            HubEvent
        </em>
        启动器项目，解压它，然后在Finder中
        <em>
        	双击HubEvent\HubEvent.xcodeproj
        </em>
        来打开这个项目在Xcode中。
    </p>
    <p>
        Build并运行
        <em>
            HubEvent
        </em>
        样本项目，你将看到它编译然后启动：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110220" src="https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent-613x500.png"
        alt="hubevent" width="613" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent-613x500.png 613w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent-392x320.png 392w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent.png 1071w"
        sizes="(max-width: 613px) 100vw, 613px">
    </p>
    <p>
    	HubEvent使用公开的GitHub API来获取一个用户的所有事件，然后在一个表格中展示它们。当你选择列表中的每一行时，相关事件的源JSON就会展示在下面的面板中。
    </p>
    <h2>
        Xcode核心功能
    </h2>
    <p>
    	HubEvent是一个相当简单的app，但是足够来演示Xcode的核心功能。这篇教程的剩余部分将覆盖如下内容：
    </p>
    <ul>
        <li>
            <em>
                代码编辑器。
            </em>
            所有的OS X app都有一个代码组件，HubEvent也不例外。HubEvent的代码对于从GitHub API下载数据是非常靠得住的，并将其展示到用户界面上。
        </li>
        <li>
            <em>
                Interface Builder.
            </em>
            当你构建你的“Hello World!”app时，你已经使用过Interface Builder。你将学到更多关于这个强有力的工具的东西，它能让你构建出用在
            <em>
                HubEvent
            </em>
            上的分离窗口的UI效果。
        </li>
        <li>
            <em>
                Asset Catalog.（资产目录）
            </em>
            所有的图像都存放在asset catalogs中 - 你将发现怎么用一些更有趣的app icon代替标注的。
        </li>
        <li>
            <em>
                Debugging.
            </em>
            在写代码和build app时，每个人都会犯错，Xcode的debugger让识别和修复bug大幅度地变得容易。
        </li>
        <li>
            <em>
                文档。                
            </em>
            OS X app构建在一些非常先进的系统frameworks上，没有人可以精确地记住怎么去使用每一种。幸运的是，苹果创建了高质量的文档，并将其整合到了Xcode中，它可以使得你找到你问题的答案变得容易。
        </li>
    </ul>
    <h3>
        代码编辑器
    </h3>
    <p>
        App主要build自代码，由Swift编程语言写成。你也可以用OC来为OS X写app，但是苹果在2014年引入了Swift，很明显它是编程语言的未来。
        <em>
            HubEvent
        </em>
        是由Swift写成的。
    </p>
    <p>
        在Xcode中一个可用的视图是
        <em>
            代码编辑器
        </em>
        ，无论何时你打开源码文件，它都是活跃的。要查看它，在
        <em>
            Project navigator
        </em>
        从
        <em>
            Controllers
        </em>
        中选择
        <em>
            WindowController.swift
        </em>
        。
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
        从这儿去向哪里？
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
        这里是这个Max OS X开发教程
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/HubEvent_7.1.zip"
        sl-processed="1">
            最终完成的项目
        </a>
        。
    </p>
    <p>
    	现在，你已经有了对于Xcode所有最重要当面的把握（birds-eye overview）。在
        <a href="http://www.raywenderlich.com/110267/mac-os-x-development-tutorial-for-beginners-part-2-os-x-app-anatomy"
        sl-processed="1">
        	下一篇文章
        </a>
        中，你将学习对一个app的剖析，并最终创建出你的第一个OS X app。
    </p>
    <p>
        苹果有着OS X的大量文档 - 全部可以获取的在这里
        <a href="https://developer.apple.com/library/mac/navigation/" sl-processed="1">
            Developer Portal
        </a>
        .
    </p>
</div>
