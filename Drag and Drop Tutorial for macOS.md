# macOS Drag和Drop的教程

#### [原文地址](https://www.raywenderlich.com/136272/drag-and-drop-tutorial-for-macos) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div id="attachment_141235" style="width: 260px" class="wp-caption alignright">
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-250x250.png"
        alt="Drag_and_Drop_Tutorial_for_macOS" width="250" height="250" class="alignright size-thumbnail wp-image-141235 bordered"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
        <p class="wp-caption-text">
        	学习全部关于macOS拖拽（drag）和投掷（drop）的东西！
        </p>
    </div>
    <p>
    	自从Mac发明开始，拖拽和投掷就是用户交互的一部分。典型的（quintessential）例子就是Finder，你可以拖拽文件来进行排列组织，或将它们投掷到垃圾桶中。
    </p>
    <p>
    	有趣的东西不至于此。
    </p>
    <p>
    	你可以从相册拖拽你最近的日落全景到你的Message，或从Dock上的Downloads中将一个文件拖拽到邮箱中。你已经get到这个点了对么？它非常得酷，并且是macOS体验的不可分割的一部分（an integral part）。
    </p>
    <p>
    	拖拽和投掷从它开始已经走过了一条很长的路，现在你已几乎可以拖拽任何东西到任何地方。尝试一下，你会高兴地惊奇于这个动作和你最喜欢的app支持的类型。
    </p>
    <p>
    	在这个macOS的拖拽和投掷的教程中，你将了解到怎样添加支持到你自己的app中，这样用户就可以在你的app中获得完整的Mac的体验。
    </p>
    <p>
    	这一路，你将学到怎样去：
    </p>
    <ul>
        <li>
        	在
        	<code>
         		NSView
            </code>
        	的子类中实现核心的拖拽及投掷动作
        </li>
        <li>
	       	接受从其它应用丢过来的数据
        </li>
        <li>
        	提供将要拖拽到你app中其它view的数据
        </li>
        <li>
        	创建定制的拖拽类型
        </li>
    </ul>
    <h2>
    	开始啦！
    </h2>
    <p>
    	这个项目最低需要Swift 3和Xcode 8 beta 6的环境。下载
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/08/StickerDrag-Start_s3-b6.zip"
        title="starter project" sl-processed="1">
            起始的项目
        </a>
        ，在Xcode中打开，并build和执行它。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/06/window-starting-361x500.png"
        alt="window-starting" width="361" height="500" class="aligncenter size-large wp-image-136312"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/06/window-starting-361x500.png 361w, https://koenig-media.raywenderlich.com/uploads/2016/06/window-starting-231x320.png 231w, https://koenig-media.raywenderlich.com/uploads/2016/06/window-starting.png 960w"
        sizes="(max-width: 361px) 100vw, 361px">
    </p>
    <h3>
    	遇见这个项目App
    </h3>
    <p>
    	很多孩子喜欢玩贴纸，并使用它们制成很酷的拼图，因此你将构建一个app来实现这个体验。
        你可以将图片拖拽到一个表面上，然后你通过添加星星（sparkle）和角（unicorn）到这个view上，来提高它的档次（kick things up a few notches）。
    </p>
    <p>
    	毕竟，怎么可能会不喜欢星星和角？:]
    </p>
    <p>
    	保持你的集中注意力在目标上 - 构建拖拽和投掷的支持 - 起始的项目已完成了你需要的view。全部你需要做的就是了解拖拽和投掷的机制。
    </p>
    <p>
    	在项目窗口中有三个部分：
    </p>
    <ul>
        <li>
        	贴纸view：你将拖拽和投掷其它东西的地方
        </li>
        <li>
        	你将转变成两个不同的拖拽资源的小view
        </li>
    </ul>
    <p>
    	来看一眼项目吧。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/06/project-display.png"
        alt="project-display" width="288" height="432" class="aligncenter size-full wp-image-136492"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/06/project-display.png 288w, https://koenig-media.raywenderlich.com/uploads/2016/06/project-display-213x320.png 213w"
        sizes="(max-width: 288px) 100vw, 288px">
        <br>
        在这个教程中，你会编辑四个指定的文件，它们在两个位置上：
        <em>
            Dragging Destinations
        </em>
        和
        <em>
            Dragging Sources
        </em>
        ：
    </p>
    <p>
        在
        <em>
            Dragging Destinations
        </em>
        中：
    </p>
    <ul>
        <li>
            <em>
                StickerBoardViewController.swift
            </em>
            ：主view controller
        </li>
        <li>
            <em>
                DestinationView.swift
            </em>
            ：在window顶部的那个view - 它将成为你拖拽动作的容器
        </li>
    </ul>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/06/view-hierachy-368x500.png"
        alt="view-hierachy" width="368" height="500" class="aligncenter size-large wp-image-136561"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/06/view-hierachy-368x500.png 368w, https://koenig-media.raywenderlich.com/uploads/2016/06/view-hierachy-235x320.png 235w, https://koenig-media.raywenderlich.com/uploads/2016/06/view-hierachy.png 493w"
        sizes="(max-width: 368px) 100vw, 368px">
    </p>
    <p>
        在
        <em>
            Dragging Sources
        </em>
        中：
    </p>
    <ul>
        <li>
            <em>
                ImageSourceView.swift
            </em>
            ：在底部带有角的图片的view，你要将它转为拖拽的资源
        </li>
        <li>
            <em>
                AppActionSourceView.swift
            </em>
            ：带有
            <i>
                星星
            </i>
            label的view - 你要将它转为另一种类型的拖拽的资源
        </li>
    </ul>
    <p>
    	这里有一些其它的文件在Drawing和Other Stuff组下，提供了一些助手方法，它们对于这个项目app是非常重要的，但是你不需要为它们花费任何时间。如果想要了解这个事是怎样构建的话，继续探索吧！
    </p>
    <h2>
    	粘贴板和拖拽session
    </h2>
    <p>
    	拖拽和投掷包含一个
        <em>
        	源（source）
        </em>
        和一个
        <em>
        	目的地（destination）
        </em>
        。
    </p>
    <p>
    	你从一个source拖拽出一个项目，它需要实现
        <code>
            NSDraggingSource
        </code>
        协议。然后投掷它到一个destination中，它则必须实现
        <code>
            NSDraggingDestination
        </code>
        协议，为了确定是接受还是拒绝收到的项目。
        <code>
            NSPasteboard
        </code>
        是用来帮助交换数据的类。
    </p>
    <p>
    	整个的过程被称作
        <em>
            dragging session
        </em>
        ：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/07/dragging-session-macro2.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/07/dragging-session-macro2-650x444.png"
            alt="dragging session macroscopic view" width="650" height="444" class="aligncenter size-large wp-image-139844"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/07/dragging-session-macro2-650x444.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/07/dragging-session-macro2-468x320.png 468w, https://koenig-media.raywenderlich.com/uploads/2016/07/dragging-session-macro2.png 1072w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
    	当你用你的鼠标拖拽一样物事的时候，例如一个文件，就会发生下列的事：
    </p>
    <ol>
        <li>
        	当你开始拖拽的时候，一个
            <em>
                拖拽session
            </em>
            就开始了。
        </li>
        <li>
        	选择一些数据 - 通常一个图片和URL - 来表示放置在拖拽粘贴板上的信息。
        </li>
        <li>
        	你将图片投掷到一个destination上，他会选择拒绝还是接受它，并采取一些动作 - 例如，移动文件到另一个目录下。
        </li>
        <li>
            <em>
                拖拽session
            </em>
            结束。
        </li>
    </ol>
    <p>
    	这就是它的要点（gist）。这是一个相当简单的概念！
    </p>
    <p>
    	第一件事，是为了从Finder和其它app接收图片，创建一个拖拽的destination。
    </p>
    <h2>
    	创建一个拖拽destination
    </h2>
    <p>
    	拖拽的destination是一个view或window，它接受来自拖拽粘贴板的数据类型。你要通过遵守（adopt）
        <code>
            NSDraggingDestination
        </code>
        协议来创建拖拽的目的地。
    </p>
    <p>
    	这个图表从拖拽destination的角度，展示了对于拖拽session的剖析。
        <br>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/06/dragging-session.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/06/dragging-session-650x212.png"
            alt="dragging session" width="650" height="212" class="aligncenter size-large wp-image-136488"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/06/dragging-session-650x212.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/06/dragging-session-480x156.png 480w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
    	创建destination包含以下几个步骤：
    </p>
    <ol>
        <li>
        	当构建view的时候，你必须声明从任何的拖拽session中可以接受的类型。
        </li>
        <li>
        	当一个拖拽的图片进入这个view的时候，你需要去实现决定这个view是否接受这种数据类型的逻辑，并让拖拽session知道这个决定。
        </li>
        <li>
        	当拖拽的图片“着陆”（lands on）在这个view上时，你会使用从拖拽粘贴板而来的数据，去展示它在你的view上。
        </li>
    </ol>
    <p>
    	是时候来撸一些代码了！
    </p>
    <p>
    	在项目的navigator中选择
        <em>
            DestinationView.swift
        </em>
        并找到方法：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">func</span> setup<span style="color: #002200;">(</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
<span style="color: #002200;">}</span></pre>
    <p>
    	将其替换为：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">var</span> acceptableTypes<span style="color: #002200;">:</span> Set&lt;String&gt; <span style="color: #002200;">{</span> <span style="color: #a61390;">return</span> <span style="color: #002200;">[</span>NSURLPboardType<span style="color: #002200;">]</span> <span style="color: #002200;">}</span>
&nbsp;
<span style="color: #a61390;">func</span> setup<span style="color: #002200;">(</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
  register<span style="color: #002200;">(</span>forDraggedTypes<span style="color: #002200;">:</span> <span style="color: #a61390;">Array</span><span style="color: #002200;">(</span>acceptableTypes<span style="color: #002200;">)</span><span style="color: #002200;">)</span>
<span style="color: #002200;">}</span></pre>
    <p>
    	这个代码定义了支持类型的集合。在这个case中，仅支持
        <em>
            URLs
        </em>
        。然后，调用
        <code>
            register(forDraggedTypes:)
        </code>
        来接受包含这些类型的拖拽。
    </p>
    <p>
    	添加下列的代码到
        <code>
            DestinationView
        </code>
        中来分析拖拽session的数据：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #11740a; font-style: italic;">//1.</span>
<span style="color: #a61390;">let</span> filteringOptions <span style="color: #002200;">=</span> <span style="color: #002200;">[</span>NSPasteboardURLReadingContentsConformToTypesKey<span style="color: #002200;">:</span><span style="color: #400080;">NSImage</span>.imageTypes<span style="color: #002200;">(</span><span style="color: #002200;">)</span><span style="color: #002200;">]</span>
&nbsp;
<span style="color: #a61390;">func</span> shouldAllowDrag<span style="color: #002200;">(</span>_ draggingInfo<span style="color: #002200;">:</span> <span style="color: #400080;">NSDraggingInfo</span><span style="color: #002200;">)</span> <span style="color: #002200;">-</span>&gt; <span style="color: #a61390;">Bool</span> <span style="color: #002200;">{</span>
&nbsp;
  <span style="color: #a61390;">var</span> canAccept <span style="color: #002200;">=</span> <span style="color: #a61390;">false</span>
&nbsp;
  <span style="color: #11740a; font-style: italic;">//2.</span>
  <span style="color: #a61390;">let</span> pasteBoard <span style="color: #002200;">=</span> draggingInfo.draggingPasteboard<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
&nbsp;
  <span style="color: #11740a; font-style: italic;">//3.</span>
  <span style="color: #a61390;">if</span> pasteBoard.canReadObject<span style="color: #002200;">(</span>forClasses<span style="color: #002200;">:</span> <span style="color: #002200;">[</span><span style="color: #400080;">NSURL</span>.<span style="color: #a61390;">self</span><span style="color: #002200;">]</span>, options<span style="color: #002200;">:</span> filteringOptions<span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
    canAccept <span style="color: #002200;">=</span> <span style="color: #a61390;">true</span>
  <span style="color: #002200;">}</span>
  <span style="color: #a61390;">return</span> canAccept
&nbsp;
<span style="color: #002200;">}</span></pre>
    <p>
    	你在这里做了几件事：
    </p>
    <ol>
        <li>
        	创建一个字典来定义期望的URL类型（图片）。
        </li>
        <li>
        	从拖拽session信息中获取对拖拽粘贴板的引用。
        </li>
        <li>
        	询问粘贴板它是否包含任何的URL，以及这些URL是指向图片的。如果有图片的话，就接受这个拖拽。否则，拒绝它。
        </li>
    </ol>
    <p>
        <code>
            NSDraggingInfo
        </code>
        是一个协议，声明了提供有关拖拽session的信息的方法。你不会创建它们，也不会在事件之间储存它们。系统会在拖拽session期间创建必要的对象。
    </p>
    <p>
    	当这个app接收到图片时，你可以使用这个信息去提供反馈给拖拽session。
    </p>
    <p>
        <code>
            NSView
        </code>
        遵守
        <code>
            NSDraggingDestination
        </code>
        协议，因此你需要在
        <code>
            DestinationView
        </code>
        的实现中添加下列代码去覆盖
        <code>
            draggingEntered(_:)
        </code>
        方法：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #11740a; font-style: italic;">//1.</span>
<span style="color: #a61390;">var</span> isReceivingDrag <span style="color: #002200;">=</span> <span style="color: #a61390;">false</span> <span style="color: #002200;">{</span>
  didSet <span style="color: #002200;">{</span>
    needsDisplay <span style="color: #002200;">=</span> <span style="color: #a61390;">true</span>
  <span style="color: #002200;">}</span>
<span style="color: #002200;">}</span>
&nbsp;
<span style="color: #11740a; font-style: italic;">//2.</span>
<span style="color: #a61390;">override</span> <span style="color: #a61390;">func</span> draggingEntered<span style="color: #002200;">(</span>_ sender<span style="color: #002200;">:</span> <span style="color: #400080;">NSDraggingInfo</span><span style="color: #002200;">)</span> <span style="color: #002200;">-</span>&gt; NSDragOperation <span style="color: #002200;">{</span>
  <span style="color: #a61390;">let</span> allow <span style="color: #002200;">=</span> shouldAllowDrag<span style="color: #002200;">(</span>sender<span style="color: #002200;">)</span>
  isReceivingDrag <span style="color: #002200;">=</span> allow
  <span style="color: #a61390;">return</span> allow ? .copy <span style="color: #002200;">:</span> NSDragOperation<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
<span style="color: #002200;">}</span></pre>
    <p>
    	上面的代码做了这些事：
    </p>
    <ol>
        <li>
        	创建了一个名为
            <code>
                isReceivingDrag
            </code>
            的property，以便去追踪当前有拖拽session在这个view中，并含有你想要的数据。每次设置时，都会触发这个view的重绘。
        </li>
        <li>
        	覆盖
            <code>
                draggingEntered(_:)
            </code>
            方法，并确定它是否接受这个拖拽操作。
        </li>
    </ol>
    <p>
    	在第二部分，这个方法需要返回一个
        <code>
            NSDragOperation
        </code>
        。你有可能注意到鼠标指针的变化是依赖于你按住的键或拖拽的destination的。
    </p>
    <p>
    	例如，如果你在
    	<em>
            Finder
        </em>
    	的拖拽期间按住
        <em>
            Option
        </em>
        键，那个指针就会获得一个绿色的
        <em>
            +
        </em>
        符号，用来展示一个文件的拷贝即将发生。这个值是你如何控制那些指针的变化。
    </p>
    <p>
    	在这个配置中，如果拖拽粘贴板带有一个图片，它就返回
        <code>
            .copy
        </code>
        来向用户展示你将要复制图片。否则，如果它不接受拖拽的项目，它就返回
        <code>
            NSDragOperation()
        </code>
        。
    </p>
    <h3>
    	处理退出
    </h3>
    <p>
    	进入view的东西同时也有可能退出，所以app需要处理当一个拖拽session没有投掷就退出了你的view时的情况。添加下列的代码：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">override</span> <span style="color: #a61390;">func</span> draggingExited<span style="color: #002200;">(</span>_ sender<span style="color: #002200;">:</span> <span style="color: #400080;">NSDraggingInfo</span>?<span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
  isReceivingDrag <span style="color: #002200;">=</span> <span style="color: #a61390;">false</span>
<span style="color: #002200;">}</span></pre>
    <p>
    	你已经覆盖了
        <code>
            draggingExited(_:)
        </code>
        方法，并设置
        <code>
            isReceivingDrag
        </code>
        变量为
        <code>
            false
        </code>
        。
    </p>
    <h3>
    	告诉用户正在发生什么
    </h3>
    <p>
    	你几乎已经完成了第一段的代码！用户喜欢当一些事在背后发生时，能够看到一个视觉上的提示，所以，接下来，你要添加一小段绘图的代码，来保持你的用户在体验闭环（loop）上。
    </p>
    <p>
        仍然是在
        <em>
            DestinationView.swift
        </em>
        中，找到
        <code>
            draw(:_)
        </code>
        并用下列代码替换它。
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">override</span> <span style="color: #a61390;">func</span> draw<span style="color: #002200;">(</span>_ dirtyRect<span style="color: #002200;">:</span> <span style="color: #400080;">NSRect</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
&nbsp;
  <span style="color: #a61390;">if</span> isReceivingDrag <span style="color: #002200;">{</span>
    <span style="color: #400080;">NSColor</span>.selectedControlColor.<span style="color: #a61390;">set</span><span style="color: #002200;">(</span><span style="color: #002200;">)</span>
&nbsp;
    <span style="color: #a61390;">let</span> path <span style="color: #002200;">=</span> <span style="color: #400080;">NSBezierPath</span><span style="color: #002200;">(</span>rect<span style="color: #002200;">:</span>bounds<span style="color: #002200;">)</span>
    path.lineWidth <span style="color: #002200;">=</span> Appearance.lineWidth
    path.stroke<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
  <span style="color: #002200;">}</span>
<span style="color: #002200;">}</span></pre>
    <p>
    	当一个有效的拖拽进入到这个view时，这个代码就会绘制出一个系统颜色的代码。除了看起来很尖锐，它通过当接受一个拖拽的项目时，提供视觉的表现，使你的app与系统其余部分保持一致。
    </p>
    <div class="note">
        <p>
            <em>
            	注意：
            </em>
            想要了解更多关于自定义绘图的内容？查看我们的
            <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Core%20Graphics%20on%20macOS%20Tutorial.md"
            target="_blank" title="Core Graphics on macOS Tutorial" sl-processed="1">
                macOS教程：Core Graphics
            </a>
            。
        </p>
    </div>
    <p>
    	build并执行，然后尝试将一个图片从Finder拖拽到
        <em>
            StickerDrag
        </em>
        中。如果你没有顺手的图片，就使用项目目录中的
        <em>
            sample.jpg
        </em>
        吧。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/06/buildrun-add-plus.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/06/buildrun-add-plus-361x500.png"
            alt="buildrun-add-plus" width="361" height="500" class="aligncenter size-large wp-image-137410"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/06/buildrun-add-plus-361x500.png 361w, https://koenig-media.raywenderlich.com/uploads/2016/06/buildrun-add-plus-231x320.png 231w, https://koenig-media.raywenderlich.com/uploads/2016/06/buildrun-add-plus.png 479w"
            sizes="(max-width: 361px) 100vw, 361px">
        </a>
    </p>
    <p>
    	你可以看到，当在这个view中时，指针会带有一个
        <em>
            +
        </em>
        的符号。并且view会在周围绘制一个边框。
    </p>
    <p>
    	当你退出这个view的时候，边框和
        <em>
            +
        </em>
        就会消失；只要你拖拽的不是一个图片文件，绝对任何事都不会发生。
    </p>
    <h3>
    	结束拖拽
    </h3>
    <p>
    	现在，到了这个部分的最后一步：你必须接受拖拽，处理数据，并告知拖拽session这已发生。
    </p>
    <p>
    	添加下列代码到
        <code>
            DestinationView
        </code>
        类的实现中：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">override</span> <span style="color: #a61390;">func</span> prepareForDragOperation<span style="color: #002200;">(</span>_ sender<span style="color: #002200;">:</span> <span style="color: #400080;">NSDraggingInfo</span><span style="color: #002200;">)</span> <span style="color: #002200;">-</span>&gt; <span style="color: #a61390;">Bool</span> <span style="color: #002200;">{</span>
  <span style="color: #a61390;">let</span> allow <span style="color: #002200;">=</span> shouldAllowDrag<span style="color: #002200;">(</span>sender<span style="color: #002200;">)</span>
  <span style="color: #a61390;">return</span> allow
<span style="color: #002200;">}</span></pre>
    <p>
    	当你在这个view中释放鼠标的时候，系统就会调用上面的方法；这是最后一次接受或拒绝拖拽的机会。返回
        <code>
            false
        </code>
        就会拒绝，导致拖拽的图像跑回了它起始的位置。返回
        <code>
            true
        </code>
        意味着view接受了这个image。当接受时，系统就会移除拖拽的图片并调用协议序列中的下一个方法：
        <code>
            performDragOperation(_:)
        </code>
        。
    </p>
    <p>
    	添加下列方法到
        <code>
            DestinationView
        </code>
        中：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">override</span> <span style="color: #a61390;">func</span> performDragOperation<span style="color: #002200;">(</span>_ draggingInfo<span style="color: #002200;">:</span> <span style="color: #400080;">NSDraggingInfo</span><span style="color: #002200;">)</span> <span style="color: #002200;">-</span>&gt; <span style="color: #a61390;">Bool</span> <span style="color: #002200;">{</span>
&nbsp;
  <span style="color: #11740a; font-style: italic;">//1.</span>
  isReceivingDrag <span style="color: #002200;">=</span> <span style="color: #a61390;">false</span>
  <span style="color: #a61390;">let</span> pasteBoard <span style="color: #002200;">=</span> draggingInfo.draggingPasteboard<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
&nbsp;
  <span style="color: #11740a; font-style: italic;">//2.</span>
  <span style="color: #a61390;">let</span> point <span style="color: #002200;">=</span> convert<span style="color: #002200;">(</span>draggingInfo.draggingLocation<span style="color: #002200;">(</span><span style="color: #002200;">)</span>, from<span style="color: #002200;">:</span> <span style="color: #a61390;">nil</span><span style="color: #002200;">)</span>
  <span style="color: #11740a; font-style: italic;">//3.</span>
  <span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> urls <span style="color: #002200;">=</span> pasteBoard.readObjects<span style="color: #002200;">(</span>forClasses<span style="color: #002200;">:</span> <span style="color: #002200;">[</span><span style="color: #400080;">NSURL</span>.<span style="color: #a61390;">self</span><span style="color: #002200;">]</span>, options<span style="color: #002200;">:</span>filteringOptions<span style="color: #002200;">)</span> <span style="color: #a61390;">as?</span> <span style="color: #002200;">[</span>URL<span style="color: #002200;">]</span>, urls.<span style="color: #a61390;">count</span> &gt; <span style="color: #2400d9;">0</span> <span style="color: #002200;">{</span>
    delegate?.processImageURLs<span style="color: #002200;">(</span>urls, center<span style="color: #002200;">:</span> point<span style="color: #002200;">)</span>
    <span style="color: #a61390;">return</span> <span style="color: #a61390;">true</span>
  <span style="color: #002200;">}</span>
  <span style="color: #a61390;">return</span> <span style="color: #a61390;">false</span>
&nbsp;
<span style="color: #002200;">}</span></pre>
    <p>
    	你做的事情有：
    </p>
    <ol>
        <li>
            重置
            <code>
                isReceivingDrag
            </code>
            标致为
            <code>
                false
            </code>
            。
        </li>
        <li>
        	将基于window的坐标转为view的相对坐标。
        </li>
        <li>
        	将图片的URL移交给delegate进行处理，并返回
            <code>
                true
            </code>
            - 否则，你拒绝拖拽操作并返回
            <code>
                false
            </code>
            。
        </li>
    </ol>
    <div class="note">
        <p>
            <em>
                注意
            </em>
            ：感觉更好了？如果你要做一个带动画的投掷序列，
            <code>
                performDragOperation(:_)
            </code>
            会是开始动画最好的地方。
        </p>
    </div>
    <p>
    	祝贺！你刚刚完成了第一部分，并完成了
    	<code>
            DestinationView
        </code>
        接收拖拽要做的所有工作。
    </p>
    <h2>
        使用DestinationView的数据
    </h2>
    <p>
        Next up you’ll use the data that
        <code>
            DestinationView
        </code>
        provides in its delegate.
    </p>
    <p>
        Open
        <em>
            StickerBoardViewController.swift
        </em>
        and introduce yourself to the class that is the delegate of
        <code>
            DestinationView
        </code>
        .
    </p>
    <p>
        To use it properly, you need to implement the
        <code>
            DestinationViewDelegate
        </code>
        method that places the images on the target layer. Find
        <code>
            processImage(_:center:)
        </code>
        and replace it with this.
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">func</span> processImage<span style="color: #002200;">(</span>_ image<span style="color: #002200;">:</span> <span style="color: #400080;">NSImage</span>, center<span style="color: #002200;">:</span> <span style="color: #400080;">NSPoint</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
&nbsp;
  <span style="color: #11740a; font-style: italic;">//1.</span>
  invitationLabel.isHidden <span style="color: #002200;">=</span> <span style="color: #a61390;">true</span>
&nbsp;
  <span style="color: #11740a; font-style: italic;">//2.</span>
  <span style="color: #a61390;">let</span> constrainedSize <span style="color: #002200;">=</span> image.aspectFitSizeForMaxDimension<span style="color: #002200;">(</span>Appearance.maxStickerDimension<span style="color: #002200;">)</span>
&nbsp;
  <span style="color: #11740a; font-style: italic;">//3.</span>
  <span style="color: #a61390;">let</span> subview <span style="color: #002200;">=</span> <span style="color: #400080;">NSImageView</span><span style="color: #002200;">(</span>frame<span style="color: #002200;">:</span><span style="color: #400080;">NSRect</span><span style="color: #002200;">(</span>x<span style="color: #002200;">:</span> center.x <span style="color: #002200;">-</span> constrainedSize.width<span style="color: #002200;">/</span><span style="color: #2400d9;">2</span>, y<span style="color: #002200;">:</span> center.y <span style="color: #002200;">-</span> constrainedSize.height<span style="color: #002200;">/</span><span style="color: #2400d9;">2</span>, width<span style="color: #002200;">:</span> constrainedSize.width, height<span style="color: #002200;">:</span> constrainedSize.height<span style="color: #002200;">)</span><span style="color: #002200;">)</span>
  subview.image <span style="color: #002200;">=</span> image
  targetLayer.addSubview<span style="color: #002200;">(</span>subview<span style="color: #002200;">)</span>
&nbsp;
  <span style="color: #11740a; font-style: italic;">//4.</span>
  <span style="color: #a61390;">let</span> maxrotation <span style="color: #002200;">=</span> <span style="color: #400080;">CGFloat</span><span style="color: #002200;">(</span>arc4random_uniform<span style="color: #002200;">(</span>Appearance.maxRotation<span style="color: #002200;">)</span><span style="color: #002200;">)</span> <span style="color: #002200;">-</span> Appearance.rotationOffset
  subview.frameCenterRotation <span style="color: #002200;">=</span> maxrotation
&nbsp;
<span style="color: #002200;">}</span></pre>
    <p>
        This code does the following tricks:
    </p>
    <ol>
        <li>
            It hides the
            <i>
                Drag Images Here
            </i>
            label.
        </li>
        <li>
            It figures out the maximum size for the dropped image while holding the
            aspect ratio constant.
        </li>
        <li>
            It constructs a subview with that size, centers it on the drop point and
            adds it to the view hierarchy.
        </li>
        <li>
            It randomly rotates the view a little bit for a bit of funkiness.
        </li>
    </ol>
    <p>
        With all that in place, you’re ready to implement the method so it deals
        with the image URLs that get dragged into the view.
        <br>
        Replace
        <code>
            processImageURLs(_:center:)
        </code>
        method with this:
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">func</span> processImageURLs<span style="color: #002200;">(</span>_ urls<span style="color: #002200;">:</span> <span style="color: #002200;">[</span>URL<span style="color: #002200;">]</span>, center<span style="color: #002200;">:</span> <span style="color: #400080;">NSPoint</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
  <span style="color: #a61390;">for</span> <span style="color: #002200;">(</span>index,url<span style="color: #002200;">)</span> <span style="color: #a61390;">in</span> urls.enumerated<span style="color: #002200;">(</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
&nbsp;
    <span style="color: #11740a; font-style: italic;">//1.</span>
    <span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> image <span style="color: #002200;">=</span> <span style="color: #400080;">NSImage</span><span style="color: #002200;">(</span>contentsOf<span style="color: #002200;">:</span>url<span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
&nbsp;
      <span style="color: #a61390;">var</span> newCenter <span style="color: #002200;">=</span> center
      <span style="color: #11740a; font-style: italic;">//2.</span>
      <span style="color: #a61390;">if</span> index &gt; <span style="color: #2400d9;">0</span> <span style="color: #002200;">{</span>
        newCenter <span style="color: #002200;">=</span> center.addRandomNoise<span style="color: #002200;">(</span>Appearance.randomNoise<span style="color: #002200;">)</span>
      <span style="color: #002200;">}</span>
&nbsp;
      <span style="color: #11740a; font-style: italic;">//3.</span>
      processImage<span style="color: #002200;">(</span>image, center<span style="color: #002200;">:</span>newCenter<span style="color: #002200;">)</span>
    <span style="color: #002200;">}</span>
  <span style="color: #002200;">}</span>
<span style="color: #002200;">}</span></pre>
    <p>
        What you’re doing here is:
    </p>
    <ol>
        <li>
            Creating an image with the contents from the URLs.
        </li>
        <li>
            If there is more than one image, this offsets the images’ centers a bit
            to create a layered, randomized effect.
        </li>
        <li>
            Pass the image and center point to the previous method so it can add the
            image to the view.
        </li>
    </ol>
    <p>
        Now build and run then drag an image file (or several) to the app window.
        Drop it!
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/06/window-demo-1-568x500.png"
        alt="window-demo-1" width="568" height="500" class="aligncenter size-large wp-image-136319"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/06/window-demo-1-568x500.png 568w, https://koenig-media.raywenderlich.com/uploads/2016/06/window-demo-1-364x320.png 364w"
        sizes="(max-width: 568px) 100vw, 568px">
    </p>
    <p>
        Look at that board of images just waiting to be made fearlessly fanciful.
    </p>
    <p>
        You’re at about the halfway point and have already explored how to make
        any view a dragging destination and how to compel it to accept a standard
        dragging type — in this case, an image URL.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/07/Screen-Shot-2016-07-09-at-2.35.20-PM.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/07/Screen-Shot-2016-07-09-at-2.35.20-PM.png"
            alt="Intermission: let's all go to the lobby and get ourselves some drinks. And snacks. And new iMacs"
            width="363" height="382" class="aligncenter size-full wp-image-138997"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/07/Screen-Shot-2016-07-09-at-2.35.20-PM.png 363w, https://koenig-media.raywenderlich.com/uploads/2016/07/Screen-Shot-2016-07-09-at-2.35.20-PM-304x320.png 304w"
            sizes="(max-width: 363px) 100vw, 363px">
        </a>
    </p>
    <h2>
        Creating a Dragging Source
    </h2>
    <p>
        You’ve played around with the receiving end, but how about the giving
        end?
    </p>
    <p>
        In this section, you’ll learn how to supercharge your app with the ability
        to be the source by letting those unicorns and sparkles break free and
        bring glee to the users’ images in the right circumstances.
    </p>
    <p>
        All dragging sources must conform to the
        <code>
            NSDraggingSource
        </code>
        protocol. This MVP (most valuable player) takes the task of placing data
        (or a promise for that data) for one or more types on the dragging pasteboard.
        It also supplies a dragging image to represent the data.
    </p>
    <p>
        When the image finally lands on its target, the destination unarchives
        the data from the pasteboard. Alternatively, the dragging source can fulfil
        the promise of providing the data.
    </p>
    <p>
        You’ll need to supply the data of two different types: a standard
        <em>
            Cocoa
        </em>
        type (an image) and custom type that you create.
    </p>
    <h3>
        Supplying a Standard Dragging Type
    </h3>
    <p>
        The dragging source will be
        <code>
            ImageSourceView
        </code>
        — the class of the view that has the unicorn. Your objective is simple:
        get that unicorn onto your collage.
    </p>
    <p>
        The class needs to adopt the necessary protocols
        <code>
            NSDraggingSource
        </code>
        and
        <code>
            NSPasteboardItemDataProvider
        </code>
        , so open
        <em>
            ImageSourceView.swift
        </em>
        and add the following extensions:
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #11740a; font-style: italic;">// MARK: - NSDraggingSource</span>
extension ImageSourceView<span style="color: #002200;">:</span> <span style="color: #400080;">NSDraggingSource</span> <span style="color: #002200;">{</span>
  <span style="color: #11740a; font-style: italic;">//1.</span>
  <span style="color: #a61390;">func</span> draggingSession<span style="color: #002200;">(</span>_ session<span style="color: #002200;">:</span> NSDraggingSession, sourceOperationMaskFor context<span style="color: #002200;">:</span> NSDraggingContext<span style="color: #002200;">)</span> <span style="color: #002200;">-</span>&gt; NSDragOperation <span style="color: #002200;">{</span>
    <span style="color: #a61390;">return</span> .generic
  <span style="color: #002200;">}</span>
<span style="color: #002200;">}</span>
&nbsp;
<span style="color: #11740a; font-style: italic;">// MARK: - NSDraggingSource</span>
extension ImageSourceView<span style="color: #002200;">:</span> NSPasteboardItemDataProvider <span style="color: #002200;">{</span>
  <span style="color: #11740a; font-style: italic;">//2.</span>
  <span style="color: #a61390;">func</span> pasteboard<span style="color: #002200;">(</span>_ pasteboard<span style="color: #002200;">:</span> <span style="color: #400080;">NSPasteboard</span>?, item<span style="color: #002200;">:</span> NSPasteboardItem, provideDataForType type<span style="color: #002200;">:</span> <span style="color: #a61390;">String</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
    <span style="color: #11740a; font-style: italic;">//TODO: Return image data</span>
  <span style="color: #002200;">}</span>
<span style="color: #002200;">}</span></pre>
    <ol>
        <li>
            This method is required by
            <code>
                NSDraggingSource
            </code>
            . It tells the dragging session what sort of operation you’re attempting
            when the user drags from the view. In this case it’s a generic operation.
        </li>
        <li>
            This implements the mandatory
            <code>
                NSPasteboardItemDataProvider
            </code>
            method. More on this soon — for now it’s just a stub.
        </li>
    </ol>
    <h3>
        Start a Dragging Session
    </h3>
    <p>
        In a real world project, the best moment to initiate a dragging session
        depends on your UI.
    </p>
    <p>
        With the project app, this particular view you’re working in exists for
        the sole purpose of dragging, so you’ll start the drag on
        <code>
            mouseDown(with:)
        </code>
        .
    </p>
    <p>
        In other cases, it may be appropriate to start in the
        <code>
            mouseDragged(with:)
        </code>
        event.
    </p>
    <p>
        Add this method inside the
        <code>
            ImageSourceView
        </code>
        class implementation:
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">override</span> <span style="color: #a61390;">func</span> mouseDown<span style="color: #002200;">(</span>with theEvent<span style="color: #002200;">:</span> <span style="color: #400080;">NSEvent</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
  <span style="color: #11740a; font-style: italic;">//1.</span>
  <span style="color: #a61390;">let</span> pasteboardItem <span style="color: #002200;">=</span> NSPasteboardItem<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
  pasteboardItem.setDataProvider<span style="color: #002200;">(</span><span style="color: #a61390;">self</span>, forTypes<span style="color: #002200;">:</span> <span style="color: #002200;">[</span>kUTTypeTIFF<span style="color: #002200;">]</span><span style="color: #002200;">)</span>
&nbsp;
  <span style="color: #11740a; font-style: italic;">//2.</span>
  <span style="color: #a61390;">let</span> draggingItem <span style="color: #002200;">=</span> NSDraggingItem<span style="color: #002200;">(</span>pasteboardWriter<span style="color: #002200;">:</span> pasteboardItem<span style="color: #002200;">)</span>
  draggingItem.setDraggingFrame<span style="color: #002200;">(</span><span style="color: #a61390;">self</span>.bounds, contents<span style="color: #002200;">:</span>snapshot<span style="color: #002200;">(</span><span style="color: #002200;">)</span><span style="color: #002200;">)</span>
&nbsp;
  <span style="color: #11740a; font-style: italic;">//3.</span>
  beginDraggingSession<span style="color: #002200;">(</span>with<span style="color: #002200;">:</span> <span style="color: #002200;">[</span>draggingItem<span style="color: #002200;">]</span>, event<span style="color: #002200;">:</span> theEvent, source<span style="color: #002200;">:</span> <span style="color: #a61390;">self</span><span style="color: #002200;">)</span>
<span style="color: #002200;">}</span></pre>
    <p>
        Things get rolling when the system calls
        <code>
            mouseDown(with:)
        </code>
        when you click on a view. The base implementation does nothing, eliminating
        the need to call super. The code in the implementation does all of this:
    </p>
    <ol>
        <li>
            Creates an
            <code>
                NSPasteboardItem
            </code>
            and sets this class as its data provider. A
            <code>
                NSPasteboardItem
            </code>
            is the box that carries the info about the item being dragged. The
            <code>
                NSPasteboardItemDataProvider
            </code>
            provides data upon request. In this case you’ll supply
            <em>
                TIFF
            </em>
            data, which is the standard way to carry images around in Cocoa.
        </li>
        <li>
            Creates a
            <code>
                NSDraggingItem
            </code>
            and assigns the pasteboard item to it. A dragging item exists to provide
            the drag image and carry one pasteboard item, but you don’t keep a reference
            to the item because of its limited lifespan. If needed, the dragging session
            will recreate this object.
            <code>
                snapshot()
            </code>
            is one of the helper methods mentioned earlier. It creates an
            <code>
                NSImage
            </code>
            of an
            <code>
                NSView
            </code>
            .
        </li>
        <li>
            Starts the dragging session. Here you trigger the dragging image to start
            following your mouse until you drop it.
        </li>
    </ol>
    <p>
        Build and run. Try to drag the unicorn onto the top view.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/06/buildrun-drag-unicorn.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/06/buildrun-drag-unicorn-361x500.png"
            alt="buildrun-drag-unicorn" width="361" height="500" class="aligncenter size-large wp-image-137417"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/06/buildrun-drag-unicorn-361x500.png 361w, https://koenig-media.raywenderlich.com/uploads/2016/06/buildrun-drag-unicorn-231x320.png 231w, https://koenig-media.raywenderlich.com/uploads/2016/06/buildrun-drag-unicorn.png 479w"
            sizes="(max-width: 361px) 100vw, 361px">
        </a>
    </p>
    <p>
        An image of the view follows your mouse, but it slides back on mouse up
        because
        <code>
            DestinationView
        </code>
        doesn’t accept TIFF data.
    </p>
    <h3>
        Take the TIFF
    </h3>
    <p>
        In order to accept this data, you need to:
    </p>
    <ol>
        <li>
            Update the registered types in
            <code>
                setup()
            </code>
            to accept TIFF data
        </li>
        <li>
            Update
            <code>
                shouldAllowDrag()
            </code>
            to accept the TIFF type
        </li>
        <li>
            Update
            <code>
                performDragOperation(_:)
            </code>
            to take the image data from the pasteboard
        </li>
    </ol>
    <p>
        Open
        <em>
            DestinationView.swift
        </em>
        .
    </p>
    <p>
        Replace the following line:
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">var</span> acceptableTypes<span style="color: #002200;">:</span> Set&lt;String&gt; <span style="color: #002200;">{</span> <span style="color: #a61390;">return</span> <span style="color: #002200;">[</span>NSURLPboardType<span style="color: #002200;">]</span> <span style="color: #002200;">}</span></pre>
    <p>
        With this:
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">var</span> nonURLTypes<span style="color: #002200;">:</span> Set&lt;String&gt;  <span style="color: #002200;">{</span> <span style="color: #a61390;">return</span> <span style="color: #002200;">[</span><span style="color: #a61390;">String</span><span style="color: #002200;">(</span>kUTTypeTIFF<span style="color: #002200;">)</span><span style="color: #002200;">]</span> <span style="color: #002200;">}</span>
<span style="color: #a61390;">var</span> acceptableTypes<span style="color: #002200;">:</span> Set&lt;String&gt; <span style="color: #002200;">{</span> <span style="color: #a61390;">return</span> nonURLTypes.union<span style="color: #002200;">(</span><span style="color: #002200;">[</span>NSURLPboardType<span style="color: #002200;">]</span><span style="color: #002200;">)</span> <span style="color: #002200;">}</span></pre>
    <p>
        You’ve just registered the TIFF type like you did for URLs and created
        a subset to use next.
    </p>
    <p>
        Next, go to
        <code>
            shouldAllowDrag(:_)
        </code>
        , and add find the
        <code>
            return canAccept
        </code>
        method. Enter the following just above the
        <code>
            return
        </code>
        statement:
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">else</span> <span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> types <span style="color: #002200;">=</span> pasteBoard.types, nonURLTypes.intersection<span style="color: #002200;">(</span>types<span style="color: #002200;">)</span>.<span style="color: #a61390;">count</span> &gt; <span style="color: #2400d9;">0</span> <span style="color: #002200;">{</span>
  canAccept <span style="color: #002200;">=</span> <span style="color: #a61390;">true</span>
<span style="color: #002200;">}</span></pre>
    <p>
        Here you’re checking if the
        <code>
            nonURLTypes
        </code>
        set contains any of the types received from the pasteboard, and if that’s
        the case, accepts the drag operation. Since you added a TIFF type to that
        set, the view accepts TIFF data from the pasteboard.
    </p>
    <h3>
        Unarchive the Image Data
    </h3>
    <p>
        Lastly, update
        <code>
            performDragOperation(_:)
        </code>
        to unarchive the image data from the pasteboard. This bit is really easy.
    </p>
    <p>
        Cocoa wants you to use pasteboards and provides an
        <code>
            NSImage
        </code>
        initializer that takes
        <code>
            NSPasteboard
        </code>
        as a parameter. You’ll find more of these convenience methods in
        <em>
            Cocoa
        </em>
        when you start exploring drag and drop more.
    </p>
    <p>
        Locate
        <code>
            performDragOperation(_:)
        </code>
        , and add the following code at the end, just above the return sentence
        <code>
            return false
        </code>
        :
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">else</span> <span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> image <span style="color: #002200;">=</span> <span style="color: #400080;">NSImage</span><span style="color: #002200;">(</span>pasteboard<span style="color: #002200;">:</span> pasteBoard<span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
  delegate?.processImage<span style="color: #002200;">(</span>image, center<span style="color: #002200;">:</span> point<span style="color: #002200;">)</span>
  <span style="color: #a61390;">return</span> <span style="color: #a61390;">true</span>
<span style="color: #002200;">}</span></pre>
    <p>
        This extracts an image from the pasteboard and passes it to the delegate
        for processing.
    </p>
    <p>
        Build and run, and then drag that unicorn onto the sticker view.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/06/buildrun-drag-unicorn-plus.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/06/buildrun-drag-unicorn-plus-361x500.png"
            alt="buildrun-drag-unicorn-plus" width="361" height="500" class="aligncenter size-large wp-image-137424"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/06/buildrun-drag-unicorn-plus-361x500.png 361w, https://koenig-media.raywenderlich.com/uploads/2016/06/buildrun-drag-unicorn-plus-231x320.png 231w, https://koenig-media.raywenderlich.com/uploads/2016/06/buildrun-drag-unicorn-plus.png 478w"
            sizes="(max-width: 361px) 100vw, 361px">
        </a>
    </p>
    <p>
        You’ll notice that now you get a green
        <em>
            +
        </em>
        on your cursor.
    </p>
    <p>
        The destination view accepts the image data, but the image still slides
        back when you drop. Hmmm. What’s missing here?
    </p>
    <h3>
        Show me the Image Data!
    </h3>
    <p>
        You need to get the dragging source to supply the image data — in other
        words: fulfil its promise.
    </p>
    <p>
        Open
        <em>
            ImageSourceView.swift
        </em>
        and replace the contents of
        <code>
            pasteboard(_:item:provideDataForType:)
        </code>
        with this:
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #11740a; font-style: italic;">//1.</span>
<span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> pasteboard <span style="color: #002200;">=</span> pasteboard, type <span style="color: #002200;">==</span> <span style="color: #a61390;">String</span><span style="color: #002200;">(</span>kUTTypeTIFF<span style="color: #002200;">)</span>, <span style="color: #a61390;">let</span> image <span style="color: #002200;">=</span> <span style="color: #400080;">NSImage</span><span style="color: #002200;">(</span>named<span style="color: #002200;">:</span><span style="color: #bf1d1a;">"unicorn"</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
  <span style="color: #11740a; font-style: italic;">//2.</span>
  <span style="color: #a61390;">let</span> finalImage <span style="color: #002200;">=</span> image.tintedImageWithColor<span style="color: #002200;">(</span><span style="color: #400080;">NSColor</span>.randomColor<span style="color: #002200;">(</span><span style="color: #002200;">)</span><span style="color: #002200;">)</span>
  <span style="color: #11740a; font-style: italic;">//3.</span>
  <span style="color: #a61390;">let</span> tiffdata <span style="color: #002200;">=</span> finalImage.tiffRepresentation
  pasteboard.setData<span style="color: #002200;">(</span>tiffdata, forType<span style="color: #002200;">:</span>type<span style="color: #002200;">)</span>
<span style="color: #002200;">}</span></pre>
    <p>
        In this method, the following things are happening:
    </p>
    <ol>
        <li>
            If the desired data type is
            <code>
                kUTTypeTIFF
            </code>
            , you load an image named
            <em>
                unicorn
            </em>
            .
        </li>
        <li>
            Use one of the supplied helpers to tint the image with a random color.
            After all, colorful unicorns are more festive than a smattering of all-black
            unicorns. :]
        </li>
        <li>
            Transform the image into TIFF data and place it on the pasteboard.
        </li>
    </ol>
    <p>
        Build and run, and drag the unicorn onto the sticker view. It’ll drop
        and place a colored unicorn on the view. Great!
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/07/midway.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/07/midway-361x500.png"
            alt="buildrun-add-unicorns" width="361" height="500" class="aligncenter size-large wp-image-139842"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/07/midway-361x500.png 361w, https://koenig-media.raywenderlich.com/uploads/2016/07/midway-231x320.png 231w, https://koenig-media.raywenderlich.com/uploads/2016/07/midway.png 480w"
            sizes="(max-width: 361px) 100vw, 361px">
        </a>
    </p>
    <p>
        So.many.unicorns!
    </p>
    <h2>
        Dragging Custom Types
    </h2>
    <p>
        Unicorns are pretty fabulous, but what good are they without magical sparkles?
        Strangely, there’s no standard
        <em>
            Cocoa
        </em>
        data type for sparkles. I bet you know what comes next. :]
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/06/sparkle.jpg"
        alt="sparkle" width="400" height="300" class="aligncenter size-full wp-image-136322">
    </p>
    <div class="note">
        <p>
            <em>
                Note
            </em>
            : In the last section you supplied a standard data type. You can explore
            the types for standard data
            <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ApplicationKit/Classes/NSPasteboard_Class/index.html#//apple_ref/doc/constant_group/Types_for_Standard_Data_OS_X_v10.6_and_later_"
            target="_blank" title="in the API reference" sl-processed="1">
                in the API reference
            </a>
            .
        </p>
    </div>
    <p>
        In this section you’ll invent your own data type.
    </p>
    <p>
        These are the tasks on your to-do list:
    </p>
    <ol>
        <li>
            Create a new dragging source with your custom type.
        </li>
        <li>
            Update the dragging destination to recognize that type.
        </li>
        <li>
            Update the view controller to react to that type.
        </li>
    </ol>
    <h3>
        Create the Dragging Source
    </h3>
    <p>
        Open
        <em>
            AppActionSourceView.swift
        </em>
        . It’s mostly empty except for this important definition:
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">enum</span> SparkleDrag <span style="color: #002200;">{</span>
  <span style="color: #a61390;">static</span> <span style="color: #a61390;">let</span> type <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"com.razeware.StickerDrag.AppAction"</span>
  <span style="color: #a61390;">static</span> <span style="color: #a61390;">let</span> action <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"make sparkles"</span>
<span style="color: #002200;">}</span></pre>
    <p>
        This defines your custom dragging type and action identifier.
    </p>
    <p>
        Dragging source types must be
        <a href="https://developer.apple.com/library/ios/documentation/FileManagement/Conceptual/understanding_utis/understand_utis_intro/understand_utis_intro.html"
        target="_blank" title="Uniform Type Identifiers" sl-processed="1">
            Uniform Type Identifiers
        </a>
        . These are reverse-coded name paths that describe a data type.
    </p>
    <p>
        For example, if you print out the value of
        <code>
            kUTTypeTIFF
        </code>
        you’ll see that it is the string
        <em>
            public.tiff
        </em>
        .
    </p>
    <p>
        To avoid a collision with an existing type, you can define the identifier
        like this:
        <em>
            bundle identifier
        </em>
        +
        <em>
            AppAction
        </em>
        . It is an arbitrary value, but you keep it under the private namespace
        of the application to minimize the risk of using an existing name.
    </p>
    <p>
        If you attempt to construct a
        <code>
            NSPasteboardItem
        </code>
        with a type that isn’t
        <em>
            UTI
        </em>
        , the operation will fail.
    </p>
    <p>
        Now you need to make
        <code>
            AppActionSourceView
        </code>
        adopt
        <code>
            NSDraggingSource
        </code>
        . Open
        <em>
            AppActionSourceView.swift
        </em>
        and add the following extension:
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #11740a; font-style: italic;">// MARK: - NSDraggingSource</span>
extension AppActionSourceView<span style="color: #002200;">:</span> <span style="color: #400080;">NSDraggingSource</span> <span style="color: #002200;">{</span>
&nbsp;
  <span style="color: #a61390;">func</span> draggingSession<span style="color: #002200;">(</span>_ session<span style="color: #002200;">:</span> NSDraggingSession, sourceOperationMaskFor
    context<span style="color: #002200;">:</span> NSDraggingContext<span style="color: #002200;">)</span> <span style="color: #002200;">-</span>&gt; NSDragOperation <span style="color: #002200;">{</span>
&nbsp;
    <span style="color: #a61390;">switch</span><span style="color: #002200;">(</span>context<span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
    <span style="color: #a61390;">case</span> .outsideApplication<span style="color: #002200;">:</span>
      <span style="color: #a61390;">return</span> NSDragOperation<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
    <span style="color: #a61390;">case</span> .withinApplication<span style="color: #002200;">:</span>
      <span style="color: #a61390;">return</span> .generic
    <span style="color: #002200;">}</span>
  <span style="color: #002200;">}</span>
<span style="color: #002200;">}</span></pre>
    <p>
        This code block differs from
        <code>
            ImageSourceView
        </code>
        because you’ll place private data on the pasteboard that has no meaning
        outside the app. That’s why you’re using the
        <code>
            context
        </code>
        parameter to return a
        <code>
            NSDragOperation()
        </code>
        when the mouse is dragged outside your application.
    </p>
    <p>
        You’re already familiar with the next step. You need to override the
        <code>
            mouseDown(with:)
        </code>
        event to start a dragging session with a pasteboard item.
    </p>
    <p>
        Add the following code into the
        <code>
            AppActionSourceView
        </code>
        class implementation:
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">override</span> <span style="color: #a61390;">func</span> mouseDown<span style="color: #002200;">(</span>with theEvent<span style="color: #002200;">:</span> <span style="color: #400080;">NSEvent</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
&nbsp;
  <span style="color: #a61390;">let</span> pasteboardItem <span style="color: #002200;">=</span> NSPasteboardItem<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
  pasteboardItem.setString<span style="color: #002200;">(</span>SparkleDrag.action, forType<span style="color: #002200;">:</span> SparkleDrag.type<span style="color: #002200;">)</span>
  <span style="color: #a61390;">let</span> draggingItem <span style="color: #002200;">=</span> NSDraggingItem<span style="color: #002200;">(</span>pasteboardWriter<span style="color: #002200;">:</span> pasteboardItem<span style="color: #002200;">)</span>
  draggingItem.setDraggingFrame<span style="color: #002200;">(</span><span style="color: #a61390;">self</span>.bounds, contents<span style="color: #002200;">:</span>snapshot<span style="color: #002200;">(</span><span style="color: #002200;">)</span><span style="color: #002200;">)</span>
&nbsp;
  beginDraggingSession<span style="color: #002200;">(</span>with<span style="color: #002200;">:</span> <span style="color: #002200;">[</span>draggingItem<span style="color: #002200;">]</span>, event<span style="color: #002200;">:</span> theEvent, source<span style="color: #002200;">:</span> <span style="color: #a61390;">self</span><span style="color: #002200;">)</span>
&nbsp;
<span style="color: #002200;">}</span></pre>
    <p>
        What did you do in there?
    </p>
    <p>
        You constructed a pasteboard item and placed the data directly inside
        it for your custom type. In this case, the data is a custom action identifier
        that the receiving view may use to make a decision.
    </p>
    <p>
        You can see how this differs from
        <code>
            ImageSourceView
        </code>
        in one way. Instead of deferring data generation to the point when the
        view accepts the drop with the
        <code>
            NSPasteboardItemDataProvider
        </code>
        protocol, the dragged data goes directly to the pasteboard.
    </p>
    <p>
        Why would you use the
        <code>
            NSPasteboardItemDataProvider
        </code>
        protocol? Because you want things to move as fast as possible when you
        start the drag session in
        <code>
            mouseDown(with:)
        </code>
        .
    </p>
    <p>
        If the data you’re moving takes too long to construct on the pasteboard,
        it’ll jam up the main thread and frustrate users with a perceptible delay
        when they start dragging.
    </p>
    <p>
        In this case, you place a small string on the pasteboard so that it can
        do it right away.
    </p>
    <h3>
        Accept the New Type
    </h3>
    <p>
        Next, you have to let the destination view accept this new type. By now,
        you already know how to do it.
    </p>
    <p>
        Open
        <em>
            DestinationView.swift
        </em>
        and add
        <code>
            SparkleDrag.type
        </code>
        to the registered types. Replace the following line:
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">var</span> nonURLTypes<span style="color: #002200;">:</span> Set&lt;String&gt;  <span style="color: #002200;">{</span> <span style="color: #a61390;">return</span> <span style="color: #002200;">[</span><span style="color: #a61390;">String</span><span style="color: #002200;">(</span>kUTTypeTIFF<span style="color: #002200;">)</span><span style="color: #002200;">]</span> <span style="color: #002200;">}</span></pre>
    <p>
        With this:
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">var</span> nonURLTypes<span style="color: #002200;">:</span> Set&lt;String&gt;  <span style="color: #002200;">{</span> <span style="color: #a61390;">return</span> <span style="color: #002200;">[</span><span style="color: #a61390;">String</span><span style="color: #002200;">(</span>kUTTypeTIFF<span style="color: #002200;">)</span>,SparkleDrag.type<span style="color: #002200;">]</span> <span style="color: #002200;">}</span></pre>
    <p>
        Now SparkleDrags are acceptable!
    </p>
    <p>
        <code>
            performDragOperation(:_)
        </code>
        needs a new
        <code>
            else-if
        </code>
        clause, so add this code at the end of the method just before
        <code>
            return false
        </code>
        :
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">else</span> <span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> types <span style="color: #002200;">=</span> pasteBoard.types, types.<span style="color: #a61390;">contains</span><span style="color: #002200;">(</span>SparkleDrag.type<span style="color: #002200;">)</span>,
  <span style="color: #a61390;">let</span> action <span style="color: #002200;">=</span> pasteBoard.string<span style="color: #002200;">(</span>forType<span style="color: #002200;">:</span> SparkleDrag.type<span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
  delegate?.processAction<span style="color: #002200;">(</span>action, center<span style="color: #002200;">:</span>point<span style="color: #002200;">)</span>
  <span style="color: #a61390;">return</span> <span style="color: #a61390;">true</span>
<span style="color: #002200;">}</span></pre>
    <p>
        This addition extracts the string from the pasteboard. If it corresponds
        to your custom type, you pass the action back to the delegate.
    </p>
    <p>
        You’re almost done, you just need to update
        <code>
            StickerBoardViewController
        </code>
        to deal with the action instruction.
    </p>
    <h3>
        Handle the Action Instruction
    </h3>
    <p>
        Open
        <em>
            StickerBoardViewController.swift
        </em>
        and replace
        <code>
            processAction(_:center:)
        </code>
        with this:
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">func</span> processAction<span style="color: #002200;">(</span>_ action<span style="color: #002200;">:</span> <span style="color: #a61390;">String</span>, center<span style="color: #002200;">:</span> <span style="color: #400080;">NSPoint</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
  <span style="color: #11740a; font-style: italic;">//1.</span>
  <span style="color: #a61390;">if</span> action <span style="color: #002200;">==</span> SparkleDrag.action  <span style="color: #002200;">{</span>
    invitationLabel.isHidden <span style="color: #002200;">=</span> <span style="color: #a61390;">true</span>
&nbsp;
    <span style="color: #11740a; font-style: italic;">//2.</span>
    <span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> image <span style="color: #002200;">=</span> <span style="color: #400080;">NSImage</span><span style="color: #002200;">(</span>named<span style="color: #002200;">:</span><span style="color: #bf1d1a;">"star"</span><span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
&nbsp;
      <span style="color: #11740a; font-style: italic;">//3.</span>
      <span style="color: #a61390;">for</span> _ <span style="color: #a61390;">in</span> <span style="color: #2400d9;">1</span>..&lt;Appearance.numStars <span style="color: #002200;">{</span>
&nbsp;
        <span style="color: #11740a; font-style: italic;">//A.</span>
        <span style="color: #a61390;">let</span> maxSize<span style="color: #002200;">:</span><span style="color: #400080;">CGFloat</span> <span style="color: #002200;">=</span> Appearance.maxStarSize
        <span style="color: #a61390;">let</span> sizeChange <span style="color: #002200;">=</span> <span style="color: #400080;">CGFloat</span><span style="color: #002200;">(</span>arc4random_uniform<span style="color: #002200;">(</span>Appearance.randonStarSizeChange<span style="color: #002200;">)</span><span style="color: #002200;">)</span>
        <span style="color: #a61390;">let</span> finalSize <span style="color: #002200;">=</span> maxSize <span style="color: #002200;">-</span> sizeChange
        <span style="color: #a61390;">let</span> newCenter <span style="color: #002200;">=</span> center.addRandomNoise<span style="color: #002200;">(</span>Appearance.randomNoiseStar<span style="color: #002200;">)</span>
&nbsp;
        <span style="color: #11740a; font-style: italic;">//B.</span>
        <span style="color: #a61390;">let</span> imageFrame <span style="color: #002200;">=</span> <span style="color: #400080;">NSRect</span><span style="color: #002200;">(</span>x<span style="color: #002200;">:</span> newCenter.x, y<span style="color: #002200;">:</span> newCenter.y, width<span style="color: #002200;">:</span> finalSize , height<span style="color: #002200;">:</span> finalSize<span style="color: #002200;">)</span>
        <span style="color: #a61390;">let</span> imageView <span style="color: #002200;">=</span> <span style="color: #400080;">NSImageView</span><span style="color: #002200;">(</span>frame<span style="color: #002200;">:</span>imageFrame<span style="color: #002200;">)</span>
&nbsp;
        <span style="color: #11740a; font-style: italic;">//C.</span>
        <span style="color: #a61390;">let</span> newImage <span style="color: #002200;">=</span> image.tintedImageWithColor<span style="color: #002200;">(</span><span style="color: #400080;">NSColor</span>.randomColor<span style="color: #002200;">(</span><span style="color: #002200;">)</span><span style="color: #002200;">)</span>
&nbsp;
        <span style="color: #11740a; font-style: italic;">//D.</span>
        imageView.image <span style="color: #002200;">=</span> newImage
        targetLayer.addSubview<span style="color: #002200;">(</span>imageView<span style="color: #002200;">)</span>
      <span style="color: #002200;">}</span>
    <span style="color: #002200;">}</span>
  <span style="color: #002200;">}</span>
<span style="color: #002200;">}</span></pre>
    <p>
        The above code does the following:
    </p>
    <ol>
        <li>
            Only responds to the known sparkle action
        </li>
        <li>
            Loads a star image from the bundle
        </li>
        <li>
            Makes some copies of the star image and…
        </li>
        <ol>
            <li>
                Generates some random numbers to alter the star position.
            </li>
            <li>
                Creates an
                <code>
                    NSImageView
                </code>
                and sets its frame.
            </li>
            <li>
                Gives the image a random color — unless you’re going for a David Bowie
                tribute, black stars are a bit gothic.
            </li>
            <li>
                Places the image on the view.
            </li>
        </ol>
    </ol>
    <p>
        Build and run. Now you can drag from the sparkles view onto the sticker
        view to add a spray of stars to your view.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/06/final-361x500.png"
        alt="final" width="361" height="500" class="aligncenter size-large wp-image-136566"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/06/final-361x500.png 361w, https://koenig-media.raywenderlich.com/uploads/2016/06/final-231x320.png 231w, https://koenig-media.raywenderlich.com/uploads/2016/06/final.png 480w"
        sizes="(max-width: 361px) 100vw, 361px">
    </p>
    <h2>
        Where to go From Here?
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
        Congratulations, you created a custom drag and drop interface in your
        very own app!
    </p>
    <p>
        You can use the
        <em>
            Save Image To Desktop
        </em>
        button to save your image as a
        <em>
            JPG
        </em>
        with the name
        <em>
            StickerDrag
        </em>
        . Maybe take it a step further and tweet it to the team
        <a href="https://twitter.com/rwenderlich" target="_blank" sl-processed="1">
            @rwenderlich
        </a>
        .
    </p>
    <p>
        Here’s the source code for the
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/08/StickerDrag-Final_S3-b6.zip"
        sl-processed="1">
            the completed project
        </a>
        .
    </p>
    <p>
        This drag and drop tutorial for macOS covered the basics of the Cocoa
        drag and drop mechanism, including:
    </p>
    <ul>
        <li>
            Creating a dragging destination and accepting several different types
            of data
        </li>
        <li>
            Using the dragging session lifecycle to provide user feedback of the drag
            operation
        </li>
        <li>
            Decoding information from the pasteboard
        </li>
        <li>
            Creating a dragging source and providing deferred data
        </li>
        <li>
            Creating a dragging source that provides a custom data type
        </li>
    </ul>
    <p>
        Now you have the knowledge and experience needed to support drag and drop
        in any macOS app.
    </p>
    <p>
        There’s certainly more to learn.
    </p>
    <p>
        You could study up on how to apply effects, such as changing the dragging
        image during the drag or implementing an animated drop transition, or working
        with promised files — Photos is one application that places promised data
        on the dragging pasteboard.
    </p>
    <p>
        Another interesting topic is how to use drag and drop with
        <code>
            NSTableView
        </code>
        and
        <code>
            NSOutlineView
        </code>
        , which work in slightly different ways. Learn about it from the following
        resources:
    </p>
    <ul>
        <li>
            Apple’s
            <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/DragandDrop/DragandDrop.html"
            target="_blank" title="Drag and Drop Programming Topics" sl-processed="1">
                Drag and Drop Programming Topics
            </a>
        </li>
        <li>
            Apple’s
            <a href="https://developer.apple.com/library/mac/documentation/Security/Conceptual/AppSandboxDesignGuide/AppSandboxInDepth/AppSandboxInDepth.html#//apple_ref/doc/uid/TP40011183-CH3-SW16"
            target="_blank" title="Sandboxing and Security Scoped Data" sl-processed="1">
                Sandboxing and Security Scoped Data
            </a>
            , where you’ll find information about how dragging and dropping files
            works if an application is sandboxed.
        </li>
        <li>
            <a href="https://developer.apple.com/library/mac/samplecode/CocoaDragAndDrop/Introduction/Intro.html"
            target="_blank" title="CocoaDragAndDrop" sl-processed="1">
                CocoaDragAndDrop
            </a>
            sample code (in Objective-C)
        </li>
        <li>
            <a href="https://developer.apple.com/library/prerelease/content/samplecode/DragNDropOutlineView/Introduction/Intro.html"
            target="_blank" title="DragNDropOutlineView" sl-processed="1">
                DragNDropOutlineView
            </a>
            sample code (in Objective-C)
        </li>
    </ul>
    <p>
        If you have any questions or comments about this drag and drop tutorial
        for macOS, please join the discussion below! And remember, sometimes life
        is a dragging experience, but everything’s better with unicorns and sparkles.
        :]
    </p>
</div>
