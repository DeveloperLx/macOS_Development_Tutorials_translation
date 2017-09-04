# OS X教程：高级Collection Views

#### [原文地址](https://www.raywenderlich.com/132268/advanced-collection-views-os-x-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/05/CollectionViews-adv-feature-250x250.png"
        alt="Advanced Collection Views in OS X Tutorial" width="250" height="250"
        class="alignright size-full wp-image-132621 bordered">
    </p>
    <p>
        如果你想了解
        <code>
            NSCollectionView
        </code>
        的高级特性，恭喜你来对了地方。这里是第二部分的教程，关于OS X中Collection View的高级特性，你已经深入到了collection view所围绕的世界中。
    </p>
    <p>
        在这篇教程中，你将学到如何：
    </p>
    <ul>
        <li>
            添加，删除，移动，以及重新排列项目
        </li>
        <li>
            实现拖拽collection view
        </li>
        <li>
            调整选择和高亮的效果
        </li>
        <li>
            在collection view中使用动画
        </li>
        <li>
            实现实现黏性的section头
        </li>
    </ul>
    <h2>
        预备知识
    </h2>
    <p>
        你需要了解关于
        <code>
            NSCollectionView
        </code>
        的基础知识，以及来自于
        <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Collection%20Views%20in%20OS%20X%20Tutorial.md"
        title="Collection Views tutorial" target="_blank">
            Collection View教程
        </a>
        的项目相关的内容。
    </p>
    <h2>
        入门
    </h2>
    <p>
        你将要构建的app叫做
        <em>
            SlidesPro
        </em>
        ，他会从之前教程撂下的地方再捡起来再继续。
    </p>
    <p>
        在
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesPro-Starter.zip">
            这里
        </a>
        下载
        <em>
            SlidesPro
        </em>
        的初始项目。
    </p>
    <p>
        运行项目。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProStarterScreen.png"
        rel="attachment wp-att-132276">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProStarterScreen-408x500.png"
            alt="SlidesProStarterScreen" width="408" height="500" class="aligncenter size-large wp-image-132276"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProStarterScreen-408x500.png 408w, https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProStarterScreen-261x320.png 261w, https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProStarterScreen-768x942.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProStarterScreen.png 960w"
            sizes="(max-width: 408px) 100vw, 408px">
        </a>
    </p>
    <h2>
        添加新的图像到Collection View
    </h2>
    <p>
        在这一部分，你将会浏览添加新的item到collection的步骤。
    </p>
    <h3>
        添加按钮
    </h3>
    <p>
        在实现相应的功能之前，你无法向collection view添加任何内容。好在你是一个开发者！现在这里需要一个按钮，点击它展示一个标准的打开面板，来选择你想要的图片。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        并拖拽一个
        <em>
            Push Button
        </em>
        到collection view的底部。在
        <em>
            Attributes Inspector
        </em>
        中，设置它的
        <em>
            Title
        </em>
        为
        <em>
            Add
        </em>
        ，并取消勾选
        <em>
            Enabled
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Slide-Button.png"
        rel="attachment wp-att-132280">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Slide-Button-625x500.png"
            alt="Add Slide Button" width="625" height="500" class="aligncenter size-large wp-image-132280"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Slide-Button-625x500.png 625w, https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Slide-Button-400x320.png 400w, https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Slide-Button-768x614.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Slide-Button.png 835w"
            sizes="(max-width: 625px) 100vw, 625px">
        </a>
    </p>
    <p>
        选择
        <em>
            Editor \ Resolve Auto Layout Issues \ Add Missing Constraints
        </em>
        菜单项来设置按钮的
        <em>
            自动布局
        </em>
        约束。
    </p>
    <p>
        运行项目，查看你是否已得到了button。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Button-Added.png"
        rel="attachment wp-att-132282">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Button-Added-700x288.png"
            alt="Add Button Added" width="700" height="288" class="aligncenter size-large wp-image-132282"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Button-Added-700x288.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Button-Added-480x197.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Button-Added-768x316.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Button-Added.png 956w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <h3>
        指定在什么地方插入新的item
    </h3>
    <p>
        <em>
            SlidesPro
        </em>
        当你选择了一个item的时候，新的item就被插入到了那个item的index path位置上。之后那个item和其后的item就会被推移到新的item之后。
    </p>
    <p>
        因此，这个添加按钮就应该只有在某个item被选中时才可使用。
    </p>
    <p>
        在
        <code>
            ViewController
        </code>
        中，为按钮添加一个
        <code>
            IBOutlet
        </code>
        ：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-meta"><font><font>@IBOutlet </font></font></span> <span class="hljs-keyword"><font><font>weak </font></font></span> <span class="hljs-keyword"><font><font>var</font></font></span><font><font> addSlideButton：</font></font><span class="hljs-type"><font><font>NSButton</font></font></span><font><font>！ 
</font></font></pre>
    <p>
        接下来，打开
        <em>
            Main.storyboard
        </em>
        并连接outlet到按钮上。
    </p>
    <p>
        你需要去跟踪item选择的变化，以在ViewController的方法
        <code>
            highlightItems(\_: atIndexPaths:)
        </code>
        中确定这个按钮的打开和关闭。当选择或取消选择一个item时，它就会被两个
        <code>
            NSCollectionViewDelegate
        </code>
        的方法去调用。
    </p>
    <p>
        为了实现这点，只需要添加一行代码到
        <code>
            highlightItems(\_: atIndexPaths:)
        </code>
        方法中：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword"><font><font>func </font></font></span> <span class="hljs-title"><font><font>highlightItems </font></font></span><span class="hljs-params"><font><font>（selected：Bool，atIndexPaths：Set &lt;NSIndexPath&gt;）</font></font></span></span><font><font> {</font></font><font></font><font><font>
    .......</font></font><font></font><font><font>
    .......</font></font><font></font><font><font>
    addSlideButton.enabled = collectionView.selectionIndexPaths。</font></font><span class="hljs-built_in"><font><font>count</font></font></span><font><font> == </font></font><span class="hljs-number"><font><font>1</font></font></span><font></font><font><font>
  }</font></font><font></font>
</pre>
    <p>
        这样这个按钮就只会在某个item被选中时才打开了。
        <br>
        运行项目。验证仅当某个item被选中时才能够使用。
        <br>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/05/First_Run.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/05/First_Run-264x320.png"
            alt="First_Run" width="408" height="494" class="aligncenter size-medium wp-image-134402"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/05/First_Run-264x320.png 264w, https://koenig-media.raywenderlich.com/uploads/2016/05/First_Run-412x500.png 412w, https://koenig-media.raywenderlich.com/uploads/2016/05/First_Run.png 1440w"
            sizes="(max-width: 408px) 100vw, 408px">
        </a>
    </p>
    <h3>
        插入新的项目
    </h3>
    <p>
        添加一个新的item到collection view包含两个步骤。首先，添加item到model中，然后，通知collection view这个变化。
    </p>
    <div class="note">
        <em>
            注意
        </em>
        ：在进行编辑时，诸如添加，删除和移动，你必须首先更新model，然后再通知collection view来更新它的布局。
    </div>
    <p>
        要更新你的model，你需要添加下列的代码到
        <code>
            ImageDirectoryLoader
        </code>
        类中：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">insertImage</span><span class="hljs-params">(image: ImageFile, atIndexPath: NSIndexPath)</span></span> {
    <span class="hljs-keyword">let</span> imageIndexInImageFiles = sectionsAttributesArray[atIndexPath.section].sectionOffset + atIndexPath.item
    imageFiles.insert(image, atIndex: imageIndexInImageFiles)
    <span class="hljs-keyword">let</span> sectionToUpdate = atIndexPath.section
    sectionsAttributesArray[sectionToUpdate].sectionLength += <span class="hljs-number">1</span>
    sectionLengthArray[sectionToUpdate] += <span class="hljs-number">1</span>
    <span class="hljs-keyword">if</span> sectionToUpdate &lt; numberOfSections-<span class="hljs-number">1</span> {
      <span class="hljs-keyword">for</span> i <span class="hljs-keyword">in</span> sectionToUpdate+<span class="hljs-number">1</span>...numberOfSections-<span class="hljs-number">1</span> {
        sectionsAttributesArray[i].sectionOffset += <span class="hljs-number">1</span>
      }
    }
  }
</pre>
    <p>
        这个方法插入了新的图片到你的数据model中，并更新相关的内容，这样就保持了你的model保持在一个一致的状态。
    </p>
    <p>
        添加下列的方法到
        <code>
            ViewController
        </code>
        中。第一个方法会被
        <code>
            IBAction
        </code>
        在动作方法中调用，第二个就是这个动作方法了，它会在点击添加按钮时被调用：
    </p>
    <pre lang="swift" class="language-swift hljs">   <span class="hljs-keyword">private</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">insertAtIndexPathFromURLs</span><span class="hljs-params">(urls: [NSURL], atIndexPath: NSIndexPath)</span></span> {
    <span class="hljs-keyword">var</span> indexPaths: <span class="hljs-type">Set</span>&lt;<span class="hljs-type">NSIndexPath</span>&gt; = []
    <span class="hljs-keyword">let</span> section = atIndexPath.section
    <span class="hljs-keyword">var</span> currentItem = atIndexPath.item
    <span class="hljs-comment">// 1</span>
    <span class="hljs-keyword">for</span> url <span class="hljs-keyword">in</span> urls {
      <span class="hljs-comment">// 2</span>
      <span class="hljs-keyword">let</span> imageFile = <span class="hljs-type">ImageFile</span>(url: url)
      <span class="hljs-keyword">let</span> currentIndexPath = <span class="hljs-type">NSIndexPath</span>(forItem: currentItem, inSection: section)
      imageDirectoryLoader.insertImage(imageFile, atIndexPath: currentIndexPath)
      indexPaths.insert(currentIndexPath)
      currentItem += <span class="hljs-number">1</span>
    }
    <span class="hljs-comment">// 3</span>
    collectionView.insertItemsAtIndexPaths(indexPaths)
  }

  <span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">addSlide</span><span class="hljs-params">(sender: NSButton)</span></span> {
    <span class="hljs-comment">// 4</span>
    <span class="hljs-keyword">let</span> insertAtIndexPath = collectionView.selectionIndexPaths.first!
    <span class="hljs-comment">//5</span>
    <span class="hljs-keyword">let</span> openPanel = <span class="hljs-type">NSOpenPanel</span>()
    openPanel.canChooseDirectories = <span class="hljs-literal">false</span>
    openPanel.canChooseFiles = <span class="hljs-literal">true</span>
    openPanel.allowsMultipleSelection = <span class="hljs-literal">true</span>;
    openPanel.allowedFileTypes = [<span class="hljs-string">"public.image"</span>]
    openPanel.beginSheetModalForWindow(<span class="hljs-keyword">self</span>.view.window!) { (response) -&gt; <span class="hljs-type">Void</span> <span class="hljs-keyword">in</span>
      <span class="hljs-keyword">guard</span> response == <span class="hljs-type">NSFileHandlingPanelOKButton</span> <span class="hljs-keyword">else</span> {<span class="hljs-keyword">return</span>}
      <span class="hljs-keyword">self</span>.insertAtIndexPathFromURLs(openPanel.<span class="hljs-type">URLs</span>, atIndexPath: insertAtIndexPath)
    }
  }
</pre>
    <ol>
        <li>
            迭代从
            <em>
                Open
            </em>
            面板中选择的
            <em>
                URLs
            </em>
            。
        </li>
        <li>
            由每个
            <em>
                URL
            </em>
            创建一个
            <code>
                ImageFile
            </code>
            实例，并添加到model中。
        </li>
        <li>
            通知给collection view。
        </li>
        <li>
            根据被选择的那个item的
            <code>
                NSIndexPath
            </code>
            觉得从什么地方插入。
        </li>
        <li>
            创建一个
            <code>
                NSOpenPanel
            </code>
            ，并配置为只允许选择图片文件，然后展示它。
        </li>
    </ol>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        并将
        <code>
            addSlide(\_:)
        </code>
        这个
        <code>
            IBAction
        </code>
        连接到这个按钮上。
    </p>
    <p>
        运行项目。
    </p>
    <p>
        选择第一部分的最后一张图片 -- 在我的系统上是
        <em>
            Desert.jpg
        </em>
        。
    </p>
    <p>
        点击
        <em>
            Add
        </em>
        按钮。在
        <em>
            Open
        </em>
        面板中找到位于项目根目录下的
        <em>
            My Private Zoo
        </em>
        目录，并选中全部文件。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/MyPrivateZoo.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/MyPrivateZoo-700x408.png"
            alt="MyPrivateZoo" width="700" height="408" class="aligncenter size-large wp-image-132304"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/MyPrivateZoo-700x408.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/MyPrivateZoo-480x280.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/MyPrivateZoo.png 734w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        点击
        <em>
            Open
        </em>
        。app将会在第一部分插入新的图像，从item 2的位置开始，
        <em>
            Desert.jpg
        </em>
        之前。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/ZooBeforeAfter.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/ZooBeforeAfter-700x459.png"
            alt="ZooBeforeAfter" width="700" height="459" class="aligncenter size-large wp-image-132313"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/ZooBeforeAfter-700x459.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/ZooBeforeAfter-480x314.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/ZooBeforeAfter-768x503.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/ZooBeforeAfter.png 974w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <h2>
        从Collection View中移除item
    </h2>
    <p>
        在SlidesPro中，你需要一个移除按钮来移除item，可以把它摆在添加按钮的旁边。最合乎逻辑的实现就是移除掉全部被选中的项目，因此，这个应当当且仅当一个或多个项目被选择是才可用。
    </p>
    <p>
        接下来就是细节了：多选必须允许你一次同时控制多个图片。
    </p>
    <p>
        这一部分将一步步地带领你添加这个按钮及打开多选。
    </p>
    <h3>
        打开多选
    </h3>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        并选择
        <em>
            Collection View
        </em>
        。并在
        <em>
            Attributes Inspector
        </em>
        中，勾选
        <em>
            Allows Multiple Selection
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/MultipleSelection.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/MultipleSelection.png"
            alt="MultipleSelection" width="259" height="385" class="aligncenter size-full wp-image-132314"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/MultipleSelection.png 259w, https://koenig-media.raywenderlich.com/uploads/2016/04/MultipleSelection-215x320.png 215w"
            sizes="(max-width: 259px) 100vw, 259px">
        </a>
    </p>
    <p>
        运行项目，并验证多选正常work。
    </p>
    <p>
        要增加或减少collection的选择，就按住
        <em>
            shift
        </em>
        或
        <em>
            command
        </em>
        键，再来点击各种item，就可以实现多选了。
    </p>
    <h3>
        移除按钮
    </h3>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        ，并从
        <em>
            Object Library
        </em>
        中拖拽一个
        <em>
            Push Button
        </em>
        ，并将它拖拽到
        <em>
            Add
        </em>
        按钮的左边。
    </p>
    <p>
        在
        <em>
            Attributes Inspector
        </em>
        中，设置它的
        <em>
            Title
        </em>
        为
        <em>
            Remove
        </em>
        ，并取消勾选
        <em>
            Enabled
        </em>
        。
        <br>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/05/RemoveButton.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/05/RemoveButton-480x314.png"
            alt="RemoveButton" width="480" height="314" class="aligncenter size-medium wp-image-134403"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/05/RemoveButton-480x314.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/05/RemoveButton-650x425.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/05/RemoveButton.png 1600w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
        <br>
        通过选择
        <em>
            Editor \ Resolve Auto Layout Issues \ Add Missing Constraints
        </em>
        菜单项，设置按钮的
        <em>
            Auto Layout
        </em>
        约束。
    </p>
    <p>
        运行项目。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/RemoveBtnAdded.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/RemoveBtnAdded-700x308.png"
            alt="RemoveBtnAdded" width="700" height="308" class="aligncenter size-large wp-image-132318"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/RemoveBtnAdded-700x308.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/RemoveBtnAdded-480x211.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/RemoveBtnAdded-768x338.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/RemoveBtnAdded.png 957w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        在
        <code>
            ViewController
        </code>
        中，添加一个
        <code>
            IBOutlet
        </code>
        ：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-meta">@IBOutlet</span> <span class="hljs-keyword">weak</span> <span class="hljs-keyword">var</span> removeSlideButton: <span class="hljs-type">NSButton</span>!
</pre>
    <p>
        接下来，打开
        <em>
            Main.storyboard
        </em>
        并连接这个outlet到按钮上。
    </p>
    <p>
        在
        <code>
            ViewController
        </code>
        中，
        <code>
            highlightItems(\_: atIndexPaths:)
        </code>
        的尾部，添加下列的代码来控制移除按钮的打开/禁用。
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">highlightItems</span><span class="hljs-params">(selected: Bool, atIndexPaths: Set&lt;NSIndexPath&gt;)</span></span> {
    .......
    .......
    removeSlideButton.enabled = !collectionView.selectionIndexPaths.isEmpty
  }
</pre>
    <p>
        运行项目，然后选择一个item。现在添加按钮和移除按钮都应变为可用了。选中更多的item，这是添加按钮就应变为禁用了，而移除按钮仍保持可用。
    </p>
    <h3>
        实现移除item
    </h3>
    <p>
        现在你就要添加代码来从collection中移除item了。正如添加一样，移除分为两个步骤，你需要首先移除相应图片的model，然后再通知给collection view相应的变化。
    </p>
    <p>
        要更新model，添加下列的方法到
        <code>
            ImageDirectoryLoader
        </code>
        类的尾部：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">removeImageAtIndexPath</span><span class="hljs-params">(indexPath: NSIndexPath)</span></span> -&gt; <span class="hljs-type">ImageFile</span> {
    <span class="hljs-keyword">let</span> imageIndexInImageFiles = sectionsAttributesArray[indexPath.section].sectionOffset + indexPath.item
    <span class="hljs-keyword">let</span> imageFileRemoved = imageFiles.removeAtIndex(imageIndexInImageFiles)
    <span class="hljs-keyword">let</span> sectionToUpdate = indexPath.section
    sectionsAttributesArray[sectionToUpdate].sectionLength -= <span class="hljs-number">1</span>
    <span class="hljs-keyword">if</span> sectionToUpdate &lt; numberOfSections-<span class="hljs-number">1</span> {
      <span class="hljs-keyword">for</span> i <span class="hljs-keyword">in</span> sectionToUpdate+<span class="hljs-number">1</span>...numberOfSections-<span class="hljs-number">1</span> {
        sectionsAttributesArray[i].sectionOffset -= <span class="hljs-number">1</span>
      }
    }
    <span class="hljs-keyword">return</span> imageFileRemoved
  }
</pre>
    <p>
        在
        <code>
            ViewController
        </code>
        中，添加
        <code>
            IBAction
        </code>
        方法，它会在你点击
        <em>
            Remove
        </em>
        按钮时被触发：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">removeSlide</span><span class="hljs-params">(sender: NSButton)</span></span> {
    <span class="hljs-keyword">let</span> selectionIndexPaths = collectionView.selectionIndexPaths
    <span class="hljs-keyword">if</span> selectionIndexPaths.isEmpty {
      <span class="hljs-keyword">return</span>
    }
    <span class="hljs-comment">// 1</span>
    <span class="hljs-keyword">var</span> selectionArray = <span class="hljs-type">Array</span>(selectionIndexPaths)
    selectionArray.sortInPlace({path1, path2 <span class="hljs-keyword">in</span> <span class="hljs-keyword">return</span> path1.compare(path2) == .<span class="hljs-type">OrderedDescending</span>})
    <span class="hljs-keyword">for</span> itemIndexPath <span class="hljs-keyword">in</span> selectionArray {
      <span class="hljs-comment">// 2</span>
      imageDirectoryLoader.removeImageAtIndexPath(itemIndexPath)
    }
    <span class="hljs-comment">// 3</span>
    collectionView.deleteItemsAtIndexPaths(selectionIndexPaths)
  }
</pre>
    <p>
        上述代码：
    </p>
    <ol>
        <li>
            创建一个数组，依据index path逆序迭代选择的item，这样你就不需要在迭代过程中调整index path了
        </li>
        <li>
            从model中移除选中的item
        </li>
        <li>
            通知collection view item已被移除
        </li>
    </ol>
    <p>
        现在，打开
        <em>
            Main.storyboard
        </em>
        并连接
        <code>
            removeSlide(\_:) IBAction
        </code>
        到移除按钮上。
    </p>
    <p>
        添加outlet和action后，
        <em>
            View Controller
        </em>
        的
        <em>
            Connections Inspector
        </em>
        看起来应当是这个样子：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProActionsOutlets.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProActionsOutlets.png"
            alt="SlidesProActionsOutlets" width="259" height="445" class="aligncenter size-full wp-image-132726"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProActionsOutlets.png 259w, https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProActionsOutlets-186x320.png 186w"
            sizes="(max-width: 259px) 100vw, 259px">
        </a>
    </p>
    <p>
        运行项目。
    </p>
    <p>
        选择一个或多个图片，并点击
        <em>
            Remove
        </em>
        按钮，来验证是否成功地移除了item。
    </p>
    <h2>
        Collection View中的拖拽
    </h2>
    <p>
        OS X中有一个最棒的事，是你可以将一个item拖拽或copy到另一个app中。用户是非常期待这个功能的，因此为你的app加入这个特性是一个非常英明的决定。
    </p>
    <p>
        在SlidesPro中，你将使用拖拽来实现下述的能力：
    </p>
    <ul>
        <li>
            在collection view中移动item
        </li>
        <li>
            从其它app从移动图片到collection view中
        </li>
        <li>
            将collection view中的item拖拽到其它app中
        </li>
    </ul>
    <p>
        要支持拖拽的功能，你就要实现
        <code>
            NSCollectionViewDelegate
        </code>
        协议中的相关方法，但首先要注册SlidesPro对于拖拽操作的支持。
    </p>
    <p>
        添加下列的方法到
        <code>
            ViewController
        </code>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">registerForDragAndDrop</span><span class="hljs-params">()</span></span> {
    <span class="hljs-comment">// 1</span>
    collectionView.registerForDraggedTypes([<span class="hljs-type">NSURLPboardType</span>])
    <span class="hljs-comment">// 2</span>
    collectionView.setDraggingSourceOperationMask(<span class="hljs-type">NSDragOperation</span>.<span class="hljs-type">Every</span>, forLocal: <span class="hljs-literal">true</span>)
    <span class="hljs-comment">// 3</span>
    collectionView.setDraggingSourceOperationMask(<span class="hljs-type">NSDragOperation</span>.<span class="hljs-type">Every</span>, forLocal: <span class="hljs-literal">false</span>)
  }
</pre>
    <p>
        上述代码中：
    </p>
    <ol>
        <li>
            注册了SlidesPro可以接收的对象的类型
        </li>
        <li>
            打开了允许item在collection view内进行拖拽的特性
        </li>
        <li>
            打开了允许将item从collection view拖拽到其它app中的特性
        </li>
    </ol>
    <p>
        在
        <code>
            viewDidLoad()
        </code>
        的尾部，添加下述代码：
    </p>
    <pre lang="swift" class="language-swift hljs">registerForDragAndDrop()
    </pre>
    <p>
        允许项目。
    </p>
    <p>
        尝试拖拽一个item -- 但item并未移动。从Finder中拖拽一个图片文件到collection view中...呃。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/Screen-Shot-2016-05-08-at-4.34.29-PM.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/Screen-Shot-2016-05-08-at-4.34.29-PM.png"
            alt="What about left-clicking for 5 seconds...while kissing my elbow?"
            width="432" height="342" class="aligncenter size-full wp-image-133795">
        </a>
    </p>
    <p>
        I asked you to perform this test so you can see that items aren't responding
        to dragging, and nothing related to drag-and-drop works. Why is that? You'll
        soon discover.
    </p>
    <p>
        The first issue is that there needs to be some additional logic to handle
        the action, so append the following methods to the
        <code>
            NSCollectionViewDelegate
        </code>
        extension of
        <code>
            ViewController
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                collectionView
            </span>
            <span class="hljs-params">
                (collectionView: NSCollectionView, canDragItemsAtIndexes indexes: NSIndexSet,
                withEvent event: NSEvent)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            Bool
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-literal">
            true
        </span>
        }
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                collectionView
            </span>
            <span class="hljs-params">
                (collectionView: NSCollectionView, pasteboardWriterForItemAtIndexPath
                indexPath: NSIndexPath)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            NSPasteboardWriting
        </span>
        ? {
        <span class="hljs-keyword">
            let
        </span>
        imageFile = imageDirectoryLoader.imageFileForIndexPath(indexPath)
        <span class="hljs-keyword">
            return
        </span>
        imageFile.url.absoluteURL }
    </pre>
    <p>
        Here's what's happening in here:
    </p>
    <ol>
        <li>
            When the collection view is about to start a drag operation, it sends
            this message to its
            <code>
                delegate
            </code>
            . The return value indicates whether the collection view is allowed to
            initiate the drag for the specified index paths. You need to be able to
            drag any item, so you return unconditionally
            <code>
                true
            </code>
            .
        </li>
        <li>
            Implementing this method is essential so the collection view can be a
            <em>
                Drag Source
            </em>
            . If the method in section one allows the drag to begin, the collection
            view invokes this method one time per item to be dragged. It requests a
            pasteboard writer for the item's underlying model object. The method returns
            a custom object that implements
            <code>
                NSPasteboardWriting
            </code>
            ; in your case it's
            <code>
                NSURL
            </code>
            . Returning
            <code>
                nil
            </code>
            prevents the drag.
        </li>
    </ol>
    <p>
        Build and run.
    </p>
    <p>
        Try to drag an item, the item moves… Hallelujah!
    </p>
    <p>
        Perhaps I spoke too soon? When you try to drop the item in a different
        location in the collection view, it just bounces back. Why? Because you
        did not define the collection view as a
        <em>
            Drop Target
        </em>
        .
    </p>
    <p>
        Now try to drag an item and drop it in Finder; a new image file is created
        matching the source
        <em>
            URL
        </em>
        . You
        <i>
            have
        </i>
        made progress because it works to drag-and-drop from
        <em>
            SlidesPro
        </em>
        to another app!
    </p>
    <h3>
        Define Your Drop Target
    </h3>
    <p>
        Add the following property to
        <code>
            ViewController
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            var
        </span>
        indexPathsOfItemsBeingDragged:
        <span class="hljs-type">
            Set
        </span>
        &lt;
        <span class="hljs-type">
            NSIndexPath
        </span>
        &gt;!
    </pre>
    <p>
        Add the following methods to the
        <code>
            NSCollectionViewDelegate
        </code>
        extension of
        <code>
            ViewController
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                collectionView
            </span>
            <span class="hljs-params">
                (collectionView: NSCollectionView, draggingSession session: NSDraggingSession,
                willBeginAtPoint screenPoint: NSPoint, forItemsAtIndexPaths indexPaths:
                Set&lt;NSIndexPath&gt;)
            </span>
        </span>
        { indexPathsOfItemsBeingDragged = indexPaths }
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                collectionView
            </span>
            <span class="hljs-params">
                (collectionView: NSCollectionView, validateDrop draggingInfo: NSDraggingInfo,
                proposedIndexPath proposedDropIndexPath: AutoreleasingUnsafeMutablePointer&lt;NSIndexPath?&gt;,
                dropOperation proposedDropOperation: UnsafeMutablePointer&lt;NSCollectionViewDropOperation&gt;)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            NSDragOperation
        </span>
        {
        <span class="hljs-comment">
            // 3
        </span>
        <span class="hljs-keyword">
            if
        </span>
        proposedDropOperation.memory ==
        <span class="hljs-type">
            NSCollectionViewDropOperation
        </span>
        .
        <span class="hljs-type">
            On
        </span>
        { proposedDropOperation.memory =
        <span class="hljs-type">
            NSCollectionViewDropOperation
        </span>
        .
        <span class="hljs-type">
            Before
        </span>
        }
        <span class="hljs-comment">
            // 4
        </span>
        <span class="hljs-keyword">
            if
        </span>
        indexPathsOfItemsBeingDragged ==
        <span class="hljs-literal">
            nil
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-type">
            NSDragOperation
        </span>
        .
        <span class="hljs-type">
            Copy
        </span>
        }
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-type">
            NSDragOperation
        </span>
        .
        <span class="hljs-type">
            Move
        </span>
        } }
    </pre>
    <p>
        Here's a section-by-section breakdown of this code:
    </p>
    <ol>
        <li>
            An
            <code>
                optional
            </code>
            method is invoked when the dragging session is imminent. You'll use this
            method to save the index paths of the items that are dragged. When this
            property is not
            <code>
                nil
            </code>
            , it's an indication that the
            <em>
                Drag Source
            </em>
            is the collection view.
        </li>
        <li>
            Implement the delegation methods related to drop. This method returns
            the type of operation to perform.
        </li>
        <li>
            In
            <em>
                SlidesPro
            </em>
            , the items aren't able to act as containers; this allows dropping between
            items but not dropping on them.
        </li>
        <li>
            When moving items inside the collection view, the operation is
            <code>
                Move
            </code>
            . When the
            <em>
                Dragging Source
            </em>
            is another app, the operation is
            <code>
                Copy
            </code>
            .
        </li>
    </ol>
    <p>
        Build and run.
    </p>
    <p>
        Drag an item. After you move it, you'll see some weird gray rectangle
        with white text. As you keep moving the item over the other items, the
        same rectangle appears in the gap between the items.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/HeaderAsInterGapIndicator.gif">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/HeaderAsInterGapIndicator-700x404.gif"
            alt="HeaderAsInterGapIndicator" width="700" height="404" class="aligncenter size-large wp-image-132798"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/HeaderAsInterGapIndicator-700x404.gif 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/HeaderAsInterGapIndicator-480x277.gif 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/HeaderAsInterGapIndicator-768x444.gif 768w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        What is happening?
    </p>
    <p>
        Inside of
        <code>
            ViewController
        </code>
        , look at the
        <code>
            DataSource
        </code>
        method that's invoked when the collection view asks for a supplementary
        view:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                collectionView
            </span>
            <span class="hljs-params">
                (collectionView: NSCollectionView, viewForSupplementaryElementOfKind kind:
                String, atIndexPath indexPath: NSIndexPath)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            NSView
        </span>
        {
        <span class="hljs-keyword">
            let
        </span>
        view = collectionView.makeSupplementaryViewOfKind(
        <span class="hljs-type">
            NSCollectionElementKindSectionHeader
        </span>
        , withIdentifier:
        <span class="hljs-string">
            "HeaderView"
        </span>
        , forIndexPath: indexPath)
        <span class="hljs-keyword">
            as
        </span>
        !
        <span class="hljs-type">
            HeaderView
        </span>
        view.sectionTitle.stringValue =
        <span class="hljs-string">
            "Section
            <span class="hljs-subst">
                \(indexPath.section)
            </span>
            "
        </span>
        <span class="hljs-keyword">
            let
        </span>
        numberOfItemsInSection = imageDirectoryLoader.numberOfItemsInSection(indexPath.section)
        view.imageCount.stringValue =
        <span class="hljs-string">
            "
            <span class="hljs-subst">
                \(numberOfItemsInSection)
            </span>
            image files"
        </span>
        <span class="hljs-keyword">
            return
        </span>
        view }
    </pre>
    <p>
        When you start dragging an item, the collection view’s layout asks for
        the interim gap indicator’s supplementary view. The above
        <code>
            DataSource
        </code>
        method unconditionally assumes that this is a request for a header view.
        Accordingly, a header view is returned and displayed for the inter-item
        gap indicator.
    </p>
    <p>
        None of this is going to work for you so replace the content of this method
        with:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                collectionView
            </span>
            <span class="hljs-params">
                (collectionView: NSCollectionView, viewForSupplementaryElementOfKind kind:
                String, atIndexPath indexPath: NSIndexPath)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            NSView
        </span>
        {
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-keyword">
            let
        </span>
        identifier:
        <span class="hljs-type">
            String
        </span>
        = kind ==
        <span class="hljs-type">
            NSCollectionElementKindSectionHeader
        </span>
        ?
        <span class="hljs-string">
            "HeaderView"
        </span>
        :
        <span class="hljs-string">
            ""
        </span>
        <span class="hljs-keyword">
            let
        </span>
        view = collectionView.makeSupplementaryViewOfKind(kind, withIdentifier:
        identifier, forIndexPath: indexPath)
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-keyword">
            if
        </span>
        kind ==
        <span class="hljs-type">
            NSCollectionElementKindSectionHeader
        </span>
        {
        <span class="hljs-keyword">
            let
        </span>
        headerView = view
        <span class="hljs-keyword">
            as
        </span>
        !
        <span class="hljs-type">
            HeaderView
        </span>
        headerView.sectionTitle.stringValue =
        <span class="hljs-string">
            "Section
            <span class="hljs-subst">
                \(indexPath.section)
            </span>
            "
        </span>
        <span class="hljs-keyword">
            let
        </span>
        numberOfItemsInSection = imageDirectoryLoader.numberOfItemsInSection(indexPath.section)
        headerView.imageCount.stringValue =
        <span class="hljs-string">
            "
            <span class="hljs-subst">
                \(numberOfItemsInSection)
            </span>
            image files"
        </span>
        }
        <span class="hljs-keyword">
            return
        </span>
        view }
    </pre>
    <p>
        Here's what you did in here:
    </p>
    <ol>
        <li>
            You set the
            <code>
                identifier
            </code>
            according to the
            <code>
                kind
            </code>
            parameter received. When it isn't a header view, you set the
            <code>
                identifier
            </code>
            to the empty
            <code>
                String
            </code>
            . When you pass to
            <code>
                makeSupplementaryViewOfKind
            </code>
            an
            <code>
                identifier
            </code>
            that doesn't have a matching class or nib, it will return
            <code>
                nil
            </code>
            . When a
            <code>
                nil
            </code>
            is returned, the collection view uses its default inter-item gap indicator.
            When you need to use a custom indicator, you define a nib (as you did for
            the header) and pass its identifier instead of the empty string.
        </li>
        <li>
            When it is a header view, you set up its labels as before.
        </li>
    </ol>
    <div class="note">
        <em>
            Note
        </em>
        : There is a bug in the Swift API regarding the method above, and the
        <code>
            makeItemWithIdentifier
        </code>
        and
        <code>
            makeSupplementaryViewOfKind
        </code>
        methods. The return value specified is
        <code>
            NSView
        </code>
        , but these methods may return
        <code>
            nil
        </code>
        so the return value should be
        <code>
            NSView?
        </code>
        -- the question mark is part of the value.
    </div>
    <p>
        Build and run.
    </p>
    <p>
        Now you see an unmistakable aqua vertical line when you drag an item,
        indicating the drop target between the items. It's a sign that the collection
        view is ready to accept the drop.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/InterItemAnimation.gif">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/InterItemAnimation.gif"
            alt="InterItemAnimation" width="641" height="345" class="aligncenter size-full wp-image-132804">
        </a>
    </p>
    <p>
        Well…it's sort of ready. When you try to drop the item, it still bounces
        back because the delegate methods to handle the drop are not in place yet.
    </p>
    <p>
        Append the following method to
        <code>
            ImageDirectoryLoader
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                moveImageFromIndexPath
            </span>
            <span class="hljs-params">
                (indexPath: NSIndexPath, toIndexPath: NSIndexPath)
            </span>
        </span>
        {
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-keyword">
            let
        </span>
        itemBeingDragged = removeImageAtIndexPath(indexPath)
        <span class="hljs-keyword">
            let
        </span>
        destinationIsLower = indexPath.compare(toIndexPath) == .
        <span class="hljs-type">
            OrderedDescending
        </span>
        <span class="hljs-keyword">
            var
        </span>
        indexPathOfDestination:
        <span class="hljs-type">
            NSIndexPath
        </span>
        <span class="hljs-keyword">
            if
        </span>
        destinationIsLower { indexPathOfDestination = toIndexPath }
        <span class="hljs-keyword">
            else
        </span>
        { indexPathOfDestination =
        <span class="hljs-type">
            NSIndexPath
        </span>
        (forItem: toIndexPath.item-
        <span class="hljs-number">
            1
        </span>
        , inSection: toIndexPath.section) }
        <span class="hljs-comment">
            // 3
        </span>
        insertImage(itemBeingDragged, atIndexPath: indexPathOfDestination) }
    </pre>
    <p>
        Here's what's going on in there:
    </p>
    <ol>
        <li>
            Call this method to update the model when items are moved
        </li>
        <li>
            Remove the dragged item from the model
        </li>
        <li>
            Reinsert at its new position in the model
        </li>
    </ol>
    <p>
        Finish things off here by adding the following methods to the
        <code>
            NSCollectionViewDelegate
        </code>
        extension in
        <code>
            ViewController
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                collectionView
            </span>
            <span class="hljs-params">
                (collectionView: NSCollectionView, acceptDrop draggingInfo: NSDraggingInfo,
                indexPath: NSIndexPath, dropOperation: NSCollectionViewDropOperation)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            Bool
        </span>
        {
        <span class="hljs-keyword">
            if
        </span>
        indexPathsOfItemsBeingDragged !=
        <span class="hljs-literal">
            nil
        </span>
        {
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-keyword">
            let
        </span>
        indexPathOfFirstItemBeingDragged = indexPathsOfItemsBeingDragged.first!
        <span class="hljs-keyword">
            var
        </span>
        toIndexPath:
        <span class="hljs-type">
            NSIndexPath
        </span>
        <span class="hljs-keyword">
            if
        </span>
        indexPathOfFirstItemBeingDragged.compare(indexPath) == .
        <span class="hljs-type">
            OrderedAscending
        </span>
        { toIndexPath =
        <span class="hljs-type">
            NSIndexPath
        </span>
        (forItem: indexPath.item-
        <span class="hljs-number">
            1
        </span>
        , inSection: indexPath.section) }
        <span class="hljs-keyword">
            else
        </span>
        { toIndexPath =
        <span class="hljs-type">
            NSIndexPath
        </span>
        (forItem: indexPath.item, inSection: indexPath.section) }
        <span class="hljs-comment">
            // 3
        </span>
        imageDirectoryLoader.moveImageFromIndexPath(indexPathOfFirstItemBeingDragged,
        toIndexPath: toIndexPath)
        <span class="hljs-comment">
            // 4
        </span>
        collectionView.moveItemAtIndexPath(indexPathOfFirstItemBeingDragged, toIndexPath:
        toIndexPath) }
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-comment">
            // 5
        </span>
        <span class="hljs-keyword">
            var
        </span>
        droppedObjects =
        <span class="hljs-type">
            Array
        </span>
        &lt;
        <span class="hljs-type">
            NSURL
        </span>
        &gt;() draggingInfo.enumerateDraggingItemsWithOptions(
        <span class="hljs-type">
            NSDraggingItemEnumerationOptions
        </span>
        .
        <span class="hljs-type">
            Concurrent
        </span>
        , forView: collectionView, classes: [
        <span class="hljs-type">
            NSURL
        </span>
        .
        <span class="hljs-keyword">
            self
        </span>
        ], searchOptions: [
        <span class="hljs-type">
            NSPasteboardURLReadingFileURLsOnlyKey
        </span>
        :
        <span class="hljs-type">
            NSNumber
        </span>
        (bool:
        <span class="hljs-literal">
            true
        </span>
        )]) { (draggingItem, idx, stop)
        <span class="hljs-keyword">
            in
        </span>
        <span class="hljs-keyword">
            if
        </span>
        <span class="hljs-keyword">
            let
        </span>
        url = draggingItem.item
        <span class="hljs-keyword">
            as
        </span>
        ?
        <span class="hljs-type">
            NSURL
        </span>
        { droppedObjects.append(url) } }
        <span class="hljs-comment">
            // 6
        </span>
        insertAtIndexPathFromURLs(droppedObjects, atIndexPath: indexPath) }
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-literal">
            true
        </span>
        }
        <span class="hljs-comment">
            // 7
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                collectionView
            </span>
            <span class="hljs-params">
                (collectionView: NSCollectionView, draggingSession session: NSDraggingSession,
                endedAtPoint screenPoint: NSPoint, dragOperation operation: NSDragOperation)
            </span>
        </span>
        { indexPathsOfItemsBeingDragged =
        <span class="hljs-literal">
            nil
        </span>
        }
    </pre>
    <p>
        Here's what happens with these methods:
    </p>
    <ol>
        <li>
            This is invoked when the user releases the mouse to commit the drop operation.
        </li>
        <li>
            Then it falls here when it's a move operation.
        </li>
        <li>
            It updates the model.
        </li>
        <li>
            Then it notifies the collection view about the changes.
        </li>
        <li>
            It falls here to accept a drop from another app.
        </li>
        <li>
            Calls the same method in
            <code>
                ViewController
            </code>
            as
            <em>
                Add
            </em>
            with
            <em>
                URLs
            </em>
            obtained from the
            <code>
                NSDraggingInfo
            </code>
            .
        </li>
        <li>
            Invoked to conclude the drag session. Clears the value of
            <code>
                indexPathsOfItemsBeingDragged
            </code>
            .
        </li>
    </ol>
    <p>
        Build and run.
    </p>
    <p>
        Now it's possible to move a single item to a different location in the
        same section. Dragging one or more items from another app should work too.
    </p>
    <h3>
        Fix the UI
    </h3>
    <p>
        The current implementation of drag-and-drop in SlidesPro doesn't support
        drop across sections. Also, multi-selection is supported only for a drop
        outside SlidesPro. To disable in
        <em>
            UI
        </em>
        , these unsupported capabilities change the
        <code>
            else
        </code>
        part of the second
        <code>
            if
        </code>
        statement to:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                collectionView
            </span>
            <span class="hljs-params">
                (collectionView: NSCollectionView, validateDrop draggingInfo: NSDraggingInfo,
                proposedIndexPath proposedDropIndexPath: AutoreleasingUnsafeMutablePointer&lt;NSIndexPath?&gt;,
                dropOperation proposedDropOperation: UnsafeMutablePointer&lt;NSCollectionViewDropOperation&gt;)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            NSDragOperation
        </span>
        {
        <span class="hljs-keyword">
            if
        </span>
        proposedDropOperation.memory ==
        <span class="hljs-type">
            NSCollectionViewDropOperation
        </span>
        .
        <span class="hljs-type">
            On
        </span>
        { proposedDropOperation.memory =
        <span class="hljs-type">
            NSCollectionViewDropOperation
        </span>
        .
        <span class="hljs-type">
            Before
        </span>
        }
        <span class="hljs-keyword">
            if
        </span>
        indexPathsOfItemsBeingDragged ==
        <span class="hljs-literal">
            nil
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-type">
            NSDragOperation
        </span>
        .
        <span class="hljs-type">
            Copy
        </span>
        }
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            let
        </span>
        sectionOfItemBeingDragged = indexPathsOfItemsBeingDragged.first!.section
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-keyword">
            if
        </span>
        <span class="hljs-keyword">
            let
        </span>
        proposedDropsection = proposedDropIndexPath.memory?.section
        <span class="hljs-keyword">
            where
        </span>
        sectionOfItemBeingDragged == proposedDropsection &amp;&amp; indexPathsOfItemsBeingDragged.
        <span class="hljs-built_in">
            count
        </span>
        ==
        <span class="hljs-number">
            1
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-type">
            NSDragOperation
        </span>
        .
        <span class="hljs-type">
            Move
        </span>
        }
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-type">
            NSDragOperation
        </span>
        .
        <span class="hljs-type">
            None
        </span>
        } } }
    </pre>
    <ol>
        <li>
            The drop is enabled only when the source and target sections match and
            exactly one item is selected.
        </li>
        <li>
            Otherwise, it prevents the drop by returning
            <code>
                .None
            </code>
        </li>
    </ol>
    <p>
        Build and run. Try dragging an item from one section to another. The drop
        indicator does not present itself, meaning a drop is impossible.
    </p>
    <p>
        Now drag a multi-selection. While inside the bounds of the collection
        view there is no drop indicator; however, drag it to
        <em>
            Finder
        </em>
        , and you'll see that a drop is allowed.
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        If you tried to drag the selection outside the collection view, you might
        have noticed a highlight issue. You'll come back to this in the upcoming
        section, "More Fun With Selection and Highlighting".
    </div>
    <h2>
        More Fun With Selection and Highlighting
    </h2>
    <p>
        In the previous section, you noticed an issue with highlighting.
    </p>
    <p>
        For the sake of sanity in this discussion, the item being moved will be
        <em>
            Item-1
        </em>
        . After
        <em>
            Item-1
        </em>
        lands at a new position it stays highlighted, and the
        <em>
            Add
        </em>
        and
        <em>
            Remove
        </em>
        buttons are enabled, but the selection is empty.
    </p>
    <p>
        To confirm this is true, select any item --
        <em>
            Item-2
        </em>
        . It highlights as expected, but
        <em>
            Item-1
        </em>
        stays highlighted. It should have been deselected and the highlight removed
        when you selected
        <em>
            Item-2
        </em>
        .
    </p>
    <p>
        Click anywhere between the items to deselect everything.
        <em>
            Item-2's
        </em>
        highlight goes away, the
        <em>
            Add
        </em>
        and
        <em>
            Remove
        </em>
        buttons are disabled, as they should be for no selection, but
        <em>
            Item-1
        </em>
        is
        <i>
            still
        </i>
        highlighted.
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        The collection view tracks its selection in its
        <code>
            selectionIndexPaths
        </code>
        property. To debug, you can insert print statements to show the value
        of this property.
    </div>
    <p>
        So what's going wrong here?
    </p>
    <p>
        Apparently, the collection view successfully deselects
        <em>
            Item-1
        </em>
        , but the
        <code>
            collectionView(\_:didDeselectItemsAtIndexPaths: )
        </code>
        delegate method is not called to remove the highlight and disable the
        buttons.
    </p>
    <p>
        In
        <code>
            NSCollectionView.h
        </code>
        , the comments for the above method and its companion for the select action
        say, "Sent at the end of interactive selection…". Hence, these notifications
        are sent only when you select/deselect via UI.
    </p>
    <p>
        Here's your answer, Sherlock: The deselection behavior that should occur
        when you're moving an item is performed programmatically via the
        <code>
            deselectItemsAtIndexPaths(\_:)
        </code>
        method of
        <code>
            NSCollectionView
        </code>
        .
    </p>
    <p>
        You'll need to override this method.
    </p>
    <p>
        Go to
        <em>
            File \ New \ File…
        </em>
        and create a new
        <em>
            Cocoa Class
        </em>
        by the name
        <em>
            CollectionView
        </em>
        make it a subclass of
        <em>
            NSCollectionView
        </em>
        and put it in the
        <em>
            Views
        </em>
        group.
    </p>
    <p>
        The template may add a
        <code>
            drawRect(\_:)
        </code>
        -- make sure to delete it.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/EmptyCollectionView.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/EmptyCollectionView-700x442.png"
            alt="EmptyCollectionView" width="700" height="442" class="aligncenter size-large wp-image-132325"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/EmptyCollectionView-700x442.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/EmptyCollectionView-480x303.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/EmptyCollectionView-768x485.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/EmptyCollectionView.png 978w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Add the following method to
        <code>
            CollectionView
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            override
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                deselectItemsAtIndexPaths
            </span>
            <span class="hljs-params">
                (indexPaths: Set&lt;NSIndexPath&gt;)
            </span>
        </span>
        {
        <span class="hljs-keyword">
            super
        </span>
        .deselectItemsAtIndexPaths(indexPaths)
        <span class="hljs-keyword">
            let
        </span>
        viewController = delegate
        <span class="hljs-keyword">
            as
        </span>
        !
        <span class="hljs-type">
            ViewController
        </span>
        viewController.highlightItems(
        <span class="hljs-literal">
            false
        </span>
        , atIndexPaths: indexPaths) }
    </pre>
    <p>
        The method calls its super implementation followed by a call to
        <code>
            highlightItems(\_:atIndexPaths:)
        </code>
        of its delegate, allowing
        <code>
            ViewController
        </code>
        to highlight/unhighlight items and enable/disable buttons respectively.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and select the
        <em>
            Collection View
        </em>
        . In the
        <em>
            Identity Inspector
        </em>
        , change
        <em>
            Class
        </em>
        to
        <em>
            CollectionView
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/CollectionViewIB.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/CollectionViewIB-700x383.png"
            alt="CollectionViewIB" width="700" height="383" class="aligncenter size-large wp-image-132328"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/CollectionViewIB-700x383.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/CollectionViewIB-480x263.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/CollectionViewIB-768x421.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/CollectionViewIB.png 1057w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Build and run.
    </p>
    <p>
        Move an item inside the collection to a different location. Nothing shows
        as highlighted and buttons disable as expected. Case closed.
    </p>
    <h2>
        Animation in Collection Views
    </h2>
    <p>
        <code>
            NSCollectionView
        </code>
        , as a subclass of
        <code>
            NSView
        </code>
        , can perform animations via the animator proxy. It's as easy as adding
        a single word in your code before an operation such as removal of items.
    </p>
    <p>
        At the end of the
        <code>
            removeSlide(\_:)
        </code>
        method in
        <code>
            ViewController
        </code>
        , replace this:
    </p>
    <pre lang="swift" class="language-swift hljs">
        collectionView.deleteItemsAtIndexPaths(selectionIndexPaths)
    </pre>
    <p>
        With this:
    </p>
    <pre lang="swift" class="language-swift hljs">
        collectionView.animator().deleteItemsAtIndexPaths(selectionIndexPaths)
    </pre>
    <p>
        Build and run.
    </p>
    <p>
        Select several items and click the
        <em>
            Remove
        </em>
        button. Watch as the items glide to take up their new positions on the
        screen.
    </p>
    <p>
        The default duration is a quarter of a second. To experience a really
        cool and beautiful effect, add a setting for the duration of the animation
        at a higher value. Place it above the line you just added:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-type">
            NSAnimationContext
        </span>
        .currentContext().duration =
        <span class="hljs-number">
            1.0
        </span>
        collectionView.animator().deleteItemsAtIndexPaths(selectionIndexPaths)
    </pre>
    <p>
        Build and run, and then remove some items. Cool effect, isn't it?
    </p>
    <p>
        You can do the same for
        <code>
            insertItemsAtIndexPaths
        </code>
        when you're adding items, as well as for
        <code>
            moveItemAtIndexPath
        </code>
        when moving an item.
    </p>
    <h2>
        Sticky Headers
    </h2>
    <p>
        When you scroll a collection view with section headers, the first element
        of a given section that vanishes at the top of the screen is its header.
    </p>
    <p>
        In this section, you'll implement
        <em>
            Sticky Headers
        </em>
        , so the top-most section header will pin itself to the top of the collection
        view. It will hold its position until the next section header bumps it
        out of the way.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeadersScreen.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeadersScreen-700x500.png"
            alt="StickyHeadersScreen" width="700" height="500" class="aligncenter size-large wp-image-132329"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeadersScreen-700x500.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeadersScreen-448x320.png 448w, https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeadersScreen-768x549.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeadersScreen.png 956w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        To make this effect reality, you'll subclass
        <code>
            NSCollectionViewFlowLayout
        </code>
        .
    </p>
    <p>
        Go to
        <em>
            File \ New \ File…
        </em>
        and create a new
        <em>
            Cocoa Class
        </em>
        named
        <em>
            StickyHeadersLayout
        </em>
        as a subclass of
        <em>
            NSCollectionViewFlowLayout
        </em>
        , and put it in the
        <em>
            Layout
        </em>
        group.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeaderSkeleton.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeaderSkeleton-700x411.png"
            alt="StickyHeaderSkeleton" width="700" height="411" class="aligncenter size-large wp-image-132330"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeaderSkeleton-700x411.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeaderSkeleton-480x282.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeaderSkeleton-768x451.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeaderSkeleton.png 960w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        In
        <code>
            ViewController
        </code>
        , change the first line of
        <code>
            configureCollectionView()
        </code>
        to:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            let
        </span>
        flowLayout =
        <span class="hljs-type">
            StickyHeadersLayout
        </span>
        ()
    </pre>
    <p>
        Now implement sticky headers by adding the following method to the empty
        body of the
        <code>
            StickyHeadersLayout
        </code>
        class:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            override
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                layoutAttributesForElementsInRect
            </span>
            <span class="hljs-params">
                (rect: NSRect)
            </span>
        </span>
        -&gt; [
        <span class="hljs-type">
            NSCollectionViewLayoutAttributes
        </span>
        ] {
        <span class="hljs-comment">
            // 1
        </span>
        <span class="hljs-keyword">
            var
        </span>
        layoutAttributes =
        <span class="hljs-keyword">
            super
        </span>
        .layoutAttributesForElementsInRect(rect)
        <span class="hljs-comment">
            // 2
        </span>
        <span class="hljs-keyword">
            let
        </span>
        sectionsToMoveHeaders =
        <span class="hljs-type">
            NSMutableIndexSet
        </span>
        ()
        <span class="hljs-keyword">
            for
        </span>
        attributes
        <span class="hljs-keyword">
            in
        </span>
        layoutAttributes {
        <span class="hljs-keyword">
            if
        </span>
        attributes.representedElementCategory == .
        <span class="hljs-type">
            Item
        </span>
        { sectionsToMoveHeaders.addIndex(attributes.indexPath!.section) } }
        <span class="hljs-comment">
            // 3
        </span>
        <span class="hljs-keyword">
            for
        </span>
        attributes
        <span class="hljs-keyword">
            in
        </span>
        layoutAttributes {
        <span class="hljs-keyword">
            if
        </span>
        <span class="hljs-keyword">
            let
        </span>
        elementKind = attributes.representedElementKind
        <span class="hljs-keyword">
            where
        </span>
        elementKind ==
        <span class="hljs-type">
            NSCollectionElementKindSectionHeader
        </span>
        { sectionsToMoveHeaders.removeIndex(attributes.indexPath!.section) } }
        <span class="hljs-comment">
            // 4
        </span>
        sectionsToMoveHeaders.enumerateIndexesUsingBlock { (index, stop) -&gt;
        <span class="hljs-type">
            Void
        </span>
        <span class="hljs-keyword">
            in
        </span>
        <span class="hljs-keyword">
            let
        </span>
        indexPath =
        <span class="hljs-type">
            NSIndexPath
        </span>
        (forItem:
        <span class="hljs-number">
            0
        </span>
        , inSection: index)
        <span class="hljs-keyword">
            let
        </span>
        attributes =
        <span class="hljs-keyword">
            self
        </span>
        .layoutAttributesForSupplementaryViewOfKind(
        <span class="hljs-type">
            NSCollectionElementKindSectionHeader
        </span>
        , atIndexPath: indexPath)
        <span class="hljs-keyword">
            if
        </span>
        attributes !=
        <span class="hljs-literal">
            nil
        </span>
        { layoutAttributes.append(attributes!) } }
        <span class="hljs-keyword">
            for
        </span>
        attributes
        <span class="hljs-keyword">
            in
        </span>
        layoutAttributes {
        <span class="hljs-comment">
            // 5
        </span>
        <span class="hljs-keyword">
            if
        </span>
        <span class="hljs-keyword">
            let
        </span>
        elementKind = attributes.representedElementKind
        <span class="hljs-keyword">
            where
        </span>
        elementKind ==
        <span class="hljs-type">
            NSCollectionElementKindSectionHeader
        </span>
        {
        <span class="hljs-keyword">
            let
        </span>
        section = attributes.indexPath!.section
        <span class="hljs-keyword">
            let
        </span>
        attributesForFirstItemInSection = layoutAttributesForItemAtIndexPath(
        <span class="hljs-type">
            NSIndexPath
        </span>
        (forItem:
        <span class="hljs-number">
            0
        </span>
        , inSection: section))
        <span class="hljs-keyword">
            let
        </span>
        attributesForLastItemInSection = layoutAttributesForItemAtIndexPath(
        <span class="hljs-type">
            NSIndexPath
        </span>
        (forItem: collectionView!.numberOfItemsInSection(section) -
        <span class="hljs-number">
            1
        </span>
        , inSection: section))
        <span class="hljs-keyword">
            var
        </span>
        frame = attributes.frame
        <span class="hljs-comment">
            // 6
        </span>
        <span class="hljs-keyword">
            let
        </span>
        offset = collectionView!.enclosingScrollView?.documentVisibleRect.origin.y
        <span class="hljs-comment">
            // 7
        </span>
        <span class="hljs-keyword">
            let
        </span>
        minY =
        <span class="hljs-type">
            CGRectGetMinY
        </span>
        (attributesForFirstItemInSection!.frame) - frame.height
        <span class="hljs-comment">
            // 8
        </span>
        <span class="hljs-keyword">
            let
        </span>
        maxY =
        <span class="hljs-type">
            CGRectGetMaxY
        </span>
        (attributesForLastItemInSection!.frame) - frame.height
        <span class="hljs-comment">
            // 9
        </span>
        <span class="hljs-keyword">
            let
        </span>
        y =
        <span class="hljs-built_in">
            min
        </span>
        (
        <span class="hljs-built_in">
            max
        </span>
        (offset!, minY), maxY)
        <span class="hljs-comment">
            // 10
        </span>
        frame.origin.y = y attributes.frame = frame
        <span class="hljs-comment">
            // 11
        </span>
        attributes.zIndex =
        <span class="hljs-number">
            99
        </span>
        } }
        <span class="hljs-comment">
            // 12
        </span>
        <span class="hljs-keyword">
            return
        </span>
        layoutAttributes }
    </pre>
    <p>
        Okay, there's a lot happening in there, but it makes sense when you take
        it section by section:
    </p>
    <ol>
        <li>
            The super method returns an array of attributes for the visible elements.
        </li>
        <li>
            The
            <code>
                NSMutableIndexSet
            </code>
            first aggregates all the sections that have at least one visible item.
        </li>
        <li>
            Remove all sections from the set where the header is already in
            <code>
                layoutAttributes
            </code>
            , leaving only the sections with “Missing Headers” in the set.
        </li>
        <li>
            Request the attributes for the missing headers and add them to
            <code>
                layoutAttributes
            </code>
            .
        </li>
        <li>
            Iterate over
            <code>
                layoutAttributes
            </code>
            and process only the headers.
        </li>
        <li>
            Set the coordinate for the top of the visible area, aka scroll offset.
        </li>
        <li>
            Make it so the header never goes further up than one-header-height above
            the upper bounds of the first item in the section.
        </li>
        <li>
            Make it so the header never goes further down than one-header-height above
            the lower bounds of the last item in the section.
        </li>
        <li>
            Let's break this into 2 statements:
            <ol>
                <li>
                    <code>
                        maybeY = max(offset!, minY)
                    </code>
                    : When the top of the section is above the visible area this pins (or
                    pushes down) the header to the top of the visible area.
                </li>
                <li>
                    <code>
                        y = min(maybeY, maxY)
                    </code>
                    : When the space between the bottom of the section to the top of the visible
                    area is less than header height, it shows only the part of the header's
                    bottom that fits this space.
                </li>
            </ol>
        </li>
        <li>
            Update the vertical position of the header.
        </li>
        <li>
            Make the items "go" under the header.
        </li>
        <li>
            Return the updated attributes.
        </li>
    </ol>
    <p>
        Add the following method to
        <code>
            StickyHeadersLayout
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            override
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                shouldInvalidateLayoutForBoundsChange
            </span>
            <span class="hljs-params">
                (newBounds: CGRect)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            Bool
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-literal">
            true
        </span>
        }
    </pre>
    <p>
        You always return
        <code>
            true
        </code>
        because you want the to invalidate the layout as the user scrolls.
    </p>
    <p>
        Build and run.
    </p>
    <p>
        Scroll the collection to see your sticky headers in action.
    </p>
    <h2>
        Where To Go From Here
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
            SlidesPro
        </em>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesPro-Final.zip">
            here
        </a>
        .
    </p>
    <p>
        In this Advanced Collection Views in OS X Tutorial you covered a lot of
        ground! You took the collection view from a rudimentary app to one that
        features the kinds of bells and whistles any Mac user would expect.
    </p>
    <p>
        After all your hard work, you're able to add and remove items, reorder
        them, and troubleshoot and correct highlighting/selection issues. You took
        it to the next level by adding in animations and implemented sticky headers
        to give SlidesPro a very polished look.
    </p>
    <p>
        Most impressively, you now know how to build a functional, elegant collection
        view in OS X. Considering that the documentation for these is fairly limited,
        it's a great skill to have.
    </p>
    <p>
        Some of the topics that were not covered neither here nor in the basic
        tutorial are:
    </p>
    <ul>
        <li>
            Creating custom layouts by subclassing directly
            <code>
                NSCollectionViewLayout
            </code>
        </li>
        <li>
            “Data Source-less” collection views using
            <em>
                <a href="https://www.raywenderlich.com/124490/cocoa-bindings-os-x-tutorial">
                    Cocoa Bindings
                </a>
            </em>
        </li>
    </ul>
    <p>
        One of the top resources recommended at the end of the
        <a href="https://www.raywenderlich.com/120494/collection-views-os-x-tutorial"
        target="_blank">
            basic tutorial
        </a>
        is this excellent video tutorial series
        <a href="https://www.raywenderlich.com/video-tutorials#CCVL" target="_blank"
        title="Custom Collection View Layout">
            Custom Collection View Layout
        </a>
        from Mic Pringle. Although it's an iOS series, you can find lots of useful
        information that's relevant to collection views in OS X as well.
    </p>
    <p>
        I hope you found this tutorial most helpful! Let's talk about it in the
        forums. I look forward to your questions, comments and discoveries!
    </p>
</div>