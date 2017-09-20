# 把你的iOS app接入到macOS上去

#### [原文地址](https://www.raywenderlich.com/161968/porting-your-ios-app-to-macos) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/PortOS-feature.png"
        alt="Porting Your iOS App to macOS" width="250" height="250" class="alignright size-thumbnail bordered">
    </p>
    <p>
        如果你是一个iOS的开发者，事实上你早已有了相当一部分的为另一个平台 - macOS开发app的能力！
    </p>
    <p>
        如果你和大多数的开发者一样，不想仅仅为了把你的app迁移到一个新的平台，就把它重写一遍，因为这会浪费太多的时间和金钱。只需一点小小的努力，你就可以学到如何把你的iOS app接入到macOS上，复用你已存在的iOS app中的大部分内容，仅需把平台特定的那一部分重写就可以了。
    </p>
    <p>
        在本教程中，你会学到如何创建一个同时支持iOS和macOS的项目，如何在两个平台上复用你的代码，以及什么时候适合去写平台指定的代码。
    </p>
    <p>
        要搞懂本教程中的主要内容，你需要熟悉
        To get the most out of this tutorial you should be familiar with
        <em>
            NSTableView
        </em>
        。如果你需要的话，我们有一个很不错的
        <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/macOS%20NSTableView%20Tutorial.md"
        sl-processed="1">
            介绍
        </a>
        可以帮助你来学习。
    </p>
    <h2>
        入门
    </h2>
    <p>
        为学习本教程，你需要从
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/BeerTracker-Port_Starter-1.zip"
        sl-processed="1">
            这里
        </a>
        下载初始项目。
    </p>
    <p>
        这个样本工程就是在之前教程中用到的BeerTracker app。你可以用它来你尝试过的啤酒，以及啤酒的说明，评分和图片。运行项目，来熟悉一下它的工作方式。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-iOS-Initial-282x500.png"
        alt="Beer Tracker iOS" width="282" height="500" class="aligncenter size-large wp-image-162149 bordered"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-iOS-Initial-282x500.png 282w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-iOS-Initial-180x320.png 180w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-iOS-Initial.png 640w"
        sizes="(max-width: 282px) 100vw, 282px">
    </p>
    <p>
        由于这个app目前只是在iOS上可用，因此要把这个app迁移到macOS上，第一件事就是创建一个新的target。target简单来说，就是一组告诉Xcode如何来构建app的指令集。当前，你只有一个iOS的target，它就包含了所有为iPhone构建你的app所需的信息。
    </p>
    <p>
        在顶部的
        <em>
            Project Navigator
        </em>
        中选择
        <em>
            BeerTracker
        </em>
        。在
        <em>
            Project and Targets
        </em>
        列表的底部，点击
        <em>
            +
        </em>
        按钮。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/AddingMacTarget.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/AddingMacTarget-345x320.png"
            alt="" width="345" height="320" class="aligncenter size-medium wp-image-164311"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/AddingMacTarget-345x320.png 345w, https://koenig-media.raywenderlich.com/uploads/2017/06/AddingMacTarget.png 441w"
            sizes="(max-width: 345px) 100vw, 345px">
        </a>
    </p>
    <p>
        这时会弹出一个窗口，让你为项目创建一个新的target。在窗口的顶部，你会看到表示所支持的不同的平台的tab。选择macOS，然后向下滚动到
        <em>
            Application
        </em>
        这里并选择
        <em>
            Cocoa App
        </em>
        。将新的target命名为
        <em>
            BeerTracker-mac
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/TargetSelection.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/TargetSelection-444x320.png"
            alt="" width="444" height="320" class="aligncenter size-medium wp-image-164312"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/TargetSelection-444x320.png 444w, https://koenig-media.raywenderlich.com/uploads/2017/06/TargetSelection-650x469.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/06/TargetSelection.png 731w"
            sizes="(max-width: 444px) 100vw, 444px">
        </a>
    </p>
    <h3>
        添加Assets
    </h3>
    <p>
        在你刚下载的起始项目中，你会发现一个名为
        <em>
            BeerTracker Mac Icons
        </em>
        的目录。你需要将其中的App Icon添加到
        <em>
            BeerTracker-mac
        </em>
        组中的
        <em>
            Assets.xcassets
        </em>
        的
        <em>
            AppIcon
        </em>
        中。并将
        <em>
            beerMug.pdf
        </em>
        也添加到
        <em>
            Assets.xcassets
        </em>
        中。选择
        <em>
            beerMug
        </em>
        ，打开
        <em>
            Attributes Inspector
        </em>
        并将
        <em>
            Scales
        </em>
        改为
        <em>
            Single Scale
        </em>
        。这样就确保了你不需要为这个asset使用不同scale的图。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/ScaleSelection.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/ScaleSelection.png"
            alt="" width="257" height="318" class="aligncenter size-full wp-image-164313">
        </a>
    </p>
    <p>
        当你完成之后，你的asset看起来应该是下面这个样子：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker_mac-assets-650x360.png"
        alt="Assets for Mac" width="650" height="360" class="aligncenter size-large wp-image-162153 bordered"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker_mac-assets-650x360.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker_mac-assets-480x266.png 480w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        在
        <em>
            Xcode
        </em>
        窗口顶部的左侧，在scheme的弹出窗口中选择
        <em>
            BeerTracker-mac
        </em>
        scheme。运行项目，你会看到一个空空的窗口。在你添加UI之前，你需要确保你的代码在iOS的框架
        <em>
            UIKit
        </em>
        和macOS的框架
        <em>
            AppKit
        </em>
        之间没有任何的冲突。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-Initial.png"
        alt="Mac starting window" width="592" height="404" class="aligncenter size-full wp-image-162150"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-Initial.png 592w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-Initial-469x320.png 469w"
        sizes="(max-width: 592px) 100vw, 592px">
    </p>
    <h2>
        能力的分离
    </h2>
    <p>
        <em>
            Foundation
        </em>
        框架让你的app可以共享大量的代码，因为它对于两个平台是通用的。然而，你的UI无法是通用的。事实上，由于你的第二个平台将会呈现你初始app的UI，苹果建议多平台的app不要去分享UI代码。
    </p>
    <p>
        iOS有着相当严格的
        <em>
            人机交互指南
        </em>
        以确保你的用户能够在他的触摸屏幕设备上读取和选择元素。然而，macOS上有着不同的要求。笔记本和台式机都有一个鼠标指针来点击和选择，这就使得屏幕上的元素可以比在手机上的更小。
    </p>
    <p>
        确定了UI在两个平台上无法相同之后，理解你代码中其它哪些部分可以被复用，哪些需要重写就变得非常重要。记住，在大多数的情况下，并没有绝对正确或错误的答案，应当确定的是怎样的工作方式才对你的app最好。永远记得被共享的代码越多，需要测试和debug的代码就越少。
    </p>
    <p>
        通常情况下，你可以共享model和 model controller。打开
        <em>
            Beer.swift
        </em>
        ，并在
        <em>
            Xcode
        </em>
        中打开
        <em>
            Utilities
        </em>
        抽屉，并选择
        <em>
            File Inspector
        </em>
        。由于两个target都会使用这个model，因此在
        <em>
            Target Membership
        </em>
        下，勾选
        <em>
            BeerTracker-mac
        </em>
        且
        <em>
            BeerTracker
        </em>
        仍然保持勾选。为
        <em>
            BeerManager.swift
        </em>
        和
        <em>
            Utilities
        </em>
        组下的
        <em>
            Utilities
        </em>
        执行同样的操作。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/TargetMembership.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/TargetMembership-245x320.png"
            alt="" width="245" height="320" class="aligncenter size-medium wp-image-164314"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/TargetMembership-245x320.png 245w, https://koenig-media.raywenderlich.com/uploads/2017/06/TargetMembership.png 260w"
            sizes="(max-width: 245px) 100vw, 245px">
        </a>
    </p>
    <p>
        如果你运行项目，你就会得到一个编译错误。这是因为
        <em>
            Beer.swift
        </em>
        导入了
        <em>
            UIKit
        </em>
        。这个model使用了一些平台特有的逻辑，来为啤酒加载和保存图片。
    </p>
    <p>
        将文件顶部import的这行代码替换成下面这样：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">import</span> Foundation
</pre>
    <p>
        尝试运行项目，你会看到，现在由于
        <em>
            UIImage
        </em>
        是已被移除的
        <em>
            UIKit
        </em>
        中的一部分，它不会再被编译。当这个文件中的model部分在两个target之间可共享时，平台指定部分的逻辑就需要被分离出来。因此在
        <em>
            Beer.swift
        </em>
        中，删除全部标记为
        <em>
            Image Saving
        </em>
        的全部extension。在
        <code>
            import
        </code>
        语句之后，添加下列的协议：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">protocol</span> <span class="hljs-title">BeerImage</span> </span>{
  associatedtype <span class="hljs-type">Image</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">beerImage</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">Image</span>?
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">saveImage</span><span class="hljs-params">(<span class="hljs-number">_</span> image: Image)</span></span>
}
</pre>
    <p>
        由于每个模块仍然都需要访问啤酒的图片，并可以保存这些图片，这个protocol就提出了一个可以交给两个target来实现的协议。
    </p>
    <h3>
        Models
    </h3>
    <p>
        点击
        <em>
            File/New/File…
        </em>
        来创建一个新的文件，选择
        <em>
            Swift File
        </em>
        ，并将其命名为
        <em>
            Beer_iOS.swift
        </em>
        。确保仅有
        <em>
            BeerTracker
        </em>
        target被勾选。然后创建另一个名为
        <em>
            Beer_mac.swift
        </em>
        的文件，这次则只选中
        <em>
            BeerTracker-mac
        </em>
        作为target。
    </p>
    <p>
        打开
        <em>
            Beer_iOS.swift
        </em>
        ，删除文件全部的原始内容，并添加下列的代码：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">import</span> UIKit

<span class="hljs-comment">// MARK: - Image Saving</span>
<span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">Beer</span>: <span class="hljs-title">BeerImage</span> </span>{
  <span class="hljs-comment">// 1.</span>
  <span class="hljs-keyword">typealias</span> <span class="hljs-type">Image</span> = <span class="hljs-type">UIImage</span>

  <span class="hljs-comment">// 2.</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">beerImage</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">Image</span>? {
    <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> imagePath = imagePath,
      <span class="hljs-keyword">let</span> path = <span class="hljs-type">NSSearchPathForDirectoriesInDomains</span>(.documentDirectory, .userDomainMask, <span class="hljs-literal">true</span>).first <span class="hljs-keyword">else</span> {
        <span class="hljs-keyword">return</span> #imageLiteral(resourceName: <span class="hljs-string">"beerMugPlaceholder"</span>)
    }
    <span class="hljs-comment">// 3.</span>
    <span class="hljs-keyword">let</span> pathName = (path <span class="hljs-keyword">as</span> <span class="hljs-type">NSString</span>).appendingPathComponent(<span class="hljs-string">"BeerTracker/<span class="hljs-subst">\(imagePath)</span>"</span>)
    <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> image = <span class="hljs-type">Image</span>(contentsOfFile: pathName) <span class="hljs-keyword">else</span> { <span class="hljs-keyword">return</span> #imageLiteral(resourceName: <span class="hljs-string">"beerMugPlaceholder"</span>) }
    <span class="hljs-keyword">return</span> image
  }

  <span class="hljs-comment">// 4.</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">saveImage</span><span class="hljs-params">(<span class="hljs-number">_</span> image: Image)</span></span> {
    <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> imgData = <span class="hljs-type">UIImageJPEGRepresentation</span>(image, <span class="hljs-number">0.5</span>),
      <span class="hljs-keyword">let</span> path = <span class="hljs-type">NSSearchPathForDirectoriesInDomains</span>(.documentDirectory, .userDomainMask, <span class="hljs-literal">true</span>).first <span class="hljs-keyword">else</span> {
        <span class="hljs-keyword">return</span>
    }
    <span class="hljs-keyword">let</span> appPath = (path <span class="hljs-keyword">as</span> <span class="hljs-type">NSString</span>).appendingPathComponent(<span class="hljs-string">"/BeerTracker"</span>)
    <span class="hljs-keyword">let</span> fileName = <span class="hljs-string">"<span class="hljs-subst">\(UUID()</span>.uuidString).jpg"</span>
    <span class="hljs-keyword">let</span> pathName = (appPath <span class="hljs-keyword">as</span> <span class="hljs-type">NSString</span>).appendingPathComponent(fileName)
    <span class="hljs-keyword">var</span> isDirectory: <span class="hljs-type">ObjCBool</span> = <span class="hljs-literal">false</span>
    <span class="hljs-keyword">if</span> !<span class="hljs-type">FileManager</span>.<span class="hljs-keyword">default</span>.fileExists(atPath: appPath, isDirectory: &amp;isDirectory) {
      <span class="hljs-keyword">do</span> {
        <span class="hljs-keyword">try</span> <span class="hljs-type">FileManager</span>.<span class="hljs-keyword">default</span>.createDirectory(atPath: pathName, withIntermediateDirectories: <span class="hljs-literal">true</span>, attributes: <span class="hljs-literal">nil</span>)
      } <span class="hljs-keyword">catch</span> {
        <span class="hljs-built_in">print</span>(<span class="hljs-string">"Failed to create directory: <span class="hljs-subst">\(error)</span>"</span>)
      }
    }
    <span class="hljs-keyword">if</span> (<span class="hljs-keyword">try</span>? imgData.write(to: <span class="hljs-type">URL</span>(fileURLWithPath: pathName), options: [.atomic])) != <span class="hljs-literal">nil</span> {
      imagePath = fileName
    }
  }
}
</pre>
    <p>
        上述的代码：
    </p>
    <ol>
        <li>
            <em>
                BeerImage
            </em>
            协议要求实现的类定义一个
            <em>
                关联类型
            </em>
            。它是基于对象的实际需要的，你真实想使用的对象类型名称的占位符。因此在这个文件中，你会使用
            <em>
                UIImage
            </em>
            。
        </li>
        <li>
            实现协议的第一个方法。这里的
            <em>
                Image
            </em>
            类型就代表了
            <em>
                UIImage
            </em>
            。
        </li>
        <li>
            此处是当初始化一个image的时候，如何使用类型别名的另一个例子。
        </li>
        <li>
            实现第二个协议方法来保存image。
        </li>
    </ol>
    <p>
        将你的scheme切换为
        <em>
            BeerTracker
        </em>
        ，然后运行项目。app此时的表现应当如同之前一样。
    </p>
    <p>
        现在既然你的iOS target已经可以正常地工作了，你就可以去添加macOS指定的代码了。打开
        <em>
            Beer_mac.swift
        </em>
        ，删除全部的原始内容，并添加下列的代码：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">import</span> AppKit

<span class="hljs-comment">// MARK: - Image Saving</span>
<span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">Beer</span>: <span class="hljs-title">BeerImage</span> </span>{
  <span class="hljs-comment">// 1.</span>
  <span class="hljs-keyword">typealias</span> <span class="hljs-type">Image</span> = <span class="hljs-type">NSImage</span>

  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">beerImage</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">Image</span>? {
    <span class="hljs-comment">// 2.</span>
    <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> imagePath = imagePath,
      <span class="hljs-keyword">let</span> path = <span class="hljs-type">NSSearchPathForDirectoriesInDomains</span>(.applicationSupportDirectory, .userDomainMask, <span class="hljs-literal">true</span>).first <span class="hljs-keyword">else</span> {
        <span class="hljs-keyword">return</span> #imageLiteral(resourceName: <span class="hljs-string">"beerMugPlaceholder"</span>)
    }
    <span class="hljs-keyword">let</span> pathName = (path <span class="hljs-keyword">as</span> <span class="hljs-type">NSString</span>).appendingPathComponent(imagePath)
    <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> image = <span class="hljs-type">Image</span>(contentsOfFile: pathName) <span class="hljs-keyword">else</span> { <span class="hljs-keyword">return</span> #imageLiteral(resourceName: <span class="hljs-string">"beerMugPlaceholder"</span>) }
    <span class="hljs-keyword">return</span> image
  }

  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">saveImage</span><span class="hljs-params">(<span class="hljs-number">_</span> image: Image)</span></span> {
    <span class="hljs-comment">// 3.</span>
    <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> imgData = image.tiffRepresentation,
      <span class="hljs-keyword">let</span> path = <span class="hljs-type">NSSearchPathForDirectoriesInDomains</span>(.applicationSupportDirectory, .userDomainMask, <span class="hljs-literal">true</span>).first <span class="hljs-keyword">else</span> {
        <span class="hljs-keyword">return</span>
    }
    <span class="hljs-keyword">let</span> fileName = <span class="hljs-string">"/BeerTracker/<span class="hljs-subst">\(UUID()</span>.uuidString).jpg"</span>
    <span class="hljs-keyword">let</span> pathName = (path <span class="hljs-keyword">as</span> <span class="hljs-type">NSString</span>).appendingPathComponent(fileName)
    <span class="hljs-keyword">if</span> (<span class="hljs-keyword">try</span>? imgData.write(to: <span class="hljs-type">URL</span>(fileURLWithPath: pathName), options: [.atomic])) != <span class="hljs-literal">nil</span> {
      imagePath = fileName
    }
  }
}
</pre>
    <p>
        上述的代码和之前的一篇几乎如出一辙，只有几点的不同：
    </p>
    <ol>
        <li>
            这里使用
            <em>
                AppKit
            </em>
            指定的类
            <em>
                NSImage
            </em>
            来替换
            <em>
                UIImage
            </em>
            。
        </li>
        <li>
            在iOS中，通常会把文件保存到Documents目录下。你通常是不需要担心会把这个目录搞乱的，因为他是指定app下的目录，并且是对用户隐藏的。但在macOS中，你是不可以弄乱用户的Documents目录的，因此你要把文件保存到App的支持目录下。
        </li>
        <li>
            由于
            <em>
                NSImage
            </em>
            并没有和
            <em>
                UIImage
            </em>
            一样的获取图片data的方法，因此你需要使用
            <code>
                tiffRepresentation
            </code>
            来代替。
        </li>
    </ol>
    <p>
        将你的target切换为
        <em>
            BeerTracker_mac
        </em>
        ，然后运行项目。由于你的model已包含了标准功能的集合，app现在可以同时在两个平台上进行编译了。
    </p>
    <h3>
        创建用户界面
    </h3>
    <p>
        你空空的Mac app并没有什么用处，因此我们要来构建UI。在
        <em>
            BeerTracker-mac
        </em>
        组中，打开
        <em>
            Main.storyboard
        </em>
        。拖拽一个
        <em>
            Table View
        </em>
        到你空空的view上。现在在Document Outline中选择
        <em>
            Table View
        </em>
        。
        <br>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/Add-TableView-650x413.png"
        alt="Adding a table view" width="650" height="413" class="aligncenter size-large wp-image-162919"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/Add-TableView-650x413.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/05/Add-TableView-480x305.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/05/Add-TableView.png 1552w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        macOS的storyboards有时会要求你深入地挖掘视图层级。这点和iOS有所不同，你看到过iOS所有的模板view都处在顶层。
    </p>
    <h3>
        配置Table View
    </h3>
    <p>
        选中
        <em>
            Table View
        </em>
        ，然后在Attributes Inspector中做出下面的改变：
    </p>
    <ul>
        <li>
            将
            <em>
                Columns
            </em>
            设为1
        </li>
        <li>
            不勾选
            <em>
                Reordering
            </em>
        </li>
        <li>
            不勾选
            <em>
                Resizing
            </em>
        </li>
    </ul>
    <p>
        在Document Outline中选择
        <em>
            Table Column
        </em>
        ，并将它的Title设置为
        <em>
            Beer Name
        </em>
        。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/Beer-TrackerSelect-Table-View-2.png"
        alt="Selecting the table view" width="268" height="222" class="aligncenter size-medium wp-image-163228"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/Beer-TrackerSelect-Table-View-2.png 537w, https://koenig-media.raywenderlich.com/uploads/2017/05/Beer-TrackerSelect-Table-View-2-387x320.png 387w"
        sizes="(max-width: 268px) 100vw, 268px">
    </p>
    <p>
        在Document Outline中，选择
        <em>
            Bordered Scroll View
        </em>
        （它包含着
        <em>
            Table View
        </em>
        ），然后在Size Inspector中找到View这一部分，并将View的位置尺寸设置为：
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            ：0
        </li>
        <li>
            <em>
                y
            </em>
            ：17
        </li>
        <li>
            <em>
                width
            </em>
            ：185
        </li>
        <li>
            <em>
                height
            </em>
            ：253
        </li>
    </ul>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/SizeSettings.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/SizeSettings-229x320.png"
            alt="" width="229" height="320" class="aligncenter size-medium wp-image-164315"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/SizeSettings-229x320.png 229w, https://koenig-media.raywenderlich.com/uploads/2017/06/SizeSettings.png 255w"
            sizes="(max-width: 229px) 100vw, 229px">
        </a>
    </p>
    <p>
        坐标的设置在这里也有一点的不同。在macOS中，UI的原点并非位于左上侧，而在左下侧。这里你将
        <em>
            y
        </em>
        坐标设置为17，就意味着距离底部是17个像素点。
    </p>
    <h3>
        添加Delegate和Data Source
    </h3>
    <p>
        接下来你需要连接
        <em>
            Table View
        </em>
        的delegate，data source和property。你需要再次在Document Outline中选择
        <em>
            Table View
        </em>
        ，然后拖拽到Document Outline中的
        <em>
            View Controller
        </em>
        并点击
        <em>
            delegate
        </em>
        。为
        <em>
            dataSource
        </em>
        执行同样的操作。
    </p>
    <p>
        在Assistant Editor中打开
        <em>
            ViewController.swift
        </em>
        ，把
        <em>
            Table View
        </em>
        <em>
            拖拽
        </em>
        到这里，并创建一个新的名为
        <code>
            tableView
        </code>
        的outlet。
    </p>
    <p>
        在你完成
        <em>
            Table View
        </em>
        之前，还有最后一件事你需要去做。返回Document Outline，找到名为
        <em>
            Table Cell View
        </em>
        的item。选中它，打开Identity Inspector，并将
        <em>
            Identifier
        </em>
        设置为
        <em>
            NameCell
        </em>
        。
    </p>
    <h3>
        图片和文本
    </h3>
    <p>
        设置
        <em>
            Table View
        </em>
        完毕后，接下来就是设置UI的“form”部分了。
    </p>
    <p>
        首先，你需要添加一个
        <em>
            Image Well
        </em>
        到table的右侧。将frame设置为如下的形式：
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            : 190
        </li>
        <li>
            <em>
                y
            </em>
            : 188
        </li>
        <li>
            <em>
                width
            </em>
            : 75
        </li>
        <li>
            <em>
                height
            </em>
            : 75
        </li>
    </ul>
    <p>
        An
        <em>
            Image Well
        </em>
        is a convenient object that displays an image, but also allows a user
        to drag and drop a picture onto it. To accomplish this, the
        <em>
            Image Well
        </em>
        has the ability to connect an action to your code!
    </p>
    <p>
        Open the BeerTracker-mac
        <em>
            ViewController.swift
        </em>
        in the Assistant Editor and create an outlet for the
        <em>
            Image Well
        </em>
        named
        <code>
            imageView
        </code>
        . Also create an action for the
        <em>
            Image View
        </em>
        , and name it
        <code>
            imageChanged
        </code>
        . Ensure that you change
        <em>
            Type
        </em>
        to
        <em>
            NSImageView
        </em>
        , as shown:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-Image-View-Action-2.png"
        alt="Adding the imageView action." width="300" height="141" class="aligncenter size-full wp-image-163219">
    </p>
    <p>
        While drag and drop is great, sometimes users want to be able to view
        an
        <em>
            Open Dialog
        </em>
        and search for the file themselves. Set this up by dropping a
        <em>
            Click Gesture Recognizer
        </em>
        on the
        <em>
            Image Well
        </em>
        . In the Document Outline, connect an action from the
        <em>
            Click Gesture Recognizer
        </em>
        to
        <em>
            ViewController.swift
        </em>
        named
        <code>
            selectImage
        </code>
        .
    </p>
    <p>
        Add a
        <em>
            Text Field
        </em>
        to the right of the
        <em>
            Image Well
        </em>
        . In the Attributes Inspector, change the
        <em>
            Placeholder
        </em>
        to
        <em>
            Enter Name
        </em>
        . Set the frame to the following:
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            : 270
        </li>
        <li>
            <em>
                y
            </em>
            : 223
        </li>
        <li>
            <em>
                width
            </em>
            : 190
        </li>
        <li>
            <em>
                height
            </em>
            : 22
        </li>
    </ul>
    <p>
        Create an outlet in
        <em>
            ViewController.swift
        </em>
        for the
        <em>
            Text Field
        </em>
        named
        <code>
            nameField
        </code>
        .
    </p>
    <h3>
        Rating a Beer
    </h3>
    <p>
        Next, add a
        <em>
            Level Indicator
        </em>
        below the name field. This will control setting the rating of your beers.
        In the Attributes Inspector, set the following:
    </p>
    <ul>
        <li>
            <em>
                Style
            </em>
            : Rating
        </li>
        <li>
            <em>
                State
            </em>
            : Editable
        </li>
        <li>
            <em>
                Minimum
            </em>
            : 0
        </li>
        <li>
            <em>
                Maximum
            </em>
            : 5
        </li>
        <li>
            <em>
                Warning
            </em>
            : 0
        </li>
        <li>
            <em>
                Critical
            </em>
            : 0
        </li>
        <li>
            <em>
                Current
            </em>
            : 5
        </li>
        <li>
            <em>
                Image
            </em>
            : beerMug
        </li>
    </ul>
    <p>
        Set the frame to the following:
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            : 270
        </li>
        <li>
            <em>
                y
            </em>
            : 176
        </li>
        <li>
            <em>
                width
            </em>
            : 115
        </li>
    </ul>
    <p>
        Create an outlet for the
        <em>
            Level Indicator
        </em>
        named
        <code>
            ratingIndicator
        </code>
        .
    </p>
    <p>
        Add a
        <em>
            Text View
        </em>
        below the rating indicator. Set the frame to:
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            : 193
        </li>
        <li>
            <em>
                y
            </em>
            : 37
        </li>
        <li>
            <em>
                width
            </em>
            : 267
        </li>
        <li>
            <em>
                height
            </em>
            : 134
        </li>
    </ul>
    <p>
        To create an outlet for the
        <em>
            Text View
        </em>
        , you’ll need to make sure you select
        <em>
            Text View
        </em>
        inside the Document Outline, like you did with the
        <em>
            Table View
        </em>
        . Name the outlet
        <code>
            noteView
        </code>
        . You’ll also need to set the
        <em>
            Text View
        </em>
        ‘s delegate to the
        <em>
            ViewController
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/TextView.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/TextView.png"
            alt="" width="216" height="84" class="aligncenter size-full wp-image-164317">
        </a>
    </p>
    <p>
        Below the note view, drop in a
        <em>
            Push Button
        </em>
        . Change the title to
        <em>
            Update
        </em>
        , and set the frame to:
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            : 284
        </li>
        <li>
            <em>
                y
            </em>
            : 3
        </li>
        <li>
            <em>
                width
            </em>
            : 85
        </li>
    </ul>
    <p>
        Connect an action from the button to
        <em>
            ViewController
        </em>
        named
        <code>
            updateBeer
        </code>
        .
    </p>
    <h3>
        Adding and Removing Beers
    </h3>
    <p>
        With that, you have all the necessary controls to edit and view your beer
        information. However, there’s no way to add or remove beers. This will
        make the app difficult to use, even if your users haven’t had anything
        to drink. :]
    </p>
    <p>
        Add a
        <em>
            Gradient Button
        </em>
        to the bottom left of the screen. In the Attributes Inspector, change
        <em>
            Image
        </em>
        to
        <em>
            NSAddTemplate
        </em>
        if it is not already set.
    </p>
    <p>
        In the Size Inspector, set the frame to:
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            : 0
        </li>
        <li>
            <em>
                y
            </em>
            : -1
        </li>
        <li>
            <em>
                width
            </em>
            : 24
        </li>
        <li>
            <em>
                height
            </em>
            : 20
        </li>
    </ul>
    <p>
        Add an action from the new button named
        <code>
            addBeer
        </code>
        .
    </p>
    <p>
        One great thing about macOS is that you get access to template images
        like the
        <em>
            +
        </em>
        sign. This can make your life a lot simpler when you have any standard
        action buttons, but don’t have the time or ability to create your own artwork.
    </p>
    <p>
        Next, you’ll need to add the remove button. Add another
        <em>
            Gradient Button
        </em>
        directly to the right of the previous button, and change the
        <em>
            Image
        </em>
        to
        <em>
            NSRemoveTemplate
        </em>
        . Set the frame to:
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            : 23
        </li>
        <li>
            <em>
                y
            </em>
            : -1
        </li>
        <li>
            <em>
                width
            </em>
            : 24
        </li>
        <li>
            <em>
                height
            </em>
            : 20
        </li>
    </ul>
    <p>
        And finally, add an action from this button named
        <code>
            removeBeer
        </code>
        .
    </p>
    <h3>
        Finishing The UI
    </h3>
    <p>
        You’re almost finished building the UI! You just need to add a few labels
        to help polish it off.
    </p>
    <p>
        Add the following labels:
    </p>
    <ul>
        <li>
            Above the name field, titled
            <em>
                Name
            </em>
            .
        </li>
        <li>
            Above the rating indicator titled
            <em>
                Rating
            </em>
            .
        </li>
        <li>
            Above the notes view titled
            <em>
                Notes
            </em>
            .
        </li>
        <li>
            Beneath the table view titled
            <em>
                Beer Count:
            </em>
            .
        </li>
        <li>
            To the right of the beer count label, titled
            <em>
                0
            </em>
            .
        </li>
    </ul>
    <p>
        For each of these labels, in the Attributes Inspector, set the font to
        <em>
            Other – Label
        </em>
        , and the size to 10.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/labelFont.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/labelFont.png"
            alt="" width="196" height="285" class="aligncenter size-full wp-image-164319">
        </a>
    </p>
    <p>
        For the last label, connect an outlet to
        <em>
            ViewController.swift
        </em>
        named
        <code>
            beerCountField
        </code>
        .
    </p>
    <p>
        Make sure your labels all line like so:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-2.png"
        alt="Final UI" width="600" height="374" class="aligncenter size-full wp-image-163220"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-2.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-2-480x299.png 480w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <p>
        Click the Resolve
        <em>
            Auto Layout Issues
        </em>
        button and in the
        <em>
            All Views in View Controller
        </em>
        section click
        <em>
            Reset to Suggested Constraints
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/AutoLayout-1.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/AutoLayout-1.png"
            alt="" width="243" height="197" class="aligncenter size-full wp-image-164423">
        </a>
    </p>
    <h3>
        Adding the Code
    </h3>
    <p>
        Whew! Now you’re ready to code. Open
        <em>
            ViewController.swift
        </em>
        and delete the property named
        <code>
            representedObject
        </code>
        . Add the following methods below
        <code>
            viewDidLoad()
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            private
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                setFieldsEnabled
            </span>
            <span class="hljs-params">
                (enabled: Bool)
            </span>
        </span>
        { imageView.isEditable = enabled nameField.isEnabled = enabled ratingIndicator.isEnabled
        = enabled noteView.isEditable = enabled }
        <span class="hljs-keyword">
            private
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                updateBeerCountLabel
            </span>
            <span class="hljs-params">
                ()
            </span>
        </span>
        { beerCountField.stringValue =
        <span class="hljs-string">
            "
            <span class="hljs-subst">
                \(BeerManager.sharedInstance.beers.
                <span class="hljs-built_in">
                    count
                </span>
                )
            </span>
            "
        </span>
        }
    </pre>
    <p>
        There are two methods that will help you control your UI:
    </p>
    <ol>
        <li>
            <code>
                setFieldsEnabled(\_:)
            </code>
            will allow you to easily turn off and on the ability to use the form controls.
        </li>
        <li>
            <code>
                updateBeerCountLabel()
            </code>
            simply sets the count of beers in the
            <code>
                beerCountField
            </code>
            .
        </li>
    </ol>
    <p>
        Beneath all of your outlets, add the following property:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            var
        </span>
        selectedBeer:
        <span class="hljs-type">
            Beer
        </span>
        ? {
        <span class="hljs-keyword">
            didSet
        </span>
        {
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        selectedBeer = selectedBeer
        <span class="hljs-keyword">
            else
        </span>
        { setFieldsEnabled(enabled:
        <span class="hljs-literal">
            false
        </span>
        ) imageView.image =
        <span class="hljs-literal">
            nil
        </span>
        nameField.stringValue =
        <span class="hljs-string">
            ""
        </span>
        ratingIndicator.integerValue =
        <span class="hljs-number">
            0
        </span>
        noteView.string =
        <span class="hljs-string">
            ""
        </span>
        <span class="hljs-keyword">
            return
        </span>
        } setFieldsEnabled(enabled:
        <span class="hljs-literal">
            true
        </span>
        ) imageView.image = selectedBeer.beerImage() nameField.stringValue = selectedBeer.name
        ratingIndicator.integerValue = selectedBeer.rating noteView.string = selectedBeer.note!
        } }
    </pre>
    <p>
        This property will keep track of the beer selected from the table view.
        If no beer is currently selected, the setter takes care of clearing the
        values from all the fields, and disabling the UI components that shouldn’t
        be used.
    </p>
    <p>
        Replace
        <code>
            viewDidLoad()
        </code>
        with the following code:
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
                viewDidLoad
            </span>
            <span class="hljs-params">
                ()
            </span>
        </span>
        {
        <span class="hljs-keyword">
            super
        </span>
        .viewDidLoad()
        <span class="hljs-keyword">
            if
        </span>
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers.
        <span class="hljs-built_in">
            count
        </span>
        ==
        <span class="hljs-number">
            0
        </span>
        { setFieldsEnabled(enabled:
        <span class="hljs-literal">
            false
        </span>
        ) }
        <span class="hljs-keyword">
            else
        </span>
        { tableView.selectRowIndexes(
        <span class="hljs-type">
            IndexSet
        </span>
        (integer:
        <span class="hljs-number">
            0
        </span>
        ), byExtendingSelection:
        <span class="hljs-literal">
            false
        </span>
        ) } updateBeerCountLabel() }
    </pre>
    <p>
        Just like in iOS, you want our app to do something the moment it starts
        up. In the macOS version, however, you’ll need to immediately fill out
        the form for the user to see their data.
    </p>
    <h3>
        Adding Data to the Table View
    </h3>
    <p>
        Right now, the table view isn’t actually able to display any data, but
        <code>
            selectRowIndexes(\_:byExtendingSelection:)
        </code>
        will select the first beer in the list. The delegate code will handle
        the rest for you.
    </p>
    <p>
        In order to get the table view showing you your list of beers, add the
        following code to the end of
        <em>
            ViewController.swift
        </em>
        , outside of the
        <code>
            ViewController
        </code>
        class:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-class">
            <span class="hljs-keyword">
                extension
            </span>
            <span class="hljs-title">
                ViewController
            </span>
            :
            <span class="hljs-title">
                NSTableViewDataSource
            </span>
        </span>
        {
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                numberOfRows
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-keyword">
                    in
                </span>
                tableView: NSTableView)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            Int
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers.
        <span class="hljs-built_in">
            count
        </span>
        } }
        <span class="hljs-class">
            <span class="hljs-keyword">
                extension
            </span>
            <span class="hljs-title">
                ViewController
            </span>
            :
            <span class="hljs-title">
                NSTableViewDelegate
            </span>
        </span>
        {
        <span class="hljs-comment">
            // MARK: - CellIdentifiers
        </span>
        <span class="hljs-keyword">
            fileprivate
        </span>
        <span class="hljs-class">
            <span class="hljs-keyword">
                enum
            </span>
            <span class="hljs-title">
                CellIdentifier
            </span>
        </span>
        {
        <span class="hljs-keyword">
            static
        </span>
        <span class="hljs-keyword">
            let
        </span>
        <span class="hljs-type">
            NameCell
        </span>
        =
        <span class="hljs-string">
            "NameCell"
        </span>
        }
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                tableView
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                tableView: NSTableView, viewFor tableColumn: NSTableColumn?, row: Int)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            NSView
        </span>
        ? {
        <span class="hljs-keyword">
            let
        </span>
        beer =
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers[row]
        <span class="hljs-keyword">
            if
        </span>
        <span class="hljs-keyword">
            let
        </span>
        cell = tableView.makeView(withIdentifier:
        <span class="hljs-type">
            NSUserInterfaceItemIdentifier
        </span>
        (rawValue:
        <span class="hljs-type">
            CellIdentifier
        </span>
        .
        <span class="hljs-type">
            NameCell
        </span>
        ), owner:
        <span class="hljs-literal">
            nil
        </span>
        )
        <span class="hljs-keyword">
            as
        </span>
        ?
        <span class="hljs-type">
            NSTableCellView
        </span>
        { cell.textField?.stringValue = beer.name
        <span class="hljs-keyword">
            if
        </span>
        beer.name.characters.
        <span class="hljs-built_in">
            count
        </span>
        ==
        <span class="hljs-number">
            0
        </span>
        { cell.textField?.stringValue =
        <span class="hljs-string">
            "New Beer"
        </span>
        }
        <span class="hljs-keyword">
            return
        </span>
        cell }
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-literal">
            nil
        </span>
        }
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                tableViewSelectionDidChange
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                notification: Notification)
            </span>
        </span>
        {
        <span class="hljs-keyword">
            if
        </span>
        tableView.selectedRow &gt;=
        <span class="hljs-number">
            0
        </span>
        { selectedBeer =
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers[tableView.selectedRow] } } }
    </pre>
    <p>
        This code takes care of populating the table view’s rows from the data
        source.
    </p>
    <p>
        Look at it closely, and you’ll see it’s not too different from the iOS
        counterpart found in
        <em>
            BeersTableViewController.swift
        </em>
        . One notable difference is that when the table view selection changes,
        it sends a
        <em>
            Notification
        </em>
        to the
        <em>
            NSTableViewDelegate
        </em>
        .
    </p>
    <p>
        Remember that your new macOS app has multiple input sources — not just
        a finger. Using a mouse or keyboard can change the selection of the table
        view, and that makes handling the change just a little different to iOS.
    </p>
    <p>
        Now to add a beer. Change
        <code>
            addBeer()
        </code>
        to:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-meta">
            @IBAction
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                addBeer
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                sender: Any)
            </span>
        </span>
        {
        <span class="hljs-comment">
            // 1.
        </span>
        <span class="hljs-keyword">
            let
        </span>
        beer =
        <span class="hljs-type">
            Beer
        </span>
        () beer.name =
        <span class="hljs-string">
            ""
        </span>
        beer.rating =
        <span class="hljs-number">
            1
        </span>
        beer.note =
        <span class="hljs-string">
            ""
        </span>
        selectedBeer = beer
        <span class="hljs-comment">
            // 2.
        </span>
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers.insert(beer, at:
        <span class="hljs-number">
            0
        </span>
        )
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.saveBeers()
        <span class="hljs-comment">
            // 3.
        </span>
        <span class="hljs-keyword">
            let
        </span>
        indexSet =
        <span class="hljs-type">
            IndexSet
        </span>
        (integer:
        <span class="hljs-number">
            0
        </span>
        ) tableView.beginUpdates() tableView.insertRows(at: indexSet, withAnimation:
        .slideDown) tableView.endUpdates() updateBeerCountLabel()
        <span class="hljs-comment">
            // 4.
        </span>
        tableView.selectRowIndexes(
        <span class="hljs-type">
            IndexSet
        </span>
        (integer:
        <span class="hljs-number">
            0
        </span>
        ), byExtendingSelection:
        <span class="hljs-literal">
            false
        </span>
        ) }
    </pre>
    <p>
        Nothing too crazy here. You’re simply doing the following:
    </p>
    <ol>
        <li>
            Creating a new beer.
        </li>
        <li>
            Inserting the beer into the model.
        </li>
        <li>
            Inserting a new row into the table.
        </li>
        <li>
            Selecting the row of the new beer.
        </li>
    </ol>
    <p>
        You might have even noticed that, like in iOS, you need to call
        <code>
            beginUpdates()
        </code>
        and
        <code>
            endUpdates()
        </code>
        before inserting the new row. See, you really do know a lot about macOS
        already!
    </p>
    <h3>
        Removing Entries
    </h3>
    <p>
        To remove a beer, add the below code for
        <code>
            removeBeer(\_:)
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-meta">
            @IBAction
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                removeBeer
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                sender: Any)
            </span>
        </span>
        {
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        beer = selectedBeer,
        <span class="hljs-keyword">
            let
        </span>
        index =
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers.index(of: beer)
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        }
        <span class="hljs-comment">
            // 1.
        </span>
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers.remove(at: index)
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.saveBeers()
        <span class="hljs-comment">
            // 2
        </span>
        tableView.reloadData() updateBeerCountLabel() tableView.selectRowIndexes(
        <span class="hljs-type">
            IndexSet
        </span>
        (integer:
        <span class="hljs-number">
            0
        </span>
        ), byExtendingSelection:
        <span class="hljs-literal">
            false
        </span>
        )
        <span class="hljs-keyword">
            if
        </span>
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers.
        <span class="hljs-built_in">
            count
        </span>
        ==
        <span class="hljs-number">
            0
        </span>
        { selectedBeer =
        <span class="hljs-literal">
            nil
        </span>
        } }
    </pre>
    <p>
        Once again, very straightforward code:
    </p>
    <ol>
        <li>
            If a beer is selected, you remove it from the model.
        </li>
        <li>
            Reload the table view, and select the first available beer.
        </li>
    </ol>
    <h3>
        Handling Images
    </h3>
    <p>
        Remember how
        <em>
            Image Wells
        </em>
        have the ability to accept an image dropped on them? Change
        <code>
            imageChanged(\_:)
        </code>
        to:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-meta">
            @IBAction
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                imageChanged
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                sender: NSImageView)
            </span>
        </span>
        {
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        image = sender.image
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        } selectedBeer?.saveImage(image) }
    </pre>
    <p>
        And you thought it was going to be hard! Apple has taken care of all the
        heavy lifting for you, and provides you with the image dropped.
    </p>
    <p>
        On the flip side to that, you’ll need to do a bit more work to handle
        user’s picking the image from within your app. Replace
        <code>
            selectImage()
        </code>
        with:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-meta">
            @IBAction
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                selectImage
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                sender: Any)
            </span>
        </span>
        {
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        window = view.window
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        }
        <span class="hljs-comment">
            // 1.
        </span>
        <span class="hljs-keyword">
            let
        </span>
        openPanel =
        <span class="hljs-type">
            NSOpenPanel
        </span>
        () openPanel.allowsMultipleSelection =
        <span class="hljs-literal">
            false
        </span>
        openPanel.canChooseDirectories =
        <span class="hljs-literal">
            false
        </span>
        openPanel.canCreateDirectories =
        <span class="hljs-literal">
            false
        </span>
        openPanel.canChooseFiles =
        <span class="hljs-literal">
            true
        </span>
        <span class="hljs-comment">
            // 2.
        </span>
        openPanel.allowedFileTypes = [
        <span class="hljs-string">
            "jpg"
        </span>
        ,
        <span class="hljs-string">
            "png"
        </span>
        ,
        <span class="hljs-string">
            "tiff"
        </span>
        ]
        <span class="hljs-comment">
            // 3.
        </span>
        openPanel.beginSheetModal(
        <span class="hljs-keyword">
            for
        </span>
        : window) { (result)
        <span class="hljs-keyword">
            in
        </span>
        <span class="hljs-keyword">
            if
        </span>
        result ==
        <span class="hljs-type">
            NSApplication
        </span>
        .
        <span class="hljs-type">
            ModalResponse
        </span>
        .
        <span class="hljs-type">
            OK
        </span>
        {
        <span class="hljs-comment">
            // 4.
        </span>
        <span class="hljs-keyword">
            if
        </span>
        <span class="hljs-keyword">
            let
        </span>
        panelURL = openPanel.url,
        <span class="hljs-keyword">
            let
        </span>
        beerImage =
        <span class="hljs-type">
            NSImage
        </span>
        (contentsOf: panelURL) {
        <span class="hljs-keyword">
            self
        </span>
        .selectedBeer?.saveImage(beerImage)
        <span class="hljs-keyword">
            self
        </span>
        .imageView.image = beerImage } } } }
    </pre>
    <p>
        The above code is how you use
        <code>
            NSOpenPanel
        </code>
        to select a file. Here’s what’s happening:
    </p>
    <ol>
        <li>
            You create an
            <code>
                NSOpenPanel
            </code>
            , and configure its settings.
        </li>
        <li>
            In order to allow the user to choose only pictures, you set the allowed
            file types to your preferred image formats.
        </li>
        <li>
            Present the sheet to the user.
        </li>
        <li>
            Save the image if the user selected one.
        </li>
    </ol>
    <p>
        Finally, add the code that will save the data model in
        <code>
            updateBeer(\_:)
        </code>
        :
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-meta">
            @IBAction
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                updateBeer
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                sender: Any)
            </span>
        </span>
        {
        <span class="hljs-comment">
            // 1.
        </span>
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        beer = selectedBeer,
        <span class="hljs-keyword">
            let
        </span>
        index =
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.beers.index(of: beer)
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        } beer.name = nameField.stringValue beer.rating = ratingIndicator.integerValue
        beer.note = noteView.string
        <span class="hljs-comment">
            // 2.
        </span>
        <span class="hljs-keyword">
            let
        </span>
        indexSet =
        <span class="hljs-type">
            IndexSet
        </span>
        (integer: index) tableView.beginUpdates() tableView.reloadData(forRowIndexes:
        indexSet, columnIndexes:
        <span class="hljs-type">
            IndexSet
        </span>
        (integer:
        <span class="hljs-number">
            0
        </span>
        )) tableView.endUpdates()
        <span class="hljs-comment">
            // 3.
        </span>
        <span class="hljs-type">
            BeerManager
        </span>
        .sharedInstance.saveBeers() }
    </pre>
    <p>
        Here’s what you added:
    </p>
    <ol>
        <li>
            You ensure the beer exists, and update its properties.
        </li>
        <li>
            Update the table view to reflect any names changes in the table.
        </li>
        <li>
            Save the data to the disk.
        </li>
    </ol>
    <p>
        You’re all set! Build and run the app, and start adding beers. Remember,
        you’ll need to select
        <em>
            Update
        </em>
        to save your data.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-Beers.png"
        alt="Final UI with some beers added." width="600" height="374" class="aligncenter size-full wp-image-163221"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-Beers.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-Beers-480x299.png 480w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <h3>
        Final Touches
    </h3>
    <p>
        You’ve learned a lot about the similarities and differences between iOS
        and macOS development. There’s another concept that you should familiarize
        yourself with:
        <em>
            Settings/Preferences
        </em>
        . In iOS, you should be comfortable with the concept of going into Settings,
        finding your desired app, and changing any settings available to you. In
        macOS, this can be accomplished inside your app through
        <em>
            Preferences
        </em>
        .
    </p>
    <p>
        Build and run the
        <em>
            BeerTracker
        </em>
        target, and in the simulator, navigate to the BeerTracker settings in
        the Settings app. There you’ll find a setting allowing your users to limit
        the length of their notes, just in case they get a little chatty after
        having a few.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTrackerSettings-282x500.png"
        alt="Settings - iOS" width="282" height="500" class="aligncenter size-large wp-image-162952"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTrackerSettings-282x500.png 282w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTrackerSettings-180x320.png 180w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTrackerSettings.png 640w"
        sizes="(max-width: 282px) 100vw, 282px">
    </p>
    <p>
        In order to get the same feature in your mac app, you’ll create a Preferences
        window for the user. In
        <em>
            BeerTracker-mac
        </em>
        , open
        <em>
            Main.storyboard
        </em>
        , and drop in a new
        <em>
            Window Controller
        </em>
        . Select the
        <em>
            Window
        </em>
        , open the Size Inspector, and change the following:
    </p>
    <ol>
        <li>
            Set
            <em>
                Content Size
            </em>
            width to 380, and height to 55.
        </li>
        <li>
            Check
            <em>
                Minimum Content Size
            </em>
            , and set width to 380, and height to 55.
        </li>
        <li>
            Check
            <em>
                Maximum Content Size
            </em>
            , and set width to 380, and height to 55.
        </li>
        <li>
            Check
            <em>
                Full Screen Minimum Content Size
            </em>
            , and set width to 380, and height to 55.
        </li>
        <li>
            Check
            <em>
                Full Screen Maximum Content Size
            </em>
            , and set width to 380, and height to 55.
        </li>
        <li>
            Under
            <em>
                Initial Position
            </em>
            , select
            <em>
                Center Horizontally
            </em>
            and
            <em>
                Center Vertically
            </em>
            .
        </li>
    </ol>
    <p>
        Next, select the View of the empty View Controller, and change the size
        to match the above settings, 380 x 55.
    </p>
    <p>
        Doing these things will ensure your Preferences window is always the same
        size, and opens in a logical place to the user. When you’re finished, your
        new window should look like this in the storyboard:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-Preferences-Window-1.png"
        alt="Preferences - Mac" width="700" height="477" class="aligncenter size-full wp-image-163222"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-Preferences-Window-1.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-Preferences-Window-1-470x320.png 470w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-Preferences-Window-1-650x443.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        At this point, there is no way for a user to open your new window. Since
        it should be tied to the
        <em>
            Preferences
        </em>
        menu item, find the menu bar scene in storyboard. It will be easier if
        you drag it close to the Preferences window for this next part. Once it
        is close enough, do the following:
    </p>
    <ol>
        <li>
            In the menu bar in storyboard, click
            <em>
                BeerTracker-mac
            </em>
            to open the menu.
        </li>
        <li>
            <em>
                Control-drag
            </em>
            from the
            <em>
                Preferences
            </em>
            menu item to the new Window Controller
        </li>
        <li>
            Select
            <em>
                Show
            </em>
            from the dialog
        </li>
    </ol>
    <p>
        Find a
        <em>
            Check Box Button
        </em>
        , and add it to the empty View Controller. Change the text to be
        <em>
            Restrict Note Length to 1,024 Characters
        </em>
        .
    </p>
    <p>
        With the
        <em>
            Checkbox Button
        </em>
        selected, open the Bindings Inspector, and do the following:
    </p>
    <ol>
        <li>
            Expand
            <em>
                Value
            </em>
            , and check
            <em>
                Bind to
            </em>
            .
        </li>
        <li>
            Select
            <em>
                Shared User Defaults Controller
            </em>
            from the drop down.
        </li>
        <li>
            In
            <em>
                Model Key Path
            </em>
            , put
            <em>
                BT_Restrict_Note_Length
            </em>
            .
        </li>
    </ol>
    <p>
        Create a new Swift file in the
        <em>
            Utilities
        </em>
        group named
        <em>
            StringValidator.swift
        </em>
        . Make sure to check both targets for this file.
    </p>
    <p>
        Open
        <em>
            StringValidator.swift
        </em>
        , and replace the contents with the following code:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-keyword">
            import
        </span>
        Foundation
        <span class="hljs-class">
            <span class="hljs-keyword">
                extension
            </span>
            <span class="hljs-title">
                String
            </span>
        </span>
        {
        <span class="hljs-keyword">
            private
        </span>
        <span class="hljs-keyword">
            static
        </span>
        <span class="hljs-keyword">
            let
        </span>
        noteLimit =
        <span class="hljs-number">
            1024
        </span>
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                isValidLength
            </span>
            <span class="hljs-params">
                ()
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            Bool
        </span>
        {
        <span class="hljs-keyword">
            let
        </span>
        limitLength =
        <span class="hljs-type">
            UserDefaults
        </span>
        .standard.bool(forKey:
        <span class="hljs-string">
            "BT_Restrict_Note_Length"
        </span>
        )
        <span class="hljs-keyword">
            if
        </span>
        limitLength {
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-keyword">
            self
        </span>
        .characters.
        <span class="hljs-built_in">
            count
        </span>
        &lt;=
        <span class="hljs-type">
            String
        </span>
        .noteLimit }
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-literal">
            true
        </span>
        } }
    </pre>
    <p>
        This class will provide both targets with the ability to check if a string
        is a valid length, but only if the user default
        <em>
            BT_Restrict_Note_Length
        </em>
        is true.
    </p>
    <p>
        In
        <em>
            ViewController.swift
        </em>
        add the following code at the bottom:
    </p>
    <pre lang="swift" class="language-swift hljs">
        <span class="hljs-class">
            <span class="hljs-keyword">
                extension
            </span>
            <span class="hljs-title">
                ViewController
            </span>
            :
            <span class="hljs-title">
                NSTextViewDelegate
            </span>
        </span>
        {
        <span class="hljs-function">
            <span class="hljs-keyword">
                func
            </span>
            <span class="hljs-title">
                textView
            </span>
            <span class="hljs-params">
                (
                <span class="hljs-number">
                    _
                </span>
                textView: NSTextView, shouldChangeTextIn affectedCharRange: NSRange, replacementString:
                String?)
            </span>
        </span>
        -&gt;
        <span class="hljs-type">
            Bool
        </span>
        {
        <span class="hljs-keyword">
            guard
        </span>
        <span class="hljs-keyword">
            let
        </span>
        replacementString = replacementString
        <span class="hljs-keyword">
            else
        </span>
        {
        <span class="hljs-keyword">
            return
        </span>
        <span class="hljs-literal">
            true
        </span>
        }
        <span class="hljs-keyword">
            let
        </span>
        currentText = textView.string
        <span class="hljs-keyword">
            let
        </span>
        proposed = (currentText
        <span class="hljs-keyword">
            as
        </span>
        <span class="hljs-type">
            NSString
        </span>
        ).replacingCharacters(
        <span class="hljs-keyword">
            in
        </span>
        : affectedCharRange, with: replacementString)
        <span class="hljs-keyword">
            return
        </span>
        proposed.isValidLength() } }
    </pre>
    <p>
        Finally, change the names of each
        <em>
            Window
        </em>
        in
        <em>
            Main.storyboard
        </em>
        to match their purpose, and give the user more clarity. Select the initial
        <em>
            Window Controller
        </em>
        , and in the
        <em>
            Attributes Inspector
        </em>
        change the title to
        <em>
            BeerTracker
        </em>
        . Select the
        <em>
            Window Controller
        </em>
        for the Preferences window, and change the title to
        <em>
            Preferences
        </em>
        .
    </p>
    <p>
        Build and run your app. If you select the Preferences menu item, you should
        now see your new Preferences window with your preferences item. Select
        the checkbox, and find some large amount of text to paste in. If this would
        make the note more 1024 characters, the
        <em>
            Text View
        </em>
        will not accept it, just like the iOS app.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/Screen-Shot-2017-06-12-at-6.31.32-PM.png"
        alt="Build and Run with Preferences" width="484" height="297" class="alignnone size-full wp-image-164558"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/Screen-Shot-2017-06-12-at-6.31.32-PM.png 484w, https://koenig-media.raywenderlich.com/uploads/2017/06/Screen-Shot-2017-06-12-at-6.31.32-PM-480x295.png 480w"
        sizes="(max-width: 484px) 100vw, 484px">
    </p>
    <h2>
        Where to Go From Here?
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
        You can download the finished project
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/BeerTracker-Port_Finished-2.zip"
        sl-processed="1">
            here
        </a>
        .
    </p>
    <p>
        In this tutorial you learned:
    </p>
    <ul>
        <li>
            How to utilize a current iOS project to host a macOS app.
        </li>
        <li>
            When to separate code based on your platform's needs.
        </li>
        <li>
            How to reuse existing code between both projects.
        </li>
        <li>
            The differences between some of Xcode's behaviors between the two platforms.
        </li>
    </ul>
    <p>
        For more information about porting your apps to macOS, check out
        <a href="https://developer.apple.com/library/content/documentation/MacOSX/Conceptual/OSX_Technology_Overview/MigratingFromCocoaTouch/MigratingFromCocoaTouch.html"
        sl-processed="1">
            Apple's Migrating from Cocoa Touch Overview
        </a>
        .
    </p>
    <p>
        If you have any questions or comments, please join in the forum discussion
        below!
    </p>
</div>