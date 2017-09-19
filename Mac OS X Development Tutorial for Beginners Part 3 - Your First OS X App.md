# macOS X 初学者开发教程 第三部分 你的第一个OS X App

#### [原文地址](https://www.raywenderlich.com/110269/mac-os-x-development-tutorial-beginners-part-3-first-os-x-app) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <img class="alignright size-full wp-image-121216 bordered" src="https://koenig-media.raywenderlich.com/uploads/2015/11/featureImage_250.png"
        alt="featureImage_250" width="250" height="250" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/featureImage_250.png 250w, https://koenig-media.raywenderlich.com/uploads/2015/11/featureImage_250-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/11/featureImage_250-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2015/11/featureImage_250-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2015/11/featureImage_250-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
    	欢迎回到我们的Max OS X新手开发教程的第三部分！
    </p>
    <p>
    	这个关于在OS X上build app的引导性的系列，包含很多的东西（ground）。这些是你已学到的：
    </p>
    <ul>
        <li>
            <em>
                Tooling
            </em>
            ：在
            <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Mac%20OS%20X%20Development%20Tutorial%20for%20Beginners%20Part%201%20-%20Intro%20to%20Xcode.md"
            sl-processed="1">
            	第一部分
            </a>
            你学到了Xcode的很多方面 - “瞥”（glimpse）了一眼你可以怎么来用它开始OS X的开发。
        </li>
        <li>
            <em>
                App剖析
            </em>
            ：
            <a href="http://www.raywenderlich.com/110267/mac-os-x-development-tutorial-for-beginners-part-2-os-x-app-anatomy"
            sl-processed="1">
                second part
                第二部分
            </a>
            包含了很多的OS X app在背后如何构建的理论 - 从数据层，到二进制的资源，再到设计UI。
        </li>
    </ul>
    <p>
    	在这个第三也就是最后一部分，你将通过创造你史无前例的第一个app，来潜入（dive deep into）OS X开发的世界！
    </p>
    <p>
    	你将要build的app是一个
    	<em>
    		magic-8 ball app
    	</em>
    	，来帮助你做出一天天生活中的困难的决定。你将从涂画（scratch）开始 - 在继续创造app来解决你的所有问题前，首先创造一个“Hello World!” app！
    </p>
    <div class="note">
        <em>
        	注意
            Note:
        </em>
        这个app要求OS X El Capitan操作系统和Xcode7.1及以上的版本 - 确认你在尝试跟随这个教程之前已升级。
    </div>
    <h2>
        开始啦
    </h2>
    <p>
        打开Xcode并点击
        <em>
            Create a new Xcode project
        </em>
        来启动你的新app。选择
        <em>
            OS X
        </em>
        <em>
            \
        </em>
        <em>
            Application
        </em>
        <em>
            \
        </em>
        <em>
            Cocoa Application
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121075" src="https://koenig-media.raywenderlich.com/uploads/2015/11/01_project_template-451x320.png"
        alt="01_project_template" width="451" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/01_project_template-451x320.png 451w, https://koenig-media.raywenderlich.com/uploads/2015/11/01_project_template-700x497.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/01_project_template.png 1460w"
        sizes="(max-width: 451px) 100vw, 451px">
    </p>
    <p>
        设置产品名称为
        <em>
            MagicEight
        </em>
        ，语言为
        <em>
            Swift
        </em>
        并确保
        <em>
            Use Storyboards
        </em>
        被勾选：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121076" src="https://koenig-media.raywenderlich.com/uploads/2015/11/02_project_options-450x320.png"
        alt="02_project_options" width="450" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/02_project_options-450x320.png 450w, https://koenig-media.raywenderlich.com/uploads/2015/11/02_project_options-700x498.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/02_project_options.png 1462w"
        sizes="(max-width: 450px) 100vw, 450px">
    </p>
    <p>
        选择一个磁盘上的位置来保存你的项目，并点击
        <em>
            Create
        </em>
        来打开你的空项目。
    </p>
    <p>
        运行
        <em>
            MagicEight
        </em>
        来检查每一项正在工作：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121077" src="https://koenig-media.raywenderlich.com/uploads/2015/11/03_bar_01-480x292.png"
        alt="03_bar_01" width="480" height="292" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/03_bar_01-480x292.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/03_bar_01-700x426.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/03_bar_01.png 962w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        很好 - 这样app运行起来了，但它确实
        <i>
            没有做任何事
        </i>
        。这样地启动了一个新的平台却没有首先创建“Hello World!”大概是不对的...
    </p>
    <h2>
        Hello World!
    </h2>
    <p>
        OS X app的用户界面是由你使用interface builder编辑的storyboard文件提供的，它让你用一种可见的方式来编辑UI，减少了大量你必须去写的复杂的代码。
    </p>
    <p>
        通过在左手边窗格中的Project Navigator中选择
        <em>
            Main.storyboard
        </em>
        来打开它：        
    </p>
    <p>
        <img class="aligncenter wp-image-121078 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/04_project_navigator-e1448290107849-357x320.png"
        alt="04_project_navigator" width="357" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/04_project_navigator-e1448290107849-357x320.png 357w, https://koenig-media.raywenderlich.com/uploads/2015/11/04_project_navigator-e1448290107849.png 424w"
        sizes="(max-width: 357px) 100vw, 357px">
    </p>
    <p>
        你会看到现在storyboard已打开在了中部的面板：
    </p>
    <p>
        <img class="aligncenter wp-image-121079 size-full" src="https://koenig-media.raywenderlich.com/uploads/2015/11/05_storyboard.png"
        alt="05_storyboard" width="666" height="896" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/05_storyboard.png 666w, https://koenig-media.raywenderlich.com/uploads/2015/11/05_storyboard-238x320.png 238w, https://koenig-media.raywenderlich.com/uploads/2015/11/05_storyboard-372x500.png 372w"
        sizes="(max-width: 666px) 100vw, 666px">
    </p>
    <p>
        模板的storyboard包含三个组件：
    </p>
    <ul>
        <li>
            <em>
                Menu Bar
            </em>
            ：控制当app运行时出现的菜单。
        </li>
        <li>
            <em>
                Window Controller
            </em>
            ：管理出现的默认窗口。使用一个或多个view controller来管理它们的内容。
        </li>
        <li>
            <em>
                View Controller
            </em>
            负责window中的一个区域，来展示和处理用户的交互。
        </li>
    </ul>
    <p>
        在这个引导性的教程中，你将集中你的努力到view controller上。
    </p>
    <h3>
        添加一个Label
    </h3>
    <p>
        首先，你需要添加一个label到view controller上来展示你的欢迎文本。label事实上特定的类型是
        <code>
            NSTextField
        </code>
        ，它被设计来展示一个单行的不可编辑的文本 - 对“Hello World”来说完美。
    </p>
    <p>
        为了添加你的第一个label：
    </p>
    <ol start="1">
        <li>
            点击在工具栏中的图标来展示右手边的工具面板（utilities panel）。
        </li>
        <li>
            使用靠近面板底部的图标来打开
            <em>
                Object Library
            </em>
            。这个，就如同它名称所表达的一样，是一个你可以拖拽到storyboard画布上的物品的目录，用来构建你的布局。
        </li>
        <li>
            使用底部的搜索框搜索
            <em>
                label
            </em>
            。
        </li>
        <li>
            你会发现label对象在library中被高亮了起来。
        </li>
    </ol>
    <p>
        <img class="aligncenter wp-image-121080 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/11/06_object_library-332x500.png"
        alt="06_object_library" width="332" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/06_object_library-332x500.png 332w, https://koenig-media.raywenderlich.com/uploads/2015/11/06_object_library-213x320.png 213w, https://koenig-media.raywenderlich.com/uploads/2015/11/06_object_library.png 520w"
        sizes="(max-width: 332px) 100vw, 332px">
    </p>
    <p>
        将label从object library拖拽到view controller上：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121081" src="https://koenig-media.raywenderlich.com/uploads/2015/11/07_label_vc-480x137.png"
        alt="07_label_vc" width="480" height="137" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/07_label_vc-480x137.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/07_label_vc-700x200.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/07_label_vc.png 986w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        为了label的文本内容，在Utilities panel中选择
        <em>
            Attributes Inspector
        </em>
        这个tab，找到
        <em>
            Title
        </em>
        域，并输入
        <em>
            Hello World!
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter wp-image-121082 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/08_hello_world-e1448325932458-480x168.png"
        alt="08_hello_world" width="480" height="168" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/08_hello_world-e1448325932458-480x168.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/08_hello_world-e1448325932458.png 517w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        你可以使用attributes inspector来控制OS X提供的不同的组件的外观和行为。找到
        <em>
            Font
        </em>
        入口，点击右边的
        <em>
            T
        </em>
        图标来打开字体面板。改变Style为
        <em>
            Thin
        </em>
        ，Size为
        <em>
            40
        </em>
        。点击
        <em>
            Done
        </em>
        来保存你的修改：
    </p>
    <p>
        <img class="aligncenter wp-image-121083 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/09_font-473x320.png"
        alt="09_font" width="473" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/09_font-473x320.png 473w, https://koenig-media.raywenderlich.com/uploads/2015/11/09_font.png 520w"
        sizes="(max-width: 473px) 100vw, 473px">
    </p>
    <p>
        将你的眼睛投回到view controller的画布上，你会看到一些奇怪的事：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121084" src="https://koenig-media.raywenderlich.com/uploads/2015/11/10_wrong_size-480x139.png"
        alt="10_wrong_size" width="480" height="139" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/10_wrong_size-480x139.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/10_wrong_size-700x202.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/10_wrong_size.png 990w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        尽管你已经调整了label的文本和大小，但它仍然是那个尺寸，造成几乎全部的文本消失了。为什么会这样？
    </p>
    <h3>
        Basic Auto Layout
        基本的自动布局
    </h3>
    <p>
    	你把label放在了view controller的画布上，但你并没有实际地告诉OS X
    	<i>
            怎么
        </i>
    	来定位它。view controller在storyboard中以一种尺寸出现，但一旦运行在app中，用户是可以改变window的尺寸的 - 因此你需要指定对于
        <i>
            任意
        </i>
        的window的尺寸，这个label该怎么定位。
    </p>
    <p>
    	这听起来是一件相当困难的任务，但幸运的是苹果会帮你（has your back）。OS X使用了一个叫做Auto Layout的强有力的布局引擎，不同view的组件之间的关系被表达为约束（constraints）。这些约束在运行时会计算view中的每个原件的尺寸和位置。
    </p>
    <div class="note">
        <em>
        	注意：
            Note:
        </em>
        Auto Layout是一个复杂的话题，在这个引导性的教程中不会覆盖任何的深度。如果你想要阅读更多关于这个话题的内容，这里有一些很棒的
        <a href="http://www.raywenderlich.com/115440/auto-layout-tutorial-in-ios-9-part-1-getting-started-2"
        sl-processed="1">
            教程
        </a>
        ，在这个地址上是面向iOS的 - 幸运的是这个引擎在这两个平台上几乎是完全相同的。
    </div>
    <p>
    	确保这个label已在view controller中被选中，单后在下面的工具栏中点击
        <em>
            Align
        </em>
        按钮。选择
        <em>
            Horizontally in Container
        </em>
        ，确定在点击
        <em>
            Add 1 Constraint
        </em>
        去添加约束前，它的值被设置为
        <em>
            0
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121085" src="https://koenig-media.raywenderlich.com/uploads/2015/11/11_align-300x320.png"
        alt="11_align" width="300" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/11_align-300x320.png 300w, https://koenig-media.raywenderlich.com/uploads/2015/11/11_align-468x500.png 468w, https://koenig-media.raywenderlich.com/uploads/2015/11/11_align.png 624w"
        sizes="(max-width: 300px) 100vw, 300px">
    </p>
    <p>
    	这会确保这个label总是出现在window的中央，无论window有多宽。你会注意到在storyboard上出现了一些“生气的”红色的线（some angry red lines）：
    </p>
    <p>
        <img class="aligncenter size-thumbnail wp-image-121086" src="https://koenig-media.raywenderlich.com/uploads/2015/11/12_angry_red-250x250.png"
        alt="12_angry_red" width="250" height="250" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/12_angry_red-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2015/11/12_angry_red-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/11/12_angry_red-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2015/11/12_angry_red-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2015/11/12_angry_red-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
    	这是因为你在水平方向上提供了一个约束来确定label的位置，但你没有提供关于数轴的任何信息。
    </p>
    <p>
    	再一次地，确定这个label在view controller中已被选中，这次点击底部Auto Layout工具栏中的
        <em>
            Pin
        </em>
        菜单。在点击
        <em>
            Add 1 Constraint
        </em>
        前，输入
        <em>
            30
        </em>
        在顶部的约束框中，确保下方的“I”型条是实心红色的：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121087" src="https://koenig-media.raywenderlich.com/uploads/2015/11/13_pin-227x320.png"
        alt="13_pin" width="227" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/13_pin-227x320.png 227w, https://koenig-media.raywenderlich.com/uploads/2015/11/13_pin-355x500.png 355w, https://koenig-media.raywenderlich.com/uploads/2015/11/13_pin.png 552w"
        sizes="(max-width: 227px) 100vw, 227px">
    </p>
    <p>
    	你会立即看到这个view controller更新了 - 你现在可以看到完全的label了，那个生气的红色的线变成了平静的蓝色：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121088" src="https://koenig-media.raywenderlich.com/uploads/2015/11/14_happy_storyboard-480x138.png"
        alt="14_happy_storyboard" width="480" height="138" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/14_happy_storyboard-480x138.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/14_happy_storyboard-700x202.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/14_happy_storyboard.png 986w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	这就是的你的“Hello World”app完成了（对于现在）。使用“play”按钮来build和运行，检查你的作品（handiwork）：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121089" src="https://koenig-media.raywenderlich.com/uploads/2015/11/15_bar_02-480x293.png"
        alt="15_bar_02" width="480" height="293" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/15_bar_02-480x293.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/15_bar_02-700x427.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/15_bar_02.png 962w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	祝贺！尽管它还不是非常个性化？在下一部分，你将发现怎么让传统的问候更友好一点。
    </p>
    <h2>
    	处理用户的输入
    </h2>
    <p>
    	在这一部分，你将添加一个text field来让用户可以输入它们的名字，这样你就可以个性化地欢迎他们了。
    </p>
    <h3>
        Control Layout
        控制布局
    </h3>
    <p>
    	在行动之前，使用object library来找到并拖拽一个
        <em>
            Text Field
        </em>
        和一个
        <em>
            Push Button
        </em>
        到view controller上。将它们放置到“Hello World!”label的上面：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121090" src="https://koenig-media.raywenderlich.com/uploads/2015/11/16_position_textfield-480x115.png"
        alt="16_position_textfield" width="480" height="115" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/16_position_textfield-480x115.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/16_position_textfield-700x168.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/16_position_textfield.png 986w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	记住，仅仅将控件放置到画布的上面是不足以让OS X理解，当window的尺寸发生变化时，你想怎么定位它们。你需要添加一些约束来传达你的意愿。
    </p>
    <p>
    	选择text field，然后
        <em>
            按住Command点击
        </em>
        button来同时选取。在storyboard底部的Auto Layout工具栏点击
        <em>
            Stack
        </em>
        图标：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121091" src="https://koenig-media.raywenderlich.com/uploads/2015/11/17_stack-480x265.png"
        alt="17_stack" width="480" height="265" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/17_stack-480x265.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/17_stack.png 604w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	这就创建了一个新的包含text field和button的stack view。stack view会自动地生成要放置和包含view在一条线上的布局约束。你可以使用attributes inspector来配置很多stack view的共同的熟悉。
    </p>
    <div class="note">
        <em>
            NOTE:
            注意：
        </em>
        <code>
            NSStackView
        </code>
        是从OS X 10.9开始支持的，但在10.11（El Capitan）时收到了一个重大的更新 - 与在iOS中介绍的（
        <code>
            UIStackView
        </code>
        ）一致。Stack view在两个平台上是类似的，因此你可以点击
        <a href="http://www.raywenderlich.com/114552/uistackview-tutorial-introducing-stack-views"
        sl-processed="1">
        	iOS的stack view教程
        </a>
        来加快学习的速度。或是稍等，
        <code>
            NSStackView
        </code>
        的教程将在接下来的几周内发布。
    </div>
    <p>
    	一旦你开始stacking，你就很难停下来了。这次，你要stack你刚创建的stack view和“Hello World!”label到一个垂直的stack view上。
    </p>
    <p>
    	使用底部工具栏左侧的按钮来展示Document Outline，然后找到“Hello World”控件和已存在的stack view。
        <i>
            按住Command点击
        </i>
        它们可以同时选择：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121092" src="https://koenig-media.raywenderlich.com/uploads/2015/11/18_document_outline-469x320.png"
        alt="18_document_outline" width="469" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/18_document_outline-469x320.png 469w, https://koenig-media.raywenderlich.com/uploads/2015/11/18_document_outline.png 674w"
        sizes="(max-width: 469px) 100vw, 469px">
    </p>
    <p>
    	和你刚才做的一样，使用底部工具栏的
        <em>
            Stack
        </em>
        按钮来创建一个新的stack view：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121093" src="https://koenig-media.raywenderlich.com/uploads/2015/11/19_stack-480x195.png"
        alt="19_stack" width="480" height="195" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/19_stack-480x195.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/19_stack-700x285.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/19_stack.png 1002w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	在这个新的stack view被选中时，打开
        <em>
            Attributes Inspector
        </em>
        并设置Alignment为
        <em>
            Center X
        </em>
        ，spacing为
        <em>
            20
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter wp-image-121094 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/20_stack_config-e1448290245207-480x306.png"
        alt="20_stack_config" width="480" height="306" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/20_stack_config-e1448290245207-480x306.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/20_stack_config-e1448290245207.png 515w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	这就确保了这个label合上面的stack view漂亮地居中了，并且它们之间有20个点的间隔。
    </p>
    <p>
    	在将你的注意力转移到处理用户输入的任务之前，有一些布局需要去完成。
    </p>
    <p>
    	stack view处理了它内容中控件相互之间的位置，但它也需要在view controller的view中被定位。选择外部的stack view并使用
        <em>
            Align
        </em>
        这个auto layout菜单，来让它在容器中居中：
    </p>
    <p>
        <img class="aligncenter wp-image-121095 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/21_align-300x320.png"
        alt="21_align" width="300" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/21_align-300x320.png 300w, https://koenig-media.raywenderlich.com/uploads/2015/11/21_align-468x500.png 468w, https://koenig-media.raywenderlich.com/uploads/2015/11/21_align.png 624w"
        sizes="(max-width: 300px) 100vw, 300px">
    </p>
    <p>
    	使用
        <em>
            Pin
        </em>
        菜单来固定住（pin）住stack view到顶部，并带有一个
        <em>
            30
        </em>
        的距离：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121096" src="https://koenig-media.raywenderlich.com/uploads/2015/11/22_pin-227x320.png"
        alt="22_pin" width="227" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/22_pin-227x320.png 227w, https://koenig-media.raywenderlich.com/uploads/2015/11/22_pin-355x500.png 355w, https://koenig-media.raywenderlich.com/uploads/2015/11/22_pin.png 552w"
        sizes="(max-width: 227px) 100vw, 227px">
    </p>
    <p>
    	最后，确保text field总是含有足够的用户名字的空间，你要修正它的宽度。
    </p>
    <p>
    	选择text field并使用底部工具栏中的
        <em>
            Pin
        </em>
        菜单，来指定
        <em>
            Width
        </em>
        为
        <em>
            100
        </em>
        。点击
        <em>
            Add 1 Constraint
        </em>
        来保存新的约束：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121097" src="https://koenig-media.raywenderlich.com/uploads/2015/11/23_textfield_width-480x311.png"
        alt="23_textfield_width" width="480" height="311" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/23_textfield_width-480x311.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/23_textfield_width-700x453.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/23_textfield_width.png 918w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	这样你的布局就较好地完成了 - 它应该看起来像下面这样：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121098" src="https://koenig-media.raywenderlich.com/uploads/2015/11/24_layout-480x176.png"
        alt="24_layout" width="480" height="176" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/24_layout-480x176.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/24_layout-700x256.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/24_layout.png 990w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	现在你可以将你的注意力转到那些你新添加的控件上了。
    </p>
    <h3>
        Outlets 和 Actions
    </h3>
    <p>
    	选择text field并打开
        <em>
            Attributes Inspector
        </em>
        。在In the Placeholder这里输入
        <em>
            Name
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter wp-image-121099 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/25_name-e1448290291815-480x249.png"
        alt="25_name" width="480" height="249" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/25_name-e1448290291815-480x249.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/25_name-e1448290291815.png 513w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	这个灰色的文本将指示用户这个text field是用来干什么的，当用户开始输入时会立即消失掉。
    </p>
    <p>
    	选择按钮，再次打开
        <em>
            Attributes Inspector
        </em>
        。设置Title为
        <em>
            Welcome
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121100" src="https://koenig-media.raywenderlich.com/uploads/2015/11/26_welcome-362x320.png"
        alt="26_welcome" width="362" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/26_welcome-362x320.png 362w, https://koenig-media.raywenderlich.com/uploads/2015/11/26_welcome.png 518w"
        sizes="(max-width: 362px) 100vw, 362px">
    </p>
    <p>
    	外观的美化就到这里了。现在是时候将这两个的控制写到代码里了。
    </p>
    <p>
    	OS X使用outlets和actions，提供了从代码和storyboard的UI交互的方法：
    </p>
    <ul>
        <li>
        	在代码中，
            <em>
                outlet
            </em>
            是一个属性，它被连接到了一个storyboard中的组件。这就让你可以从你的代码中访问在storyboard中的属性。
        </li>
        <li>
            <em>
                action
            </em>
            是一个代码中的类中的方法；当用户和UI中的组件交互时，就会调用它 - 例如，点击一个button。
        </li>
    </ul>
    <p>
    	你将为text field和label添加outlet，当用户点击欢迎按钮的时候，一个动作就会被调用。
    </p>
    <p>
    	你一直工作在的这个view controller早已有了一个骨架类关联到了代码中 - 就在
        <em>
            ViewController.swift
        </em>
        。这是你将要添加outlets和action的地方。
    </p>
    <p>
    	使用工具栏中的按钮打开assistant editor。
    </p>
    <p>
        <img class="aligncenter size-full wp-image-121101" src="https://koenig-media.raywenderlich.com/uploads/2015/11/27_assistant_editor.png"
        alt="27_assistant_editor" width="210" height="64">
    </p>
    <p>
    	这会拆分屏幕，并展示出一个代码文件在storyboard旁边。它本应该展示
        <em>
            ViewController.swift
        </em>
        ，但如果不是的话，就使用跳转栏（jump bar）来选择
        <em>
            Automatic
        </em>
        <em>
            \
        </em>
        <em>
            ViewController.swift
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter wp-image-121102 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/28_jump_bar-480x52.png"
        alt="28_jump_bar" width="480" height="52" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/28_jump_bar-480x52.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/28_jump_bar.png 596w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	从storyboard中
        <em>
	        右击拖拽
        </em>
        （或
        <em>
        	按住control拖拽
        </em>
        ）text field直到那条线到了
        <em>
            ViewController.swift
        </em>
        中的  
        <code>
            override func viewDidLoad()
        </code>
        的上边：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121103" src="https://koenig-media.raywenderlich.com/uploads/2015/11/29_textfield_outlet-700x289.png"
        alt="29_textfield_outlet" width="700" height="289" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/29_textfield_outlet-700x289.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/29_textfield_outlet-480x199.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/29_textfield_outlet.png 1417w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
    	确保
        <em>
            Outlet
        </em>
        已选中，并叫做
        <em>
            nameTextField
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121104" src="https://koenig-media.raywenderlich.com/uploads/2015/11/30_name_textfield-480x276.png"
        alt="30_name_textfield" width="480" height="276" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/30_name_textfield-480x276.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/30_name_textfield.png 530w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	这将添加下列的属性到
        <code>
            ViewController
        </code>
        中，并在加载view controller时，更新storyboard来自动地连接text field：
    </p>
	<pre class="swift" style="font-family:monospace;">@IBOutlet weak <span style="color: #a61390;">var</span> nameTextField<span style="color: #002200;">:</span> <span style="color: #400080;">NSTextField</span><span style="color: #002200;">!</span></pre>
    <p>
    	对“Hello World!”label正确地重复相同的过程，这次指定这个outlet应当被叫做
        <em>
            welcomeLabel
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121105" src="https://koenig-media.raywenderlich.com/uploads/2015/11/31_welcome_label-480x282.png"
        alt="31_welcome_label" width="480" height="282" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/31_welcome_label-480x282.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/31_welcome_label.png 534w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	现在是时间把你的注意力转到button上了。再一次从storyboard中
        Now time to turn your attention to the button. Once again
        <em>
        	按住Control拖拽
            Control-drag
        </em>
        button到你的
        <code>
            ViewController
        </code>
        类上：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121106" src="https://koenig-media.raywenderlich.com/uploads/2015/11/32_button_action-700x177.png"
        alt="32_button_action" width="700" height="177" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/32_button_action-700x177.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/32_button_action-480x121.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/32_button_action.png 1150w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
    	这次，改变这个连接到
        <em>
            Action
        </em>
        ，并命名为
        <em>
            handleWelcome
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121107" src="https://koenig-media.raywenderlich.com/uploads/2015/11/33_action_settings-480x241.png"
        alt="33_action_settings" width="480" height="241" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/33_action_settings-480x241.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/33_action_settings.png 534w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        点击
        <em>
            Connect
        </em>
        来完成连接，Xcode会添加下列的空方法到
        <code>
            ViewController
        </code>
        上：
    </p>
    <pre class="swift" style="font-family:monospace;">@IBAction <span style="color: #a61390;">func</span> handleWelcome<span style="color: #002200;">(</span>sender<span style="color: #002200;">:</span> <span style="color: #a61390;">AnyObject</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
    <span style="color: #002200;">}</span></pre>
    <p>
    	这个方法会在用户每次点击按钮时被调用。
    </p>
    <p>
    	添加下面这行代码到
        <code>
            handleWelcome(\_:)
        </code>
        方法体中：
    </p>
    <pre class="swift" style="font-family:monospace;">welcomeLabel.stringValue <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"Hello <span style="color: #2400d9;">\(</span>nameTextField.stringValue)!"</span></pre>
    <p>
    	这会更新
    	<code>
            welcomeLabel
        </code>
        的
        <code>
            stringValue
        </code>
        属性，变为一个由nameTextField的stringValue所构成的欢迎的信息。
        <code>
            stringValue
        </code>
        代表了一个基于文本的控件的当前的值 - 由用户输入的或在storyboard上定义的。
    </p>
    <p>
    	这就是你需要的“Hello World”的个人化版本的全部代码！build并执行来尝试一下。当app启动的时候，尝试输入你的名字到
        <em>
            Name
        </em>
        框中并点击
        <em>
            Welcome
        </em>
        按钮。你会看到你的非常个性化版本的“Hello world!”：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121108" src="https://koenig-media.raywenderlich.com/uploads/2015/11/34_hello_sam-700x426.png"
        alt="34_hello_sam" width="700" height="426" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/34_hello_sam-700x426.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/34_hello_sam-480x292.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/34_hello_sam.png 962w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
    	是不是相当酷？好的，乐趣不止于此。下一步你将学习关于添加image到你的app，来创建一个令人惊奇的magic-8 ball工具！
    </p>
    <h2>
        Assets
    </h2>
    <p>
    	你在教程的开头被承诺了一个magic 8-ball的app，但到目前为止你看到都没有提到过一个球。好了，这就是全部将要改变的事。
    </p>
    <p>
    	8-ball是相当与众不同的，如果没有一些可视化的东西，它无法成为一个令人兴奋的8-ball app。
        An 8-ball is pretty distinctive, and it wouldn’t be a very exciting 8-ball
        app without some visualization.
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/8ball-images.zip"
        sl-processed="1">
            Download
            下载
        </a>
        这些你需要的图片，它们会让你的app看起来更漂亮。你会发现在zip文件中有两个图片 - 代表magic 8-ball的两面：
    </p>
    <p>
        <img class="aligncenter size-full wp-image-121109" src="https://koenig-media.raywenderlich.com/uploads/2015/11/35_assets.png"
        alt="35_assets" width="650" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/35_assets.png 650w, https://koenig-media.raywenderlich.com/uploads/2015/11/35_assets-480x236.png 480w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
    	图片资产保存在OS X app中的一个资产目录中。这个目录管理了由app图标和app中的图像所要求的，含有不同分辨率的图像（imagery）。
    </p>
    <p>
    	通过在project navigator中选择
        <em>
            Assets.xcassets
        </em>
        来打开它：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121110" src="https://koenig-media.raywenderlich.com/uploads/2015/11/36_asset_catalog-700x182.png"
        alt="36_asset_catalog" width="700" height="182" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/36_asset_catalog-700x182.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/36_asset_catalog-480x125.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/36_asset_catalog.png 1178w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
    	你可以看到这个目录中当前仅包含了一个项目 - 
        <em>
            AppIcon
        </em>
        。这里就是你可以用艺术品（artwork）来给你的app一个很酷的图标的地方。
    </p>
    <p>
    	你需要将下载到的图片添加到asset目录中。在finder找到图片，并将它们都
        <em>
            拖拽到
        </em>
        asset catalog目录中：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121111" src="https://koenig-media.raywenderlich.com/uploads/2015/11/37_drag_asset_catalog-700x323.png"
        alt="37_drag_asset_catalog" width="700" height="323" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/37_drag_asset_catalog-700x323.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/37_drag_asset_catalog-480x221.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/37_drag_asset_catalog.png 1176w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
    	这将在asset catalog中创建两个记录（entry）：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121112" src="https://koenig-media.raywenderlich.com/uploads/2015/11/38_added_assets-700x372.png"
        alt="38_added_assets" width="700" height="372" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/38_added_assets-700x372.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/38_added_assets-480x255.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/38_added_assets.png 1380w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
    	注意到这里有三个图片的“单元格”（cell）。这些单元格代表了三种不同的屏幕分辨率 - 标准的 (1x), retina (2x) 和 retina-HD (3x)。通常来说，你要为每一个单元格提供资产，但在这个简单的工程中你提供一个就行了。
    </p>
    <p>
    	你刚刚提供的图像实际上被设计为用作retina分辨率的 (2x)，因此将它从左边的单元格拖到中间来：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121113" src="https://koenig-media.raywenderlich.com/uploads/2015/11/39_drag_retina-480x176.png"
        alt="39_drag_retina" width="480" height="176" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/39_drag_retina-480x176.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/39_drag_retina-700x256.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/39_drag_retina.png 839w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	对两个8-balls资产做同样的操作，asset目录现在看起来就像这样了：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121114" src="https://koenig-media.raywenderlich.com/uploads/2015/11/40_finished_asset_catalog-700x434.png"
        alt="40_finished_asset_catalog" width="700" height="434" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/40_finished_asset_catalog-700x434.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/40_finished_asset_catalog-480x298.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/40_finished_asset_catalog.png 1022w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
    	那些图像现在可以被用在你的app中了 - 无论在代码中还是storyboard中。
    </p>
    <h3>
        Displaying Images
        展示图像
    </h3>
    <p>
    	你已经看过怎么在你的app中展示文本，按钮和文本输入框了，但对于图像呢？进入
        <code>
            ImageView
        </code>
        。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        ，并使用object library来搜索
        <em>
            image view
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121115" src="https://koenig-media.raywenderlich.com/uploads/2015/11/41_image_view-340x320.png"
        alt="41_image_view" width="340" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/41_image_view-340x320.png 340w, https://koenig-media.raywenderlich.com/uploads/2015/11/41_image_view.png 518w"
        sizes="(max-width: 340px) 100vw, 340px">
    </p>
    <p>
    	将一个image view拖拽到view controller的画布上，放在stack view的底部。注意一条水平的蓝色的线是怎么出现的，它会指示新的image view会出现在stack view的哪里：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121116" src="https://koenig-media.raywenderlich.com/uploads/2015/11/42_add_to_stack-480x299.png"
        alt="42_add_to_stack" width="480" height="299" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/42_add_to_stack-480x299.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/42_add_to_stack.png 622w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        打开
        <em>
            Attributes Inspector
        </em>
        ，并设置Image属性为
        <em>
            8ball
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter wp-image-121117 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/43_set_8ball-e1448290344741-480x160.png"
        alt="43_set_8ball" width="480" height="160" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/43_set_8ball-e1448290344741-480x160.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/43_set_8ball-e1448290344741.png 513w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	这将使用来自asset目录的图像来更新画布：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121118" src="https://koenig-media.raywenderlich.com/uploads/2015/11/44_vc_with_image-480x310.png"
        alt="44_vc_with_image" width="480" height="310" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/44_vc_with_image-480x310.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/44_vc_with_image-700x453.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/44_vc_with_image.png 990w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	运行app来查看这个图怎么出现：
    </p>
    <p>
        <img class="aligncenter wp-image-121119 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/11/45_bar_03-e1448290439265-700x430.png"
        alt="45_bar_03" width="700" height="430" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/45_bar_03-e1448290439265-700x430.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/45_bar_03-e1448290439265-480x295.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/45_bar_03-e1448290439265.png 961w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
    	好的，这个图出现了，但却被window裁剪掉了一部分。你可以以通常的方式拖拽来改变window的大小，但显然如果当app启动时，window的尺寸就是正确的就更好了，并且要保持一个固定的尺寸。
    </p>
    <h2>
        Window Size
    </h2>
    <p>
    	MagicEight的window的初始尺寸是由storyboard中的view controller的尺寸决定的。在
        <em>
            Main.storyboard
        </em>
        中选择view controller的view，并打开
        <em>
            Size Inspector
        </em>
        。设置Width为
        <em>
            350
        </em>
        ，height为
        <em>
            480
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter wp-image-121120 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/46_vc_size-e1448290482977-421x320.png"
        alt="46_vc_size" width="421" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/46_vc_size-e1448290482977-421x320.png 421w, https://koenig-media.raywenderlich.com/uploads/2015/11/46_vc_size-e1448290482977.png 514w"
        sizes="(max-width: 421px) 100vw, 421px">
    </p>
    <p>
    	注意storyboard的画布现在看起来很奇怪：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121121" src="https://koenig-media.raywenderlich.com/uploads/2015/11/47_stange_vc-220x320.png"
        alt="47_stange_vc" width="220" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/47_stange_vc-220x320.png 220w, https://koenig-media.raywenderlich.com/uploads/2015/11/47_stange_vc-344x500.png 344w, https://koenig-media.raywenderlich.com/uploads/2015/11/47_stange_vc.png 722w"
        sizes="(max-width: 220px) 100vw, 220px">
    </p>
    <p>
    	这是因为布局的约束需要重新被计算。
    </p>
    <p>
        使用在底部的自动布局菜单栏中的
        <em>
            Resolve Auto Layout Issues
        </em>
        菜单，并选择
        <em>
            All View in View Controller
        </em>
        <em>
            \
        </em>
        <em>
            Update Frames
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121122" src="https://koenig-media.raywenderlich.com/uploads/2015/11/48_fix_al-374x320.png"
        alt="48_fix_al" width="374" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/48_fix_al-374x320.png 374w, https://koenig-media.raywenderlich.com/uploads/2015/11/48_fix_al-585x500.png 585w, https://koenig-media.raywenderlich.com/uploads/2015/11/48_fix_al.png 622w"
        sizes="(max-width: 374px) 100vw, 374px">
    </p>
    <p>
    	这会在storyboard中重新运行布局引擎，并更新预览图：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121123" src="https://koenig-media.raywenderlich.com/uploads/2015/11/49_fixed_vc-537x500.png"
        alt="49_fixed_vc" width="537" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/49_fixed_vc-537x500.png 537w, https://koenig-media.raywenderlich.com/uploads/2015/11/49_fixed_vc-343x320.png 343w, https://koenig-media.raywenderlich.com/uploads/2015/11/49_fixed_vc.png 732w"
        sizes="(max-width: 537px) 100vw, 537px">
    </p>
    <p>
    	build并执行来查看app的样子：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121124" src="https://koenig-media.raywenderlich.com/uploads/2015/11/50_bar_04-348x500.png"
        alt="50_bar_04" width="348" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/50_bar_04-348x500.png 348w, https://koenig-media.raywenderlich.com/uploads/2015/11/50_bar_04-223x320.png 223w, https://koenig-media.raywenderlich.com/uploads/2015/11/50_bar_04.png 700w"
        sizes="(max-width: 348px) 100vw, 348px">
    </p>
    <p>
    	看起来好了很多。尝试调整window的大小 - 你会看到你仍然可以手动拖动它到对MagicEight的布局无效的尺寸。
    </p>
    <p>
    	在这儿你有几个选项 - 你可以更新布局，让它在window的尺寸改变时也适应得不错（例如对于小的window调整image的尺寸），或者你可以固定window的尺寸。你将使用第二种较容易的方法。
    </p>
    <h3>
        Window Sizing
       	调整Window的尺寸
    </h3>
    <p>
    	window controller是用来负责管理window的尺寸的。打开
        <em>
            Main.storyboard
        </em>
        ，并选择window controller中的window：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121125" src="https://koenig-media.raywenderlich.com/uploads/2015/11/51_select_window-700x295.png"
        alt="51_select_window" width="700" height="295" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/51_select_window-700x295.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/51_select_window-480x202.png 480w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
    	打开
        <em>
            Size Inspector
        </em>
        ，并设定Content Size的Width为
        <em>
            350
        </em>
        ，height为
        <em>
            480
        </em>
        。然后点击
        <em>
            Minimum Content Size
        </em>
        和
        <em>
            Maximum Content Size
        </em>
        ，确认它们和你刚输入的content size相同：
    </p>
    <p>
        <img class="aligncenter wp-image-121126 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/52_content_size-e1448290524705-410x320.png"
        alt="52_content_size" width="410" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/52_content_size-e1448290524705-410x320.png 410w, https://koenig-media.raywenderlich.com/uploads/2015/11/52_content_size-e1448290524705.png 514w"
        sizes="(max-width: 410px) 100vw, 410px">
    </p>
    <p>
    	再次build和运行MagicEight，并尝试改变window的大小。你已不再能控制window的大小 - 现在它是固定的。的确，这就是你想要的。
    </p>
    <p>
    	现在你可以将你的注意力转回手上的任务了 - build magic 8-ball的“magic”。好的，接近了 - 首先这里有一些布局要做。
    </p>
    <h2>
    	处理点击
    </h2>
    <p>
    	当用户点击8-ball时，你将改变图片到另一面，并展示一条建议。你需要一个新的label来展示这条建议。
    </p>
    <p>
    	打开
        <em>
            Main.storyboard
        </em>
        ，并找到view controller场景。使用
        <em>
            Object Library
        </em>
        去找到一个
        <em>
            wrapping label
        </em>
        ，并将它从library拖拽到stack view的下方：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121127" src="https://koenig-media.raywenderlich.com/uploads/2015/11/53_wrapping_label-700x388.png"
        alt="53_wrapping_label" width="700" height="388" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/53_wrapping_label-700x388.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/53_wrapping_label-480x266.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/53_wrapping_label.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
    	你想要将这个label放置在magic-8图片的中央，因此你需要添加一些自动布局的约束。
    </p>
    <p>    
    	在
    	<em>
            Document Outline
        </em>
    	中，
        <em>
        	按住control拖拽
        </em>
        <em>
            Multiline Label
        </em>
        到
        <em>
            Image View
        </em>
        上
        <em>
            Document Outline
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-full wp-image-121128" src="https://koenig-media.raywenderlich.com/uploads/2015/11/54_adding_constraints.png"
        alt="54_adding_constraints" width="486" height="164" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/54_adding_constraints.png 486w, https://koenig-media.raywenderlich.com/uploads/2015/11/54_adding_constraints-480x162.png 480w"
        sizes="(max-width: 486px) 100vw, 486px">
    </p>
    <p>
    	在点击
  	    <em>
            Add Constraints
        </em>
    	前，按住
        <i>
            shift
        </i>
        并选择
        <em>
            Center Vertically
        </em>
        和
        <em>
            Center Horizontally
        </em>
		：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121129" src="https://koenig-media.raywenderlich.com/uploads/2015/11/55_center_constraints-215x320.png"
        alt="55_center_constraints" width="215" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/55_center_constraints-215x320.png 215w, https://koenig-media.raywenderlich.com/uploads/2015/11/55_center_constraints-335x500.png 335w, https://koenig-media.raywenderlich.com/uploads/2015/11/55_center_constraints.png 373w"
        sizes="(max-width: 215px) 100vw, 215px">
    </p>
    <p>
    	这个label不能自动地重新调整位置 - 但你之前已经处理了。使用底部自动布局工具栏中的
        <em>
            Resolve Auto Layout Issues
        </em>
        菜单，选择
        <em>
            All View in View Controller
        </em>
        <em>
            \
        </em>
        <em>
            Update Frames
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121130" src="https://koenig-media.raywenderlich.com/uploads/2015/11/56_fix_al-374x320.png"
        alt="56_fix_al" width="374" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/56_fix_al-374x320.png 374w, https://koenig-media.raywenderlich.com/uploads/2015/11/56_fix_al-585x500.png 585w, https://koenig-media.raywenderlich.com/uploads/2015/11/56_fix_al.png 622w"
        sizes="(max-width: 374px) 100vw, 374px">
    </p>
    <p>
    	这样就重新调整了label的位置，立即变得明显了，你需要在外表上做一些工作。
    </p>
    <p>
    	选择multiline label，使用
        <em>
            Attributes Inspector
        </em>
        来进行如下的设置：
    </p>
    <ul>
        <li>
            <em>
                Title
            </em>
            ：
            <em>
                Piece of Advice
            </em>
        </li>
        <li>
            <em>
                Alignment
            </em>
            ：
            <em>
                Center
            </em>
        </li>
        <li>
            <em>
                Text Color
            </em>
            ：
            <em>
                Keyboard Focus Indicator
            </em>
        </li>
        <li>
            <em>
                Font
            </em>
            ：
            <em>
                System 20
            </em>
        </li>
    </ul>
    <p>
        <img class="aligncenter size-medium wp-image-121131" src="https://koenig-media.raywenderlich.com/uploads/2015/11/57_label_config-356x320.png"
        alt="57_label_config" width="356" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/57_label_config-356x320.png 356w, https://koenig-media.raywenderlich.com/uploads/2015/11/57_label_config.png 518w"
        sizes="(max-width: 356px) 100vw, 356px">
    </p>
    <p>
    	前往
        <em>
            Size Inspector
        </em>
        ，设置Preferred Width为
        <em>
            Explicit
        </em>
        ，值为
        <em>
            75
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter wp-image-121132 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/58_label_size-e1448290564918-480x184.png"
        alt="58_label_size" width="480" height="184" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/58_label_size-e1448290564918-480x184.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/58_label_size-e1448290564918.png 516w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	为了了解产品最后可能的样子，选择image view，并使用
        <em>
            Attributes Inspector
        </em>
        来设置Image为
        <em>
            magic8ball
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter wp-image-121133 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/59_change_image-e1448290610187-480x147.png"
        alt="59_change_image" width="480" height="147" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/59_change_image-e1448290610187-480x147.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/59_change_image-e1448290610187.png 516w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	再一次的，点击主view，并使用
        <em>
            Resolve Auto Layout Issues\All Views in View Controller\Update Frames
        </em>
        去更新布局：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121134" src="https://koenig-media.raywenderlich.com/uploads/2015/11/60_magic8_layout-337x320.png"
        alt="60_magic8_layout" width="337" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/60_magic8_layout-337x320.png 337w, https://koenig-media.raywenderlich.com/uploads/2015/11/60_magic8_layout-526x500.png 526w, https://koenig-media.raywenderlich.com/uploads/2015/11/60_magic8_layout.png 718w"
        sizes="(max-width: 337px) 100vw, 337px">
    </p>
    <p>
    	这看起来相当好。当每次用户点击8-ball时，你需要响应去发现手势识别。
    </p>
    <h3>
        Gesture Recognizer
    </h3>
    <p>
    	你可以在代码中创造一个动作，在每次用户点击button时执行。这是可以的，因为button被设计来处理点击 - 但是相同的事对于image view来说却是不成立的。
    </p>
    <p>
    	苹果提供了一组gesture recognizer，可以被添加到任何view上。这些recognizer将低级的鼠标和触控板的输入转化成语义化的事件 - 例如点击，缩放和旋转。
    </p>
    <p>
    	你将添加一个gesture recognizer到image view上，然后在view controller的代码中创建相应的动作。
    </p>
    <p>
    	在
        <em>
            Main.storyboard
        </em>
        中，前往
        <em>
            Object Library
        </em>
        并搜索
        <em>
            click gesture
        </em>
        。将
        <em>
            Click Gesture Recognizer
        </em>
        从library拖拽到image view上。它将像这样的出现在document outline中：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121135" src="https://koenig-media.raywenderlich.com/uploads/2015/11/61_gesture_recogniser-480x119.png"
        alt="61_gesture_recogniser" width="480" height="119" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/61_gesture_recogniser-480x119.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/61_gesture_recogniser.png 484w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	无论何时用户点击图片，这个gesture recognizer都会被激活 - 恰好是你想要的。现在你需要添加一些新的连接，然后你将为最后的冲刺，准备好切换到代码。
    </p>
    <h3>
        IB Connections
    </h3>
    <p>
    	用你之前的相同的方式，打开assistant editor，并确保它正在展示
        <em>
            ViewController.swift
        </em>
        。然后通过从storyboard
        <em>
        	按住control拖拽
        </em>
        到代码中：一个是从image view（叫做
        <em>
            ballImageView
        </em>
        ），另一个是从multiline label（交错
        <em>
            adviceLabel
        </em>
        ）。这添加了下列的outlets：
    </p>
    <pre class="swift" style="font-family:monospace;">
    @IBOutlet weak <span style="color: #a61390;">var</span> ballImageView<span style="color: #002200;">:</span> <span style="color: #400080;">NSImageView</span><span style="color: #002200;">!</span>
    @IBOutlet weak <span style="color: #a61390;">var</span> adviceLabel<span style="color: #002200;">:</span> <span style="color: #400080;">NSTextField</span><span style="color: #002200;">!</span></pre>
    <p>
    	你也需要一个action来接通新创建的gesture recognizer。从document outline中的click gesture recognizer，
        <em>
        	按住Control拖拽
        </em>
        到代码中：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121136" src="https://koenig-media.raywenderlich.com/uploads/2015/11/62_gesture_action-700x158.png"
        alt="62_gesture_action" width="700" height="158" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/62_gesture_action-700x158.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/62_gesture_action-480x108.png 480w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
    	改变Connection为
        <em>
            Action
        </em>
        ，并命名为
        <em>
            handleBallClick
        </em>
        ：
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121137" src="https://koenig-media.raywenderlich.com/uploads/2015/11/63_action_config-480x220.png"
        alt="63_action_config" width="480" height="220" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/63_action_config-480x220.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/63_action_config.png 568w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
    	点击
        <em>
            Connect
        </em>
        ，Xcode将添加下列的函数定义到
        <code>
            ViewController
        </code>
        类中：
    </p>
    <pre class="swift" style="font-family:monospace;">@IBAction <span style="color: #a61390;">func</span> handleBallClick<span style="color: #002200;">(</span>sender<span style="color: #002200;">:</span> <span style="color: #a61390;">AnyObject</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
<span style="color: #002200;">}</span></pre>
    <p>
    	现在你完成了所有在Interface Builder中的工作，你可以切回到标注编辑器中了，打开
        <em>
            ViewController.swift
        </em>
        。
    </p>
    <h2>
        在代码中操作UI
    </h2>
    <p>
    	当用户点击8-ball时，你想在展示建议或展示“8”。这意味着
        <code>
            handleBallClick(\_:)
        </code>
        会同时操作image view和建议label。
    </p>
    <p>
    	添加下列的代码到
        <code>
            handleBallClick(\_:)
        </code>
        中：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #11740a; font-style: italic;">// 1:</span>
<span style="color: #a61390;">if </span><span style="color: #002200;">(</span>adviceLabel.hidden<span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
  <span style="color: #11740a; font-style: italic;">// 2:</span>
  adviceLabel.hidden <span style="color: #002200;">=</span> <span style="color: #a61390;">false</span>
  ballImageView.image <span style="color: #002200;">=</span> <span style="color: #400080;">NSImage</span><span style="color: #002200;">(</span>named<span style="color: #002200;">:</span> <span style="color: #bf1d1a;">"magic8ball"</span><span style="color: #002200;">)</span>
<span style="color: #002200;">}</span> <span style="color: #a61390;">else</span> <span style="color: #002200;">{</span>
  <span style="color: #11740a; font-style: italic;">// 3:</span>
  adviceLabel.hidden <span style="color: #002200;">=</span> <span style="color: #a61390;">true</span>
  ballImageView.image <span style="color: #002200;">=</span> <span style="color: #400080;">NSImage</span><span style="color: #002200;">(</span>named<span style="color: #002200;">:</span> <span style="color: #bf1d1a;">"8ball"</span><span style="color: #002200;">)</span>
<span style="color: #002200;">}</span></pre>
    <ol start="1">
        <li>
        	检查当前
            <code>
                adviceLabel
            </code>
            是否可见。
            <code>
                hidden
            </code>
            是一个在
            <code>
                NSView
            </code>
            上的布尔类型的属性（因此
            <code>
                NSTextField
            </code>
            也就有了），允许你指定是否要让view隐藏。
        </li>
        <li>
        	如果建议label当前被隐藏了，显示它，并改变图片为magic这边。
            <code>
                NSImage(named:)
            </code>
            会从asset目录中加载图片，而
            <code>
                NSImageView
            </code>
            的
            <code>
                image
            </code>
            属性指定了要展示的图片。
        </li>
        <li>
        	反过来，如果当前建议label是可见的，隐藏它，并将其切换到“8”这边。
        </li>
    </ol>
    <p>
    	build并执行，点击那个球来查看它的“8”和一条建议之间的切换。相当好对么？注意怎么当你第一次启动app时，建议已经显示了？这确实不是你想要的，但要修复它很简单。
    </p>
    <h2>
    	初始设置
    </h2>
    <p>
    	当app第一次启动时，你想确保那个建议label是隐藏的，8-ball则是显示的。View controller有一个完美的方法来配置这个初始化的设置 - 以
        <code>
            viewDidLoad()
        </code>
        的形式。
    </p>
    <p>
    	一旦view controller完成了从storyboard中加载所有的view组件，它就会调用
        <code>
            viewDidLoad()
        </code>
        ；来给你一个机会执行最终的配置。
    </p>
    <p>
        在
        <em>
            ViewController.swift
        </em>
        中，找到
        <code>
            viewDidLoad()
        </code>
        方法并添加下列的内容：
    </p>
    <pre class="swift" style="font-family:monospace;">adviceLabel.hidden <span style="color: #002200;">=</span> <span style="color: #a61390;">true</span>ballImageView.image <span style="color: #002200;">=</span> <span style="color: #400080;">NSImage</span><span style="color: #002200;">(</span>named<span style="color: #002200;">:</span> <span style="color: #bf1d1a;">"8ball"</span><span style="color: #002200;">)</span></pre>
    <p>
    	你将从点击事件的处理动作中区别出这个代码 - 它仅是隐藏了建议label，并设置image为
        <em>
            8ball
        </em>
        。
    </p>
    <p>
    	运行项目，来检查你在开始时不会看到建议。
    </p>
    <h2>
    	建议生成器
    </h2>
    <p>
    	此刻，无论你“摇动”那个球多少次，它总是给你相同的建议。这不是特别有帮助的。是时候添加一些随机性了。
    </p>
    <p>
    	在
    	<code>
            ViewController
        </code>
        中添加下列的代码作为属性 - 就在类定义的下面：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">let</span> adviceList <span style="color: #002200;">=</span> <span style="color: #002200;">[</span>
    <span style="color: #bf1d1a;">"Yes"</span>,
    <span style="color: #bf1d1a;">"No"</span>,
    <span style="color: #bf1d1a;">"Ray says 'do it!'"</span>,
    <span style="color: #bf1d1a;">"Maybe"</span>,
    <span style="color: #bf1d1a;">"Try again later"</span>,
    <span style="color: #bf1d1a;">"How can I know?"</span>,
    <span style="color: #bf1d1a;">"Totally"</span>,
    <span style="color: #bf1d1a;">"Never"</span>,
<span style="color: #002200;">]</span></pre>
    <p>
    	这是一个字符串的数组，由全部不同的那个球可以分发的建议构成。
    </p>
    <p>
    	找到文件的最底部（不在）
        <code>
            ViewController
        </code>
        类中），添加下列的extension:
    </p>
    <pre class="swift" style="font-family:monospace;">extension <span style="color: #a61390;">Array</span> <span style="color: #002200;">{</span>
  <span style="color: #a61390;">var</span> randomElement<span style="color: #002200;">:</span> Element? <span style="color: #002200;">{</span>
    <span style="color: #a61390;">if</span> <span style="color: #a61390;">count</span> &lt; <span style="color: #2400d9;">1</span> <span style="color: #002200;">{</span> <span style="color: #a61390;">return</span> .None <span style="color: #002200;">}</span>
    <span style="color: #a61390;">let</span> randomIndex <span style="color: #002200;">=</span> arc4random_uniform<span style="color: #002200;">(</span>UInt32<span style="color: #002200;">(</span><span style="color: #a61390;">count</span><span style="color: #002200;">)</span><span style="color: #002200;">)</span>
    <span style="color: #a61390;">return</span> <span style="color: #a61390;">self</span><span style="color: #002200;">[</span><span style="color: #a61390;">Int</span><span style="color: #002200;">(</span>randomIndex<span style="color: #002200;">)</span><span style="color: #002200;">]</span>
  <span style="color: #002200;">}</span>
<span style="color: #002200;">}</span></pre>
    <p>
    	这添加了一个新的property到标注库的
        <code>
            Array
        </code>
        类型，它会返回一个随机的严肃。如果Array是空的，它就返回
        <code>
            nil
        </code>
        ，否则它会在返回相应的元素前，使用
        <code>
            arc4random_uniform()
        </code>
        产生一个随机的序号。
    </p>
    <p>
    	在
        <code>
            handleBallClick(\_:)
        </code>
        中，更新
    	<code>
            if
        </code>
        语句的第一个分支（也就是说
        <code>
            adviceLabel.hidden == true
        </code>
        ）为如下：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> advice <span style="color: #002200;">=</span> adviceList.randomElement <span style="color: #002200;">{</span>
    adviceLabel.stringValue <span style="color: #002200;">=</span> advice
    adviceLabel.hidden <span style="color: #002200;">=</span> <span style="color: #a61390;">false</span>
    ballImageView.image <span style="color: #002200;">=</span> <span style="color: #400080;">NSImage</span><span style="color: #002200;">(</span>named<span style="color: #002200;">:</span> <span style="color: #bf1d1a;">"magic8ball"</span><span style="color: #002200;">)</span>
<span style="color: #002200;">}</span></pre>
    <p>
    	这会尝试获取一条随机的建议来展示，如果成功的话就会更新
    	<code>
            adviceLabel
        </code>
        的
        <code>
            stringValue
        </code>
        来展示。
    </p>
    <p>
    	build并执行，点击8-ball几次开始从这个球的智慧中受益：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121138" src="https://koenig-media.raywenderlich.com/uploads/2015/11/64_final_bar-700x334.png"
        alt="64_final_bar" width="700" height="334" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/64_final_bar.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/64_final_bar-480x229.png 480w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        从这儿去向哪里
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
        你可以下载完整版本的MagicEight在
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/MagicEight.zip"
        sl-processed="1">
            这里
        </a>
        。
    </p>
    <p>
        这个Mac OS X的开发教程引导系列已经给了你一个开始OS X app的基层的知识 - 但是这里有太多的东西要学！
    </p>
    <p>
        苹果有一些很棒的文档，覆盖了OS X开发的全部方面 - 请前往
        <a href="https://developer.apple.com/library/mac/navigation/" sl-processed="1">
            https://developer.apple.com/library/mac/navigation/
        </a>
    </p>
</div>
