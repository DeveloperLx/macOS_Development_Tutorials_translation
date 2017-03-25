# OS X View Controllers教程

#### [原文地址](https://www.raywenderlich.com/112811/os-x-view-controllers-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div id="attachment_119460" style="width: 260px" class="wp-caption alignright">
        <img class="wp-image-119460 size-full" src="https://koenig-media.raywenderlich.com/uploads/2015/10/featured_image3.png"
        alt="macOS view controllers tutorial" width="250" height="250" srcset="https://koenig-media.raywenderlich.com/uploads/2015/10/featured_image3.png 250w, https://koenig-media.raywenderlich.com/uploads/2015/10/featured_image3-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/10/featured_image3-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2015/10/featured_image3-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2015/10/featured_image3-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
        <p class="wp-caption-text">
            使用这个macOS View Controller的教程，来学习怎样控制UI！
        </p>
    </div>
    <p>
        在撰写任意代码的时候，对关注点做出清晰的分割是非常重要的 - 功能应当被分为恰当的较小的类。这可以让代码易于维护且容易理解。苹果在macOS上，围绕Model-View-Controller模式设计了可用的框架，并提供了各种各样的负责管理UI的controller对象。
    </p>
    <p>
        View controller负责连结model层到view层，在你的macOS app的架构中扮演了难以置信的重要的角色。
    </p>
    <p>
        在这个macOS view controller的教程中，你将看到广泛的功能被“烘焙”成了“香草味”的view controller，并学习怎样创建你自己的view controller的子类，来以容易被理解的方式构建你的app。你将了解到生命周期的方法，如何hook到你的app的重要的事件，还有关于view controller和window controller之间的比较。
    </p>
    <p>
        为了跟进这个教程，你需要安装最新版本的macOS和Xcode。这次没有起始项目 - 你将从0开始构建一个很赞的项目！在着手这个view controller教程之前，你可以首先阅读一下Gabriel Miro的
        <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Windows%20and%20Window%20Controllers%20in%20OS%20X%20Tutorial.md"
        sl-processed="1">
            window和window controller的教程
        </a>
        ，但这不是必须的。
    </p>
    <p>
        开场白足够了 - 让我们从一些理论开始吧！
    </p>
    <h2>
        介绍View Controller
    </h2>
    <p>
        view controller是用来负责管理一个view和它的子view的。在
        <em>
            macOS
        </em>
        中，view controller是由
        <code>
            NSViewController
        </code>
        的子类实现的。
    </p>
    <p>
        View controller已经存在有一定的时间了（苹果是在OS X 10.5时引入的这个），但在OS X 10.10之前，它并不在相应者链中的一部分。这就意味着，例如，如果你的view controller的view上有一个button，这个view controller是无法接受到它的事件的。然而，在OS X 10.10之后，view controller作为负责的用户界面的构建块，已变得非常有用。
    </p>
    <p>
        View controller使你将window的内容切分为逻辑的单元。view controller来照顾那些更小的单元，就如同window controller，处理类似改变大小或关闭window之类的指定的任务。这就让你的代码变得更容易组织。
    </p>
    <p>
        另一个好处是view controller是比较容易在其它应用中重用的。如果在一个文件浏览器中，左侧带有一个被单独的view controller控制的层级的视图，你就可以将它用到另一个需要类似的view的应用中。你就可以用省下的时间和精力去喝啤酒了！
    </p>
    <h3>
        Window Controller或View Controller？
    </h3>
    <p>
        你可能想要知道，什么时候该使用仅仅一个window controller，什么时候又该去实现多个的view controller。
    </p>
    <p>
        在OS X 10.10 Yosemite之前，
        <code>
            NSViewController
        </code>
        并不是一个非常有用的类。它没有提供任何你所期待的view controller的功能 - 例如，可以在
        <code>
            UIViewController
        </code>
        中找到的。
    </p>
    <p>
        由于引入的变化，诸如view的生命周期，以及view controller被包含到响应者链中来接收从它的view中而来的事件，苹果正在推进它正在iOS开发中实习的Model View Controller（MVC）模式。你应当使用view controller来处理你的view、子view以及用户界面的全部的功能。使用window controller来实现相应于应用window的功能，例如设置根view controller，调整大小，改变位置，设置title等。
    </p>
    <p>
        这个教程，将通过将UI的不同部分为几个view controller来构建负责的用户界面，并使用它们，如构建的块来组成完整的用户界面。
    </p>
    <h2>
        View Controller的动作
    </h2>
    <p>
        在这个教程中，你将要写一个叫做
        <em>
            RWStore
        </em>
        的应用，你可以在其中选择来自
        <a href="http://www.raywenderlich.com/store" sl-processed="1">
            raywenderlich.com store
        </a>
        的不同的书。 让我们开始吧！
    </p>
    <p>
        打开Xcode选择创建一个新的Xcode的项目，并从模板菜单中选择
        <em>
            macOS/Application/Cocoa Application
        </em>
        。单击
        <em>
            Next
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/SelectTemplate.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/SelectTemplate-449x320.png"
            alt="" width="449" height="320" class="aligncenter size-medium wp-image-155677"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/SelectTemplate-449x320.png 449w, https://koenig-media.raywenderlich.com/uploads/2017/02/SelectTemplate-650x463.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/SelectTemplate.png 1462w"
            sizes="(max-width: 449px) 100vw, 449px">
        </a>
    </p>
    <p>
        为你的项目起名
        <em>
            RWStore
        </em>
        。在选择这屏中，确保选择
        <em>
            Swift
        </em>
        语言，并勾选
        <em>
            Use Storyboards
        </em>
        选择框。你不需要Unit和UI Tests，因此取消相应的勾选框。单击
        <em>
            Next
        </em>
        并保存你的项目。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/TemplateSettings.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/TemplateSettings-452x320.png"
            alt="" width="452" height="320" class="aligncenter size-medium wp-image-155678"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/TemplateSettings-452x320.png 452w, https://koenig-media.raywenderlich.com/uploads/2017/02/TemplateSettings-650x460.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/TemplateSettings.png 1462w"
            sizes="(max-width: 452px) 100vw, 452px">
        </a>
    </p>
    <p>
        下载项目
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/resources2.zip"
        sl-processed="1">
            资源
        </a>
        。这个压缩文件包含书的图片，和一个
        <em>
            Products.plist
        </em>
        的文件，包含有产品信息的字典，例如名称、描述和价格。你也将找到一个名叫
        <em>
            Product.swift
        </em>
        的源码文件。这个文件包含了
        <em>
            Product
        </em>
        类，它会从那个plist文件中读取产品的信息。你将添加这些到RWStore中。
    </p>
    <p>
        在
        <em>
            Project Navigator
        </em>
        中选择
        <em>
            Assets.xcassets
        </em>
        目录，并拖拽下载的图片到包含有app icon的列中。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/AddAssets.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/AddAssets-480x277.png"
            alt="" width="480" height="277" class="aligncenter size-medium wp-image-155680"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/AddAssets-480x277.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/02/AddAssets-650x375.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/AddAssets.png 1022w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        将
        <em>
            Products.plist
        </em>
        和
        <em>
            Product.swift
        </em>
        拖拽到左侧的
        <em>
            Project Navigator
        </em>
        中。确保
        <em>
            Copy items if needed
        </em>
        已选中。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/AddProductsPlist.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/AddProductsPlist-480x220.png"
            alt="" width="480" height="220" class="aligncenter size-medium wp-image-155681"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/AddProductsPlist-480x220.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/02/AddProductsPlist-650x298.png 650w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        build并运行app。你应会看到你的应用的主窗口。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/window-empty.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113611" src="https://koenig-media.raywenderlich.com/uploads/2015/09/window-empty.png"
            alt="window-empty" width="480" height="292">
        </a>
    </p>
    <p>
        现在它是空的，但不要担心 - 这只是开始。
    </p>
    <h2>
        创建用户界面
    </h2>
    <p>
        打开 
        <em>
            Main.storyboard
        </em>
        ，选择
        <em>
            View Controller Scene
        </em>
        ，并拖拽一个
        <em>
            pop-up button
        </em>
        到view上。你将使用这个
        <em>
            pop-up button
        </em>
        来展示产品的列表。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/add-popup.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113645" src="https://koenig-media.raywenderlich.com/uploads/2015/09/add-popup-700x264.png"
            alt="add-popup" width="700" height="264" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/add-popup-700x264.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/add-popup-480x181.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/add-popup.png 894w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        使用自动布局来设置它的位置。这个pop-up button应当占据这个view全部的宽度，并贴近在顶部，因此选择这个pop-up，点击位于底部的
        <em>
            Add New Constraints
        </em>
        按钮。
    </p>
    <p>
        在出现的pop-up中，选择trailing约束并设置它的值为
        <em>
            Use Standard Value
        </em>
        。对top和leading约束重复同样的操作，并单击
        <em>
            Add 3 Constraints
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/PinPopupButton.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/PinPopupButton-424x320.png"
            alt="" width="424" height="320" class="aligncenter size-medium wp-image-155682"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/PinPopupButton-424x320.png 424w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinPopupButton-650x490.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinPopupButton.png 1554w"
            sizes="(max-width: 424px) 100vw, 424px">
        </a>
    </p>
    <p>
        为了完成这个UI，添加一个view去展示产品的细节。选择
        <em>
            container view
        </em>
        并将它拖拽到pop-up按钮的底部。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/add-container.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113612" src="https://koenig-media.raywenderlich.com/uploads/2015/09/add-container-700x271.png"
            alt="add-container" width="700" height="271" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/add-container-700x271.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/add-container-480x186.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/add-container.png 872w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        <em>
            container view
        </em>
        是为了另外的view的占位符，并伴随着它自己的View Controller。
    </p>
    <p>
        现在来设置这个view的自动布局的约束。选择container view并单击
        <em>
            Add New Constraints
        </em>
        按钮。添加
        <em>
            top
        </em>
        ，
        <em>
            bottom
        </em>
        ，
        <em>
            trailing
        </em>
        和
        <em>
            leading
        </em>
        约束，值为
        <em>
            0
        </em>
        。单击
        <em>
            Add 4 Constraints
        </em>
        按钮。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/PinContainer.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/PinContainer-458x320.png"
            alt="" width="458" height="320" class="aligncenter size-medium wp-image-155684"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/PinContainer-458x320.png 458w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinContainer-650x455.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinContainer.png 1330w"
            sizes="(max-width: 458px) 100vw, 458px">
        </a>
    </p>
    <p>
        选择你view controller的view，并点击那几行约束按钮中的
        <em>
            Update Frames
        </em>
        按钮。你的view应当看起来像这样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/FinishedVC.png"
        sl-processed="1">
            <img class="size-medium wp-image-112828 aligncenter" src="https://koenig-media.raywenderlich.com/uploads/2015/08/FinishedVC-480x302.png"
            alt="FinishedVC" width="480" height="302" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/FinishedVC-480x302.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/FinishedVC.png 485w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        现在你将创建一个动作，它将在这个按钮的选择发生变化时被调用。打开
        <em>
            Assistant Editor
        </em>
        （你也可以使用快捷键
        <em>
            Command-Option-Return
        </em>
        ），并确定
        <em>
            ViewController.swift
        </em>
        已打开。从
        <em>
            pop-up button
        </em>
        <em>
            拖拽
        </em>
        到
        <em>
            ViewController.swift
        </em>
        中来添加一个Action连接。在弹出的视图中，确认connection是
        <em>
            Action
        </em>
        ，Name为
        <em>
            valueChanged
        </em>
        ，Type为
        <em>
            NSPopUpButton
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/PopupActionDrag.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/PopupActionDrag-480x300.png"
            alt="" width="480" height="300" class="aligncenter size-medium wp-image-155706"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/PopupActionDrag-480x300.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/02/PopupActionDrag-650x406.png 650w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/PopupButtonAction2.png"
        alt="" width="511" height="247" class="aligncenter size-full wp-image-155924"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/PopupButtonAction2.png 511w, https://koenig-media.raywenderlich.com/uploads/2017/02/PopupButtonAction2-480x232.png 480w"
        sizes="(max-width: 511px) 100vw, 511px">
    </p>
    <p>
        在画布中，现在有了一个新的view controller通过
        <i>
            embed segue
        </i>
        被连接到了container view上。你的app将使用一个定制的view controller，因此你可以删除自动生成的那个：选择相应于container view的那个view controller并按
        <em>
            delete
        </em>
        键。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/delete-viewcontroller.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113615" src="https://koenig-media.raywenderlich.com/uploads/2015/09/delete-viewcontroller-700x459.png"
            alt="delete-viewcontroller" width="700" height="459" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/delete-viewcontroller-700x459.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/delete-viewcontroller-480x314.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/delete-viewcontroller.png 983w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <h2>
        Tab View Controller
    </h2>
    <p>
        现在你已经添加了用来展示产品信息的view controller：
        <em>
            Tab View Controller
        </em>
        。
        <em>
            Tab View Controller
        </em>
        是
        <code>
            NSTabViewController
        </code>
        的子类；它包含一个带有两个或更多的项目的tab view和一个container view。在每个tab的背后是另一个view controller，它的内容被用来填充container view。每次当一个新的tab被选择时，这个Tab View Controller就用相应的view controller替换了它的内容。
    </p>
    <p>
        选择
        <em>
            Tab View Controller
        </em>
        并将其拖拽到画布上。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/drag-tabcontroller.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113616" src="https://koenig-media.raywenderlich.com/uploads/2015/09/drag-tabcontroller-700x385.png"
            alt="drag-tabcontroller" width="700" height="385" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/drag-tabcontroller-700x385.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/drag-tabcontroller-480x264.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/drag-tabcontroller.png 1050w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        现在这个tab controller已经在storyboard上了，但到现在都没有用过。使用一个embed segue来将它连接到container view；从container view
        <em>
            拖拽
        </em>
        到Tab View Controller.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/control-drag-tabview.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113617" src="https://koenig-media.raywenderlich.com/uploads/2015/09/control-drag-tabview-700x344.png"
            alt="control-drag-tabview" width="700" height="344" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/control-drag-tabview-700x344.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/control-drag-tabview-480x236.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/control-drag-tabview.png 772w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        在弹出的菜单中选择
        <em>
            embed
        </em>
        。
        <br>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/Embed.png"
        sl-processed="1">
            <img class="size-full wp-image-112831 aligncenter" src="https://koenig-media.raywenderlich.com/uploads/2015/08/Embed.png"
            alt="Embed" width="130" height="33" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/Embed.png 130w, https://koenig-media.raywenderlich.com/uploads/2015/08/Embed-128x33.png 128w"
            sizes="(max-width: 130px) 100vw, 130px">
        </a>
    </p>
    <p>
        这样变化之后，当app运行container view时，container view的区域被替换为Tab View Controller的view。双击Tab View左侧的那个tab，并将它重命名为
        <em>
            Overview
        </em>
        。重复同样的操作，将右边的tab重命名为
        <em>
            Details
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/rename-tabs.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113618" src="https://koenig-media.raywenderlich.com/uploads/2015/09/rename-tabs.png"
            alt="rename-tabs" width="476" height="360" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/rename-tabs.png 476w, https://koenig-media.raywenderlich.com/uploads/2015/09/rename-tabs-423x320.png 423w"
            sizes="(max-width: 476px) 100vw, 476px">
        </a>
    </p>
    <p>
        build并运行app
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/tabview-empty2.png"
        alt="" width="480" height="287" class="aligncenter size-full wp-image-155926">
    </p>
    <p>
        现在这个tab view controller已经展示出来了，你可以使用tab来在两个不同的view controller之间进行选择。但现在还不是显而易见的（noticeable），因为这两个view恰好是相同的，但当你选择了一个tab时，在内部tab view controller确实是将他们替换了的。
    </p>
    <h2>
        Overview的View Controller
    </h2>
    <p>
        接下来你需要为
        <em>
            Overview
        </em>
        tab创建相应的view controller。
    </p>
    <p>
        前往
        <em>
            File/New/File…
        </em>
        ，选择
        <em>
            macOS/Source/Cocoa Class
        </em>
        ，并单击
        <em>
            Next
        </em>
        。将类命名为
        <em>
            OverviewController
        </em>
        ，使其成为
        <em>
            NSViewController
        </em>
        的子类，确保
        <em>
            Also Create XIB for user interface
        </em>
        未被选中。单击
        <em>
            Next
        </em>
        并保存。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/add-overview.png"
        sl-processed="1">
            <img class="aligncenter wp-image-113621 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/09/add-overview-453x320.png"
            alt="add-overview" width="453" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/add-overview-453x320.png 453w, https://koenig-media.raywenderlich.com/uploads/2015/09/add-overview-700x495.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/add-overview.png 716w"
            sizes="(max-width: 453px) 100vw, 453px">
        </a>
    </p>
    <p>
        Return to
        <em>
            Main.storyboard
        </em>
        and select
        <em>
            Overview Scene
        </em>
        . Click the blue circle on the view and change the class to
        <em>
            OverviewController
        </em>
        in the
        <em>
            Identity Inspector
        </em>
        on the right.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/OverviewVC.png"
        sl-processed="1">
            <img class="size-medium wp-image-112832 aligncenter" src="https://koenig-media.raywenderlich.com/uploads/2015/08/OverviewVC-480x246.png"
            alt="OverviewVC" width="480" height="246" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/OverviewVC-480x246.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/OverviewVC.png 633w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Drag three
        <em>
            labels
        </em>
        onto the
        <em>
            OverviewController’s
        </em>
        view. Place the labels on the top left side of the view, one below each
        other. Add an
        <em>
            image view
        </em>
        on the top right corner of the view.
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            By default, the image view has no borders and can be a bit difficult to
            find in the view. To help during the layout process, you can set an image.
            With the image view selected, open the
            <em>
                Attributes Inspector
            </em>
            and select
            <em>
                2d_games
            </em>
            in the
            <em>
                Image
            </em>
            field. This image will be replaced in runtime with the proper product
            image in the tutorial code
        </p>
    </div>
    <p>
        Select the top label. In the
        <em>
            Attributes Inspector
        </em>
        , change the font to System Bold and the size to 19. You will need to
        resize the label now to see all the text.
    </p>
    <p>
        The view should now look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/OverviewFinishedUI.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/OverviewFinishedUI-432x320.png"
            alt="" width="432" height="320" class="aligncenter size-medium wp-image-155686"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/OverviewFinishedUI-432x320.png 432w, https://koenig-media.raywenderlich.com/uploads/2017/02/OverviewFinishedUI-650x481.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/OverviewFinishedUI.png 908w"
            sizes="(max-width: 432px) 100vw, 432px">
        </a>
    </p>
    <p>
        It’s time to use the superpowers of auto layout to make this view look
        great.
    </p>
    <p>
        Select the image view and click the
        <em>
            Add New Constraints
        </em>
        button on the bottom. Add constraints for top and trailing with the standard
        value, and constraints for width and height with a value of 180.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/PinImageView.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/PinImageView-325x320.png"
            alt="" width="325" height="320" class="aligncenter size-medium wp-image-155687"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/PinImageView-325x320.png 325w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinImageView-508x500.png 508w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinImageView-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinImageView-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinImageView-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinImageView-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinImageView.png 1274w"
            sizes="(max-width: 325px) 100vw, 325px">
        </a>
    </p>
    <p>
        Select the top label and add bottom, top, leading, and trailing constraints
        using the standard value.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/PinTopLabel.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/PinTopLabel-480x300.png"
            alt="" width="480" height="300" class="aligncenter size-medium wp-image-155688"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/PinTopLabel-480x300.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinTopLabel-650x406.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinTopLabel.png 1316w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Select the label below and add constraints for trailing and leading using
        the standard value.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/PinMiddleLabel.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/PinMiddleLabel-480x284.png"
            alt="" width="480" height="284" class="aligncenter size-medium wp-image-155689"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/PinMiddleLabel-480x284.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinMiddleLabel-650x385.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinMiddleLabel.png 1314w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Widen the last label so it goes under the image, then add constraints
        for leading, trailing and bottom, using the standard value. For the top
        constraint, make sure that the image view is selected (so that the top
        is aligned to the image view), and use the standard value.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/PinBottomLabel.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/PinBottomLabel-480x273.png"
            alt="" width="480" height="273" class="aligncenter size-medium wp-image-155690"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/PinBottomLabel-480x273.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinBottomLabel-650x370.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinBottomLabel-266x151.png 266w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinBottomLabel.png 1458w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Select the view and click on the
        <em>
            Update Frames
        </em>
        button in the bottom bar. Your view should look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/OverviewFinishedConstraints.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/OverviewFinishedConstraints-480x298.png"
            alt="" width="480" height="298" class="aligncenter size-medium wp-image-155691"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/OverviewFinishedConstraints-480x298.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/02/OverviewFinishedConstraints-650x403.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/OverviewFinishedConstraints.png 916w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        After all your hard work on the interface, it’s finally time to see the
        result, so build and run.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/RunOverview.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/RunOverview-424x320.png"
            alt="" width="424" height="320" class="aligncenter size-medium wp-image-155692"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/RunOverview-424x320.png 424w, https://koenig-media.raywenderlich.com/uploads/2017/02/RunOverview-650x491.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/RunOverview.png 1184w"
            sizes="(max-width: 424px) 100vw, 424px">
        </a>
    </p>
    <p>
        Click on the tabs and see how the tab view controller shows the appropriate
        view controller. It works right out of the box and without a single line
        of code!
    </p>
    <h2>
        Add Some Code
    </h2>
    <p>
        It’s time to get your hands dirty adding some code to show the products
        details in the view. In order to refer to the labels and image view from
        code you need to add an
        <em>
            IBOutlet
        </em>
        for each of them.
    </p>
    <p>
        First, open the
        <em>
            Assistant Editor
        </em>
        and make sure
        <em>
            OverviewViewController.swift
        </em>
        is selected.&nbsp;
        <em>
            Control-drag
        </em>
        from the top label into
        <em>
            OverviewController.swift
        </em>
        and add an outlet named
        <code>
            titleLabel
        </code>
        . Ensure&nbsp;the type is
        <em>
            NSTextField
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/TitleOutlet.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/TitleOutlet-480x232.png"
            alt="" width="480" height="232" class="aligncenter size-medium wp-image-155693"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/TitleOutlet-480x232.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/02/TitleOutlet-650x314.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/TitleOutlet.png 1214w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Repeat the process with the other two labels and the image view to create
        the rest of the outlets with the following names:
    </p>
    <ol>
        <li>
            <code>
                priceLabel
            </code>
            for the label in the middle.
        </li>
        <li>
            <code>
                descriptionLabel
            </code>
            for the bottom label.
        </li>
        <li>
            <code>
                productImageView
            </code>
            for the image view.
        </li>
    </ol>
    <p>
        Like most UI elements, labels and image views are built of multiple subviews,
        so make sure that you have the correct view selected. You can see this
        when you look at the class for the outlet: for the image view it must be
        <em>
            NSImageView
        </em>
        , not
        <em>
            NSImageCell
        </em>
        . For the labels, it must be
        <em>
            NSTextField
        </em>
        , not
        <em>
            NSTextFieldCell
        </em>
        .
    </p>
    <p>
        To show the product information in the overview tab, open
        <em>
            OverviewController.swift
        </em>
        and add the following code inside the class implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1538441">
                    <td class="code" id="p153844code1">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #008312;">
                                //1
                            </span>
                            <span style="color: #B833A1;">
                                let
                            </span>
                            numberFormatter = NumberFormatter
                            <span style="color: black;">
                                (
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: #008312;">
                                //2
                            </span>
                            <span style="color: #B833A1;">
                                var
                            </span>
                            selectedProduct
                            <span style="color: black;">
                                :
                            </span>
                            Product?
                            <span style="color: black;">
                                {
                            </span>
                            <span style="color: #B833A1;">
                                didSet
                            </span>
                            <span style="color: black;">
                                {
                            </span>
                            updateUI
                            <span style="color: black;">
                                (
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Taking this code bit-by-bit:
    </p>
    <ol>
        <li>
            <code>
                numberFormatter
            </code>
            is an
            <code>
                NumberFormatter
            </code>
            object used to show the value of the price, formatted as currency.
        </li>
        <li>
            <code>
                selectedProduct
            </code>
            holds the currently selected product. Every time the value changes,
            <code>
                didSet
            </code>
            is executed, and with it
            <code>
                updateUI
            </code>
            .
        </li>
    </ol>
    <p>
        Now add the&nbsp;
        <code>
            updateUI
        </code>
        method to
        <em>
            OverviewController.swift
        </em>
        .
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1538442">
                    <td class="code" id="p153844code2">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #B833A1;">
                                private
                            </span>
                            <span style="color: #B833A1;">
                                func
                            </span>
                            updateUI
                            <span style="color: black;">
                                (
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: black;">
                                {
                            </span>
                            <span style="color: #008312;">
                                //1
                            </span>
                            <span style="color: #B833A1;">
                                if
                            </span>
                            isViewLoaded
                            <span style="color: black;">
                                {
                            </span>
                            <span style="color: #008312;">
                                //2
                            </span>
                            <span style="color: #B833A1;">
                                if
                            </span>
                            <span style="color: #B833A1;">
                                let
                            </span>
                            product = selectedProduct
                            <span style="color: black;">
                                {
                            </span>
                            productImageView.
                            <span style="color: #508187;">
                                image
                            </span>
                            = product.
                            <span style="color: #508187;">
                                image
                            </span>
                            titleLabel.
                            <span style="color: #508187;">
                                stringValue
                            </span>
                            = product.
                            <span style="color: #508187;">
                                title
                            </span>
                            priceLabel.
                            <span style="color: #508187;">
                                stringValue
                            </span>
                            = numberFormatter.
                            <span style="color: #508187;">
                                string
                            </span>
                            <span style="color: black;">
                                (
                            </span>
                            from
                            <span style="color: black;">
                                :
                            </span>
                            product.
                            <span style="color: #508187;">
                                price
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: black;">
                                ??
                            </span>
                            <span style="color: #C41A16;">
                                "n/a"
                            </span>
                            descriptionLabel.
                            <span style="color: #508187;">
                                stringValue
                            </span>
                            = product.
                            <span style="color: #508187;">
                                descriptionText
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <ol>
        <li>
            Checks to see if the view is loaded.
            <code>
                isViewLoaded
            </code>
            is a property of
            <code>
                NSViewController
            </code>
            , and it’s true if the view is loaded into memory. If the view is loaded,
            it’s safe to access all view-related properties, like the labels.
        </li>
        <li>
            Unwraps
            <code>
                selectedProduct
            </code>
            to see if there is a product. After that, the labels and image are updated
            to show the appropriate values.
        </li>
    </ol>
    <p>
        This method is already called when the product changes, but also needs
        to be called as the view is ready to be displayed.
    </p>
    <h2>
        View Controller Life Cycle
    </h2>
    <p>
        Since view controllers are responsible for managing views, they expose
        methods that allow you to hook into events associated with the views. For
        example&nbsp;the point at which the views have loaded from the storyboard,
        or when the views are about to appear on the screen. This collection of
        event-based methods are known as the
        <em>
            view controller life cycle
        </em>
        .
    </p>
    <p>
        The life cycle of a view controller can be divided into three major parts:
        its creation, its lifetime, and finally its termination. Each part has
        methods you can override to do additional work.
    </p>
    <h3>
        Creation
    </h3>
    <ol>
        <li>
            <code>
                viewDidLoad
            </code>
            is called once the view is fully loaded and can be used to do one-time
            initializations like the configuration of a number formatter, registering
            for notifications, or calls to API that only need to be done once.
        </li>
        <li>
            <code>
                viewWillAppear
            </code>
            is called every time the view is about to appear on screen. In our application,
            it is called every time you select the Overview tab. This is a good point
            to update your UI or to refresh your data model.
        </li>
        <li>
            <code>
                viewDidAppear
            </code>
            is called after the view appears on screen. Here you can start some fancy
            animations.
        </li>
    </ol>
    <h3>
        Lifetime
    </h3>
    <p>
        Once a view controller has been created, it then enters a period during
        which it it handles user interactions. It has three methods specific to
        this phase of its life:
    </p>
    <ol>
        <li>
            <code>
                updateViewConstraints
            </code>
            is called every time the layout changes, like when the window is resized.
        </li>
        <li>
            <code>
                viewWillLayout
            </code>
            is called before the
            <code>
                layout
            </code>
            method of a view controller’s view is called. For example, you can use
            this method to adjust constraints.
        </li>
        <li>
            <code>
                viewDidLayout
            </code>
            is called after
            <code>
                layout
            </code>
            is called.
        </li>
    </ol>
    <h3>
        Termination
    </h3>
    <p>
        These are the counterpart methods to creation:
    </p>
    <ol>
        <li>
            <code>
                viewWillDisappear
            </code>
            is called before the view disappears. Here you can stop your fancy animations
            you started in
            <code>
                viewDidAppear
            </code>
            .
        </li>
        <li>
            <code>
                viewDidDisappear
            </code>
            is called after the view is no longer on the screen. Here you can discard&nbsp;everything
            you no longer need. For example, you could invalidate a timer you used
            to upate your data model on a periodic time base.
        </li>
    </ol>
    <p>
        In all these methods, you should call the&nbsp;
        <em>
            super
        </em>
        implementation at some point.
    </p>
    <h3>
        Life cycle in practice
    </h3>
    <p>
        Now that you know the most important things about a view controller’s
        life cycle, it’s time for a short test!
    </p>
    <p>
        Question: Every time
        <em>
            OverviewController’s
        </em>
        view appears, you want to update the UI to take into account that a user
        selected a product when the Details tab was selected. Which method would
        be a good fit?
        <br>
    </p>
    <div class="easySpoilerWrapper" style="">
        <table class="easySpoilerTable" border="0" style="text-align:center;"
        align="center" bgcolor="FFFFFF">
            <tbody>
                <tr style="white-space:normal;">
                    <th class="easySpoilerTitleA" style="white-space:normal;font-weight:normal;text-align:left;vertical-align:middle;font-size:120%;color:#000000;">
                        Solution Inside
                    </th>
                    <th class="easySpoilerTitleB" style="text-align:right;vertical-align:middle;font-size:100%; white-space:nowrap;">
                        <a href="" onclick="wpSpoilerSelect(&quot;spoilerDiv3a5b8001&quot;); return false;"
                        class="easySpoilerButtonOther" style="font-size:100%;color:#000000;background-color:#fcfcfc;background-image:none;border: 1px inset;border-style:solid;border-color:#cccccc; margin: 3px 0px 3px; padding: 4px; "
                        align="right" sl-processed="1">
                            Select
                        </a>
                        <a href="" onclick="wpSpoilerToggle(&quot;spoilerDiv3a5b8001&quot;,true,&quot;Show&quot;,&quot;Hide&quot;,&quot;fast&quot;,false); return false;"
                        id="spoilerDiv3a5b8001_action" class="easySpoilerButton" value="Show" align="right"
                        style="font-size:100%;color:#000000;background-color:#fcfcfc;background-image:none;border: 1px inset;border-style:solid;border-color:#cccccc; margin: 3px 0px 3px 5px; padding: 4px;"
                        sl-processed="1">
                            Show
                        </a>
                    </th>
                </tr>
                <tr>
                    <td class="easySpoilerRow" colspan="2" style="">
                        <div id="spoilerDiv3a5b8001" class="easySpoilerSpoils" style="display:none; white-space:wrap; overflow:auto; vertical-align:middle;">
                            <br>
                            There are two possible methods:
                            <code>
                                viewWillAppear
                            </code>
                            and
                            <code>
                                viewDidAppear
                            </code>
                            . The best solution is to use
                            <code>
                                viewWillAppear
                            </code>
                            so that the user sees the updated UI at the moment the view appears. Using
                            <code>
                                viewDidAppear
                            </code>
                            means that a user would see the UI appear first showing old data before
                            updating.
                            <br>
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
    </p>
    <p>
        Open
        <em>
            OverviewController.swift
        </em>
        and add this code inside the class implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1538443">
                    <td class="code" id="p153844code3">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #B833A1;">
                                override
                            </span>
                            <span style="color: #B833A1;">
                                func
                            </span>
                            viewWillAppear
                            <span style="color: black;">
                                (
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: black;">
                                {
                            </span>
                            <span style="color: #B833A1;">
                                super
                            </span>
                            .
                            <span style="color: #508187;">
                                viewWillAppear
                            </span>
                            <span style="color: black;">
                                (
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            updateUI
                            <span style="color: black;">
                                (
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This overrides the
        <code>
            viewWillAppear
        </code>
        to update the user interface before the view becomes visible.
    </p>
    <p>
        The number formatter currently uses default values, which doesn’t fit
        your needs. You’ll configure it to format numbers as currency values; since
        you only need to do this once, a good place is the method
        <code>
            viewDidLoad
        </code>
        .
    </p>
    <p>
        In
        <code>
            OverviewController
        </code>
        add this code inside&nbsp;
        <code>
            viewDidLoad
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1538444">
                    <td class="code" id="p153844code4">
                        <pre class="swift" style="font-family:monospace;">
                            numberFormatter.
                            <span style="color: #508187;">
                                numberStyle
                            </span>
                            = .
                            <span style="color: #508187;">
                                currency
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        For the next step, the main view controller needs to react on product
        selection and then inform the
        <code>
            OverviewController
        </code>
        about this change. The best place for this is in the
        <em>
            ViewController
        </em>
        class, because this controller owns the pop-up button. Open
        <em>
            ViewController.swift
        </em>
        and add these properties inside the
        <em>
            ViewController
        </em>
        class implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1538445">
                    <td class="code" id="p153844code5">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #B833A1;">
                                private
                            </span>
                            <span style="color: #B833A1;">
                                var
                            </span>
                            products =
                            <span style="color: black;">
                                [
                            </span>
                            Product
                            <span style="color: black;">
                                ]
                            </span>
                            <span style="color: black;">
                                (
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: #B833A1;">
                                var
                            </span>
                            selectedProduct
                            <span style="color: black;">
                                :
                            </span>
                            Product?
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The first property,
        <code>
            products
        </code>
        , is an array used to keep a reference to all the products. The second,
        <code>
            selectedProduct
        </code>
        , holds the product selected in the pop-up button.
    </p>
    <p>
        Find
        <code>
            viewDidLoad
        </code>
        and add the following code inside:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1538446">
                    <td class="code" id="p153844code6">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #B833A1;">
                                if
                            </span>
                            <span style="color: #B833A1;">
                                let
                            </span>
                            filePath = Bundle.
                            <span style="color: #508187;">
                                main
                            </span>
                            .
                            <span style="color: #508187;">
                                path
                            </span>
                            <span style="color: black;">
                                (
                            </span>
                            forResource
                            <span style="color: black;">
                                :
                            </span>
                            <span style="color: #C41A16;">
                                "Products"
                            </span>
                            <span style="color: black;">
                                ,
                            </span>
                            ofType
                            <span style="color: black;">
                                :
                            </span>
                            <span style="color: #C41A16;">
                                "plist"
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: black;">
                                {
                            </span>
                            products = Product.
                            <span style="color: #508187;">
                                productsList
                            </span>
                            <span style="color: black;">
                                (
                            </span>
                            filePath
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This loads the array of products from the plist file using the
        <code>
            Product
        </code>
        class added at the beginning of the tutorial, and keeps it in the
        <code>
            products
        </code>
        property. Now you can use this array to populate the pop-up button.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        , select
        <em>
            View Controller Scene
        </em>
        , and switch to the
        <em>
            Assistant Editor
        </em>
        . Make sure
        <em>
            ViewController.swift
        </em>
        is selected, and
        <em>
            Control-drag
        </em>
        from the pop-up button to
        <em>
            ViewController.swift
        </em>
        to create an outlet named
        <em>
            productsButton
        </em>
        . Make sure the type is
        <code>
            NSPopUpButton
        </code>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/PopupOutlet.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/PopupOutlet-480x117.png"
            alt="" width="480" height="117" class="aligncenter size-medium wp-image-155694"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/PopupOutlet-480x117.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/02/PopupOutlet-650x158.png 650w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Return to
        <em>
            ViewController.swift
        </em>
        and add the following code to the end of
        <code>
            viewDidLoad
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1538447">
                    <td class="code" id="p153844code7">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #008312;">
                                //1
                            </span>
                            productsButton.
                            <span style="color: #508187;">
                                removeAllItems
                            </span>
                            <span style="color: black;">
                                (
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: #008312;">
                                //2
                            </span>
                            <span style="color: #B833A1;">
                                for
                            </span>
                            product
                            <span style="color: #B833A1;">
                                in
                            </span>
                            products
                            <span style="color: black;">
                                {
                            </span>
                            productsButton.
                            <span style="color: #508187;">
                                addItem
                            </span>
                            <span style="color: black;">
                                (
                            </span>
                            withTitle
                            <span style="color: black;">
                                :
                            </span>
                            product.
                            <span style="color: #508187;">
                                title
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                            <span style="color: #008312;">
                                //3
                            </span>
                            selectedProduct = products
                            <span style="color: black;">
                                [
                            </span>
                            <span style="color: #1C00CF;">
                                0
                            </span>
                            <span style="color: black;">
                                ]
                            </span>
                            productsButton.
                            <span style="color: #508187;">
                                selectItem
                            </span>
                            <span style="color: black;">
                                (
                            </span>
                            at
                            <span style="color: black;">
                                :
                            </span>
                            <span style="color: #1C00CF;">
                                0
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This piece of code does the following:
    </p>
    <ol>
        <li>
            It removes all items in the pop-up button, getting rid of the Item1 and
            Item2 entries.
        </li>
        <li>
            It adds an item for every product, showing its title.
        </li>
        <li>
            It selects the first product and the first item of the pop-up button.
            This makes sure that everything is consistent.
        </li>
    </ol>
    <p>
        The final piece in this puzzle&nbsp;is reacting to the pop-up button selection
        changes. Find
        <code>
            valueChanged
        </code>
        and add the following lines:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1538448">
                    <td class="code" id="p153844code8">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #B833A1;">
                                if
                            </span>
                            <span style="color: #B833A1;">
                                let
                            </span>
                            bookTitle = sender.
                            <span style="color: #508187;">
                                selectedItem
                            </span>
                            ?.
                            <span style="color: #508187;">
                                title
                            </span>
                            <span style="color: black;">
                                ,
                            </span>
                            <span style="color: #B833A1;">
                                let
                            </span>
                            index = products.
                            <span style="color: #508187;">
                                index
                            </span>
                            <span style="color: black;">
                                (
                            </span>
                            <span style="color: #B833A1;">
                                where
                            </span>
                            <span style="color: black;">
                                :
                            </span>
                            <span style="color: black;">
                                {
                            </span>
                            $
                            <span style="color: #1C00CF;">
                                0
                            </span>
                            .
                            <span style="color: #508187;">
                                title
                            </span>
                            <span style="color: black;">
                                ==
                            </span>
                            bookTitle
                            <span style="color: black;">
                                }
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: black;">
                                {
                            </span>
                            selectedProduct = products
                            <span style="color: black;">
                                [
                            </span>
                            index
                            <span style="color: black;">
                                ]
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This code tries to get the selected book title and searches in the products
        for the index of the title. With this index, it sets
        <code>
            selectedProduct
        </code>
        to the correct product.
    </p>
    <p>
        Now you only need to inform
        <code>
            OverviewController
        </code>
        &nbsp;when the selected product&nbsp;changes. For this you need a reference
        to the
        <code>
            OverviewController
        </code>
        . You can get a reference within code, but first you have to add another
        property to
        <em>
            ViewController.swift
        </em>
        to hold that reference. Add the following code inside the
        <code>
            ViewController
        </code>
        implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1538449">
                    <td class="code" id="p153844code9">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #B833A1;">
                                private
                            </span>
                            <span style="color: #B833A1;">
                                var
                            </span>
                            overviewViewController
                            <span style="color: black;">
                                :
                            </span>
                            OverviewController?
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        You can get the instance of
        <code>
            OverviewController
        </code>
        inside
        <code>
            prepare(for:sender:)
        </code>
        , which is called by the system when the view controllers are embedded
        in the container view. Add the following method to the
        <code>
            ViewController
        </code>
        implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15384410">
                    <td class="code" id="p153844code10">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #B833A1;">
                                override
                            </span>
                            <span style="color: #B833A1;">
                                func
                            </span>
                            prepare
                            <span style="color: black;">
                                (
                            </span>
                            <span style="color: #B833A1;">
                                for
                            </span>
                            segue
                            <span style="color: black;">
                                :
                            </span>
                            <span style="color: #6F41A7;">
                                NSStoryboardSegue
                            </span>
                            <span style="color: black;">
                                ,
                            </span>
                            sender
                            <span style="color: black;">
                                :
                            </span>
                            <span style="color: #6F41A7;">
                                Any
                            </span>
                            ?
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: black;">
                                {
                            </span>
                            guard
                            <span style="color: #B833A1;">
                                let
                            </span>
                            tabViewController = segue.
                            <span style="color: #508187;">
                                destinationController
                            </span>
                            <span style="color: #B833A1;">
                                as
                            </span>
                            ?
                            <span style="color: #6F41A7;">
                                NSTabViewController
                            </span>
                            <span style="color: #B833A1;">
                                else
                            </span>
                            <span style="color: black;">
                                {
                            </span>
                            <span style="color: #B833A1;">
                                return
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                            &nbsp;
                            <span style="color: #B833A1;">
                                for
                            </span>
                            controller
                            <span style="color: #B833A1;">
                                in
                            </span>
                            tabViewController.
                            <span style="color: #508187;">
                                childViewControllers
                            </span>
                            <span style="color: black;">
                                {
                            </span>
                            &nbsp;
                            <span style="color: #B833A1;">
                                if
                            </span>
                            <span style="color: #B833A1;">
                                let
                            </span>
                            controller = controller
                            <span style="color: #B833A1;">
                                as
                            </span>
                            ? OverviewController
                            <span style="color: black;">
                                {
                            </span>
                            overviewViewController = controller overviewViewController?.
                            <span style="color: #508187;">
                                selectedProduct
                            </span>
                            = selectedProduct
                            <span style="color: black;">
                                }
                            </span>
                            <span style="color: #008312;">
                                // More later
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This code does the following:
    </p>
    <ol>
        <li>
            Gets a reference to the Tab View controller if possible.
        </li>
        <li>
            Iterates over all its child view controllers.
        </li>
        <li>
            Checks if the current child view controller is an instance of
            <code>
                OverviewController
            </code>
            , and if it is, sets its
            <code>
                selectedProduct
            </code>
            property.
        </li>
    </ol>
    <p>
        Now add the following line in the method
        <code>
            valueChanged
        </code>
        , inside the
        <em>
            if let
        </em>
        block.
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15384411">
                    <td class="code" id="p153844code11">
                        <pre class="swift" style="font-family:monospace;">
                            overviewViewController?.
                            <span style="color: #508187;">
                                selectedProduct
                            </span>
                            = selectedProduct
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run to see how the UI updates when you select a different product.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/OverviewRun.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/OverviewRun-480x246.png"
            alt="" width="480" height="246" class="aligncenter size-medium wp-image-155695"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/OverviewRun-480x246.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/02/OverviewRun-650x333.png 650w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <h2>
        Detail View Controller
    </h2>
    <p>
        Now you will create a view controller class for the Details tab.
    </p>
    <p>
        Go to
        <em>
            File/New/File…
        </em>
        , choose
        <em>
            macOS/Source/Cocoa Class
        </em>
        , and click
        <em>
            Next
        </em>
        . Name the class
        <em>
            DetailViewController
        </em>
        , make it a subclass of
        <em>
            NSViewController
        </em>
        , and make sure
        <em>
            Also Create XIB for user interface
        </em>
        is not selected. Click
        <em>
            Next
        </em>
        and save.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/create-detailviewcontroller.png"
        sl-processed="1">
            <img class="aligncenter wp-image-113634 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/09/create-detailviewcontroller-455x320.png"
            alt="create-detailviewcontroller" width="455" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/create-detailviewcontroller-455x320.png 455w, https://koenig-media.raywenderlich.com/uploads/2015/09/create-detailviewcontroller-700x492.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/create-detailviewcontroller.png 715w"
            sizes="(max-width: 455px) 100vw, 455px">
        </a>
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and select
        <em>
            Details Scene
        </em>
        . In the
        <em>
            Identity Inspector
        </em>
        change the class to
        <code>
            DetailViewController
        </code>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-vcname.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113636" src="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-vcname.png"
            alt="detail-vcname" width="258" height="321" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-vcname.png 258w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail-vcname-257x320.png 257w"
            sizes="(max-width: 258px) 100vw, 258px">
        </a>
    </p>
    <p>
        Add an
        <code>
            image view
        </code>
        to the detail view. Select it and click on the
        <em>
            Add New Constraints
        </em>
        button to create its constraints. Set
        <em>
            width
        </em>
        and
        <em>
            height
        </em>
        constraints to a value of
        <em>
            180
        </em>
        , and a
        <em>
            top
        </em>
        constraint to the
        <em>
            standard
        </em>
        &nbsp;value. As you did with the
        <em>
            OverviewController
        </em>
        , give it an image to make it easier to see.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/PinDetailImageView.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/PinDetailImageView-430x320.png"
            alt="" width="430" height="320" class="aligncenter size-medium wp-image-155696"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/PinDetailImageView-430x320.png 430w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinDetailImageView-650x484.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinDetailImageView.png 1278w"
            sizes="(max-width: 430px) 100vw, 430px">
        </a>
    </p>
    <p>
        Click on the
        <em>
            Align
        </em>
        button in the bottom bar and add a constraint to center the view
        <em>
            Horizontally in the Container
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/AlignImageView.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/AlignImageView-421x320.png"
            alt="" width="421" height="320" class="aligncenter size-medium wp-image-155697"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/AlignImageView-421x320.png 421w, https://koenig-media.raywenderlich.com/uploads/2017/02/AlignImageView-650x493.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/AlignImageView.png 1246w"
            sizes="(max-width: 421px) 100vw, 421px">
        </a>
    </p>
    <p>
        Add a label below the image view. Change the font to bold and the size
        to 19, then click on the
        <em>
            Add New Constraints
        </em>
        button to add constraints for
        <em>
            top
        </em>
        ,
        <em>
            leading
        </em>
        , and
        <em>
            trailing
        </em>
        , using the
        <em>
            standard
        </em>
        values.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/PinDetailTitleLabel.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/PinDetailTitleLabel-434x320.png"
            alt="" width="434" height="320" class="aligncenter size-medium wp-image-155698"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/PinDetailTitleLabel-434x320.png 434w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinDetailTitleLabel-650x480.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinDetailTitleLabel.png 1290w"
            sizes="(max-width: 434px) 100vw, 434px">
        </a>
    </p>
    <p>
        Add another label below the previous one. Select it, and click on the
        <em>
            Add New Constraints
        </em>
        button first to add constraints for
        <em>
            top
        </em>
        ,
        <em>
            leading
        </em>
        and
        <em>
            trailing
        </em>
        , using
        <em>
            standard
        </em>
        &nbsp;values.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/PinDetailBottomLabel.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/PinDetailBottomLabel-432x320.png"
            alt="" width="432" height="320" class="aligncenter size-medium wp-image-155699"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/PinDetailBottomLabel-432x320.png 432w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinDetailBottomLabel-650x481.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinDetailBottomLabel.png 1272w"
            sizes="(max-width: 432px) 100vw, 432px">
        </a>
    </p>
    <p>
        Make the view taller, then drag a
        <em>
            Box
        </em>
        under the last label. Select it and add constraints for
        <em>
            top
        </em>
        ,
        <em>
            leading
        </em>
        ,
        <em>
            trailing
        </em>
        and
        <em>
            bottom
        </em>
        , using
        <em>
            standard
        </em>
        values.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/PinBox.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/PinBox-432x320.png"
            alt="" width="432" height="320" class="aligncenter size-medium wp-image-155700"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/PinBox-432x320.png 432w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinBox-650x482.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/02/PinBox.png 1274w"
            sizes="(max-width: 432px) 100vw, 432px">
        </a>
    </p>
    <p>
        Open the
        <em>
            Attributes Inspector
        </em>
        and change the box font to
        <em>
            System Bold
        </em>
        and the size to
        <em>
            14
        </em>
        . Change the title to “Who is this Book For?”.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/BoxAttributes2.png"
        alt="" width="516" height="338" class="aligncenter size-full wp-image-155931"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/BoxAttributes2.png 516w, https://koenig-media.raywenderlich.com/uploads/2017/02/BoxAttributes2-480x314.png 480w"
        sizes="(max-width: 516px) 100vw, 516px">
    </p>
    <p>
        An
        <code>
            NSBox
        </code>
        is a nice way to group related UI elements and to them a name you can
        see in Xcode’s
        <em>
            Document Outline
        </em>
        .
    </p>
    <p>
        To complete the UI, drag a label inside the content area of the
        <code>
            NSBox
        </code>
        . Select the label and click on the
        <em>
            Add New Constraints
        </em>
        button to add constraints for
        <em>
            top
        </em>
        ,
        <em>
            leading
        </em>
        ,
        <em>
            trailing
        </em>
        , and
        <em>
            bottom
        </em>
        , all using the
        <em>
            standard
        </em>
        value.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/BoxLabel.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/BoxLabel-364x320.png"
            alt="" width="364" height="320" class="aligncenter size-medium wp-image-155702"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/BoxLabel-364x320.png 364w, https://koenig-media.raywenderlich.com/uploads/2017/02/BoxLabel-569x500.png 569w, https://koenig-media.raywenderlich.com/uploads/2017/02/BoxLabel.png 1232w"
            sizes="(max-width: 364px) 100vw, 364px">
        </a>
    </p>
    <p>
        After updating the frames, the UI should look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/DetailFinished.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/DetailFinished-374x320.png"
            alt="" width="374" height="320" class="aligncenter size-medium wp-image-155703"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/DetailFinished-374x320.png 374w, https://koenig-media.raywenderlich.com/uploads/2017/02/DetailFinished-585x500.png 585w, https://koenig-media.raywenderlich.com/uploads/2017/02/DetailFinished.png 924w"
            sizes="(max-width: 374px) 100vw, 374px">
        </a>
    </p>
    <p>
        To create the outlets for those controls, open the
        <em>
            Assistant Editor
        </em>
        and make sure that
        <em>
            DetailViewController.swift
        </em>
        is open. Add four IBOutlets, giving them the following names:
    </p>
    <ol>
        <li>
            <code>
                productImageView
            </code>
            for the NSImageView.
        </li>
        <li>
            <code>
                titleLabel
            </code>
            for the label with the bold font.
        </li>
        <li>
            <code>
                descriptionLabel
            </code>
            for the label below.
        </li>
        <li>
            <code>
                audienceLabel
            </code>
            for the label in the NSBox.
        </li>
    </ol>
    <p>
        With the outlets in place, add the implementation to show the product
        detail. Add the following code to
        <code>
            DetailViewController
        </code>
        class implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15384412">
                    <td class="code" id="p153844code12">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #008312;">
                                // 1
                            </span>
                            <span style="color: #B833A1;">
                                var
                            </span>
                            selectedProduct
                            <span style="color: black;">
                                :
                            </span>
                            Product?
                            <span style="color: black;">
                                {
                            </span>
                            <span style="color: #B833A1;">
                                didSet
                            </span>
                            <span style="color: black;">
                                {
                            </span>
                            updateUI
                            <span style="color: black;">
                                (
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                            <span style="color: #008312;">
                                // 2
                            </span>
                            <span style="color: #B833A1;">
                                override
                            </span>
                            <span style="color: #B833A1;">
                                func
                            </span>
                            viewWillAppear
                            <span style="color: black;">
                                (
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: black;">
                                {
                            </span>
                            <span style="color: #B833A1;">
                                super
                            </span>
                            .
                            <span style="color: #508187;">
                                viewWillAppear
                            </span>
                            <span style="color: black;">
                                (
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            updateUI
                            <span style="color: black;">
                                (
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                            <span style="color: #008312;">
                                // 3
                            </span>
                            <span style="color: #B833A1;">
                                private
                            </span>
                            <span style="color: #B833A1;">
                                func
                            </span>
                            updateUI
                            <span style="color: black;">
                                (
                            </span>
                            <span style="color: black;">
                                )
                            </span>
                            <span style="color: black;">
                                {
                            </span>
                            <span style="color: #B833A1;">
                                if
                            </span>
                            isViewLoaded
                            <span style="color: black;">
                                {
                            </span>
                            <span style="color: #B833A1;">
                                if
                            </span>
                            <span style="color: #B833A1;">
                                let
                            </span>
                            product = selectedProduct
                            <span style="color: black;">
                                {
                            </span>
                            productImageView.
                            <span style="color: #508187;">
                                image
                            </span>
                            = product.
                            <span style="color: #508187;">
                                image
                            </span>
                            titleLabel.
                            <span style="color: #508187;">
                                stringValue
                            </span>
                            = product.
                            <span style="color: #508187;">
                                title
                            </span>
                            descriptionLabel.
                            <span style="color: #508187;">
                                stringValue
                            </span>
                            = product.
                            <span style="color: #508187;">
                                descriptionText
                            </span>
                            audienceLabel.
                            <span style="color: #508187;">
                                stringValue
                            </span>
                            = product.
                            <span style="color: #508187;">
                                audience
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                            <span style="color: black;">
                                }
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        You’re probably familiar with this code already, because it’s very similar
        to the Overview view controller implementation. This code:
    </p>
    <ol>
        <li>
            Defines a
            <code>
                selectedProduct
            </code>
            property and updates the UI whenever it changes.
        </li>
        <li>
            Forces a UI update whenever the view appears (when the detail view tab
            is selected).
        </li>
        <li>
            Sets the product information (using
            <code>
                updateUI
            </code>
            ) in the labels and image view using the appropriate outlets.
        </li>
    </ol>
    <p>
        When the product selection changes, you need to change the selected product
        in the detail view controller so that it updates the UI. Open
        <em>
            ViewController.swift
        </em>
        and add a property to hold a reference to the the detail view controller.
        Just below the
        <code>
            overviewViewController
        </code>
        property, add the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15384413">
                    <td class="code" id="p153844code13">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #B833A1;">
                                private
                            </span>
                            <span style="color: #B833A1;">
                                var
                            </span>
                            detailViewController
                            <span style="color: black;">
                                :
                            </span>
                            DetailViewController?
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Find
        <code>
            valueChanged
        </code>
        and add the following inside:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15384414">
                    <td class="code" id="p153844code14">
                        <pre class="swift" style="font-family:monospace;">
                            detailViewController?.
                            <span style="color: #508187;">
                                selectedProduct
                            </span>
                            = selectedProduct
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This updates the selected product property of the view controller when
        the pop-up selection changes.
    </p>
    <p>
        The last change is inside
        <code>
            prepare(for:sender:)
        </code>
        . Find the comment
        <code>
            // More later
        </code>
        and replace with the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15384415">
                    <td class="code" id="p153844code15">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #B833A1;">
                                else
                            </span>
                            <span style="color: #B833A1;">
                                if
                            </span>
                            <span style="color: #B833A1;">
                                let
                            </span>
                            controller = controller
                            <span style="color: #B833A1;">
                                as
                            </span>
                            ? DetailViewController
                            <span style="color: black;">
                                {
                            </span>
                            detailViewController = controller detailViewController?.
                            <span style="color: #508187;">
                                selectedProduct
                            </span>
                            = selectedProduct
                            <span style="color: black;">
                                }
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
            selectedProduct
        </code>
        when the detail view is embedded.
    </p>
    <p>
        Build and run, and enjoy your finished application!
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/FinalRun.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/FinalRun-480x257.png"
            alt="" width="480" height="257" class="aligncenter size-medium wp-image-155704"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/FinalRun-480x257.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/02/FinalRun-650x348.png 650w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <h2>
        Where to Go From Here
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
        You can download the final project
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/RWStore_Final2.zip"
        sl-processed="1">
            here
        </a>
        .
    </p>
    <p>
        In this macOS view controller tutorial you’ve learned the following:
    </p>
    <ul>
        <li>
            What a view controller is and how it compares to a window controller.
        </li>
        <li>
            How to create a custom view controller subclass.
        </li>
        <li>
            How to connect elements in your view to a view controller.
        </li>
        <li>
            How to manipulate the view from the view controller.
        </li>
        <li>
            The lifecycle of&nbsp;a view controller, and how to hook into the different
            events.
        </li>
    </ul>
    <p>
        In addition to the functionality you’ve added to your custom view controller
        subclasses, there are many built-in subclasses provided for you. To see
        what built-in view controllers are available, take a look at the
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/NSViewController_Class/index.html#//apple_ref/swift/cl/c:objc(cs)NSViewController"
        target="_blank" sl-processed="1">
            documentation
        </a>
        .
    </p>
    <p>
        If you’ve not already read it, you should take a look at Gabriel Miro’s
        excellent
        <a href="http://www.raywenderlich.com/111947/windows-and-window-controllers-in-os-x-tutorial"
        sl-processed="1">
            tutorial on windows and window controllers
        </a>
        .
    </p>
    <p>
        View controllers are one of the most powerful and useful aspects of architecting
        an macOS app, and there’s plenty more to learn. However, you’re now equipped
        with the knowledge to go out there and start playing around building apps
        — which you should do now!
    </p>
</div>