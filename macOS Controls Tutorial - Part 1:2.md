# macOS控件教程：1/2部分

#### [原文地址](https://www.raywenderlich.com/149295/macos-controls-tutorial-part-12) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <em>
            更新日志：
        </em>
        已由Ernesto García更新至 Xcode 8.2 / Swift 3 版。
        <a href="https://www.raywenderlich.com/82046/introduction-to-os-x-tutorial-core-controls-and-swift-part-1">
            之前
        </a>
        由
        <a href="https://www.raywenderlich.com/u/skyrocketsw">
            Michael Briscoe
        </a>
        更新至Xcode 6.3 / Swift 1.2。
        <a href="https://www.raywenderlich.com/27388/core-controls-in-mac-os-x-part-12">
            初始版本
        </a>
        作者为
        <a href="http://www.raywenderlich.com/u/ernesto">
            Ernesto García
        </a>
        。
    </p>
    <p>
        如果你是一个iOS开发者，并且你感兴趣学习Mac开发，你很幸运 - 由于你的iOS的技能，你会发现它非常易学！
    </p>
    <p>
        很多你了解并喜欢Cocoa的类和设计模式，例如字符型、字典和代理在Mac开发中都是直接提供的。你会感到非常舒服！
    </p>
    <p>
        然而，一个和macOS开发很大的区别是它们存在不同的控件。消失的是
        <code>
            UIButton
        </code>
        和
        <code>
            UITextField
        </code>
        - 用来取代的是相似（但有轻微不同的）变量。
    </p>
    <p>
        这篇教程将向你介绍一些用户交互中，更常用的macOS控件 - 它们是构建多数Mac app的基础。你将学习这些控件的方法和property，作为一个开发者，为了建造和运行起来，你需要去理解它们！:]
    </p>
    <p>
        在这篇教程中，你会创建一个简单的Mac应用，就像流行的游戏
        <a href="http://en.wikipedia.org/wiki/Mad_Libs" title="Mad Libs" target="_blank">
            Mad Libs
        </a>
        。Mad Libs是一个单词游戏，你可以在一个文本块中，插入不同的单词，来创建一个故事 - 这常常会造成非常滑稽的结果！
    </p>
    <p>
        一旦你完成了这篇教程中的两个部分，你就会拥有对下列macOS控件的基本的理解：
    </p>
    <ul>
        <li>
            Labels和Text Fields
        </li>
        <li>
            Combo Boxes
        </li>
        <li>
            Popup Buttons
        </li>
        <li>
            Text Views
        </li>
        <li>
            Sliders
        </li>
        <li>
            Date Pickers
        </li>
        <li>
            Buttons
        </li>
        <li>
            Radio Buttons
        </li>
        <li>
            Check Buttons
        </li>
        <li>
            Image Views
        </li>
    </ul>
    <div class="note">
        <em>
            注意：
        </em>
        学习本教程需要一些macOS开发的基础知识。如果这是你第一次开发macOS，你可以参考我们的
        <a href="https://www.raywenderlich.com/110170/mac-os-x-development-tutorial-for-beginners-part-1-intro-to-xcode"
        target="_blank">
            macOS开发初学者教程
        </a>
        系列来学习基础。
    </div>
    <p>
        学习任何新的编程平台的最好的方式就是钻入并入门 - 所以不要担心得太多，这里就是你学习macOS控件的向导！:]
    </p>
    <h2>
        macOS控件入门
    </h2>
    <p>
        打开
        <em>
            Xcode
        </em>
        ，并选择
        <em>
            File/New/Project
        </em>
        。在
        <em>
            Choose a template
        </em>
        对话框中，选择
        <em>
            macOS/Application/Cocoa
        </em>
        ，它是你用来创建带有GUI的macOS app的模板。然后点击
        <em>
            Next
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/macos-template.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/macos-template-650x455.png"
            alt="macos-template" width="650" height="455" class="aligncenter size-large wp-image-149748"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/macos-template-650x455.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/12/macos-template-458x320.png 458w, https://koenig-media.raywenderlich.com/uploads/2016/12/macos-template.png 1424w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        在下一屏中，输入
        <em>
            MadLibs
        </em>
        作为产品名称，然后输入唯一的组织名称和标识符。确保
        <em>
            Use Storyboards
        </em>
        被选中，选中
        <em>
            Swift
        </em>
        作为语言。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/macos-projectname.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/macos-projectname-650x457.png"
            alt="macos-projectname" width="650" height="457" class="aligncenter size-large wp-image-149749"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/macos-projectname-650x457.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/12/macos-projectname-455x320.png 455w, https://koenig-media.raywenderlich.com/uploads/2016/12/macos-projectname.png 1434w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        单击
        <em>
            Next
        </em>
        并选择你想要保存你的新项目的位置。点击
        <em>
            Create
        </em>
        。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        。
        <em>
            Xcode
        </em>
        已为你创建了一个macOS app的基本的骨架：一个Window controller及一个content View controller。
    </p>
    <p>
        选择
        <em>
            Window Controller Scene
        </em>
        中的window并打开
        <em>
            Attributes Inspector
        </em>
        。将window的
        <em>
            Title
        </em>
        改为
        <em>
            MadLibs
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibsWindowTitle.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibsWindowTitle-650x400.png"
            alt="MadLibsWindowTitle" width="650" height="400" class="aligncenter size-large wp-image-153685"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibsWindowTitle-650x400.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibsWindowTitle-480x295.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibsWindowTitle.png 1084w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        macOS app通常会带有一个可以改变大小的窗口，因此它的内容就不得不适应于窗口的尺寸。对此最有用的工具就是
        <em>
            自动布局
        </em>
        。添加自动布局到这篇教程中全部控件 会造成很大的分神；我们想要你把注意力完全集中到macOS控件上。
    </p>
    <p>
        因此，我们只会应用默认的autoresizing，它意味着全部的控件都会保持一个规定的位置和尺寸，无论窗口大小如何改变，用户的平台有何不同 —— 包括潜在的一些控件会全部或部分地超出窗口的课件范围。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            如果你想要了解更多关于自动布局，以及如何在你的macOS app中使用，你可以跟随我们的
            <a href="https://www.raywenderlich.com/110269/mac-os-x-development-tutorial-beginners-part-3-first-os-x-app"
            target="_blank">
                macOS开发初学者教程，第三部分
            </a>
            。
        </p>
    </div>
    <p>
        在这篇教程中，你需要为这个view添加一些macOS控件。默认的高度可能无法盛得下。如果你需要调整尺寸，向下拖拽content view的底部边缘，或在
         <em>
            Size Inspector
        </em>
        中设置view的
        <em>
            Height
        </em>
        property。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-resize-1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-resize-1-480x290.png"
            alt="drag-resize" width="480" height="290" class="aligncenter size-medium wp-image-153172"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-resize-1-480x290.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/drag-resize-1-650x393.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/drag-resize-1.png 1471w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        运行项目。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/empty-window.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/empty-window-353x320.png"
            alt="empty-window" width="353" height="320" class="aligncenter size-medium wp-image-153163"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/empty-window-353x320.png 353w, https://koenig-media.raywenderlich.com/uploads/2017/01/empty-window-552x500.png 552w, https://koenig-media.raywenderlich.com/uploads/2017/01/empty-window.png 672w"
            sizes="(max-width: 353px) 100vw, 353px">
        </a>
    </p>
    <p>
        你已经构建了一个可工作的应用 - 没有一句代码。窗口现在是空的，但马上你就会用一些macOS的控件来填充它，让它看起来更棒！:]
    </p>
    <p>
        既然基本的框架已搭完，你就可以转移注意力到这篇教程的主题上了 - 添加macOS控件到你的app上。
    </p>
    <p>
        这篇教程中剩余的每一步骤都会聚焦在一个单独的、不同的控件上。你会了解到每个控件的基础，和如何在MadLibs app中使用它们来造出东西来。
    </p>
    <h2>
        NSControl – MacOS控件的构建模块
    </h2>
    <p>
        <a href="http://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Classes/NSControl_Class/Reference/Reference.html"
        title="NSControl" target="_blank">
            NSControl
        </a>
        是所有其它的macOS控件构建的基础。
        <code>
            NSControl
        </code>
        提供了三个对于用户交互非常重要的特性：绘制到屏幕上，相应用户事件，发送动作消息。
    </p>
    <p>
        <code>
            NSControl
        </code>
        是一个抽象的基类，非常有可能从不需要在你的app中直接使用它，除非你想要定制你自己的macOS控件。所有的常用控件都是
        <code>
            NSControl
        </code>
        的子类，因此就继承了定义在NSControl中的property和方法。
    </p>
    <p>
        一个control最常用的方法是获取和设置它的值，就像打开和禁用这个控件本身一样。下面来看一下这些方法背后的细节：
    </p>
    <h3>
        设置macOS控件的值
    </h3>
    <p>
        如果你需要展示信息，通常就要改变控件的值。根据你的需要，这个值可能是一个字符串，一个数字，甚至是一个对象。在大多数环境下，你需要一个能够匹配被展示的信息的类型的值，但
        <code>
            NSControl
        </code>
        允许你超越这个，并设置几个不同类型的值！
    </p>
    <p>
        获取和设置一个控件的值的方法有：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-comment">// getting &amp; setting a string</span>
<span class="hljs-keyword">let</span> myString = myControl.stringValue
myControl.stringValue = myString

<span class="hljs-comment">// getting &amp; setting an integer</span>
<span class="hljs-keyword">let</span> myInteger = myControl.integerValue
myControl.integerValue = myInteger

<span class="hljs-comment">// getting &amp; setting a float</span>
<span class="hljs-keyword">let</span> myFloat = myControl.floatValue
myControl.floatValue = myFloat

<span class="hljs-comment">// getting &amp; setting a double</span>
<span class="hljs-keyword">let</span> myDouble = myControl.doubleValue
myControl.doubleValue = myDouble

<span class="hljs-comment">// getting &amp; setting an object</span>
<span class="hljs-keyword">let</span> myObject: Any? = myControl.objectValue
myControl.objectValue = myObject
</pre>
    <p>
        你可以看到不同的setter和getter是如何适应Swift的类型安全特性的。
    </p>
    <h3>
        启用和禁用macOS控件
    </h3>
    <p>
        基于一个app的状态启用或禁用macOS控件，是一个非常常见的UI任务。当一个控件被禁用时，它就不会响应鼠标或键盘的事件，并且通常会更新它的图形表示，来提供一些被禁用的视觉提示，例如用较轻的灰色来绘制本身。
    </p>
    <p>
        启用和禁用的一个控件的方法有：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-comment">// disable a control</span>
myControl.isEnabled = <span class="hljs-literal">false</span>

<span class="hljs-comment">// enable a control</span>
myControl.isEnabled = <span class="hljs-literal">true</span>

<span class="hljs-comment">// get a control's enabled state</span>
<span class="hljs-keyword">let</span> isEnabled = myControl.isEnabled
</pre>
    <p>
        OK，看起来相当得容易 - 很棒的事是这些方法对于所有的macOS空间都是通用的。对于任何你在你的UI中使用的控件来说，它们都以相同的方式工作。
    </p>
    <p>
        现在是时候去看一看更通用的macOS控件了。
    </p>
    <h2>
        梦想的域 - NSTextField
    </h2>
    <p>
        在任何UI中，最常用的控件之一，是一个能够用来展示或编辑文本的域。在macOS中负责这个功能的控件就是
        <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Classes/NSTextField_Class/Reference/Reference.html"
        title="NSTextField Class Reference">
            NSTextField
        </a>
        了。
    </p>
    <p>
        <code>
            NSTextField
        </code>
        是用来展示或编辑文本的。你会注意到它和iOS的差别：在iOS中，
        <code>
            UILabel
        </code>
        是用来展示固定的文本的，
        <code>
            UITextField
        </code>
        是用来编辑文本的。在macOS中它们被合二为一，它的行为会根据
        <code>
            isEditable
        </code>
        这个property的值变化而变化。
    </p>
    <p>
        如果你想要text field成为一个label，你可以设置它的
        <code>
            isEditable
        </code>
        property为
        <code>
            false
        </code>
        。要让它的行为像一个text field - 是的，你就可以设置
        <code>
            isEditable
        </code>
        为
        <code>
            true
        </code>
        ！你可以从代码或从Interface Builder中改变这个property。
    </p>
    <p>
        为了让你编写代码更容易一些，Interface Builder事实上提供了几个预先配置好的 基于
        <code>
            NSTextField
        </code>
        的macOS控件，来展示和编辑文本。这些可以在
        <em>
            Object Library
        </em>
        中找到的预配置的macOS控件有：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/textfields-catalog.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/textfields-catalog-253x500.png"
            alt="textfields-catalog" width="253" height="500" class="aligncenter size-large wp-image-150177"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/textfields-catalog-253x500.png 253w, https://koenig-media.raywenderlich.com/uploads/2016/12/textfields-catalog-162x320.png 162w, https://koenig-media.raywenderlich.com/uploads/2016/12/textfields-catalog.png 522w"
            sizes="(max-width: 253px) 100vw, 253px">
        </a>
    </p>
    <p>
        现在你已经了解了有关
        <code>
            NSTextField
        </code>
        的基础，你可以添加它到你爹Mad Libs应用中了！:]
    </p>
    <h2>
        生活在过去 - 过去时态的动词
    </h2>
    <p>
        你会添加各种macOS控件到MadLibs app上，让你可以“盲目地”构建一个有趣的句子。一旦你完成后，你就会把各部分连起来，并展示结果，很有可能就是一些喜剧的结果。你越有创造了，它们就会越有趣！
    </p>
    <p>
        你要添加的第一个控件是一个text field，可以在这里输入一个动词来添加到句子中。以及一个表示这个text field是为什么的label。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        。定位到
        <em>
            Object Library
        </em>
        中的
        <em>
            Label
        </em>
        控件，并将其拖拽到
        <em>
            View Controller Scene
        </em>
        的view上。双击label来编辑默认的文本，并将其改为
        <em>
            Past Tense Verb:
        </em>
        。
    </p>
    <p>
        接下来，找到
        <em>
            Text Field
        </em>
        控件并将它拖拽到view上，放置到label的右边，就像这样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-label.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-label-650x480.png"
            alt="drag-label" width="650" height="480" class="aligncenter size-large wp-image-153173"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-label-650x480.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/drag-label-434x320.png 434w, https://koenig-media.raywenderlich.com/uploads/2017/01/drag-label.png 1476w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        现在，你要在view controller中创建这个text field的outlet。打开
        <em>
            Main.storyboard
        </em>
        ，前往
        <em>
            Assistant editor
        </em>
        。确保
        <em>
            ViewController.swift
        </em>
        被选中，并从storyboard的text field中拖拽到
        <em>
            按住Ctrl拖拽到
        </em>
        包含
        <em>
            ViewController.swift
        </em>
        的窗格中，然后在类定义的下面放开鼠标，来创建一个新的property：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-1-650x371.png"
            alt="textoutlet-1" width="650" height="371" class="aligncenter size-large wp-image-150118"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-1-650x371.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-1-480x274.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-1-266x151.png 266w, https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-1.png 1066w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        在出现的下拉菜单中，将Outlet命名为
        <em>
            pastTenseVerbTextField
        </em>
        ，并单击
        <em>
            Connect
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-popup.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-popup-480x270.png"
            alt="textoutlet-popup" width="400" height="225" class="aligncenter size-medium wp-image-150119">
        </a>
    </p>
    <p>
        就是这样！现在你已经在你的view controller中拥有了一个
        <code>
            NSTextField
        </code>
        的property，并且它已经连接到了在主窗口的text field上。
    </p>
    <p>
        你知道，在app启动时显示一些默认的文本，来提示该往文本框中输入什么是非常棒的。由于每个人都喜欢吃，关于Mad Libs的实物总是最有趣的，
        <em>
            ate
        </em>
        这个词在这里就会成为一个很棒的选择。
    </p>
    <p>
        放置这个的一个很好的地方就在
        <code>
            viewDidLoad()
        </code>
        中。现在设置你先前学过的
        <code>
            stringValue
        </code>
        property。
    </p>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        ，并添加下列的代码到
        <code>
            viewDidLoad()
        </code>
        方法末尾：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-comment">// Sets the default text for the pastTenseVerbTextField property</span>
pastTenseVerbTextField.stringValue = <span class="hljs-string">"ate"</span>
</pre>
    <p>
        运行项目。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-textfield.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-textfield-409x320.png"
            alt="buildrun-textfield" width="409" height="320" class="aligncenter size-medium wp-image-153174"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-textfield-409x320.png 409w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-textfield-639x500.png 639w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-textfield.png 672w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <p>
        OK，它负责了一个默认值的输入。但如果你想要提供一个值得列表来方便选择呢？
    </p>
    <p>
        Combo Boxes可以解救你！
    </p>
    <h2>
        值的组合 - NSComboBox
    </h2>
    <p>
        combo box是非常得有趣且便利的 - 它让用户可以从一个选项的数组中选择一个值，就如同输入它们自己的文本一样。
    </p>
    <p>
        它看起来就类似于一个用户可以自由输入的text field，但还包含了一个让用户可以展示一个可选项目列表的按钮。你可以在macOS的“日期时间”偏好面板中找到一个示例：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/date-sshot.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/date-sshot.png"
            alt="date-sshot" width="655" height="161" class="aligncenter size-full wp-image-150148"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/date-sshot.png 655w, https://koenig-media.raywenderlich.com/uploads/2016/12/date-sshot-480x118.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/date-sshot-650x160.png 650w"
            sizes="(max-width: 655px) 100vw, 655px">
        </a>
    </p>
    <p>
        这里，用户可以从一个预定义的列表中进行选择，或输入他们自己的服务器名称，如果他们希望的话。
    </p>
    <p>
        在macOS中负责这个的是
        <a href="http://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Classes/NSComboBox_Class/Reference/Reference.html"
        title="NSComboBox Class reference">
            NSComboBox
        </a>
        。
    </p>
    <p>
        <code>
            NSComboBox
        </code>
        有两个不同的成分：你可以进行输入的text field，还有当嵌入的按钮被点击时展示的选项的列表。你可以分别地控制两部分的数据。
    </p>
    <p>
        要获取或设置text field中的值，只需使用前面提到的
        <code>
            stringValue
        </code>
        property。为保持事情简单一致喝彩吧！:]
    </p>
    <p>
        为列表提供选项会有一点复杂，但仍是相对直接了当的。你可以直接调用控件上的方法来添加元素，就类似于可变数组一样，也可以使用data source - 任何有iOS编程经验的人都会感到非常舒适！
    </p>
    <div class="note">
        <p>
            <em>
               注意：
            </em>
            如果你并不熟悉Data Sources的相关概念，你可以在苹果的
            <a href="https://developer.apple.com/library/content/documentation/General/Conceptual/CocoaEncyclopedia/DelegatesandDataSources/DelegatesandDataSources.html"
            target="_blank">
                文档
            </a>
            中进行了解。
        </p>
    </div>
    <h3>
        方法1 - 直接调用控件上的方法
    </h3>
    <p>
        <code>
            NSComboBox
        </code>
        包含了一个内部的项目列表，并暴露了几个允许你操纵这个列表的方法，例如：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-comment">// Add an object to the list</span>
myComboBox.addItem(withObjectValue: anObject)

<span class="hljs-comment">// Add an array of objects to the list</span>
myComboBox.addItems(withObjectValues: [objectOne, objectTwo, objectThree])

<span class="hljs-comment">// Remove all objects from the list</span>
myComboBox.removeAllItems()

<span class="hljs-comment">// Remove an object from the list at a specific index</span>
myComboBox.removeItem(at: <span class="hljs-number">2</span>)

<span class="hljs-comment">// Get the index of the currently selected object</span>
<span class="hljs-keyword">let</span> selectedIndex = myComboBox.indexOfSelectedItem

<span class="hljs-comment">// Select an object at a specific index</span>
myComboBox.selectItem(at: <span class="hljs-number">1</span>)
</pre>
    <p>
        这个相对比较直接，但如果你不想在你的app中选择硬编码 - 例如一个储存在app外部的动态列表的话？这时候使用datasource就会显得相当便利！:]
    </p>
    <h3>
        方法 2 - 使用Data Source
    </h3>
    <p>
        当使用data source时，combo box会查询数据源，来查找需要展示的项目，以及任何必须的元数据，例如将要在列表中展示的数据的项目。为了获取这个信息，你需要在你的一个类中实现
        <a href="http://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Protocols/NSComboBoxDataSource_Protocol/Reference/Reference.html"
        title="NSComboBoxDataSource Protocol Reference">
            NSComboBoxDataSource
        </a>
        协议，通常是由View Controller来托管控件。从这里，需要两个步骤来配置combo
        box使用数据源。
    </p>
    <p>
        首先，设置控件的
        <code>
            usesDataSource
        </code>
        property为
        <code>
            true
        </code>
        。然后设置控件的
        <code>
            dataSource
        </code>
        property，传递一个实现了这个协议的类的实例；当实现data source的类是托管的view controller时，配置这个的很好的一个地方就是
        <code>
            viewDidLoad()
        </code>
        这里了，然后你就可以设置
        <code>
            dataSource
        </code>
        property为
        <code>
            self
        </code>
        ，就像下面这样：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">ViewController</span>: <span class="hljs-title">NSViewController</span>, <span class="hljs-title">NSComboBoxDataSource</span> </span>{
.....
  <span class="hljs-keyword">override</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">viewDidLoad</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">super</span>.viewDidLoad()
    myComboBox.usesDataSource = <span class="hljs-literal">true</span>
    myComboBox.dataSource = <span class="hljs-keyword">self</span>
  }
.....
}
</pre>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            上面这些指令的顺序是非常重要的。尝试当
            <code>
                useDataSource
            </code>
            为
            <code>
                false（这是默认的值）
            </code>
            时，设置
            <code>
                dataSource
            </code>
            property会导致失败，你的data source将不会被用到。
        </p>
    </div>
    <p>
        为了遵守这个协议，你需要实现来自这个协议中的两个方法：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-comment">// Returns the number of items that the data source manages for the combo box</span>
<span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">numberOfItems</span><span class="hljs-params">(<span class="hljs-keyword">in</span> comboBox: NSComboBox)</span></span> -&gt; <span class="hljs-type">Int</span> {
  <span class="hljs-comment">// anArray is an Array variable containing the objects</span>
  <span class="hljs-keyword">return</span> anArray.<span class="hljs-built_in">count</span>
}
    
<span class="hljs-comment">// Returns the object that corresponds to the item at the specified index in the combo box</span>
<span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">comboBox</span><span class="hljs-params">(<span class="hljs-number">_</span> comboBox: NSComboBox, objectValueForItemAt index: Int)</span></span> -&gt; <span class="hljs-type">Any</span>? {
  <span class="hljs-keyword">return</span> anArray[index]
}
</pre>
    <p>
        最后，无论什么时候你的数据源发生变化，为了更新这个控件，只需调用combo box上的
        <code>
            reloadData()
        </code>
        方法。
    </p>
    <h3>
        该使用哪个方法？
    </h3>
    <p>
        如果你的项目列表相对较小，并且你并不需要经常改变它，一次性地添加到内部列表中可能就是最佳的选择了。但如果你的项目列表很大，或者是动态的，使用data source来进行处理就会显得更有效率。在这篇教程中，我们将使用方法1。
    </p>
    <p>
        既然你已经掌握了combo box的基础，就马上到你的app中实现一个吧！:]
    </p>
    <h2>
        一个Bar - 一个名词
    </h2>
    <p>
        在这个部分，你将添加一个combo box来输入一个名词。你可以选择从列表中输入，或者自己来输入。
    </p>
    <p>
        首先，添加一个label来描述控件的目的。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        。找到
        <em>
            Object Library
        </em>
        面板中的
        <em>
            Label
        </em>
        控件，并拖拽它到content view上。改变它的alignment值为
        <em>
            Right
        </em>
        ，它的标题为
        <em>
            Singular Noun:
        </em>
        。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            作为替代的捷径，按住
            <em>
                Option
            </em>
            键并拖拽一个存在的label来复制它。这么做是非常方便的，你可以保持和已存在label相同的尺寸和property值。
        </p>
    </div>
    <p>
        找到
        <em>
            Combo Box
        </em>
        控件并将它拖拽到content view上，将它放置到label的右边。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/addcombo.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/addcombo-650x481.png"
            alt="addcombo" width="650" height="481" class="aligncenter size-large wp-image-153175"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/addcombo-650x481.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/addcombo-433x320.png 433w, https://koenig-media.raywenderlich.com/uploads/2017/01/addcombo.png 1471w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        现在你需要添加一个
        <code>
            NSComboBox
        </code>
        outlet到view controller上。使用你在text field上相同的技术：选择
        <em>
            Assistant Editor
        </em>
        （确保
        <em>
            ViewController.swift
        </em>
        已选中）并
        <em>
            按住Ctrl拖拽
            Ctrl-Drag
        </em>
        combo box到
        <code>
            ViewController
        </code>
        类上，就在
        <code>
            NSTextField
        </code>
        的下方：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/combo-outlet.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/combo-outlet-650x382.png"
            alt="combo-outlet" width="650" height="382" class="aligncenter size-large wp-image-153176"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/combo-outlet-650x382.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/combo-outlet-480x282.png 480w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
        在出现的窗口中，命名outlet为
        <em>
            singularNounCombo
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/combo-outlet-2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/combo-outlet-2.png"
            alt="combo-outlet-2" width="400" height="227" class="aligncenter size-full wp-image-150151"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/combo-outlet-2.png 496w, https://koenig-media.raywenderlich.com/uploads/2016/12/combo-outlet-2-480x273.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/combo-outlet-2-266x151.png 266w"
            sizes="(max-width: 400px) 100vw, 400px">
        </a>
    </p>
    <p>
        现在
        <code>
            NSComboBox
        </code>
        property就被连接到了combo box控件上。接下来添加一些数据来填充这个列表。
    </p>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        并添加下面的代码到outlets的下方：
    </p>
    <pre lang="swift" class="hljs javascript">fileprivate <span class="hljs-keyword">let</span> singularNouns = [<span class="hljs-string">"dog"</span>, <span class="hljs-string">"muppet"</span>, <span class="hljs-string">"ninja"</span>, <span class="hljs-string">"pirate"</span>, <span class="hljs-string">"dev"</span> ]
</pre>
    <p>
        现在，添加下列的代码到
        <em>
            viewDidLoad()
        </em>
        方法的尾部：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-comment">// Setup the combo box with singular nouns</span>
singularNounCombo.removeAllItems()
singularNounCombo.addItems(withObjectValues: singularNouns)
singularNounCombo.selectItem(at: singularNouns.<span class="hljs-built_in">count</span>-<span class="hljs-number">1</span>)
</pre>
    <p>
        第一行代码移除了所有默认添加的项目。接下来，它使用
         <code>
            addItems()
        </code>
        方法添加来自
        <code>
            singularNouns
        </code>
        的名称到了combo box中。然后，它选择了列表中的最后一个项目。
    </p>
    <p>
        运行app来查看你的combo box的动作！
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-combo.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-combo-409x320.png"
            alt="buildrun-combo" width="409" height="320" class="aligncenter size-medium wp-image-153178"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-combo-409x320.png 409w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-combo-639x500.png 639w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-combo.png 672w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <p>
        Great - 看起来似乎一切正常。如果你点击combo box，你就可以在接下来查看并选择任一其它的项目。
    </p>
    <p>
        现在，如果你想要展示一个选择的列表，但不允许你自己输入，该怎么办呢？继续阅读，还有一个控件！
    </p>
    <h2>
        砰!鼹鼠要跑掉啦 - NSPopupButton
    </h2>
    <p>
        pop up button让用户可以从一个选项的列表中进行选择，但不允许用户在控件中输入它们自己的值。在macOS中负责这项工作的控件是
        <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Classes/NSPopUpButton_Class/Reference/Reference.html"
        title="NSPopupButton Class Reference">
            NSPopupButton
        </a>
        。
    </p>
    <p>
        Pop up button在macOS中非常常用，你可以在几乎每个应用中找到它们 - 包含你正在使用的这个：Xcode！:] 你正在使用pop up button来设置很多你在这篇教程中使用的macOS控件上的property，就像下面的截图中一样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/popup-example.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/popup-example-445x320.png"
            alt="popup-example" width="445" height="320" class="aligncenter size-medium wp-image-150155"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/popup-example-445x320.png 445w, https://koenig-media.raywenderlich.com/uploads/2016/12/popup-example.png 614w"
            sizes="(max-width: 445px) 100vw, 445px">
        </a>
    </p>
    <h3>
        填充空格 - 添加项目到Pop Up Button上
    </h3>
    <p>
        正如你所期望的，添加项目到
        <code>
            NSPopUpButton
        </code>
        就类似于添加项目到
        <code>
            NSComboBox
        </code>
        上 - 除了
        <code>
            NSPopUpButton
        </code>
        不支持使用data source来为这个控件填充内容。
        <code>
            NSPopUpButton
        </code>
        持有着一个内部的项目的列表，并暴露了几个方法来操纵它：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-comment">// Add an item to the list</span>
myPopUpbutton.addItem(withTitle: <span class="hljs-string">"Pop up buttons rock"</span>)

<span class="hljs-comment">// Add an array of items to the list</span>
myPopUpbutton.addItems(withTitles: [<span class="hljs-string">"Item 1"</span>, <span class="hljs-string">"Item 2"</span>, <span class="hljs-string">"Item 3"</span>])

<span class="hljs-comment">// Remove all items from the list</span>
myPopUpbutton.removeAllItems()

<span class="hljs-comment">// Get the index of the currently selected item</span>
<span class="hljs-keyword">let</span> selectedIndex = myPopUpbutton.indexOfSelectedItem

<span class="hljs-comment">// Select an item at a specific index</span>
myPopUpbutton.selectItem(at: <span class="hljs-number">1</span>)
</pre>
    <p>
        相当的直截了当，不是么？这就是macOS控件的美 - 用来操纵控件的方法会有很多的相似之处。
    </p>
    <p>
        是时候在你的app中实现一个pop up button了！:]
    </p>
    <h2>
        越多越愉快 - 复数的名词
    </h2>
    <p>
        现在你将添加一个pop up button到你的Mad Libs app上，去选择不同的复数名词来填充你的滑稽的句子。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        。拖拽一个label到
        <em>
            Singular Noun
        </em>
        label的下面。
    </p>
    <p>
        改变对齐方式为
        <em>
            靠右
        </em>
        ，title为
        <em>
            Plural Noun:
        </em>
        。接下来，找到
        <em>
            Pop Up Button
        </em>
        控件并把它拖到窗口上，把它放到label的右边。
    </p>
    <p>
        这个content view应当看起来像这样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/add-popup.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/add-popup-650x478.png"
            alt="add-popup" width="650" height="478" class="aligncenter size-large wp-image-153180"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/add-popup-650x478.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/add-popup-435x320.png 435w, https://koenig-media.raywenderlich.com/uploads/2017/01/add-popup.png 1033w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        现在你需要添加一个outlet到popup button上，现在你应该对此相当熟悉了：打开
        <em>
            Assistant editor
        </em>
        ，确认
        <em>
            ViewController.swift
        </em>
        已被选中，然后
        <em>
            按住Ctrl拖拽
        </em>
        pop up button到
        <code>
            ViewController
        </code>
        类上来创建一个新的outlet：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-popup.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-popup-650x424.png"
            alt="drag-popup" width="650" height="424" class="aligncenter size-large wp-image-153181"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-popup-650x424.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/drag-popup-480x313.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/drag-popup.png 1495w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
        在弹出的窗口中，将outlet命名为
        <em>
            pluralNounPopup
        </em>
        ：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/popup-outlet-2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/popup-outlet-2.png"
            alt="popup-outlet-2" width="400" height="244" class="aligncenter size-full wp-image-150159">
        </a>
    </p>
    <p>
        现在你只需要添加一些数据来填充控件了！
    </p>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        并添加下面的property到类的实现中。
    </p>
    <pre lang="swift" class="hljs javascript">fileprivate <span class="hljs-keyword">let</span> pluralNouns = [<span class="hljs-string">"tacos"</span>, <span class="hljs-string">"rainbows"</span>, <span class="hljs-string">"iPhones"</span>, <span class="hljs-string">"gold coins"</span>]
</pre>
    <p>
        现在，添加下面的代码到
        <code>
            viewDidLoad()
        </code>
        的底部：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-comment">// Setup the pop up button with plural nouns</span>
pluralNounPopup.removeAllItems()
pluralNounPopup.addItems(withTitles: pluralNouns)
pluralNounPopup.selectItem(at: <span class="hljs-number">0</span>)
</pre>
    <p>
        第一行代码移除了所有pop up button中已存的项目。第二行代码则使用
        <code>
            addItems()
        </code>
        方法添加了名词的数组。最后，选中列表中的第一个项目。
    </p>
    <p>
        运行app查看结果：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-popup.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-popup-407x320.png"
            alt="buildrun-popup" width="407" height="320" class="aligncenter size-medium wp-image-153182"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-popup-407x320.png 407w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-popup-635x500.png 635w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-popup.png 672w"
            sizes="(max-width: 407px) 100vw, 407px">
        </a>
    </p>
    <p>
        当app启动时，注意到pop up button会展示初始的项目，
        <em>
            tacos
        </em>
        ，如果你点击pop up button，你就会看到在列表中的其它项目。
    </p>
    <p>
        OK，现在你已经有了两个让用户可以从列表中进行选择的macOS控件，以及一个让用户可以输入单行文本的控件。但如果你需要在text field中输入不仅仅几个单词，该怎么办呢？
    </p>
    <p>
        继续阅读来学习text view！
    </p>
    <h2>
        文本是下一个 - NSTextView
    </h2>
    <p>
        Text view和text field不同，通常是作为展示富文本的控件。它甚至会允许一些更高级的特性，诸如展示行内的图像。
    </p>
    <p>
        在macOS中，负责这个的控件是
        <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Classes/NSTextView_Class/Reference/Reference.html"
        title="NSTextView Class Reference">
            NSTextView
        </a>
        。
    </p>
    <p>
        一个全部使用由
        <code>
            NSTextView
        </code>
        提供的特性的应用的例子就是TextEdit了：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/textedit.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/textedit-650x210.png"
            alt="textedit" width="650" height="210" class="aligncenter size-large wp-image-150163"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/textedit-650x210.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/12/textedit-480x155.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/textedit.png 1430w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        <code>
            NSTextView
        </code>
        的特性非常的丰富，如果要覆盖所有的特性，可能就得单独得出一个对于它的教程。因此这里你只会看到一些能够让你的app运行起来的基本的特性。（你是不是松了一口气？）:]
    </p>
    <p>
        这里有一些你需要在text views上使用的基本方法：
    </p>
    <pre lang="swift" class="hljs cs"><span class="hljs-comment">// Get the text from a text view</span>
<span class="hljs-keyword">let</span> text = myTextView.<span class="hljs-keyword">string</span>

<span class="hljs-comment">// Set the text of a text view</span>
myTextView.<span class="hljs-keyword">string</span> = <span class="hljs-string">"Text views rock too!"</span>

<span class="hljs-comment">// Set the background color of a text view</span>
myTextView.backgroundColor = NSColor.white

<span class="hljs-comment">// Set the text color of a text view</span>
myTextView.textColor = NSColor.black
</pre>
    <p>
        相对地简单 - 这里没有太让人震惊的事。
    </p>
    <p>
        <code>
            NSTextView
        </code>
        也內建了对
        <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Reference/Foundation/Classes/NSAttributedString_Class/Reference/Reference.html"
        title="NSAttributedString Class Reference">
            NSAttributedString
        </a>
        的支持。如果你向text view传递了一个attributed string，这个string就会使用所有诸如字体，字体大小，字体颜色等恰当的属性正确地展示出来。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            attributed string是特殊类型的string，你可以将string的子集标记为不同的属性 - 诸如字体，它的颜色，是否加粗，等等。要了解全部的attributed strings，请访问我们的
            <a href="https://www.raywenderlich.com/77092/text-kit-tutorial-swift" target="_blank">
                TextKit教程
            </a>
            。这是一个iOS教程，但有关
            <code>
                NSAttributedString
            </code>
            的信息也可以用到Mac开发上面。
        </p>
    </div>
    <h2>
        支付的短语 - 添加一个Text View
    </h2>
    <p>
        看起来，你已经拥有了所有添加一个text view到你的Mad Libs app所需的知识！这个text view将允许用户输入一个多行的短语，用在最终渲染的Mad Lib上面。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        并拖拽一个label到
        <em>
            Plural Noun
        </em>
        label（或复制一个已存在的label，就像之前提到的一样）的下面。将对齐方式改为
        <em>
            Right
        </em>
        ，标题设置为
        <em>
            Phrase:
        </em>
        。
    </p>
    <p>
        接下来，找到
        <em>
            Text View
        </em>
        控件并把它拖到窗口上，放到你刚创建的label的旁边。
    </p>
    <p>
        你的窗口现在看起来应该是这样的：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/add-textview.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/add-textview-650x491.png"
            alt="add-textview" width="650" height="491" class="aligncenter size-large wp-image-153184"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/add-textview-650x491.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/add-textview-423x320.png 423w, https://koenig-media.raywenderlich.com/uploads/2017/01/add-textview.png 1439w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        现在，如果你尝试改变view的大小，并让它变得更高，你会注意到一些相当特别的事。text view会独自移动，在你改变窗口大小的时候改变它的位置。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-error.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-error-304x320.png"
            alt="textview-error" width="304" height="320" class="aligncenter size-medium wp-image-153185"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-error-304x320.png 304w, https://koenig-media.raywenderlich.com/uploads/2017/01/textview-error-474x500.png 474w, https://koenig-media.raywenderlich.com/uploads/2017/01/textview-error.png 683w"
            sizes="(max-width: 304px) 100vw, 304px">
        </a>
    </p>
    <p>
        这是因为默认情况下，Xcode会为text view添加Auto resizing的约束，因此它会在父view的大小改变的时候改变它自身的位置。由于你想让text view的位置保证固定，你就需要禁用一些约束。
    </p>
    <p>
        从Document Outline中选择
        <em>
            Bordered Scroll View – Text View
        </em>
        并前往
        <em>
            Size Inspector
        </em>
        。
    </p>
    <p>
        在
        In the
        <em>
            AutoResizing
        </em>
        部分，你会看到一个带有四条连接到父view的红线的矩形。每一个红色的“连接器”都代表了一个Auto resizing的约束。你只需要点击
        <em>
            右边
        </em>
        和
        <em>
            下面
        </em>
        的红色连接器来禁用它们，红色的实现就会变成带有褪色红色的虚线，就像下面这样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/add-autores.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/add-autores.png"
            alt="add-autores" width="344" height="109" class="aligncenter size-full wp-image-153187">
        </a>
    </p>
    <p>
        现在，即使你改变了窗口的大小，text view仍会保持它的位置和对齐方式。
    </p>
    <p>
        下面，添加一个
        <code>
            NSTextView
        </code>
        outlet到view controller上。选择textview，打开
        <em>
            Assistant editor
        </em>
        并确保
        <em>
            ViewController.swift
        </em>
        已选中。
        <em>
            按住Ctrl拖拽
        </em>
        text view到
        <code>
            ViewController
        </code>
        类中已存在的outlet的下面。
    </p>
    <div class="note">
        <p>
            <em>
                重点：
            </em>
            Text view内部包含了Text view。在创建outlet前，确保你选中的是text view。要做到这个，只需在text view上单击三次，或在
            <em>
                Document Outline
            </em>
            中选中它。
        </p>
    </div>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-drag.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-drag-650x447.png"
            alt="textview-drag" width="650" height="447" class="aligncenter size-large wp-image-153188"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-drag-650x447.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/textview-drag-465x320.png 465w, https://koenig-media.raywenderlich.com/uploads/2017/01/textview-drag.png 1393w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        在弹出的窗口中，确定类型为
        <code>
            NSTextView
        </code>
        ，并命名outlet为
        <em>
            phraseTextView
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/textview-outlet2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/textview-outlet2.png"
            alt="textview-outlet2" width="400" height="227" class="aligncenter size-full wp-image-150166"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/textview-outlet2.png 496w, https://koenig-media.raywenderlich.com/uploads/2016/12/textview-outlet2-480x273.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/textview-outlet2-266x151.png 266w"
            sizes="(max-width: 400px) 100vw, 400px">
        </a>
    </p>
    <p>
        现在，添加下列的代码到
        <em>
            viewDidLoad()
        </em>
        的尾部：
    </p>
    <pre lang="swift" class="hljs cs"><span class="hljs-comment">// Setup the default text to display in the text view</span>
phraseTextView.<span class="hljs-keyword">string</span> = <span class="hljs-string">"Me coding Mac Apps!!!"</span>
</pre>
    <p>
        运行app，查看结果：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-result.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-result-355x320.png"
            alt="textview-result" width="355" height="320" class="aligncenter size-medium wp-image-153189"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-result-355x320.png 355w, https://koenig-media.raywenderlich.com/uploads/2017/01/textview-result-554x500.png 554w, https://koenig-media.raywenderlich.com/uploads/2017/01/textview-result.png 672w"
            sizes="(max-width: 355px) 100vw, 355px">
        </a>
    </p>
    <p>
        太棒了！Mad Libs app现在开始真正地成型了。
    </p>
    <h2>
        推出你的按钮 - NSButton
    </h2>
    <p>
        Button是当用户点击它时，向app发送一个消息的macOS控件。
    </p>
    <p>
        在macOS中，负责这个的控件是
        <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Classes/NSButton_Class/Reference/Reference.html"
        title="NSButton Class Reference">
            NSButton
        </a>
        。
    </p>
    <p>
        有很多不同风格的button（你可以在Interface Builder的Object Library中查看它们）。它们都以相同的方式工作，唯一的区别只是外观不同。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/button-catalog-1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/button-catalog-1-476x500.png"
            alt="button-catalog" width="476" height="500" class="aligncenter size-large wp-image-150182"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/button-catalog-1-476x500.png 476w, https://koenig-media.raywenderlich.com/uploads/2016/12/button-catalog-1-305x320.png 305w, https://koenig-media.raywenderlich.com/uploads/2016/12/button-catalog-1.png 1090w"
            sizes="(max-width: 476px) 100vw, 476px">
        </a>
        你应当使用最匹配你的应用设计风格的button - 引用自
        <a href="https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/OSXHIGuidelines/ControlsButtons.html#//apple_ref/doc/uid/20000957-CH48-SW1">
            macOS人机交互指南
        </a>
        中，关于你的app的最佳设计实践的建议和指导。
    </p>
    <p>
        一般地，当使用button的时候，你只需要关联一个动作到button上，并设置它的标题。然而，你可能需要禁用按钮，或改变它的外观。下面的方法让你可以执行这些操作：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-comment">// disable a button</span>
myButton.isEnabled = <span class="hljs-literal">false</span>

<span class="hljs-comment">// enable a button</span>
myButton.isEnabled = <span class="hljs-literal">true</span>

<span class="hljs-comment">// getting &amp; setting a button's title</span>
<span class="hljs-keyword">let</span> theTitle = myButton.title
myButton.title = theTitle

<span class="hljs-comment">// getting &amp; setting a button's image</span>
<span class="hljs-keyword">let</span> theImage = myButton.image
myButton.image = theImage
</pre>
    <p>
        看起来相当地简单 - 在下一部分添加一个按钮到你的app上应当是相当容易的。
    </p>
    <h2>
        按钮事务落定 - 添加一个Button
    </h2>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        。在Object Library的面板中找到
        <em>
            Push Button
        </em>
        ，并将它拖拽到content view上。双击它来改变它的标题为
        <em>
            Go!
        </em>
        ：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/button-add.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/button-add-614x500.png"
            alt="button-add" width="614" height="500" class="aligncenter size-large wp-image-153191"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/button-add-614x500.png 614w, https://koenig-media.raywenderlich.com/uploads/2017/01/button-add-393x320.png 393w, https://koenig-media.raywenderlich.com/uploads/2017/01/button-add.png 1474w"
            sizes="(max-width: 614px) 100vw, 614px">
        </a>
    </p>
    <p>
        这次你不需要为button创建outlet。然而，你确实需要创建一个动作并将它关联到button上，这样你的app就知道button是何时被点击的了！:]
    </p>
    <p>
        打开
        <em>
            Assistant Editor
        </em>
        并
        <em>
            按住Ctrl拖拽
        </em>
        button到
        <code>
            ViewController
        </code>
        的实现中。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/button-addaction.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/button-addaction-650x373.png"
            alt="button-addaction" width="650" height="373" class="aligncenter size-large wp-image-153194"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/button-addaction-650x373.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/button-addaction-480x276.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/button-addaction.png 1435w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        在出现的窗口中，确保connection被设置为
        <em>
            Action
        </em>
        。将action命名为
        <em>
            goButtonClicked
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/button-action-2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/button-action-2-480x229.png"
            alt="button-action-2" width="400" height="190" class="aligncenter size-medium wp-image-150171"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/button-action-2-480x229.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/button-action-2.png 504w"
            sizes="(max-width: 400px) 100vw, 400px">
        </a>
    </p>
    <p>
        当用户点击按钮时，方法
        <code>
            goButtonClicked()
        </code>
        就会被调用。现在，你只是在这里添加一个debug代码，来确保一切工作正常。
    </p>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        并添加下列的代码到
        <code>
            goButtonClicked()
        </code>
        中：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-keyword">let</span> pastTenseVerb = pastTenseVerbTextField.stringValue
<span class="hljs-keyword">let</span> singularNoun = singularNounCombo.stringValue
<span class="hljs-keyword">let</span> pluralNoun = pluralNouns[pluralNounPopup.indexOfSelectedItem]
<span class="hljs-keyword">let</span> phrase = phraseTextView.string ?? <span class="hljs-string">""</span>

<span class="hljs-keyword">let</span> madLibSentence = <span class="hljs-string">"A <span class="hljs-subst">\(singularNoun)</span> <span class="hljs-subst">\(pastTenseVerb)</span> <span class="hljs-subst">\(pluralNoun)</span> and said, <span class="hljs-subst">\(phrase)</span>!"</span>

<span class="hljs-built_in">print</span>(<span class="hljs-string">"<span class="hljs-subst">\(madLibSentence)</span>"</span>)
</pre>
    <p>
        上面的代码从text field、combo box、popup button，以及text view获取了字符串，并构成了Mad Lib的句子。
    </p>
    <p>
        注意text view
        <code>
            string
        </code>
        这个property事实上是可选的，因此它可以是
        <code>
            nil
        </code>
        。要避免这种情况，你可以使用nil coalescing操作符
        <code>
            ??
        </code>
        因此如果
        <code>
            string
        </code>
        是nil，你就会得到
        <code>
            ""
        </code>
        来代替。
    </p>
    <p>
        这就是到目前为止你所需的全部代码 - 运行你的app。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/button-buildrun.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/button-buildrun-458x320.png"
            alt="button-buildrun" width="458" height="320" class="aligncenter size-medium wp-image-153195"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/button-buildrun-458x320.png 458w, https://koenig-media.raywenderlich.com/uploads/2017/01/button-buildrun-650x455.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/button-buildrun.png 672w"
            sizes="(max-width: 458px) 100vw, 458px">
        </a>
        <br>
        每次当你单击按钮的时候，你银弹看到一个又短又傻的句子出现在Xcode的控制台中。
    </p>
    <pre lang="bash" class="hljs">A dev ate tacos and said: Me coding Mac Apps!!!!
</pre>
    <p>
        非常棒，但怎样可以让它变得更加有趣？
    </p>
    <p>
        让你的电脑来阅读句子怎么样？Steve Jobs让第一台Macintosh在它的发布会上向世界说hello。你也可以让你的电脑说话...让我们来吧！
    </p>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        并添加下列的代码到
        <code>
            ViewController
        </code>
        的实现中：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-comment">// 1</span>
fileprivate <span class="hljs-class"><span class="hljs-keyword">enum</span> <span class="hljs-title">VoiceRate</span>: <span class="hljs-title">Int</span>  </span>{
  <span class="hljs-keyword">case</span> slow
  <span class="hljs-keyword">case</span> normal
  <span class="hljs-keyword">case</span> fast

  <span class="hljs-keyword">var</span> speed: <span class="hljs-type">Float</span> {
    <span class="hljs-keyword">switch</span> <span class="hljs-keyword">self</span> {
    <span class="hljs-keyword">case</span> .slow:
      <span class="hljs-keyword">return</span> <span class="hljs-number">60</span>
    <span class="hljs-keyword">case</span> .normal:
      <span class="hljs-keyword">return</span> <span class="hljs-number">175</span>;
    <span class="hljs-keyword">case</span> .fast:
      <span class="hljs-keyword">return</span> <span class="hljs-number">360</span>;
    }
  }
}
<span class="hljs-comment">//2</span>
fileprivate <span class="hljs-keyword">let</span> synth = <span class="hljs-type">NSSpeechSynthesizer</span>()
</pre>
    <p>
        首先，你声明了一个
        <code>
            enum
        </code>
        来代表声速。然后你创建了一个
        <code>
            NSSpeechSynthesizer
        </code>
        的实例，它会将文本朗读出来。
    </p>
    <p>
        现在，添加这个代码到
        <code>
            ViewController
        </code>
        的实现中：
    </p>
    <pre lang="swift" class="hljs swift">fileprivate <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">readSentence</span><span class="hljs-params">(<span class="hljs-number">_</span> sentence: String, rate: VoiceRate )</span></span> {
  synth.rate = rate.speed
  synth.stopSpeaking()
  synth.startSpeaking(sentence)
}
</pre>
    <p>
        该方法启动
        <code>
            synth
        </code>
        对象来以被选中的速度朗读一个字符串。
    </p>
    <p>
        是时候来调用它了！添加下列代码到
        <code>
            goButtonClicked()
        </code>
        方法的尾部来朗读Mad Libs的句子：
    </p>
    <pre lang="swift" class="hljs bash"><span class="hljs-built_in">read</span>Sentence(madLibSentence, rate: .normal)
</pre>
    <p>
        运行项目；点击
        <em>
            Go!
        </em>
        ，听你的Mac大声朗读出你的句子！
    </p>
    <h2>
        从这儿去向哪里？
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
        你可以下载
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibs-part1-final-1.zip">
            最终的项目
        </a>
        ，它包含了教程到目前为止所提到内容的全部的源码。
    </p>
    <p>
        在这个教程的
        <a href="https://www.raywenderlich.com/149297/macos-controls-tutorial-part-22"
        target="_blank" title="Core Controls in macOS: Part 2/2">
            第二部分
        </a>
        ，你会了解到更多关于macOS控件的知识，包括sliders，date pickers，
        radio buttons，check boxes以及image views - 每个控件都会添加到你的Mad Lib app上来完成它。
    </p>
</div>
