# OS X教程：Collection Views

#### [原文地址](https://www.raywenderlich.com/120494/collection-views-os-x-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/CollectionViews_feature-250x250.png"
        alt="CollectionViews_feature" width="250" height="250" class="alignright size-thumbnail wp-image-124870"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/CollectionViews_feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/01/CollectionViews_feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/01/CollectionViews_feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/01/CollectionViews_feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/01/CollectionViews_feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/01/CollectionViews_feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/01/CollectionViews_feature-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
        collection view对可视化布局一系列有序的数据项目，是一个非常强有力的机制。用技术术语来进行解释会非常地无聊，因此考虑类似这些app：Finder和Photos；这些app让你在一个“画廊布局”下浏览文件。
    </p>
    <p>
        在OS X 10.5发布时，
        <code>
            NSCollectionView
        </code>
        提供了一个便利的手段，那就是在一个可滚动的view上，用网格式的相同尺寸的项目，来排列一组对象。
    </p>
    <p>
        OS X 10.11，也就是El Capitan，受iOS中的
        <code>
            UICollectionView
        </code>
        启发，对El Capitan进行了一次大修改。
    </p>
    <p>
        除其它方面之外，新的
        <code>
            NSCollectionView
        </code>
        API添加了以下的支持：
    </p>
    <ul>
        <li>
            带有可选的header/footer的section
        </li>
        <li>
            可变尺寸的项目
        </li>
        <li>
            可定制的布局
        </li>
        <li>
            可重用的Cell
        </li>
    </ul>
    <p>
        在这个OS X的collection view的教程中，你将会发现用漂亮流动的界面对桌面进行布局的乐趣。你将会关闭UX在移动和桌面之间的隔阂，并通过构建
        <em>
            SlidesMagic
        </em>
        - 你自己的基于网格的图片浏览app，享受到对你的app更棒的控制。
    </p>
    <p> 
        这篇教程假定你已了解编写OS X app的基本技能。如果你是一个OS X的新手，你可以先学习一下这里的
        <a href="http://www.raywenderlich.com/category/os-x" target="_blank" title="OS X tutorials">
            OS X教程
        </a>
        然后再回来学习collection view。
    </p>
    <p>
        表演马上要开始了！所以找一个座位，准备好你自己的有关
        <code>
            NSCollectionView
        </code>
        的个人魔术表演。
    </p>
    <h2>
        在Collection View的场景之后
    </h2>
    <p>
        <code>
            NSCollectionView
        </code>
        是主要的view - 也就是魔法将会发生的舞台。它展示了可见的项目，并包含了这些关键的成分：
    </p>
    <h3>
        布局
    </h3>
    <p>
        <code>
            NSCollectionViewLayout
        </code>
        - 这个版本中的新内容，让你可以通过设置collection
        view的 
        <code>
            collectionViewLayout
        </code>
        来指定一个布局。它是一个抽象类，所有实际的布局的类都继承自它。
    </p>
    <p>
        <code>
            NSCollectionViewFlowLayout
        </code>
        - 提供了一个灵活的网格布局，对于大多数的app，你都可以达到你所期望的结果。
    </p>
    <p>
        <code>
            NSCollectionViewGridLayout
        </code>
        - 匹配
        <code>
            NSCollectionView
        </code>
        的简单的OS X 10.11前的网格布局的行为，但不支持部分和所有新的API带来的好东西。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/Layouts.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/Layouts-700x220.png"
            alt="Layouts" width="700" height="220" class="aligncenter size-large wp-image-120979"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/Layouts-700x220.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/Layouts-480x151.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/Layouts.png 894w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        <em>
            Section和
        </em>
        <code>
            NSIndexPath
        </code>
        - 可以把项目分组成section。这些项目就构成了一个section的有序列表，每个section则包含一个有序的项目列表。每个项目都被关联到一个被封装到一个包含一堆整数（section,item）的
        <code>
            NSIndexPath
        </code>
        的实例中。
        <i>
            当需求并非是将项目分组到一个个section中时，默认你仍然含有至少一个section。
        </i>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/NSIndexPath.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/NSIndexPath-700x437.png"
            alt="NSIndexPath" width="700" height="437" class="aligncenter size-large wp-image-120996"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/NSIndexPath-700x437.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/NSIndexPath-480x300.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/NSIndexPath.png 830w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <h3>
        Collection View的项目
    </h3>
    <p>
        就像很多其它的
        <em>
            Cocoa
        </em>
        框架一样，collection view的项目遵循
        <em>
            MVC
        </em>
        设计模式。
    </p>
    <p>
        <em>
            Model和View
        </em>
        - item的内容来自你的model的数据对象。每个单独的对象都从大的collection view中得到了它自己的view，进而变得可视化。这些单独的view的结构都被定义到了一个单独的nib文件中（扩展名为“.xib”）。
    </p>
    <p>
        <em>
            Controller
        </em>
        - 上面提到的nib文件是由一个
        <em>
            NSCollectionViewItem
        </em>
        的实例持有的，它是一个
        <code>
            NSViewController
        </code>
        或其子类的节点。它协调了在item和model对象中的信息流。通常，你会继承
        <code>
            NSCollectionViewItem
        </code>
        。当item并非相同的类型时，你就要为每种类型定义不同的子类和nib。
    </p>
    <h3>
        Supplementary View
    </h3>
    <p>
        为了展示在collection view中不属于任一item的额外信息，你将使用supplementary view；对于这些一些共同的实现，就是section的header和footer了。
    </p>
    <h3>
        Collection View的Data Source和Delegate
    </h3>
    <ul>
        <li>
            <code>
                NSCollectionViewDataSource
            </code>
            - 是在
            <em>
                OS X 10.11
            </em>
            引入的新API，它会使用item和supplementary填充collection view。
        </li>
        <li>
            <code>
                NSCollectionViewDelegate
            </code>
            - 处理有关拖拽，选择和高亮的事件。
        </li>
        <li>
            <code>
                NSCollectionViewDelegateFlowLayout
            </code>
            - 让你可以定制一个流式布局。
        </li>
    </ul>
    <div class="note">
        <em>
            注意：
        </em>
        ：你可以使用data source或Cocoa Binding来填充table view。本collection views的OS X教程覆盖了data source。
    </div>
    <h2>
        介绍SlidesMagic
    </h2>
    <p>
        <em>
            SlidesMagic
        </em>
        你将要构建的app是一个图片浏览器。它相当得酷，但你不要太过兴奋把你的Mac中的照片都删掉了。
    </p>
    <p>
        它会检索文件系统中的一个目录的所有图片文件，并展示它们及其名字到一个优雅的collection view上。当你想象它的时候，它其实是一种神奇的东西！完成的app看起来将会是这样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/SlidesMagicSections1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/SlidesMagicSections1-409x500.png"
            alt="SlidesMagicSections" width="409" height="500" class="aligncenter size-large wp-image-121165"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/SlidesMagicSections1-409x500.png 409w, https://koenig-media.raywenderlich.com/uploads/2015/11/SlidesMagicSections1-262x320.png 262w, https://koenig-media.raywenderlich.com/uploads/2015/11/SlidesMagicSections1.png 960w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <p>
        在
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/02/SlidesMagic-Starter.zip"
        rel="">
            这里
        </a>
        下载起始项目，并在Xcode
        <em>
            Xcode
        </em>
        中打开它。Build并运行：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/empty-app.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/empty-app-415x500.png"
            alt="empty-app" width="415" height="500" class="aligncenter size-large wp-image-122803"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/empty-app-415x500.png 415w, https://koenig-media.raywenderlich.com/uploads/2015/12/empty-app-265x320.png 265w, https://koenig-media.raywenderlich.com/uploads/2015/12/empty-app.png 1136w"
            sizes="(max-width: 415px) 100vw, 415px">
        </a>
    </p>
    <p>
        现在出现了一个空的窗口，但它包含隐藏的特性，它将会成为图片浏览器的基础。
    </p>
    <p>
        当
        <em>
            SlidesMagic
        </em>
        运行时，它会从系统的
        <em>
            Desktop Pictures
        </em>
        目录中自动地加载全部的图片。从
        <em>
            Xcode
        </em>
        的控制log中，你可以看到文件的名称。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/desktop-photos.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/desktop-photos-401x320.png"
            alt="desktop photos" width="401" height="320" class="aligncenter size-medium wp-image-122805"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/desktop-photos-401x320.png 401w, https://koenig-media.raywenderlich.com/uploads/2015/12/desktop-photos-627x500.png 627w, https://koenig-media.raywenderlich.com/uploads/2015/12/desktop-photos.png 772w"
            sizes="(max-width: 401px) 100vw, 401px">
        </a>
    </p>
    <p>
        在控制台中的这个列表是模型逻辑加载完毕的指示器。你可以通过选择
        <em>
            File \ Open Another Folder…
        </em>
        菜单来选择另一个目录。
    </p>
    <h3>
        Starter项目代码的概述
    </h3>
    <p>
        启动项目提供了并非和collocation view直接相关，但特定于
        <em>
            SlidesMagic
        </em>
        的功能。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionProjectNav.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionProjectNav.png"
            alt="CollectionProjectNav" width="254" height="395" class="aligncenter size-full wp-image-121179"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionProjectNav.png 254w, https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionProjectNav-206x320.png 206w"
            sizes="(max-width: 254px) 100vw, 254px">
        </a>
    </p>
    <h3>
        Model
    </h3>
    <ul>
        <li>
            <em>
                ImageFile.swift
            </em>
            ：封装了一个单独的图片文件
        </li>
        <li>
            <em>
                ImageDirectoryLoader.swift
            </em>
            ：用来从磁盘中加载图片的助手类
        </li>
    </ul>
    <h3>
        Controller
    </h3>
    <p>
        app有两个主要的controller：
    </p>
    <ul>
        <li>
            <em>
                WindowController.swift
            </em>
            -
            <code>
                windowDidLoad()
            </code>
            负责初始化屏幕左侧窗口的尺寸。
            <code>
                openAnotherFolder
            </code>
            方法是由
            <em>
                File \ Open Another Folder…
            </em>
            菜单项调用的，它代表一个标准的打开对话框来选择不同的目录。
        </li>
        <li>
            <em>
                ViewController.swift
            </em>
            –
            <code>
                viewDidLoad()
            </code>
            打开了桌面的图片目录作为待浏览的初始目录，而
            <code>
                loadDataForNewFolderWithUrl()
            </code>
            是通过来自
            <code>
                WindowController
            </code>
            的
            <code>
                openAnotherFolder
            </code>
            使用的。
        </li>
    </ul>
    <h2>
        创建Collection View
    </h2>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        。找到
        <em>
            Object Library
        </em>
        ，并拖拽一个
        <em>
            Collection View
        </em>
        到
        <em>
            View Controller Scene
        </em>
        的view上。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/AddCollectionView.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/AddCollectionView-700x424.png"
            alt="AddCollectionView" width="700" height="424" class="aligncenter size-large wp-image-121242"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/AddCollectionView-700x424.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/AddCollectionView-480x291.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/AddCollectionView.png 1298w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <div class="note">
        <em>
            注意
        </em>
        ：你可能会注意到
        <em>
            Interface Builder
        </em>
        添加了三个view而不是一个。那只是因为
        <em>
            Collection View
        </em>
        被嵌入到了一个
        <em>
            Scroll View
        </em>
        中（它也同时含有另一个被叫做
        <em>
            Clip View
        </em>
        的子view）。当教程告知你选择
        <em>
            Collection View
        </em>
        时，确保你选择
        <i>
            不是
        </i>
        <em>
            Scroll View
        </em>
        或
        <em>
            Clip View
        </em>
        。
    </div>
    <p>
        如果你现在build，你会看到一个错误：
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1204941">
                    <td class="code" id="p120494code1">
                        <pre class="bash" style="font-family:monospace;">
                            Main.storyboard: Unknown segue relationship: Prototype
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Along with the collection view,
        <em>
            Xcode
        </em>
        also added an
        <code>
            NSCollectionViewItem
        </code>
        , connected with a
        <em>
            Prototype
        </em>
        segue.
    </p>
    <p>
        Therein you have the cause of your build error — it’s this type of segue
        that’s causing the trouble. This is a vestige (or bug if you like…) of
        the OS X 10.10 and earlier API model that prevents you from using collection
        view items in storyboards.
    </p>
    <p>
        The fix is to delete it and reincarnate it in a separate
        <em>
            xib
        </em>
        file.
    </p>
    <p>
        Select the
        <em>
            Collection View Item
        </em>
        and press
        <em>
            Delete
        </em>
        to, well, delete it.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/deleteItem.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/deleteItem-480x228.png"
            alt="deleteItem" width="480" height="228" class="aligncenter size-medium wp-image-122807"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/deleteItem-480x228.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/deleteItem-700x332.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Now the build error is gone.
    </p>
    <p>
        Resize the
        <em>
            Bordered Scroll View
        </em>
        so it takes up the whole area of the parent view. Then, select
        <em>
            Editor \ Resolve Auto Layout Issues \ Add Missing Constraints
        </em>
        to add the
        <em>
            Auto Layout
        </em>
        constraints.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionZeroConstraints.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionZeroConstraints-700x427.png"
            alt="CollectionZeroConstraints" width="700" height="427" class="aligncenter size-large wp-image-121245"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionZeroConstraints-700x427.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionZeroConstraints-480x293.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionZeroConstraints.png 1336w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        You need to add an outlet in
        <em>
            ViewController
        </em>
        to access the collection view. Open
        <em>
            ViewController.swift
        </em>
        and add the following inside the
        <code>
            ViewController
        </code>
        class definition:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1204942">
                    <td class="code" id="p120494code2">
                        <pre class="swift" style="font-family:monospace;">
                            @IBOutlet weak var collectionView: NSCollectionView!
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        , and select the
        <em>
            View Controller
        </em>
        inside the
        <em>
            View Controller Scene
        </em>
        .
    </p>
    <p>
        Open the
        <em>
            Connections Inspector
        </em>
        and find the
        <em>
            collectionView
        </em>
        element within the
        <em>
            Outlets
        </em>
        section. Connect it to the collection view by
        <em>
            dragging
        </em>
        from the button next to it to the collection view control in the canvas.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectCollectionView.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectCollectionView-700x353.png"
            alt="ConnectCollectionView" width="700" height="353" class="aligncenter size-large wp-image-121275"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectCollectionView-700x353.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectCollectionView-480x242.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectCollectionView.png 1062w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <h3>
        Configure the Collection View Layout
    </h3>
    <p>
        You’ve got options: You can set the initial layout and some of its attributes
        in
        <em>
            Interface Builder
        </em>
        , or you can set them programmatically.
    </p>
    <p>
        For SlidesMagic, you’ll take the programmatic approach.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add the following method to
        <code>
            ViewController
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1204943">
                    <td class="code" id="p120494code3">
                        <pre class="swift" style="font-family:monospace;">
                            private func configureCollectionView() { // 1 let flowLayout = NSCollectionViewFlowLayout()
                            flowLayout.itemSize = NSSize(width: 160.0, height: 140.0) flowLayout.sectionInset
                            = NSEdgeInsets(top: 10.0, left: 20.0, bottom: 10.0, right: 20.0) flowLayout.minimumInteritemSpacing
                            = 20.0 flowLayout.minimumLineSpacing = 20.0 collectionView.collectionViewLayout
                            = flowLayout // 2 view.wantsLayer = true // 3 collectionView.layer?.backgroundColor
                            = NSColor.blackColor().CGColor }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s what you’re doing in this method:
    </p>
    <ol>
        <li>
            Creating an
            <code>
                NSCollectionViewFlowLayout
            </code>
            and setting its attributes and the
            <code>
                collectionViewLayout
            </code>
            property of the
            <code>
                NSCollectionView
            </code>
            .
        </li>
        <li>
            For optimal performance,
            <code>
                NSCollectionView
            </code>
            is designed to be layer-backed. So, you’re setting an ancestor’s
            <code>
                wantsLayer
            </code>
            property to
            <code>
                true
            </code>
            .
        </li>
        <li>
            Making an addition related to the layer that’s specific to
            <em>
                SlidesMagic
            </em>
            , setting the collection view’s background color to black.
        </li>
    </ol>
    <p>
        You need to call this method when the view is created, so add this to
        the end of
        <code>
            viewDidLoad()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1204944">
                    <td class="code" id="p120494code4">
                        <pre class="swift" style="font-family:monospace;">
                            configureCollectionView()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/BlackView.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/BlackView-262x320.png"
            alt="BlackView" width="262" height="320" class="aligncenter size-medium wp-image-121354"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/BlackView-262x320.png 262w, https://koenig-media.raywenderlich.com/uploads/2015/11/BlackView-409x500.png 409w, https://koenig-media.raywenderlich.com/uploads/2015/11/BlackView.png 960w"
            sizes="(max-width: 262px) 100vw, 262px">
        </a>
    </p>
    <p>
        At this point, you have a black background and a layout. You’ve set the
        stage for your magic show!
    </p>
    <h2>
        Loading Items in the Collection View
    </h2>
    <p>
        To load items, you need to call its
        <code>
            reloadData()
        </code>
        method, which causes the collection view to discard and redisplay any
        currently visible items.
    </p>
    <p>
        You’d typically call this method when the model changes.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add this code at the end of
        <code>
            loadDataForNewFolderWithUrl(_:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1204945">
                    <td class="code" id="p120494code5">
                        <pre class="swift" style="font-family:monospace;">
                            collectionView.reloadData()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This makes it so that selecting
        <em>
            File \ Open Another Folder…
        </em>
        calls this method. it loads a new model then calls
        <code>
            reloadData()
        </code>
        .
    </p>
    <h2>
        Creating a Collection View Item
    </h2>
    <p>
        Just because you removed
        <code>
            NSCollectionViewItem
        </code>
        from the storyboard doesn’t mean you don’t need it. :] Here’s how to bring
        it back the right way.
    </p>
    <p>
        Go to
        <em>
            File \ New \ File…
        </em>
        , select
        <em>
            OS X \ Source \ Cocoa Class
        </em>
        and click
        <em>
            Next
        </em>
        .
    </p>
    <p>
        Set the
        <em>
            Class
        </em>
        field to
        <em>
            CollectionViewItem
        </em>
        , the
        <em>
            Subclass of
        </em>
        field to
        <code>
            NSCollectionViewItem
        </code>
        , and check
        <em>
            Also create XIB for user interface
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/CreateColViewItems.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/CreateColViewItems.png"
            alt="CreateColViewItems" width="444" height="163" class="aligncenter size-full wp-image-121352">
        </a>
    </p>
    <p>
        Click
        <em>
            Next
        </em>
        , and in the save dialog, select
        <em>
            Controllers
        </em>
        from
        <em>
            Group
        </em>
        and click
        <em>
            Create
        </em>
        .
    </p>
    <p>
        Open
        <em>
            CollectionViewItem.swift
        </em>
        and replace the whole class with this:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1204946">
                    <td class="code" id="p120494code6">
                        <pre class="swift" style="font-family:monospace;">
                            class CollectionViewItem: NSCollectionViewItem { &nbsp; // 1 var imageFile:
                            ImageFile? { didSet { guard viewLoaded else { return } if let imageFile
                            = imageFile { imageView?.image = imageFile.thumbnail textField?.stringValue
                            = imageFile.fileName } else { imageView?.image = nil textField?.stringValue
                            = "" } } } &nbsp; // 2 override func viewDidLoad() { super.viewDidLoad()
                            view.wantsLayer = true view.layer?.backgroundColor = NSColor.lightGrayColor().CGColor
                            } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        In here, you:
    </p>
    <ol>
        <li>
            Define the
            <code>
                imageFile
            </code>
            property that holds the model object to be presented in this item. When
            set, its
            <code>
                didSet
            </code>
            property observer sets the content of the item’s image and label.
        </li>
        <li>
            Change the background color to the item’s view.
        </li>
    </ol>
    <h2>
        Add Controls to the View
    </h2>
    <p>
        The
        <em>
            View
        </em>
        in the nib is the root view for a subtree of controls to be displayed
        in the item. You’re going to add an image view and a label for the file
        name.
    </p>
    <p>
        Open
        <em>
            CollectionViewItem.xib
        </em>
        .
    </p>
    <p>
        Add an
        <code>
            NSImageView
        </code>
        :
    </p>
    <ol>
        <li>
            From the
            <em>
                Object Library
            </em>
            , add an
            <em>
                Image View
            </em>
            to
            <em>
                View
            </em>
            .
        </li>
        <li>
            Select and click
            <em>
                Pin
            </em>
            from the
            <em>
                Auto Layout
            </em>
            toolbar to set its constraints.
        </li>
        <li>
            Set the
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
            constraints to 0, the
            <em>
                bottom
            </em>
            to 30 and click
            <em>
                Add 4 Constraints
            </em>
            .
            <p>
                <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL1.png">
                    <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL1-700x410.png"
                    alt="ImageAL1" width="700" height="410" class="aligncenter size-large wp-image-121359"
                    srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL1-700x410.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL1-480x281.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL1.png 1449w"
                    sizes="(max-width: 700px) 100vw, 700px">
                </a>
            </p>
        </li>
        <li>
            To fix the Auto Layout issues, select
            <em>
                Editor \ Resolve Auto Layout Issues \ Update Frames
            </em>
            .
        </li>
    </ol>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL2-700x365.png"
            alt="ImageAL2" width="700" height="365" class="aligncenter size-large wp-image-121361"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL2-700x365.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL2-480x251.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL2.png 774w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Add a label:
    </p>
    <ol>
        <li>
            From the
            <em>
                Object Library
            </em>
            , add a
            <em>
                Label
            </em>
            below the
            <em>
                Image View
            </em>
            .
        </li>
        <p>
            <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/LabelInPlace.png">
                <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/LabelInPlace-700x330.png"
                alt="LabelInPlace" width="700" height="330" class="aligncenter size-large wp-image-121365"
                srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/LabelInPlace-700x330.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/LabelInPlace-480x226.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/LabelInPlace.png 757w"
                sizes="(max-width: 700px) 100vw, 700px">
            </a>
        </p>
        <li>
            Click the
            <em>
                Pin
            </em>
            button. Set the
            <em>
                top
            </em>
            ,
            <em>
                bottom
            </em>
            ,
            <em>
                trailing
            </em>
            and
            <em>
                leading
            </em>
            constraints to 0, and then click
            <em>
                Add 4 Constraints
            </em>
            .
        </li>
        <p>
            <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-20.11.30.png">
                <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-20.11.30-225x320.png"
                alt="Screen Shot 2015-12-09 at 20.11.30" width="225" height="320" class="aligncenter size-medium wp-image-122816"
                srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-20.11.30-225x320.png 225w, https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-20.11.30-351x500.png 351w, https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-20.11.30.png 562w"
                sizes="(max-width: 225px) 100vw, 225px">
            </a>
        </p>
        <li>
            Select
            <em>
                Editor \ Resolve Auto Layout Issues \ Update Frames
            </em>
            to update its position.
        </li>
    </ol>
    <p>
        Select the
        <em>
            Label
        </em>
        , and in the
        <em>
            Attributes Inspector
        </em>
        set the following attributes:
    </p>
    <ol>
        <li>
            <em>
                Alignment
            </em>
            to
            <em>
                center
            </em>
        </li>
        <li>
            <em>
                Text Color
            </em>
            to
            <em>
                white
            </em>
        </li>
        <li>
            <em>
                Line Break
            </em>
            to
            <em>
                Truncate Tail
            </em>
        </li>
    </ol>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ConfigLabel.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ConfigLabel-700x391.png"
            alt="ConfigLabel" width="700" height="391" class="aligncenter size-large wp-image-121369"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ConfigLabel-700x391.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConfigLabel-480x268.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConfigLabel.png 813w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Now you need to connect the controls to the
        <code>
            imageView
        </code>
        and the
        <code>
            textField
        </code>
        outlets:
    </p>
    <ol>
        <li>
            Select
            <em>
                File’s Owner
            </em>
            and show the
            <em>
                Connections Inspector
            </em>
            .
        </li>
        <li>
            Next,
            <em>
                drag
            </em>
            from the button next
            <em>
                imageView
            </em>
            to the
            <em>
                Image View
            </em>
            control to connect them.
        </li>
        <li>
            In the same way, connect the
            <code>
                textField
            </code>
            outlet to
            <em>
                Label
            </em>
            .
        </li>
    </ol>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/OwnerOutlets2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/OwnerOutlets2-700x287.png"
            alt="OwnerOutlets2" width="700" height="287" class="aligncenter size-large wp-image-121372"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/OwnerOutlets2-700x287.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/OwnerOutlets2-480x197.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/OwnerOutlets2.png 1032w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <h2>
        Add a Top Level CollectionViewItem to the Nib
    </h2>
    <p>
        The
        <em>
            File’s Owner
        </em>
        in the nib — of type
        <code>
            CollectionViewItem
        </code>
        — is just a placeholder. You still need to instantiate it.
    </p>
    <p>
        <code>
            CollectionView's
        </code>
        method
        <code>
            makeItemWithIdentifier(_:forIndexPath:)
        </code>
        instantiates the collection view item, and it requires the nib to contain
        a single top-level instance of either
        <code>
            NSCollectionViewItem
        </code>
        or a subclass thereof.
    </p>
    <p>
        You need to make it appear.
    </p>
    <p>
        Drag a
        <em>
            Collection View Item
        </em>
        from the
        <em>
            Object Library
        </em>
        and drop it into
        <em>
            Document Outline
        </em>
        . Select it, and in the
        <em>
            Identity Inspector
        </em>
        , set its
        <em>
            Class
        </em>
        to
        <code>
            CollectionViewItem
        </code>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/TopLevelObject.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/TopLevelObject-700x318.png"
            alt="TopLevelObject" width="700" height="318" class="aligncenter size-large wp-image-121406"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/TopLevelObject-700x318.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/TopLevelObject-480x218.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/TopLevelObject.png 1074w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <h2>
        Populate the Collection View
    </h2>
    <p>
        You need to implement the data source methods so the view knows the answers
        to these questions:
    </p>
    <ol>
        <li>
            How many sections are in the collection?
        </li>
        <li>
            How many items are in each section?
        </li>
        <li>
            Which item is associated with a specified index path?
        </li>
    </ol>
    <p>
        Meet your data source method:
        <code>
            NSCollectionViewDataSource
        </code>
        protocol.
    </p>
    <p>
        Put it into action now — open
        <em>
            ViewController.swift
        </em>
        and add the following extension at the end of the file:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1204947">
                    <td class="code" id="p120494code7">
                        <pre class="swift" style="font-family:monospace;">
                            extension ViewController : NSCollectionViewDataSource { &nbsp; // 1 func
                            numberOfSectionsInCollectionView(collectionView: NSCollectionView) -&gt;
                            Int { return imageDirectoryLoader.numberOfSections } &nbsp; // 2 func collectionView(collectionView:
                            NSCollectionView, numberOfItemsInSection section: Int) -&gt; Int { return
                            imageDirectoryLoader.numberOfItemsInSection(section) } &nbsp; // 3 func
                            collectionView(collectionView: NSCollectionView, itemForRepresentedObjectAtIndexPath
                            indexPath: NSIndexPath) -&gt; NSCollectionViewItem { &nbsp; // 4 let item
                            = collectionView.makeItemWithIdentifier("CollectionViewItem", forIndexPath:
                            indexPath) guard let collectionViewItem = item as? CollectionViewItem else
                            {return item} &nbsp; // 5 let imageFile = imageDirectoryLoader.imageFileForIndexPath(indexPath)
                            collectionViewItem.imageFile = imageFile return item } &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <ol>
        <li>
            This method provides the number of sections. When your app doesn’t support
            sections, you can omit this method because a single section will be assumed.
            When
            <em>
                SlidesMagic
            </em>
            launches, the model
            <code>
                imageDirectoryLoader
            </code>
            is set to return the value 1.
        </li>
        <li>
            This is one of two required methods for
            <code>
                NSCollectionViewDataSource
            </code>
            . Here you return the number of items in the section specified by the
            <code>
                section
            </code>
            parameter. Upon launch,
            <em>
                SlidesMagic
            </em>
            has a single section, so you set the model to return the total number
            of images in the folder.
        </li>
        <li>
            This is the second required method. It returns a collection view item
            for a given
            <code>
                indexPath
            </code>
            .
        </li>
        <li>
            The collection view’s method
            <code>
                makeItemWithIdentifier(_:forIndexPath:)
            </code>
            instantiates an item from a nib where its name equals the value of the
            <code>
                identifier
            </code>
            parameter. In this case, it’s
            <code>
                "CollectionViewItem"
            </code>
            . First, it attempts to reuse an unused item of the requested type, and
            if nothing is available it creates a new one.
        </li>
        <li>
            This code gets the model object for the given
            <code>
                NSIndexPath
            </code>
            and sets the content of the image and the label.
        </li>
    </ol>
    <div class="note">
        <em>
            Note
        </em>
        : The ability of the collection view to recycle unused collection view
        items provides a scalable solution for large collections. Items associated
        with model objects that aren’t visible are the objects that get recycled.
    </div>
    <h3>
        Set the Data Source
    </h3>
    <p>
        A collection view without data is like a magic act with no slight of hand
        — pointless and uninspiring. So, your next step is to define the data source;
        in this case it’s the view controller.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and select the collection view.
    </p>
    <p>
        Open the
        <em>
            Connections Inspector
        </em>
        and locate
        <em>
            dataSource
        </em>
        in the
        <em>
            Outlets
        </em>
        section.
        <em>
            Drag
        </em>
        from the adjacent button to the
        <em>
            View Controller
        </em>
        in
        <em>
            Document Outline View
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/SetAsDataSource.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/SetAsDataSource-700x202.png"
            alt="SetAsDataSource" width="700" height="202" class="aligncenter size-large wp-image-121329"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/SetAsDataSource-700x202.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/SetAsDataSource-480x139.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/SetAsDataSource.png 1053w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Build and run.
        <br>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/OneSectionFinal.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/OneSectionFinal-409x500.png"
            alt="OneSectionFinal" width="409" height="500" class="aligncenter size-large wp-image-121409"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/OneSectionFinal-409x500.png 409w, https://koenig-media.raywenderlich.com/uploads/2015/11/OneSectionFinal-262x320.png 262w, https://koenig-media.raywenderlich.com/uploads/2015/11/OneSectionFinal.png 960w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <p>
        Voila! It was worth all that work! Your collection view displays images
        from the
        <em>
            Desktop Pictures
        </em>
        folder!
    </p>
    <h3>
        Troubleshooting
    </h3>
    <p>
        If you don’t see images, then something went wrong. You worked through
        several steps, so you probably just missed something small.
    </p>
    <ol>
        <li>
            Are all the connections in the
            <em>
                Connections Inspector
            </em>
            set as instructed?
        </li>
        <li>
            Did you set the
            <code>
                dataSource
            </code>
            outlet?
        </li>
        <li>
            Did you use the right type for custom classes in the
            <em>
                Identity Inspector
            </em>
            .
        </li>
        <li>
            Did you add the top level
            <code>
                NSCollectionViewItem
            </code>
            object and change its type to
            <code>
                CollectionViewItem
            </code>
            ?
        </li>
        <li>
            Is the value for the
            <code>
                identifier
            </code>
            parameter in
            <code>
                makeItemWithIdentifier
            </code>
            identical to the nib name?
        </li>
    </ol>
    <h2>
        Going Multi-Section
    </h2>
    <p>
        MagicSlides is doing some serious magic now. But you’re going to improve
        it by adding sections.
    </p>
    <p>
        First, you need to add a check box at the bottom of the view so you can
        toggle between single and multi-section.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        , and in the
        <em>
            Document Outline
        </em>
        view, select the scroll view’s bottom constraint. Open the
        <em>
            Size Inspector
        </em>
        and change its
        <em>
            Constant
        </em>
        to 30.
    </p>
    <p>
        This is how you move the collection view up to make room for the check
        box.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/change-constraint.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/change-constraint-480x194.png"
            alt="change-constraint" width="480" height="194" class="aligncenter size-medium wp-image-122825"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/change-constraint-480x194.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/change-constraint-700x282.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Now, drag a
        <em>
            Check Box Button
        </em>
        from the
        <em>
            Object Library
        </em>
        into the space below the collection view. Select it, and in the
        <em>
            Attributes Inspector
        </em>
        , set its
        <em>
            Title
        </em>
        to
        <em>
            Show Sections
        </em>
        , and its
        <em>
            State
        </em>
        to
        <em>
            Off
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSections.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSections-700x425.png"
            alt="ShowSections" width="700" height="425" class="aligncenter size-large wp-image-121428"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSections-700x425.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSections-480x292.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSections.png 1180w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Then, set its
        <em>
            Auto Layout
        </em>
        constraints by selecting the
        <em>
            Editor \ Resolve Auto Layout Issues \ Add Missing Constraints
        </em>
        menu.
    </p>
    <p>
        Build and run. It should look like this at the bottom:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSectionsBottom.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSectionsBottom-700x263.png"
            alt="ShowSectionsBottom" width="700" height="263" class="aligncenter size-large wp-image-121431"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSectionsBottom-700x263.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSectionsBottom-480x180.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSectionsBottom.png 960w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Now for a little UI. When you click the box, the application needs to
        change the collection view’s appearance.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add the following method at the end of the
        <code>
            ViewController
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1204948">
                    <td class="code" id="p120494code8">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 @IBAction func showHideSections(sender: AnyObject) { // 2 let show
                            = (sender as! NSButton).state imageDirectoryLoader.singleSectionMode =
                            (show == NSOffState) imageDirectoryLoader.setupDataForUrls(nil) // 3 collectionView.reloadData()
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Section by section, here’s what you’re doing:
    </p>
    <ol>
        <li>
            Calling this method by toggling the state of the checkbox.
        </li>
        <li>
            Accordingly, retrieving the state of the checkbox and setting data model
            mode
            <code>
                singleSelectionMode
            </code>
            , and then calling the model’s
            <code>
                setupDataForUrls(_:)
            </code>
            method to rearrange the sections structure. The
            <code>
                nil
            </code>
            value passed means you skip image loading — same images, different layout.
        </li>
    </ol>
    <p>
        If you’re curious how images are distributed across sections, look up
        <code>
            sectionLengthArray
        </code>
        in
        <code>
            ImageDirectoryLoader
        </code>
        . The number of elements in this array sets the max number of sections,
        and the element values set the number of items in each section.
    </p>
    <p>
        Now, open
        <em>
            Main.storyboard
        </em>
        . In the
        <em>
            Document Outline
        </em>
        ,
        <em>
            Control-Drag
        </em>
        from the
        <em>
            Show Sections
        </em>
        control over the
        <em>
            View Controller
        </em>
        . In the black pop-up window click
        <em>
            showHideSections:
        </em>
        to connect it. You can check if the connection was set properly in the
        <em>
            Connections Inspector
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectShowSections.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectShowSections-700x247.png"
            alt="ConnectShowSections" width="700" height="247" class="aligncenter size-large wp-image-121433"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectShowSections-700x247.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectShowSections-480x170.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectShowSections.png 954w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Build and run.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/SectionsShowing.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/SectionsShowing-409x500.png"
            alt="SectionsShowing" width="409" height="500" class="aligncenter size-large wp-image-121432"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/SectionsShowing-409x500.png 409w, https://koenig-media.raywenderlich.com/uploads/2015/11/SectionsShowing-262x320.png 262w, https://koenig-media.raywenderlich.com/uploads/2015/11/SectionsShowing.png 960w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <p>
        Check
        <em>
            Show Sections
        </em>
        and watch the layout change.
    </p>
    <p>
        Because of the “black tail” in the second row, you see section 0 has seven
        images, but section 1 has five and section 2 has 10 (look at
        <code>
            sectionLengthArray
        </code>
        ). It’s not clear because the sections are rather cozy.
    </p>
    <p>
        To fix this, open
        <em>
            ViewController.swift
        </em>
        and modify the layout’s
        <code>
            sectionInset
        </code>
        property in the
        <code>
            configureCollectionView()
        </code>
        function.
    </p>
    <p>
        Replace:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1204949">
                    <td class="code" id="p120494code9">
                        <pre class="swift" style="font-family:monospace;">
                            flowLayout.sectionInset = NSEdgeInsets(top: 10.0, left: 20.0, bottom:
                            10.0, right: 20.0)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        With this:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12049410">
                    <td class="code" id="p120494code10">
                        <pre class="swift" style="font-family:monospace;">
                            flowLayout.sectionInset = NSEdgeInsets(top: 30.0, left: 20.0, bottom:
                            30.0, right: 20.0)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here you set the bottom and top section insets to 30 to provide better
        visual separation between sections.
    </p>
    <p>
        Build and run.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/SectionInsets.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/SectionInsets-409x500.png"
            alt="SectionInsets" width="409" height="500" class="aligncenter size-large wp-image-121435"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/SectionInsets-409x500.png 409w, https://koenig-media.raywenderlich.com/uploads/2015/11/SectionInsets-262x320.png 262w, https://koenig-media.raywenderlich.com/uploads/2015/11/SectionInsets.png 960w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <p>
        Check
        <em>
            Show Sections
        </em>
        , and note the additional spacing between sections.
    </p>
    <h2>
        Add Section Headers
    </h2>
    <p>
        The app is looking great so far, but more organization will make it even
        better.
    </p>
    <p>
        Another way to see section boundaries is adding a header or footer view.
        To do this, you need a custom
        <code>
            NSView
        </code>
        class and will need to implement a data source method to provide the header
        views to the table view.
    </p>
    <p>
        To create the header view, select
        <em>
            File \ New \ File…
        </em>
        . Select
        <em>
            OS X \ User Interface \ View
        </em>
        and click
        <em>
            Next
        </em>
        .
    </p>
    <p>
        Enter
        <em>
            HeaderView.xib
        </em>
        as the file name and for
        <em>
            Group
        </em>
        select
        <em>
            Resources
        </em>
        .
    </p>
    <p>
        Click
        <em>
            Create
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderView.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderView-700x297.png"
            alt="HeaderView" width="700" height="297" class="aligncenter size-large wp-image-121443"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderView-700x297.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderView-480x204.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderView.png 1067w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Open
        <em>
            HeaderView.xib
        </em>
        and select the
        <em>
            Custom View
        </em>
        . Open the
        <em>
            Size Inspector
        </em>
        and change
        <em>
            Width
        </em>
        to 500 and
        <em>
            Height
        </em>
        to 40.
    </p>
    <p>
        Drag a label from the
        <em>
            Object Library
        </em>
        to the left-hand side of
        <em>
            Custom View
        </em>
        . Open the
        <em>
            Attributes Inspector
        </em>
        and change
        <em>
            Title
        </em>
        to
        <em>
            Section Number
        </em>
        and
        <em>
            Font Size
        </em>
        to
        <em>
            16
        </em>
        .
    </p>
    <p>
        Drag a second label to the right-hand side of
        <em>
            Custom View
        </em>
        and change
        <em>
            Title
        </em>
        to
        <em>
            Images Count
        </em>
        and
        <em>
            Text Alignment
        </em>
        to
        <em>
            Right
        </em>
        .
    </p>
    <p>
        Now, select the
        <em>
            Editor \ Resolve Auto Layout Issues \ Add Missing Constraints
        </em>
        menu to add its
        <em>
            Auto Layout
        </em>
        constraints.
    </p>
    <p>
        The header view should look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderControls.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderControls-700x202.png"
            alt="HeaderControls" width="700" height="202" class="aligncenter size-large wp-image-121450"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderControls-700x202.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderControls-480x138.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderControls.png 1290w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        With the interface ready for show time, the next task is to create a custom
        view subclass for the header view.
    </p>
    <p>
        Select
        <em>
            File \ New \ File…
        </em>
        to create a new file.
    </p>
    <p>
        Choose
        <em>
            OS X \ Source \ Cocoa Class
        </em>
        and name the class
        <code>
            HeaderView
        </code>
        , and then make it a subclass of
        <code>
            NSView
        </code>
        . Click next, and for
        <em>
            Group
        </em>
        select
        <em>
            Views
        </em>
        . Click
        <em>
            Create
        </em>
        .
    </p>
    <p>
        Open
        <em>
            HeaderView.swift
        </em>
        and replace the contents of the class with the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12049411">
                    <td class="code" id="p120494code11">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 @IBOutlet weak var sectionTitle: NSTextField! @IBOutlet weak var
                            imageCount: NSTextField! &nbsp; // 2 override func drawRect(dirtyRect:
                            NSRect) { super.drawRect(dirtyRect) NSColor(calibratedWhite: 0.8 , alpha:
                            0.8).set() NSRectFillUsingOperation(dirtyRect, NSCompositingOperation.CompositeSourceOver)
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        In here, you’re:
    </p>
    <ol>
        <li>
            Setting up outlets you’ll use to connect to the labels in the nib.
        </li>
        <li>
            Drawing a gray background.
        </li>
    </ol>
    <p>
        With the framework in place, the next task is changing the nib file to
        use this new class and connecting the outlets to the labels.
    </p>
    <p>
        Open
        <em>
            HeaderView.xib
        </em>
        and select the
        <em>
            Custom View
        </em>
        . Open the
        <em>
            Identity Inspector
        </em>
        . Change the
        <em>
            Class
        </em>
        to
        <em>
            HeaderView
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-22.50.57.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-22.50.57-480x196.png"
            alt="Screen Shot 2015-12-09 at 22.50.57" width="480" height="196" class="aligncenter size-small wp-image-122895"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-22.50.57-480x196.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-22.50.57.png 520w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        In the
        <em>
            Document Outline
        </em>
        view,
        <em>
            Control-Click
        </em>
        on the
        <em>
            Header View
        </em>
        . In the black pop-up window,
        <em>
            drag
        </em>
        from
        <em>
            imageCount
        </em>
        to the
        <em>
            Images Count
        </em>
        label on the canvas to connect the outlet.
    </p>
    <p>
        Repeat the operation for the second label, dragging from
        <em>
            sectionTitle
        </em>
        to the
        <em>
            Section Number
        </em>
        label in the canvas.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectHeaderControls.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectHeaderControls-700x242.png"
            alt="ConnectHeaderControls" width="700" height="242" class="aligncenter size-large wp-image-121459"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectHeaderControls-700x242.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectHeaderControls-480x166.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectHeaderControls.png 1329w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <h3>
        Implement the Data Source and Delegate Methods
    </h3>
    <p>
        Your header view is in place and ready to go, and you need to pass the
        header views to the collection view to implement the
        <code>
            collectionView(_:viewForSupplementaryElementOfKind:atIndexPath:)
        </code>
        method.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add the following method to the
        <code>
            NSCollectionViewDataSource
        </code>
        extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12049412">
                    <td class="code" id="p120494code12">
                        <pre class="swift" style="font-family:monospace;">
                            func collectionView(collectionView: NSCollectionView, viewForSupplementaryElementOfKind
                            kind: String, atIndexPath indexPath: NSIndexPath) -&gt; NSView { // 1 let
                            view = collectionView.makeSupplementaryViewOfKind(NSCollectionElementKindSectionHeader,
                            withIdentifier: "HeaderView", forIndexPath: indexPath) as! HeaderView //
                            2 view.sectionTitle.stringValue = "Section \(indexPath.section)" let numberOfItemsInSection
                            = imageDirectoryLoader.numberOfItemsInSection(indexPath.section) view.imageCount.stringValue
                            = "\(numberOfItemsInSection) image files" return view }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The collection view calls this method when it needs the data source to
        provide a header for a section. The method:
    </p>
    <ol>
        <li>
            Calls
            <code>
                makeSupplementaryViewOfKind(_:withIdentifier:forIndexPath:)
            </code>
            to instantiate a
            <code>
                HeaderView
            </code>
            object using the nib with a name equal to
            <code>
                withIdentifier
            </code>
            .
        </li>
        <li>
            Sets the values for the labels.
        </li>
    </ol>
    <p>
        At the end of
        <em>
            ViewController.swift
        </em>
        , add this
        <code>
            NSCollectionViewDelegateFlowLayout
        </code>
        extension.
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12049413">
                    <td class="code" id="p120494code13">
                        <pre class="swift" style="font-family:monospace;">
                            extension ViewController : NSCollectionViewDelegateFlowLayout { func collectionView(collectionView:
                            NSCollectionView, layout collectionViewLayout: NSCollectionViewLayout,
                            referenceSizeForHeaderInSection section: Int) -&gt; NSSize { return imageDirectoryLoader.singleSectionMode
                            ? NSZeroSize : NSSize(width: 1000, height: 40) } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The above method, although technically optional, is a must when you use
        headers because the flow layout delegate needs to provide the size of the
        header for every section.
    </p>
    <p>
        When not implemented, the header won’t show because zero size is assumed.
        Additionally, it ignores the specified width, effectively setting it to
        the collection view’s width.
    </p>
    <p>
        In this case, the method returns a size of zero when the collection view
        is in single section mode, and it returns 40 when in multiple sections
        mode.
    </p>
    <p>
        For the collection view to use
        <code>
            NSCollectionViewDelegateFlowLayout
        </code>
        , you must connect
        <code>
            ViewController
        </code>
        to the
        <code>
            delegate
        </code>
        outlet of
        <code>
            NSCollectionView
        </code>
        .
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and select the collection view. Open the
        <em>
            Connections Inspector
        </em>
        , and locate the
        <em>
            delegate
        </em>
        in the
        <em>
            Outlets
        </em>
        section.
        <em>
            Drag
        </em>
        from the button next to it to the view controller in the
        <em>
            Document Outline
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectTheDelegate.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectTheDelegate.png"
            alt="ConnectTheDelegate" width="319" height="383" class="aligncenter size-full wp-image-121461"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectTheDelegate.png 319w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectTheDelegate-267x320.png 267w"
            sizes="(max-width: 319px) 100vw, 319px">
        </a>
    </p>
    <p>
        Build and run.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/WithHeaders.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/WithHeaders-409x500.png"
            alt="WithHeaders" width="409" height="500" class="aligncenter size-large wp-image-121462"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/WithHeaders-409x500.png 409w, https://koenig-media.raywenderlich.com/uploads/2015/11/WithHeaders-262x320.png 262w, https://koenig-media.raywenderlich.com/uploads/2015/11/WithHeaders.png 960w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <p>
        Check
        <em>
            Show Sections
        </em>
        and watch your header neatly define sections.
    </p>
    <h2>
        Selection in Collection Views
    </h2>
    <p>
        Collection views support both single and multiple selections. To show
        an item as selected, you must highlight it.
    </p>
    <p>
        Before you can do that, you need to make the collection view selectable.
        Open the
        <em>
            Main.storyboard
        </em>
        . Then, select the
        <em>
            Collection View
        </em>
        and in the
        <em>
            Attributes Inspector
        </em>
        , check
        <em>
            Selectable
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/SelectionAttributes.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/SelectionAttributes.png"
            alt="SelectionAttributes" width="316" height="374" class="aligncenter size-full wp-image-121466"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/SelectionAttributes.png 316w, https://koenig-media.raywenderlich.com/uploads/2015/11/SelectionAttributes-270x320.png 270w"
            sizes="(max-width: 316px) 100vw, 316px">
        </a>
    </p>
    <p>
        Checking
        <em>
            Selectable
        </em>
        enables single selection, meaning you can click an item to select it.
        And when you choose a different item, it deselects the previous item and
        selects item you just picked.
    </p>
    <p>
        To show an item as selected, you’ll set a white border with
        <code>
            borderWith
        </code>
        set to 5.0. Non-selected items will get no special treatment.
    </p>
    <p>
        Open
        <em>
            CollectionViewItem.swift
        </em>
        . Add the following at the end of
        <code>
            viewDidLoad()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12049414">
                    <td class="code" id="p120494code14">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 view.layer?.borderWidth = 0.0 // 2 view.layer?.borderColor = NSColor.whiteColor().CGColor
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <ol>
        <li>
            Setting
            <code>
                borderWidth
            </code>
            to
            <code>
                0.0
            </code>
            initializes the item to show not selected
        </li>
        <li>
            Sets white for the color when selected
        </li>
    </ol>
    <p>
        Add the following method at the end of
        <code>
            CollectionViewItem
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12049415">
                    <td class="code" id="p120494code15">
                        <pre class="swift" style="font-family:monospace;">
                            func setHighlight(selected: Bool) { view.layer?.borderWidth = selected
                            ? 5.0 : 0.0 }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This method is called to add or remove highlighting.
    </p>
    <p>
        When the user selects an item in the collection view, you find out via
        delegate methods. You’ll need to implement those methods, so open
        <em>
            ViewController.swift
        </em>
        and add this extension at the end of the file:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12049416">
                    <td class="code" id="p120494code16">
                        <pre class="swift" style="font-family:monospace;">
                            extension ViewController : NSCollectionViewDelegate { // 1 func collectionView(collectionView:
                            NSCollectionView, didSelectItemsAtIndexPaths indexPaths: Set&lt;NSIndexPath&gt;)
                            { // 2 guard let indexPath = indexPaths.first else { return } // 3 guard
                            let item = collectionView.itemAtIndexPath(indexPath) else { return } (item
                            as! CollectionViewItem).setHighlight(true) } &nbsp; // 4 func collectionView(collectionView:
                            NSCollectionView, didDeselectItemsAtIndexPaths indexPaths: Set&lt;NSIndexPath&gt;)
                            { guard let indexPath = indexPaths.first else { return } guard let item
                            = collectionView.itemAtIndexPath(indexPath) else { return } (item as! CollectionViewItem).setHighlight(false)
                            } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This implements the necessary
        <code>
            NSCollectionViewDelegate
        </code>
        methods. Further detail:
    </p>
    <ol>
        <li>
            When you select an item,
            <code>
                NSCollectionView
            </code>
            calls this method.
        </li>
        <li>
            Here you get the selected item — since multiple selection is disabled,
            it is always the first.
        </li>
        <li>
            This retrieves an item by its index and highlights it.
        </li>
        <li>
            The same as the previous method, but it’s called when an item is deselected.
        </li>
    </ol>
    <h3>
        What Happens During Selection Stays in Selection
    </h3>
    <p>
        When selected, an item is set in:
    </p>
    <ol>
        <li>
            The
            <code>
                selectionIndexPaths
            </code>
            property of
            <code>
                NSCollectionView
            </code>
            .
        </li>
        <li>
            The
            <code>
                selected
            </code>
            property of
            <code>
                NSCollectionViewItem
            </code>
            .
        </li>
    </ol>
    <p>
        It’s
        <i>
            critical
        </i>
        to understand that when an
        <code>
            NSCollectionViewItem
        </code>
        instance is recycled, the data set must be refreshed with the data from
        the new object. Your
        <code>
            selected
        </code>
        property of
        <code>
            NSCollectionViewItem
        </code>
        is where you ensure this happens.
    </p>
    <p>
        Accordingly, in the
        <code>
            NSCollectionViewDataSource
        </code>
        extension you need to add the following inside
        <code>
            collectionView(_:itemForRepresentedObjectAtIndexPath:)
        </code>
        method, just before the
        <code>
            return
        </code>
        statement:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12049417">
                    <td class="code" id="p120494code17">
                        <pre class="swift" style="font-family:monospace;">
                            if let selectedIndexPath = collectionView.selectionIndexPaths.first where
                            selectedIndexPath == indexPath { collectionViewItem.setHighlight(true)
                            } else { collectionViewItem.setHighlight(false) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This guarantees that selection and highlighting are in sync.
    </p>
    <p>
        Build and run.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSelection.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSelection-409x500.png"
            alt="ShowSelection" width="409" height="500" class="aligncenter size-large wp-image-121470"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSelection-409x500.png 409w, https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSelection-262x320.png 262w, https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSelection.png 960w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <p>
        Click an item and you’ll see highlighting. Choose a different image and
        you’ll see fully functional highlighting. Poof! Magic!
    </p>
    <h2>
        Where to go From Here
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
        Download the final version of
        <em>
            SlidesMagic
        </em>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/02/SlidesMagic-Final.zip"
        rel="">
            here
        </a>
        .
    </p>
    <p>
        In this collection views in OS X tutorial you went all the way from creating
        your first ever collection view, through discovering the intricacies of
        the data source API with sections, to handling selection with the delegate
        protocol. However, although you covered a lot of ground, you’ve barely
        explored the capabilities of collection views. For instance, you didn’t
        look into any of these:
    </p>
    <ul>
        <li>
            “Data Source-less” collection views using Cocoa Bindings
        </li>
        <li>
            Different kind of items
        </li>
        <li>
            Adding and removing items
        </li>
        <li>
            Custom layouts
        </li>
        <li>
            Drag and drop
        </li>
        <li>
            Animations
        </li>
        <li>
            Tweaking
            <code>
                NSCollectionViewFlowLayout
            </code>
            (sticky headers, for example)
        </li>
    </ul>
    <p>
        We will be covering some of these topics in upcoming OS X tutorials here
        on
        <a href="http://www.raywenderlich.com">
            raywenderlich.com
        </a>
        , so be sure to check back over the coming months.
    </p>
    <p>
        Unfortunately, the documentation for collection views from Apple and other
        sources is limited, but here are my suggestions:
    </p>
    <ul>
        <li>
            <a href="https://developer.apple.com/videos/play/wwdc2015-225/" target="_blank">
                WWDC 2015 – Session 225 – What’s New in NSCollectionView
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/mac/releasenotes/AppKit/RN-AppKit/#10_11CollectionView"
            target="_blank">
                OS X 10.11 El Capitan Release Notes for Cocoa Application Framework
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/prerelease/mac/samplecode/CocoaSlideCollection/Introduction/Intro.html"
            target="_blank">
                CocoaSlideCollection
            </a>
            – Sample code of WWDC Session 225 above. Written in Objective-C
        </li>
        <li>
            <a href="https://developer.apple.com/library/prerelease/mac/samplecode/Exhibition/Listings/Exhibition_ImageListController_swift.html"
            target="_blank">
                Exhibition
            </a>
            – Sample code from Apple, written in Swift using
            <code>
                NSCollectionViewGridLayout
            </code>
        </li>
    </ul>
</div>