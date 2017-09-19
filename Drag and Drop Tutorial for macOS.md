# macOS Drag和Drop的教程

#### [原文地址](https://www.raywenderlich.com/136272/drag-and-drop-tutorial-for-macos) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div id="attachment_141235" style="width: 260px" class="wp-caption alignright">
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-250x250.png"
        alt="Drag_and_Drop_Tutorial_for_macOS" width="250" height="250" class="alignright size-thumbnail wp-image-141235 bordered"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/08/DragandDrop-feature-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
        <p class="wp-caption-text">
        	学习全部关于macOS拖拽（drag）和投放（drop）的东西！
        </p>
    </div>
    <p>
    	自从Mac发明开始，拖拽和投放就是用户交互的一部分。典型的（quintessential）例子就是Finder，你可以拖拽文件来进行排列组织，或将它们投放到垃圾桶中。
    </p>
    <p>
    	有趣的东西不至于此。
    </p>
    <p>
    	你可以从相册拖拽你最近的日落全景到你的Message，或从Dock上的Downloads中将一个文件拖拽到邮箱中。你已经get到这个点了对么？它非常得酷，并且是macOS体验的不可分割的一部分（an integral part）。
    </p>
    <p>
    	拖拽和投放从它开始已经走过了一条很长的路，现在你已几乎可以拖拽任何东西到任何地方。尝试一下，你会高兴地惊奇于这个动作和你最喜欢的app支持的类型。
    </p>
    <p>
    	在这个macOS的拖拽和投放的教程中，你将了解到怎样添加支持到你自己的app中，这样用户就可以在你的app中获得完整的Mac的体验。
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
        	的子类中实现核心的拖拽及投放动作
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
    	很多孩子喜欢玩贴纸，并使用它们制成很酷的拼图，因此你将构建一个app来实现这个体验。你可以将图片拖拽到一个表面上，然后你通过添加星星（sparkle）和独角兽（unicorn）到这个view上，来提高它的档次（kick things up a few notches）。
    </p>
    <p>
    	毕竟，怎么可能会不喜欢星星和独角兽？:]
    </p>
    <p>
    	保持你的集中注意力在目标上 - 构建拖拽和投放的支持 - 起始的项目已完成了你需要的view。全部你需要做的就是了解拖拽和投放的机制。
    </p>
    <p>
    	在项目窗口中有三个部分：
    </p>
    <ul>
        <li>
        	贴纸view：你将拖拽和投放其它东西的地方
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
            ：在底部带有独角兽的图片的view，你要将它转为拖拽的资源
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
    	拖拽和投放包含一个
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
        协议。然后投放它到一个destination中，它则必须实现
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
        	你将图片投放到一个destination上，他会选择拒绝还是接受它，并采取一些动作 - 例如，移动文件到另一个目录下。
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
            draggingEntered(\_:)
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
                draggingEntered(\_:)
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
    	进入view的东西同时也有可能退出，所以app需要处理当一个拖拽session没有投放，就退出了你的view时的情况。添加下列的代码：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">override</span> <span style="color: #a61390;">func</span> draggingExited<span style="color: #002200;">(</span>_ sender<span style="color: #002200;">:</span> <span style="color: #400080;">NSDraggingInfo</span>?<span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
  isReceivingDrag <span style="color: #002200;">=</span> <span style="color: #a61390;">false</span>
<span style="color: #002200;">}</span></pre>
    <p>
    	你已经覆盖了
        <code>
            draggingExited(\_:)
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
            performDragOperation(\_:)
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
            ：感觉更好了？如果你要做一个带动画的投放序列，
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
    	接下来你将使用
        <code>
            DestinationView
        </code>
        在它的delegate中使用的数据。
    </p>
    <p>
    	打开
        <em>
            StickerBoardViewController.swift
        </em>
        并将其指定为
        <code>
            DestinationView
        </code>
        的delegate。
    </p>
    <p>
    	为了恰当地使用它，你需要实现
        <code>
            DestinationViewDelegate协议
        </code>
        的方法，将图片放到目标的层上。找到
        <code>
            processImage(\_:center:)
        </code>
        并用下列的代码替换它。
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
    	这个代码玩了下列的招（tricks）：
    </p>
    <ol>
        <li>
        	将
            <i>
                Drag Images Here
            </i>
            label隐藏。
        </li>
        <li>
        	为投放的图片，算出其保持长宽比的情况下，最大的尺寸。
        </li>
        <li>
        	使用这个尺寸构建了一个subview，将它的中心定位在投放点上，并将其添加到view的图层上。
        </li>
        <li>
        	随机地旋转这个view一点角度，让它看起来更好。
        </li>
    </ol>
    <p>
    	到这里，你已经准备好了去实现处理投放到这个view的图片的URL的方法。
        <br>
        使用下列代码替换
        <code>
            processImageURLs(\_:center:)
        </code>
        方法：
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
    	你在这里做的是：
    </p>
    <ol>
        <li>
        	使用URL的内容中创建图片。
        </li>
        <li>
        	如果这里有超过一张的图片，就将图片的中心偏移一些，来创建分层的，随机的效果。
        </li>
        <li>
        	将图片和中心点传递到上一个方法，让它可以添加图片到view上。
        </li>
    </ol>
    <p>
    	现在build并执行，然后拖拽一个（或几个）图片到app的window上，投放它！
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/06/window-demo-1-568x500.png"
        alt="window-demo-1" width="568" height="500" class="aligncenter size-large wp-image-136319"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/06/window-demo-1-568x500.png 568w, https://koenig-media.raywenderlich.com/uploads/2016/06/window-demo-1-364x320.png 364w"
        sizes="(max-width: 568px) 100vw, 568px">
    </p>
    <p>
        看看那张图板，等待大胆的幻想~~
    </p>
    <p>
        你大约已走了一半的路，探索过怎样使如何一个view变为拖拽的destination，以及怎样使它接受一个标准类型 - 在这个case中，是图片的URL。
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
        创建拖拽Source
    </h2>
    <p>
        你已经玩转了接受这一头的，但是发送这一头的呢？
    </p>
    <p>
        在这一部分，你将学到怎样通过让那些独角兽和星星自由地活动，并在适当的环境中给用户的图像带来快乐，让你的app充满能量（supercharge your app）。
    </p>
    <p>
        所有的拖动source都必须遵循
        <code>
            NSDraggingSource
        </code>
        协议。这个MVP（最重要的玩家）承担了将一个或多个类型的数据（或数据的“承诺”（promise））放置到拖拽板上的任务。它还提供一个拖拽图片来展示数据。
    </p>
    <p>
        当这个图片最终着陆在它的目标时，这个destination就从粘贴板中解档数据。或者是，拖拽source就可以实现提供数据的承诺。
    </p>
    <p>
        你需要提供两种不同类型的数据：一个标准的
        <em>
            Cocoa
        </em>
        类型（一个image）和你创建的定制类型。
    </p>
    <h3>
        提供标准的拖动类型
    </h3>
    <p>
        拖拽source将是
        <code>
            ImageSourceView
        </code>
        - 包含独角兽的view的类。你的目的很简单：把这个独角兽弄到你的拼图（collage）上。
    </p>
    <p>
        这个类需要遵循必须的协议
        <code>
            NSDraggingSource
        </code>
        和
        <code>
            NSPasteboardItemDataProvider
        </code>
        ，因此打开
        <em>
            ImageSourceView.swift
        </em>
        并添加下列的extension：
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
            这个方法是
            <code>
                NSDraggingSource
            </code>
            协议要求的。它告诉拖拽session你在尝试的操作类型，当用户从这个view中拖拽时。在这个case中，它是一个泛型的操作。
        </li>
        <li>
            这实现了强制的
            <code>
                NSPasteboardItemDataProvider
            </code>
            方法。后面还有更多的东西 - 现在的只是一点点的根。
        </li>
    </ol>
    <h3>
        开始一个拖拽session
    </h3>
    <p>
        在真实世界的项目中，启动一个拖拽session的最佳时机取决于你的UI。
    </p>
    <p>
        在这个项目app中，这个你工作所在的特定的view，是为了拖拽的单独的目标存在的，因此你将启动拖拽在
        <code>
            mouseDown(with:)
        </code>
        这里。
    </p>
    <p>
        在其它case中，它启动在
        <code>
            mouseDragged(with:)
        </code>
        事件中启动可能会更恰当。
    </p>
    <p>
        在
        <code>
            ImageSourceView
        </code>
        类的实现中添加下列方法：
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
        当你点击一个view时，系统调用
        <code>
            mouseDown(with:)
        </code>
        ，事件开始“滚动”（rolling）。基类的实现中没有做任何事，因此无需再去调用。在实现中的代码做了全部的事：
    </p>
    <ol>
        <li>
            创建一个
            <code>
                NSPasteboardItem
            </code>
            ，并设定这个类作为它的数据提供者。
            <code>
                NSPasteboardItem
            </code>
            是一个“箱子”，可以“运载”有关被拖拽的项目的信息。
            <code>
                NSPasteboardItemDataProvider
            </code>
            根据请求提供数据。在这个case中你将提供
            <em>
                TIFF
            </em>
            数据，这是在Cocoa中运载图片的标准形式。
        </li>
        <li>
            创建一个
            <code>
                NSDraggingItem
            </code>
            并将粘贴板的项目（item）赋给它。存在拖拽项目（item）来提供拖拽的图片，并运载一个粘贴板项目（item），但由于它有限的寿命，你不能保留对这个项目（item）的引用。如果需要的话，拖拽session会重新创建这个对象。
            <code>
                snapshot()
            </code>
            是前面提到的助手方法之一。它创建一个
            <code>
                NSView
            </code>
            的
            <code>
                NSImage
            </code>
            。
        </li>
        <li>
            开始拖拽session。这里你触发拖拽图片，来跟随你的鼠标，直到你投放它。
        </li>
    </ol>
    <p>
        build并执行。尝试拖拽独角兽到顶部的view。
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
        这个view的一个图片跟随你的鼠标，但它滑到了你鼠标的后面，因为
        <code>
            DestinationView
        </code>
        不接受TIFF数据。
    </p>
    <h3>
        拿TIFF
    </h3>
    <p>
        为了接受这个数据，你需要：
    </p>
    <ol>
        <li>
            在
            <code>
                setup()
            </code>
            中更新注册的类型来接受TIFF数据
        </li>
        <li>
            更新
            <code>
                shouldAllowDrag()
            </code>
            来接受TIFF类型
        </li>
        <li>
            更新
            <code>
                performDragOperation(\_:)
            </code>
            来从粘贴板中拿到图片
        </li>
    </ol>
    <p>
        打开
        <em>
            DestinationView.swift
        </em>
        。
    </p>
    <p>
        替换下面这行：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">var</span> acceptableTypes<span style="color: #002200;">:</span> Set&lt;String&gt; <span style="color: #002200;">{</span> <span style="color: #a61390;">return</span> <span style="color: #002200;">[</span>NSURLPboardType<span style="color: #002200;">]</span> <span style="color: #002200;">}</span></pre>
    <p>
        为：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">var</span> nonURLTypes<span style="color: #002200;">:</span> Set&lt;String&gt;  <span style="color: #002200;">{</span> <span style="color: #a61390;">return</span> <span style="color: #002200;">[</span><span style="color: #a61390;">String</span><span style="color: #002200;">(</span>kUTTypeTIFF<span style="color: #002200;">)</span><span style="color: #002200;">]</span> <span style="color: #002200;">}</span>
<span style="color: #a61390;">var</span> acceptableTypes<span style="color: #002200;">:</span> Set&lt;String&gt; <span style="color: #002200;">{</span> <span style="color: #a61390;">return</span> nonURLTypes.union<span style="color: #002200;">(</span><span style="color: #002200;">[</span>NSURLPboardType<span style="color: #002200;">]</span><span style="color: #002200;">)</span> <span style="color: #002200;">}</span></pre>
    <p>
        你刚刚注册了TIFF类型，就像你为URL做的，并创建一个子集来下次使用。
    </p>
    <p>
        接下来，来到
        <code>
            shouldAllowDrag(:_)
        </code>
        ，并添加发现
        <code>
            return canAccept
        </code>
        。输入下列代码在
        <code>
            return
        </code>
        语句之前：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">else</span> <span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> types <span style="color: #002200;">=</span> pasteBoard.types, nonURLTypes.intersection<span style="color: #002200;">(</span>types<span style="color: #002200;">)</span>.<span style="color: #a61390;">count</span> &gt; <span style="color: #2400d9;">0</span> <span style="color: #002200;">{</span>
  canAccept <span style="color: #002200;">=</span> <span style="color: #a61390;">true</span>
<span style="color: #002200;">}</span></pre>
    <p>
        这里你检查了
        <code>
            nonURLTypes
        </code>
        集合是否包含了任何从粘贴板接受到的类型，如果是的话，接受拖拽的操作。从你添加了一个TIFF类型到这个集合，这个view就接受从粘贴板而来的TIFF数据。
    </p>
    <h3>
        解档图片数据
    </h3>
    <p>
        最后，更新
        <code>
            performDragOperation(\_:)
        </code>
        来解档从粘贴板来的图片数据。这相当得容易。
    </p>
    <p>
        Cocoa想让你使用粘贴板，并提供了一个
        <code>
            NSImage
        </code>
        的带有
        <code>
            NSPasteboard
        </code>
        参数的构造方法。当你开始探索更多关于拖拽和投放的内容后，你将在
        <em>
            Cocoa
        </em>
        中发现更多的这些便利方法。
    </p>
    <p>
        找到
        <code>
            performDragOperation(\_:)
        </code>
        ，在最后添加下列的代码，就在return语句
        <code>
            return false
        </code>
        的上面：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">else</span> <span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> image <span style="color: #002200;">=</span> <span style="color: #400080;">NSImage</span><span style="color: #002200;">(</span>pasteboard<span style="color: #002200;">:</span> pasteBoard<span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
  delegate?.processImage<span style="color: #002200;">(</span>image, center<span style="color: #002200;">:</span> point<span style="color: #002200;">)</span>
  <span style="color: #a61390;">return</span> <span style="color: #a61390;">true</span>
<span style="color: #002200;">}</span></pre>
    <p>
        这从粘贴板中抽取一张图片，并传递给delegate来处理。
    </p>
    <p>
        build并执行，然后拖拽独角兽到sticker view上面。
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
        你将注意到，现在你的指针上带有了一个绿色的
        <em>
            +
        </em>
        。
    </p>
    <p>
        destination view接受图片数据，但是当你投放的时候，图片仍然滑到了后面。啊啊啊啊啊啊啊...这里缺少了什么？
    </p>
    <h3>
        向我展示图片数据！
    </h3>
    <p>
        你需要获得拖拽source来提供图片数据 - 换句话说：“履行它的承诺”。
    </p>
    <p>
        打开
        <em>
            ImageSourceView.swift
        </em>
        并用下列代码替换
        <code>
            pasteboard(\_:item:provideDataForType:)
        </code>
        的内容：
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
        在这个方法中，发生了下面的事情：
    </p>
    <ol>
        <li>
            如果期望的数据类型是
            <code>
                kUTTypeTIFF
            </code>
            ，你就加载一个名为
            <em>
                unicorn
            </em>
            的图片。
        </li>
        <li>
            使用提供的助手方法之一，来一任意的颜色给图片染色。毕竟，带颜色的独角兽比几个（a smattering of）全黑的独角兽更喜庆（festive）。:]
        </li>
        <li>
            将图片转为TIFF数据，并将其放置到粘贴板上。
        </li>
    </ol>
    <p>
        运行项目，拖拽独角兽的图片到sticker view上。它将投放带颜色的独角兽到view上。赞！
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
        好多的独角兽！
    </p>
    <h2>
        拖拽定制类型
    </h2>
    <p>
        独角兽是相当棒的（fabulous），但没有星星怎么能好？奇怪的是，没有相应于星星的
        <em>
            Cocoa
        </em>
        数据类型。我打赌你已经知道接下来要做什么了。:]
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/06/sparkle.jpg"
        alt="sparkle" width="400" height="300" class="aligncenter size-full wp-image-136322">
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            在上一部分，提供了你一个标准的数据类型。你可以在
            <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ApplicationKit/Classes/NSPasteboard_Class/index.html#//apple_ref/doc/constant_group/Types_for_Standard_Data_OS_X_v10.6_and_later_"
            target="_blank" title="in the API reference" sl-processed="1">
                API参考
            </a>
            中探索标准数据的类型。
        </p>
    </div>
    <p>
        在这一部分，你将发明你自己的数据类型。
    </p>
    <p>
        在你的to-do列表中有下列任务：
    </p>
    <ol>
        <li>
            用你定制的类型创建一个新的拖拽source。
        </li>
        <li>
            更新拖拽destination来识别这个类型。
        </li>
        <li>
            更新view controller来相应这个类型。
        </li>
    </ol>
    <h3>
        创建拖拽Source
    </h3>
    <p>
        打开
        <em>
            AppActionSourceView.swift
        </em>
        。除了这个重要的定义，它几乎是空的：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">enum</span> SparkleDrag <span style="color: #002200;">{</span>
  <span style="color: #a61390;">static</span> <span style="color: #a61390;">let</span> type <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"com.razeware.StickerDrag.AppAction"</span>
  <span style="color: #a61390;">static</span> <span style="color: #a61390;">let</span> action <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"make sparkles"</span>
<span style="color: #002200;">}</span></pre>
    <p>
        这定义了你定制的拖拽类型，和动作的id。
    </p>
    <p>
        拖拽source的types必须是
        <a href="https://developer.apple.com/library/ios/documentation/FileManagement/Conceptual/understanding_utis/understand_utis_intro/understand_utis_intro.html"
        target="_blank" title="Uniform Type Identifiers" sl-processed="1">
            Uniform Type Identifiers
        </a>
        。这些是描述数据类型的反向编码的名称路径。
    </p>
    <p>
        例如，如果你将
        <code>
            kUTTypeTIFF
        </code>
        的值打印出来，你将看到它的值就是字符串
        <em>
            public.tiff
        </em>
        。
    </p>
    <p>
        为了避免和已存在的类型的冲突，你可以定义id像这样：
        <em>
            bundle identifier
        </em>
        +
        <em>
            AppAction
        </em>
        。这是一个任意的值，但你可以保持它在应用的私有命名空间下，来最小化使用了已存在名称的危险。
    </p>
    <p>
        如果你尝试用一个不是
        <em>
            UTI
        </em>
        的类型构建
        <code>
            NSPasteboardItem
        </code>
        ，和这个操作将会失败。
    </p>
    <p>
        现在你需要让
        <code>
            AppActionSourceView
        </code>
        遵循
        <code>
            NSDraggingSource
        </code>
        协议。打开
        <em>
            AppActionSourceView.swift
        </em>
        并添加下列的extension：
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
        这个代码块和
        <code>
            ImageSourceView
        </code>
        不同，因为你将放置私人的数据到粘贴板上，它们在app的外部是没有意义的。这就是为什么当鼠标被拖拽到你的应用之外时，你使用
        <code>
            context
        </code>
        参数来返回
        <code>
            NSDragOperation()
        </code>
        。
    </p>
    <p>
        你早已熟悉了下一步。你需要覆盖
        <code>
            mouseDown(with:)
        </code>
        事件来用一个粘贴板项目（item）启动一个拖拽session。
    </p>
    <p>
        添加下列的代码到
        <code>
            AppActionSourceView
        </code>
        类的实现中：
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
        在这里你做了什么？
    </p>
    <p>
        你构建了一个粘贴板项目（item），并为你定制的类型，直接将数据放到它内部。在这个case中的数据是一个接收的view可以用来做决定的定制动作的id。
    </p>
    <p>
    	你可以看到这个和
        <code>
            ImageSourceView
        </code>
        在某种程度上的不同之处。投放的数据直接到了粘贴板上，而不是将数据的产生推迟到当view使用
        <code>
            NSPasteboardItemDataProvider
        </code>
        协议接受了投放时。
    </p>
    <p>
    	为什么你要用
        <code>
            NSPasteboardItemDataProvider
        </code>
        协议？因为你希望当你在
        <code>
            mouseDown(with:)
        </code> 
        中开始拖拽session时，东西能够移动得尽可能得快。
    </p>
    <p>
    	如果你移动的数据花费了太长的时间在粘贴板上构建，它会阻塞（jam up）主线程，并在用户开始拖拽时，让他们感受到一个令人沮丧的可察觉的延迟。
    </p>
    <p>
    	在这个case重，你只是放置了一个小字符创到粘贴板上，以便它可以立即执行。
    </p>
    <h3>
    	接受新的类型
    </h3>
    <p>
    	下一步，你必须让destination view接受这个新的类型。现在，你早已知道了怎么可以做到。
    </p>
    <p>
        打开
        <em>
            DestinationView.swift
        </em>
        并添加
        <code>
            SparkleDrag.type
        </code>
        到注册类型。替换下面这行：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">var</span> nonURLTypes<span style="color: #002200;">:</span> Set&lt;String&gt;  <span style="color: #002200;">{</span> <span style="color: #a61390;">return</span> <span style="color: #002200;">[</span><span style="color: #a61390;">String</span><span style="color: #002200;">(</span>kUTTypeTIFF<span style="color: #002200;">)</span><span style="color: #002200;">]</span> <span style="color: #002200;">}</span></pre>
    <p>
        为：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">var</span> nonURLTypes<span style="color: #002200;">:</span> Set&lt;String&gt;  <span style="color: #002200;">{</span> <span style="color: #a61390;">return</span> <span style="color: #002200;">[</span><span style="color: #a61390;">String</span><span style="color: #002200;">(</span>kUTTypeTIFF<span style="color: #002200;">)</span>,SparkleDrag.type<span style="color: #002200;">]</span> <span style="color: #002200;">}</span></pre>
    <p>
    	现在SparkleDrags就可以被接受了！
    </p>
    <p>
        <code>
            performDragOperation(:_)
        </code>
        需要一个新的
        <code>
            else-if
        </code>
        字句，因此添加下列的代码到这个方法的最后
        <code>
            return false
        </code>
        之前：
    </p>
    <pre class="swift" style="font-family:monospace;"><span style="color: #a61390;">else</span> <span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> types <span style="color: #002200;">=</span> pasteBoard.types, types.<span style="color: #a61390;">contains</span><span style="color: #002200;">(</span>SparkleDrag.type<span style="color: #002200;">)</span>,
  <span style="color: #a61390;">let</span> action <span style="color: #002200;">=</span> pasteBoard.string<span style="color: #002200;">(</span>forType<span style="color: #002200;">:</span> SparkleDrag.type<span style="color: #002200;">)</span> <span style="color: #002200;">{</span>
  delegate?.processAction<span style="color: #002200;">(</span>action, center<span style="color: #002200;">:</span>point<span style="color: #002200;">)</span>
  <span style="color: #a61390;">return</span> <span style="color: #a61390;">true</span>
<span style="color: #002200;">}</span></pre>
    <p>
    	这就从粘贴板中抽取了字符串。如果它符合你定制的类型，你就将动作传回给delegate。
    </p>
    <p>
    	你已几乎完成，只需要更新
        <code>
            StickerBoardViewController
        </code>
        来处理动作指令。
    </p>
    <h3>
    	处理动作指令
    </h3>
    <p>
        打开
        <em>
            StickerBoardViewController.swift
        </em>
        并替换
        <code>
            processAction(\_:center:)
        </code>
        为：
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
    	以上代码做了下列的事：
    </p>
    <ol>
        <li>
        	仅响应已知的动作
        </li>
        <li>
        	从bundle中载入一个星的图片
        </li>
        <li>
        	制作一些这个星的图片的拷贝，并...
        </li>
        <ol>
            <li>
            	生成一些随机的数字来改变星的位置。
            </li>
            <li>
            	创建一个
                <code>
                    NSImageView
                </code>
                并设置它的frame。
            </li>
            <li>
            	这个图片设定一个随机的颜色 - 除非你要向David Bowie致敬（tribute），黑色的星总是有些野蛮。
            	（译者注：David Bowie是英国著名的摇滚音乐家，2016年去世，《Blackstar》是其遗作，在59届格莱美奖中获五项大奖）
            </li>
            <li>
            	放置图片到这个view上。
            </li>
        </ol>
    </ol>
    <p>
    	运行项目。现在你可以拖拽星星的view到sticker view上了，来添加“一阵”（a spray of）星星到你的view上。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/06/final-361x500.png"
        alt="final" width="361" height="500" class="aligncenter size-large wp-image-136566"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/06/final-361x500.png 361w, https://koenig-media.raywenderlich.com/uploads/2016/06/final-231x320.png 231w, https://koenig-media.raywenderlich.com/uploads/2016/06/final.png 480w"
        sizes="(max-width: 361px) 100vw, 361px">
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
    	恭喜，你已经在你自己的app中创建了一个定制的拖放UI！
    </p>
    <p>
    	你可以使用
        <em>
            Save Image To Desktop
        </em>
        按钮来保存你的图片作为一个
        <em>
            JPG
        </em>
        ，名叫
        <em>
            StickerDrag
        </em>
        。或者更进一步，将它发送给
        <a href="https://twitter.com/rwenderlich" target="_blank" sl-processed="1">
            @rwenderlich
        </a>
        的团队。
    </p>
    <p>
    	这里是完整项目的
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/08/StickerDrag-Final_S3-b6.zip"
        sl-processed="1">
	        源码
        </a>
        。
    </p>
    <p>
    	这个macOS的拖放教程，覆盖了Cocoa拖放机制的基础，包括：
    </p>
    <ul>
        <li>
        	创建一个拖拽destination并接受几种不同类型的数据
        </li>
        <li>
        	使用拖拽session的生命循环，来提供给用户拖拽操作的反馈
        </li>
        <li>
        	从粘贴板中解码信息
        </li>
        <li>
        	创建一个拖拽source，并提供推迟的数据
        </li>
        <li>
        	创建一个提供指定数据类型的拖拽source
        </li>
    </ul>
    <p>
    	现在你已经有了用来在任意mac app中支持拖放的知识和经验了。
    </p>
    <p>
    	这里有更多要去学的。
    </p>
    <p>
    	你可以学习诸如如何在拖拽期间改变拖拽的图片，或实现一个动画的投放过渡效果，或使用承诺的文件 - Photos是一个应用程序，可将承诺的数据放在拖拽粘贴板上。
    </p>
    <p>
    	另一个有趣的话题是怎么在
        <code>
            NSTableView
        </code>
        和
        <code>
            NSOutlineView
        </code>
        中使用拖放，它们的工作方式略有不同。可以在以下的资源中进行了解：
    </p>
    <ul>
        <li>
            苹果的
            <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/DragandDrop/DragandDrop.html"
            target="_blank" title="Drag and Drop Programming Topics" sl-processed="1">
            	拖拽编程话题
            </a>
        </li>
        <li>
	        苹果的
            <a href="https://developer.apple.com/library/mac/documentation/Security/Conceptual/AppSandboxDesignGuide/AppSandboxInDepth/AppSandboxInDepth.html#//apple_ref/doc/uid/TP40011183-CH3-SW16"
            target="_blank" title="Sandboxing and Security Scoped Data" sl-processed="1">
            	沙盒和安全范围内的数据
            </a>
            ，在这里你将找到，有关如果应用在沙盒中，如何让拖拽生效。
        </li>
        <li>
        	示例代码（用OC写的）：
            <a href="https://developer.apple.com/library/mac/samplecode/CocoaDragAndDrop/Introduction/Intro.html"
            target="_blank" title="CocoaDragAndDrop" sl-processed="1">
                CocoaDragAndDrop
            </a>            
        </li>
        <li>
        	示例代码（用OC写的）：
            <a href="https://developer.apple.com/library/prerelease/content/samplecode/DragNDropOutlineView/Introduction/Intro.html"
            target="_blank" title="DragNDropOutlineView" sl-processed="1">
                DragNDropOutlineView
            </a>
        </li>
    </ul>
    <p>
    	如果你有任何关于这个macOS的拖放教程的问题或意见，请加入下面的讨论！记住，有时候生活是拖拽的体验，但每件事遇到独角兽和星星都会变得更好。:]
    </p>
</div>
