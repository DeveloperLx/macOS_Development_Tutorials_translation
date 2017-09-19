# macOS NSTableView教程

#### [原文地址](https://www.raywenderlich.com/143828/macos-nstableview-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div class="note">
        <p>
            <em>
                更新记录：
            </em>
            这个macOS NSTableView的教程已由Warren Burton更新到Xcode 8及Swift 3的版本。
            <a href="https://www.raywenderlich.com/118835/os-x-nstableview-tutorial">
                原教程
            </a>
            是由Ernesto García撰写的。
        </p>
    </div>
    <div id="attachment_148775" style="width: 260px" class="wp-caption alignright">
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-250x250.png"
            alt="Create awesome user interfaces with table views!" width="250" height="250"
            class="size-thumbnail wp-image-148775" srcset="https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-128x128.png 128w"
            sizes="(max-width: 250px) 100vw, 250px">
        </a>
        <p class="wp-caption-text">
        	使用table view创建超级棒的用户界面！
        </p>
    </div>
    <p>
    	在macOS应用中，table view是最普遍存在的控件之一，熟悉的例子有邮件信息的列表及Spotlight的搜索结果。它可以让你的Mac以一个迷人的方式，来展现列成表格的数据。
    </p>
    <p>
        <code>
            NSTableView
        </code>
        使用行和列来排列数据。每一行代表给出的数据集合中的一个单独的数据模型，每一列展示这个数据模型中的一个特定的属性。
    </p>
    <p>
    	在这篇macOS的NSTableView教程中，你将使用一个table view来创建带有功能的文件查看器，它具有和Finder惊人的相似性。在你完成它之后，你将学到很多关于table view的知识，例如：
    </p>
    <ul>
        <li>
        	怎么填充一个table view。
        </li>
        <li>
        	怎么改变它的视觉风格。
        </li>
        <li>
        	怎么响应类似选择或双击用户交互。
        </li>
    </ul>
    <p>
    	准备好创建你的第一个table view了么？继续阅读！
    </p>
    <h2>
    	开始吧
    </h2>
    <p>
    	下载
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/FileViewer_starter-2.zip">
            起始的项目
        </a>
        并在
        <em>
            Xcode
        </em>
        中打开它。
    </p>
    <p>
    	运行项目，来查看你会从什么地方开始：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-empty.png">
            <img class="aligncenter size-full wp-image-118915" src="https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-empty.png"
            alt="window at start of tutorial" width="537" height="306" srcset="https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-empty.png 537w, https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-empty-480x274.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-empty-266x151.png 266w"
            sizes="(max-width: 537px) 100vw, 537px">
        </a>
    </p>
    <p>
    	你有一块空白的画布，这是你将要创建很酷的文件查看器的地方。这个起始的app已经包含了一些你需要在这个教程中使用的功能。
    </p>
    <p>
    	当文件打开时，选择
        <em>
            File &gt; Open…
        </em>
        （或使用
        <em>
            Command+O
        </em>
        快捷键）。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-fileopen.png">
            <img class="aligncenter size-large wp-image-118916" src="https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-fileopen-700x403.png"
            alt="open a folder" width="700" height="403" srcset="https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-fileopen-700x403.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-fileopen-480x276.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-fileopen.png 726w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
    	从弹出的新窗口中，选择任意你想要的目录，并点击
        <em>
            Open
        </em>
        按钮。你会在Xcode的控制台中看到像如下的东西：
    </p>
    <pre class="none" style="font-family:monospace;">
    Represented object: file:///Users/tutorials/FileViewer/FileViewer/	</pre>
    <p>
    	这个信息展示了被选择的目录的路径，在起始项目的代码中传递了URL到view controller中。
    </p>
    <p>
    	如果你很好奇，并想了解更多有关这些东西是怎么实现的，这些是你应该查看的地方：
    </p>
    <ul>
        <li>
            <em>
                Directory.swift
            </em>
            ：包含了结构体
            <em>
                Directory
            </em>
            从目录中读取内容的实现。
        </li>
        <li>
            <em>
                WindowController.swift
            </em>
            ：包含了展示给你目录选择面板的代码，并传递被选择的目录给
            <em>
                ViewController
            </em>
            。
        </li>
        <li>
            <em>
                ViewController.swift
            </em>
            ：包含了
            <code>
                ViewController
            </code>
            这个类的实现，这也是今天你要花费一些时间的地方。它是你将要创建table view和展示文件列表的地方。
        </li>
    </ul>
    <h2>
        创建Table View
    </h2>
    <p>
    	在
    	<em>
            Project Navigator
        </em>
    	中打开
        <em>
            Main.storyboard
        </em>
        。选择
        <em>
            View Controller Scene
        </em>
        ，然后从
        <em>
            Object Library
        </em>
        放置一个table view到这个view上。这个在view的层级中，名叫
        <em>
            Table Container
        </em>
        的容器早已为你备好。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/add-table.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/add-table-650x430.png"
            alt="add a table in interface builder" width="650" height="430" class="aligncenter size-large wp-image-145671"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/add-table-650x430.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/add-table-480x318.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/10/add-table.png 1525w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
    	下一步，你需要添加一些约束。在Auto Layout的工具栏中点击
        <em>
            Pin
        </em>
        按钮。在出现的弹出菜单中，设置全部的边缘约束如下：
    </p>
    <ul>
        <li>
            <em>
                Top
            </em>
            ,
            <em>
                Bottom
            </em>
            ,
            <em>
                Leading
            </em>
            及
            <em>
                Trailing
            </em>
            ：0。
        </li>
    </ul>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/11/constrain-table.png"
        alt="constrain the table to its container" width="362" height="500" class="aligncenter size-large wp-image-148614"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/11/constrain-table.png 576w, https://koenig-media.raywenderlich.com/uploads/2016/11/constrain-table-232x320.png 232w, https://koenig-media.raywenderlich.com/uploads/2016/11/constrain-table-362x500.png 362w"
        sizes="(max-width: 362px) 100vw, 362px">
    </p>
    <p>
    	务必设置
        <em>
            Update Frames
        </em>
        为
        <em>
            Items of New Constraints
        </em>
        ，然后点击
        <em>
            Add 4 Constraints
        </em>
        。
    </p>
    <p>
    	花几分钟来看一下新创建的table view的结构。正如你可能从它的名称中获取的一样，它遵循典型的table的结构：
    </p>
    <ul>
        <li>
        	由行和列构成。
        </li>
        <li>
        	每一行代表在数据模型集合中的单独的一项。
        </li>
        <li>
        	每一列展示这个model的指定的属性。
        </li>
        <li>
        	每一列也可以有一个列头（header row）。
        </li>
        <li>
        	列头描述了这一列的数据。
        </li>
    </ul>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/11/tableStructure.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/11/tableStructure-268x320.png"
            alt="table view inner structure" width="268" height="320" class="aligncenter size-medium wp-image-148302"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/11/tableStructure-268x320.png 268w, https://koenig-media.raywenderlich.com/uploads/2016/11/tableStructure-419x500.png 419w, https://koenig-media.raywenderlich.com/uploads/2016/11/tableStructure.png 606w"
            sizes="(max-width: 268px) 100vw, 268px">
        </a>
    </p>
    <p>
    	如果你熟悉iOS中的
        <code>
            UITableView
        </code>
        ，你会在走熟悉的路上（treading familiar waters），但在macOS中，它们会深更加入。事实上，你会惊讶于构成
        <code>
            NSTableView
        </code>
        的单个的UI对象的层级的数量。
    </p>
    <p>
        <code>
            NSTableView
        </code>
        是一个更老且比
        <code>
            UITableView
        </code>
        更复杂的控件，它服务于一个不同的用户交互的范例中，特别地在用户有一个鼠标或触控板的情况下。
    </p>
    <p>
    	相对于
        <em>
            UITableView
        </em>
        ，它的主要区别是你可以有多列，及一个可以用来同table view交互的表头，例如排序和选取。
    </p>
    <p>
        <code>
            NSScrollView
        </code>
        和
        <code>
            NSClipView
        </code>
        会分别负责滚动和裁剪
        <code>
            NSTableView
        </code>
        的内容。
    </p>
    <p>
    	这里有两个
        <code>
            NSScroller
        </code>
        对象 - 各自负责table在垂直和水平方向上的滚动。
    </p>
    <p>
    	这里也有一些列的对象。一个
        <code>
            NSTableView
        </code>
        有若干的列，这些列都有标题。注意，让用户能够改变列的大小和重新排序是非常重要的，尽管你可以通过设置默认为关闭的来移除这项能力。
    </p>
    <h3>
        剖析NSTableView
    </h3>
    <p>
    	在Interface Builder中，你已经看到了table view中的view层级的复杂性。很多的类协作来构建table的结构，通常最终看起来会像这样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/Artboard-1.png">
            <img class="aligncenter size-large wp-image-120794" src="https://koenig-media.raywenderlich.com/uploads/2015/11/Artboard-1-700x377.png"
            alt="components of a table view" width="700" height="377" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/Artboard-1-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/Artboard-1-480x258.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/Artboard-1.png 1454w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
    	这些是构成
        <code>
            NSTableView
        </code>
        的关键部分：
    </p>
    <ul>
        <li>
            <em>
                Header View
            </em>
            ：header view是
            <code>
                NSTableHeaderView
            </code>
            的实例。它负责在table的顶部绘制header。如果你需要展示一个定制的header，你可以使用你自己的header的子类。
        </li>
        <li>
            <em>
                Row View
            </em>
            ：row view展示了table view中的每一行的可见的属性，像一个选择高亮。展示在table中的每一行都有它自己的row view的实例。一个重大的区别是row不代表你的数据，cell才代表。它只处理可见的数据，例如选择颜色或分隔线。你可以创建新的row的子类来让你的table view风格不同。
        </li>
        <li>
            <em>
                Cell Views
            </em>
            ：cell可能是table view中最重要的对象了。在行和列交叉的地方，你会找到一个cell。每个cell都是
            <code>
                NSView
            </code>
            或
            <code>
                NSTableCellView
            </code>
            的子类，它用来负责展示实际的数据。猜下还有什么？你可以创建定制的cell view的类来展示任何你喜欢的内容。
        </li>
        <li>
            <em>
                Column
            </em>
            ：它是由
            <code>
                NSTableViewColumn
            </code>
            代表的，负责管理列的宽度和行为，例如调整大小和重新定位。这个类不是一个view，但却是一个controller的类。你可以用它来指定列的行为，但由于header的缘故，你不能控制列的可见的风格。row和cell view把这件事已经覆盖了。
        </li>
    </ul>
    <div class="note">
        <p>
            <em>
            	注意：
            </em>
            NSTableView有两种模式。第一种是基于被称作
            <code>
                NSCell
            </code>
            的cell。它像是一个
            <code>
                NSView
            </code>
            ，但是更老且更轻量。它来自于计算早期的时候，当桌面需要优化，要以最低的消耗绘制时而产生的。
        </p>
        <p>
        	苹果推荐使用基于view的table view，但是你会在AppKit的多个控件中看到
            <code>
                NSCell
            </code>
            ，值得去了解它是什么及它从哪里来的。你可以阅读更多的
            <code>
                NSCell
            </code>
            在苹果的
            <a title="Control and Cell Programming Topics" href="https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/ControlCell/Concepts/AboutControlsCells.html#//apple_ref/doc/uid/20000731-BBCEACEA"
            target="_blank">
                Control and Cell Programming Topics
            </a>
            这篇文档中。
        </p>
    </div>
    <p>
    	好的，现在一个很好的“小步慢跑”（little jog），了解table view结构背后的基础理论。既然你已了解了那些，现在就是时候返回
        <em>
            Xcode
        </em>
        来继续完成您非常个性化的table view。
    </p>
    <h3>
    	玩转table view中的行
    </h3>
    <p>
    	默认的，Interface Builder创建的table view会带有两列，但是你需要三列来展示名称，日期和大小的文件信息。
    </p>
    <p>
    	回到
        <em>
            Main.storyboard
        </em>
        。
    </p>
    <p>
        在
        <em>
            View Controller场景
        </em>
        中选择table view。确保你选择的是table view而
        <i>
            不是
        </i>
        包含它的scroll view。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/add-table-column.png"
        alt="table in the view hierarchy" width="317" height="360" class="aligncenter size-full wp-image-145681"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/add-table-column.png 317w, https://koenig-media.raywenderlich.com/uploads/2016/10/add-table-column-282x320.png 282w"
        sizes="(max-width: 317px) 100vw, 317px">
    </p>
    <p>
    	打开
        <em>
            Attributes Inspector
        </em>
        。改变
        <em>
            Columns
        </em>
        为3。它是如此地简单！你的table view现在就有了三列。
    </p>
    <p>
    	下一步，因为你想一次操作多个文件，在
    	<em>
            Selection
        </em>
        中勾选
        <em>
            Multiple
        </em>
        。同时在
        <em>
            Highlight
        </em>
        这里勾选
        <em>
            Alternating Rows
        </em>
        。当它打开时，table view就会使用交替的行的背景颜色，就像Finder一样。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-attributes.png"
        alt="configure table attributes" width="261" height="382" class="aligncenter size-full wp-image-145679">
    </p>
    <p>
    	重命名列头，让它更有描述性。在
        <em>
            View Controller场景
        </em>
        中选择第一列。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/configure-column.png"
        alt="configure-column" width="322" height="360" class="aligncenter size-full wp-image-145679"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/configure-column.png 322w, https://koenig-media.raywenderlich.com/uploads/2016/10/configure-column-286x320.png 286w"
        sizes="(max-width: 322px) 100vw, 322px">
    </p>
    <p>
        打开
        <em>
            Attributes Inspector
        </em>
        并改变列的
        <em>
            Title
        </em>
        为
        <em>
            Name
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-changetitle.png">
            <img class="aligncenter size-full wp-image-118863" src="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-changetitle.png"
            alt="change the header title in attributes" width="275" height="266" srcset="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-changetitle.png 275w, https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-changetitle-32x32.png 32w"
            sizes="(max-width: 275px) 100vw, 275px">
        </a>
    </p>
    <p>
    	对于第二列和第三列重复同样的操作，分别改变
        <em>
            Title
        </em>
        为
        <em>
            Modification Date
        </em>
        和
        <em>
            Size
        </em>
		。
    </p>
    <div class="note">
        <p>
            <em>
            	注意
            </em>
            ：这里有一个可供替代的方法来改变列的标题。你可以直接双击table view的header来让它变得可编辑。两条路都可以得到正确的结果，所以按你更喜欢的那种来就可以了。
        </p>
    </div>
    <p>
    	最后，如果你还是不能看到Size这列，选择Modification Date这列并改变Width为200。通过使用你的鼠标来回调整 :]
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/date-column-size-1.png"
        alt="resize modification date if needed" width="260" height="129" class="aligncenter size-full wp-image-145687">
    </p>
    <p>
    	运行项目。这里是你应该看到的：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/post-column-naming.png"
        alt="table with configured headers" width="598" height="253" class="aligncenter size-full wp-image-145677"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/post-column-naming.png 598w, https://koenig-media.raywenderlich.com/uploads/2016/10/post-column-naming-480x203.png 480w"
        sizes="(max-width: 598px) 100vw, 598px">
    </p>
    <h3>
    	改变信息的表现方式
    </h3>
    <p>
    	在当前的状态下，这个table view 有三列，每一列包含一个用text field展示的cell view。
    </p>
    <p>
    	但这有一点乏味。所以加工一下吧，在文件名旁边展示一下它的图标。你的table会在这个小升级之后变得更整洁。
    </p>
    <p>
    	你需要用一个包含image和text field的新的cell来替换第一列的cell view。
    </p>
    <p>
    	你是幸运的，因为Interface Builder拥有这种内建类型的cell。
    </p>
    <p>
    	在
    	<em>
            Name
        </em>
        这列中选择
        <em>
            Table Cell View
        </em>
        ，并删除它。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/delete-this-view-1.png"
        alt="delete this view" width="301" height="257" class="aligncenter size-full wp-image-145802">
    </p>
    <p>
    	打开
        <em>
            Object Library
        </em>
        并将一个
        <em>
            Image &amp; Text Table Cell View
        </em>
        拖拽到table view的第一列或
        <em>
            View Controller Scene
        </em>
        的“树”中，就在
        <em>
            Name
        </em>
        这个table view的列下面.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/set-name-cell.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/set-name-cell-650x399.png"
            alt="add a new cell type in interface builder" width="650" height="399"
            class="aligncenter size-large wp-image-145676" srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/set-name-cell-650x399.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/set-name-cell-480x295.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/10/set-name-cell.png 1464w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
    	现在你就把它打造成型了！
    </p>
    <h3>
        设定Identifier
    </h3>
    <p>
    	每个cell类型都需要有一个被设定的identifier。否则，当你coding时就无法根据指定的列来创建cell view了。
    </p>
    <p>
    	选择第一列的cell view，在
        <em>
            Identity Inspector
        </em>
        中，改变
        <em>
            Identifier
        </em>
        为
        <em>
            NameCellID
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-identifier.png">
            <img class="aligncenter size-full wp-image-118867" src="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-identifier.png"
            alt="edit column identifiers" width="274" height="181">
        </a>
    </p>
    <p>
    	在第二列及第三列中的cell view上重复同样的操作，分别命名为
    	<em>
            DateCellID
        </em>
        和
        <em>
            SizeCellID
        </em>
        。
    </p>
    <h2>
	    填充table view
    </h2>
    <div class="note">
        <em>
	        注意：
        </em>
        你有两种方法可以填充tableview：一种使用datasource和delegate协议，你将在这个教程中看到它们；另一种通过
        <a href="https://www.raywenderlich.com/141297/cocoa-bindings-macos" target="_blank">
            Cocoa bindings
        </a>
        来完成。这两种技术不是互斥的，你可以同时使用他们来得到你想要的。
    </div>
    <p>
    	这个table view当前并不知道你需要展示的数据，和怎么来展示，但这确实需要形成回路。所以你要实现这两个协议来提供这些信息：
    </p>
    <ul>
        <li>
            <code>
                NSTableViewDataSource
            </code>
            ：告诉table view有多少行需要展示。
        </li>
        <li>
            <code>
                NSTableViewDelegate
            </code>
            ：提供将要展示在指定行和列上的view cell。
        </li>
    </ul>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/population-diagram1.png">
            <img class="aligncenter size-large wp-image-118891" src="https://koenig-media.raywenderlich.com/uploads/2015/10/population-diagram1-700x394.png"
            alt="population flow of a table view" width="700" height="394" srcset="https://koenig-media.raywenderlich.com/uploads/2015/10/population-diagram1-700x394.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/10/population-diagram1-480x270.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/10/population-diagram1-266x151.png 266w, https://koenig-media.raywenderlich.com/uploads/2015/10/population-diagram1.png 701w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
    	这个形象化的过程是关于table view，delegate和data source之间的协作：
    </p>
    <ol>
        <li>
        	这个table view调用data source的方法
            <code>
                numberOfRows(in:)
            </code>
            ，它会返回table将要展示的行的数量。
        </li>
        <li>
        	这个table view为每一行和列调用delegate的方法
            <code>
                tableView(\_:viewFor:row:)
            </code>
            。delegate会创建这个位置上的view，并用恰当的数据填充它，然后返回给table view。
        </li>
    </ol>
    <p>
    	为了在table view中展示你的数据，两个方法都必须实现。
    </p>
    <p>
    	在
    	<em>
            Assistant editor
        </em>
    	中打开
	    <em>
            ViewController.swift
        </em>
        并
        <em>
        	按住control拖拽
        </em>
		table view到
	    <code>
            ViewController
        </code>
        类的实现中来插入一个outlet。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/add-outlet.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/add-outlet-650x228.png"
            alt="add an outlet to the tableview" width="650" height="228" class="aligncenter size-large wp-image-145674"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/add-outlet-650x228.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/add-outlet-480x168.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/10/add-outlet.png 1197w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
    	确认
        <em>
            Type
        </em>
        为
        <em>
            NSTableView
        </em>
		，                
        <em>
            Connection
        </em>
        为
        <em>
            Outlet
        </em>
        。将outlet命名为：
        <code>
            tableView
        </code>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-outlet-22.png">
            <img class="aligncenter size-full wp-image-118921" src="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-outlet-22.png"
            alt="define the outlet" width="263" height="154">
        </a>
    </p>
    <p>
    	你现在就可以在代码中使用outlet引用table view了。
    </p>
    <p>
        切回到
        <em>
            Standard Editor
        </em>
        ，并打开
        <em>
            ViewController.swift
        </em>
        。通过添加这些代码到
        <code>
            ViewController
        </code>
        类的最后来实现提供数据源的方法：
    </p>
    <pre class="swift" style="font-family:monospace;">extension ViewController<span style="color: #002200;">:</span> NSTableViewDataSource <span style="color: #002200;">{</span>
&nbsp;
  <span style="color: #a61390;">func</span> numberOfRows<span style="color: #002200;">(</span><span style="color: #a61390;">in</span> tableView<span style="color: #002200;">:</span> <span style="color: #400080;">NSTableView</span><span style="color: #002200;">)</span> <span style="color: #002200;">-</span>&gt; <span style="color: #a61390;">Int</span> <span style="color: #002200;">{</span>
    <span style="color: #a61390;">return</span> directoryItems?.<span style="color: #a61390;">count</span> ?? <span style="color: #2400d9;">0</span>
  <span style="color: #002200;">}</span>
&nbsp;
<span style="color: #002200;">}</span></pre>
    <p>
    	这创建了一个遵守
    	<code>
            NSTableViewDataSource
        </code>
    	协议的extension，并实现了要求的方法
        <code>
            numberOfRows(in:)
        </code>
        来返回目录中文件的数量，它就是
        <code>
            directoryItems
        </code>
        数组的大小。
    </p>
    <p>
    	现在你需要实现delegate。添加下列的extension到
        <em>
            ViewController.swift
        </em>
        的最后：
    </p>
    <pre class="swift" style="font-family:monospace;">extension ViewController<span style="color: #002200;">:</span> NSTableViewDelegate <span style="color: #002200;">{</span>
&nbsp;
  fileprivate <span style="color: #a61390;">enum</span> CellIdentifiers <span style="color: #002200;">{</span>
    <span style="color: #a61390;">static</span> <span style="color: #a61390;">let</span> NameCell <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"NameCellID"</span>
    <span style="color: #a61390;">static</span> <span style="color: #a61390;">let</span> DateCell <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"DateCellID"</span>
    <span style="color: #a61390;">static</span> <span style="color: #a61390;">let</span> SizeCell <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"SizeCellID"</span>
  <span style="color: #002200;">}</span>
&nbsp;
  <span style="color: #a61390;">func</span> tableView<span style="color: #002200;">(</span>_ tableView<span style="color: #002200;">:</span> <span style="color: #400080;">NSTableView</span>, viewFor tableColumn<span style="color: #002200;">:</span> <span style="color: #400080;">NSTableColumn</span>?, row<span style="color: #002200;">:</span> <span style="color: #a61390;">Int</span><span style="color: #002200;">)</span> <span style="color: #002200;">-</span>&gt; <span style="color: #400080;">NSView</span>? <span style="color: #002200;">{</span>
&nbsp;
    <span style="color: #a61390;">var</span> image<span style="color: #002200;">:</span> <span style="color: #400080;">NSImage</span>?
    <span style="color: #a61390;">var</span> text<span style="color: #002200;">:</span> <span style="color: #a61390;">String</span> <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">""</span>
    <span style="color: #a61390;">var</span> cellIdentifier<span style="color: #002200;">:</span> <span style="color: #a61390;">String</span> <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">""</span>
&nbsp;
    <span style="color: #a61390;">let</span> dateFormatter <span style="color: #002200;">=</span> DateFormatter<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
    dateFormatter.dateStyle <span style="color: #002200;">=</span> .long
    dateFormatter.timeStyle <span style="color: #002200;">=</span> .long
&nbsp;
    <span style="color: #11740a; font-style: italic;">// 1</span>
    guard <span style="color: #a61390;">let</span> item <span style="color: #002200;">=</span> directoryItems?<span style="color: #002200;">[</span>row<span style="color: #002200;">]</span> <span style="color: #a61390;">else</span> <span style="color: #002200;">{</span>
      <span style="color: #a61390;">return</span> <span style="color: #a61390;">nil</span>
    <span style="color: #002200;">}</span>
&nbsp;
    <span style="color: #11740a; font-style: italic;">// 2</span>
    <span style="color: #a61390;">if</span> tableColumn <span style="color: #002200;">==</span> tableView.tableColumns<span style="color: #002200;">[</span><span style="color: #2400d9;">0</span><span style="color: #002200;">]</span> <span style="color: #002200;">{</span>
      image <span style="color: #002200;">=</span> item.icon
      text <span style="color: #002200;">=</span> item.name
      cellIdentifier <span style="color: #002200;">=</span> CellIdentifiers.NameCell
    <span style="color: #002200;">}</span> <span style="color: #a61390;">else</span> <span style="color: #a61390;">if</span> tableColumn <span style="color: #002200;">==</span> tableView.tableColumns<span style="color: #002200;">[</span><span style="color: #2400d9;">1</span><span style="color: #002200;">]</span> <span style="color: #002200;">{</span>
      text <span style="color: #002200;">=</span> dateFormatter.string<span style="color: #002200;">(</span>from<span style="color: #002200;">:</span> item.date<span style="color: #002200;">)</span>
      cellIdentifier <span style="color: #002200;">=</span> CellIdentifiers.DateCell
    <span style="color: #002200;">}</span> <span style="color: #a61390;">else</span> <span style="color: #a61390;">if</span> tableColumn <span style="color: #002200;">==</span> tableView.tableColumns<span style="color: #002200;">[</span><span style="color: #2400d9;">2</span><span style="color: #002200;">]</span> <span style="color: #002200;">{</span>
      text <span style="color: #002200;">=</span> item.isFolder ? <span style="color: #bf1d1a;">"--"</span> <span style="color: #002200;">:</span> sizeFormatter.string<span style="color: #002200;">(</span>fromByteCount<span style="color: #002200;">:</span> item.size<span style="color: #002200;">)</span>
      cellIdentifier <span style="color: #002200;">=</span> CellIdentifiers.SizeCell
    <span style="color: #002200;">}</span>
&nbsp;
    <span style="color: #11740a; font-style: italic;">// 3</span>
    <span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> cell <span style="color: #002200;">=</span> tableView.make<span style="color: #002200;">(</span>withIdentifier<span style="color: #002200;">:</span> cellIdentifier, owner<span style="color: #002200;">:</span> <span style="color: #a61390;">nil</span><span style="color: #002200;">)</span> <span style="color: #a61390;">as?</span> NSTableCellView <span style="color: #002200;">{</span>
      cell.textField?.stringValue <span style="color: #002200;">=</span> text
      cell.imageView?.image <span style="color: #002200;">=</span> image ?? <span style="color: #a61390;">nil</span>
      <span style="color: #a61390;">return</span> cell
    <span style="color: #002200;">}</span>
    <span style="color: #a61390;">return</span> <span style="color: #a61390;">nil</span>
  <span style="color: #002200;">}</span>
&nbsp;
<span style="color: #002200;">}</span></pre>
    <p>
    	这个代码声明了一个遵守
        <code>
            NSTableViewDelegate
        </code>
        协议的extension，并实现了方法
        <code>
            tableView(\_:viewFor:row)
        </code>
        。它接下来会被table view的每一行和每一列调用，来得到恰当的cell。
    </p>
    <p>
    	这个方法中还有很多需要做的事，这里有一个一步步的项（breakdown）：
    </p>
    <ol>
        <li>
        	如果没有数据要展示，它应该不返回cell。
        </li>
        <li>
        	基于cell将要展示的列（Name，Date或Size），它要设置cell identifier，文本和图像。
        </li>
        <li>
        	它通过调用
            <code>
                make(withIdentifier:owner:)
            </code>
            来得到一个cell。这个方法通过那个identifier来创建或复用一个cell，然后使用之前一步提供的数据来填充它，并返回。
        </li>
    </ol>
    <p>
    	接下来，在
        <code>
            viewDidLoad()
        </code>
        中添加这个代码：
    </p>
    <pre class="swift" style="font-family:monospace;">tableView.delegate <span style="color: #002200;">=</span> <span style="color: #a61390;">self</span>
tableView.dataSource <span style="color: #002200;">=</span> <span style="color: #a61390;">self</span></pre>
    <p>
    	这里你告诉table view它的data source和delegate是这个view controller。
    </p>
    <p>
    	最后一步是当一个新的目录被选中时，告诉tableview刷新数据。
    </p>
    <p>
    	首先，添加这个方法到
        <code>
            ViewController
        </code>
        的实现中：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">func</span> reloadFileList<span style="color: #002200;">(</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
  directoryItems <span style="color: #002200;">=</span> directory?.contentsOrderedBy<span style="color: #002200;">(</span>sortOrder, ascending<span style="color: #002200;">:</span> sortAscending<span style="color: #002200;">)</span>
  tableView.reloadData<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
<span style="color: #002200;">}</span></pre>
    <p>
    	这个助手方法可以更新文件的列表。
    </p>
    <p>
    	首先，它调用了
        <code>
            directory
        </code>
        的方法
        <code>
            contentsOrderedBy(\_:ascending)
        </code>
        ，并返回了一个包含目录文件的有序的数组。然后调用了table view的方法
        <code>
            reloadData()
        </code>
        来告诉它进行刷新。
    </p>
    <p>
    	注意你仅需要在一个新的目录被选中时调用这个方法。
    </p>
    <p>
    	来到
        <code>
            representedObject
        </code>
        的观察者
        <code>
            didSet
        </code>
        中，替换这行代码：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">print</span><span style="color: #002200;">(</span><span style="color: #bf1d1a;">"Represented object: <span style="color: #2400d9;">\(</span>url)"</span><span style="color: #002200;">)</span></pre>
    <p>
    	为：
    </p>
    <pre class="swift" style="font-family:monospace;">directory <span style="color: #002200;">=</span> Directory<span style="color: #002200;">(</span>folderURL<span style="color: #002200;">:</span> url<span style="color: #002200;">)</span>
reloadFileList<span style="color: #002200;">(</span><span style="color: #002200;">)</span></pre>
    <p>
    	你刚创建了一个
        <code>
            Directory
        </code>
        的示例，指向目录的URL，它调用
        <code>
            reloadFileList()
        </code>
        方法来更新table view的数据。
    </p>
    <p>
        运行项目。
    </p>
    <p>
        使用菜单上的
        <em>
            File &gt; Open…
        </em>
        或
        <em>
            Command+O
        </em>
        快捷键来打开一个目录，观察魔法的发生！现在table已经被你刚选择目录的内容填满了。调整列的大小来查看每一个文件或目录的所有信息。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/table-first-population.png"
        alt="your table now shows content" width="560" height="291" class="aligncenter size-full wp-image-145756"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/table-first-population.png 560w, https://koenig-media.raywenderlich.com/uploads/2016/10/table-first-population-480x249.png 480w"
        sizes="(max-width: 560px) 100vw, 560px">
    </p>
    <p>
        Nice job!
    </p>
    <h2>
    	table view的交互
    </h2>
    <p>
    	在这一部分，你将与一些交互共事，来提升UI。
    </p>
    <h3>
    	响应用户的选择
    </h3>
    <p>
    	当用户选择了一个或多个文件，这个应用应当更新底部栏的信息，来展示目录中文件的个数，以及被选中的个数。
    </p>
    <p>
    	为了在选择发生变化时收到通知，你需要在delegate中实现
        <code>
            tableViewSelectionDidChange(\_:)
        </code>
        。这个方法将在table view探测到选择发生变化时被调用。
    </p>
    <p>
    	添加这个代码到
        <em>
            ViewController
        </em>
        的实现中：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">func</span> updateStatus<span style="color: #002200;">(</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
&nbsp;
  <span style="color: #a61390;">let</span> text<span style="color: #002200;">:</span> <span style="color: #a61390;">String</span>
&nbsp;
  <span style="color: #11740a; font-style: italic;">// 1</span>
  <span style="color: #a61390;">let</span> itemsSelected <span style="color: #002200;">=</span> tableView.selectedRowIndexes.<span style="color: #a61390;">count</span>
&nbsp;
  <span style="color: #11740a; font-style: italic;">// 2</span>
  <span style="color: #a61390;">if</span> <span style="color: #002200;">(</span>directoryItems <span style="color: #002200;">==</span> <span style="color: #a61390;">nil</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
    text <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"No Items"</span>
  <span style="color: #002200;">}</span>
  <span style="color: #a61390;">else</span> <span style="color: #a61390;">if</span><span style="color: #002200;">(</span>itemsSelected <span style="color: #002200;">==</span> <span style="color: #2400d9;">0</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
    text <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"<span style="color: #2400d9;">\(</span>directoryItems!.count) items"</span>
  <span style="color: #002200;">}</span>
  <span style="color: #a61390;">else</span> <span style="color: #002200;">{</span>
    text <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"<span style="color: #2400d9;">\(</span>itemsSelected) of <span style="color: #2400d9;">\(</span>directoryItems!.count) selected"</span>
  <span style="color: #002200;">}</span>
  <span style="color: #11740a; font-style: italic;">// 3</span>
  statusLabel.stringValue <span style="color: #002200;">=</span> text
<span style="color: #002200;">}</span></pre>
    <p>
    	这个方法基于用户的选择更新了status label。
    </p>
    <ol>
        <li>
        	table view的属性
            <code>
                selectedRowIndexes
            </code>
            包含了选择的行的序号。要得知有多少项被选择了，只需获取这个array的count。
        </li>
        <li>
        	基于项目的个数，构建了有益的文本字符串。
        </li>
        <li>
        	设置状态label的文本。
        </li>
    </ol>
    <p>
    	现在，你只需要当用户改变了table view的选择时，调用这个方法。在table view的delegate extension中添加下列代码：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">func</span> tableViewSelectionDidChange<span style="color: #002200;">(</span>_ notification<span style="color: #002200;">:</span> Notification<span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
  updateStatus<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
<span style="color: #002200;">}</span></pre>
    <p>
    	当选择改变时，table view就会调用这个方法，然后更新状态文本。
    </p>
    <p>
        运行项目。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/table-selection-label.png"
        alt="selection label now configured" width="606" height="351" class="aligncenter size-full wp-image-145757"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/table-selection-label.png 606w, https://koenig-media.raywenderlich.com/uploads/2016/10/table-selection-label-480x278.png 480w"
        sizes="(max-width: 606px) 100vw, 606px">
    </p>
    <p>
    	自己来试一下；在table view中选择一个或多个文件，并观察情报信息的改变，反映你的选择。
    </p>
    <h3>
    	响应双击
    </h3>
    <p>
    	在macOS中，双击通常意味着用户触发了一个动作，你的程序就需要执行它。
    </p>
    <p>
    	例如，当你正在处理文件，你通常期望双击这个文件来已它默认的应用打开它；对于目录，则你期望查看它的内容。
    </p>
    <p>
    	现在你就要实现双击的响应。
    </p>
    <p>
    	双击的通知不是通过table view的delegate来发送，而是发送一个动作给table view的target。但是为了在view controller中接收到那些通知，你需要设定
        <code>
            target
        </code>
        和
        <code>
            doubleAction
        </code>
        两个属性。
    </p>
    <div class="note">
        <p>
            <em>
            	注意
            </em>
            ：Target-action是一个被大多数Cocoa的控件使用的模式。如果你不熟悉这个模式，你可以在苹果的
            <em>
                Cocoa Application Competencies for macOS
            </em>
            这个文档中学习
            <a title="Target-Action" href="https://developer.apple.com/library/mac/documentation/General/Devpedia-CocoaApp-MOSX/TargetAction.html"
            target="_blank">
                Target-Action
            </a>
            这一部分。
        </p>
    </div>
    <p>
    	在
    	<code>
            ViewController
        </code>
        的
        <code>
            viewDidLoad()
        </code>
        方法中添加下列代码：
    </p>
    <pre class="swift" style="font-family:monospace;">tableView.target <span style="color: #002200;">=</span> <span style="color: #a61390;">self</span>
tableView.doubleAction <span style="color: #002200;">=</span> <span style="color: #6e371a;">#selector(tableViewDoubleClick(\_:))</span></pre>
    <p>
    	这告诉了table view这个view controller将变成它的动作的target，这样这个方法就会在双击后被调用。
    </p>
    <p>
    	添加
        <code>
            tableViewDoubleClick(\_:)
        </code>
        方法的实现：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">func</span> tableViewDoubleClick<span style="color: #002200;">(</span>_ sender<span style="color: #002200;">:</span><span style="color: #a61390;">AnyObject</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
&nbsp;
  <span style="color: #11740a; font-style: italic;">// 1</span>
  guard tableView.selectedRow &gt;<span style="color: #002200;">=</span> <span style="color: #2400d9;">0</span>,     
      <span style="color: #a61390;">let</span> item <span style="color: #002200;">=</span> directoryItems?<span style="color: #002200;">[</span>tableView.selectedRow<span style="color: #002200;">]</span> <span style="color: #a61390;">else</span> <span style="color: #002200;">{</span>
    <span style="color: #a61390;">return</span>
  <span style="color: #002200;">}</span>
&nbsp;
  <span style="color: #a61390;">if</span> item.isFolder <span style="color: #002200;">{</span>
    <span style="color: #11740a; font-style: italic;">// 2</span>
    <span style="color: #a61390;">self</span>.representedObject <span style="color: #002200;">=</span> item.url <span style="color: #a61390;">as</span> <span style="color: #a61390;">Any</span>
  <span style="color: #002200;">}</span>
  <span style="color: #a61390;">else</span> <span style="color: #002200;">{</span>
    <span style="color: #11740a; font-style: italic;">// 3</span>
    <span style="color: #400080;">NSWorkspace</span>.shared<span style="color: #002200;">(</span><span style="color: #002200;">)</span>.open<span style="color: #002200;">(</span>item.url <span style="color: #a61390;">as</span> URL<span style="color: #002200;">)</span>
  <span style="color: #002200;">}</span>
<span style="color: #002200;">}</span></pre>
    <p>
    	这里是上述代码的一步步的分解：
    </p>
    <ol>
        <li>
        	如果table view的选择是空的，它什么都不会做直接返回。同时注意，双击一个table view的空的区域将使得
            <code>
                tableView.selectedRow
            </code>
            的值等于1。
        </li>
        <li>
        	如果是一个目录，它会设置
            <code>
                representedObject
            </code>
            属性为它的URL。然后这个table view会刷新来显示那个目录的内容。
        </li>
        <li>
        	如果这一项是一个文件，它会通过调用
            <code>
                NSWorkspace
            </code>
            的方法
            <code>
                openURL()
            </code>
            来使用默认的应用打开它。
        </li>
    </ol>
    <p>
    	运行项目以检查你的作品。
    </p>
    <p>
    	双击任何文件并观察它是怎么用默认的应用打开的。现在，选择一个目录并观察table view怎么更新及展示那个目录的内容。
    </p>
    <p>
        咳，稍等，你只是创造了一个DIY版本的Finder？确实看起来是这样！
    </p>
    <h3>
        数据排序
    </h3>
    <p>
    	每个人都喜欢好的排序，在这一部分你将学习怎么基于用户的选择给table view排序。
    </p>
    <p>
    	table最好的特性之一，就是通过单击或双击指定的一列来排序。单击会以升序排列，双击则以降序排列。
    </p>
    <p>
    	实现这个特定的UI是非常容易的，因为
        <code>
            NSTableView
        </code>
        打包了大多数直接“开箱即用”（out of the box）的功能。
    </p>
    <p>
        <em>
            Sort descriptors
        </em>
        是你用来处理这个的
        <code>
            NSSortDescriptor
        </code>
        类的简单的实例，它指定了要求的属性并排序。
    </p>
    <p>
    	在设置descriptor之后，将会发生：点击table view的一个列头，将通知你，通过代理，哪个属性将被使用，用户就能够给数据排序。
    </p>
    <p>
    	一旦你设置了sort descriptor，table view就会提供全部的UI来处理排序，像是可点击的header，箭头，以及哪个sort descriptor被选择了的通知。然而，基于那些信息排序，然后刷新table view来反映新的顺序是你的责任。
    </p>
    <p>
    	现在你将学到怎么去做：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/Screen-Shot-2015-11-29-at-6.24.36-PM.png">
            <img class="aligncenter size-full wp-image-121566" src="https://koenig-media.raywenderlich.com/uploads/2015/11/Screen-Shot-2015-11-29-at-6.24.36-PM.png"
            alt="Woot!" width="294" height="299" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/Screen-Shot-2015-11-29-at-6.24.36-PM.png 294w, https://koenig-media.raywenderlich.com/uploads/2015/11/Screen-Shot-2015-11-29-at-6.24.36-PM-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/11/Screen-Shot-2015-11-29-at-6.24.36-PM-64x64.png 64w"
            sizes="(max-width: 294px) 100vw, 294px">
        </a>
    </p>
    <p>    
        在
        <code>
            viewDidLoad()
        </code>
        中添加下列代码来创建sort descriptor:
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #11740a; font-style: italic;">// 1</span>
<span style="color: #a61390;">let</span> descriptorName <span style="color: #002200;">=</span> <span style="color: #400080;">NSSortDescriptor</span><span style="color: #002200;">(</span>key<span style="color: #002200;">:</span> Directory.FileOrder.Name.rawValue, ascending<span style="color: #002200;">:</span> <span style="color: #a61390;">true</span><span style="color: #002200;">)</span>
<span style="color: #a61390;">let</span> descriptorDate <span style="color: #002200;">=</span> <span style="color: #400080;">NSSortDescriptor</span><span style="color: #002200;">(</span>key<span style="color: #002200;">:</span> Directory.FileOrder.Date.rawValue, ascending<span style="color: #002200;">:</span> <span style="color: #a61390;">true</span><span style="color: #002200;">)</span>
<span style="color: #a61390;">let</span> descriptorSize <span style="color: #002200;">=</span> <span style="color: #400080;">NSSortDescriptor</span><span style="color: #002200;">(</span>key<span style="color: #002200;">:</span> Directory.FileOrder.Size.rawValue, ascending<span style="color: #002200;">:</span> <span style="color: #a61390;">true</span><span style="color: #002200;">)</span>
&nbsp;
<span style="color: #11740a; font-style: italic;">// 2</span>
tableView.tableColumns<span style="color: #002200;">[</span><span style="color: #2400d9;">0</span><span style="color: #002200;">]</span>.sortDescriptorPrototype <span style="color: #002200;">=</span> descriptorName
tableView.tableColumns<span style="color: #002200;">[</span><span style="color: #2400d9;">1</span><span style="color: #002200;">]</span>.sortDescriptorPrototype <span style="color: #002200;">=</span> descriptorDate
tableView.tableColumns<span style="color: #002200;">[</span><span style="color: #2400d9;">2</span><span style="color: #002200;">]</span>.sortDescriptorPrototype <span style="color: #002200;">=</span> descriptorSize</pre>
    <p>
    	这个代码做了下面的事：
    </p>
    <ol>
        <li>
        	为每一列创建sort descriptor，使用一个键(Name，Date或Size)来完成，它指示了可以让文件列表被排序的那个属性。
        </li>
        <li>
        	通过设置
        	<code>
                sortDescriptorPrototype
            </code>
        	属性，为每一列添加sort descriptor。
        </li>
    </ol>
    <p>
    	当用户点击任一列头时，这个table view会调用data source的方法
        <code>
            tableView(\_:sortDescriptorsDidChange:)
        </code>
        ，app就会基于提供的descriptor来进行排序。
    </p>
    <p>
    	添加下列的代码到data source的extension中：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">func</span> tableView<span style="color: #002200;">(</span>_ tableView<span style="color: #002200;">:</span> <span style="color: #400080;">NSTableView</span>, sortDescriptorsDidChange oldDescriptors<span style="color: #002200;">:</span> <span style="color: #002200;">[</span><span style="color: #400080;">NSSortDescriptor</span><span style="color: #002200;">]</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
  <span style="color: #11740a; font-style: italic;">// 1</span>
  guard <span style="color: #a61390;">let</span> sortDescriptor <span style="color: #002200;">=</span> tableView.sortDescriptors.first <span style="color: #a61390;">else</span> <span style="color: #002200;">{</span>
    <span style="color: #a61390;">return</span>
  <span style="color: #002200;">}</span>
  <span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> order <span style="color: #002200;">=</span> Directory.FileOrder<span style="color: #002200;">(</span>rawValue<span style="color: #002200;">:</span> sortDescriptor.key<span style="color: #002200;">!</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
    <span style="color: #11740a; font-style: italic;">// 2</span>
    sortOrder <span style="color: #002200;">=</span> order
    sortAscending <span style="color: #002200;">=</span> sortDescriptor.ascending
    reloadFileList<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
  <span style="color: #002200;">}</span>
<span style="color: #002200;">}</span></pre>
    <p>
    	这个代码做了这些事：
    </p>
    <ol>
        <li>
        	获取符合用户点击的列头的第一个sort descriptor。
        </li>
        <li>
        	给view controller的
            <code>
                sortOrder
            </code>
            和
            <code>
                sortAscending
            </code>
            属性赋值，然后调用
            <code>
                reloadFileList()
            </code>
            。你提早设置它来获取一个已排好序的文件的列表，并告诉table view来重载数据。
        </li>
    </ol>
    <p>
    	运行项目。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/sortable-columns.png"
        alt="sortable-columns" width="619" height="298" class="aligncenter size-full wp-image-145673"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/sortable-columns.png 619w, https://koenig-media.raywenderlich.com/uploads/2016/10/sortable-columns-480x231.png 480w"
        sizes="(max-width: 619px) 100vw, 619px">
    </p>
    <p>
	    点击任一header来查看你的table view排序数据。再次点击相同的header来在升序和降序之间切换。
    </p>
    <p>
    	你已经使用table view构建了一个很好的文件查看器。恭喜！
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
	    你可以在
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/FileViewer_final2.zip">
            这里
        </a>
        下载完整版本的项目。
    </p>
    <p>
    	这个macOS NSTableView教程覆盖了相当多的内容，你现在应当感到更多的自信，来以你的能力使用table view来组织数据。除此以外，你还学到了：
    </p>
    <ul>
        <li>
        	table view的基本结构，包括header、row、column和cell的单独的特质。
        </li>
        <li>
        	怎样添加列来展示更多的数据。
        </li>
        <li>
        	怎么为之后的引用鉴别多种元件。
        </li>
        <li>
        	怎样在table中加载数据。
        </li>
        <li>
        	怎样响应各种用户交互。
        </li>
    </ul>
    <p>
    	这里有更多你可以使用table view来做的事，让你可以为你的app构建高雅的UI。如果你想要关于它更多的内容，可以参考下列资源：
    </p>
    <ul>
        <li>
            苹果的
            <a title="Table View Programming Guide for Mac" href="https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/TableView/Introduction/Introduction.html"
            target="_blank">
                Table View Programming Guide for Mac
            </a>
            .
        </li>
        <li>
            WWDC 2016 – Session 239 Video –
            <a href="https://developer.apple.com/videos/play/wwdc2016/239/" target="_blank">
                Crafting Modern Cocoa Apps
            </a>
            中的一个关于怎样构建一个切掉边的（cutting edge）table view的快速教程。
        </li>
        <li>
            WWDC 2011 – Session 120 Video
            <a title="View Based NSTableView Basic to Advanced " href="https://developer.apple.com/videos/play/wwdc2011-120/"
            target="_blank">
                View Based NSTableView Basic to Advanced
            </a>
            .
        </li>
        <li>
            <a title="TableViewPlayGround" href="https://developer.apple.com/library/mac/samplecode/TableViewPlayground/Introduction/Intro.html#//apple_ref/doc/uid/DTS40010727"
            target="_blank">
                TableViewPlayGround
            </a>
            中有OC的示例代码来展示怎样创建不同种的定制的table view。
        </li>
    </ul>
</div>
