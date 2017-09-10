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
        我让你进行了测试，但你会看到item并没有响应拖拽的事件。为什么会这样？很快你就会知道。
    </p>
    <p>
        第一个问题是，这里需要一些额外的逻辑来处理拖拽的动作，因此，在
        <code>
            ViewController
        </code>
        的
        <code>
            NSCollectionViewDelegate
        </code>
        extension中添加下列的方法：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-comment">// 1</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">collectionView</span><span class="hljs-params">(collectionView: NSCollectionView, canDragItemsAtIndexes indexes: NSIndexSet, withEvent event: NSEvent)</span></span> -&gt; <span class="hljs-type">Bool</span> {
    <span class="hljs-keyword">return</span> <span class="hljs-literal">true</span>
  }
  
  <span class="hljs-comment">// 2</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">collectionView</span><span class="hljs-params">(collectionView: NSCollectionView, pasteboardWriterForItemAtIndexPath indexPath: NSIndexPath)</span></span> -&gt; <span class="hljs-type">NSPasteboardWriting</span>? {
    <span class="hljs-keyword">let</span> imageFile = imageDirectoryLoader.imageFileForIndexPath(indexPath)
    <span class="hljs-keyword">return</span> imageFile.url.absoluteURL
  }
</pre>
    <p>
        上述代码：
    </p>
    <ol>
        <li>
            当collection view将开始一个拖拽操作时，就会发送这个消息给它的
            <code>
                delegate
            </code>
            。它的返回值代表了collection view是否指定index path的item允许被拖动。你需要能够拖动任意item，因此你就无条件地返回
            <code>
                true
            </code>
            。
        </li>
        <li>
            实现这个方法是非常关键的，因为这样collection view才可以成为一个
            <em>
                Drag Source
            </em>
            。如果在第一部分中的方法允许开始拖拽，collection view就会为每个item调用一次这个方法，来为item的底层模型对象请求一个pasteboard writer。这个方法就返回一个实现了
            <code>
                NSPasteboardWriting
            </code>
            的自定义对象；在这个case中就是
            <code>
                NSURL
            </code>
            。返回
            <code>
                nil
            </code>
            则会阻止拖拽。
        </li>
    </ol>
    <p>
        运行项目。
    </p>
    <p>
        尝试拖拽一个item，item移动了...哈利路亚!
    </p>
    <p>
        获取我说得太快了？当你尝试把item拖拽到collection view上一个不同的位置的时候，它却又弹回去了。Why？因为你还未将collection view设置为一个
        <em>
            Drop Target
        </em>
        。
    </p>
    <p>
        现在尝试把一个item拖拽到Finder中；你就会发现一个新的基于源
        <em>
            URL
        </em>
        的图片文件创建了出来。你
        <i>
            已经
        </i>
        取得了巨大的进展，因为从
        <em>
            SlidesPro
        </em>
        拖拽图片到另一个app上已经可以work了！
    </p>
    <h3>
        定义你的Drop Target
    </h3>
    <p>
        添加下列的property到
        <code>
            ViewController
        </code>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-keyword">var</span> indexPathsOfItemsBeingDragged: <span class="hljs-type">Set</span>&lt;<span class="hljs-type">NSIndexPath</span>&gt;!
</pre>
    <p>
        添加下列方法到
        <code>
            ViewController
        </code>
        的
        <code>
            NSCollectionViewDelegate
        </code>
        extension中：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-comment">// 1</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">collectionView</span><span class="hljs-params">(collectionView: NSCollectionView, draggingSession session: NSDraggingSession, willBeginAtPoint screenPoint: NSPoint, forItemsAtIndexPaths indexPaths: Set&lt;NSIndexPath&gt;)</span></span> {
    indexPathsOfItemsBeingDragged = indexPaths
  }

  <span class="hljs-comment">// 2</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">collectionView</span><span class="hljs-params">(collectionView: NSCollectionView, validateDrop draggingInfo: NSDraggingInfo, proposedIndexPath
    proposedDropIndexPath: AutoreleasingUnsafeMutablePointer&lt;NSIndexPath?&gt;, dropOperation proposedDropOperation: UnsafeMutablePointer&lt;NSCollectionViewDropOperation&gt;)</span></span> -&gt; <span class="hljs-type">NSDragOperation</span> {
    <span class="hljs-comment">// 3</span>
    <span class="hljs-keyword">if</span> proposedDropOperation.memory == <span class="hljs-type">NSCollectionViewDropOperation</span>.<span class="hljs-type">On</span> {
      proposedDropOperation.memory = <span class="hljs-type">NSCollectionViewDropOperation</span>.<span class="hljs-type">Before</span>
    }
    <span class="hljs-comment">// 4</span>
    <span class="hljs-keyword">if</span> indexPathsOfItemsBeingDragged == <span class="hljs-literal">nil</span> {
      <span class="hljs-keyword">return</span> <span class="hljs-type">NSDragOperation</span>.<span class="hljs-type">Copy</span>
    } <span class="hljs-keyword">else</span> {
        <span class="hljs-keyword">return</span> <span class="hljs-type">NSDragOperation</span>.<span class="hljs-type">Move</span>
    }
  }
</pre>
    <p>
        一步一步来看上述代码：
    </p>
    <ol>
        <li>
            当拖拽回话即将开始时，一个
            <code>
                optional
            </code>
            的方法就会被调用。你将使用跟这个方法来保存被拖拽的item。当这个property不为
            <code>
                nil
            </code>
            时，就表示
            <em>
                Drag Source
            </em>
            是这个collection view。
        </li>
        <li>
            实现放置的相关代理方法。这个方法会方法将要执行的操作的类型。
        </li>
        <li>
            在
            <em>
                SlidesPro
            </em>
            中，item并不能充当一个容器；因此只能在item之间进行拖拽，而不能把一个item放到另一个item上。
        </li>
        <li>
            当在collection view中移动item时，操作类型为
            <code>
                Move
            </code>
            。而当
            <em>
                Dragging Source
            </em>
            是另一个app的时候，操作类型就为
            <code>
                Copy
            </code>
            。
        </li>
    </ol>
    <p>
        运行项目。
    </p>
    <p>
        拖拽一个item。在你移动它之后，你就会看到一些带有文字的奇怪的灰色矩形。在你移动它经过其它item的时候，相同的矩形也出现在了item之间。
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
        神马情况？
    </p>
    <p>
        在
        <code>
            ViewController
        </code>
        中，找到这个
        <code>
            DataSource
        </code>
        方法，它会在collection view请求一个supplementary view时被调用：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">collectionView</span><span class="hljs-params">(collectionView: NSCollectionView, viewForSupplementaryElementOfKind kind: String, atIndexPath indexPath: NSIndexPath)</span></span> -&gt; <span class="hljs-type">NSView</span> {
    <span class="hljs-keyword">let</span> view = collectionView.makeSupplementaryViewOfKind(<span class="hljs-type">NSCollectionElementKindSectionHeader</span>, withIdentifier: <span class="hljs-string">"HeaderView"</span>, forIndexPath: indexPath) <span class="hljs-keyword">as</span>! <span class="hljs-type">HeaderView</span>
    view.sectionTitle.stringValue = <span class="hljs-string">"Section <span class="hljs-subst">\(indexPath.section)</span>"</span>
    <span class="hljs-keyword">let</span> numberOfItemsInSection = imageDirectoryLoader.numberOfItemsInSection(indexPath.section)
    view.imageCount.stringValue = <span class="hljs-string">"<span class="hljs-subst">\(numberOfItemsInSection)</span> image files"</span>
    <span class="hljs-keyword">return</span> view
  }
</pre>
    <p>
        当你开始拖拽一个item的时候，collection view的布局就会请求“过渡间隔指示器”的supplementary view。上述的
        <code>
            DataSource
        </code>
        方法无条件地假定这是一个对header view的请求。因此，就会返回header view作为“过渡间隔指示器”。
    </p>
    <p>
        这些东西对你来说都是没用的，因此，用下列代码来替换这个方法的内容：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">collectionView</span><span class="hljs-params">(collectionView: NSCollectionView, viewForSupplementaryElementOfKind kind: String, atIndexPath indexPath: NSIndexPath)</span></span> -&gt; <span class="hljs-type">NSView</span> {
    <span class="hljs-comment">// 1</span>
    <span class="hljs-keyword">let</span> identifier: <span class="hljs-type">String</span> = kind == <span class="hljs-type">NSCollectionElementKindSectionHeader</span> ? <span class="hljs-string">"HeaderView"</span> : <span class="hljs-string">""</span>
    <span class="hljs-keyword">let</span> view = collectionView.makeSupplementaryViewOfKind(kind, withIdentifier: identifier, forIndexPath: indexPath)
    <span class="hljs-comment">// 2</span>
    <span class="hljs-keyword">if</span> kind == <span class="hljs-type">NSCollectionElementKindSectionHeader</span> {
      <span class="hljs-keyword">let</span> headerView = view <span class="hljs-keyword">as</span>! <span class="hljs-type">HeaderView</span>
      headerView.sectionTitle.stringValue = <span class="hljs-string">"Section <span class="hljs-subst">\(indexPath.section)</span>"</span>
      <span class="hljs-keyword">let</span> numberOfItemsInSection = imageDirectoryLoader.numberOfItemsInSection(indexPath.section)
      headerView.imageCount.stringValue = <span class="hljs-string">"<span class="hljs-subst">\(numberOfItemsInSection)</span> image files"</span>
    }
    <span class="hljs-keyword">return</span> view
  }
</pre>
    <p>
        上述代码：
    </p>
    <ol>
        <li>
            你根据接受到的
            <code>
                kind
            </code>
            参数，设置了一个
            <code>
                identifier
            </code>
            。如果它不是header view的话，你就将
            <code>
                identifier
            </code>
            设置为一个空的
            <code>
                String
            </code>
            。当你传递给
            <code>
                makeSupplementaryViewOfKind
            </code>
            方法的
            <code>
                identifier
            </code>
            不能匹配任何的类或nib文件，它就会返回
            <code>
                nil
            </code>
            。当返回
            <code>
                nil
            </code>
            的时候，collection view就会使用默认的“过渡间隔指示器”。当你需要使用自定义一个指示器的时候，你就可以创建一个nib文件（就像你在header中做的一样），并将它的identifier传进来。
        </li>
        <li>
            当它是一个header view的时候，你就像之前一样设置它的label。
        </li>
    </ol>
    <div class="note">
        <em>
            注意
        </em>
        ：对于上述提到的方法，以及
        <code>
            makeItemWithIdentifier
        </code>
        和
        <code>
            makeSupplementaryViewOfKind
        </code>
        方法中，Swift的API中存在一个bug。它们的返回值被指定为
        <code>
            NSView
        </code>
        类型，但这些方法是有可能返回
        <code>
            nil
        </code>
        的。所以返回值应当是
        <code>
            NSView?
        </code>
        类型的吗 -- 问好也是这个值的一部分。
    </div>
    <p>
        运行项目。
    </p>
    <p>
        现在当你拖拽一个item的时候，你就会看到一个明显的竖线，表示item将会被放置到的位置。它是collection view已经准备好接收item的标志。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/InterItemAnimation.gif">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/InterItemAnimation.gif"
            alt="InterItemAnimation" width="641" height="345" class="aligncenter size-full wp-image-132804">
        </a>
    </p>
    <p>
        已经有那么几分意思了。但当你尝试把item放下的时候，它仍会弹回到原来的位置，因为处理接收item的方法还没有实现。
    </p>
    <p>
        为
        <code>
            ImageDirectoryLoader
        </code>
        添加下列方法：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-comment">// 1</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">moveImageFromIndexPath</span><span class="hljs-params">(indexPath: NSIndexPath, toIndexPath: NSIndexPath)</span></span> {
    <span class="hljs-comment">// 2</span>
    <span class="hljs-keyword">let</span> itemBeingDragged = removeImageAtIndexPath(indexPath)
    <span class="hljs-keyword">let</span> destinationIsLower = indexPath.compare(toIndexPath) == .<span class="hljs-type">OrderedDescending</span>
    <span class="hljs-keyword">var</span> indexPathOfDestination: <span class="hljs-type">NSIndexPath</span>
    <span class="hljs-keyword">if</span> destinationIsLower {
      indexPathOfDestination = toIndexPath
    } <span class="hljs-keyword">else</span> {
      indexPathOfDestination = <span class="hljs-type">NSIndexPath</span>(forItem: toIndexPath.item-<span class="hljs-number">1</span>, inSection: toIndexPath.section)
    }
    <span class="hljs-comment">// 3</span>
    insertImage(itemBeingDragged, atIndexPath: indexPathOfDestination)
  }
</pre>
    <p>
        上述的代码：
    </p>
    <ol>
        <li>
            当item被移动的时候，就会调用这个方法来更新model
        </li>
        <li>
            从model中移除被拖拽的item
        </li>
        <li>
            重新插入到model的新的位置上
        </li>
    </ol>
    <p>
        通过添加下列的方法到
        <code>
            ViewController
        </code>
        的
        <code>
            NSCollectionViewDelegate
        </code>
        extension中来把拖拽的过程收尾：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-comment">// 1</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">collectionView</span><span class="hljs-params">(collectionView: NSCollectionView, acceptDrop draggingInfo: NSDraggingInfo, indexPath: NSIndexPath, dropOperation: NSCollectionViewDropOperation)</span></span> -&gt; <span class="hljs-type">Bool</span> {
    <span class="hljs-keyword">if</span> indexPathsOfItemsBeingDragged != <span class="hljs-literal">nil</span> {
      <span class="hljs-comment">// 2</span>
      <span class="hljs-keyword">let</span> indexPathOfFirstItemBeingDragged = indexPathsOfItemsBeingDragged.first!
      <span class="hljs-keyword">var</span> toIndexPath: <span class="hljs-type">NSIndexPath</span>
      <span class="hljs-keyword">if</span> indexPathOfFirstItemBeingDragged.compare(indexPath) == .<span class="hljs-type">OrderedAscending</span> {
        toIndexPath = <span class="hljs-type">NSIndexPath</span>(forItem: indexPath.item-<span class="hljs-number">1</span>, inSection: indexPath.section)
      } <span class="hljs-keyword">else</span> {
        toIndexPath = <span class="hljs-type">NSIndexPath</span>(forItem: indexPath.item, inSection: indexPath.section)
      }
      <span class="hljs-comment">// 3</span>
      imageDirectoryLoader.moveImageFromIndexPath(indexPathOfFirstItemBeingDragged, toIndexPath: toIndexPath)
      <span class="hljs-comment">// 4</span>
      collectionView.moveItemAtIndexPath(indexPathOfFirstItemBeingDragged, toIndexPath: toIndexPath)
    } <span class="hljs-keyword">else</span> {
      <span class="hljs-comment">// 5</span>
      <span class="hljs-keyword">var</span> droppedObjects = <span class="hljs-type">Array</span>&lt;<span class="hljs-type">NSURL</span>&gt;()
      draggingInfo.enumerateDraggingItemsWithOptions(<span class="hljs-type">NSDraggingItemEnumerationOptions</span>.<span class="hljs-type">Concurrent</span>, forView: collectionView, classes: [<span class="hljs-type">NSURL</span>.<span class="hljs-keyword">self</span>], searchOptions: [<span class="hljs-type">NSPasteboardURLReadingFileURLsOnlyKey</span> : <span class="hljs-type">NSNumber</span>(bool: <span class="hljs-literal">true</span>)]) { (draggingItem, idx, stop) <span class="hljs-keyword">in</span>
        <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> url = draggingItem.item <span class="hljs-keyword">as</span>? <span class="hljs-type">NSURL</span> {
          droppedObjects.append(url)
        }
      }
      <span class="hljs-comment">// 6</span>
      insertAtIndexPathFromURLs(droppedObjects, atIndexPath: indexPath)
    }
    <span class="hljs-keyword">return</span> <span class="hljs-literal">true</span>
  }
  
  <span class="hljs-comment">// 7</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">collectionView</span><span class="hljs-params">(collectionView: NSCollectionView, draggingSession session: NSDraggingSession, endedAtPoint screenPoint: NSPoint, dragOperation operation: NSDragOperation)</span></span> {
    indexPathsOfItemsBeingDragged = <span class="hljs-literal">nil</span>
  }
</pre>
    <p>
        上述的代码：
    </p>
    <ol>
        <li>
            他会在用户释放鼠标来完成拖拽操作时被调用。
        </li>
        <li>
            当它是一个移动的操作的时候，代码就会执行到此处。
        </li>
        <li>
            更新model
        </li>
        <li>
            将数据的变化通知给collection view。
        </li>
        <li>
            当从其它的app接收到拖拽的东西时，代码则会执行到此处。
        </li>
        <li>
            用从
            <code>
                NSDraggingInfo
            </code>
            中获取的
            <em>
                URLs
            </em>
            ，去调用
            <code>
                ViewController
            </code>
            中的
            <em>
                Add
            </em>
            方法。
        </li>
        <li>
            调用结论性的方法。清除
            <code>
                indexPathsOfItemsBeingDragged
            </code>
            的值。
        </li>
    </ol>
    <p>
        运行项目。
    </p>
    <p>
        现在你就可以将单个的item移动到同一section上不同的位置上了。同时也可以从另一个app拖拽一个或多个item到这里了。
    </p>
    <h3>
        修复UI
    </h3>
    <p>
        现在SlidesPro还不能支持在不同section之间进行拖拽移动。并且一次接收多个对象，也必须得从SlidesPro外的app拖来才行。要在
        <em>
            UI
        </em>
        中禁用这些不支持的特性，可将第二个
        <code>
            if
        </code>
        语句中的
        <code>
            else
        </code>
        部分改为：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">collectionView</span><span class="hljs-params">(collectionView: NSCollectionView, validateDrop draggingInfo: NSDraggingInfo, proposedIndexPath
    proposedDropIndexPath: AutoreleasingUnsafeMutablePointer&lt;NSIndexPath?&gt;, dropOperation proposedDropOperation: UnsafeMutablePointer&lt;NSCollectionViewDropOperation&gt;)</span></span> -&gt; <span class="hljs-type">NSDragOperation</span> {
    <span class="hljs-keyword">if</span> proposedDropOperation.memory == <span class="hljs-type">NSCollectionViewDropOperation</span>.<span class="hljs-type">On</span> {
      proposedDropOperation.memory = <span class="hljs-type">NSCollectionViewDropOperation</span>.<span class="hljs-type">Before</span>
    }
    <span class="hljs-keyword">if</span> indexPathsOfItemsBeingDragged == <span class="hljs-literal">nil</span> {
      <span class="hljs-keyword">return</span> <span class="hljs-type">NSDragOperation</span>.<span class="hljs-type">Copy</span>
    } <span class="hljs-keyword">else</span> {
      <span class="hljs-keyword">let</span> sectionOfItemBeingDragged = indexPathsOfItemsBeingDragged.first!.section
      <span class="hljs-comment">// 1</span>
      <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> proposedDropsection = proposedDropIndexPath.memory?.section <span class="hljs-keyword">where</span> sectionOfItemBeingDragged == proposedDropsection &amp;&amp; indexPathsOfItemsBeingDragged.<span class="hljs-built_in">count</span> == <span class="hljs-number">1</span> {
        <span class="hljs-keyword">return</span> <span class="hljs-type">NSDragOperation</span>.<span class="hljs-type">Move</span>
      } <span class="hljs-keyword">else</span> {
        <span class="hljs-comment">// 2</span>
        <span class="hljs-keyword">return</span> <span class="hljs-type">NSDragOperation</span>.<span class="hljs-type">None</span>
      }
    }
  }
</pre>
    <ol>
        <li>
            这个拖拽只能在源头和目标匹配，且只有一个item被选中时才可以执行。
        </li>
        <li>
            否则，就通过返回
            <code>
                .None
            </code>
            来阻止拖拽动作的完成。
        </li>
    </ol>
    <p>
        运行项目。尝试将item拖拽到另一个section中。指示器现在不会再展示出来了，代表这个拖拽动作是不可行的。
    </p>
    <p>
        现在，拖拽多个选中的item。当拖拽到collection view的范围中时，并不会展示允许放置的指示；然而，将它拖拽到
        <em>
            Finder
        </em>
        中时，你会发现这种是允许的。
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        如果把选中的item拖拽到collection view之外，你会发现一个高亮问题。请看下一部分“关于选择和高亮的更多内容”。
    </div>
    <h2>
        关于选择和高亮的更多内容
    </h2>
    <p>
        在上一部分，你会注意到一个关于高亮的问题。
    </p>
    <p>
        为了便于清楚地进行讨论，被移动的这个item将被称作
        <em>
            Item-1
        </em>
        。在
        <em>
            Item-1
        </em>
        被放置到一个新的位置后，它仍会保持高亮，
        <em>
            Add
        </em>
        和
        <em>
            Remove
        </em>
        按钮此时都是可用的，但选择现在却是空的。
    </p>
    <p>
        为了确认这点是真实的，选择任一item -- 我们将其称作
        <em>
            Item-2
        </em>
        。如同设想中的一样，它变为高亮的，但
        <em>
            Item-1
        </em>
        仍保持着高亮。它本来应该是在
        <em>
            Item-2
        </em>
        被选择时，被取消选择和高亮的效果的。
    </p>
    <p>
        点击item之间的任意位置以取消选择全部的item。
        <em>
            Item-2
        </em>
        的高亮效果消失了，
        <em>
            Add
        </em>
        和
        <em>
            Remove
        </em>
        按钮也被禁用了，现在应当是没有任何的选择了，但
        <em>
            Item-1
        </em>
        却
        <i>
            仍然
        </i>
        是高亮的。
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        collection view会同步选择到
        <code>
            selectionIndexPaths
        </code>
        这个property上。在debug的时候，你就可以打印它的值。
    </div>
    <p>
        所以到底是哪里出问题了？
    </p>
    <p>
        显然，collection view成功地取消选择了
        <em>
            Item-1
        </em>
        ，但
        <code>
            collectionView(\_:didDeselectItemsAtIndexPaths: )
        </code>
        这个代理方法却未被调用，以将高亮的效果移除掉并禁用按钮。
    </p>
    <p>
        在
        <code>
            NSCollectionView.h
        </code>
        中，collectionView(\_:didDeselectItemsAtIndexPaths: )上面的注释中描述到，“在交互式选择后调用...”。因此，这些通知仅仅会在你通过UI选择或取消选择item时，才会调用这个方法。
    </p>
    <p>
        这就是你的答案了，“夏洛克”：这个当你移动一个item时发生的取消选择的行为，是因为程序性地执行
        <code>
            NSCollectionView
        </code>
        的方法
        <code>
            deselectItemsAtIndexPaths(\_:)
        </code>
        而触发的。
    </p>
    <p>
        你需要重写这个方法。
    </p>
    <p>
        依次点击
        <em>
            File \ New \ File…
        </em>
        创建一个新的名为
        <em>
            CollectionView
        </em>
        的
        <em>
            Cocoa类
        </em>
        ，它是
        <em>
            NSCollectionView
        </em>
        的子类，并将它放到
        <em>
            Views
        </em>
        这组中。
    </p>
    <p>
        默认可能会添加一个
        <code>
            drawRect(\_:)
        </code>
        方法 -- 将其删除掉。
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
        添加下列的方法到
        <code>
            CollectionView
        </code>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-keyword">override</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">deselectItemsAtIndexPaths</span><span class="hljs-params">(indexPaths: Set&lt;NSIndexPath&gt;)</span></span> {
    <span class="hljs-keyword">super</span>.deselectItemsAtIndexPaths(indexPaths)
    <span class="hljs-keyword">let</span> viewController = delegate <span class="hljs-keyword">as</span>! <span class="hljs-type">ViewController</span>
    viewController.highlightItems(<span class="hljs-literal">false</span>, atIndexPaths: indexPaths)
  }
</pre>
    <p>
        这个方法首先会调用其父类的实现，然后在调用它的delegate的
        <code>
            highlightItems(\_:atIndexPaths:)
        </code>
        方法，并相应地让
        <code>
            ViewController
        </code>
        高亮/取消高亮item，打开使用/禁用按钮。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        并选择
        <em>
            Collection View
        </em>
        。在
        <em>
            Identity Inspector
        </em>
        中，将
        <em>
            Class
        </em>
        改为
        <em>
            CollectionView
        </em>
        。
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
        运行项目。
    </p>
    <p>
        在collection中将一个item移动到一个不同的位置上。现在没有高亮的项目出现了，按钮也如同期望的一样被禁用了。问题解决。
    </p>
    <h2>
        Collection View中的动画
    </h2>
    <p>
        <code>
            NSCollectionView
        </code>
        ，作为
        <code>
            NSView
        </code>
        的子类，可以通用动画代理来执行动画。在诸如移除item的操作之前，它就和你在代码中添加一个单词一样的容易。
    </p>
    <p>
        在
        <code>
            ViewController
        </code>
        中，
        <code>
            removeSlide(\_:)
        </code>
        方法的尾部，将代码：
    </p>
    <pre lang="swift" class="language-swift hljs">    collectionView.deleteItemsAtIndexPaths(selectionIndexPaths)
</pre>
    <p>
        替换为：
    </p>
    <pre lang="swift" class="language-swift hljs">    collectionView.animator().deleteItemsAtIndexPaths(selectionIndexPaths)
</pre>
    <p>
        运行项目
    </p>
    <p>
        选择几个item并点击
        <em>
            Remove
        </em>
        按钮。你会看到item在屏幕中滑动到了新的位置。
    </p>
    <p>
        动画默认的持续时间是四分之一秒。如果想要体验一个更酷的效果，可以把动画的持续时间替换为一个更高的值。把你上面刚刚添加的这行代码替换为：
    </p>
    <pre lang="swift" class="language-swift hljs">    <span class="hljs-type">NSAnimationContext</span>.currentContext().duration = <span class="hljs-number">1.0</span>
    collectionView.animator().deleteItemsAtIndexPaths(selectionIndexPaths)
</pre>
    <p>
        运行项目，移除一些项目。效果赞不？
    </p>
    <p>
        你可以在添加item时，为
        <code>
            insertItemsAtIndexPaths
        </code>
        做相同的事，同理也适用于使用
        <code>
            moveItemAtIndexPath
        </code>
        方法移动item时的情况。
    </p>
    <h2>
        黏性Headers
    </h2>
    <p>
        当你使用section header滚动collection view时，这个section在屏幕顶部消失的第一个元素会是header。
    </p>
    <p>
        在这一部分，你将实现
        <em>
            黏性的Headers
        </em>
        ，section顶部的header将把自己固定在collection view的顶部。它会将自己的位置保持到下一个section的header把它顶出去为止。
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
        为了让效果显得更加真实，你将撰写一个
        <code>
            NSCollectionViewFlowLayout
        </code>
        的子类。
    </p>
    <p>
        依次点击
        <em>
            File \ New \ File…
        </em>
        ，并创建一个新的名为
        <em>
            StickyHeadersLayout
        </em>
        的
        <em>
            Cocoa类
        </em>
        ，它是
        <em>
            NSCollectionViewFlowLayout
        </em>
        的子类，并将它放到
        <em>
            Layout
        </em>
        组中。
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
        在
        <code>
            ViewController
        </code>
        中，将
        <code>
            configureCollectionView()
        </code>
        的第一行改为：
    </p>
    <pre lang="swift" class="language-swift hljs">    <span class="hljs-keyword">let</span> flowLayout = <span class="hljs-type">StickyHeadersLayout</span>()
</pre>
    <p>
        现在通过添加下列的方法到
        <code>
            StickyHeadersLayout
        </code>
        内来实现黏性headers：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-keyword">override</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">layoutAttributesForElementsInRect</span><span class="hljs-params">(rect: NSRect)</span></span> -&gt; [<span class="hljs-type">NSCollectionViewLayoutAttributes</span>] {
    <span class="hljs-comment">// 1</span>
    <span class="hljs-keyword">var</span> layoutAttributes = <span class="hljs-keyword">super</span>.layoutAttributesForElementsInRect(rect)
    <span class="hljs-comment">// 2</span>
    <span class="hljs-keyword">let</span> sectionsToMoveHeaders = <span class="hljs-type">NSMutableIndexSet</span>()
    <span class="hljs-keyword">for</span> attributes <span class="hljs-keyword">in</span> layoutAttributes {
      <span class="hljs-keyword">if</span> attributes.representedElementCategory == .<span class="hljs-type">Item</span> {
        sectionsToMoveHeaders.addIndex(attributes.indexPath!.section)
      }
    }
    <span class="hljs-comment">// 3</span>
    <span class="hljs-keyword">for</span> attributes <span class="hljs-keyword">in</span> layoutAttributes {
      <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> elementKind = attributes.representedElementKind <span class="hljs-keyword">where</span> elementKind == <span class="hljs-type">NSCollectionElementKindSectionHeader</span> {
        sectionsToMoveHeaders.removeIndex(attributes.indexPath!.section)
      }
    }
    <span class="hljs-comment">// 4</span>
    sectionsToMoveHeaders.enumerateIndexesUsingBlock { (index, stop) -&gt; <span class="hljs-type">Void</span> <span class="hljs-keyword">in</span>
      <span class="hljs-keyword">let</span> indexPath = <span class="hljs-type">NSIndexPath</span>(forItem: <span class="hljs-number">0</span>, inSection: index)
      <span class="hljs-keyword">let</span> attributes = <span class="hljs-keyword">self</span>.layoutAttributesForSupplementaryViewOfKind(<span class="hljs-type">NSCollectionElementKindSectionHeader</span>, atIndexPath: indexPath)
      <span class="hljs-keyword">if</span> attributes != <span class="hljs-literal">nil</span> {
        layoutAttributes.append(attributes!)
      }
    }
    <span class="hljs-keyword">for</span> attributes <span class="hljs-keyword">in</span> layoutAttributes {
      <span class="hljs-comment">// 5</span>
      <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> elementKind = attributes.representedElementKind <span class="hljs-keyword">where</span> elementKind == <span class="hljs-type">NSCollectionElementKindSectionHeader</span> {
        <span class="hljs-keyword">let</span> section = attributes.indexPath!.section
        <span class="hljs-keyword">let</span> attributesForFirstItemInSection = layoutAttributesForItemAtIndexPath(<span class="hljs-type">NSIndexPath</span>(forItem: <span class="hljs-number">0</span>, inSection: section))
        <span class="hljs-keyword">let</span> attributesForLastItemInSection = layoutAttributesForItemAtIndexPath(<span class="hljs-type">NSIndexPath</span>(forItem: collectionView!.numberOfItemsInSection(section) - <span class="hljs-number">1</span>, inSection: section))
        <span class="hljs-keyword">var</span> frame = attributes.frame
        <span class="hljs-comment">// 6</span>
        <span class="hljs-keyword">let</span> offset = collectionView!.enclosingScrollView?.documentVisibleRect.origin.y
        <span class="hljs-comment">// 7</span>
        <span class="hljs-keyword">let</span> minY = <span class="hljs-type">CGRectGetMinY</span>(attributesForFirstItemInSection!.frame) - frame.height
        <span class="hljs-comment">// 8</span>
        <span class="hljs-keyword">let</span> maxY = <span class="hljs-type">CGRectGetMaxY</span>(attributesForLastItemInSection!.frame) - frame.height
        <span class="hljs-comment">// 9</span>
        <span class="hljs-keyword">let</span> y = <span class="hljs-built_in">min</span>(<span class="hljs-built_in">max</span>(offset!, minY), maxY)
        <span class="hljs-comment">// 10</span>
        frame.origin.y = y
        attributes.frame = frame
        <span class="hljs-comment">// 11</span>
        attributes.zIndex = <span class="hljs-number">99</span>
      }
    }
    <span class="hljs-comment">// 12</span>
    <span class="hljs-keyword">return</span> layoutAttributes
  }
</pre>
    <p>
        ok，发生了好多的事，我们一部分一部分来看：
    </p>
    <ol>
        <li>
            父类方法返回了一个可见元素的属性的数组。
        </li>
        <li>
            这个
            <code>
                NSMutableIndexSet
            </code>
            对象首先会收集所有的至少含有一个可见的item的section。
        </li>
        <li>
            从这个set中，移除所有header早已在
            <code>
                layoutAttributes
            </code>
            中的section，只留下“缺少Header”的section。
        </li>
        <li>
            获取缺少header的section的attribute，并添加到
            <code>
                layoutAttributes
            </code>
            中。
        </li>
        <li>
            便利
            <code>
                layoutAttributes
            </code>
            但只处理headers。
        </li>
        <li>
            设置可见区域顶部的坐标，也就是说滚动的偏移。
        </li>
        <li>
            这么做，让header从不超过所属section中的第一个item上边界一个header的高度。
        </li>
        <li>
            这么做，则让header从不超过所属section中的最后一个item下边界一个header的高度。
        </li>
        <li>
            可将这里拆分为两步：
            <ol>
                <li>
                    <code>
                        maybeY = max(offset!, minY)
                    </code>
                    ：当这个section的顶部位于可见区域的上方时，就会将header固定到可见区域的顶部。
                </li>
                <li>
                    <code>
                        y = min(maybeY, maxY)
                    </code>
                    ：当从section底部到可见区域顶部的距离，小于header的高度的时候，它就只展示header底部的一部分，以适应这部分空间。
                </li>
            </ol>
        </li>
        <li>
            更新header的垂直位置。
        </li>
        <li>
            把item放置到header的下面。
        </li>
        <li>
            返回更新后的attributes.
        </li>
    </ol>
    <p>
        添加下列的方法到
        <code>
            StickyHeadersLayout
        </code>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-keyword">override</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">shouldInvalidateLayoutForBoundsChange</span><span class="hljs-params">(newBounds: CGRect)</span></span> -&gt; <span class="hljs-type">Bool</span> {
    <span class="hljs-keyword">return</span> <span class="hljs-literal">true</span>
  }
</pre>
    <p>
        你将总是返回
        <code>
            true
        </code>
        ，因为你想要在用户滚动collection view时清除原先的布局。
    </p>
    <p>
        运行项目。
    </p>
    <p>
        滚动collection以观察黏性header实际的效果。
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
        可以从
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesPro-Final.zip">
            这里
        </a>
        下载
        <em>
            SlidesPro
        </em>
        的最终版本。
    </p>
    <p>
        在这篇OS X的高级Collection View教程中，你已经学习了很多的内容！你已把它从一个最基本的app，发展成了任何Mac用户所期望的，包含各种铃声和口哨等各种特性的app。
    </p>
    <p>
        在所有的辛勤工作之后，你已经可以添加和删除item，重新排序它们，排查错误以及纠正高亮/选择的问题。并且通过添加动画和实现黏性header给SlidesPro以一个优雅的外表，将它提升到了下一等级。
    </p>
    <p>
        留下最深印象的是，你现在已经知道了如何在OS X中构建一个功能丰富，优雅的collection view。考虑到关于它的文档相当地有限，这是一个非常值得去拥有的技能。
    </p>
    <p>
        在本教程中尚未覆盖到的主题还有：
    </p>
    <ul>
        <li>
            通过直接继承
            <code>
                NSCollectionViewLayout
            </code>
            来创建自定义的布局
        </li>
        <li>
            使用
            <em>
                <a href="https://www.raywenderlich.com/124490/cocoa-bindings-os-x-tutorial">
                    Cocoa Bindings
                </a>
            </em>
            的“无Data Source”的collection views
        </li>
    </ul>
    <p>
        在这篇
        <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/OS%20X%20View%20Controllers%20Tutorial.md"
        target="_blank">
            基本教程
        </a>
        的最后，推荐的一个资源，是来自Mic Pringle的优秀的视频教程系列
        <a href="https://www.raywenderlich.com/video-tutorials#CCVL" target="_blank"
        title="Custom Collection View Layout">
            Custom Collection View Layout
        </a>
        。尽管它是一个iOS系列的教程，你可以找到很多用到有用的信息，也可以用到OS X的collection view上。
    </p>
</div>