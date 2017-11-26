# macOS教程：NSOutlineView

#### [原文地址](https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div class="note">
        <p>
            <em>
                更新于2016年9月30日：
            </em>
            本教程已适配Xcode 8及Swift 3。
        </p>
    </div>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature-250x250.png"
        alt="NSOutlineView-feature" width="250" height="250" class="alignright size-thumbnail wp-image-126006"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
        当编写app的时候，你会经常想以一个类似列表的结构来展示数据。例如，你想要展示一个食谱的列表，这可以很容易地使用
        <code>
            NSTableView
        </code>
        完成。但如果你想依据开胃菜或主要成分对食谱进行分组呢？现在你遇到了问题，因为table view不能进行分组。上图展示了设想中的分级食谱，只可惜我们还不会做！
    </p>
    <p>
        幸好，
        <code>
            NSOutlineView
        </code>
        提供了更多的功能。
        <code>
            NSOutlineView
        </code>
        是macOS中的一个常用组件，且它是
        <code>
            NSTableView
        </code>
        的子类。和table view一样，它也用行和列来展示内容；有所不同的是，它使用分层的数据结构。
    </p>
    <p>
        来实际地看一下outline view吧，打开一个已存在的工程，查看你的project navigator。项目名称的旁边有一个小三角形，你可以用它来将项目展开。如下图所示：在项目的下发就是分组，各组的内部则是Swift或Objective-C文件。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Outline_Xcode.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Outline_Xcode.png"
            alt="Xcode's Outline View" width="242" height="228" class="aligncenter size-full wp-image-123488"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Outline_Xcode.png 484w, https://koenig-media.raywenderlich.com/uploads/2015/12/Outline_Xcode-340x320.png 340w"
            sizes="(max-width: 242px) 100vw, 242px">
        </a>
    </p>
    <p>
        在本教程中，你将学到如何使用outline view来展示你分级的数据。你将会编写一个RSS阅读器 - 从文件中加载出RSS的信息流，并将其展示到outline view上。 
    </p>
    <h2>
        入门
    </h2>
    <p>
        从
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/Reader_Starter.zip"
        sl-processed="1">
            这里
        </a>
        下载起始的项目。打开项目来看一下吧。除了由模板创建的文件外，还有一个
        <em>
            Feeds.plist
        </em>
        ，你将从这里加载信息流。你需要在之后创建model类的时候进一步查看这个文件。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        来查看预备好的UI。左边是一个普通的outline view，旁边则是一个空白的区域，它是一个web view。上述内容使用了一个水平布局的stack view，它被固定到窗口的边缘。Stack view是处理自动布局最新和最后的方式，如果你到现在还未尝试过，你可以在
        <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/OS%20X%20Stack%20Views%20with%20NSStackView.md"
        sl-processed="1">
            这里
        </a>
        进行学习。
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/starter_ui-2"
        rel="attachment wp-att-124504" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Starter_UI-480x302.png"
            alt="Starter UI" width="480" height="302" class="aligncenter size-medium wp-image-124504"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Starter_UI-480x302.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Starter_UI-768x483.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/Starter_UI-700x440.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/Starter_UI.png 1564w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        你的第一个任务就是完成UI。双击header，来将第一列的标题修改为
        <em>
            Feed
        </em>
        ；第二列的标题则修改为
        <em>
            Date
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Header.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Header.png"
            alt="Change_Header" width="318" height="153" class="aligncenter size-full wp-image-123490"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Header.png 636w, https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Header-480x231.png 480w"
            sizes="(max-width: 318px) 100vw, 318px">
        </a>
    </p>
    <p>
        非常得容易！现在在document outline中选择outline view - 你可以在
        <em>
            Bordered Scroll View – Outline View / Clip View / Outline View
        </em>
        下找到它。在
        <em>
            Attributes Inspector
        </em>
        中，将
        <em>
            Indentation
        </em>
        修改为5，打开
        <em>
            Floats Group Rows
        </em>
        并关闭
        <em>
            Reordering
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/01/nsoutline-inspector-new.png"
        rel="attachment wp-att-124331" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/nsoutline-inspector-new-296x320.png"
            alt="nsoutline-inspector-new" width="296" height="320" class="aligncenter size-medium wp-image-124331"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/nsoutline-inspector-new-296x320.png 296w, https://koenig-media.raywenderlich.com/uploads/2016/01/nsoutline-inspector-new.png 463w"
            sizes="(max-width: 296px) 100vw, 296px">
        </a>
    </p>
    <p>
        在左侧的document outline中，点击
        <em>
            Outline View
        </em>
        旁边的三角形来展开它。为
        <em>
            Feed
        </em>
        和
        <em>
            Date
        </em>
        执行同样的操作。选择
        <em>
            Date
        </em>
        下的Table View Cell。
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/date_selection"
        rel="attachment wp-att-124505" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Date_Selection-468x320.png"
            alt="Date_Selection" width="234" height="160" class="aligncenter size-medium wp-image-124505"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Date_Selection-468x320.png 468w, https://koenig-media.raywenderlich.com/uploads/2016/01/Date_Selection.png 638w"
            sizes="(max-width: 234px) 100vw, 234px">
        </a>
    </p>
    <p>        
        在
        <em>
            Identity Inspector
        </em>
        中将
        <em>
            Identifier
        </em>
        修改为
        <em>
            DateCell
        </em>
        。
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/change_cell_identifier-2"
        rel="attachment wp-att-124506" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Change_Cell_Identifier-480x301.png"
            alt="Change_Cell_Identifier" width="480" height="301" class="aligncenter size-medium wp-image-124506"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Change_Cell_Identifier-480x301.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Change_Cell_Identifier.png 530w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        现在切换到
        <em>
            Size Inspector
        </em>
        并将
        <em>
            Width
        </em>
        修改为102。为Feed下的cell重复同样的步骤，将
        <em>
            Identifier
        </em>
        修改为
        <em>
            FeedCell
        </em>
        ，
        <em>
            Width
        </em>
        修改为。
    </p>
    <p>
        展开feed下的cell并选择名为
        <em>
            Table View Cell
        </em>
        的text field。
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/selected_textfield"
        rel="attachment wp-att-124507" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Selected_Textfield.png"
            alt="Selected_Textfield" width="438" height="190" class="aligncenter size-full wp-image-124507">
        </a>
    </p>
    <p>
        使用自动布局工具栏中的Pin和Align菜单，来添加一个2点leading的约束，以及另一个将text field垂直居中的约束。你可以在
        <em>
            Size Inspector
        </em>
        中查看被添加的约束：
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/constraints-5"
        rel="attachment wp-att-124508" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Constraints-480x163.png"
            alt="Constraints" width="480" height="163" class="aligncenter size-medium wp-image-124508"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Constraints-480x163.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Constraints.png 490w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        现在再次选择table cell（就在布局层级中text field的上方）。按下
        <em>
            Cmd + C
        </em>
        和
        <em>
            Cmd + V
        </em>
        键对它进行复制，然后将副本的        
        <em>
            Identifier
        </em>
        修改为
        <em>
            FeedItemCell
        </em>
        。现在你就有了3个不同的cell，每个类型的cell都会被展示在outline view中。
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/finishedcells"
        rel="attachment wp-att-124510" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/FinishedCells.png"
            alt="FinishedCells" width="468" height="304" class="aligncenter size-full wp-image-124510">
        </a>
    </p>
    <p>
        选择
        <em>
            Date
        </em>
        ，并在
        <em>
            Identity Inspector
        </em>
        中将Identifier修改为
        <em>
            DateColumn
        </em>
        ；为
        <em>
            Feed
        </em>
        执行相同的操作将Identifier修改为
        <em>
            TitleColumn
        </em>
        ：
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/titlecolumn"
        rel="attachment wp-att-124512" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/TitleColumn-480x255.png"
            alt="TitleColumn" width="480" height="255" class="aligncenter size-medium wp-image-124512"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/TitleColumn-480x255.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/TitleColumn.png 512w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        最后的一步是给outline view设置一个delegate和data source。选择outline view并右击或按住control点击它，从
        <em>
            dataSource
        </em>
        拖拽一个到代表你的view controller的
        <em>
            蓝色圆圈
        </em>
        上；重复类似的步骤来设置delegate。
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/add_delegate"
        rel="attachment wp-att-123505" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Add_Delegate-480x202.png"
            alt="Add_Delegate" width="480" height="202" class="aligncenter size-medium wp-image-123505"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Add_Delegate-480x202.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Add_Delegate-700x294.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/12/Add_Delegate.png 1172w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        运行项目，你将会看到...
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/first_run-5"
        rel="attachment wp-att-123493" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/First_Run-480x318.png"
            alt="First_Run" width="480" height="318" class="aligncenter size-medium wp-image-123493"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/First_Run-480x318.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/First_Run-700x464.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        只有一个空空的outline view，和你控制台中的错误信息，说你的data source是非法的。What’s wrong？
    </p>
    <p>
        在你填充outline view并解除错误信息之前，你需要一个data model。
    </p>
    <h2>
        Data Model
    </h2>
    <p>
        outline view的数据结构和table view中的有所不同。就像在介绍中提到的，outline view展示的是分层级的数据模型，你的模型类必须能够代表这个层级。每个层级都要有一个顶层或根对象。这里，它就RSS的信息流；feed的名称就是根。
    </p>
    <p>
        按
        <em>
            Cmd + N
        </em>
        键来创建一个新的类。在
        <em>
            macOS
        </em>
        部分中选择
        <em>
            Cocoa Class
        </em>
        并点击
        <em>
            Next
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/New_File_Template.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/New_File_Template-449x320.png"
            alt="New_File_Template" width="449" height="320" class="aligncenter size-medium wp-image-145290"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/New_File_Template-449x320.png 449w, https://koenig-media.raywenderlich.com/uploads/2016/04/New_File_Template-650x463.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/04/New_File_Template.png 1460w"
            sizes="(max-width: 449px) 100vw, 449px">
        </a>
    </p>
    <p>
        将这个类命名为
        <code>
            Feed
        </code>
        ，且让它成为
        <code>
            NSObject
        </code>
        的子类。然后点击
        <em>
            Next
        </em>
        ，下一页中则点击
        <em>
            Create
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Create_Feed_Class_2.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Create_Feed_Class_2-700x497.png"
            alt="Create_Feed_Class_2" width="350" height="248" class="aligncenter size-large wp-image-123495"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Create_Feed_Class_2-700x497.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/12/Create_Feed_Class_2-451x320.png 451w, https://koenig-media.raywenderlich.com/uploads/2015/12/Create_Feed_Class_2.png 1462w"
            sizes="(max-width: 350px) 100vw, 350px">
        </a>
    </p>
    <p>
        将自动生成的代码替换为：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">import</span> Cocoa

<span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">Feed</span>: <span class="hljs-title">NSObject</span> </span>{
   <span class="hljs-keyword">let</span> name: <span class="hljs-type">String</span>
       
   <span class="hljs-keyword">init</span>(name: <span class="hljs-type">String</span>) {
     <span class="hljs-keyword">self</span>.name = name
   }
}
</pre>
    <p>
        上述代码为你的类添加了一个名为
        <code>
            name
        </code>
        的property，以及一个方便设备此property的初始化分发。你的类会将它的“孩子”储存到一个数组中，但在你这么做之前，你需要创建一个类作为这个“孩子”。和之前的步骤一样，添加一个新名为
        <code>
            FeedItem
        </code>
        的类。打开新建的
        <em>
            FeedItem.swift
        </em>
        文件，并将其内容替换为：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">import</span> Cocoa

<span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">FeedItem</span>: <span class="hljs-title">NSObject</span> </span>{
  <span class="hljs-keyword">let</span> url: <span class="hljs-type">String</span>
  <span class="hljs-keyword">let</span> title: <span class="hljs-type">String</span>
  <span class="hljs-keyword">let</span> publishingDate: <span class="hljs-type">Date</span>
	  
  <span class="hljs-keyword">init</span>(dictionary: <span class="hljs-type">NSDictionary</span>) {
    <span class="hljs-keyword">self</span>.url = dictionary.object(forKey: <span class="hljs-string">"url"</span>) <span class="hljs-keyword">as</span>! <span class="hljs-type">String</span>
    <span class="hljs-keyword">self</span>.title = dictionary.object(forKey: <span class="hljs-string">"title"</span>) <span class="hljs-keyword">as</span>! <span class="hljs-type">String</span>
    <span class="hljs-keyword">self</span>.publishingDate = dictionary.object(forKey: <span class="hljs-string">"date"</span>) <span class="hljs-keyword">as</span>! <span class="hljs-type">Date</span>
  }
}
</pre>
    <p>
        这是另一个简答的模型类：
        <code>
            FeedItem
        </code>
        ，它包含一个
        <code>
            url
        </code>
        用来储存将加载到web view的网页的地址，一个
        <code>
            title
        </code>
        ，及一个
        <code>
            publishingDate
        </code>
        。它的构造器使用一个字典作为它的参数。它既可以从网络服务器中接收内容，也可以像本例中一样，从plist文件中获取。
    </p>
    <p>
        找到
        <em>
            Feed.swift
        </em>
        并添加下列的property到
        <code>
            Feed
        </code>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">var</span> children = [<span class="hljs-type">FeedItem</span>]()
 </pre>
    <p>
        这样就创建了一个空数组来储存
        <em>
            FeedItem
        </em>
        对象。
    </p>
    <p>
        现在添加下列的类方法到
        <code>
            Feed
        </code>
        中来加载plist文件：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">func</span> <span class="hljs-title">feedList</span>(<span class="hljs-title">\_</span> <span class="hljs-title">fileName</span>: <span class="hljs-title">String</span>) -&gt; [<span class="hljs-title">Feed</span>] </span>{
  <span class="hljs-comment">//1</span>
  <span class="hljs-keyword">var</span> feeds = [<span class="hljs-type">Feed</span>]()
    
  <span class="hljs-comment">//2</span>
  <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> feedList = <span class="hljs-type">NSArray</span>(contentsOfFile: fileName) <span class="hljs-keyword">as</span>? [<span class="hljs-type">NSDictionary</span>] {
    <span class="hljs-comment">//3</span>
    <span class="hljs-keyword">for</span> feedItems <span class="hljs-keyword">in</span> feedList {
      <span class="hljs-comment">//4</span>
      <span class="hljs-keyword">let</span> feed = <span class="hljs-type">Feed</span>(name: feedItems.object(forKey: <span class="hljs-string">"name"</span>) <span class="hljs-keyword">as</span>! <span class="hljs-type">String</span>)
      <span class="hljs-comment">//5</span>
      <span class="hljs-keyword">let</span> items = feedItems.object(forKey: <span class="hljs-string">"items"</span>) <span class="hljs-keyword">as</span>! [<span class="hljs-type">NSDictionary</span>]
      <span class="hljs-comment">//6</span>
      <span class="hljs-keyword">for</span> dict <span class="hljs-keyword">in</span> items {
        <span class="hljs-comment">//7</span>
        <span class="hljs-keyword">let</span> item = <span class="hljs-type">FeedItem</span>(dictionary: dict)
        feed.children.append(item)
      }
      <span class="hljs-comment">//8</span>
      feeds.append(feed)
    }
  }
    
  <span class="hljs-comment">//9</span>
  <span class="hljs-keyword">return</span> feeds
 }
</pre>
    <p>
        这个方法以一个文件名作为它的参数，然后返回了一个由
        <code>
            Feed
        </code>
        对象组成的数组。上述代码：
    </p>
    <ol>
        <li>
            创建了一个空的
            <code>
                Feed
            </code>
            数组。
        </li>
        <li>
            尝试从文件中加载一个字典的数组。
        </li>
        <li>
            如果加载成功的话，遍历数组中的每一个项目。
        </li>
        <li>
            这个字典包含一个键
            <em>
                name
            </em>
            ，用来初始化
            <code>
                Feed
            </code>
            。
        </li>
        <li>
            键
            <em>
                items
            </em>
            则包含了另一个字典的数组。
        </li>
        <li>
            遍历字典。
        </li>
        <li>
            初始化一个
            <code>
                FeedItem
            </code>
            。这个item被添加到了父
            <code>
                Feed
            </code>
            的
            <code>
                children
            </code>
            数组中。
        </li>
        <li>
            循环完成后，在
            <code>
                Feed
            </code>
            开始加载之前，
            <code>
                Feed
            </code>
            的每个child都被添加到了
            <code>
                feeds
            </code>
            的数组中。
        </li>
        <li>
            返回
            <code>
                feeds
            </code>
            。如果每件事都如同期望中的工作方式，这个数组将包含两个
            <code>
                Feed
            </code>
            对象。
        </li>
    </ol>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        ，并在IBOutlet部分的下面添加一个property来储存feeds：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">var</span> feeds = [<span class="hljs-type">Feed</span>]()
</pre>
    <p>
        找到
        <code>
            viewDidLoad()
        </code>
        并添加下列的代码：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> filePath = <span class="hljs-type">Bundle</span>.main.path(forResource: <span class="hljs-string">"Feeds"</span>, ofType: <span class="hljs-string">"plist"</span>) {
  feeds = <span class="hljs-type">Feed</span>.feedList(filePath)
  <span class="hljs-built_in">print</span>(feeds)
}
</pre>
    <p>
        运行项目；你应当会在控制台中类似如下的内容：
    </p>
    <pre lang="bash" class="language-bash hljs">[&lt;Reader.Feed: 0x600000045010&gt;, &lt;Reader.Feed: 0x6000000450d0&gt;]
</pre>
    <p>
        可以看到你已经成功地加载了两个
        <code>
            Feed
        </code>
        对象到
        <code>
            feeds
        </code>
        property中 — 哇！
    </p>
    <h2>
        介绍NSOutlineViewDataSource
    </h2>
    <p>
        到目前为止，你已告知了outline view
        <code>
            ViewController
        </code>
        是它的data source — 但
        <code>
            ViewController
        </code>
        至今不知道如何完成它的新工作。现在是时候来改变这点去解决错误信息了。
    </p>
    <p>
        在你的
        <code>
            ViewController
        </code>
        的类声明下添加如下的
        <em>
            extension
        </em>
        ：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">ViewController</span>: <span class="hljs-title">NSOutlineViewDataSource</span> </span>{
  
}
</pre>
    <p>
        这就让
        <code>
            ViewController
        </code>
        采取了
        <code>
            NSOutlineViewDataSource
        </code>
        协议。由于在本教程中，我们不会使用binding，因此你必须实现几个方法来填充outline view。让我们来看看每个方法。
    </p>
    <p>
        你的outline view需要知道该展示多少个item。因此，使用方法
        <code>
            outlineView(\_: numberOfChildrenOfItem:) -&gt; Int
        </code>
        。
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">outlineView</span><span class="hljs-params">(<span class="hljs-number">\_</span> outlineView: NSOutlineView, numberOfChildrenOfItem item: Any?)</span></span> -&gt; <span class="hljs-type">Int</span> {
  <span class="hljs-comment">//1</span>
  <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> feed = item <span class="hljs-keyword">as</span>? <span class="hljs-type">Feed</span> {
    <span class="hljs-keyword">return</span> feed.children.<span class="hljs-built_in">count</span>
  }
  <span class="hljs-comment">//2</span>
  <span class="hljs-keyword">return</span> feeds.<span class="hljs-built_in">count</span>
}
</pre>
    <p>
        展示在outline view中的每个层级都会调用这个方法。由于你的outline view中只有两个层级，因此这个方法的实现相当得简单：
    </p>
    <ol>
        <li>
            如果
            <code>
                item
            </code>
            是一个
            <code>
                Feed
            </code>
            ，就返回
            <code>
                children
            </code>
            的数量。
        </li>
        <li>
            否则，返回
            <code>
                feeds
            </code>
            的数量。
        </li>
    </ol>
    <p>
        值得注意的是：
        <code>
            item
        </code>
        是可选类型，对于你data model的根对象，它就是
        <code>
            nil
        </code>
        。在本例中，它对于
        <code>
            Feed
        </code>
        就会返回
        <code>
            nil
        </code>
        ；否则它就会包含对象的父对象。对于
        <code>
            FeedItem
        </code>
        对象，
        <code>
            item
        </code>
        就会是一个
        <code>
            Feed
        </code>
        。
    </p>
    <p>
        继续！outline view需要知道对于给定的parent和index，应该展示那个child。这里的代码和之前的很类似：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">outlineView</span><span class="hljs-params">(<span class="hljs-number">\_</span> outlineView: NSOutlineView, child index: Int, ofItem item: Any?)</span></span> -&gt; <span class="hljs-type">Any</span> {
  <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> feed = item <span class="hljs-keyword">as</span>? <span class="hljs-type">Feed</span> {
    <span class="hljs-keyword">return</span> feed.children[index]
  }
    
  <span class="hljs-keyword">return</span> feeds[index]
}
</pre>
    <p>
        首先检查
        <code>
            item
        </code>
        是否是一个
        <code>
            Feed
        </code>
        ；如果是的话，就为给定的index返回相应的
        <code>
            FeedItem
        </code>
        。否则，就返回
        <code>
            Feed
        </code>
        。同样，对于根对象，
        <code>
            item
        </code>
        将是
        <code>
            nil
        </code>
        。
    </p>
    <p>
        <code>
            NSOutlineView
        </code>
        的一个很棒的特性就是他可以折叠item。然而，你必须首先告诉它那些item可以折叠或是展开。添加下列的代码：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">outlineView</span><span class="hljs-params">(<span class="hljs-number">\_</span> outlineView: NSOutlineView, isItemExpandable item: Any)</span></span> -&gt; <span class="hljs-type">Bool</span> {
  <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> feed = item <span class="hljs-keyword">as</span>? <span class="hljs-type">Feed</span> {
    <span class="hljs-keyword">return</span> feed.children.<span class="hljs-built_in">count</span> &gt; <span class="hljs-number">0</span>
  }
    
  <span class="hljs-keyword">return</span> <span class="hljs-literal">false</span>
}
</pre>
    <p>
        在本app中，只有
        <code>
            Feeds
        </code>
        可以展开或收起，因为只有它有children。因此首先检查
        <code>
            item
        </code>
        是否是
        <code>
            Feed
        </code>
        ，如果是的话，就判断它的child数量是否大于0，大于的话就返回true，否则返回false。对于其它的item，都返回false。
    </p>
    <p>
        运行你的app。万岁！错误的消息已经消失了，outline view已经被填充好了。但是稍等 - 你现在只能看到2个小三角形，来指示你可以展开这一行。如果你点击它的话，就可以看到更多的行。
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/second_run"
        rel="attachment wp-att-123497" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Second_Run-480x318.png"
            alt="Second_Run" width="480" height="318" class="aligncenter size-medium wp-image-123497"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Second_Run-480x318.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Second_Run-700x464.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        是你做错了什么吗？不是 - 你只需要在添加一个方法。
    </p>
    <h2>
        介绍NSOutlineViewDelegate
    </h2>
    <p>
        outline view会询问它的delegate，该为每个特定的条目展示什么样的view。然而，你至今还没有添加任何delegate方法的实现 - 现在就是该去添加的时候了。
    </p>
    <p>
        在
        <em>
            ViewController.swift
        </em>
        中添加另一个
        <code>
            ViewController
        </code>
        的extension：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">ViewController</span>: <span class="hljs-title">NSOutlineViewDelegate</span> </span>{

}
</pre>
    <p>
        下面的这个方法会有一点复杂，因为outline view应当为每个
        <code>
            Feed
        </code>
        和
        <code>
            FeedItems
        </code>
        展示不同的view。让我们一块一块地说。
    </p>
    <p>
        首先，添加方法体到extension中。
    </p>
    <pre lang="swift" class="language-swift hljs">		
<span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">outlineView</span><span class="hljs-params">(<span class="hljs-number">\_</span> outlineView: NSOutlineView, viewFor tableColumn: NSTableColumn?, item: Any)</span></span> -&gt; <span class="hljs-type">NSView</span>? {
  <span class="hljs-keyword">var</span> view: <span class="hljs-type">NSTableCellView</span>?
  <span class="hljs-comment">// More code here</span>
  <span class="hljs-keyword">return</span> view
}
</pre>
    <p>
        现在对于每个
        <code>
            item
        </code>
        我们都返回了nil。下一步你要为
        <code>
            Feed
        </code>
        来返回view。在
        <code>
            // More code here
        </code>
        注释的上方添加如下的代码：
    </p>
    <pre lang="swift" class="language-swift hljs">	
<span class="hljs-comment">//1</span>
<span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> feed = item <span class="hljs-keyword">as</span>? <span class="hljs-type">Feed</span> {
  <span class="hljs-comment">//2</span>
  view = outlineView.make(withIdentifier: <span class="hljs-string">"FeedCell"</span>, owner: <span class="hljs-keyword">self</span>) <span class="hljs-keyword">as</span>? <span class="hljs-type">NSTableCellView</span>
  <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> textField = view?.textField {
    <span class="hljs-comment">//3</span>
    textField.stringValue = feed.name
    textField.sizeToFit()
  }
} 
</pre>
    <p>
        上述代码：
    </p>
    <ol>
        <li>
            检查
            <code>
                item
            </code>
            是否是
            <code>
                Feed
            </code>
            。
        </li>
        <li>
            从outline view中获取一个对应于
            <code>
                Feed
            </code>
            的view，包含一个text field的正常的
            <code>
                NSTableViewCell
            </code>
            。
        </li>
        <li>
            设置text field中的文本为feed的名称并调用
            <code>
                sizeToFit()
            </code>
            ，来重新计算它的frame以适应它内容的大小。
        </li>
    </ol>
    <p>
        运行你的项目。你现在可以看到
        <code>
            Feed
        </code>
        的cell，但展开的行中仍然看不到任何内容。
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/third_run"
        rel="attachment wp-att-123506" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Third_Run-480x318.png"
            alt="Third_Run" width="480" height="318" class="aligncenter size-medium wp-image-123506"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Third_Run-480x318.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Third_Run-700x464.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        这是因为你现在仅仅提供了代表
        <code>
            Feed
        </code>
        的view。继续前进到下一步吧！依然在
        <em>
            ViewController.swift
        </em>
        中，在
        <code>
            feeds
        </code>
        这个property下添加下列的property：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">let</span> dateFormatter = <span class="hljs-type">DateFormatter</span>() 
</pre>
    <p>
        在
        <code>
            viewDidLoad()
        </code>
        中
        <code>
            super.viewDidLoad()
        </code>
        后添加下列的代码：
    </p>
    <pre lang="swift" class="language-swift hljs">dateFormatter.dateStyle = .short
</pre>
    <p>
        上述代码添加了一个
        <code>
            NSDateformatter
        </code>
        ，用来依据
        <code>
            FeedItem
        </code>
        中的
        <code>
            publishingDate
        </code>
        创建一个很好的格式化日期。
    </p>
    <p>
        回到
        <code>
            outlineView(\_:viewForTableColumn:item:)
        </code>
        并添加一个
        <em>
            else-if
        </em>
        子句
        <code>
            if let feed = item as? Feed
        </code>
        ：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">else</span> <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> feedItem = item <span class="hljs-keyword">as</span>? <span class="hljs-type">FeedItem</span> {
  <span class="hljs-comment">//1</span>
  <span class="hljs-keyword">if</span> tableColumn?.identifier == <span class="hljs-string">"DateColumn"</span> {
    <span class="hljs-comment">//2</span>
    view = outlineView.make(withIdentifier: <span class="hljs-string">"DateCell"</span>, owner: <span class="hljs-keyword">self</span>) <span class="hljs-keyword">as</span>? <span class="hljs-type">NSTableCellView</span>
    <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> textField = view?.textField {
      <span class="hljs-comment">//3</span>
      textField.stringValue = dateFormatter.string(from: feedItem.publishingDate)
      textField.sizeToFit()
    }
  } <span class="hljs-keyword">else</span> {
    <span class="hljs-comment">//4</span>
    view = outlineView.make(withIdentifier: <span class="hljs-string">"FeedItemCell"</span>, owner: <span class="hljs-keyword">self</span>) <span class="hljs-keyword">as</span>? <span class="hljs-type">NSTableCellView</span>
    <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> textField = view?.textField {
      <span class="hljs-comment">//5</span>
      textField.stringValue = feedItem.title
      textField.sizeToFit()
    }
  }
}
</pre>
    <p>
        上述代码：
    </p>
    <ol>
        <li>
            如果
            <code>
                item
            </code>
            是一个
            <code>
                FeedItem
            </code>
            ，你就需要填充两列：一列是
            <code>
                title
            </code>
            ，另一列是
            <code>
                publishingDate
            </code>
            。你可以使用它们的
            <code>
                identifier
            </code>
            来区分列。
        </li>
        <li>
            如果
            <code>
                identifier
            </code>
            是
            <em>
                dateColumn
            </em>
            ，就请求一个DateCell。
        </li>
        <li>
            使用date formatter来根据
            <code>
                publishingDate
            </code>
            创建一个字符串。
        </li>
        <li>
            如果不是
            <em>
                dateColumn
            </em>
            的话，你就需要一个对应于
            <code>
                FeedItem
            </code>
            的cell。
        </li>
        <li>
            将文本设置为
            <code>
                FeedItem
            </code>
            的
            <code>
                title
            </code>
            。
        </li>
    </ol>
    <p>
        再次运行你的项目，相应的单元格已被正确地填充。
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/fourth_run"
        rel="attachment wp-att-123507" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Fourth_Run-480x318.png"
            alt="Fourth_Run" width="480" height="318" class="aligncenter size-medium wp-image-123507"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Fourth_Run-480x318.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Fourth_Run-700x464.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        还剩一个问题 - 相应于
        <code>
            Feed
        </code>
        的date这列展示了一个静态的文本。要修复这里，可将if语句
        <code>
            if let feed = item as? Feed
        </code>
        的内容修改为：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">if</span> tableColumn?.identifier == <span class="hljs-string">"DateColumn"</span> {
  view = outlineView.make(withIdentifier: <span class="hljs-string">"DateCell"</span>, owner: <span class="hljs-keyword">self</span>) <span class="hljs-keyword">as</span>? <span class="hljs-type">NSTableCellView</span>
  <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> textField = view?.textField {
    textField.stringValue = <span class="hljs-string">""</span>
    textField.sizeToFit()
  }
} <span class="hljs-keyword">else</span> {
  view = outlineView.make(withIdentifier: <span class="hljs-string">"FeedCell"</span>, owner: <span class="hljs-keyword">self</span>) <span class="hljs-keyword">as</span>? <span class="hljs-type">NSTableCellView</span>
  <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> textField = view?.textField {
    textField.stringValue = feed.name
    textField.sizeToFit()
  }
}
</pre>
    <p>
        要完成这app，你还需要在选择一个条目后，在web view中展示出相应的文字。你应该怎么做？幸运的是，下列的方法可以跟踪outline view选择的变化。
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">outlineViewSelectionDidChange</span><span class="hljs-params">(<span class="hljs-number">\_</span> notification: Notification)</span></span> {
  <span class="hljs-comment">//1</span>
  <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> outlineView = notification.object <span class="hljs-keyword">as</span>? <span class="hljs-type">NSOutlineView</span> <span class="hljs-keyword">else</span> {
    <span class="hljs-keyword">return</span>
  }
  <span class="hljs-comment">//2</span>
  <span class="hljs-keyword">let</span> selectedIndex = outlineView.selectedRow
  <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> feedItem = outlineView.item(atRow: selectedIndex) <span class="hljs-keyword">as</span>? <span class="hljs-type">FeedItem</span> {
    <span class="hljs-comment">//3</span>
    <span class="hljs-keyword">let</span> url = <span class="hljs-type">URL</span>(string: feedItem.url)
    <span class="hljs-comment">//4</span>
    <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> url = url {
      <span class="hljs-comment">//5</span>
      <span class="hljs-keyword">self</span>.webView.mainFrame.load(<span class="hljs-type">URLRequest</span>(url: url))
    }
  }
}
</pre>
    <p>
        上述代码：
    </p>
    <ol>
        <li>
            检查通知的对象是否是NSOutlineView。如果不是的话，退出方法。
        </li>
        <li>
            获取被选择的序号，并检查被选择的行是否包含
            <code>
                FeedItem
            </code>
            或
            <code>
                Feed
            </code>
            。
        </li>
        <li>
            如果选中的是
            <code>
                FeedItem
            </code>
            ，就根据
            <code>
                Feed
            </code>
            对象的
            <code>
                url
            </code>
            property创建一个
            <code>
                NSURL
            </code>
            。
        </li>
        <li>
            检查url是否创建成功。
        </li>
        <li>
            最后，加载页面。
        </li>
    </ol>
    <p>
        在你进行测试之前，返回
        <em>
            Info.plist
        </em>
        文件。添加一项
        <em>
            App Transport Security Settings
        </em>
        的
        <em>
            Dictionary
        </em>
        （如果Xcode中还没有的情况下）。在其中添加一项
        <em>
            Allow Arbitrary Loads
        </em>
        ，类型为
        <em>
            Boolean
        </em>
        ，值为
        <em>
            YES
        </em>
        。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            添加此条目到你的plist文件中，会使你的app能够接受任何不安全的主机，可能会造成一定的风险。通常添加
            <em>
                Exception Domains
            </em>
            为某个接口，而对其它接口则使用加密连接的后端，会更好一些。
        </p>
    </div>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Info_Plist.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Info_Plist-700x38.png"
            alt="Change_Info_Plist" width="700" height="38" class="aligncenter size-large wp-image-123498"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Info_Plist-700x38.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Info_Plist-480x26.png 480w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        现在运行项目，并选择一个
        <code>
            FeedItem
        </code>
        。如果你的网路已连接，对应的文章就会在几秒中之后被加载出来。
    </p>
    <h2>
        完成项目
    </h2>
    <p>
        你的示例app已经可以正常地工作了，但现在至少还有两种行为是缺失的：双击来展开或收起一个组，以及从outline view中移除一个组。
    </p>
    <p>
        让我们从双击的特性开始。按
        <em>
            Alt + Cmd + Enter
        </em>
        键打开
        <em>
            Assistant Editor
        </em>
        。在窗口的左边打开
        <em>
            Main.storyboard
        </em>
        ，右边打开
        <em>
            ViewController.swift
        </em>
        。
    </p>
    <p>
        双击左边
        <em>
            Document Outline
        </em>
        中的outline view。在弹出的菜单中，找到
        <em>
            doubleAction
        </em>
        并点击它右侧的小圆圈。
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/assistanteditor-9"
        rel="attachment wp-att-124518" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/AssistantEditor-480x168.png"
            alt="AssistantEditor" width="600" height="210" class="aligncenter size-medium wp-image-124518"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/AssistantEditor-480x168.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/AssistantEditor-768x269.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/AssistantEditor-700x245.png 700w"
            sizes="(max-width: 600px) 100vw, 600px">
        </a>
    </p>
    <p>
        拖拽小圆圈到
        <em>
            ViewController.swift
        </em>
        中，添加一个名为
        <code>
            doubleClickedItem
        </code>
        的
        <em>
            IBAction
        </em>
        。确保sender的类型为
        <code>
            NSOutlineView
        </code>
        而不是
        <code>
            AnyObject
        </code>
        。
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/addaction-2"
        rel="attachment wp-att-124520" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/AddAction-480x230.png"
            alt="AddAction" width="240" height="115" class="aligncenter size-medium wp-image-124520"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/AddAction-480x230.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/AddAction.png 504w"
            sizes="(max-width: 240px) 100vw, 240px">
        </a>
    </p>
    <p>
        切回到Standard editor中（按
        <em>
            Cmd + Enter
        </em>
        键），打开
        <em>
            ViewController.swift
        </em>
        。添加下列代码到你刚创建的动作方法中。
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">doubleClickedItem</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: NSOutlineView)</span></span> {
  <span class="hljs-comment">//1</span>
  <span class="hljs-keyword">let</span> item = sender.item(atRow: sender.clickedRow)
 
  <span class="hljs-comment">//2</span>
  <span class="hljs-keyword">if</span> item <span class="hljs-keyword">is</span> <span class="hljs-type">Feed</span> {
    <span class="hljs-comment">//3</span>
    <span class="hljs-keyword">if</span> sender.isItemExpanded(item) {
      sender.collapseItem(item)
    } <span class="hljs-keyword">else</span> {
      sender.expandItem(item)
    }
  }
}
</pre>
    <p>
        上述代码：
    </p>
    <ol>
        <li>
            获取被点击的item。
        </li>
        <li>
            检查这个item是否为
            <code>
                Feed
            </code>
            ，只有Feed的item可以被展开或收起。
        </li>
        <li>
            如果这个item是
            <code>
                Feed
            </code>
            的话，就询问outline view这个item是展开的还是收起的，然后调用恰当地方法完成操作。
        </li>
    </ol>
    <p>
        运行你的项目，然后双击一个feed。成功了！
    </p>
    <p>
        你想实现的最后一个特性，就是让用户可以按下退格键删除被选择的feed或文章。
    </p>
    <p>
        还是在
        <em>
            ViewController.swift
        </em>
        中，为
        <code>
            ViewController
        </code>
        添加下列的方法。确保将它添加到原始的类声明中而不是extension中，因为这个方法和delegate或datasource的协议无关。
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">override</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">keyDown</span><span class="hljs-params">(with theEvent: NSEvent)</span></span> {
  interpretKeyEvents([theEvent])
}
</pre>
    <p>
        这个方法会在每次某个键被按下时被调用，并询问系统是哪个键被按下了。对于一些键，系统会执行相应的动作。将被退格键调用的方法是
        <code>
            deleteBackward(\_:)
        </code>
        。
    </p>
    <p>
        添加下面的方法
        <code>
            keyDown(\_:)
        </code>
        ：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">override</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">deleteBackward</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: Any?)</span></span> {
  <span class="hljs-comment">//1</span>
  <span class="hljs-keyword">let</span> selectedRow = outlineView.selectedRow
  <span class="hljs-keyword">if</span> selectedRow == -<span class="hljs-number">1</span> {
    <span class="hljs-keyword">return</span>
  }
   	
  <span class="hljs-comment">//2</span>
  outlineView.beginUpdates()

  outlineView.endUpdates()
}
</pre>
    <ol>
        <li>
            第一件事是检查现在有无被选中的项。如果没有任何项被选中，
            <code>
                selectedRow
            </code>
            的值就会是-1，直接退出本方法。
        </li>
        <li>
            否则，就告知outline view现在需要更新一些内容，以及什么时候会更新完毕。
        </li>
    </ol>
    <p>
        现在在
        <code>
            beginUpdates()
        </code>
        和
        <code>
            endUpdates()
        </code>
        间添加下列的代码：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-comment">//3</span>
<span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> item = outlineView.item(atRow: selectedRow) {
     
  <span class="hljs-comment">//4</span>
  <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> item = item <span class="hljs-keyword">as</span>? <span class="hljs-type">Feed</span> {
    <span class="hljs-comment">//5</span>
    <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> index = <span class="hljs-keyword">self</span>.feeds.index( <span class="hljs-keyword">where</span>: {$<span class="hljs-number">0</span>.name == item.name} ) {
      <span class="hljs-comment">//6</span>
      <span class="hljs-keyword">self</span>.feeds.remove(at: index)
      <span class="hljs-comment">//7</span>
      outlineView.removeItems(at: <span class="hljs-type">IndexSet</span>(integer: selectedRow), inParent: <span class="hljs-literal">nil</span>, withAnimation: .slideLeft)
    }
  }
}
</pre>
    <p>
        上述代码：
    </p>
    <ol start="3">
        <li>
            获取被选择的item。
        </li>
        <li>
            检查它是否为
            <code>
                Feed
            </code>
            或
            <code>
                FeedItem
            </code>
            。
        </li>
        <li>
            如果是
            <code>
                Feed
            </code>
            的话，就在
            <code>
                feeds
            </code>
            数组中查找它的序号。
        </li>
        <li>
            找到后，从数组中移除它。
        </li>
        <li>
            从outline view中移除相应的行，要带有一个小小的动画。
        </li>
    </ol>
    <p>
        为了完成这个方法，添加下列的代码来处理
        <code>
            FeedItems
        </code>
        ，将它作为
        <code>
            if let item = item as? Feed
        </code>
        的else部分：
    </p>
    <pre lang="swift" class="language-swift hljs">		
<span class="hljs-keyword">else</span> <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> item = item <span class="hljs-keyword">as</span>? <span class="hljs-type">FeedItem</span> {
  <span class="hljs-comment">//8</span>
  <span class="hljs-keyword">for</span> feed <span class="hljs-keyword">in</span> <span class="hljs-keyword">self</span>.feeds {
    <span class="hljs-comment">//9</span>
    <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> index = feed.children.index( <span class="hljs-keyword">where</span>: {$<span class="hljs-number">0</span>.title == item.title} ) {
      feed.children.remove(at: index)
      outlineView.removeItems(at: <span class="hljs-type">IndexSet</span>(integer: index), inParent: feed, withAnimation: .slideLeft)
    }
  }
}
</pre>
    <ol start="8">
        <li>
            这里的代码非常类似于
            <code>
                Feed
            </code>
            。唯一额外的步骤是它会迭代所有的feed，因为你不知道这个
            <code>
                FeedItem
            </code>
            属于哪个
            <code>
                Feed
            </code>
            。
        </li>
        <li>
            对于每个
            <code>
                Feed
            </code>
            ，检查它的
            <code>
                children
            </code>
            数组中是否可以找到
            <code>
                FeedItem
            </code>
            。如果可以的话，就将它从数组和outline view中删除。
        </li>
    </ol>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            不仅你可以删除一行，但你还可以添加和移动行。步骤是相同的：添加一个item到你的data model中并调用
            <code>
                insertItemsAtIndexes(\_:, inParent:, withAnimation:)
            </code>
            来插入item，或通过
            <code>
                moveItemAtIndex(\_:, inParent:, toIndex:, inParent:)
            </code>
            来移动item。确保你的datasource做出相应的改变。
        </p>
    </div>
    <p>
        现在你的app全部完成了！运行项目来测试你刚添加的新功能。选择一个feed的item并按下删除键 - 它会如你期望中的一样消失掉。测试对于feed也会发生同样的动作。
    </p>
    <h2>
        从这儿去向哪里？
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
        恭喜！你已创建好了一个RSS Feed的阅读器 - 一个带有层级功能的app，它允许用户可以删除行，还可以双击来展开或收起列表。
    </p>
    <p>
        你可以在
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/Reader_Final.zip"
        sl-processed="1">
            这里
        </a>
        下载最终完成后的项目。
    </p>
    <p>
        在本教程中，你学到了大量有关
        <code>
            NSOutlineView
        </code>
        的内容：
    </p>
    <ul>
        <li>
            如何与Interface Builder中的
            <code>
                NSOutlineView
            </code>
            进行交互。
        </li>
        <li>
            如何填充outline view中的数据。
        </li>
        <li>
            如何展开/收起item。
        </li>
        <li>
            如何移除条目。
        </li>
        <li>
            如何响应用户的交互。
        </li>
    </ul>
    <p>
        还有很多未能覆盖到的功能，如拖拽深层级结构的data model。因此，如果你想要了解更多关于
        <code>
            NSOutlineView
        </code>
        的内容，可以去查阅
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ApplicationKit/Classes/NSOutlineView_Class/"
        sl-processed="1">
            官方文档
        </a>
        。由于NSOutlineView是
        <code>
            NSTableView
        </code>
        的子类，Ernesto García的教程
        <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/macOS%20NSTableView%20Tutorial.md"
        sl-processed="1">
            table views
        </a>
        同样值得一看。
    </p>
</div>