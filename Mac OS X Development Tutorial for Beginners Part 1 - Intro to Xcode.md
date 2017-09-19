# macOS X 初学者开发教程 第一部分 Xcode介绍

#### [原文地址](https://www.raywenderlich.com/110170/mac-os-x-development-tutorial-for-beginners-part-1-intro-to-xcode) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
    	想要学习怎么使用Swift为你的Mac开发App？
        <img class="alignright size-full wp-image-110249 bordered" src="https://koenig-media.raywenderlich.com/uploads/2015/07/250x250.png"
        alt="250x250" width="250" height="250" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2015/07/250x250-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/07/250x250-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2015/07/250x250-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2015/07/250x250-128x128.png 128w" sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
        好消息 - 苹果让开发OS X变得难以置信得容易 - 在这个系列教程中，我们会展示给你要怎么做。你会学到怎么创建你的第一个OS X app - 即使你是一个完全的新手。
    </p>
    <ol>
        <li>在这个第一部分，你将首次了解怎么获取你需要的用来开发OS X的工具。然后，使用你下载的app作为例子，你将进行一次Xcode的游览，发现怎么去运行一个App，编辑代码，设计UI，debug程序。
        </li>
        <li>在<a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Mac%20OS%20X%20Development%20Tutorial%20for%20Beginners%20Part%202%20-%20OS%20X%20App%20Anatomy.md" sl-processed="1">第二部分</a>，你将从Xcode回退一步，学习构成一个OS X app的组成成分。从一个app怎么启动，到UI怎么构建，再到怎么处理交互。
        </li>
        <li>在<a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Mac%20OS%20X%20Development%20Tutorial%20for%20Beginners%20Part%203%20-%20Your%20First%20OS%20X%20App.md"
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
            这里有一些这个系列该从哪里开始的指导：
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
                ，来获取一个很赞的介绍。
            </li>
            <li>
                <em>
                	如果你早就有了iOS的经验
                </em>
                ，这个系列的第一部分将是回顾。快速地浏览主题，来确认你已掌握它们，然后直接跳到这个系列的<a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Mac%20OS%20X%20Development%20Tutorial%20for%20Beginners%20Part%202%20-%20OS%20X%20App%20Anatomy.md"
                sl-processed="1">下一部分</a>。
            </li>
            <li>
                <em>否则</em>，继续阅读 - 这个系列是面对纯小白的 - 不要求有过开发iOS或OS X的经验。
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
            OS X操作系统只能在苹果电脑上运行，因此你需要一个Mac来开发和运行OS X app。如果你困惑该买哪个Mac，我们推荐Mac mini，搭配额外的内存，和固态或融合的驱动；这是对于费用和性能的最佳平衡。
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
            它是用来创建OS X app的集成开发环境和工具链。你会在下一个部分学到如何来安装它。
        </li>
    </ul>
    <p>
    	一旦你构建好了你的app，你想把它上传到App Store并发布，你就需要去买一个苹果开发者账号。但在你准备好发送你的app到全世界前，这都不是必须的。
    </p>
    <h2>
        获取工具
    </h2>
    <p>
        开发OS X只要求安装一个工具 - 就是我们所知的Xcode，不像一些其它的平台。Xcode是一个包含所有开发iOS，watchOS和OS X app所需的集成开发环境。
    </p>
    <p>
        如果你还没有Xcode，点击你菜单栏左上角的Apple icon图标，选择<em>App Store</em>来打开Mac App商店。
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
        搜索Xcode并下载它：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110235 bordered" src="https://koenig-media.raywenderlich.com/uploads/2015/07/xcode_mas-679x500.png"
        alt="xcode_mas" width="679" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/xcode_mas-679x500.png 679w, https://koenig-media.raywenderlich.com/uploads/2015/07/xcode_mas-435x320.png 435w"
        sizes="(max-width: 679px) 100vw, 679px">
    </p>
    <p>
        下载和安装好它之后，从你的Applications目录下打开Xcode。第一次打开Xcode时，它会请求你安装一些额外的组件。让它安装，如果它要求的话，输入你的密码。
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
        恭喜你成功地安装了Xcode！继续阅读，学习它能够做什么。
    </p>
    <h3>
    	Beta版本的Xcode
    </h3>
    <p>
    	在继续描述Xcode的能量之前，值得花几分钟去了解一下Beta版本的Xcode。
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
    	注意你可以在稳定版的Xcode旁，安装一个beta版本的Xcode。所以在没有为升级做好准备的项目上继续工作完全没有问题。
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
    	Xcode是一个集成开发环境，这意味着它是一个你需要的从源码编辑，编译，到debug和UI设计的所有开发的工具的集合。
    </p>
    <p>
    	当你打开Xcode时，它会让你创建一个新项目，或打开一个已存在的项目。你也可以通过双击目录中的Xcode project或workspace来打开一个已存在的项目：
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
    	在这个教程中的大部分，你将通过一个样本项目来游览Xcode，但是首先的第一件事情 - 你必须创建一个“Hello World”app来了解新的平台！
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
    	模板选择器允许你来决定Xcode怎么配置你的新工程。在
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
        ，让language被设置为
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
    	这将创建一个新的空项目，准备好为你打造令人惊叹的app。你想做第一件的事，是build和运行来检查它是否工作正常。
    </p>
    <h3>
        运行你的app
    </h3>
    <p>
    	不管你是打开一个已存在的，还是创建一个新的app，你想做的最重要的事都是build和运行它。
    </p>
    <p>
    	这会将所有你写的code编译成机器码，打包所有app需求的资源，然后执行。这个过程是复杂的，但幸运的是Xcode会帮你搞定。要想build和执行你的项目，只需点击工具栏上的
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
        当你第一次用Xcode build和执行app时，可能被询问你是否想要
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
    	这会在Interface Builder中打开storyboard文件 - 你会看到你全部app的概貌：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110288" src="https://koenig-media.raywenderlich.com/uploads/2015/07/hello_world_storyboard-343x500.png"
        alt="hello_world_storyboard" width="343" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/hello_world_storyboard-343x500.png 343w, https://koenig-media.raywenderlich.com/uploads/2015/07/hello_world_storyboard-219x320.png 219w, https://koenig-media.raywenderlich.com/uploads/2015/07/hello_world_storyboard.png 602w"
        sizes="(max-width: 343px) 100vw, 343px">
    </p>
    <p>
        下方的组件（被标为“View Controller”）的，代表着你app的可见的外观。你要添加一个text label到这里，来创建你的“Hello World”app。
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
        alt="drag_label" width="480" height="312" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/drag_label-480x312.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/drag_label-700x455.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/drag_label.png 1022w" sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	一个label代表一块静态的文本 - 没有用户交互 - 对于你的Hello World app来说是完美的。你并不想让它说“label”，直到你下次要升级之前。
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
    	你可能会看到label的尺寸不再合适 - 下一步你将修复，把它设到正确的位置上。
    </p>
    <p>
    	在OS X中，你定位UI原件是使用一个名叫Auto Layout的系统 - 它允许你根据它们之间的关系，指定UI原件的位置和大小。你想要摆放你的“Hello OS X!” label在窗口中央 - 因此你需要添加约束（constraints）来实现。
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
        运行
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
    	HubEvent是一个相当简单的app，但是足够来演示Xcode的核心功能。这篇教程的剩余部分将包含如下内容：
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
        中，从
        <em>
            Controllers
        </em>
        选择
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
            注意：
        </em>
        你可能需要工具栏中的按钮展示左手边栏的
        <em>
            Navigator面板
        </em>
        ，然后选择导航面板中的
        <em>
            Project navigator
        </em>
        。这些按钮已展示在上面的屏幕截图中。
    </div>
    <p>
        在Xcode窗口的主要部分，你现在可以看到相关于Window Controller的源代码。找到下面这行：
    </p>
<pre class="swift" style="font-family:monospace;">
    <span style="color: #11740a; font-style: italic;">// The shared data model</span>
    <span style="color: #a61390;">let</span> sharedDataStore <span style="color: #002200;">=</span> DataStore<span style="color: #002200;">(</span>username<span style="color: #002200;">:</span> <span style="color: #bf1d1a;">"rwenderlich"</span>, type<span style="color: #002200;">:</span> .Network<span style="color: #002200;">)</span>
</pre>
    <p>
        这行选择了GitHub事件的数据源 - 这里选择了Ray的名字（
        <code>
            rwenderlich
        </code>
        ）。
    </p>
    <p>
        尝试改变
        <code>
            rwenderlich
        </code>
        为一个不同的GitHub用户名 - 例如
        <code>
            sammyd
        </code>
        。然后，就像你刚刚选择的一样，构建并运行你的app。你就会看到在app中列出了新用户的事件：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110221" src="https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_sammyd-629x500.png"
        alt="hubevent_sammyd" width="629" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_sammyd-629x500.png 629w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_sammyd-403x320.png 403w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_sammyd.png 979w"
        sizes="(max-width: 629px) 100vw, 629px">
    </p>
    <p>
        干得好！你已经在OS X app里改变了你的第一行代码！
    </p>
    <p>
        这个文档编辑器包含了很多有力的特性来帮助你写代码，包含自动完成（autocompletion）和快速查看的文档（QuickLook documentation）。
    </p>
    <h3>
        Interface Builder
    </h3>
    <p>
        尽管你是可以完全用代码来构建一个OS X app，由于UI本来是可见的，使用这个模式并不非常直观。
    </p>
    <p>
        Xcode包含一个名叫Interface Builder (IB)的工具，这是一个全特性的可见的设计工具，让你可以从可重用的组件来构建你的UI。
    </p>
    <p>
        构建这些可见界面的文件被叫做Storyboard - 这个名称的灵感来自于电影产业。同样的方式，storyboard被用来在一个电影中描述场景，连接起来。在一个app钟，一个storyboard描述场景和它们之间的流程（flow）。
    </p>
    <p>
        要在Interface Builder中看到storyboard，请在
        <em>
            Project navigator
        </em>
        中选择
        <em>
            Main.storyboard
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter wp-image-110239 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/07/storyboard-700x492.png"
        alt="" width="700" height="492" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/storyboard-700x492.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/storyboard-456x320.png 456w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        这个storyboard中包含了整个app的布局。你可以看到怎么从底部的JSON观察器中被分离出这个app顶部的列表作为一个分离的实体。
    </p>
    <p>
        要得到一个interface builder的快速的体验，你可以改变icon的颜色在左手边的栏中。
    </p>
    <p>
        尽管可以通过收缩来获得一个全部storyboard的好的视角，但是你不能编译一个收缩的storyboard。使用
        <em>
            ⌘+
        </em>
        键来将其收缩到
        <em>
            EventList VC
        </em>
        。这是包含列表的场景：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110218" src="https://koenig-media.raywenderlich.com/uploads/2015/07/eventlist-700x320.png"
        alt="eventlist" width="700" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/eventlist-700x320.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/eventlist-480x219.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/eventlist.png 946w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        使用左下角的按钮来
        <em>
            显示Document Outline
        </em>
        。这是一个在Interface Builder左手边的面板，会向你展示构成当前场景的组件的层级。
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110228" src="https://koenig-media.raywenderlich.com/uploads/2015/07/select_icon-345x500.png"
        alt="select_icon" width="345" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/select_icon-345x500.png 345w, https://koenig-media.raywenderlich.com/uploads/2015/07/select_icon-221x320.png 221w, https://koenig-media.raywenderlich.com/uploads/2015/07/select_icon.png 782w"
        sizes="(max-width: 345px) 100vw, 345px">
    </p>
    <p>
        如果你在列表视图点击紫色的
        <em>
            ⌘
        </em>
        符号，你就会高亮在
        <em>
            Document Outline
        </em>
        中的相应的
        <em>
            列表单元格视图
        </em>
        。要是你想访问在这个单元格
        <i>
            中
        </i>
        的text field，再次点击
        <em>
            ⌘
        </em>
        。现在你就有了行的选择在之前的图像中。
    </p>
    <p>
        你选择了这个text field之后，你就可以配置各种相关于它的属性，这会决定它的外观。
    </p>
    <p>
        如果在Xcode右手边底部的
        <em>
            Utilities
        </em>
        面板不可见， 使用工具栏中的按钮来展示它：
    </p>
    <p>
        <img class="aligncenter size-full wp-image-110233" src="https://koenig-media.raywenderlich.com/uploads/2015/07/utilities_button.png"
        alt="utilities_button" width="220" height="66">
    </p>
    <p>
        这个面板可以展示很多inspectors（检查器），但是你现在想要的那个是
        <em>
            Atrributes Inspector
        </em>
        。选择它，你会找到
        <em>
            Text Color
        </em>
        属性：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110210" src="https://koenig-media.raywenderlich.com/uploads/2015/07/attributes_inspector-337x500.png"
        alt="attributes_inspector" width="337" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/attributes_inspector-337x500.png 337w, https://koenig-media.raywenderlich.com/uploads/2015/07/attributes_inspector-216x320.png 216w, https://koenig-media.raywenderlich.com/uploads/2015/07/attributes_inspector.png 520w"
        sizes="(max-width: 337px) 100vw, 337px">
    </p>
    <p>
        点击紫色的条，你会看到一个颜色的面板。使用它来选择一个不同的颜色 - 例如黄色：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110212" src="https://koenig-media.raywenderlich.com/uploads/2015/07/color_panel-290x500.png"
        alt="color_panel" width="290" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/color_panel-290x500.png 290w, https://koenig-media.raywenderlich.com/uploads/2015/07/color_panel-186x320.png 186w, https://koenig-media.raywenderlich.com/uploads/2015/07/color_panel.png 460w"
        sizes="(max-width: 290px) 100vw, 290px">
    </p>
    <p>
        现在你可以再次build和执行
        <em>
            HubEvent
        </em>
        来查看你刚刚改变的效果：
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
        除了代码和用户交互，你的app也需要一些资产（assets）例如原图（artwork）。由于不同的屏幕类型（例如视网膜的和非视网膜的），你通常需要提供多种版本的资产。为了简化这个过程，Xcode使用
        <em>
            Asset Libraries
        </em>
        来保存和组织伴同app的资产。
    </p>
    <p>
        <em>
            HubEvent
        </em>
        早已有了一个默认的asset library，名叫
        <em>
            Images.xcassets
        </em>
        。在
        <em>
            Project navigator
        </em>
        中选择它来展示它的内容：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110208" src="https://koenig-media.raywenderlich.com/uploads/2015/07/asset_library-700x247.png"
        alt="asset_library" width="700" height="247" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/asset_library-700x247.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/asset_library-480x170.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/asset_library.png 1126w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        当你创建一个新的app时，它的模板就会包含一个asset library，并只有一个入口 - app的logo。这正是
        <em>
            HubEvent
        </em>
        的状态。你可以通过右击library左侧的窗格，看到不同的你可以创建的资产类型：
    </p>
    <p>
        <img class="aligncenter wp-image-110209 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/07/asset_types-285x320.png"
        alt="asset_types" width="285" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/asset_types-285x320.png 285w, https://koenig-media.raywenderlich.com/uploads/2015/07/asset_types-445x500.png 445w, https://koenig-media.raywenderlich.com/uploads/2015/07/asset_types.png 532w"
        sizes="(max-width: 285px) 100vw, 285px">
    </p>
    <p>
        当前
        <em>
            HubEvent
        </em>
        的app图标是默认的OS X图标：
    </p>
    <p>
        <img class="aligncenter size-full wp-image-110226" src="https://koenig-media.raywenderlich.com/uploads/2015/07/original_icon.png"
        alt="original_icon" width="126" height="144">
    </p>
    <p>
        因为app icon是由asset catalog提供的，你可以用一些更合适的来替换它。点击
        <em>
            AppIcon
        </em>
        资产：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110206" src="https://koenig-media.raywenderlich.com/uploads/2015/07/appicon-700x328.png"
        alt="appicon" width="700" height="328" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/appicon-700x328.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/appicon-480x225.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/appicon.png 1444w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        当你为一个app提供icon时，你必须为围绕这个系统使用 提供多种尺寸和分辨率，作为一个演示，你将添加这些尺寸中的一种来查看app图标的变化。
    </p>
    <p>
        使用Finder来在你刚下载和解压的目录中找到
        <em>
            rw
        </em>
        <em>
            _
        </em>
        <em>
            icon.png
        </em>
        。然后将其从Finder中拖拽到在
        <em>
            AppIcon
        </em>
        资产，
        <em>
            Mac 512pt 2x
        </em>
        的单元格中的
        <em>
            AppIcon
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110207" src="https://koenig-media.raywenderlich.com/uploads/2015/07/appicon_updated-700x320.png"
        alt="appicon_updated" width="700" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/appicon_updated-700x320.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/appicon_updated-480x219.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/appicon_updated.png 1444w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        像这样地提供一个单独的图像通常都是不合适的。在真实的应用中你应该提供全部版本的icon。
    </div>
    <p>
        现在再次build和运行app，你将在dock中看到更新的图标：
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
        没有人有能力，让每次写的代码都能够完美运行，因此你很有可能需要花费一些时间来修复代码中的问题。你会很快发现，能够在特定的那行代码停下来，并调查变量的值是非常有用的。这恰恰就是debugger所提供的功能。
    </p>
    <p>
        Xcode在这里再次提供猎头帮助。它有一个整合的debugger，使得在运行时研究（investigation）你的代码非常容易。为了演示它的一些功能，你要使用它：
    </p>
    <p>
        通过选择
        <em>
            Project navigator
        </em>
        上的
        <em>
            Value Transformers\CodeStringFormattingTransformer.swift
        </em>
        来打开它。
    </p>
    <p>
        找到下面这行代码：
    </p>
    <pre class="swift" style="font-family:monospace;">
        <span style="color: #a61390;">return</span> <span style="color: #400080;">NSAttributedString</span><span style="color: #002200;">(</span>string<span style="color: #002200;">:</span> unescaped, attributes<span style="color: #002200;">:</span> attributes<span style="color: #002200;">)</span>
    </pre>
    <p>
        <em>
            点击
        </em>
        这行代码左边的“沟”（gutter）来插入一个
        <em>
            断点
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-full wp-image-110211" src="https://koenig-media.raywenderlich.com/uploads/2015/07/breakpoint.png"
        alt="breakpoint" width="672" height="64" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/breakpoint.png 672w, https://koenig-media.raywenderlich.com/uploads/2015/07/breakpoint-480x46.png 480w"
        sizes="(max-width: 672px) 100vw, 672px">
    </p>
    <p>
        断点将标记你代码中的这行在执行时停下。你的app会在此刻暂停来让你研究它的状态。
    </p>
    <p>
        <em>
            Build并执行
        </em>
        app。你将看到app被启动，在Xcode进入前台之前。你会看到你添加断点的这行代码被高亮了起来：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110219" src="https://koenig-media.raywenderlich.com/uploads/2015/07/highlighted_line-700x39.png"
        alt="highlighted_line" width="700" height="39" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/highlighted_line-700x39.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/highlighted_line-480x27.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/highlighted_line.png 1082w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        这意味着你的app已经启动运行，并到达了代码中的这行。它暂停在了此处，让你可以研究。
    </p>
    <p>
        Xcode底部的窗格展示给你当前执行时变量的状态，包括它们所含的变量。
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110214" src="https://koenig-media.raywenderlich.com/uploads/2015/07/debug_pane-700x186.png"
        alt="debug_pane" width="700" height="186" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/debug_pane-700x186.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/debug_pane-480x127.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/debug_pane.png 1296w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        这个方法是用来从下载自GitHub API的JSON中移除转义的字符。你可以看到输入的字符串
        <code>
            s
        </code>
        和合成的字符串
        <code>
            unescaped
        </code>
        。
    </p>
    <p>
        你可以使用
        <em>
            stepover
        </em>
        按钮前进到执行的下一行：
    </p>
    <p>
        <img class="aligncenter size-full wp-image-110230" src="https://koenig-media.raywenderlich.com/uploads/2015/07/stepover.png"
        alt="stepover" width="56" height="52">
    </p>
    <p>
        或使用
        <em>
            continue
        </em>
        按钮来继续程序的进行：
    </p>
    <p>
        <img class="aligncenter size-full wp-image-110213" src="https://koenig-media.raywenderlich.com/uploads/2015/07/continue.png"
        alt="continue" width="52" height="50" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/continue.png 52w, https://koenig-media.raywenderlich.com/uploads/2015/07/continue-32x32.png 32w"
        sizes="(max-width: 52px) 100vw, 52px">
    </p>
    <p>
        注意，继续会接着执行程序直到遇到另一个断点。
    </p>
    <p>
        为了移除一个断点，你可以将它拖拽出“沟”（gutter），直到指针变成了一个
        <em>
            x
        </em>
        。
    </p>
    <h3>
        使用debugger来修复一个bug
    </h3>
    <p>
        为了看到debug怎么工作，你将修复一个真实世界中的bug！
        你得到报告说，如果你将HubEvent从基于网络改变为基于磁盘的数据源，然后发现它忽视了你的选择 - 仍是查询网络。你的工作是找到并修复它。
    </p>
    <p>
        首先，为了改变app到磁盘模式来替换网络模式，打开
        <em>
            WindowController.swift
        </em>
        ，定位到创建
        <code>
            sharedDataStore
        </code>
        的那行，更新它到如下的样子：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">let</span> sharedDataStore <span style="color: #002200;">=</span> DataStore<span style="color: #002200;">(</span>username<span style="color: #002200;">:</span> <span style="color: #bf1d1a;">"rwenderlich"</span>, type<span style="color: #002200;">:</span> .Disk<span style="color: #002200;">)</span>
    </pre>
    <p>
        现在运行app，确认数据就是从网络获取的（磁盘上的数据是2015年四月获取的）。
    </p>
    <p>
        为了debug这个问题，你要添加在数据存储的地方添加一个断点，来找到发生了什么。打开
        <em>
            DataStore.swift
        </em>
        ，然后添加一个断点在包含
        <code>
            super.init()
        </code>
        的这行。
    </p>
    <p>
        运行app，并等待停到断点这里。使用debug来在
        <code>
            self
        </code>
        中定位
        <code>
            dataProvider
        </code>
        属性：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110313" src="https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_dataprovider-480x254.png"
        alt="debugging_dataprovider" width="480" height="254" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_dataprovider-480x254.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_dataprovider-700x370.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_dataprovider.png 960w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        注意靠近它的类型是
        <code>
            GitHubData.GitHubDataNetworkProvider
        </code>
        。这听起来不对 - 为何它从磁盘读取的时候，使用一个叫做网络的对象。
    </p>
    <p>
        现在更进一步地看下这个文件，你会找到
        <code>
            dataProvider
        </code>
        这个对象是从哪里创建的：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">switch</span> type <span style="color: #002200;">{</span>
    <span style="color: #a61390;">case</span> .Network<span style="color: #002200;">:</span>
      dataProvider <span style="color: #002200;">=</span> GitHubDataNetworkProvider<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
    <span style="color: #a61390;">case</span> .Disk<span style="color: #002200;">:</span>
      dataProvider <span style="color: #002200;">=</span> GitHubDataNetworkProvider<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
    <span style="color: #002200;">}</span>
    </pre>
    <p>
        这是一个选择哪种提供者需要被创建的转换语句 - 为何它为
        <code>
            .Disk
        </code>
        创建的是
        <code>
            GitHubDataNetworkProvider
        </code>
        类型？这就是bug！
    </p>
    <p>
        替换
        <code>
            .Disk
        </code>
        到如下的样子：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">case</span> .Disk<span style="color: #002200;">:</span>
      dataProvider <span style="color: #002200;">=</span> GitHubDataFileProvider<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
    </pre>
    <p>
        现在再次运行app，它会停到相同的断点上。再次检查
        <code>
            dataProvider
        </code>
        属性的类型：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-110314" src="https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_fixed-480x166.png"
        alt="debugging_fixed" width="480" height="166" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_fixed-480x166.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_fixed-700x242.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/debugging_fixed.png 960w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        这个类型看起来就正确了 - 使用
        <em>
            Continue program execution
        </em>
        按钮来运行app：
    </p>
    <p>
        <img class="aligncenter wp-image-110315 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_disk-479x500.png"
        alt="hubevent_disk" width="479" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_disk-479x500.png 479w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_disk-307x320.png 307w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_disk-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/07/hubevent_disk.png 1002w"
        sizes="(max-width: 479px) 100vw, 479px">
    </p>
    <p>
        哇！现在app从磁盘中读取了，而不是从网络中。干得好 - 你修复了你的第一个OS X bug！
    </p>
    <h2>
        文档
    </h2>
    <p>
        Xcode有一些整合的方法去访问系统frameworks的文档。第一是展示包含关于类或方法的最显著信息的提示工具的能力。
    </p>
    <p>
        例如，打开
        <em>
            Controllers\WindowController.swift
        </em>
        在
        <code>
            transformedValueClass()
        </code>
        方法里，
        <em>
            Option-点击
        </em>
        <code>
            NSString
        </code>
        ：
    </p>
    <p>
        <img class="aligncenter wp-image-110232 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/07/tooltip-480x194.png"
        alt="tooltip" width="480" height="194" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/tooltip-480x194.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/07/tooltip-700x282.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/tooltip.png 1022w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        第二种访问文档的方法会展示完整的文档在一个专用的浏览器中。要访问它，点击
        <em>
            Reference
        </em>
        在工具提示的底部，或点击
        <em>
            Window
        </em>
        <em>
            \
        </em>
        <em>
            Documentation and Reference
        </em>
        菜单。然后搜获
        <code>
            NSString
        </code>
        来获取文档：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-110216" src="https://koenig-media.raywenderlich.com/uploads/2015/07/doc_browser-700x339.png"
        alt="doc_browser" width="700" height="339" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/doc_browser-700x339.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/07/doc_browser-480x233.png 480w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        使用文档来修复一个bug
    </h2>
    <p>
        让我们来看一看你可以怎么使用Xcode的文档来修复另一个bug。
    </p>
    <p>
        当HubEvent第一次加载时，你将注意到在table和JSON视图之间的分隔器被放置得非常高：
    </p>
    <p>
        <img class="aligncenter wp-image-110310 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/07/divider_initial-479x500.png"
        alt="divider_initial" width="479" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/divider_initial-479x500.png 479w, https://koenig-media.raywenderlich.com/uploads/2015/07/divider_initial-306x320.png 306w, https://koenig-media.raywenderlich.com/uploads/2015/07/divider_initial-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/07/divider_initial.png 1002w"
        sizes="(max-width: 479px) 100vw, 479px">
    </p>
    <p>
        如果你想把分隔器拖拽下来，你将看到它会“咬合”（snaps）到窗口中央，然后就固定不动了。这是你想要的效果，但是在app启动时，应该让分隔器在正确的位置上。
    </p>
    <p>
        你可以通过在
        <em>
            SplitViewController.swift
        </em>
        文件中添加一行到
        <code>
            viewWillAppear()
        </code>
        方法。使用文档浏览器来搜索
        <code>
            NSSplitView
        </code>
        ，阅读
        <code>
            setPosition(\_:, ofDividerAtIndex:)
        </code>
        方法的相关内容。然后使用这个方法在
        <code>
            splitView
        </code>
        property （在之前提到的方法），传递
        <code>
            view.bounds.height / 2.0
        </code>
        在这个位置。
    </p>
    <pre class="swift" style="font-family:monospace;">splitView.setPosition<span style="color: #002200;">(</span>view.bounds.height <span style="color: #002200;">/</span> <span style="color: #2400d9;">2.0</span>, ofDividerAtIndex<span style="color: #002200;">:</span> <span style="color: #2400d9;">0</span><span style="color: #002200;">)</span>
    </pre>
    <p>
        &nbsp;
    </p>
    <h2>
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
        <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Mac%20OS%20X%20Development%20Tutorial%20for%20Beginners%20Part%202%20-%20OS%20X%20App%20Anatomy.md"
        sl-processed="1">
            下一篇文章
        </a>
        中，你将学习对一个app的剖析，并最终创建出你的第一个OS X app。
    </p>
    <p>
        可以在这里获取苹果大量的OS X官方文档
        <a href="https://developer.apple.com/library/mac/navigation/" sl-processed="1">
            Developer Portal
        </a>
        。
    </p>
</div>
