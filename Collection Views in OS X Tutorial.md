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
        中打开它。运行项目：
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
    <pre lang="bash" class="language-bash hljs">Main.storyboard: Unknown segue relationship: Prototype 
</pre>
    <p>
        和collection view一起，
        <em>
            Xcode
        </em>
        还添加了一个
        <code>
            NSCollectionViewItem
        </code>
        ，且于一个
        <em>
            Prototype
        </em>
        segue相连。
    </p>
    <p>
        这其中就有造成了你build错误的原因 - 这就是造成这种麻烦的segue的类型。这是一个OS X 10.10的遗产（或是一个bug如果你喜欢的话），早期的API model可以避免你在storyboard中使用collection view item。
    </p>
    <p>
        修复的方法是删除它，并将它转化为一个独立的
        <em>
            xib
        </em>
        文件。
    </p>
    <p>
        选择
        <em>
            Collection View Item
        </em>
        并按
        <em>
            Delete
        </em>
        键来删除它。
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
        现在错误就消失了。
    </p>
    <p>
        调整
        <em>
            Bordered Scroll View
        </em>
        的大小，让它可以占据整个父view的区域。然后，选择
        <em>
            Editor \ Resolve Auto Layout Issues \ Add Missing Constraints
        </em>
        来添加
        <em>
            Auto Layout
        </em>
        约束。
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
        你需要在
        <em>
            ViewController
        </em>
        添加一个outlet来连接collection view。打开
        <em>
            ViewController.swift
        </em>
        并添加下列的代码到
        <code>
            ViewController
        </code>
        类的定义中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@IBOutlet</span> <span class="hljs-keyword">weak</span> <span class="hljs-keyword">var</span> collectionView: <span class="hljs-type">NSCollectionView</span>!
</pre>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        ，并选择
        <em>
            View Controller Scene
        </em>
        中的
        <em>
            View Controller
        </em>
        。
    </p>
    <p>
        打开
        <em>
            Connections Inspector
        </em>
        并在
        <em>
            Outlets
        </em>
        部分找到
        <em>
            collectionView
        </em>
        元素。通过
        <em>
            拖拽
        </em>
        画布上靠近collection view控件的button到collection view来进行连接。
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
        配置Collection View的布局
    </h3>
    <p>
        你已获得了选项：你可以获取初始的布局，和一些
        <em>
            Interface Builder
        </em>
        中的attribute，或者你可以用编程方式来设置它们。
    </p>
    <p>
        对于，你将采用编程的方式。
    </p>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        并添加下列的方法到
        <code>
            ViewController
        </code>
        ：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">private</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">configureCollectionView</span><span class="hljs-params">()</span></span> {
  <span class="hljs-comment">// 1</span>
  <span class="hljs-keyword">let</span> flowLayout = <span class="hljs-type">NSCollectionViewFlowLayout</span>()
  flowLayout.itemSize = <span class="hljs-type">NSSize</span>(width: <span class="hljs-number">160.0</span>, height: <span class="hljs-number">140.0</span>)
  flowLayout.sectionInset = <span class="hljs-type">NSEdgeInsets</span>(top: <span class="hljs-number">10.0</span>, <span class="hljs-keyword">left</span>: <span class="hljs-number">20.0</span>, bottom: <span class="hljs-number">10.0</span>, <span class="hljs-keyword">right</span>: <span class="hljs-number">20.0</span>)
  flowLayout.minimumInteritemSpacing = <span class="hljs-number">20.0</span>
  flowLayout.minimumLineSpacing = <span class="hljs-number">20.0</span>
  collectionView.collectionViewLayout = flowLayout
  <span class="hljs-comment">// 2</span>
  view.wantsLayer = <span class="hljs-literal">true</span>
  <span class="hljs-comment">// 3</span>
  collectionView.layer?.backgroundColor = <span class="hljs-type">NSColor</span>.blackColor().<span class="hljs-type">CGColor</span>
}
</pre>
    <p>
        以上代码完成了：
    </p>
    <ol>
        <li>
            创建一个
            <code>
                NSCollectionViewFlowLayout
            </code>
            并设置它的attribute，以及
            <code>
                NSCollectionView
            </code>
            的
            <code>
                collectionViewLayout
            </code>
            property。
        </li>
        <li>
            为了优化性能，
            <code>
                NSCollectionView
            </code>
            被设计为基于layer的。因此，你要设置其
            <code>
                wantsLayer
            </code>
            property为
            <code>
                true
            </code>
            。
        </li>
        <li>
            建立一个对于layer的特定于
            <em>
                SlidesMagic
            </em>
            的额外的关联，设置collection view的北京颜色为黑色。
        </li>
    </ol>
    <p>
        你需要在view被创建时调用这个方法，因此添加下列的代码到
        <code>
            viewDidLoad()
        </code>
        的尾部：
    </p>
    <pre lang="swift" class="language-swift hljs"><font><font>configureCollectionView（）
</font></font></pre>
    <p>
        运行项目：
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
        现在，你已经有了一个黑色的背景和布局。你已经为你的魔法show设置好了舞台！
    </p>
    <h2>
        在Collection View中加载项目
    </h2>
    <p>
        为了加载项目，你需要调用这个
        <code>
            reloadData()
        </code>
        方法，它会让collection view重新展示当前可见的item。
    </p>
    <p>
        你通常会在model发生变化时调用这个方法。
    </p>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        并添加下列的代码到
        <code>
            loadDataForNewFolderWithUrl(\_:)
        </code>
        的尾部：
    </p>
    <pre lang="swift" class="language-swift hljs">collectionView.reloadData()
</pre>
    <p>
        这让它可以通过选择
        <em>
            File \ Open Another Folder…
        </em>
        来调用这个方法。它会加载一个新的model，然后调用
        <code>
            reloadData()
        </code>
        。
    </p>
    <h2>
        创建一个Collection View的Item
    </h2>
    <p>
        由于你从storyboard移除
        <code>
            NSCollectionViewItem
        </code>
        并不意味着你不需要它。:] 这里是如何将它带回来的正确方式。
    </p>
    <p>
        前往
        <em>
            File \ New \ File…
        </em>
        ，选择
        <em>
            OS X \ Source \ Cocoa Class
        </em>
        并单击
        <em>
            Next
        </em>
        。
    </p>
    <p>
        设置
        <em>
            Class
        </em>
        域为
        <em>
            CollectionViewItem
        </em>
        ，它是
        <code>
            NSCollectionViewItem
        </code>
        的
        <em>
            子类
        </em>
        ，并单击
        <em>
            Also create XIB for user interface
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/CreateColViewItems.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/CreateColViewItems.png"
            alt="CreateColViewItems" width="444" height="163" class="aligncenter size-full wp-image-121352">
        </a>
    </p>
    <p>
        单击
        <em>
            Next
        </em>
        ，在保存对话框中，从
        <em>
            Group
        </em>
        选择
        <em>
            Controllers
        </em>
        并单击
        <em>
            Create
        </em>
        。
    </p>
    <p>
        打开
        <em>
            CollectionViewItem.swift
        </em>
        并使用下列代码替换整个类：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">CollectionViewItem</span>: <span class="hljs-title">NSCollectionViewItem</span> </span>{<font></font>
<font></font>
  <span class="hljs-comment">// 1</span>
  <span class="hljs-keyword">var</span> imageFile: <span class="hljs-type">ImageFile</span>? {
    <span class="hljs-keyword">didSet</span> {
      <span class="hljs-keyword">guard</span> viewLoaded <span class="hljs-keyword">else</span> { <span class="hljs-keyword">return</span> }
      <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> imageFile = imageFile {<font></font>
        imageView?.image = imageFile.thumbnail<font></font>
        textField?.stringValue = imageFile.fileName<font></font>
      } <span class="hljs-keyword">else</span> {<font></font>
        imageView?.image = <span class="hljs-literal">nil</span>
        textField?.stringValue = <span class="hljs-string">""</span><font></font>
      }<font></font>
    }<font></font>
  }<font></font>
  <font></font>
  <span class="hljs-comment">// 2</span>
  <span class="hljs-keyword">override</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">viewDidLoad</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">super</span>.viewDidLoad()<font></font>
    view.wantsLayer = <span class="hljs-literal">true</span>
    view.layer?.backgroundColor = <span class="hljs-type">NSColor</span>.lightGrayColor().<span class="hljs-type">CGColor</span><font></font>
  }<font></font>
}<font></font>
</pre>
    <p>
        在，这里：
    </p>
    <ol>
        <li>
            定义
            <code>
                imageFile
            </code>
            property来持有将在这个item中展示的model对象。当设置的时候，它的
            <code>
                didSet
            </code>
            property观察者就会设置item的图片和标签内容。
        </li>
        <li>
            改变item的view的背景颜色。
        </li>
    </ol>
    <h2>
        添加控件到view上
    </h2>
    <p>
        在nib文件中的
        <em>
            View
        </em>
        ，是在item中展示的控件树的根view。你将会添加一个image view，和一个用来展示文件名的label。
    </p>
    <p>
        打开
        <em>
            CollectionViewItem.xib
        </em>
        。
    </p>
    <p>
        添加一个
        <code>
            NSImageView
        </code>
        ：
    </p>
    <ol>
        <li>
            从
            <em>
                Object Library
            </em>
            中，添加一个
            <em>
                Image View
            </em>
            到
            <em>
                View
            </em>
            上。
        </li>
        <li>
            选择并从
            <em>
                Auto Layout
            </em>
            的工具栏中单击
            <em>
                Pin
            </em>
            来设置它的约束。
        </li>
        <li>
            设置
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
            约束为0，
            <em>
                bottom
            </em>
            为30并单击
            <em>
                Add 4 Constraints
            </em>
            。
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
            为了修复这个Auto Layout的问题，选择
            <em>
                Editor \ Resolve Auto Layout Issues \ Update Frames
            </em>
            。
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
        添加一个label：
    </p>
    <ol>
        <li>
            从
            <em>
                Object Library
            </em>
            中，添加一个
            <em>
                Label
            </em>
            到
            <em>
                Image View
            </em>
            下面。
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
            单击
            <em>
                Pin
            </em>
            按钮。设置
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
            约束为0，然后单击
            <em>
                Add 4 Constraints
            </em>
            。
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
            选择
            <em>
                Editor \ Resolve Auto Layout Issues \ Update Frames
            </em>
            来更新它的位置。
        </li>
    </ol>
    <p>
        选择
        <em>
            Label
        </em>
        ，在
        <em>
            Attributes Inspector
        </em>
        中设置下列的attribute：
    </p>
    <ol>
        <li>
            <em>
                Alignment
            </em>
            为
            <em>
                center
            </em>
        </li>
        <li>
            <em>
                Text Color
            </em>
            为
            <em>
                white
            </em>
        </li>
        <li>
            <em>
                Line Break
            </em>
            为
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
        现在你需要连接控件到
        <code>
            imageView
        </code>
        和
        <code>
            textField
        </code>
        的outlets上：
    </p>
    <ol>
        <li>
            选择
            <em>
                File’s Owner
            </em>
            并展示
            <em>
                Connections Inspector
            </em>
            。
        </li>
        <li>
            接下来，将靠近
            <em>
                imageView
            </em>
            的按钮
            <em>
                拖拽到
            </em>
            <em>
                Image View
            </em>
            控件上，并连接它们。
        </li>
        <li>
            用相同的方式，连接
            <code>
                textField
            </code>
            的outlet到
            <em>
                Label
            </em>
            上。
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
        添加一个顶层的CollectionViewItem到Nib上
    </h2>
    <p>
        在nib文件中的
        <em>
            File’s Owner
        </em>
        - 它的类型是
        <code>
            CollectionViewItem
        </code>
        - 只是一个占位符。你仍然需要去实例化它。
    </p>
    <p>
        <code>
            CollectionView
        </code>
        的方法
        <code>
            makeItemWithIdentifier(\_:forIndexPath:)
        </code>
        会实例化collection view的item，它要求nib文件包含一个单独的顶层的
        <code>
            NSCollectionViewItem
        </code>
        的实例或它的子类。
    </p>
    <p>
        你需要让它显示出来。
    </p>
    <p>
        从
        <em>
            Object Library
        </em>
        中拖拽一个
        <em>
            Collection View Item
        </em>
        并将它放置到
        <em>
            Document Outline
        </em>
        中。选择它，并在
        <em>
            Identity Inspector
        </em>
        中，设置它的
        <em>
            Class
        </em>
        为
        <code>
            CollectionViewItem
        </code>
        。
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
        填充Collection View
    </h2>
    <p>
        你需要实现data source的方法，让Collection View可以了解下列内容：
    </p>
    <ol>
        <li>
            在collection中有多少个section？
        </li>
        <li>
            在每个section中有多少个item？
        </li>
        <li>
            哪个item和指定的索引路径相关联？
        </li>
    </ol>
    <p>
        满足你的data source方法：
        <code>
            NSCollectionViewDataSource
        </code>
        协议。
    </p>
    <p>
        现在进入实践 - 打开
        <em>
            ViewController.swift
        </em>
        并添加下列的extension到文件的尾部：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">ViewController</span> : <span class="hljs-title">NSCollectionViewDataSource</span> </span>{
  
  <span class="hljs-comment">// 1</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">numberOfSectionsInCollectionView</span><span class="hljs-params">(collectionView: NSCollectionView)</span></span> -&gt; <span class="hljs-type">Int</span> {
    <span class="hljs-keyword">return</span> imageDirectoryLoader.numberOfSections
  }
  
  <span class="hljs-comment">// 2</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">collectionView</span><span class="hljs-params">(collectionView: NSCollectionView, numberOfItemsInSection section: Int)</span></span> -&gt; <span class="hljs-type">Int</span> {
    <span class="hljs-keyword">return</span> imageDirectoryLoader.numberOfItemsInSection(section)
  }
  
  <span class="hljs-comment">// 3</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">collectionView</span><span class="hljs-params">(collectionView: NSCollectionView, itemForRepresentedObjectAtIndexPath indexPath: NSIndexPath)</span></span> -&gt; <span class="hljs-type">NSCollectionViewItem</span> {
    <span class="hljs-comment">// 4</span>
    <span class="hljs-keyword">let</span> item = collectionView.makeItemWithIdentifier(<span class="hljs-string">"CollectionViewItem"</span>, forIndexPath: indexPath)
    <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> collectionViewItem = item <span class="hljs-keyword">as</span>? <span class="hljs-type">CollectionViewItem</span> <span class="hljs-keyword">else</span> {<span class="hljs-keyword">return</span> item}
    <span class="hljs-comment">// 5</span>
    <span class="hljs-keyword">let</span> imageFile = imageDirectoryLoader.imageFileForIndexPath(indexPath)
    collectionViewItem.imageFile = imageFile
    <span class="hljs-keyword">return</span> item
  }
  
}
</pre>
    <ol>
        <li>
            这个方法提供了section的数量。当你的app不支持section的时候，你可以忽略这个方法，collection view就会只有一个section。当
            <em>
                SlidesMagic
            </em>
            启动的时候，model
            <code>
                imageDirectoryLoader
            </code>
            会被设置返回值为1。
        </li>
        <li>
            这是
            <code>
                NSCollectionViewDataSource
            </code>
            中的两个必须方法之一。在这里，你要返回由
            <code>
                section
            </code>
            参数所指定的section中的item的数量。在启动的时候
            <em>
                SlidesMagic
            </em>
            有一个单独的section，因此你设置让model来返回目录中image的总数。
        </li>
        <li>
            这是第二个必须的方法。它对于给定的
            <code>
                indexPath
            </code>
            ，返回一个collection view的item。
        </li>
        <li>
            collection view的方法
            <code>
                makeItemWithIdentifier(\_:forIndexPath:)
            </code>
            从nib文件中初始化了一个item，该nib文件的名称和
            <code>
                identifier
            </code>
            参数相同。在本例中，它是
            <code>
                “CollectionViewItem”
            </code>
            。首先，它尝试去复用一个要求类型的未使用的item，如果没有的话，它就会创建一个新的。
        </li>
        <li>
            此代码根据给定的
            <code>
                NSIndexPath
            </code>
            得到相应的model对象，并设置图片和标签的内容。
        </li>
    </ol>
    <div class="note">
        <em>
            注意
        </em>
        ：collection view复用item的能力，为支持大型的collection提供了可扩展的解决方案。那些关联到不可见的item的model对象，就是将会被引用到的对象。
    </div>
    <h3>
        设置Data Source
    </h3>
    <p>
        没有数据的collection view就像是一个“没有灵巧的手的魔法表演” - 毫无生趣。因此，下一步就是定义data source了。在本案中它就是view controller。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        并选择collection view。
    </p>
    <p>
        打开
        <em>
            Connections Inspector
        </em>
        并在
        <em>
            Outlets
        </em>
        部分找到
        <em>
            dataSource
        </em>
        。
        <em>
            拖拽
        </em>
        临近的按钮到
        <em>
            Document Outline View
        </em>
        中的
        <em>
            View Controller
        </em>
        上。
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
        运行项目。
        <br>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/OneSectionFinal.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/OneSectionFinal-409x500.png"
            alt="OneSectionFinal" width="409" height="500" class="aligncenter size-large wp-image-121409"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/OneSectionFinal-409x500.png 409w, https://koenig-media.raywenderlich.com/uploads/2015/11/OneSectionFinal-262x320.png 262w, https://koenig-media.raywenderlich.com/uploads/2015/11/OneSectionFinal.png 960w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <p>
        看！对得起全部的工作！你的collection view展示了来自
        <em>
            Desktop Pictures
        </em>
        目录中的图片！
    </p>
    <h3>
        故障排除
    </h3>
    <p>
        如果你不能看到图片，然后某些事发生了错误。你已经通过了几个步骤，因此你只是犯了一些小错误。
    </p>
    <ol>
        <li>
            所有的
            <em>
                Connections Inspector
            </em>
            是否已按照教程设置？
        </li>
        <li>
            你是否设置了
            <code>
                dataSource
            </code>
            outlet？
        </li>
        <li>
            你是否在
            <em>
                Identity Inspector
            </em>
            中使用了正确的定制的类。
        </li>
        <li>
            你是否添加了顶层的
            <code>
                NSCollectionViewItem
            </code>
            的对象，并将它的类型改变为
            <code>
                CollectionViewItem
            </code>
            ？
        </li>
        <li>
            在
            <code>
                makeItemWithIdentifier
            </code>
            中
            <code>
                identifier
            </code>
            参数的值是否相等于nib的名称？
        </li>
    </ol>
    <h2>
        前往多section式
    </h2>
    <p>
        MagicSlides现在正在认真地表演魔法。但你还想通过添加一些section来提高它。
    </p>
    <p>
        首先，你需要在view的底部添加一个check box，让你可以在单section和多section之间切换。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        ，并在
        <em>
            Document Outline
        </em>
        view中，选择scroll view的底部约束。打开
        <em>
            Size Inspector
        </em>
        并将
        <em>
            Constant
        </em>
        改变为30。
    </p>
    <p>
        这样你就将collection view向上移动了一些，并给check box留出了空间。
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
        现在，从
        <em>
            Object Library
        </em>
        中拖拽一个
        <em>
            Check Box Button
        </em>
        到collection view的下方。选择它，并在
        <em>
            Attributes Inspector
        </em>
        中，设置
        <em>
            Title
        </em>
        为
        <em>
            Show Sections
        </em>
        ，
        <em>
            State
        </em>
        为
        <em>
            Off
        </em>
        。
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
        然后，通过选择
        <em>
            Editor \ Resolve Auto Layout Issues \ Add Missing Constraints
        </em>
        菜单项设置
        <em>
            Auto Layout
        </em>
        约束。
    </p>
    <p>
        运行项目。它的底部应当看起来就像这样：
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
        现在是一个小UI。当你单击box时，app需要改变collection view的外观。
    </p>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        并添加下列的方法到
        <code>
            ViewController
        </code>
        类的尾部：
    </p>
    <pre lang="swift" class="language-swift hljs">  
<span class="hljs-comment">// 1</span>
<span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">showHideSections</span><span class="hljs-params">(sender: AnyObject)</span></span> {
  <span class="hljs-comment">// 2</span>
  <span class="hljs-keyword">let</span> show = (sender <span class="hljs-keyword">as</span>! <span class="hljs-type">NSButton</span>).state
  imageDirectoryLoader.singleSectionMode = (show == <span class="hljs-type">NSOffState</span>)
  imageDirectoryLoader.setupDataForUrls(<span class="hljs-literal">nil</span>)
  <span class="hljs-comment">// 3</span>
  collectionView.reloadData()
}
</pre>
    <p>
        一部分一部分地说，这里是你所做的事：
    </p>
    <ol>
        <li>
            通过切换checkbox的状态来调用这个方法。
        </li>
        <li>
            相应地，检索checkbox的状态，并设置数据model的mode为
            <code>
                singleSelectionMode
            </code>
            ，然后调用model的
            <code>
                setupDataForUrls(\_:)
            </code>
            方法来重新排列section的结构。传递
            <code>
                nil
            </code>
            的值则意味着你跳过了图片的加载 - 相同的图片，不同的布局。
        </li>
    </ol>
    <p>
        如果你好奇于图片是如何通过section进行分布，可查阅
        <code>
            ImageDirectoryLoader
        </code>
        中的
        <code>
            sectionLengthArray
        </code>
        。在这个数组中元素的数量，就被设定成了section的最大数量，元素的值则设定了在每一section中item的数量。
    </p>
    <p>
        现在，打开
        <em>
            Main.storyboard
        </em>
        。在
        <em>
            Document Outline
        </em>
        中，
        <em>
            按住Control拖拽
        </em>
        <em>
            Show Sections
        </em>
        控件到
        <em>
            View Controller
        </em>
        上。在弹出的黑色菜单中，单击
        <em>
            showHideSections:
        </em>
        来连接它。你可以在
        <em>
            Connections Inspector
        </em>
        中查看connection是否被正确地设置。
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
        运行项目。
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
        查看
        <em>
            Show Sections
        </em>
        ，并观察布局的变化。
    </p>
    <p>
        由于第二行中的“黑色尾巴”，你会看到在第0部分有7个图像，但第1部分有5个图像，第2个部分则有10个（请看
        <code>
            sectionLengthArray
        </code>
        ）。这并不清楚，因为这些section相当得懵逼。
    </p>
    <p>
        要解决这个，打开
        <em>
            ViewController.swift
        </em>
        并在
        <code>
            configureCollectionView()
        </code>
        方法中修改布局的
        <code>
            sectionInset
        </code>
        property。
    </p>
    <p>
        用：
    </p>
    <pre lang="swift" class="language-swift hljs">  
flowLayout.sectionInset = <span class="hljs-type">NSEdgeInsets</span>(top: <span class="hljs-number">30.0</span>, <span class="hljs-keyword">left</span>: <span class="hljs-number">20.0</span>, bottom: <span class="hljs-number">30.0</span>, <span class="hljs-keyword">right</span>: <span class="hljs-number">20.0</span>)
</pre>
    <p>
        替换：
    </p>
    <pre lang="swift" class="language-swift hljs">  
flowLayout.sectionInset = <span class="hljs-type">NSEdgeInsets</span>(top: <span class="hljs-number">10.0</span>, <span class="hljs-keyword">left</span>: <span class="hljs-number">20.0</span>, bottom: <span class="hljs-number">10.0</span>, <span class="hljs-keyword">right</span>: <span class="hljs-number">20.0</span>)
</pre>
    <p>
        在这里，你设置底部和顶部section的inset为30，以便提供更好的section之间的分隔。
    </p>
    <p>
        运行项目：
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
        查看
        <em>
            Show Sections
        </em>
        ，注意到在section之间的额外的空间。
    </p>
    <h2>
        添加Section Header
    </h2>
    <p>
        这个app到目前看起来都很棒，但更多的组织可以让它看起来更棒！
    </p>
    <p>
        让section的边界看得更清楚的另一种方式，是添加一个header或footer。为实现这点，你需要添加一个定制的
        <code>
            NSView
        </code>
        类，以及实现一个data source的方法来提供header view到table view上。
    </p>
    <p>
        为了创建header view，选择
        <em>
            File \ New \ File…
        </em>
        。选择
        <em>
            OS X \ User Interface \ View
        </em>
        并单击
        <em>
            Next
        </em>
        。
    </p>
    <p>
        输入
        <em>
            HeaderView.xib
        </em>
        作为文件名称，对于
        <em>
            Group
        </em>
        则选择
        <em>
            Resources
        </em>
        。
    </p>
    <p>
        单击
        <em>
            Create
        </em>
        。
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
        打开
        <em>
            HeaderView.xib
        </em>
        并选择
        <em>
            Custom View
        </em>
        。打开
        <em>
            Size Inspector
        </em>
        ，并改变
        <em>
            Width
        </em>
        为500以及
        <em>
            Height
        </em>
        为40。
    </p>
    <p>
        从
        <em>
            Object Library
        </em>
        中拖拽一个label到
        <em>
            Custom View
        </em>
        的左侧。打开
        <em>
            Attributes Inspector
        </em>
        并改变
        <em>
            Title
        </em>
        为
        <em>
            Section Number
        </em>
        ，以及
        <em>
            Font Size
        </em>
        为
        <em>
            16
        </em>
        。
    </p>
    <p>
        拖拽第二个label到
        <em>
            Custom View
        </em>
        的右边，并将
        <em>
            Title
        </em>
        改为
        <em>
            Images Count
        </em>
        ，
        <em>
            Text Alignment
        </em>
        改为
        <em>
            Right
        </em>
        。
    </p>
    <p>
        现在，选择
        <em>
            Editor \ Resolve Auto Layout Issues \ Add Missing Constraints
        </em>
        菜单来添加
        <em>
            Auto Layout
        </em>
        约束。
    </p>
    <p>
        header view应当看起来就像这样：
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
        随着界面已准备好显示时间，下一个任务就是为header view创建一个定制的view的子类。
    </p>
    <p>
        选择
        <em>
            File \ New \ File…
        </em>
        来创建一个新的文件。
    </p>
    <p>
        选择
        <em>
            OS X \ Source \ Cocoa Class
        </em>
        并将类命名为
        <code>
            HeaderView
        </code>
        ，并让它成为
        <code>
            NSView
        </code>
        的子类。单击下一步，对于
        <em>
            Group
        </em>
        选择
        <em>
            Views
        </em>
        。单击
        <em>
            Create
        </em>
        。
    </p>
    <p>
        打开
        <em>
            HeaderView.swift
        </em>
        并使用下列代码替换类的内容：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-comment">// 1</span>
<span class="hljs-meta">@IBOutlet</span> <span class="hljs-keyword">weak</span> <span class="hljs-keyword">var</span> sectionTitle: <span class="hljs-type">NSTextField</span>!
<span class="hljs-meta">@IBOutlet</span> <span class="hljs-keyword">weak</span> <span class="hljs-keyword">var</span> imageCount: <span class="hljs-type">NSTextField</span>!

<span class="hljs-comment">// 2</span>
<span class="hljs-keyword">override</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">drawRect</span><span class="hljs-params">(dirtyRect: NSRect)</span></span> {
  <span class="hljs-keyword">super</span>.drawRect(dirtyRect)
  <span class="hljs-type">NSColor</span>(calibratedWhite: <span class="hljs-number">0.8</span> , alpha: <span class="hljs-number">0.8</span>).<span class="hljs-keyword">set</span>()
  <span class="hljs-type">NSRectFillUsingOperation</span>(dirtyRect, <span class="hljs-type">NSCompositingOperation</span>.<span class="hljs-type">CompositeSourceOver</span>)
}
</pre>
    <p>
        这里：
    </p>
    <ol>
        <li>
            设置你用来连接到nib上的label的outlet。
        </li>
        <li>
            绘制一个灰色的背景。
        </li>
    </ol>
    <p>
        随着框架已到位，下一个任务就是改变nib文件去使用新的类，以及连接outlet到label上。
    </p>
    <p>
        打开
        <em>
            HeaderView.xib
        </em>
        并选择
        <em>
            Custom View
        </em>
        。打开
        <em>
            Identity Inspector
        </em>
        。改变
        <em>
            Class
        </em>
        为
        <em>
            HeaderView
        </em>
        。
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
        在
        <em>
            Document Outline
        </em>
        view中，
        <em>
            按住Control单击
        </em>
        <em>
            Header View
        </em>
        。在弹出的黑色窗口中，将
        <em>
            imageCount
        </em>
        <em>
            拖拽
        </em>
        到画布的
        <em>
            Images Count
        </em>
        label上来连接outlet。
    </p>
    <p>
        为第二个label执行重复的操作，将
        <em>
            sectionTitle
        </em>
        拖拽到画布的
        <em>
            Section Number
        </em>
        label上。
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
        实现Data Source和Delegate方法
    </h3>
    <p>
        你的header view已准备就绪，你需要将它拖拽到collection view上来实现
        <code>
            collectionView(\_:viewForSupplementaryElementOfKind:atIndexPath:)
        </code>
        方法。
    </p>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        并添加下列的方法到
        <code>
            NSCollectionViewDataSource
        </code>
        到extension中：
    </p>
    <pre lang="swift" class="language-swift hljs">  
<span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">collectionView</span><span class="hljs-params">(collectionView: NSCollectionView, viewForSupplementaryElementOfKind kind: String, atIndexPath indexPath: NSIndexPath)</span></span> -&gt; <span class="hljs-type">NSView</span> {
  <span class="hljs-comment">// 1</span>
  <span class="hljs-keyword">let</span> view = collectionView.makeSupplementaryViewOfKind(<span class="hljs-type">NSCollectionElementKindSectionHeader</span>, withIdentifier: <span class="hljs-string">"HeaderView"</span>, forIndexPath: indexPath) <span class="hljs-keyword">as</span>! <span class="hljs-type">HeaderView</span>
  <span class="hljs-comment">// 2</span>
  view.sectionTitle.stringValue = <span class="hljs-string">"Section <span class="hljs-subst">\(indexPath.section)</span>"</span>
  <span class="hljs-keyword">let</span> numberOfItemsInSection = imageDirectoryLoader.numberOfItemsInSection(indexPath.section)
  view.imageCount.stringValue = <span class="hljs-string">"<span class="hljs-subst">\(numberOfItemsInSection)</span> image files"</span>
  <span class="hljs-keyword">return</span> view
}
</pre>
    <p>
        collection view会在它需要data source为某个section提供header时，调用这个方法。方法：
    </p>
    <ol>
        <li>
            调用
            <code>
                makeSupplementaryViewOfKind(\_:withIdentifier:forIndexPath:)
            </code>
            方法来初始化一个
            <code>
                withIdentifier
            </code>
            参数和nib名称相同的
            <code>
                HeaderView
            </code>
            对象。
        </li>
        <li>
            给label设置值。
        </li>
    </ol>
    <p>
        在
        <em>
            ViewController.swift
        </em>
        的尾部，添加下列的
        <code>
            NSCollectionViewDelegateFlowLayout
        </code>
        extension。
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">ViewController</span> : <span class="hljs-title">NSCollectionViewDelegateFlowLayout</span> </span>{
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">collectionView</span><span class="hljs-params">(collectionView: NSCollectionView, layout collectionViewLayout: NSCollectionViewLayout, referenceSizeForHeaderInSection section: Int)</span></span> -&gt; <span class="hljs-type">NSSize</span> {
    <span class="hljs-keyword">return</span> imageDirectoryLoader.singleSectionMode ? <span class="hljs-type">NSZeroSize</span> : <span class="hljs-type">NSSize</span>(width: <span class="hljs-number">1000</span>, height: <span class="hljs-number">40</span>)
  }
}
</pre>
    <p>
        以上的方法，在技术上也是可选的，但当你需要为每个section提供header的时候，你就必须使用它来为每个header提供尺寸的大小。
    </p>
    <p>
        如果你没有实现，header就不会展示出来，因为它的尺寸会被认为是0。此外，它还会忽略指定的宽度，而是将宽度设置为collection view的宽度。
    </p>
    <p>
        在本例中，这个方法会在collection view采取单个section模式时，返回尺寸为0；当collection view采取多section模式时，返回40。
    </p>
    <p>
        为使collection view使用
        <code>
            NSCollectionViewDelegateFlowLayout
        </code>
        ，你必须连接
        <code>
            ViewController
        </code>
        到
        <code>
            NSCollectionView
        </code>
        的outlet
        <code>
            delegate
        </code>
        上。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        并选择collection view。打开
        <em>
            Connections Inspector
        </em>
        ，并在
        <em>
            Outlets
        </em>
        部分中找到
        <em>
            delegate
        </em>
        。将靠近它的按钮
        <em>
            拖拽
        </em>
        到
        <em>
            Document Outline
        </em>
        中的view controller。
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
        运行项目。
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
        查看
        <em>
            Show Sections
        </em>
        ，并观察你的header已很好地区分了section。
    </p>
    <h2>
        Collection View的选择操作
    </h2>
    <p>
        Collection view支持单选和多选。为了表示item已被选取，你必须将它高亮一下。
    </p>
    <p>
        在你行动之前，你必须让collection view变得可选。打开
        <em>
            Main.storyboard
        </em>
        。然后选择
        <em>
            Collection View
        </em>
        ，并在
        <em>
            Attributes Inspector
        </em>
        中勾选
        <em>
            Selectable
        </em>
        。
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
        勾选
        <em>
            Selectable
        </em>
        就可以打开单选，也就是你可以单击一个item来选择它。并且当你选择另一个item时，之前选择的那个就会被取消。
    </p>
    <p>
        为了展示一个item已被选择，为它设置一个白色的边框，并使用
        <code>
            borderWith
        </code>
        将边框的粗细设定为5。未被选择的item则不会有特殊的处理。
    </p>
    <p>
        打开
        <em>
            CollectionViewItem.swift
        </em>
        。添加下列代码到
        <code>
            viewDidLoad()
        </code>
        方法的尾部：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-comment">// 1</span>
view.layer?.borderWidth = <span class="hljs-number">0.0</span>
<span class="hljs-comment">// 2</span>
view.layer?.borderColor = <span class="hljs-type">NSColor</span>.whiteColor().<span class="hljs-type">CGColor</span>
</pre>
    <ol>
        <li>
            设定
            <code>
                borderWidth
            </code>
            为
            <code>
                0.0
            </code>
            ，即将item初始化为未被选择的状态
        </li>
        <li>
            当item被选中时，设置为白色
        </li>
    </ol>
    <p>
        添加下列的方法到
        <code>
            CollectionViewItem
        </code>
        类的尾部：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">setHighlight</span><span class="hljs-params">(selected: Bool)</span></span> {
  view.layer?.borderWidth = selected ? <span class="hljs-number">5.0</span> : <span class="hljs-number">0.0</span>
}
</pre>
    <p>
        这个方法是用来添加或移除高亮效果的。
    </p>
    <p>
        当用户在collection view中选择了一个item，你就会从它的代理方法得到响应。你需要实现这些方法，因此，打开
        <em>
            ViewController.swift
        </em>
        并添加下列的extension到文件的尾部：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">ViewController</span> : <span class="hljs-title">NSCollectionViewDelegate</span> </span>{
  <span class="hljs-comment">// 1</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">collectionView</span><span class="hljs-params">(collectionView: NSCollectionView, didSelectItemsAtIndexPaths indexPaths: Set&lt;NSIndexPath&gt;)</span></span> {
    <span class="hljs-comment">// 2</span>
    <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> indexPath = indexPaths.first <span class="hljs-keyword">else</span> {
      <span class="hljs-keyword">return</span>
    }
    <span class="hljs-comment">// 3</span>
    <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> item = collectionView.itemAtIndexPath(indexPath) <span class="hljs-keyword">else</span> {
      <span class="hljs-keyword">return</span>
    }
    (item <span class="hljs-keyword">as</span>! <span class="hljs-type">CollectionViewItem</span>).setHighlight(<span class="hljs-literal">true</span>)
  }

  <span class="hljs-comment">// 4</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">collectionView</span><span class="hljs-params">(collectionView: NSCollectionView, didDeselectItemsAtIndexPaths indexPaths: Set&lt;NSIndexPath&gt;)</span></span> {
    <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> indexPath = indexPaths.first <span class="hljs-keyword">else</span> {
      <span class="hljs-keyword">return</span>
    }
    <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> item = collectionView.itemAtIndexPath(indexPath) <span class="hljs-keyword">else</span> {
      <span class="hljs-keyword">return</span>
    }
    (item <span class="hljs-keyword">as</span>! <span class="hljs-type">CollectionViewItem</span>).setHighlight(<span class="hljs-literal">false</span>)
  }
}
</pre>
    <p>
        这就实现了必须的
        <code>
            NSCollectionViewDelegate
        </code>
        方法。更多细节：
    </p>
    <ol>
        <li>
            当你选择了一个item，
            <code>
                NSCollectionView
            </code>
            就会调用这个方法。
        </li>
        <li>
            这里你获得了被选择的item - 由于多选是被禁用的，它总是第一个。
        </li>
        <li>
            通过序号来检索到item，并将它高亮。
        </li>
        <li>
            就像上一个方法一样，但它是在item被取消选择是调用的。
        </li>
    </ol>
    <h3>
        在选择期间时，发生了什么？
    </h3>
    <p>
        当被选择时，item就被设置了：
    </p>
    <ol>
        <li>
            加入
            <code>
                NSCollectionView
            </code>
            的property
            <code>
                selectionIndexPaths
            </code>
            。
        </li>
        <li>
            <code>
                NSCollectionViewItem
            </code>
            的property
            <code>
                selected
            </code>
            被设置为YES。
        </li>
    </ol>
    <p>
        理解当
        <code>
            NSCollectionViewItem
        </code>
        的实例被循环使用时，它的数据必须被来自新的对象的数据刷新是非常
        <i>
            重要的
        </i>
        。你
        <code>
            NSCollectionViewItem
        </code>
        的property
        <code>
            selected
        </code>
        就是确保这点的地方。
    </p>
    <p>
        因此，在
        <code>
            NSCollectionViewDataSource
        </code>
        的extension中，你需要添加下列的代码到
        <code>
            collectionView(\_:itemForRepresentedObjectAtIndexPath:)
        </code>
        方法中，就在
        <code>
            return
        </code>
        语句之前：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> selectedIndexPath = collectionView.selectionIndexPaths.first <span class="hljs-keyword">where</span> selectedIndexPath == indexPath {
  collectionViewItem.setHighlight(<span class="hljs-literal">true</span>)
} <span class="hljs-keyword">else</span> {
  collectionViewItem.setHighlight(<span class="hljs-literal">false</span>)
}
</pre>
    <p>
        这就确保了选择和高亮是同步的。
    </p>
    <p>
        运行项目。
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
        点击一个item，你会看到高亮的效果。选择一个不同的图片，你就会看到完全的高亮功能。哇！真是魔术！
    </p>
    <h2>
        从这儿去向哪里
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
        在
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/02/SlidesMagic-Final.zip"
        rel="">
            这里
        </a>
        可以下载到最终版本的
        <em>
            SlidesMagic
        </em>
        。
    </p>
    <p>
        在这个OS X的collection view教程中，你从创建第一个collection view，到发掘了带有section的复杂的data sourc API，到使用代理协议来处理选择。然而，尽管你已了解了很多基础的内容，你仍然只是探索到了collection view能力的皮毛。例如，下面的内容你还并不了解：
    </p>
    <ul>
        <li>
            使用Cocoa Bindings的“Data Source-less”的collection view
        </li>
        <li>
            不同类型的item
        </li>
        <li>
            添加和删除item
        </li>
        <li>
            定制布局
        </li>
        <li>
            拖拽和放置
        </li>
        <li>
            动画
        </li>
        <li>
            调整
            <code>
                NSCollectionViewFlowLayout
            </code>
            （例如，粘性的header）
        </li>
    </ul>
    <p>
        我们将会覆盖其中的一些话题在
        <a href="http://www.raywenderlich.com">
            raywenderlich.com
        </a>
        的即将到来的OS X教程中，因此，这几个月记得常来看看。
    </p>
    <p>
        有点不幸的是，来自苹果和其它来源的collection view的文档是非常有限的，但以下是我的建议：
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