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
        运行app。你应会看到你的应用的主窗口。
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
        运行app
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
        返回
        <em>
            Main.storyboard
        </em>
        并选择
        <em>
            Overview Scene
        </em>
        。单击view上的蓝色的圈，并将右侧的
        <em>
            Identity Inspector
        </em>
        中的class更改为
        <em>
            OverviewController
        </em>
        。
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
        拖拽三个
        <em>
            label
        </em>
        到
        <em>
            OverviewController
        </em>
        的view上。将这些label放到这个view顶部的左边，一个在另一个下面地摆放。添加一个
        <em>
            image view
        </em>
        到这个view的右上角。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            默认情况下，image view是没有边界的，要在view中找到它会有点困难。为了方便布局，你可以设置一个图片。选中image view，打开
            <em>
                Attributes Inspector
            </em>
            并在
            <em>
                Image
            </em>
            这里选择
            <em>
                2d_games
            </em>
            。这个图片在教程的代码中，在运行时，将被合适的产品图片所替换。
        </p>
    </div>
    <p>
        选择顶部的label。在
        <em>
            Attributes Inspector
        </em>
        中，改变font为System Bold及size为19。现在你需要调整label的大小，来看到全部的文本。
    </p>
    <p>
        这个view现在看起来应该是这样的：
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
        是时候使用自动布局的超能力，来让这个view看起来更好了。
    </p>
    <p>
        选择这个image view并单击底部的
        <em>
            Add New Constraints
        </em>
        按钮。使用standard value来添加top和trailing的约束，将width和height的约束的值设置为180.
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
        选择顶部的label，使用standard value来添加bottom，top，leading和trailing约束。
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
        选择下面的label，并使用standard value来添加trailing和leading约束。
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
        扩宽最后一个label，让它到达image的底部，然后使用standard value添加leading，trailing和bottom的约束。对于top约束，确保这个image被选中（以便它的顶部可以和image view对齐），然后使用standard value添加。
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
        选择这个view，并在底部的栏中单击
        <em>
            Update Frames
        </em>
        按钮。你的view现在看起来应该是这样子的：
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
        毕竟你努力工作在界面上，现在是最终的时间来查看结果了，运行项目。
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
        单击tab，并查看tab view controller是怎样展示恰当的view controller的。在没有一行代码的情况下，它已正确地运行。
    </p>
    <h2>
        添加一些代码
    </h2>
    <p>
        是时候亲自动手，添加一些代码，来在这个view上展示产品的详细信息了。为了在代码中引用这些label和image view，你需要对它们的每一项添加
        <em>
            IBOutlet
        </em>
        。
    </p>
    <p>
        首先，打开
        <em>
            Assistant Editor
        </em>
        ，确保选中
        <em>
            OverviewViewController.swift
        </em>
        。从顶部的label
        <em>
            拖拽
        </em>
        到
        <em>
            OverviewController.swift
        </em>
        并添加一个名为
        <code>
            titleLabel
        </code>
        的outlet。确定其type为
        <em>
            NSTextField
        </em>
        。
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
        对另外的两个label和image view重复相同的操作，来使用下列的名称创建剩余的outlet：
    </p>
    <ol>
        <li>
            中间的label：
            <code>
                priceLabel
            </code>
        </li>
        <li>
            底部的label：
            <code>
                descriptionLabel
            </code>
        </li>
        <li>
            image view：
            <code>
                productImageView
            </code>
        </li>
    </ol>
    <p>
        就像大多数的UI元素，label和image view是由多个子view构成的，所以，确保你选择的view是正确的。你可以查看outlet的class：对于image view，它必须是
        <em>
            NSImageView
        </em>
        ，而不是
        <em>
            NSImageCell
        </em>
        。对于label，它必须是
        <em>
            NSTextField
        </em>
        ，而不是
        <em>
            NSTextFieldCell
        </em>
        。
    </p>
    <p>
        为了在overview的tab中展示产品信息，打开
        <em>
            OverviewController.swift
        </em>
        ，并添加下列的代码到类的实现中：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #008312;">//1</span>
<span style="color: #B833A1;">let</span> numberFormatter = NumberFormatter<span style="color: black;">(</span><span style="color: black;">)</span>
<span style="color: #008312;">//2    </span>
<span style="color: #B833A1;">var</span> selectedProduct<span style="color: black;">:</span> Product? <span style="color: black;">{</span>
  <span style="color: #B833A1;">didSet</span> <span style="color: black;">{</span>
    updateUI<span style="color: black;">(</span><span style="color: black;">)</span>
  <span style="color: black;">}</span>
<span style="color: black;">}</span></pre>
    <p>
        一步一步来看代码：
    </p>
    <ol>
        <li>
            <code>
                numberFormatter
            </code>
            是一个
            <code>
                NumberFormatter
            </code>
            对象，用来展示加个的值，以货币的形式格式化。
        </li>
        <li>
            <code>
                selectedProduct
            </code>
            持有了当前选中的产品。每次当值发生变化时，
            <code>
                didSet
            </code>
            就被执行，也就是执行
            <code>
                updateUI
            </code>
            。
        </li>
    </ol>
    <p>
        现在添加
        <code>
            updateUI
        </code>
        方法到
        <em>
            OverviewController.swift
        </em>
        中。
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #B833A1;">private</span> <span style="color: #B833A1;">func</span> updateUI<span style="color: black;">(</span><span style="color: black;">)</span> <span style="color: black;">{</span>
  <span style="color: #008312;">//1</span>
  <span style="color: #B833A1;">if</span> isViewLoaded <span style="color: black;">{</span>
    <span style="color: #008312;">//2</span>
    <span style="color: #B833A1;">if</span> <span style="color: #B833A1;">let</span> product = selectedProduct <span style="color: black;">{</span>
      productImageView.<span style="color: #508187;">image</span> = product.<span style="color: #508187;">image</span>
      titleLabel.<span style="color: #508187;">stringValue</span> = product.<span style="color: #508187;">title</span>
      priceLabel.<span style="color: #508187;">stringValue</span> = numberFormatter.<span style="color: #508187;">string</span><span style="color: black;">(</span>from<span style="color: black;">:</span> product.<span style="color: #508187;">price</span><span style="color: black;">)</span> <span style="color: black;">??</span> <span style="color: #C41A16;">"n/a"</span>
      descriptionLabel.<span style="color: #508187;">stringValue</span> = product.<span style="color: #508187;">descriptionText</span>
    <span style="color: black;">}</span>
  <span style="color: black;">}</span>
<span style="color: black;">}</span></pre>
    <ol>
        <li>
            检查这个view是否已加载。
            <code>
                isViewLoaded
            </code>
            是
            <code>
                NSViewController
            </code>
            的一个property，当这个view已被加载到内存中时，它的值就变为true。当这个view被加载完毕后，访问全部的view相关的property，例如label，就都会是安全的了。
        </li>
        <li>
            Unwrap
            <code>
                selectedProduct
            </code>
            ，来查看是否这里有一个产品。之后，label和image就被更新，来展示适当的值。
        </li>
    </ol>
    <p>
        这个方法已在产品发生变化时被调用，但也需要在这个view准备要被展示时被调用。
    </p>
    <h2>
        View Controller的生命周期
    </h2>
    <p>
        由于view controller是负责管理view的，因此它会暴露让你可以hook住相应的view的事件的方法。例如当这些view要从storyboard加载到屏幕上时，或这些view将要出现在屏幕上时。这些基于事件的方法的集合，被称作
        <em>
            view controller生命周期
        </em>
        。
    </p>
    <p>
        一个view controller的生命周期被分为三个主要的部分：创建，使用期（lifetime），还有终止。每个部分都有你可以重写，以添加额外工作的方法。
    </p>
    <h3>
        创建
    </h3>
    <ol>
        <li>
            <code>
                viewDidLoad
            </code>
            会在这个view被全部加载时被调用，可以用来一次性地初始化例如，配置一个数的formatter，注册通知，或调用仅仅需要被执行一次的API。
        </li>
        <li>
            <code>
                viewWillAppear
            </code>
            会在每次view将要展示在屏幕上时被调用。在我们的应用中，它会在每次你选择Overview的tab时被调用。这是一个更新你的UI或刷新你的数据模型的好时机。
        </li>
        <li>
            <code>
                viewDidAppear
            </code>
            会在view被展示到屏幕上时被调用。在这里你可以启动一些花哨的（fancy）动画。
        </li>
    </ol>
    <h3>
        使用期
    </h3>
    <p>
        一旦创建了一个view controller，它就进入了一个可以用来处理用户交互的时期。它有三个方法针对这个时期：
    </p>
    <ol>
        <li>
            <code>
                updateViewConstraints
            </code>
            会在每次布局发生变化时被调用，例如window的大小被调整时。
        </li>
        <li>
            <code>
                viewWillLayout
            </code>
            会在view controller的view的
            <code>
                layout
            </code>
            方法被调用前调用。例如，你可以使用这个方法来调整约束。
        </li>
        <li>
            <code>
                viewDidLayout
            </code>
            会在
            <code>
                layout
            </code>
            方法被调用之后调用。
        </li>
    </ol>
    <h3>
        终止
    </h3>
    <p>
        这些是对应的方法：
    </p>
    <ol>
        <li>
            <code>
                viewWillDisappear
            </code>
            会在view消失之前被调用。在这里你可以停止你在
            <code>
                viewDidAppear
            </code>
            启动的那些花哨的动画。
        </li>
        <li>
            <code>
                viewDidDisappear
            </code>
            会在view不再在屏幕上时被调用。在这里你可以抛弃所有你不在需要的东西。例如，你可以废弃你用来周期性更新你的数据模型的定时器。
        </li>
    </ol>
    <p>
        在所有的这些方法中，你应当在某个时刻调用
        <em>
            super
        </em>
        的实现。
    </p>
    <h3>
        实践什么循环
    </h3>
    <p>
        既然你已了解了有关view controller的生命周期的最重要的事，是时候来做一个简短的测试了！
    </p>
    <p>
        问题：每次当
        Question: Every time
        <em>
            OverviewController
        </em>
        出现时，你想要更新UI，以便当Details的tab被选择时，顾及用户选择了一个产品。哪个方法会比较适合？
        <br>
    </p>
    <div class="easySpoilerWrapper" style="">
        <table class="easySpoilerTable" border="0" style="text-align:center;"
        align="center" bgcolor="FFFFFF">
            <tbody>
                <tr style="white-space:normal;">
                    <th class="easySpoilerTitleA" style="white-space:normal;font-weight:normal;text-align:left;vertical-align:middle;font-size:120%;color:#000000;">
                        解决办法
                    </th>
                </tr>
                <tr>
                    <td class="easySpoilerRow" colspan="2" style="">
                        <div id="spoilerDiv3a5b8001" class="easySpoilerSpoils" style="display:none; white-space:wrap; overflow:auto; vertical-align:middle;">
                            <br>
                            有两个可能的方法：
                            <code>
                                viewWillAppear
                            </code>
                            和
                            <code>
                                viewDidAppear
                            </code>
                            。最好的解决方案是
                            <code>
                                viewWillAppear
                            </code>
                            ，这样用户就可以在view一出现时，来更新UI了。使用
                            <code>
                                viewDidAppear
                            </code>
                            会导致一个用户将在数据更新前，首先看到UI的出现。
                            <br>
                        </div>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
    </p>
    <p>
        打开
        <em>
            OverviewController.swift
        </em>
        并添加这个代码到类的实现中：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #B833A1;">override</span> <span style="color: #B833A1;">func</span> viewWillAppear<span style="color: black;">(</span><span style="color: black;">)</span> <span style="color: black;">{</span>
  <span style="color: #B833A1;">super</span>.<span style="color: #508187;">viewWillAppear</span><span style="color: black;">(</span><span style="color: black;">)</span>
  updateUI<span style="color: black;">(</span><span style="color: black;">)</span>
<span style="color: black;">}</span></pre>
    <p>
        它覆盖了
        <code>
            viewWillAppear
        </code>
        方法，以在view可见之前更新用户的界面。
    </p>
    <p>
        数的formatter当前使用的是默认的值，这并不符合你的需求。你将配置它成为货币的值的格式；由于你只需要做一次，一个很好的地方就是在方法
        <code>
            viewDidLoad
        </code>
        中。
    </p>
    <p>
        在
        <code>
            OverviewController
        </code>
        添加下列的代码到
        <code>
            viewDidLoad
        </code>
        中：
    </p>
    <pre class="swift" style="font-family:monospace;">numberFormatter.<span style="color: #508187;">numberStyle</span> = .<span style="color: #508187;">currency</span></pre>
    <p>
        下一步，主view controller需要响应产品的选择，然后通知给
        <code>
            OverviewController
        </code>
        这个变化。这个最好的地方是在
        <em>
            ViewController
        </em>
        类中，因为这个controller控制着pop-up按钮。打开
        <em>
            ViewController.swift
        </em>
        ，并添加这些property到
        <em>
            ViewController
        </em>
        类的实现中：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #B833A1;">private</span> <span style="color: #B833A1;">var</span> products = <span style="color: black;">[</span>Product<span style="color: black;">]</span><span style="color: black;">(</span><span style="color: black;">)</span>
<span style="color: #B833A1;">var</span> selectedProduct<span style="color: black;">:</span> Product?</pre>
    <p>
        第一个property
        <code>
            products
        </code>
        ，是一个用来持有全部产品的引用的数组。第二个
        <code>
            selectedProduct
        </code>
        ，则持有了被pop-up按钮选中的产品。
    </p>
    <p>
        找到
        <code>
            viewDidLoad
        </code>
        方法，并添加下列代码到里面：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #B833A1;">if</span> <span style="color: #B833A1;">let</span> filePath = Bundle.<span style="color: #508187;">main</span>.<span style="color: #508187;">path</span><span style="color: black;">(</span>forResource<span style="color: black;">:</span> <span style="color: #C41A16;">"Products"</span><span style="color: black;">,</span> ofType<span style="color: black;">:</span> <span style="color: #C41A16;">"plist"</span><span style="color: black;">)</span> <span style="color: black;">{</span>
  products = Product.<span style="color: #508187;">productsList</span><span style="color: black;">(</span>filePath<span style="color: black;">)</span>
<span style="color: black;">}</span></pre>
    <p>
        它使用
        <code>
            Product
        </code>
        类从plist文件中加载了产品的数组（Product类是在教程一开始时被添加的），并保存到了
        <code>
            products
        </code>
        的propert中。现在你可以使用这个数组来填充pop-up按钮了。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        ，选择
        <em>
            View Controller Scene
        </em>
        ，并切换到
        <em>
            Assistant Editor
        </em>
        。确保选中
        <em>
            ViewController.swift
        </em>
        ，从pop-up按钮
        <em>
            拖拽
        </em>
        到
        <em>
            ViewController.swift
        </em>
        来创建一个名为
        <em>
            productsButton
        </em>
        的outlet。确认type为
        <code>
            NSPopUpButton
        </code>
        。
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
        返回
        <em>
            ViewController.swift
        </em>
        并添加下列的代码到
        <code>
            viewDidLoad
        </code>
        方法的末尾：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #008312;">//1</span>
productsButton.<span style="color: #508187;">removeAllItems</span><span style="color: black;">(</span><span style="color: black;">)</span>
<span style="color: #008312;">//2</span>
<span style="color: #B833A1;">for</span> product <span style="color: #B833A1;">in</span> products <span style="color: black;">{</span>
  productsButton.<span style="color: #508187;">addItem</span><span style="color: black;">(</span>withTitle<span style="color: black;">:</span> product.<span style="color: #508187;">title</span><span style="color: black;">)</span>
<span style="color: black;">}</span>
<span style="color: #008312;">//3        </span>
selectedProduct = products<span style="color: black;">[</span><span style="color: #1C00CF;">0</span><span style="color: black;">]</span>
productsButton.<span style="color: #508187;">selectItem</span><span style="color: black;">(</span>at<span style="color: black;">:</span> <span style="color: #1C00CF;">0</span><span style="color: black;">)</span></pre>
    <p>
        这些代码做了如下的事：
    </p>
    <ol>
        <li>
            移除了pop-up按钮中全部的项目，去除了Item1和Item2的记录。
        </li>
        <li>
            为每个产品添加了一个项目，展示它的标题。
        </li>
        <li>
            选择第一个产品和pop-up按钮中的第一个项目。确保了所有的事始终如一。
        </li>
    </ol>
    <p>
        问题的最后一部分，是响应pop-up按钮选择的变化。找到
        <code>
            valueChanged
        </code>
        并添加下列的行：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #B833A1;">if</span> <span style="color: #B833A1;">let</span> bookTitle = sender.<span style="color: #508187;">selectedItem</span>?.<span style="color: #508187;">title</span><span style="color: black;">,</span>
  <span style="color: #B833A1;">let</span> index = products.<span style="color: #508187;">index</span><span style="color: black;">(</span><span style="color: #B833A1;">where</span><span style="color: black;">:</span> <span style="color: black;">{</span>$<span style="color: #1C00CF;">0</span>.<span style="color: #508187;">title</span> <span style="color: black;">==</span> bookTitle<span style="color: black;">}</span><span style="color: black;">)</span> <span style="color: black;">{</span>
  selectedProduct = products<span style="color: black;">[</span>index<span style="color: black;">]</span>     
<span style="color: black;">}</span></pre>
    <p>
        这个代码尝试获取被选择的书的标题，并在产品中搜索这个标题的产品的的序号。使用这个序号，来设置
        <code>
            selectedProduct
        </code>
        为正确的产品。
    </p>
    <p>
        现在，你只需要在选择的产品发生变化时，通知
        <code>
            OverviewController
        </code>
        。为此你需要一个指向
        <code>
            OverviewController
        </code>
        的引用。你可以在代码中获取引用，但首先你必须添加另一个property到
        <em>
            ViewController.swift
        </em>
        中来持有这个引用。添加下列的代码到
        <code>
            ViewController
        </code>
        的实现中：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #B833A1;">private</span> <span style="color: #B833A1;">var</span> overviewViewController<span style="color: black;">:</span> OverviewController?</pre>
    <p>
        你可以在
        <code>
            prepare(for:sender:)
        </code>
        方法中获得
        <code>
            OverviewController
        </code>
        的实例，它会在当view controller被嵌入到container view时被调用。添加下列的方法到
        <code>
            ViewController
        </code>
        的实现中：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #B833A1;">override</span> <span style="color: #B833A1;">func</span> prepare<span style="color: black;">(</span><span style="color: #B833A1;">for</span> segue<span style="color: black;">:</span> <span style="color: #6F41A7;">NSStoryboardSegue</span><span style="color: black;">,</span> sender<span style="color: black;">:</span> <span style="color: #6F41A7;">Any</span>?<span style="color: black;">)</span> <span style="color: black;">{</span>
  guard <span style="color: #B833A1;">let</span> tabViewController = segue.<span style="color: #508187;">destinationController</span>
    <span style="color: #B833A1;">as</span>? <span style="color: #6F41A7;">NSTabViewController</span> <span style="color: #B833A1;">else</span> <span style="color: black;">{</span> <span style="color: #B833A1;">return</span> <span style="color: black;">}</span>
&nbsp;
  <span style="color: #B833A1;">for</span> controller <span style="color: #B833A1;">in</span> tabViewController.<span style="color: #508187;">childViewControllers</span> <span style="color: black;">{</span>
&nbsp;
    <span style="color: #B833A1;">if</span> <span style="color: #B833A1;">let</span> controller = controller <span style="color: #B833A1;">as</span>? OverviewController <span style="color: black;">{</span>
      overviewViewController = controller
      overviewViewController?.<span style="color: #508187;">selectedProduct</span> = selectedProduct
    <span style="color: black;">}</span>
    <span style="color: #008312;">// More later</span>
  <span style="color: black;">}</span>
<span style="color: black;">}</span></pre>
    <p>
        这个代码完成了下列的事：
    </p>
    <ol>
        <li>
            在可以做到的情况下，获取对Tab View controller的引用。
        </li>
        <li>
            遍历它全部的子view controller。
        </li>
        <li>
            检查当前的view controller是否是
            <code>
                OverviewController
            </code>
            的实例，如果是的话，设置它的
            <code>
                selectedProduct
            </code>
            property。
        </li>
    </ol>
    <p>
        现在，在
        <code>
            valueChanged
        </code>
        方法的
        <em>
            if let
        </em>
        代码块中添加下面这行代码。
    </p>
    <pre class="swift" style="font-family:monospace;">overviewViewController?.<span style="color: #508187;">selectedProduct</span> = selectedProduct</pre>
    <p>
        运行项目，查看当你选择了一个不同的产品时，UI是怎么更新的。
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
        现在你将为Details这个tab创建view controller。
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
        ，单击
        <em>
            Next
        </em>
        。将类命名为
        <em>
            DetailViewController
        </em>
        ，作为
        <em>
            NSViewController
        </em>
        的子类，取消勾选
        <em>
            Also Create XIB for user interface
        </em>
        。单击
        <em>
            Next
        </em>
        并保存。
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
        打开
        <em>
            Main.storyboard
        </em>
        并选择
        <em>
            Details Scene
        </em>
        。在
        <em>
            Identity Inspector
        </em>
        中将类改变为
        <code>
            DetailViewController
        </code>
        。
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
        添加一个
        <code>
            image view
        </code>
        到detail view上。选择它并单击
        <em>
            Add New Constraints
        </em>
        按钮来创建约束。设置
        <em>
            width
        </em>
        和
        <em>
            height
        </em>
        约束的值为
        <em>
            180
        </em>
        ，top
        <em>
            top
        </em>
        约束的值为
        <em>
            standard
        </em>
        value。正如你在
        <em>
            OverviewController
        </em>
        做的一样，给它一张图片来让它更容易被看到。
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
        单击底栏的
        <em>
            Align
        </em>
        按钮，并添加一个
        <em>
            Horizontally in the Container
        </em>
        的约束来让view居中。
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
        在image view下面添加一个label。将字体改为bold，大小为19，然后单击
        <em>
            Add New Constraints
        </em>
        按钮来使用
        <em>
            standard
        </em>
        values添加
        <em>
            top
        </em>
        ，
        <em>
            leading
        </em>
        ，和
        <em>
            trailing
        </em>
        的约束。        
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
        添加另一个label到之前的label下面。选择它，并单击
        <em>
            Add New Constraints
        </em>
        按钮来使用
        <em>
            standard
        </em>
        values添加
        <em>
            top
        </em>
        ，
        <em>
            leading
        </em>
        和
        <em>
            trailing
        </em>
        的约束。
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
        使view变得更高，然后拖拽一个
        <em>
            Box
        </em>
        到上一个label的下面。选择它，并使用
        <em>
            standard
        </em>
        value添加
        <em>
            top
        </em>
        ，
        <em>
            leading
        </em>
        ，
        <em>
            trailing
        </em>
        和
        <em>
            bottom
        </em>
        约束。
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
        打开
        <em>
            Attributes Inspector
        </em>
        并将box的字体改变为
        <em>
            System Bold
        </em>
        ，size改变为
        <em>
            14
        </em>
        。将title改变为“Who is this Book For?”。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/02/BoxAttributes2.png"
        alt="" width="516" height="338" class="aligncenter size-full wp-image-155931"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/02/BoxAttributes2.png 516w, https://koenig-media.raywenderlich.com/uploads/2017/02/BoxAttributes2-480x314.png 480w"
        sizes="(max-width: 516px) 100vw, 516px">
    </p>
    <p>
        <code>
            NSBox
        </code>
        是一个很好的组织相关的UI元素的方式，给他们一个名字，你可以在Xcode的
        <em>
            Document Outline
        </em>
        中看到它们。
    </p>
    <p>
        为了完成UI，拖拽一个label，到
        <code>
            NSBox
        </code>
        的内容中。选择这个label并单击
        <em>
            Add New Constraints
        </em>
        按钮来添加
        <em>
            top
        </em>
        ，
        <em>
            leading
        </em>
        ，
        <em>
            trailing
        </em>
        ，和
        <em>
            bottom
        </em>
        约束，全部使用
        <em>
            standard
        </em>
        value。
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
        更新frame之后，UI看起来应该像是这样：
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
        为了给那些控件创建outlet，打开
        <em>
            Assistant Editor
        </em>
        ，并确保
        <em>
            DetailViewController.swift
        </em>
        已打开。添加四个IBOutlet，为他们命名如下：
    </p>
    <ol>
        <li>
            NSImageView命名为
            <code>
                productImageView
            </code>
            。
        </li>
        <li>
            label名为
            <code>
                titleLabel
            </code>
            ，字体为粗体。
        </li>
        <li>
            下面的label名为
            <code>
                descriptionLabel
            </code>
            。
        </li>
        <li>
            NSBox中的label名为
            <code>
                audienceLabel
            </code>
            。
        </li>
    </ol>
    <p>
        通过恰当的outlet，添加实现来展示产品的细节。添加下列的代码到
        <code>
            DetailViewController
        </code>
        类的实现中：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #008312;">// 1</span>
<span style="color: #B833A1;">var</span> selectedProduct<span style="color: black;">:</span> Product? <span style="color: black;">{</span>
  <span style="color: #B833A1;">didSet</span> <span style="color: black;">{</span>
    updateUI<span style="color: black;">(</span><span style="color: black;">)</span>
  <span style="color: black;">}</span>
<span style="color: black;">}</span>
<span style="color: #008312;">// 2</span>
<span style="color: #B833A1;">override</span> <span style="color: #B833A1;">func</span> viewWillAppear<span style="color: black;">(</span><span style="color: black;">)</span> <span style="color: black;">{</span>
  <span style="color: #B833A1;">super</span>.<span style="color: #508187;">viewWillAppear</span><span style="color: black;">(</span><span style="color: black;">)</span>
  updateUI<span style="color: black;">(</span><span style="color: black;">)</span>
<span style="color: black;">}</span>
<span style="color: #008312;">// 3</span>
<span style="color: #B833A1;">private</span> <span style="color: #B833A1;">func</span> updateUI<span style="color: black;">(</span><span style="color: black;">)</span> <span style="color: black;">{</span>
  <span style="color: #B833A1;">if</span> isViewLoaded <span style="color: black;">{</span>
    <span style="color: #B833A1;">if</span> <span style="color: #B833A1;">let</span> product = selectedProduct <span style="color: black;">{</span>
      productImageView.<span style="color: #508187;">image</span> = product.<span style="color: #508187;">image</span>
      titleLabel.<span style="color: #508187;">stringValue</span> = product.<span style="color: #508187;">title</span>
      descriptionLabel.<span style="color: #508187;">stringValue</span> = product.<span style="color: #508187;">descriptionText</span>
      audienceLabel.<span style="color: #508187;">stringValue</span> = product.<span style="color: #508187;">audience</span>
    <span style="color: black;">}</span>
  <span style="color: black;">}</span>
<span style="color: black;">}</span></pre>
    <p>
        你可能早已熟悉这个代码，因为它和Overview view controller的实现非常相似。这个代码：
    </p>
    <ol>
        <li>
            定义了一个
            <code>
                selectedProduct
            </code>
            property并在它发生变化时更新UI。
        </li>
        <li>
            当view出现的时候（也就是当detail view的tab被选中时）更新UI。
        </li>
        <li>
            使用适当的outlet，来设置在label和image view上的产品信息（通过
            <code>
                updateUI
            </code>
            ）。
        </li>
    </ol>
    <p>
        当产品的选择发生变化时，你需要在detail view controller中改变选择的产品，来更新它的UI。打开
        <em>
            ViewController.swift
        </em>
        并添加一个property来持有到detail view controller的引用。在
        <code>
            overviewViewController
        </code>
        property的下方，添加下列代码：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #B833A1;">private</span> <span style="color: #B833A1;">var</span> detailViewController<span style="color: black;">:</span> DetailViewController?</pre>
    <p>
        找到
        <code>
            valueChanged
        </code>
        ，并添加下列的代码到里面：
    </p>
    <pre class="swift" style="font-family:monospace;">detailViewController?.<span style="color: #508187;">selectedProduct</span> = selectedProduct</pre>
    <p>
        这会在pop-up的选择发生变化时，更新view controller的selectedProduct的property。
    </p>
    <p>
        最后一个改变位于
        <code>
            prepare(for:sender:)
        </code>
        中。找到评论
        <code>
            // More later
        </code>
        并用下列代码将其替换：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #B833A1;">else</span> <span style="color: #B833A1;">if</span> <span style="color: #B833A1;">let</span> controller = controller <span style="color: #B833A1;">as</span>? DetailViewController <span style="color: black;">{</span>
  detailViewController = controller
  detailViewController?.<span style="color: #508187;">selectedProduct</span> = selectedProduct
<span style="color: black;">}</span></pre>
    <p>
        这会在detail view被嵌入时，更新
        <code>
            selectedProduct
        </code>
        。
    </p>
    <p>
        运行项目，并enjoy你完成的应用！
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
        从这儿去向哪里
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
        你可以在
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/RWStore_Final2.zip"
        sl-processed="1">
            这里
        </a>
        下载最终的项目。
    </p>
    <p>
        在这个macOS view controller的教程中，你学到了下面的东西：
    </p>
    <ul>
        <li>
            什么是view controller，以及它和window controller之间的比较。
        </li>
        <li>
            怎样创建一个定制的view controller的子类。
        </li>
        <li>
            怎讲将你的view中的元素，连接到view controller。
        </li>
        <li>
            怎样从view controller中操纵view。
        </li>
        <li>
            view controller的生命周期，以及怎样hook到不同的事件中。
        </li>
    </ul>
    <p>
        除了你添加到定制的view controller的子类的功能，苹果还为你提供了很多內建的子类。为了查看有哪些可用的view controller，请查看
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/NSViewController_Class/index.html#//apple_ref/swift/cl/c:objc(cs)NSViewController"
        target="_blank" sl-processed="1">
            文档
        </a>
        。
    </p>
    <p>
        如果你还没有读过它，你应该看一下Gabriel Miro的杰出的
        <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Windows%20and%20Window%20Controllers%20in%20OS%20X%20Tutorial.md"
        sl-processed="1">
            window和window controller教程
        </a>
        .
    </p>
    <p>
        View controller是构建一个macOS app的最有力和最有用的方面之一，有足够的更多的东西可以去学。然而，你已经具备了走出这里并玩转构建app的知识 - 这正是你现在应该做的！
    </p>
</div>