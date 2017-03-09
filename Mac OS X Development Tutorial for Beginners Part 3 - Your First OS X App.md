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
        Build并运行
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
    </h3>
    <p>
        You placed the label on the view controller’s canvas, but you haven’t
        actually told OS X
        <i>
            how
        </i>
        it should position it. The view controller appears at one size in the
        storyboard, but once it’s running in the app, the user can change the window
        size–so you need to specify how the label should be positioned for
        <i>
            any
        </i>
        window size.
    </p>
    <p>
        This sounds like it might be a really difficult task, but luckily Apple
        has your back. OS X uses a powerful layout engine called Auto Layout, in
        which the relationships between different components of the view are expressed
        as constraints. These constraints&nbsp;are then interpreted at runtime
        to calculate the size and position of each element within the view.
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        Auto Layout is a complex topic, and this introductory tutorial won’t cover
        it in any great depth. If you’d like to read more on the topic then there
        are some excellent
        <a href="http://www.raywenderlich.com/115440/auto-layout-tutorial-in-ios-9-part-1-getting-started-2"
        sl-processed="1">
            tutorials
        </a>
        on the site targeted to Auto Layout on iOS—luckily the engine is almost
        identical on the two platforms.
    </div>
    <p>
        Ensure that the label is selected in the view controller, and then click
        the
        <em>
            Align
        </em>
        button in the lower toolbar. Select
        <em>
            Horizontally in Container
        </em>
        , ensuring the value is set to
        <em>
            0
        </em>
        before clicking
        <em>
            Add 1 Constraint
        </em>
        to add the constraint:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121085" src="https://koenig-media.raywenderlich.com/uploads/2015/11/11_align-300x320.png"
        alt="11_align" width="300" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/11_align-300x320.png 300w, https://koenig-media.raywenderlich.com/uploads/2015/11/11_align-468x500.png 468w, https://koenig-media.raywenderlich.com/uploads/2015/11/11_align.png 624w"
        sizes="(max-width: 300px) 100vw, 300px">
    </p>
    <p>
        This will ensure that the label will always appear in the center of the
        window, irrespective of its width. You’ll notice that some angry red lines
        have appeared in the storyboard:
    </p>
    <p>
        <img class="aligncenter size-thumbnail wp-image-121086" src="https://koenig-media.raywenderlich.com/uploads/2015/11/12_angry_red-250x250.png"
        alt="12_angry_red" width="250" height="250" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/12_angry_red-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2015/11/12_angry_red-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/11/12_angry_red-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2015/11/12_angry_red-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2015/11/12_angry_red-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
        This is because you’ve provided a constraint that&nbsp;specifies the location
        of the label in the horizontal direction, but you’ve not provided any information
        about the vertical axis yet.
    </p>
    <p>
        Once again, ensure that the label is selected in the view controller,
        and this time click the
        <em>
            Pin
        </em>
        menu on the Auto Layout toolbar at the bottom. Enter
        <em>
            30
        </em>
        in the top constraint box and ensure that the I-bar beneath it is solid
        red. Set the value of Update Frames to
        <em>
            Items of New Constraints
        </em>
        before clicking
        <em>
            Add 1 Constraint
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121087" src="https://koenig-media.raywenderlich.com/uploads/2015/11/13_pin-227x320.png"
        alt="13_pin" width="227" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/13_pin-227x320.png 227w, https://koenig-media.raywenderlich.com/uploads/2015/11/13_pin-355x500.png 355w, https://koenig-media.raywenderlich.com/uploads/2015/11/13_pin.png 552w"
        sizes="(max-width: 227px) 100vw, 227px">
    </p>
    <p>
        Immediately you’ll notice the view controller update—you can now see the
        entire label, and the angry red lines have changed to calming blue:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121088" src="https://koenig-media.raywenderlich.com/uploads/2015/11/14_happy_storyboard-480x138.png"
        alt="14_happy_storyboard" width="480" height="138" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/14_happy_storyboard-480x138.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/14_happy_storyboard-700x202.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/14_happy_storyboard.png 986w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        And that’s your “Hello World” app done (for now). Use the “play” button
        to build and run, and inspect your handiwork:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121089" src="https://koenig-media.raywenderlich.com/uploads/2015/11/15_bar_02-480x293.png"
        alt="15_bar_02" width="480" height="293" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/15_bar_02-480x293.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/15_bar_02-700x427.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/15_bar_02.png 962w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        Congratulations! Not very personal though is it? In the next section you’ll
        discover how to make the traditional greeting a little more friendly.
    </p>
    <h2>
        Handling User Input
    </h2>
    <p>
        In this section you’re going to add a text field to allow the user to
        enter their name so that you can welcome them personally.
    </p>
    <h3>
        Control Layout
    </h3>
    <p>
        As you did before, use the object library to locate and then drag a
        <em>
            Text Field
        </em>
        and a
        <em>
            Push Button
        </em>
        onto the view controller. Position them above the “Hello World!” label:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121090" src="https://koenig-media.raywenderlich.com/uploads/2015/11/16_position_textfield-480x115.png"
        alt="16_position_textfield" width="480" height="115" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/16_position_textfield-480x115.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/16_position_textfield-700x168.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/16_position_textfield.png 986w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        Remember that placing the controls on the canvas isn’t enough for OS X
        to understand how you want them positioned as the window changes size.
        You need to add some constraints to convey your wishes.
    </p>
    <p>
        Select the text field, and then
        <em>
            Command-Click
        </em>
        the button to select both simultaneously. Click the
        <em>
            Stack
        </em>
        icon on the Auto Layout toolbar at the bottom of the storyboard:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121091" src="https://koenig-media.raywenderlich.com/uploads/2015/11/17_stack-480x265.png"
        alt="17_stack" width="480" height="265" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/17_stack-480x265.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/17_stack.png 604w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        This has created a new stack view containing the text field and the button.
        A stack view automatically generates the layout constraints required to
        position the contained views in a line. You can use the attributes inspector
        to configure many common properties of the stack view.
    </p>
    <div class="note">
        <em>
            NOTE:
        </em>
        <code>
            NSStackView
        </code>
        has been in OS X since 10.9, but received a significant update in 10.11
        (El Capitan)—in line with its introduction (
        <code>
            UIStackView
        </code>
        ) in iOS. Stack views are similar on both platforms, so you can check
        out the iOS
        <a href="http://www.raywenderlich.com/114552/uistackview-tutorial-introducing-stack-views"
        sl-processed="1">
            tutorial on stack views
        </a>
        to get up to speed. Or hang tight—there’s a tutorial on
        <code>
            NSStackView
        </code>
        &nbsp;dropping in the next few weeks.
    </div>
    <p>
        Once you’ve started stacking it’s difficult to stop. This time, you’re
        going to stack your newly created stack view with the “Hello World!” label—in
        a vertical stack view.
    </p>
    <p>
        Use the button to the left of the lower toolbar to show the Document Outline
        and then locate the “Hello World” control and the existing stack view.
        <i>
            Command-click
        </i>
        them to select both:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121092" src="https://koenig-media.raywenderlich.com/uploads/2015/11/18_document_outline-469x320.png"
        alt="18_document_outline" width="469" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/18_document_outline-469x320.png 469w, https://koenig-media.raywenderlich.com/uploads/2015/11/18_document_outline.png 674w"
        sizes="(max-width: 469px) 100vw, 469px">
    </p>
    <p>
        As you did before, use the
        <em>
            Stack
        </em>
        button on the bottom toolbar to create a new stack view:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121093" src="https://koenig-media.raywenderlich.com/uploads/2015/11/19_stack-480x195.png"
        alt="19_stack" width="480" height="195" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/19_stack-480x195.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/19_stack-700x285.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/19_stack.png 1002w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        While this new stack view is selected, open the
        <em>
            Attributes Inspector
        </em>
        and set the Alignment to
        <em>
            Center X
        </em>
        , and the spacing to
        <em>
            20
        </em>
        :
    </p>
    <p>
        <img class="aligncenter wp-image-121094 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/20_stack_config-e1448290245207-480x306.png"
        alt="20_stack_config" width="480" height="306" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/20_stack_config-e1448290245207-480x306.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/20_stack_config-e1448290245207.png 515w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        This ensures that the label and the upper stack view are nicely centered
        and there’s a gap of 20 points between them.
    </p>
    <p>
        A couple more bits of layout to complete before you can turn your attention
        to the task of handling user input.
    </p>
    <p>
        The stack view handles the positioning of its content relative to each
        other, but it needs to be positioned within the view controller’s view.
        Select the outer stack view and use the
        <em>
            Align
        </em>
        auto layout menu to center it horizontally&nbsp;within its container:
    </p>
    <p>
        <img class="aligncenter wp-image-121095 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/21_align-300x320.png"
        alt="21_align" width="300" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/21_align-300x320.png 300w, https://koenig-media.raywenderlich.com/uploads/2015/11/21_align-468x500.png 468w, https://koenig-media.raywenderlich.com/uploads/2015/11/21_align.png 624w"
        sizes="(max-width: 300px) 100vw, 300px">
    </p>
    <p>
        And use the
        <em>
            Pin
        </em>
        menu to pin the stack view to the top, with a spacing of
        <em>
            30
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121096" src="https://koenig-media.raywenderlich.com/uploads/2015/11/22_pin-227x320.png"
        alt="22_pin" width="227" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/22_pin-227x320.png 227w, https://koenig-media.raywenderlich.com/uploads/2015/11/22_pin-355x500.png 355w, https://koenig-media.raywenderlich.com/uploads/2015/11/22_pin.png 552w"
        sizes="(max-width: 227px) 100vw, 227px">
    </p>
    <p>
        Finally, to ensure that the text field always has the space for the user’s
        name, you will fix its width.
    </p>
    <p>
        Select the text field and use the
        <em>
            Pin
        </em>
        menu in the bottom toolbar to specify a
        <em>
            Width
        </em>
        of
        <em>
            100
        </em>
        . Click
        <em>
            Add 1 Constraint
        </em>
        to save the new constraint:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121097" src="https://koenig-media.raywenderlich.com/uploads/2015/11/23_textfield_width-480x311.png"
        alt="23_textfield_width" width="480" height="311" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/23_textfield_width-480x311.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/23_textfield_width-700x453.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/23_textfield_width.png 918w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        With that your layout is pretty much complete—it should look like the
        following:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121098" src="https://koenig-media.raywenderlich.com/uploads/2015/11/24_layout-480x176.png"
        alt="24_layout" width="480" height="176" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/24_layout-480x176.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/24_layout-700x256.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/24_layout.png 990w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        Now you can turn your attention back to those new controls you added.
    </p>
    <h3>
        Outlets and Actions
    </h3>
    <p>
        Select the text field and open the
        <em>
            Attributes Inspector
        </em>
        . In the Placeholder field type
        <em>
            Name
        </em>
        :
    </p>
    <p>
        <img class="aligncenter wp-image-121099 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/25_name-e1448290291815-480x249.png"
        alt="25_name" width="480" height="249" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/25_name-e1448290291815-480x249.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/25_name-e1448290291815.png 513w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        This grayed out text will instruct the user what the field is for, and
        disappears as soon as they start typing.
    </p>
    <p>
        Select the button, and again open the
        <em>
            Attributes Inspector
        </em>
        . Set the Title to
        <em>
            Welcome
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121100" src="https://koenig-media.raywenderlich.com/uploads/2015/11/26_welcome-362x320.png"
        alt="26_welcome" width="362" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/26_welcome-362x320.png 362w, https://koenig-media.raywenderlich.com/uploads/2015/11/26_welcome.png 518w"
        sizes="(max-width: 362px) 100vw, 362px">
    </p>
    <p>
        That’s the cosmetic aspect done. Time to wire these two controls into
        code.
    </p>
    <p>
        OS X provides a way to interact with the storyboard UI from code using
        outlets and actions:
    </p>
    <ul>
        <li>
            <em>
                An outlet
            </em>
            is a property in code that is connected to a component in the storyboard.
            This allows you to access the properties of controls within a storyboard
            from your code.
        </li>
        <li>
            <em>
                An action
            </em>
            is a method on a class&nbsp;in code that is invoked when the user interacts
            with the components in the UI – e.g. by clicking on a button.
        </li>
    </ul>
    <p>
        You are going to add outlets for the text field and the label, and an
        action that will be called when the user clicks the welcome button.
    </p>
    <p>
        The view controller you’ve been working on already has a skeleton class
        associated with it in code—in
        <em>
            ViewController.swift
        </em>
        . This is where you’ll add the outlets and action.
    </p>
    <p>
        Open the assistant editor using the button in the toolbar:
    </p>
    <p>
        <img class="aligncenter size-full wp-image-121101" src="https://koenig-media.raywenderlich.com/uploads/2015/11/27_assistant_editor.png"
        alt="27_assistant_editor" width="210" height="64">
    </p>
    <p>
        This will split the screen and show a code file alongside the storyboard.
        It should be displaying
        <em>
            ViewController.swift
        </em>
        , but if it isn’t use the jump bar to select
        <em>
            Automatic
        </em>
        <em>
            \
        </em>
        <em>
            ViewController.swift
        </em>
        :
    </p>
    <p>
        <img class="aligncenter wp-image-121102 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/28_jump_bar-480x52.png"
        alt="28_jump_bar" width="480" height="52" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/28_jump_bar-480x52.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/28_jump_bar.png 596w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        <em>
            Right-click-drag
        </em>
        (or
        <em>
            control-drag
        </em>
        ) from the text field in the storyboard over to the line above
        <code>
            override func viewDidLoad()
        </code>
        in
        <em>
            ViewController.swift
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121103" src="https://koenig-media.raywenderlich.com/uploads/2015/11/29_textfield_outlet-700x289.png"
        alt="29_textfield_outlet" width="700" height="289" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/29_textfield_outlet-700x289.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/29_textfield_outlet-480x199.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/29_textfield_outlet.png 1417w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Ensure that
        <em>
            Outlet
        </em>
        is selected and call the new outlet
        <em>
            nameTextField
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121104" src="https://koenig-media.raywenderlich.com/uploads/2015/11/30_name_textfield-480x276.png"
        alt="30_name_textfield" width="480" height="276" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/30_name_textfield-480x276.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/30_name_textfield.png 530w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        This will add the following property to&nbsp;
        <code>
            ViewController
        </code>
        &nbsp;and updates the storyboard to automatically connect the text field
        when loading the view controller:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1102691">
                    <td class="code" id="p110269code1">
                        <pre class="swift" style="font-family:monospace;">
                            @IBOutlet weak
                            <span style="color: #a61390;">
                                var
                            </span>
                            nameTextField
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #400080;">
                                NSTextField
                            </span>
                            <span style="color: #002200;">
                                !
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Repeat exactly the same process for the “Hello World!” label, this time
        specifying that the outlet should be called
        <em>
            welcomeLabel
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121105" src="https://koenig-media.raywenderlich.com/uploads/2015/11/31_welcome_label-480x282.png"
        alt="31_welcome_label" width="480" height="282" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/31_welcome_label-480x282.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/31_welcome_label.png 534w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        Now time to turn your attention to the button. Once again
        <em>
            Control-drag
        </em>
        from the button in the storyboard over to the
        <code>
            ViewController
        </code>
        class:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121106" src="https://koenig-media.raywenderlich.com/uploads/2015/11/32_button_action-700x177.png"
        alt="32_button_action" width="700" height="177" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/32_button_action-700x177.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/32_button_action-480x121.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/32_button_action.png 1150w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        This time, change the Connection to
        <em>
            Action
        </em>
        and name it
        <em>
            handleWelcome
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121107" src="https://koenig-media.raywenderlich.com/uploads/2015/11/33_action_settings-480x241.png"
        alt="33_action_settings" width="480" height="241" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/33_action_settings-480x241.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/33_action_settings.png 534w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        Click
        <em>
            Connect
        </em>
        to make the connection and Xcode will add the following empty method to&nbsp;
        <code>
            ViewController
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1102692">
                    <td class="code" id="p110269code2">
                        <pre class="swift" style="font-family:monospace;">
                            @IBAction
                            <span style="color: #a61390;">
                                func
                            </span>
                            handleWelcome
                            <span style="color: #002200;">
                                (
                            </span>
                            sender
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #a61390;">
                                AnyObject
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                {
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
        This method will be called every time the user clicks the button.
    </p>
    <p>
        Add the following line to the
        <code>
            handleWelcome(_:)
        </code>
        method body:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1102693">
                    <td class="code" id="p110269code3">
                        <pre class="swift" style="font-family:monospace;">
                            welcomeLabel.stringValue
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #bf1d1a;">
                                "Hello
                                <span style="color: #2400d9;">
                                    \(
                                </span>
                                nameTextField.stringValue)!"
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This updates the
        <code>
            stringValue
        </code>
        property of the
        <code>
            welcomeLabel
        </code>
        to a welcome message constructed using the
        <code>
            stringValue
        </code>
        of the
        <code>
            nameTextField
        </code>
        .
        <code>
            stringValue
        </code>
        represents the value currently displayed by a text-based control—be it
        user-entered or defined in the storyboard.
    </p>
    <p>
        That’s all the code you need to get your personalized version of “Hello
        World” going! Build and run to give it a try. Once the app has started,
        try entering your name in the
        <em>
            Name
        </em>
        box and clicking the
        <em>
            Welcome
        </em>
        button. You’ll see your very own version of “Hello world!”:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121108" src="https://koenig-media.raywenderlich.com/uploads/2015/11/34_hello_sam-700x426.png"
        alt="34_hello_sam" width="700" height="426" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/34_hello_sam-700x426.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/34_hello_sam-480x292.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/34_hello_sam.png 962w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Pretty cool eh? Well, the fun doesn’t stop there. Next up you’re going
        to learn about adding images to your app, to create an amazing magic-8
        ball utility!
    </p>
    <h2>
        Assets
    </h2>
    <p>
        You were promised a magic 8-ball app at the start of this tutorial, and
        so far you’ve seen no mention of a ball. Well, that’s all about to change.
    </p>
    <p>
        An 8-ball is pretty distinctive, and it wouldn’t be a very exciting 8-ball
        app without some visualization.
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/8ball-images.zip"
        sl-processed="1">
            Download
        </a>
        &nbsp;the images you’ll need to make your app look swish. You’ll find
        two images inside the zip file—representing the two sides of a magic 8-ball:
    </p>
    <p>
        <img class="aligncenter size-full wp-image-121109" src="https://koenig-media.raywenderlich.com/uploads/2015/11/35_assets.png"
        alt="35_assets" width="650" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/35_assets.png 650w, https://koenig-media.raywenderlich.com/uploads/2015/11/35_assets-480x236.png 480w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        Image assets are stored in an asset catalog within an OS X app. This catalog
        manages the different imagery and the different resolutions required for
        the app icons and the in-app images.
    </p>
    <p>
        Open
        <em>
            Assets.xcassets
        </em>
        by selecting it in the project navigator:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121110" src="https://koenig-media.raywenderlich.com/uploads/2015/11/36_asset_catalog-700x182.png"
        alt="36_asset_catalog" width="700" height="182" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/36_asset_catalog-700x182.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/36_asset_catalog-480x125.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/36_asset_catalog.png 1178w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        You can see that the catalog currently only contains one item –
        <em>
            AppIcon
        </em>
        . This is where you would put the artwork to give your app a cool icon.
    </p>
    <p>
        You need to add the downloaded images to the asset catalog. Locate the
        images in finder, and
        <em>
            drag
        </em>
        them both into the asset catalog:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121111" src="https://koenig-media.raywenderlich.com/uploads/2015/11/37_drag_asset_catalog-700x323.png"
        alt="37_drag_asset_catalog" width="700" height="323" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/37_drag_asset_catalog-700x323.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/37_drag_asset_catalog-480x221.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/37_drag_asset_catalog.png 1176w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        This will create two new entries in the asset catalog:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121112" src="https://koenig-media.raywenderlich.com/uploads/2015/11/38_added_assets-700x372.png"
        alt="38_added_assets" width="700" height="372" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/38_added_assets-700x372.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/38_added_assets-480x255.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/38_added_assets.png 1380w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Notice that there are three “cells” for the images. These cells represent
        the different screen scales–standard (1x), retina (2x) and retina-HD (3x).
        Normally you would provide assets for each of these cells, but in this
        simple project you will provide just one.
    </p>
    <p>
        The image you’ve been provided is actually designed to be used at retina
        resolutions (2x), so drag the image from the left-hand cell to the central
        (2x) cell:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121113" src="https://koenig-media.raywenderlich.com/uploads/2015/11/39_drag_retina-480x176.png"
        alt="39_drag_retina" width="480" height="176" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/39_drag_retina-480x176.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/39_drag_retina-700x256.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/39_drag_retina.png 839w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        Repeat for both of the 8-balls assets, so that the asset catalog looks
        like this:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121114" src="https://koenig-media.raywenderlich.com/uploads/2015/11/40_finished_asset_catalog-700x434.png"
        alt="40_finished_asset_catalog" width="700" height="434" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/40_finished_asset_catalog-700x434.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/40_finished_asset_catalog-480x298.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/40_finished_asset_catalog.png 1022w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Those images are now available to use in your app—both from code and inside
        the storyboard.
    </p>
    <h3>
        Displaying Images
    </h3>
    <p>
        You’ve already seen how to display text, buttons and text input fields
        in your app, but how about images? Enter
        <code>
            ImageView
        </code>
        .
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and use the object library to search for
        <em>
            image view
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121115" src="https://koenig-media.raywenderlich.com/uploads/2015/11/41_image_view-340x320.png"
        alt="41_image_view" width="340" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/41_image_view-340x320.png 340w, https://koenig-media.raywenderlich.com/uploads/2015/11/41_image_view.png 518w"
        sizes="(max-width: 340px) 100vw, 340px">
    </p>
    <p>
        Drag an image view onto the view controller canvas, at the bottom of the
        stack view. Notice how a horizontal blue line will appear denoting where
        in the stack view that the new image view will appear:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121116" src="https://koenig-media.raywenderlich.com/uploads/2015/11/42_add_to_stack-480x299.png"
        alt="42_add_to_stack" width="480" height="299" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/42_add_to_stack-480x299.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/42_add_to_stack.png 622w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        Open the
        <em>
            Attributes Inspector
        </em>
        and set the Image property to
        <em>
            8ball
        </em>
        :
    </p>
    <p>
        <img class="aligncenter wp-image-121117 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/43_set_8ball-e1448290344741-480x160.png"
        alt="43_set_8ball" width="480" height="160" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/43_set_8ball-e1448290344741-480x160.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/43_set_8ball-e1448290344741.png 513w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        This will update the canvas with the image, read from the asset catalog:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121118" src="https://koenig-media.raywenderlich.com/uploads/2015/11/44_vc_with_image-480x310.png"
        alt="44_vc_with_image" width="480" height="310" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/44_vc_with_image-480x310.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/44_vc_with_image-700x453.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/44_vc_with_image.png 990w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        Build and run the app to see how the image appears:
    </p>
    <p>
        <img class="aligncenter wp-image-121119 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/11/45_bar_03-e1448290439265-700x430.png"
        alt="45_bar_03" width="700" height="430" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/45_bar_03-e1448290439265-700x430.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/45_bar_03-e1448290439265-480x295.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/45_bar_03-e1448290439265.png 961w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Well, the image has appeared, but is clipped by the window. You can drag
        to resize the window in the usual way, but it would be much better if the
        window was correctly sized when the app starts, and then keeps a fixed
        size.
    </p>
    <h2>
        Window Size
    </h2>
    <p>
        The initial size of MagicEight’s window is determined by the size of the
        view controller in the storyboard. Select the view controller’s view in
        <em>
            Main.storyboard
        </em>
        and open the
        <em>
            Size Inspector
        </em>
        . Set the Width to
        <em>
            350
        </em>
        and the height to
        <em>
            480
        </em>
        :
    </p>
    <p>
        <img class="aligncenter wp-image-121120 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/46_vc_size-e1448290482977-421x320.png"
        alt="46_vc_size" width="421" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/46_vc_size-e1448290482977-421x320.png 421w, https://koenig-media.raywenderlich.com/uploads/2015/11/46_vc_size-e1448290482977.png 514w"
        sizes="(max-width: 421px) 100vw, 421px">
    </p>
    <p>
        Notice that the storyboard canvas now looks strange:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121121" src="https://koenig-media.raywenderlich.com/uploads/2015/11/47_stange_vc-220x320.png"
        alt="47_stange_vc" width="220" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/47_stange_vc-220x320.png 220w, https://koenig-media.raywenderlich.com/uploads/2015/11/47_stange_vc-344x500.png 344w, https://koenig-media.raywenderlich.com/uploads/2015/11/47_stange_vc.png 722w"
        sizes="(max-width: 220px) 100vw, 220px">
    </p>
    <p>
        This is because the layout constraints need to be re-evaluated.
    </p>
    <p>
        Use the
        <em>
            Resolve Auto Layout Issues
        </em>
        menu on the bottom auto layout menu bar and select
        <em>
            All View in View Controller
        </em>
        <em>
            \
        </em>
        <em>
            Update Frames
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121122" src="https://koenig-media.raywenderlich.com/uploads/2015/11/48_fix_al-374x320.png"
        alt="48_fix_al" width="374" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/48_fix_al-374x320.png 374w, https://koenig-media.raywenderlich.com/uploads/2015/11/48_fix_al-585x500.png 585w, https://koenig-media.raywenderlich.com/uploads/2015/11/48_fix_al.png 622w"
        sizes="(max-width: 374px) 100vw, 374px">
    </p>
    <p>
        This will re-run the layout engine over the storyboard, and update the
        preview:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121123" src="https://koenig-media.raywenderlich.com/uploads/2015/11/49_fixed_vc-537x500.png"
        alt="49_fixed_vc" width="537" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/49_fixed_vc-537x500.png 537w, https://koenig-media.raywenderlich.com/uploads/2015/11/49_fixed_vc-343x320.png 343w, https://koenig-media.raywenderlich.com/uploads/2015/11/49_fixed_vc.png 732w"
        sizes="(max-width: 537px) 100vw, 537px">
    </p>
    <p>
        Build and run to see how the app looks now:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121124" src="https://koenig-media.raywenderlich.com/uploads/2015/11/50_bar_04-348x500.png"
        alt="50_bar_04" width="348" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/50_bar_04-348x500.png 348w, https://koenig-media.raywenderlich.com/uploads/2015/11/50_bar_04-223x320.png 223w, https://koenig-media.raywenderlich.com/uploads/2015/11/50_bar_04.png 700w"
        sizes="(max-width: 348px) 100vw, 348px">
    </p>
    <p>
        That looks much better. Try resizing the window—you’ll see that you can
        still manually drag it to sizes that don’t work for MagicEight’s layout.
    </p>
    <p>
        You have a couple of options here—you can either update the layout so
        that it adapts nicely as the window changes size (e.g. to resize the image
        for small windows), or you can fix the window size. You’re going to take
        the second, easier approach.
    </p>
    <h3>
        Window Sizing
    </h3>
    <p>
        The window controller is responsible for managing the size of the window.
        Open
        <em>
            Main.storyboard
        </em>
        and select the window inside the window controller:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121125" src="https://koenig-media.raywenderlich.com/uploads/2015/11/51_select_window-700x295.png"
        alt="51_select_window" width="700" height="295" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/51_select_window-700x295.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/51_select_window-480x202.png 480w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Open the
        <em>
            Size Inspector
        </em>
        and set the Content Size to a Width of
        <em>
            350
        </em>
        and a height of
        <em>
            480
        </em>
        . Then check
        <em>
            Minimum Content Size
        </em>
        and
        <em>
            Maximum Content Size
        </em>
        ensuring that the the sizes are the same as the content size you entered:
    </p>
    <p>
        <img class="aligncenter wp-image-121126 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/52_content_size-e1448290524705-410x320.png"
        alt="52_content_size" width="410" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/52_content_size-e1448290524705-410x320.png 410w, https://koenig-media.raywenderlich.com/uploads/2015/11/52_content_size-e1448290524705.png 514w"
        sizes="(max-width: 410px) 100vw, 410px">
    </p>
    <p>
        Build and run MagicEight again, and attempt to resize the window. You
        no longer have control over the window size—it’s now fixed. Mega—just what
        you wanted.
    </p>
    <p>
        You can now turn your attention back to the task in-hand—building the
        “magic” of the magic 8-ball. Well, nearly—there’s a bit more layout to
        do first.
    </p>
    <h2>
        Handling clicks
    </h2>
    <p>
        When the user clicks on the 8-ball you will switch the image to the other
        side and display a piece of advice. You need a new label to display this
        advice.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and find the view controller scene. Use the
        <em>
            Object Library
        </em>
        to locate a
        <em>
            wrapping label
        </em>
        and drag it from the library beneath the stack view:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121127" src="https://koenig-media.raywenderlich.com/uploads/2015/11/53_wrapping_label-700x388.png"
        alt="53_wrapping_label" width="700" height="388" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/53_wrapping_label-700x388.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/53_wrapping_label-480x266.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/53_wrapping_label.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        You want this label to be positioned at the center of the magic-8 image,
        so you need to add some auto layout constraints.
    </p>
    <p>
        <em>
            Control-drag
        </em>
        from the
        <em>
            Multiline Label
        </em>
        to the
        <em>
            Image View
        </em>
        in the
        <em>
            Document Outline
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-full wp-image-121128" src="https://koenig-media.raywenderlich.com/uploads/2015/11/54_adding_constraints.png"
        alt="54_adding_constraints" width="486" height="164" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/54_adding_constraints.png 486w, https://koenig-media.raywenderlich.com/uploads/2015/11/54_adding_constraints-480x162.png 480w"
        sizes="(max-width: 486px) 100vw, 486px">
    </p>
    <p>
        Hold
        <i>
            shift
        </i>
        and select
        <em>
            Center Vertically
        </em>
        and
        <em>
            Center Horizontally
        </em>
        before clicking
        <em>
            Add Constraints
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121129" src="https://koenig-media.raywenderlich.com/uploads/2015/11/55_center_constraints-215x320.png"
        alt="55_center_constraints" width="215" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/55_center_constraints-215x320.png 215w, https://koenig-media.raywenderlich.com/uploads/2015/11/55_center_constraints-335x500.png 335w, https://koenig-media.raywenderlich.com/uploads/2015/11/55_center_constraints.png 373w"
        sizes="(max-width: 215px) 100vw, 215px">
    </p>
    <p>
        The label doesn’t automatically reposition—but you’ve handled this before.
        Use the
        <em>
            Resolve Auto Layout Issues
        </em>
        menu on the bottom auto layout toolbar to select
        <em>
            All View in View Controller
        </em>
        <em>
            \
        </em>
        <em>
            Update Frames
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121130" src="https://koenig-media.raywenderlich.com/uploads/2015/11/56_fix_al-374x320.png"
        alt="56_fix_al" width="374" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/56_fix_al-374x320.png 374w, https://koenig-media.raywenderlich.com/uploads/2015/11/56_fix_al-585x500.png 585w, https://koenig-media.raywenderlich.com/uploads/2015/11/56_fix_al.png 622w"
        sizes="(max-width: 374px) 100vw, 374px">
    </p>
    <p>
        This repositions the label, and it becomes&nbsp;immediately obvious that
        you need to do some work on the appearance.
    </p>
    <p>
        Select the multiline label, and use the
        <em>
            Attributes Inspector
        </em>
        to set the following:
    </p>
    <ul>
        <li>
            <em>
                Title
            </em>
            :
            <em>
                Piece of Advice
            </em>
        </li>
        <li>
            <em>
                Alignment
            </em>
            :
            <em>
                Center
            </em>
        </li>
        <li>
            <em>
                Text Color
            </em>
            :
            <em>
                Keyboard Focus Indicator
            </em>
        </li>
        <li>
            <em>
                Font
            </em>
            :
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
        Head over to the
        <em>
            Size Inspector
        </em>
        and set the Preferred Width to
        <em>
            Explicit
        </em>
        with a value of
        <em>
            75
        </em>
        :
    </p>
    <p>
        <img class="aligncenter wp-image-121132 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/58_label_size-e1448290564918-480x184.png"
        alt="58_label_size" width="480" height="184" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/58_label_size-e1448290564918-480x184.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/58_label_size-e1448290564918.png 516w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        To get an idea of what the end product might look like, select the image
        view, and use the
        <em>
            Attributes Inspector
        </em>
        to set the Image to
        <em>
            magic8ball
        </em>
        :
    </p>
    <p>
        <img class="aligncenter wp-image-121133 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/11/59_change_image-e1448290610187-480x147.png"
        alt="59_change_image" width="480" height="147" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/59_change_image-e1448290610187-480x147.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/59_change_image-e1448290610187.png 516w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        Once again, click the main view and use the
        <em>
            Resolve Auto Layout Issues\All Views in View Controller\Update Frames
        </em>
        to update the layout:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121134" src="https://koenig-media.raywenderlich.com/uploads/2015/11/60_magic8_layout-337x320.png"
        alt="60_magic8_layout" width="337" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/60_magic8_layout-337x320.png 337w, https://koenig-media.raywenderlich.com/uploads/2015/11/60_magic8_layout-526x500.png 526w, https://koenig-media.raywenderlich.com/uploads/2015/11/60_magic8_layout.png 718w"
        sizes="(max-width: 337px) 100vw, 337px">
    </p>
    <p>
        This is looking pretty good. You need to respond each time the user clicks
        on the 8-ball—time to discover gesture recognizers.
    </p>
    <h3>
        Gesture Recognizers
    </h3>
    <p>
        You were able to create an action in code that would run every time the
        user clicks the button. That was possible because buttons are designed
        to handle clicks—but the same is not true of image views.
    </p>
    <p>
        Apple has provided a set of gesture recognizers that can be added to any
        view. These recognizers convert low-level mouse and trackpad input into
        semantic events—such as click, zoom and rotate.
    </p>
    <p>
        You will add a click gesture recognizer to the image view, and then create
        a corresponding action in the view controller’s code.
    </p>
    <p>
        In
        <em>
            Main.storyboard
        </em>
        , head over to the
        <em>
            Object Library
        </em>
        and search for
        <em>
            click gesture
        </em>
        . Drag the
        <em>
            Click Gesture Recognizer
        </em>
        out of the library and onto the image view. It will appear like this in
        the document outline:
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121135" src="https://koenig-media.raywenderlich.com/uploads/2015/11/61_gesture_recogniser-480x119.png"
        alt="61_gesture_recogniser" width="480" height="119" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/61_gesture_recogniser-480x119.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/61_gesture_recogniser.png 484w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        This gesture recognizer will be activated whenever the user clicks on
        the image—exactly what you want. You now need to create some new connections,
        and then you’ll be ready to switch over to code for the final sprint.
    </p>
    <h3>
        IB Connections
    </h3>
    <p>
        In the same way you did before, open up the assistant editor and ensure
        that it is showing
        <em>
            ViewController.swift
        </em>
        . Then create two new outlets by
        <em>
            control-dragging
        </em>
        from the storyboard to the code: one for the image view (call it
        <em>
            ballImageView
        </em>
        ) and one for the multiline label (call it
        <em>
            adviceLabel
        </em>
        ). This adds the following new outlets:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1102694">
                    <td class="code" id="p110269code4">
                        <pre class="swift" style="font-family:monospace;">
                            @IBOutlet weak
                            <span style="color: #a61390;">
                                var
                            </span>
                            ballImageView
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #400080;">
                                NSImageView
                            </span>
                            <span style="color: #002200;">
                                !
                            </span>
                            @IBOutlet weak
                            <span style="color: #a61390;">
                                var
                            </span>
                            adviceLabel
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #400080;">
                                NSTextField
                            </span>
                            <span style="color: #002200;">
                                !
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        You also need an action to wire up the newly-created gesture recognizer.
        <em>
            Control-drag
        </em>
        from the click gesture recognizer in the document outline, over to the
        code:
    </p>
    <p>
        <img class="aligncenter size-large wp-image-121136" src="https://koenig-media.raywenderlich.com/uploads/2015/11/62_gesture_action-700x158.png"
        alt="62_gesture_action" width="700" height="158" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/62_gesture_action-700x158.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/62_gesture_action-480x108.png 480w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Change the Connection to
        <em>
            Action
        </em>
        and name it
        <em>
            handleBallClick
        </em>
        :
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-121137" src="https://koenig-media.raywenderlich.com/uploads/2015/11/63_action_config-480x220.png"
        alt="63_action_config" width="480" height="220" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/63_action_config-480x220.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/63_action_config.png 568w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        Click
        <em>
            Connect
        </em>
        and Xcode will add the following function definition to the
        <code>
            ViewController
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1102695">
                    <td class="code" id="p110269code5">
                        <pre class="swift" style="font-family:monospace;">
                            @IBAction
                            <span style="color: #a61390;">
                                func
                            </span>
                            handleBallClick
                            <span style="color: #002200;">
                                (
                            </span>
                            sender
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #a61390;">
                                AnyObject
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                {
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
        You’ve now finished all the work in Interface Builder, so you can switch
        back to the standard editor, and open
        <em>
            ViewController.swift
        </em>
        .
    </p>
    <h2>
        Manipulating UI from code
    </h2>
    <p>
        When the user clicks on the 8-ball you want to switch between showing
        some advice, or showing the “8”. This means that the
        <code>
            handleBallClick(_:)
        </code>
        will manipulate both the image view and the advice label.
    </p>
    <p>
        Add the following code to
        <code>
            handleBallClick(_:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1102696">
                    <td class="code" id="p110269code6">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #11740a; font-style: italic;">
                                // 1:
                            </span>
                            <span style="color: #a61390;">
                                if
                            </span>
                            <span style="color: #002200;">
                                (
                            </span>
                            adviceLabel.hidden
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            <span style="color: #11740a; font-style: italic;">
                                // 2:
                            </span>
                            adviceLabel.hidden
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #a61390;">
                                false
                            </span>
                            ballImageView.image
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #400080;">
                                NSImage
                            </span>
                            <span style="color: #002200;">
                                (
                            </span>
                            named
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #bf1d1a;">
                                "magic8ball"
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                }
                            </span>
                            <span style="color: #a61390;">
                                else
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            <span style="color: #11740a; font-style: italic;">
                                // 3:
                            </span>
                            adviceLabel.hidden
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #a61390;">
                                true
                            </span>
                            ballImageView.image
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #400080;">
                                NSImage
                            </span>
                            <span style="color: #002200;">
                                (
                            </span>
                            named
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #bf1d1a;">
                                "8ball"
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
    <ol start="1">
        <li>
            Check whether the
            <code>
                adviceLabel
            </code>
            is currently visible.
            <code>
                hidden
            </code>
            is a boolean property on
            <code>
                NSView
            </code>
            (and hence
            <code>
                NSTextField
            </code>
            ) that allows you to specify whether the view should be visible or not.
        </li>
        <li>
            If the advice label is currently hidden then show it, and change the image
            to the magic-side.
            <code>
                NSImage(named:)
            </code>
            loads the image from the asset catalog, and the
            <code>
                image
            </code>
            property on
            <code>
                NSImageView
            </code>
            specifies the image to display.
        </li>
        <li>
            Conversely, if the advice label is currently visible then hide it and
            switch the ball back to the “8” side.
        </li>
    </ol>
    <p>
        Build and run and click the ball to see it switching between showing the
        “8” and the piece of advice. Pretty neat right? Notice how when you first
        start the app the advice is already showing? That’s not really what you
        want, but it’s a simple fix.
    </p>
    <h2>
        Initial Setup
    </h2>
    <p>
        When the app first starts you want to ensure that the advice label is
        hidden, and the 8-ball image is showing. View controllers have a perfect
        way of configuring this initial setup—in the form of
        <code>
            viewDidLoad()
        </code>
        .
    </p>
    <p>
        Once the view controller has finished loading all the view components
        from the storyboard, it calls&nbsp;
        <code>
            viewDidLoad()
        </code>
        &nbsp;to give you a chance to perform&nbsp;some final configuration.
    </p>
    <p>
        In
        <em>
            ViewController.swift
        </em>
        , find the
        <code>
            viewDidLoad()
        </code>
        method and add the following body:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1102697">
                    <td class="code" id="p110269code7">
                        <pre class="swift" style="font-family:monospace;">
                            adviceLabel.hidden
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #a61390;">
                                true
                            </span>
                            ballImageView.image
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #400080;">
                                NSImage
                            </span>
                            <span style="color: #002200;">
                                (
                            </span>
                            named
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #bf1d1a;">
                                "8ball"
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
        You’ll recognize this code from the click handler action—it just hides
        the advice label and sets the image to
        <em>
            8ball
        </em>
        .
    </p>
    <p>
        Build and run to check that you can’t see the advice from the outset.
    </p>
    <h2>
        Advice Generator
    </h2>
    <p>
        At the moment, no matter how many times you “shake” the ball, it always
        gives you the same advice. That’s not especially helpful. Time to add a
        bit of randomness.
    </p>
    <p>
        Add the following code as a property inside
        <code>
            ViewController
        </code>
        —just below the class definition line:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1102698">
                    <td class="code" id="p110269code8">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #a61390;">
                                let
                            </span>
                            adviceList
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #002200;">
                                [
                            </span>
                            <span style="color: #bf1d1a;">
                                "Yes"
                            </span>
                            ,
                            <span style="color: #bf1d1a;">
                                "No"
                            </span>
                            ,
                            <span style="color: #bf1d1a;">
                                "Ray says 'do it!'"
                            </span>
                            ,
                            <span style="color: #bf1d1a;">
                                "Maybe"
                            </span>
                            ,
                            <span style="color: #bf1d1a;">
                                "Try again later"
                            </span>
                            ,
                            <span style="color: #bf1d1a;">
                                "How can I know?"
                            </span>
                            ,
                            <span style="color: #bf1d1a;">
                                "Totally"
                            </span>
                            ,
                            <span style="color: #bf1d1a;">
                                "Never"
                            </span>
                            ,
                            <span style="color: #002200;">
                                ]
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This is an array of strings the make up all the different options for
        advice that the ball can dispense.
    </p>
    <p>
        Head to the very bottom of the file (not within the
        <code>
            ViewController
        </code>
        class) and add the following extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1102699">
                    <td class="code" id="p110269code9">
                        <pre class="swift" style="font-family:monospace;">
                            extension
                            <span style="color: #a61390;">
                                Array
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            <span style="color: #a61390;">
                                var
                            </span>
                            randomElement
                            <span style="color: #002200;">
                                :
                            </span>
                            Element?
                            <span style="color: #002200;">
                                {
                            </span>
                            <span style="color: #a61390;">
                                if
                            </span>
                            <span style="color: #a61390;">
                                count
                            </span>
                            &lt;
                            <span style="color: #2400d9;">
                                1
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            <span style="color: #a61390;">
                                return
                            </span>
                            .None
                            <span style="color: #002200;">
                                }
                            </span>
                            <span style="color: #a61390;">
                                let
                            </span>
                            randomIndex
                            <span style="color: #002200;">
                                =
                            </span>
                            arc4random_uniform
                            <span style="color: #002200;">
                                (
                            </span>
                            UInt32
                            <span style="color: #002200;">
                                (
                            </span>
                            <span style="color: #a61390;">
                                count
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #a61390;">
                                return
                            </span>
                            <span style="color: #a61390;">
                                self
                            </span>
                            <span style="color: #002200;">
                                [
                            </span>
                            <span style="color: #a61390;">
                                Int
                            </span>
                            <span style="color: #002200;">
                                (
                            </span>
                            randomIndex
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                ]
                            </span>
                            <span style="color: #002200;">
                                }
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
        This adds a new property to the standard library’s
        <code>
            Array
        </code>
        type that will return a random element. If the array is empty it returns
        <code>
            nil
        </code>
        , otherwise it generates a random index using
        <code>
            arc4random_uniform()
        </code>
        before returning the corresponding element.
    </p>
    <p>
        Update the first branch (i.e.
        <code>
            adviceLabel.hidden == true
        </code>
        ) of the
        <code>
            if
        </code>
        statement in
        <code>
            handleBallClick(_:)
        </code>
        to match the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p11026910">
                    <td class="code" id="p110269code10">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #a61390;">
                                if
                            </span>
                            <span style="color: #a61390;">
                                let
                            </span>
                            advice
                            <span style="color: #002200;">
                                =
                            </span>
                            adviceList.randomElement
                            <span style="color: #002200;">
                                {
                            </span>
                            adviceLabel.stringValue
                            <span style="color: #002200;">
                                =
                            </span>
                            advice adviceLabel.hidden
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #a61390;">
                                false
                            </span>
                            ballImageView.image
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #400080;">
                                NSImage
                            </span>
                            <span style="color: #002200;">
                                (
                            </span>
                            named
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #bf1d1a;">
                                "magic8ball"
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
        This attempts to get a random piece of advice to display, and if successful
        updates the
        <code>
            stringValue
        </code>
        on
        <code>
            adviceLabel
        </code>
        to show it.
    </p>
    <p>
        Build and run, and click the 8-ball a few times to start benefiting from
        the ball’s wisdom:
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
