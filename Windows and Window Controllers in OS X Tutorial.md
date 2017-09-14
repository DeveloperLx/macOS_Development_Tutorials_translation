#### [原文地址](https://www.raywenderlich.com/111947/windows-and-window-controllers-in-os-x-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <img class="alignright size-full wp-image-111951" src="https://koenig-media.raywenderlich.com/uploads/2015/08/Windows250x250.png"
        alt="Windows250x250" width="250" height="250" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/Windows250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2015/08/Windows250x250-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/08/Windows250x250-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2015/08/Windows250x250-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2015/08/Windows250x250-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
    	window是相应于全部OS X app的UI的“容器”。它们定义了你的app当前负责的屏幕的区域，用户可以使用容易理解的多任务范式（multi-tasking paradigm）来进行交互。OS X app总是落入如下种类中的一种：
    </p>
    <ul>
        <li>
            <em>
                单窗口的工具
            </em>
            ，就像计算器
        </li>
        <li>
            <em>
                单窗口，库风格的“鞋盒
            </em>
            ，就像Photos
        </li>
        <li>
            <em>
                多窗口基于文档的
            </em>
            ，就像TextEdit
        </li>
    </ul>
    <p>
        不管是哪种类型的app，几乎每种OS X app都利用了
        <em>
            MVC
        </em>
        (Model-View-Controller)，一种核心的设计模式。
    </p>
    <p>
        在Cocoa中，window是
        <code>
            NSWindow
        </code>
        类的一个实例，相应的控制器对象则是
        <code>
            NSWindowController
        </code>
        类的实例。在一个有着很好设计的app中，你通常（typically）都会使用一对一关系的window和它的controller。这个模型层会根据你app类型和设计各有不同。
    </p>
    <p>
        在这个OS X教程中的window和window controller，你将创建
        <em>
            BabyScript
        </em>
        ，一个多窗口的基于文档的app，它的灵感来自于TextEdit。在这个过程中，你将学到：
    </p>
    <ul>
        <li>
            Window 和 window controller
        </li>
        <li>
            文档的架构
        </li>
        <li>
            NSTextView
        </li>
        <li>
            模型window
        </li>
        <li>
            菜单栏和菜单项
        </li>
    </ul>
    <h2>
        预备知识
    </h2>
    <p>
        这篇教程是面向新手的。话虽如此，它要求下列的基础知识：
    </p>
    <ul>
        <li>
            Swift
        </li>
        <li>
            Xcode，特别的，storyboards
        </li>
        <li>
            创建一个简答的 Mac (OS X) app
        </li>
    </ul>
    <p>
        如果你对上面的任意一项都不熟悉，你可能要复习（brush up）一些这个网站上的其它教程：
    </p>
    <ul>
        <li>
            <a title=" Swift Language Tutorials " href="http://www.raywenderlich.com/category/swift"
            target="_blank" sl-processed="1">
                Swift语言教程
            </a>
        </li>
        <li>
            <a title="macOS X 初学者开发教程 第一部分 Xcode介绍"
            href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Mac%20OS%20X%20Development%20Tutorial%20for%20Beginners%20Part%201%20-%20Intro%20to%20Xcode.md" target="_blank" sl-processed="1">
                macOS X 初学者开发教程 第一部分 Xcode介绍
            </a>
        </li>
        <li>
            <a title="macOS X 初学者开发教程 第二部分 OS X App剖析"
            href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Mac%20OS%20X%20Development%20Tutorial%20for%20Beginners%20Part%202%20-%20OS%20X%20App%20Anatomy.md" target="_blank" sl-processed="1">
                macOS X 初学者开发教程 第二部分 OS X App剖析
            </a>
        </li>
        <li>
            <a title="macOS X 初学者开发教程 第三部分 你的第一个OS X App"
            href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Mac%20OS%20X%20Development%20Tutorial%20for%20Beginners%20Part%203%20-%20Your%20First%20OS%20X%20App.md" target="_blank" sl-processed="1">
                macOS X 初学者开发教程 第三部分 你的第一个OS X App
            </a>
        </li>
    </ul>
    <h2>
        开始吧！
    </h2>
    <p>
        运行
        <em>
            Xcode
        </em>
        ，并选择
        <em>
            File / New / Project…
        </em>
        。选择
        <em>
            OS X / Application / Cocoa Application
        </em>
        ，然后点击
        <em>
            Next
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/1-CocoaApp.png"
        sl-processed="1">
            <img class="aligncenter wp-image-112376 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/08/1-CocoaApp-448x320.png"
            alt="1-CocoaApp" width="448" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/1-CocoaApp-448x320.png 448w, https://koenig-media.raywenderlich.com/uploads/2015/08/1-CocoaApp-700x500.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/1-CocoaApp.png 734w"
            sizes="(max-width: 448px) 100vw, 448px">
        </a>
    </p>
    <p>
        在下一屏，填写如下所示的字段，但输入你自己的名字（或超级英雄的别名），而不要像我一样。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/2-XcodeTemplate.png"
        sl-processed="1">
            <img class="aligncenter wp-image-112377 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/08/2-XcodeTemplate-450x320.png"
            alt="2-XcodeTemplate" width="450" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/2-XcodeTemplate-450x320.png 450w, https://koenig-media.raywenderlich.com/uploads/2015/08/2-XcodeTemplate-700x497.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/2-XcodeTemplate.png 732w"
            sizes="(max-width: 450px) 100vw, 450px">
        </a>
    </p>
    <p>
        点击
        <em>
            Next
        </em>
        并保存你的项目。
    </p>
    <p>
        运行项目，你将看到：
    </p>
    <p>
        <img class="aligncenter size-full wp-image-112378" src="https://koenig-media.raywenderlich.com/uploads/2015/08/3-FirstWindow.png"
        alt="3-FirstWindow" width="480" height="292">
    </p>
    <p>
        为了打开更多的文档，选择
        <em>
            File / New
        </em>
        。全部的文档都位于
        <i>
            同一位置
        </i>
        ，因此你只有在点击和拖拽他们时，才会看到顶部的文档。这不是理想的效果，所以把它添加到你的to-do列表中，但先不要钻进去。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/4-Open-Many.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112519" src="https://koenig-media.raywenderlich.com/uploads/2015/08/4-Open-Many-700x287.png"
            alt="4-Open-Many" width="700" height="287" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/4-Open-Many-700x287.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/4-Open-Many-480x197.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/4-Open-Many.png 940w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        也是可以使用
        <em>
            Windows
        </em>
        菜单来讲window带到前台。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/5-Bring-ToFront.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112520" src="https://koenig-media.raywenderlich.com/uploads/2015/08/5-Bring-ToFront-700x292.png"
            alt="5-Bring-ToFront" width="700" height="292" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/5-Bring-ToFront-700x292.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/5-Bring-ToFront-480x200.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/5-Bring-ToFront.png 930w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <h2>
        文档：在Hood之下
    </h2>
    <p>
        现在你已经看到了它在行动，让我们花几分钟来看看它的工作原理。
    </p>
    <h3>
        文档结构
    </h3>
    <p>
        文档是在内存中的数据的容器，你可以在window中查看它。最终，它可以从磁盘或iCould中写入和读出。从程序上讲，文档是一个
        <code>
            NSDocument
        </code>
        类的实例，充当数据对象的控制器 - 也就是说 - 相应于文档的模型。
    </p>
    <p>
        在文档架构中的其它的两个主要的类是
        <code>
            NSWindowcontroller
        </code>
        和
        <code>
            NSDocumentController
        </code>
        。这些是它们的角色：
    </p>
    <ul>
        <li>
            <code>
                NSDocument
            </code>
            ：穿件，展示及保存文档数据
        </li>
        <li>
            <code>
                NSWindowController
            </code>
            ：管理展示文档的那个window
        </li>
        <li>
            <code>
                NSDocumentController
            </code>
            ：管理app中全部的文档对象
        </li>
    </ul>
    <p>
        还是可视化比较好，所以这里有一个表，来展示这些类如何在一起工作：
        <br>
        <img class="aligncenter size-full wp-image-112108" src="https://koenig-media.raywenderlich.com/uploads/2015/08/DocArchitecture.png"
        alt="DocArchitecture" width="576" height="281" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/DocArchitecture.png 576w, https://koenig-media.raywenderlich.com/uploads/2015/08/DocArchitecture-480x234.png 480w"
        sizes="(max-width: 576px) 100vw, 576px">
    </p>
    <h3>
        禁用文档的保存和打开
    </h3>
    <p>
        文档的建构也提供了文档的保存和打开机制。
    </p>
    <p>
        在
        <em>
            Document.swift
        </em>
        中，你会发现实现为空的
        <code>
            dataOfType
        </code>
        ，它是为了写入的，还有
        <code>
            readFromData
        </code>
        ，是为了读出的。保存和打开文档是在这个教程的范围之外的，因此你要做出一些变化来避免令人困惑的行为的出现。
    </p>
    <p>
        在
        <em>
            Document.swift
        </em>
        中，
        <i>
            移除
        </i>
        <code>
            autosavesInPlace
        </code>
        ：
    </p>
    <pre class="swift" style="font-family:monospace;">  <span style="color: #a61390;">override</span> <span style="color: #a61390;">class</span> <span style="color: #a61390;">func</span> autosavesInPlace<span style="color: #002200;">(</span><span style="color: #002200;">)</span> <span style="color: #002200;">-&amp;</span>gt; <span style="color: #a61390;">Bool</span> <span style="color: #002200;">{</span>
    <span style="color: #a61390;">return</span> <span style="color: #a61390;">true</span>
  <span style="color: #002200;">}</span></pre>
    <p>
        现在你将禁掉全部关于打开和保存的菜单项，但是在你行动之前，注意到全部你所期望的功能早已在这里了。例如，选择
        <em>
            File / Open
        </em>
        并find的对话框，包括控制器，侧边栏，工具栏等等已经都在这里了：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/OpenDialog.png"
        sl-processed="1">
            <img class="aligncenter wp-image-112527 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/08/OpenDialog-480x309.png"
            alt="OpenDialog" width="480" height="309" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/OpenDialog-480x309.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/OpenDialog-700x451.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/OpenDialog.png 712w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        一个菜单项，当没有定义动作时是无用的。相同的禁用的效果同样也发生在，当响应者链中没有相应的能够响应那个动作selector的对象时。
    </p>
    <p>
        因此，你将断开需要禁用的，为菜单项定义的动作。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/no-saving-for-you.jpg"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113579" src="https://koenig-media.raywenderlich.com/uploads/2015/08/no-saving-for-you.jpg"
            alt="no-saving-for-you" width="300" height="295" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/no-saving-for-you.jpg 300w, https://koenig-media.raywenderlich.com/uploads/2015/08/no-saving-for-you-32x32.jpg 32w, https://koenig-media.raywenderlich.com/uploads/2015/08/no-saving-for-you-64x64.jpg 64w"
            sizes="(max-width: 300px) 100vw, 300px">
        </a>
    </p>
    <p>
        在storyboard中，在
        <em>
            Main Menu
        </em>
        的
        <em>
            Application Scene
        </em>
        ，选择
        <em>
            File / Open
        </em>
        。
    </p>
    <p>
        选择
        <em>
            Connections Inspector
        </em>
        并点击
        <em>
            Open
        </em>
        。正如你看到的，它通过
        <code>
            openDocument
        </code>
        selector连接到了第一响应者，也就是在响应者链中，第一个响应这个selector的对象。就像下面这样，通过点击 
        <em>
            x
        </em>
        来删除这个连接：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/TargetAction.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112525" src="https://koenig-media.raywenderlich.com/uploads/2015/08/TargetAction-700x427.png"
            alt="TargetAction" width="700" height="427" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/TargetAction-700x427.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/TargetAction-480x293.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/TargetAction.png 751w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        对
        <em>
            Save
        </em>
        ，
        <em>
            Save As
        </em>
        和
        <em>
            Revert to Saved
        </em>
        重复该步骤。
    </p>
    <p>
        运行项目，切换到
        <em>
            Open
        </em>
        菜单，并检查它是否看起来像下面这样：
    </p>
    <p>
        <img class="aligncenter size-full wp-image-112528" src="https://koenig-media.raywenderlich.com/uploads/2015/08/7-OpenMenu.png"
        alt="7-OpenMenu" width="178" height="225">
    </p>
    <h2>
        Window的位置
    </h2>
    <p>
        当你运行BabyScript的时候，window会在靠近左边，但稍低于屏幕中心的的位置打开。
    </p>
    <p>
        为何它选择了这个位置？
    </p>
    <p>
        找到storyboard，在
        <em>
            outline view
        </em>
        中选择
        <em>
            Window
        </em>
        ，然后选择
        <em>
            Size Inspector
        </em>
        。运行BabyScript - 或将它带到前面 - 你现在看到的屏幕应该是下面这样的：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/5-WindowSizeInspector.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112379" src="https://koenig-media.raywenderlich.com/uploads/2015/08/5-WindowSizeInspector-625x500.png"
            alt="5-WindowSizeInspector" width="625" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/5-WindowSizeInspector-625x500.png 625w, https://koenig-media.raywenderlich.com/uploads/2015/08/5-WindowSizeInspector-400x320.png 400w, https://koenig-media.raywenderlich.com/uploads/2015/08/5-WindowSizeInspector.png 1280w"
            sizes="(max-width: 625px) 100vw, 625px">
        </a>
    </p>
    <p>
        在
        <em>
            Initial Position
        </em>
        下输入
        <i>
            X
        </i>
        和
        <i>
            Y
        </i>
        的数值。这是设置window的位置的一种方法。你也可以通过拖动下面灰色的矩形直观地（graphically）设置它。
    </p>
    <p>
        <img class="aligncenter size-full wp-image-112397" src="https://koenig-media.raywenderlich.com/uploads/2015/08/6-QuartzCoordinates.png"
        alt="6-QuartzCoordinates" width="658" height="447" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/6-QuartzCoordinates.png 658w, https://koenig-media.raywenderlich.com/uploads/2015/08/6-QuartzCoordinates-471x320.png 471w"
        sizes="(max-width: 658px) 100vw, 658px">
    </p>
    <div class="note">
        <p>
            <em>
                注意
            </em>
            ：在Cocoa中，一个可见对象(window, view, control等)的原点位于
            <i>
                左下
            </i>
            角。在向上和向右的方向上，坐标值会增加。
        </p>
        <p>
            相反地，在很多图形环境下，尤其是iOS，其原点是位于
            <i>
                上
            </i>
            左角的，则在向下和向右的方向上，坐标值会增加。
        </p>
    </div>
    <p>
        假设你期望你的window打开的位置，是从左上角水平和垂直偏移200个点。你可以用Xcode在window中的
        <em>
            Size Inspector
        </em>
        来设置它，或依靠编程来实现。
    </p>
    <h3>
        使用Interface Builder来设置window的位置
    </h3>
    <p>
        基本可以打赌，用户会在各种尺寸的屏幕上运行BabyScript。由于你的app没有一个水晶球，能在编译时看到它将打开在一个怎样的屏幕尺寸上，因此Xcode使用了一个虚拟的屏幕尺寸，和一个类似于自动布局的概念，来在运行时决定window的位置。
    </p>
    <p>
        为了设置这个位置，你将用到
        <em>
            Initial Position
        </em>
        下的两个值
        <em>
            X
        </em>
        、
        <em>
            Y
        </em>
        ，和两个下拉式（drop-down）菜单。
    </p>
    <p>
        找到
        <em>
            Initial Position
        </em>
        ，依据屏幕坐标系来设置window的打开位置。给
        <em>
            X
        </em>
        和
        <em>
            Y
        </em>
        都输入200，并在下拉式菜单中选择
        <em>
            Fixed from Left
        </em>
        和
        <em>
            Fixed from Bottom
        </em>
        。这就设置了window在x和y的方向上都是200个点的偏移。
    </p>
    <p>
        <img class="aligncenter wp-image-119246 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/09/set_initial_position-241x500.png"
        alt="" width="241" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/set_initial_position-241x500.png 241w, https://koenig-media.raywenderlich.com/uploads/2015/09/set_initial_position-154x320.png 154w, https://koenig-media.raywenderlich.com/uploads/2015/09/set_initial_position.png 512w"
        sizes="(max-width: 241px) 100vw, 241px">
    </p>
    <p>
        运行项目，你应当看到：
    </p>
    <p>
        <img class="aligncenter wp-image-119247 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/09/demonstrating_position-452x320.png"
        alt="" width="452" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/demonstrating_position-452x320.png 452w, https://koenig-media.raywenderlich.com/uploads/2015/09/demonstrating_position-700x495.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/demonstrating_position.png 1564w"
        sizes="(max-width: 452px) 100vw, 452px">
    </p>
    <p>
        跟随下面的步骤来让window定位到左上角：
    </p>
    <ol>
        <li>
            在预览图中拖拽灰色的矩形到虚拟屏幕的左上角 - 这就改变了初始的位置。
        </li>
        <li>
            在
            <em>
                X
            </em>
            处输入200，在
            <em>
                Y
            </em>
            这里，输入最大的值“负200”，在这个case中就是557.
        </li>
        <li>
            在底部的下拉菜单中选择
            <em>
                Fixed from Top
            </em>
            。
        </li>
    </ol>
    <p>
        下面右侧的图片展示了你应该输入的地方和值：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/Window757557.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113030" src="https://koenig-media.raywenderlich.com/uploads/2015/08/Window757557-581x500.png"
            alt="Window757557" width="581" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/Window757557-581x500.png 581w, https://koenig-media.raywenderlich.com/uploads/2015/08/Window757557-372x320.png 372w, https://koenig-media.raywenderlich.com/uploads/2015/08/Window757557.png 646w"
            sizes="(max-width: 581px) 100vw, 581px">
        </a>
    </p>
    <div class="note">
        <p>
            <em>
                注意
            </em>
            ：OS X在每次启动时会记忆window的位置。为了查看你做的变化，你需要确保关掉了app的window - 而不仅仅是重新运行。
        </p>
    </div>
    <p>
        关掉所有的窗口，然后运行项目。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/10-Window200x200Xcode.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112575" src="https://koenig-media.raywenderlich.com/uploads/2015/08/10-Window200x200Xcode-625x500.png"
            alt="10-Window200x200Xcode" width="625" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/10-Window200x200Xcode-625x500.png 625w, https://koenig-media.raywenderlich.com/uploads/2015/08/10-Window200x200Xcode-400x320.png 400w, https://koenig-media.raywenderlich.com/uploads/2015/08/10-Window200x200Xcode.png 1280w"
            sizes="(max-width: 625px) 100vw, 625px">
        </a>
    </p>
    <h3>
        编程设置window的位置
    </h3>
    <p>
        现在你要完成和刚刚在Interface Builder中所完成的一样的工作，但这一你要通过编程来完成。
    </p>
    <p>
        采取“硬的方式”（hard way）的原因有两个。第一，你可以对
        <code>
            NSWindowController
        </code>
        有一个更好的理解。第二，它是一种更灵活和很直接的方式。
    </p>
    <p>
        在运行时，app将在得知屏幕尺寸之后执行窗口最终的位置。
    </p>
    <p>
        在
        <em>
            Project Navigator
        </em>
        中选择
        <em>
            BabyScript
        </em>
        组，然后选择
        <em>
            File / New / File..
        </em>
        。从弹出的对话框中，选择
        <em>
            OS X / Source / Cocoa Class
        </em>
        并点击
        <em>
            Next.
        </em>
        。
    </p>
    <p>
        创建一个名叫
        <code>
            WindowController
        </code>
        的新的类，让它作为
        <code>
            NSWindowController
        </code>
        的子类。不要勾选
        <em>
            XIB
        </em>
        ，将
        <em>
            Language
        </em>
        设为
        <em>
            Swift
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/11-WindowController.png"
        sl-processed="1">
            <img class="aligncenter wp-image-112585 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/08/11-WindowController-451x320.png"
            alt="11-WindowController" width="451" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/11-WindowController-451x320.png 451w, https://koenig-media.raywenderlich.com/uploads/2015/08/11-WindowController-700x497.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/11-WindowController.png 731w"
            sizes="(max-width: 451px) 100vw, 451px">
        </a>
    </p>
    <p>
        选择一个位置来保存新的未见。之后，你会看到一个新的名叫
        <em>
            WindowController.swift
        </em>
        的文件出现在了
        <em>
            BabyScript
        </em>
        组中。
    </p>
    <p>
        找到storyboard，在
        <em>
            Outline View
        </em>
        中从
        <em>
            Window Controller Scene
        </em>
        选择
        <em>
            Window Controller
        </em>
        。选择
        <em>
            Identity Inspector
        </em>
        ，再从
        <em>
            Class
        </em>
        下拉菜单中选择
        <code>
            WindowController
        </code>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/12-WindowController-2.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112598" src="https://koenig-media.raywenderlich.com/uploads/2015/08/12-WindowController-2-700x218.png"
            alt="12-WindowController-2" width="700" height="218" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/12-WindowController-2-700x218.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/12-WindowController-2-480x149.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/12-WindowController-2.png 1275w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        当
        <code>
            windowDidLoad
        </code>
        方法被调用时，这个window就完成了从storyboard加载的过程，因此这是你的任何配置都会覆盖在storyboard中的设置。
    </p>
    <p>
        打开
        <em>
            WindowController.swift
        </em>
        并用下列代码替换
        <code>
            windowDidLoad
        </code>
        方法：
    </p>
    <pre class="swift" style="font-family:monospace;">  <span style="color: #a61390;">override</span> <span style="color: #a61390;">func</span> windowDidLoad<span style="color: #002200;">(</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
    <span style="color: #a61390;">super</span>.windowDidLoad<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
    <span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> window <span style="color: #002200;">=</span> window, screen <span style="color: #002200;">=</span> window.screen <span style="color: #002200;">{</span>
      <span style="color: #a61390;">let</span> offsetFromLeftOfScreen<span style="color: #002200;">:</span> <span style="color: #400080;">CGFloat</span> <span style="color: #002200;">=</span> <span style="color: #2400d9;">20</span>
      <span style="color: #a61390;">let</span> offsetFromTopOfScreen<span style="color: #002200;">:</span> <span style="color: #400080;">CGFloat</span> <span style="color: #002200;">=</span> <span style="color: #2400d9;">20</span>
      <span style="color: #a61390;">let</span> screenRect <span style="color: #002200;">=</span> screen.visibleFrame
      <span style="color: #a61390;">let</span> newOriginY <span style="color: #002200;">=</span> CGRectGetMaxY<span style="color: #002200;">(</span>screenRect<span style="color: #002200;">)</span> <span style="color: #002200;">-</span> window.frame.height
        <span style="color: #002200;">-</span> offsetFromTopOfScreen
      window.setFrameOrigin<span style="color: #002200;">(</span><span style="color: #400080;">NSPoint</span><span style="color: #002200;">(</span>x<span style="color: #002200;">:</span> offsetFromLeftOfScreen, y<span style="color: #002200;">:</span> newOriginY<span style="color: #002200;">)</span><span style="color: #002200;">)</span>
    <span style="color: #002200;">}</span>
  <span style="color: #002200;">}</span></pre>
    <p>
        这个逻辑将window的位置定位在了其左上角距离屏幕左上角的位置上。
    </p>
    <p>
        正如你看到的，
        <code>
            NSWindowController
        </code>
        有一个
        <code>
            window
        </code>
        property，而
        <code>
            NSWindow
        </code>
        一个
        <code>
            screen
        </code>
        property。你可以使用这两个property来访问window和屏幕的几何信息（geometry）。
    </p>
    <p>
        在确定了（ascertaining）屏幕的高度之后 ，你的window的frame就被减去了期望的偏移。记住Y的值是随着你在屏幕中向上移而增大的。
    </p>
    <p>
        <code>
            visibleFrame
        </code>
        排除了被dock和菜单栏占用的区域。如果你不把这个纳入考量，你可能最终会让dock模糊掉了你的window的一部分。
    </p>
    <p>
        当你隐藏了dock和菜单的时候，
        <code>
            visibleFrame
        </code>
        可能仍然会比
        <code>
            frame
        </code>
        小，因为系统会持有了一个小的边界区域来当展示dock时进行检测。
    </p>
    <p>
        运行项目，这个window应该被设定为，距离屏幕左上角的每个方向都是20个点的位置上。
    </p>
    <h2>
        Cascading window
    </h2>
    <p>
        为了进一步提升你的window的位置，你将采用
        <em>
            Cascading Windows
        </em>
        ，意思是整理多个互相重叠的window的排列，让每个window的标题栏可以被看到。
    </p>
    <p>
        在
        <em>
            WindowController.swift
        </em>
        中，
        <code>
            WindowController
        </code>
        定义下面添加下列代码：
    </p>
    <pre class="swift" style="font-family:monospace;">  required <span style="color: #a61390;">init</span>?<span style="color: #002200;">(</span>coder<span style="color: #002200;">:</span> <span style="color: #400080;">NSCoder</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
    <span style="color: #a61390;">super</span>.<span style="color: #a61390;">init</span><span style="color: #002200;">(</span>coder<span style="color: #002200;">:</span> coder<span style="color: #002200;">)</span>
    shouldCascadeWindows <span style="color: #002200;">=</span> <span style="color: #a61390;">true</span>
  <span style="color: #002200;">}</span></pre>
    <p>
        通过覆盖
        <code>
            NSWindowController
        </code>
        的
        <code>
            required init
        </code>
        方法，你将
        <code>
            NSWindowController
        </code>
        的
        <code>
            shouldCascadeWindows
        </code>
        property设置为true。
    </p>
    <p>
        运行app，然后打开5个window。你的屏幕看起来应该就更友好些了：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/13-CascadingWindows.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112641" src="https://koenig-media.raywenderlich.com/uploads/2015/08/13-CascadingWindows-625x500.png"
            alt="13-CascadingWindows" width="625" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/13-CascadingWindows-625x500.png 625w, https://koenig-media.raywenderlich.com/uploads/2015/08/13-CascadingWindows-400x320.png 400w, https://koenig-media.raywenderlich.com/uploads/2015/08/13-CascadingWindows.png 1280w"
            sizes="(max-width: 625px) 100vw, 625px">
        </a>
    </p>
    <h2>
        将BabyScript制成一个迷你的文字处理器
    </h2>
    <p>
        现在到了这个教程最令人兴奋的部分。只需
        <i>
            两
        </i>
        行代码并添加一个
        <code>
            NSTextView
        </code>
        的控制到你window的
        <code>
            contentView
        </code>
        上，你将添加激动人心（blow your mind）的功能！
    </p>
    <h3>
        The Content View
    </h3>
    <p>
        一个window在创建时，自动地创建了两个view：一个不透明的带有边界、标题栏等的框架view，和一个通过window的
        <code>
            contentView
        </code>
        property访问的透明content view。
    </p>
    <p>
        content view是一个window的view图层的根，你可以用一个定制的view来替换这个默认的。注意，你必须使用
        <code>
            NSWindow
        </code>
        的
        <code>
            setContentView
        </code>
        方法来定位content view - 你不可以用标准的
        <code>
            NSView
        </code>
        的
        <code>
            setFrame
        </code>
        方法来定位它。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/ContentView.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112651" src="https://koenig-media.raywenderlich.com/uploads/2015/08/ContentView-440x500.png"
            alt="ContentView" width="440" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/ContentView-440x500.png 440w, https://koenig-media.raywenderlich.com/uploads/2015/08/ContentView-282x320.png 282w, https://koenig-media.raywenderlich.com/uploads/2015/08/ContentView.png 758w"
            sizes="(max-width: 440px) 100vw, 440px">
        </a>
    </p>
    <div class="note">
        <p>
            <em>
                注意
            </em>
            ：如果你是一个iOS的开发者，请注意在Cocoa中，
            <code>
                NSWindow
            </code>
            <i>
                不是
            </i>
            <code>
                NSView
            </code>
            的子类！在
            <em>
                iOS
            </em>
            中，
            <code>
                UIWindow
            </code>
            是
            <code>
                UIView
            </code>
            的一个特殊的子类。
            <code>
                UIWindow
            </code>
            它自己是view图层的根，就由它来扮演content view的角色。
        </p>
    </div>
    <h3>
        添加Text View
    </h3>
    <p>
        在storyboard的
        <code>
            contentView
        </code>
        中，通过选择并按
        <em>
            delete
        </em>
        键，
        <i>
            移除
        </i>
        那个说“Your document contents here”的text field。
    </p>
    <p>
        为了创建将要构成你的UI的主要部分的新的
        <code>
            NSTextField
        </code>
        ，跟随下列的说明：
    </p>
    <ol>
        <li>
            在storyboard中，打开
            <em>
                Object Library
            </em>
            。
        </li>
        <li>
            搜索
            <em>
                nstextview
            </em>
            。
        </li>
        <li>
            拖动
            <em>
                Text View
            </em>
            并将其放到content view上。
        </li>
        <li>
            调整text view的尺寸，让它的每边都距离content view相应边20个点。
        </li>
        <li>
            在
            <em>
                Outline View
            </em>
            中，选择
            <em>
                Bordered Scroll View
            </em>
            。注意到text view是被嵌入到了
            <em>
                Clip View
            </em>
            中，Clip View则被嵌入到了一个scroll view中。
        </li>
        <li>
            选择
            <em>
                Size Inspector
            </em>
            。输入
            <em>
                X
            </em>
            和
            <em>
                Y
            </em>
            均为20，
            <em>
                Width
            </em>
            为440，
            <em>
                Height
            </em>
            为230。
        </li>
    </ol>
    <p>
        <img class="aligncenter size-large wp-image-112655" src="https://koenig-media.raywenderlich.com/uploads/2015/08/15-TextViewCreation-625x500.png"
        alt="15-TextViewCreation" width="625" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/15-TextViewCreation-625x500.png 625w, https://koenig-media.raywenderlich.com/uploads/2015/08/15-TextViewCreation-400x320.png 400w, https://koenig-media.raywenderlich.com/uploads/2015/08/15-TextViewCreation.png 1280w"
        sizes="(max-width: 625px) 100vw, 625px">
    </p>
    <p>
        运行项目 - 你应该看到如下这样：
    </p>
    <p>
        <img class="aligncenter size-full wp-image-112657" src="https://koenig-media.raywenderlich.com/uploads/2015/08/16-EmptyText.png"
        alt="16-EmptyText" width="480" height="292">
    </p>
    <p>
        看起来那么友好，闪烁的文字插入点邀请你输入你的文本！开始你的宣言（manifesto），或仅仅让它保持简单的“Hello World”，然后选择文本。用
        <em>
            File / Copy
        </em>
        或
        <em>
            command – C
        </em>
        来拷贝它，然后粘贴几次，感受这个app！
    </p>
    <p>
        探索
        <em>
            Edit
        </em>
        和
        <em>
            Format
        </em>
        菜单来获得有用的idea。你可能会注意到
        <em>
            Font / Show Fonts
        </em>
        是被禁用的。现在你就来打开它！
    </p>
    <h3>
        启用字体面板
    </h3>
    <p>
        在故事版中，找到主菜单，点击
        <em>
            Format
        </em>
        菜单，然后是
        <em>
            Font
        </em>
        ，然后点击
        <em>
            Show Fonts
        </em>
        。
    </p>
    <p>
        找到
        <em>
            Connections Inspector
        </em>
        ，你会发现这个菜单项中没有动作被定义。这就解释了为何菜单项被禁用了，但是你该将它连接到何处？
    </p>
    <p>
        显然，这个动作早已被定义在了Xcode没有直接导入的代码中，你只是需要连接一下。
    </p>
    <p>
        右击
        <em>
            Show Fonts
        </em>
        并将其拖动到
        <em>
            Application Scene
        </em>
        的
        <em>
            First Responder
        </em>
        上，然后释放鼠标。一个带有全部动作的小型的可滚动的列表window就会弹出。找到并选择
        <code>
            orderFrontFontPanel
        </code>
        。你也可以输入这个名称以便更快地找到它。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/17-ConnectFontPanel.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112658" src="https://koenig-media.raywenderlich.com/uploads/2015/08/17-ConnectFontPanel-625x500.png"
            alt="17-ConnectFontPanel" width="625" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/17-ConnectFontPanel-625x500.png 625w, https://koenig-media.raywenderlich.com/uploads/2015/08/17-ConnectFontPanel-400x320.png 400w, https://koenig-media.raywenderlich.com/uploads/2015/08/17-ConnectFontPanel.png 1280w"
            sizes="(max-width: 625px) 100vw, 625px">
        </a>
    </p>
    <p>
        现在，选择
        <em>
            Show Fonts
        </em>
        来看一下
        <em>
            Connections Inspector
        </em>
        。你会看到，现在这个菜单已经被连接到了在响应者链中响应 
        <code>
            orderFrontFontPanel
        </code>
        这个selector的第一响应者。
    </p>
    <p>
        运行app，然后输入一些文本并选择它。选择
        <em>
            Format / Font / Show Fonts
        </em>
        来打开字体面板。调整（Play with）字体面板右侧的垂直的滑动条，观察文本的大小如何实时地变化。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/18-FontPanel.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112660" src="https://koenig-media.raywenderlich.com/uploads/2015/08/18-FontPanel-647x500.png"
            alt="18-FontPanel" width="647" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/18-FontPanel-647x500.png 647w, https://koenig-media.raywenderlich.com/uploads/2015/08/18-FontPanel-414x320.png 414w, https://koenig-media.raywenderlich.com/uploads/2015/08/18-FontPanel.png 838w"
            sizes="(max-width: 647px) 100vw, 647px">
        </a>
    </p>
    <p>
        等等，你甚至都没有输入一行关于text view的代码，它就有了改变文本大小的能力。你太棒了！
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/word-processing-like-a-boss-e1441874078350.jpg"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113580" src="https://koenig-media.raywenderlich.com/uploads/2015/08/word-processing-like-a-boss-e1441874078350.jpg"
            alt="Word Processing...Like A Boss" width="330" height="304">
        </a>
    </p>
    <h3>
        使用富文本（Rich Text）来初始化text view
    </h3>
    <p>
        为了看到这个app全部的能力，请从
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/BabyScript.rtf"
        sl-processed="1">
            这里
        </a>
        下载一些格式化的文本，并使用它作为这个text view的初始化文本。
    </p>
    <p>
        使用TextEdit打开它，全选并拷贝到剪贴板中。找到storyboard，选择Text View，然后
        <strong>
            Attributes Inspector
        </strong>
        ，然后将文本粘贴到
        <em>
            Text Storage
        </em>
        中。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/20-RichText.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112671" src="https://koenig-media.raywenderlich.com/uploads/2015/08/20-RichText-625x500.png"
            alt="20-RichText" width="625" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/20-RichText-625x500.png 625w, https://koenig-media.raywenderlich.com/uploads/2015/08/20-RichText-400x320.png 400w, https://koenig-media.raywenderlich.com/uploads/2015/08/20-RichText.png 1280w"
            sizes="(max-width: 625px) 100vw, 625px">
        </a>
    </p>
    <p>
        运行项目，你应该会看到：
    </p>
    <p>
        <img class="aligncenter size-full wp-image-112672" src="https://koenig-media.raywenderlich.com/uploads/2015/08/21-EditMe.png"
        alt="21-EditMe" width="480" height="292">
    </p>
    <h3>
        使用自动布局
    </h3>
    <p>
        你确实可以滚动不适合当前window大小的文本，但尝试一下改变window的尺寸吧。
    </p>
    <p>
        哎呀！text view不能随着window尺寸的改变而改变。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/TextNoGrow.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112801" src="https://koenig-media.raywenderlich.com/uploads/2015/08/TextNoGrow-697x500.png"
            alt="TextNoGrow" width="697" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/TextNoGrow-697x500.png 697w, https://koenig-media.raywenderlich.com/uploads/2015/08/TextNoGrow-446x320.png 446w, https://koenig-media.raywenderlich.com/uploads/2015/08/TextNoGrow.png 767w"
            sizes="(max-width: 697px) 100vw, 697px">
        </a>
    </p>
    <p>
        使用
        <em>
            自动布局
        </em>
        ，这是一个非常简单的修复。
    </p>
    <div class="note">
        <p>
            <em>
                注意
            </em>
            ：自动布局在你的Cocoa和iOS app的UI中都可以使用。它创建了一套规则来定义元素之间的几何关系，而你以约束的形式来定义这些关系。
        </p>
        <p>
            使用自动布局，你可以创建一个动态的界面，以恰当地相应屏幕大小、window大小、设备方向和本地化的变化。
        </p>
        <p>
            关于自动布局还有更多的内容，但为了本教程的缘故，所有你需要做的只是跟随下面的步骤 - 你可以在之后学习更多关于Auto Layout的内容。这里有一些很好的教程供查看：在iOS 7中开始自动布局教程，
            <a href="http://www.raywenderlich.com/50317/beginning-auto-layout-tutorial-in-ios-7-part-1"
            target="_blank" sl-processed="1">
                第一部分
            </a>
            和
            <a href="http://www.raywenderlich.com/50317/beginning-auto-layout-tutorial-in-ios-7-part-1"
            target="_blank" sl-processed="1">
                第二部分
            </a>
            。
        </p>
    </div>
    <p>
        在storyboard的
        <em>
            Outline View
        </em>
        中，选择
        <em>
            Bordered Scroll View
        </em>
        ，点击画布右下角的
        <em>
            Pin
        </em>
        按钮。
    </p>
    <p>
        分别点击四个小红色的条的约束；那个“破碎的凋谢的红色”就会转变成“实的红色”。点击底部的叫做
        <em>
            Add 4 Constraints
        </em>
        的按钮。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/PinTextView.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112682" src="https://koenig-media.raywenderlich.com/uploads/2015/08/PinTextView-700x456.png"
            alt="PinTextView" width="700" height="456" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/PinTextView-700x456.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/PinTextView-480x312.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/PinTextView.png 882w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        运行项目，观察window和text view怎样一起改变大小：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/22-AutoLayoutFixed.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112673" src="https://koenig-media.raywenderlich.com/uploads/2015/08/22-AutoLayoutFixed-607x500.png"
            alt="22-AutoLayoutFixed" width="607" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/22-AutoLayoutFixed-607x500.png 607w, https://koenig-media.raywenderlich.com/uploads/2015/08/22-AutoLayoutFixed-388x320.png 388w, https://koenig-media.raywenderlich.com/uploads/2015/08/22-AutoLayoutFixed.png 671w"
            sizes="(max-width: 607px) 100vw, 607px">
        </a>
    </p>
    <h3>
        默认地展示尺子
    </h3>
    <p>
        为了在window打开时自动地展示尺子，你需要在代码中有一个
        <code>
            IBOutlet
        </code>
        。从菜单中选择
        <em>
            Format / Text / Show Ruler
        </em>
        。在
        <em>
            ViewController.swift
        </em>
        中，添加一行代码方法
        <code>
            toggleRuler
        </code>
        到
        <code>
            viewDidLoad
        </code>
        中，并添加一个
        <em>
            IBOutlet
        </em>
        在这个方法之上，就像下面这样：
    </p>
    <pre class="swift" style="font-family:monospace;">  @IBOutlet <span style="color: #a61390;">var</span> text<span style="color: #002200;">:</span> <span style="color: #400080;">NSTextView</span><span style="color: #002200;">!</span>
&nbsp;
  <span style="color: #a61390;">override</span> <span style="color: #a61390;">func</span> viewDidLoad<span style="color: #002200;">(</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
    <span style="color: #a61390;">super</span>.viewDidLoad<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
    text.toggleRuler<span style="color: #002200;">(</span><span style="color: #a61390;">nil</span><span style="color: #002200;">)</span>
  <span style="color: #002200;">}</span></pre>
    <p>
        现在你将在storyboard中，连接text view到view controller上。
    </p>
    <p>
        在storyboard中，右击
        <code>
            ViewController
        </code>
        ，不放手并拖拽到text view直到它变得高亮，然后放开鼠标。你将会看到一个带有
        <em>
            Outlets
        </em>
        列表的小的window。选择
        <code>
            text
        </code>
        的outlet：
    </p>
    <p>
        <img class="aligncenter size-full wp-image-112688" src="https://koenig-media.raywenderlich.com/uploads/2015/08/23-TextConnect.png"
        alt="23-TextConnect" width="550" height="410" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/23-TextConnect.png 550w, https://koenig-media.raywenderlich.com/uploads/2015/08/23-TextConnect-429x320.png 429w"
        sizes="(max-width: 550px) 100vw, 550px">
    </p>
    <p>
        运行项目，现在这个window就会默认id展示尺子：
    </p>
    <p>
        <img class="aligncenter size-full wp-image-112689" src="https://koenig-media.raywenderlich.com/uploads/2015/08/RulerShowing.png"
        alt="RulerShowing" width="480" height="292">
    </p>
    <p>
        就像我承诺的，仅靠两行代码和storyboard，你就创建了一个小的迷你文字处理器 - 致敬（Chapeau），苹果！
    </p>
    <h2>
        模态Window
    </h2>
    <p>
        你可以让window运行在模态方式下。这个window仍然使用app的标准时间循环，但输入仅限于模态window。
    </p>
    <p>
        有两种方式来利用模态窗口。你可以调用
        <code>
            NSApplication
        </code>
        的方法
        <code>
            runModalForWindow
        </code>
        。这种方式为指定的窗口垄断（monopolizes）了事件，直到它得到了一个你可以通过
        <code>
            stopModal
        </code>
        、
        <code>
            abortModal
        </code>
        或
        <code>
            stopModalWithCode
        </code>
        来调用的请求才停止。
    </p>
    <p>
        对于这个case，你将使用
        <code>
            stopModal
        </code>
        。另一种方式被称作
        <em>
            模态session
        </em>
        ，不会包含在本教程中。
    </p>
    <h3>
        添加一个字符统计window
    </h3>
    <p>
        你可以添加一个模态窗口来在活动的window中统计字数和段落数。由于会关联于一个指定的窗口和指定的状态，它必须是模态的。
    </p>
    <p>
        从
        <em>
            Object Library
        </em>
        中，拖拽一个新的
        <em>
            window controller
        </em>
        到画布上。它创建了两个新的场景：一个
        <em>
            window controller scene
        </em>
        和一个
        <em>
            view controller scene
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-112710" src="https://koenig-media.raywenderlich.com/uploads/2015/08/NewScenes-625x500.png"
        alt="NewScenes" width="625" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/NewScenes-625x500.png 625w, https://koenig-media.raywenderlich.com/uploads/2015/08/NewScenes-400x320.png 400w, https://koenig-media.raywenderlich.com/uploads/2015/08/NewScenes.png 1280w"
        sizes="(max-width: 625px) 100vw, 625px">
    </p>
    <p>
        从新的
        <em>
            window controller scene
        </em>
        中选择
        <em>
            Window
        </em>
        ，并使用
        <em>
            Size Inspector
        </em>
        来设定它的宽为300，高为150。从新的
        <em>
            view controller scene
        </em>
        中选择
        <em>
            View
        </em>
        并调整它的大小来匹配这个window：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountReduced.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112720" src="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountReduced-625x500.png"
            alt="WordCountReduced" width="625" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountReduced-625x500.png 625w, https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountReduced-400x320.png 400w, https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountReduced.png 1280w"
            sizes="(max-width: 625px) 100vw, 625px">
        </a>
    </p>
    <p>
        由于字数统计是模态的，它的标题栏上如果有关闭、最小化和重新调整大小的按钮就会显得很奇怪，并违反了
        <em>
            HIG
        </em>
        （苹果的人机交互指南）。
    </p>
    <p>
        对于
        <em>
            关闭
        </em>
        按钮，它还会引入一个严重的bug，因为点击它就会关闭window，但没有调用
        <code>
            stopModal
        </code>
        。这样，这个app就会永远停留在“模态状态”下。
    </p>
    <h3>
        从模态中删除按钮
    </h3>
    <p>
        在storyboard中，选择
        <em>
            Word Count
        </em>
        window并选择
        <em>
            Attributes Inspector
        </em>
        。取消勾选
        <em>
            Close
        </em>
        ，
        <em>
            Minimize
        </em>
        和
        <em>
            Resize
        </em>
        。同时改变
        <em>
            Title
        </em>
        为
        <em>
            Word Count
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountAppearance.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113032" src="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountAppearance.png"
            alt="WordCountAppearance" width="259" height="335" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountAppearance.png 259w, https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountAppearance-247x320.png 247w"
            sizes="(max-width: 259px) 100vw, 259px">
        </a>
    </p>
    <p>
        现在，你将从Object Library中添加四个label控件和一个push button到Word Count window的
        <code>
            contentView
        </code>
        上。
    </p>
    <p>
        选择
        <em>
            Attributes Inspector
        </em>
        。相应地改变Title为
        <em>
            Word Count
        </em>
        ，
        <em>
            Paragraph Count
        </em>
        ，
        <em>
            0
        </em>
        和
        <em>
            0
        </em>
        。同时两个0的label的
        <em>
            alignment
        </em>
        为右对齐。将push button的Title改为
        <em>
            OK
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountFields.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112748" src="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountFields-544x500.png"
            alt="WordCountFields" width="544" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountFields-544x500.png 544w, https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountFields-348x320.png 348w, https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountFields.png 704w"
            sizes="(max-width: 544px) 100vw, 544px">
        </a>
    </p>
    <p>
        接下来为Window Count ViewController创建一个子类。选择
        <em>
            File / New / File..
        </em>
        ，选择
        <em>
            OS X / Source / Cocoa Class
        </em>
        。在
        <em>
            Choose Options
        </em>
        的对话框中，在
        <em>
            Class
        </em>
        后输入
        <code>
            WordCountViewController
        </code>
        ，而在
        <em>
            Subclass of
        </em>
        后输入
        <code>
            NSViewController
        </code>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountViewController.png"
        sl-processed="1">
            <img class="aligncenter wp-image-112751 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountViewController-480x320.png"
            alt="WordCountViewController" width="480" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountViewController-480x320.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountViewController-700x468.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountViewController.png 729w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        点击
        <em>
            Next
        </em>
        创建新的文件。确认
        <em>
            WordCountWindowControll.swift
        </em>
        现在已经在project navigator中了。
    </p>
    <p>
        找到storyboard. 为文字计数在
        <em>
            view controller scene
        </em>
        的view controller中选择proxy图标。打开        
        <em>
            Identity Inspector
        </em>
        , 从
        <em>
            Class
        </em>
        的下拉菜单中选择
        <code>
            WordCountViewController
        </code>
        。
        注意在画板和
        <em>
            Outline View
        </em>
        上的名字是如何从通用的改变成
        <em>
            Word Count View Controller
        </em>
        的。
    </p>
    <p>
        <img class="aligncenter size-full wp-image-112758" src="https://koenig-media.raywenderlich.com/uploads/2015/08/SetWCViewController.png"
        alt="SetWCViewController" width="604" height="649" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/SetWCViewController.png 604w, https://koenig-media.raywenderlich.com/uploads/2015/08/SetWCViewController-298x320.png 298w, https://koenig-media.raywenderlich.com/uploads/2015/08/SetWCViewController-465x500.png 465w"
        sizes="(max-width: 604px) 100vw, 604px">
    </p>
    <h3>
        创建统计Label
    </h3>
    <p>
        现在你可以为两个label创建outlet了，让它们来展示统计的值 - 就是那两个0 label。在
        <em>
            WordCountViewController.swift
        </em>
        中的类的定义下，添加下列代码：
    </p>
    <pre class="swift" style="font-family:monospace;">  @IBOutlet weak <span style="color: #a61390;">var</span> wordCount<span style="color: #002200;">:</span> <span style="color: #400080;">NSTextField</span><span style="color: #002200;">!</span>
  @IBOutlet weak <span style="color: #a61390;">var</span> paragraphCount<span style="color: #002200;">:</span> <span style="color: #400080;">NSTextField</span><span style="color: #002200;">!</span></pre>
    <p>
        在storyboard中，右击
        <em>
            word count view controller
        </em>
        的proxy图标，拖拽到0 label，并当它高亮时释放鼠标。从弹出的
        <em>
            Outlets
        </em>
        列表中，选择
        <code>
            wordCount
        </code>
        。
    </p>
    <p>
        为下面那个0 label重复同样的操作，但是这次选择
        <code>
            paragraphCount
        </code>
        。查看
        <em>
            Connections Inspector
        </em>
        中的每一个label，让它们的
        <em>
            Outlets
        </em>
        都像下面这么连接：
    </p>
    <p>
        <img class="aligncenter size-full wp-image-112772" src="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountConnected.png"
        alt="WordCountConnected" width="602" height="468" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountConnected.png 602w, https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountConnected-412x320.png 412w"
        sizes="(max-width: 602px) 100vw, 602px">
    </p>
    <p>
        很快，你就会添加代码来加载count window controller。这要求它有一个
        <em>
            storyboard ID
        </em>
        。从storyboard的
        <em>
            word count window
        </em>
        中选择
        <em>
            window controller
        </em>
        。选择
        <em>
            Identity Inspector
        </em>
        ，在
        <em>
            Storyboard ID
        </em>
        中输入
        <em>
            Word Count Window Controller
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-full wp-image-112791" src="https://koenig-media.raywenderlich.com/uploads/2015/08/WCControllerStoryboardId.png"
        alt="WCControllerStoryboardId" width="578" height="342" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/WCControllerStoryboardId.png 578w, https://koenig-media.raywenderlich.com/uploads/2015/08/WCControllerStoryboardId-480x284.png 480w"
        sizes="(max-width: 578px) 100vw, 578px">
    </p>
    <h3>
        展示给我模态
    </h3>
    <p>
        现在到了展示模态window的基本逻辑了。在文档window的view controller中，找到并选择
        <em>
            ViewController.swift
        </em>
        ，在
        <code>
            viewDidLoad
        </code>
        下面添加如下代码：
    </p>
    <pre class="swift" style="font-family:monospace;">  @IBAction <span style="color: #a61390;">func</span> showWordCountWindow<span style="color: #002200;">(</span>sender<span style="color: #002200;">:</span> <span style="color: #a61390;">AnyObject</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
&nbsp;
    <span style="color: #11740a; font-style: italic;">// 1</span>
    <span style="color: #a61390;">let</span> storyboard <span style="color: #002200;">=</span> NSStoryboard<span style="color: #002200;">(</span>name<span style="color: #002200;">:</span> <span style="color: #bf1d1a;">"Main"</span>, bundle<span style="color: #002200;">:</span> <span style="color: #a61390;">nil</span><span style="color: #002200;">)</span>
    <span style="color: #a61390;">let</span> wordCountWindowController <span style="color: #002200;">=</span> storyboard.instantiateControllerWithIdentifier<span style="color: #002200;">(</span><span style="color: #bf1d1a;">"Word Count Window Controller"</span><span style="color: #002200;">)</span> <span style="color: #a61390;">as</span><span style="color: #002200;">!</span> <span style="color: #400080;">NSWindowController</span>
&nbsp;
    <span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> wordCountWindow <span style="color: #002200;">=</span> wordCountWindowController.window, textStorage <span style="color: #002200;">=</span> text.textStorage <span style="color: #002200;">{</span>
&nbsp;
      <span style="color: #11740a; font-style: italic;">// 2</span>
      <span style="color: #a61390;">let</span> wordCountViewController <span style="color: #002200;">=</span> wordCountWindow.contentViewController <span style="color: #a61390;">as</span><span style="color: #002200;">!</span> WordCountViewController
      wordCountViewController.wordCount.stringValue <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"<span style="color: #2400d9;">\(</span>textStorage.words.count)"</span>
      wordCountViewController.paragraphCount.stringValue <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"<span style="color: #2400d9;">\(</span>textStorage.paragraphs.count)"</span>
&nbsp;
      <span style="color: #11740a; font-style: italic;">// 3</span>
      <span style="color: #a61390;">let</span> application <span style="color: #002200;">=</span> <span style="color: #400080;">NSApplication</span>.sharedApplication<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
      application.runModalForWindow<span style="color: #002200;">(</span>wordCountWindow<span style="color: #002200;">)</span>
    <span style="color: #002200;">}</span>
  <span style="color: #002200;">}</span></pre>
    <p>
        一步一步来看：
    </p>
    <ol>
        <li>
            使用你之前指定的storyboard ID初始化word count window controller。
        </li>
        <li>
            设置检索自text view的相应的值到字数统计window中
        </li>
        <li>
            模态地展示字数统计window
        </li>
    </ol>
    <div class="note">
        <p>
            <em>
                注意
            </em>
            ：在第二步，你在两个view controller间传递了数据。这就类似于当transition涉及到一个segue时，你经常在
            <code>
                prepareForSegue
            </code>
            中做的一样。由于展示模态window是直接通过调用
            <code>
                runModalForWindow
            </code>
            完成的，没有涉及到segue，你只需在调用之前传递数据。
        </p>
    </div>
    <h3>
        走开，模态
    </h3>
    <p>
        现在你将添加代码来让字符统计window消失。在
        <em>
            WordCountViewController.swift
        </em>
        中，添加下列代码到
        <code>
            paragraphCount
        </code>
        outlet的下边：
    </p>
    <pre class="swift" style="font-family:monospace;">  @IBAction <span style="color: #a61390;">func</span> dismissWordCountWindow<span style="color: #002200;">(</span>sender<span style="color: #002200;">:</span> <span style="color: #400080;">NSButton</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
    <span style="color: #a61390;">let</span> application <span style="color: #002200;">=</span> <span style="color: #400080;">NSApplication</span>.sharedApplication<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
    application.stopModal<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
  <span style="color: #002200;">}</span></pre>
    <p>
        这是当用户点击
        <em>
            字符统计window
        </em>
        中的
        <em>
            OK
        </em>
        时，应当被调用的
        <em>
            IBAction
        </em>
        。
    </p>
    <p>
        找到storyboard，右击
        <em>
            OK
        </em>
        ，并拖动带
        <em>
            word count view controller
        </em>
        的proxy图标上。释放鼠标并在出现的列表中选择
        <code>
            dismissWordCountWindow:
        </code>
        ：
    </p>
    <p>
        <img class="alignnone size-full wp-image-112794" src="https://koenig-media.raywenderlich.com/uploads/2015/08/ConnectOK.png"
        alt="ConnectOK" width="360" height="314">
    </p>
    <h3>
        添加UI来调用它
    </h3>
    <p>
        剩下的要来展示window的唯一一件事，就是添加UI并去调用它了。找到storyboard，在
        <em>
            Main Menu
        </em>
        中点击
        <em>
            Edit
        </em>
        。从
        <em>
            Object Library
        </em>
        中拖出一个
        <em>
            Menu Item
        </em>
        到
        <em>
            Edit
        </em>
        菜单的底部。选择
        <em>
            Attributes Inspector
        </em>
        并设置title为
        <em>
            Word Count
        </em>
        。
    </p>
    <p>
        <img class="alignnone size-full wp-image-112795" src="https://koenig-media.raywenderlich.com/uploads/2015/08/WCMenu.png"
        alt="WCMenu" width="626" height="847" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/WCMenu.png 626w, https://koenig-media.raywenderlich.com/uploads/2015/08/WCMenu-237x320.png 237w, https://koenig-media.raywenderlich.com/uploads/2015/08/WCMenu-370x500.png 370w"
        sizes="(max-width: 626px) 100vw, 626px">
    </p>
    <p>
        花几分钟来通过输入
        <em>
            command – K
        </em>
        创建一个快捷键，作为
        <em>
            key equivalent
        </em>
        。
    </p>
    <p>
        现在你将在
        <em>
            ViewController.swift
        </em>
        中连接新的菜单项到
        <code>
            showWordCountWindow
        </code>
        方法上。        
    </p>
    <p>
        找到storyboard，右击
        <em>
            Word Count
        </em>
        菜单项，拖拽到
        <em>
            application scene
        </em>
        的
        <em>
            First Responder
        </em>
        上。从列表中选择
        <code>
            showWordCountWindow
        </code>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/ConnectWCMenuItem.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-112796" src="https://koenig-media.raywenderlich.com/uploads/2015/08/ConnectWCMenuItem-625x500.png"
            alt="ConnectWCMenuItem" width="625" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/ConnectWCMenuItem-625x500.png 625w, https://koenig-media.raywenderlich.com/uploads/2015/08/ConnectWCMenuItem-400x320.png 400w, https://koenig-media.raywenderlich.com/uploads/2015/08/ConnectWCMenuItem.png 710w"
            sizes="(max-width: 625px) 100vw, 625px">
        </a>
    </p>
    <div class="note">
        <p>
            <em>
                注意
            </em>
            ：你可能会奇怪为什么你要连接菜单项到first responder，而不是直接到
            <code>
                showWordCountWindow
            </code>
            这里。这是因为文档view的主菜单和view controller是在不同的storyboard的scene中，因此，不能直接连接。
        </p>
    </div>
    <p>
        运行app，选择
        <em>
            Edit / Word Count
        </em>
        ，瞧（voila），字数统计window展示了它自己。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountFinal.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113033" src="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountFinal-700x331.png"
            alt="WordCountFinal" width="700" height="331" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountFinal-700x331.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountFinal-480x227.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/WordCountFinal.png 1007w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        单击OK关闭window。
    </p>
    <h3>
        从这儿去向哪里？
    </h3>
    <p>
        这里是BabyScript的
        <a title="final project" href="https://koenig-media.raywenderlich.com/uploads/2015/08/BabyScript-Final-Project.zip"
        sl-processed="1">
            最终版本
        </a>
        。
    </p>
    <p>
        在这个OS X的window和window controller教程中，你已经覆盖了很多基本的内容！但它对于你可以利用window和window controller做的事来说，只是冰山的一角。
    </p>
    <p>
        你已经覆盖了：
    </p>
    <ul>
        <li>
            动作的MVC设计模式
        </li>
        <li>
            怎样创建一个多window的app
        </li>
        <li>
            OS X app的典型app架构
        </li>
        <li>
            怎样使用Interface Builder
            <i>
                和
            </i>
            编程方式来定位和排列window
        </li>
        <li>
            使用自动布局来来根据window调整view的大小
        </li>
        <li>
            使用模态window来展示附加的信息
        </li>
    </ul>
    <p>
        还有更多！
    </p>
    <p>
        我强烈地建议你探索苹果在
        <a href="https://developer.apple.com/library/prerelease/mac/navigation/"
        target="_blank" sl-processed="1">
            El Capitan’s Mac 开发者库
        </a>
        中提供的的大量文档。特别的，参考
        <em>
            Window编程指南
        </em>
        .
    </p>
    <p>
        为了更好地理解Cocoa app的设计，以及如何使用文档开头提到的app的类型，请查看
        <a title="Mac App Programming Guide" href=" https://developer.apple.com/library/prerelease/mac/documentation/General/Conceptual/MOSXAppProgrammingGuide/CoreAppDesign/CoreAppDesign.html "
        target="_blank" sl-processed="1">
            Mac App编程指南
        </a>
        。这个文档还扩展了基于多窗口文档的应用程序的概念，你会在这里找到改善BabyScript的idea。
    </p>
</div>
