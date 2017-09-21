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
        到table的右侧。将frame设置为如下的数值：
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            ：190
        </li>
        <li>
            <em>
                y
            </em>
            ：188
        </li>
        <li>
            <em>
                width
            </em>
            ：75
        </li>
        <li>
            <em>
                height
            </em>
            ：75
        </li>
    </ul>
    <p>
        <em>
            Image Well
        </em>
        是一个方便的用来展示图片的对象，但也允许用户把一张图片拖拽到它的上面。为了实现这点，
        <em>
            Image Well
        </em>
        拥有将动作连接到你代码上的能力！
    </p>
    <p>
        在Assistant Editor中打开BeerTracker-mac的
        <em>
            ViewController.swift
        </em>
        ，并为
        <em>
            Image Well
        </em>
        创建一个名为
        <code>
            imageView
        </code>
        的outlet。然后为
        <em>
            Image View
        </em>
        创建一个名为
        <code>
            imageChanged
        </code>
        的动作。确保将
        <em>
            Type
        </em>
        设置为
        <em>
            NSImageView
        </em>
        ，就像下面这样：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-Image-View-Action-2.png"
        alt="Adding the imageView action." width="300" height="141" class="aligncenter size-full wp-image-163219">
    </p>
    <p>
        拖拽尽管非常得棒，有时用户却更希望看到一个
        <em>
            打开对话框
        </em>
        由它们自己来搜索文件。拖拽一个
        <em>
            Click Gesture Recognizer
        </em>
        到
        <em>
            Image Well
        </em>
        的上面。在Document Outline中，将
        <em>
            Click Gesture Recognizer
        </em>
        连接到
        <em>
            ViewController.swift
        </em>
        中并命名为
        <code>
            selectImage
        </code>
        。
    </p>
    <p>
        在
        <em>
            Image Well
        </em>
        的右侧添加一个
        <em>
            Text Field
        </em>
        。在Attributes Inspector中，将
        <em>
            Placeholder
        </em>
        改为
        <em>
            Enter Name
        </em>
        。将frame设置成下面的样子：
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            ：270
        </li>
        <li>
            <em>
                y
            </em>
            ：223
        </li>
        <li>
            <em>
                width
            </em>
            ：190
        </li>
        <li>
            <em>
                height
            </em>
            ：22
        </li>
    </ul>
    <p>
        在
        <em>
            ViewController.swift
        </em>
        中为
        <em>
            Text Field
        </em>
        创建一个名为
        <code>
            nameField
        </code>
        的outlet。
    </p>
    <h3>
        给啤酒评分
    </h3>
    <p>
        下面，添加一个
        <em>
            Level Indicator
        </em>
        到name field的下面。它将用来控制你的啤酒的评分。在Attributes Inspector中进行如下的设置：
    </p>
    <ul>
        <li>
            <em>
                Style
            </em>
            ：Rating
        </li>
        <li>
            <em>
                State
            </em>
            ：Editable
        </li>
        <li>
            <em>
                Minimum
            </em>
            ：0
        </li>
        <li>
            <em>
                Maximum
            </em>
            ：5
        </li>
        <li>
            <em>
                Warning
            </em>
            ：0
        </li>
        <li>
            <em>
                Critical
            </em>
            ：0
        </li>
        <li>
            <em>
                Current
            </em>
            ：5
        </li>
        <li>
            <em>
                Image
            </em>
            ：beerMug
        </li>
    </ul>
    <p>
        将frame设置为下面的样子：
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            ：270
        </li>
        <li>
            <em>
                y
            </em>
            ：176
        </li>
        <li>
            <em>
                width
            </em>
            ：115
        </li>
    </ul>
    <p>
        为
        <em>
            Level Indicator
        </em>
        创建一个名为
        <code>
            ratingIndicator
        </code>
        的outlet。
    </p>
    <p>
        在rating indicator的下面添加一个        
        <em>
            Text View
        </em>
        。将它的frame设置为：
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            ：193
        </li>
        <li>
            <em>
                y
            </em>
            ：37
        </li>
        <li>
            <em>
                width
            </em>
            ：267
        </li>
        <li>
            <em>
                height
            </em>
            ：134
        </li>
    </ul>
    <p>
        要为
        <em>
            Text View
        </em>
        创建一个outlet，你需要确保在Document Outline中选择的是
        <em>
            Text View
        </em>
        ，就像你在
        <em>
            Table View
        </em>
        中做的一样。将outlet命名为
        <code>
            noteView
        </code>
        。你还需要将
        <em>
            Text View
        </em>
        的delegate设置为
        <em>
            ViewController
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/TextView.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/TextView.png"
            alt="" width="216" height="84" class="aligncenter size-full wp-image-164317">
        </a>
    </p>
    <p>
        在note view的下方，放置一个
        <em>
            Push Button
        </em>
        。将它的title改为
        <em>
            Update
        </em>
        ，并将它的frame设置为：
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            ：284
        </li>
        <li>
            <em>
                y
            </em>
            ：3
        </li>
        <li>
            <em>
                width
            </em>
            ：85
        </li>
    </ul>
    <p>
        从按钮连接一个名为
        <code>
            updateBeer
        </code>
        的动作到
        <em>
            ViewController
        </em>
        上。
    </p>
    <h3>
        添加和删除啤酒
    </h3>
    <p>
        到目前为止，你已经有了所有用来编辑和查看啤酒必须的控件。然而，现在还无法添加和删除啤酒。这将使得app很难使用，即使你的用户还没有任何要喝的酒:]
    </p>
    <p>
        添加一个
        <em>
            Gradient Button
        </em>
        到屏幕底部的左侧。在Attributes Inspector中，将
        <em>
            Image
        </em>
        改为
        <em>
            NSAddTemplate
        </em>
        。
    </p>
    <p>
        在Size Inspector中，将frame设置为：
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
            ：-1
        </li>
        <li>
            <em>
                width
            </em>
            ：24
        </li>
        <li>
            <em>
                height
            </em>
            ：20
        </li>
    </ul>
    <p>
        为新的按钮添加一个名为
        <code>
            addBeer
        </code>
        的动作。
    </p>
    <p>
        在macOS中有一件很棒的事情，是你可以访问像
        <em>
            +
        </em>
        号这样的模板图片。这样当你有任何标准动作的按钮，但没有时间或能力创建你自己的图片，就能够让你的生活变得更加的容易。
    </p>
    <p>
        接下来，你需要添加移除的按钮。直接添加另一个
        <em>
            Gradient Button
        </em>
        到前一个按钮的右边，并将
        <em>
            Image
        </em>
        改为
        <em>
            NSRemoveTemplate
        </em>
        。将它的frame设置为：
    </p>
    <ul>
        <li>
            <em>
                x
            </em>
            ：23
        </li>
        <li>
            <em>
                y
            </em>
            ：-1
        </li>
        <li>
            <em>
                width
            </em>
            ：24
        </li>
        <li>
            <em>
                height
            </em>
            ：20
        </li>
    </ul>
    <p>
        最后，为这个按钮添加一个名为
        <code>
            removeBeer
        </code>
        的动作。
    </p>
    <h3>
        完成UI
    </h3>
    <p>
        你几乎已经完成了构建UI！你只需要添加几个label让它变得更棒。
    </p>
    <p>
        添加下列的label：
    </p>
    <ul>
        <li>
            在name field的上方，添加文本为
            <em>
                Name
            </em>
            的label。
        </li>
        <li>
            在rating indicator的上方，添加文本为
            <em>
                Rating
            </em>
            的label。
        </li>
        <li>
            在notes view的上方，添加文本为
            <em>
                Notes
            </em>
            的label。
        </li>
        <li>
            在table view的下方，添加文本为
            <em>
                Beer Count:
            </em>
            的label。
        </li>
        <li>
            在beer count label的下方，添加文本为
            <em>
                0
            </em>
            beer count label
        </li>
    </ul>
    <p>
        对于上述添加的每一个label，在Attributes Inspector中，将它们的font设置为
        <em>
            Other – Label
        </em>
        ，size设置为10。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/labelFont.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/labelFont.png"
            alt="" width="196" height="285" class="aligncenter size-full wp-image-164319">
        </a>
    </p>
    <p>
        为最后一个label，创建一个名为
        <code>
            beerCountField
        </code>
        的outlet到
        <em>
            ViewController.swift
        </em>
        上。
    </p>
    <p>
        确保你的所有label看起来像是这样：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-2.png"
        alt="Final UI" width="600" height="374" class="aligncenter size-full wp-image-163220"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-2.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-2-480x299.png 480w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <p>
        点击解决
        <em>
            Auto Layout Issues
        </em>
        的按钮，并在
        <em>
            All Views in View Controller
        </em>
        的部分点击
        <em>
            Reset to Suggested Constraints
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/AutoLayout-1.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/AutoLayout-1.png"
            alt="" width="243" height="197" class="aligncenter size-full wp-image-164423">
        </a>
    </p>
    <h3>
        添加代码
    </h3>
    <p>
        好的！现在你要准备开始coding了。打开
        <em>
            ViewController.swift
        </em>
        并删除名为
        <code>
            representedObject
        </code>
        的property。在
        <code>
            viewDidLoad()
        </code>
        下面添加下列的方法：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">private</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">setFieldsEnabled</span><span class="hljs-params">(enabled: Bool)</span></span> {
  imageView.isEditable = enabled
  nameField.isEnabled = enabled
  ratingIndicator.isEnabled = enabled
  noteView.isEditable = enabled
}

<span class="hljs-keyword">private</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">updateBeerCountLabel</span><span class="hljs-params">()</span></span> {
  beerCountField.stringValue = <span class="hljs-string">"<span class="hljs-subst">\(BeerManager.sharedInstance.beers.<span class="hljs-built_in">count</span>)</span>"</span>
}
</pre>
    <p>
        这里有两个方法来帮助你控制UI：
    </p>
    <ol>
        <li>
            <code>
                setFieldsEnabled(\_:)
            </code>
            可以帮助你快速地打开或关闭使用form控件的能力。
        </li>
        <li>
            <code>
                updateBeerCountLabel()
            </code>
            帮助你快速地在
            <code>
                beerCountField
            </code>
            中设置啤酒的数量。
        </li>
    </ol>
    <p>
        在你所有的outlet下面，添加下列的property：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">var</span> selectedBeer: <span class="hljs-type">Beer</span>? {
  <span class="hljs-keyword">didSet</span> {
    <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> selectedBeer = selectedBeer <span class="hljs-keyword">else</span> {
      setFieldsEnabled(enabled: <span class="hljs-literal">false</span>)
      imageView.image = <span class="hljs-literal">nil</span>
      nameField.stringValue = <span class="hljs-string">""</span>
      ratingIndicator.integerValue = <span class="hljs-number">0</span>
      noteView.string = <span class="hljs-string">""</span>
      <span class="hljs-keyword">return</span>
    }
    setFieldsEnabled(enabled: <span class="hljs-literal">true</span>)
    imageView.image = selectedBeer.beerImage()
    nameField.stringValue = selectedBeer.name
    ratingIndicator.integerValue = selectedBeer.rating
    noteView.string = selectedBeer.note!
  }
}
</pre>
    <p>
        这个property将会跟踪从table view选中的啤酒。如果当前没有啤酒被选择，setter会负责清空所有field中的值，并禁用所有当前无法使用的UI组件。
    </p>
    <p>
        将
        <code>
            viewDidLoad()
        </code>
        替换为下列的代码：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">override</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">viewDidLoad</span><span class="hljs-params">()</span></span> {
  <span class="hljs-keyword">super</span>.viewDidLoad()
  <span class="hljs-keyword">if</span> <span class="hljs-type">BeerManager</span>.sharedInstance.beers.<span class="hljs-built_in">count</span> == <span class="hljs-number">0</span> {
    setFieldsEnabled(enabled: <span class="hljs-literal">false</span>)
  } <span class="hljs-keyword">else</span> {
    tableView.selectRowIndexes(<span class="hljs-type">IndexSet</span>(integer: <span class="hljs-number">0</span>), byExtendingSelection: <span class="hljs-literal">false</span>)
  }
  updateBeerCountLabel()
}
</pre>
    <p>
        就像在iOS中一样，你希望在一启动的时候去做一些事情。然而，在macOS的版本中，你需要一上来就将form填充好，以便用户能够及时看到他们的数据。
    </p>
    <h3>
        添加数据到Table View上
    </h3>
    <p>
        现在table view还不可以实际地展示任何数据，但
        <code>
            selectRowIndexes(\_:byExtendingSelection:)
        </code>
        会选中列表中的第一瓶啤酒。delegate中的代码将会为你处理剩余的事情。
    </p>
    <p>
        为了让table view去展示你的啤酒列表，添加下列的代码到
        <em>
            ViewController.swift
        </em>
        尾部，要在
        <code>
            ViewController
        </code>
        类之外：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">ViewController</span>: <span class="hljs-title">NSTableViewDataSource</span> </span>{
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">numberOfRows</span><span class="hljs-params">(<span class="hljs-keyword">in</span> tableView: NSTableView)</span></span> -&gt; <span class="hljs-type">Int</span> {
    <span class="hljs-keyword">return</span> <span class="hljs-type">BeerManager</span>.sharedInstance.beers.<span class="hljs-built_in">count</span>
  }
}

<span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">ViewController</span>: <span class="hljs-title">NSTableViewDelegate</span> </span>{
  <span class="hljs-comment">// MARK: - CellIdentifiers</span>
  <span class="hljs-keyword">fileprivate</span> <span class="hljs-class"><span class="hljs-keyword">enum</span> <span class="hljs-title">CellIdentifier</span> </span>{
    <span class="hljs-keyword">static</span> <span class="hljs-keyword">let</span> <span class="hljs-type">NameCell</span> = <span class="hljs-string">"NameCell"</span>
  }

  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">tableView</span><span class="hljs-params">(<span class="hljs-number">_</span> tableView: NSTableView, viewFor tableColumn: NSTableColumn?, row: Int)</span></span> -&gt; <span class="hljs-type">NSView</span>? {

    <span class="hljs-keyword">let</span> beer = <span class="hljs-type">BeerManager</span>.sharedInstance.beers[row]

    <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> cell = tableView.makeView(withIdentifier: <span class="hljs-type">NSUserInterfaceItemIdentifier</span>(rawValue: <span class="hljs-type">CellIdentifier</span>.<span class="hljs-type">NameCell</span>), owner: <span class="hljs-literal">nil</span>) <span class="hljs-keyword">as</span>? <span class="hljs-type">NSTableCellView</span> {
      cell.textField?.stringValue = beer.name
      <span class="hljs-keyword">if</span> beer.name.characters.<span class="hljs-built_in">count</span> == <span class="hljs-number">0</span> {
        cell.textField?.stringValue = <span class="hljs-string">"New Beer"</span>
      }
      <span class="hljs-keyword">return</span> cell
    }
    <span class="hljs-keyword">return</span> <span class="hljs-literal">nil</span>
  }

  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">tableViewSelectionDidChange</span><span class="hljs-params">(<span class="hljs-number">_</span> notification: Notification)</span></span> {
    <span class="hljs-keyword">if</span> tableView.selectedRow &gt;= <span class="hljs-number">0</span> {
      selectedBeer = <span class="hljs-type">BeerManager</span>.sharedInstance.beers[tableView.selectedRow]
    }
  }

}
</pre>
    <p>
        上述代码负责用来自data source的数据填充table view中的行。
    </p>
    <p>
        仔细地看一下它，你会发现它和iOS中相应的部分
        <em>
            BeersTableViewController.swift
        </em>
        并没有太大的差别。一个值得注意的区别是，当table view选择的行发生变化时，NSTableView会发送一个
        <em>
            Notification
        </em>
        到
        <em>
            NSTableViewDelegate
        </em>
        上。
    </p>
    <p>
        记住，你的新macOS app现在有了多个的输入源 - 不仅仅依靠一根手指来操作。使用鼠标或键盘都可以改变table view的选择，这导致处理这些改变时，将和iOS有一点点不同。
    </p>
    <p>
        现在添加一个啤酒。将
        <code>
            addBeer()
        </code>
        修改为：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">addBeer</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: Any)</span></span> {
  <span class="hljs-comment">// 1.</span>
  <span class="hljs-keyword">let</span> beer = <span class="hljs-type">Beer</span>()
  beer.name = <span class="hljs-string">""</span>
  beer.rating = <span class="hljs-number">1</span>
  beer.note = <span class="hljs-string">""</span>
  selectedBeer = beer

  <span class="hljs-comment">// 2.</span>
  <span class="hljs-type">BeerManager</span>.sharedInstance.beers.insert(beer, at: <span class="hljs-number">0</span>)
  <span class="hljs-type">BeerManager</span>.sharedInstance.saveBeers()

  <span class="hljs-comment">// 3.</span>
  <span class="hljs-keyword">let</span> indexSet = <span class="hljs-type">IndexSet</span>(integer: <span class="hljs-number">0</span>)
  tableView.beginUpdates()
  tableView.insertRows(at: indexSet, withAnimation: .slideDown)
  tableView.endUpdates()
  updateBeerCountLabel()

  <span class="hljs-comment">// 4.</span>
  tableView.selectRowIndexes(<span class="hljs-type">IndexSet</span>(integer: <span class="hljs-number">0</span>), byExtendingSelection: <span class="hljs-literal">false</span>)
}
</pre>
    <p>
        这里没有太多累赘的东西。你只需去完成下列的事情：
    </p>
    <ol>
        <li>
            创建一个新的啤酒。
        </li>
        <li>
            将啤酒插入到model中。
        </li>
        <li>
            为table插入一个新的行。
        </li>
        <li>
            选择新啤酒所在的这行。
        </li>
    </ol>
    <p>
        你货主注意到了这点，就像在iOS中一样，你需要在插入新的行之前调用
        <code>
            beginUpdates()
        </code>
        和
        <code>
            endUpdates()
        </code>
        。所以说，你其实早已懂得了关于macOS的很多的内容！
    </p>
    <h3>
        移除条目
    </h3>
    <p>
        为了移除一瓶啤酒，添加下列的代码到
        <code>
            removeBeer(\_:)
        </code>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">removeBeer</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: Any)</span></span> {
  <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> beer = selectedBeer,
    <span class="hljs-keyword">let</span> index = <span class="hljs-type">BeerManager</span>.sharedInstance.beers.index(of: beer) <span class="hljs-keyword">else</span> {
      <span class="hljs-keyword">return</span>
  }

  <span class="hljs-comment">// 1.</span>
  <span class="hljs-type">BeerManager</span>.sharedInstance.beers.remove(at: index)
  <span class="hljs-type">BeerManager</span>.sharedInstance.saveBeers()

  <span class="hljs-comment">// 2</span>
  tableView.reloadData()
  updateBeerCountLabel()
  tableView.selectRowIndexes(<span class="hljs-type">IndexSet</span>(integer: <span class="hljs-number">0</span>), byExtendingSelection: <span class="hljs-literal">false</span>)
  <span class="hljs-keyword">if</span> <span class="hljs-type">BeerManager</span>.sharedInstance.beers.<span class="hljs-built_in">count</span> == <span class="hljs-number">0</span> {
    selectedBeer = <span class="hljs-literal">nil</span>
  }
}
</pre>
    <p>
        依然是非常直接的代码：
    </p>
    <ol>
        <li>
            如果已选中一个啤酒，就从model中移除它。
        </li>
        <li>
            重载table view，选择第一瓶可用的啤酒。
        </li>
    </ol>
    <h3>
        处理图片
    </h3>
    <p>
        记得
        <em>
            Image Wells
        </em>
        拥有接收拖拽到它上面的图片的能力么？将
        <code>
            imageChanged(\_:)
        </code>
        的方法修改为：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">imageChanged</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: NSImageView)</span></span> {
  <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> image = sender.image <span class="hljs-keyword">else</span> { <span class="hljs-keyword">return</span> }
  selectedBeer?.saveImage(image)
}
</pre>
    <p>
        你以为这可能会很难！但苹果早已为你负责处理了所有繁重的工作，并将接收拖拽来的图片的能力赐予了你。
    </p>
    <p>
        但另一方面，你需要做很多工作，来方便用户从你的app中选取图片。将
        <code>
            selectImage()
        </code>
        方法替换为：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">selectImage</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: Any)</span></span> {
  <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> window = view.window <span class="hljs-keyword">else</span> { <span class="hljs-keyword">return</span> }
  <span class="hljs-comment">// 1.</span>
  <span class="hljs-keyword">let</span> openPanel = <span class="hljs-type">NSOpenPanel</span>()
  openPanel.allowsMultipleSelection = <span class="hljs-literal">false</span>
  openPanel.canChooseDirectories = <span class="hljs-literal">false</span>
  openPanel.canCreateDirectories = <span class="hljs-literal">false</span>
  openPanel.canChooseFiles = <span class="hljs-literal">true</span>

  <span class="hljs-comment">// 2.</span>
  openPanel.allowedFileTypes = [<span class="hljs-string">"jpg"</span>, <span class="hljs-string">"png"</span>, <span class="hljs-string">"tiff"</span>]

  <span class="hljs-comment">// 3.</span>
  openPanel.beginSheetModal(<span class="hljs-keyword">for</span>: window) { (result) <span class="hljs-keyword">in</span>
    <span class="hljs-keyword">if</span> result == <span class="hljs-type">NSApplication</span>.<span class="hljs-type">ModalResponse</span>.<span class="hljs-type">OK</span> {
      <span class="hljs-comment">// 4.</span>
      <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> panelURL = openPanel.url,
        <span class="hljs-keyword">let</span> beerImage = <span class="hljs-type">NSImage</span>(contentsOf: panelURL) {
        <span class="hljs-keyword">self</span>.selectedBeer?.saveImage(beerImage)
        <span class="hljs-keyword">self</span>.imageView.image = beerImage
      }
    }
  }
}
</pre>
    <p>
        上述代码实现了你使用
        <code>
            NSOpenPanel
        </code>
        来选取一个文件的过程。以下是详细步骤：
    </p>
    <ol>
        <li>
            创建一个
            <code>
                NSOpenPanel
            </code>
            ，并配置它的设置。
        </li>
        <li>
            为了让用户只可以选择图片，你将允许的文件类型设置为你所需的文件格式。
        </li>
        <li>
            展示这个sheet给用户。
        </li>
        <li>
            如果用户选择了一张图片的话，保存它。
        </li>
    </ol>
    <p>
        最后，在
        <code>
            updateBeer(\_:)
        </code>
        中添加保存数据model的代码：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">updateBeer</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: Any)</span></span> {
  <span class="hljs-comment">// 1.</span>
  <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> beer = selectedBeer,
    <span class="hljs-keyword">let</span> index = <span class="hljs-type">BeerManager</span>.sharedInstance.beers.index(of: beer) <span class="hljs-keyword">else</span> { <span class="hljs-keyword">return</span> }
  beer.name = nameField.stringValue
  beer.rating = ratingIndicator.integerValue
  beer.note = noteView.string

  <span class="hljs-comment">// 2.</span>
  <span class="hljs-keyword">let</span> indexSet = <span class="hljs-type">IndexSet</span>(integer: index)
  tableView.beginUpdates()
  tableView.reloadData(forRowIndexes: indexSet, columnIndexes: <span class="hljs-type">IndexSet</span>(integer: <span class="hljs-number">0</span>))
  tableView.endUpdates()

  <span class="hljs-comment">// 3.</span>
  <span class="hljs-type">BeerManager</span>.sharedInstance.saveBeers()
}
</pre>
    <p>
        上述代码：
    </p>
    <ol>
        <li>
            确认啤酒是存在的，并更新它的property。
        </li>
        <li>
            更新table view以在table上反映任何名称的变化。
        </li>
        <li>
            保存数据到磁盘上。
        </li>
    </ol>
    <p>
        你已经全部设定完毕！运行app，然后添加啤酒。记住你需要选择
        <em>
            Update
        </em>
        来更新你的数据。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-Beers.png"
        alt="Final UI with some beers added." width="600" height="374" class="aligncenter size-full wp-image-163221"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-Beers.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-mac-UI-Beers-480x299.png 480w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <h3>
        最后的接触
    </h3>
    <p>
        你已经学到了大量关于iOS和macOS开发的不同之处。但这里还有一个你需要熟悉的概念：
        <em>
            Settings/Preferences
        </em>
        。在iOS中，你可能已经习惯了前往Setting，找到你的app，然后修改你可用的设置。在macOS中，这些却需要你在app内部的
        <em>
            Preferences
        </em>
        中来完成。
    </p>
    <p>
        运行
        <em>
            BeerTracker
        </em>
        target，在模拟器中的Settings app中找到BeerTracker的设置。这里你会发现一个让用户限制他的笔记长度的设置，以避免他们日后会进行投诉。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTrackerSettings-282x500.png"
        alt="Settings - iOS" width="282" height="500" class="aligncenter size-large wp-image-162952"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTrackerSettings-282x500.png 282w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTrackerSettings-180x320.png 180w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTrackerSettings.png 640w"
        sizes="(max-width: 282px) 100vw, 282px">
    </p>
    <p>
        为了在你的mac app中获得相同的特性，你要为你的用户创建一个Preferences窗口。在
        <em>
            BeerTracker-mac
        </em>
        中，打开
        <em>
            Main.storyboard
        </em>
        ，并拖拽一个新的
        <em>
            Window Controller
        </em>
        。选择这个
        <em>
            Window
        </em>
        ，打开Size Inspector，并进行如下的修改：
    </p>
    <ol>
        <li>
            将
            <em>
                Content Size
            </em>
            的width设置为380，height设置为55。
        </li>
        <li>
            在
            <em>
                Minimum Content Size
            </em>
            中，将width设置为380，height设置为55。
        </li>
        <li>
            在
            <em>
                Maximum Content Size
            </em>
            中，将width设置为380，height设置为55。
        </li>
        <li>
            在
            <em>
                Full Screen Minimum Content Size
            </em>
            中，将width设置为380，height设置为55。
        </li>
        <li>
            在
            <em>
                Full Screen Maximum Content Size
            </em>
            中，将width设置为380，height设置为55。
        </li>
        <li>
            在
            <em>
                Initial Position
            </em>
            中，选择
            <em>
                Center Horizontally
            </em>
            和
            <em>
                Center Vertically
            </em>
            。
        </li>
    </ol>
    <p>
        接下来，选择这个空空的View Controller的view，然后将它的size修改至和上面设置中相匹配的380 x 55。
    </p>
    <p>
        以上操作可以让你的Preferences窗口始终保持在相同的尺寸下，以在合乎逻辑的位置打开给用户。当你完成之后，你的新窗口看起来在storyboard中像这个样子：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-Preferences-Window-1.png"
        alt="Preferences - Mac" width="700" height="477" class="aligncenter size-full wp-image-163222"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-Preferences-Window-1.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-Preferences-Window-1-470x320.png 470w, https://koenig-media.raywenderlich.com/uploads/2017/05/BeerTracker-Preferences-Window-1-650x443.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        现在，用户还没有办法来打开你的新窗口。由于它应当被绑定到
        <em>
            Preferences
        </em>
        的菜单项上，因此要在storyboard中找到菜单栏场景。你可以把它拖动到靠近Preferences窗口的地方，这样以下部分的操作就可以方便一些。当它足够接近之后，执行如下的操作：
    </p>
    <ol>
        <li>
            在storyboard的菜单栏中，点击
            <em>
                BeerTracker-mac
            </em>
            来打开菜单。
        </li>
        <li>    
            将
            <em>
                Preferences
            </em>
            菜单项
            <em>
                拖拽
            </em>
            到新Window Controller上
        </li>
        <li>
            在弹出的对话框中选择
            <em>
                Show
            </em>
        </li>
    </ol>
    <p>
        添加一个
        <em>
            Check Box Button
        </em>
        到空空的View Controller上。将它的text修改为
        <em>
            Restrict Note Length to 1,024 Characters
        </em>
        。
    </p>
    <p>
        选中
        <em>
            Checkbox Button
        </em>
        后，打开Bindings Inspector，执行下列的操作：
    </p>
    <ol>
        <li>
            展开
            <em>
                Value
            </em>
            ，并勾选
            <em>
                Bind to
            </em>
            。
        </li>
        <li>
            在弹出的菜单中选择
            <em>
                Shared User Defaults Controller
            </em>
            。
        </li>
        <li>
            在
            <em>
                Model Key Path
            </em>
            中，输入
            <em>
                BT_Restrict_Note_Length
            </em>
            。
        </li>
    </ol>
    <p>
        在
        <em>
            Utilities
        </em>
        组中创建一个新的名为
        <em>
            StringValidator.swift
        </em>
        的Swift文件。确定为这个文件同时勾选两个target。
    </p>
    <p>
        打开
        <em>
            StringValidator.swift
        </em>
        ，并使用下列的代码来替换其中的内容：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">import</span> Foundation

<span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">String</span> </span>{
  <span class="hljs-keyword">private</span> <span class="hljs-keyword">static</span> <span class="hljs-keyword">let</span> noteLimit = <span class="hljs-number">1024</span>

  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">isValidLength</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">Bool</span> {
    <span class="hljs-keyword">let</span> limitLength = <span class="hljs-type">UserDefaults</span>.standard.bool(forKey: <span class="hljs-string">"BT_Restrict_Note_Length"</span>)
    <span class="hljs-keyword">if</span> limitLength {
      <span class="hljs-keyword">return</span> <span class="hljs-keyword">self</span>.characters.<span class="hljs-built_in">count</span> &lt;= <span class="hljs-type">String</span>.noteLimit
    }
    <span class="hljs-keyword">return</span> <span class="hljs-literal">true</span>
  }
}
</pre>
    <p>
        这个类为两个target提供了检查一个字符串的长度是否合法的能力，只要用户默认的
        <em>
            BT_Restrict_Note_Length
        </em>
        值为true。
    </p>
    <p>
        在
        <em>
            ViewController.swift
        </em>
        中添加下列的代码到文件的尾部：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">ViewController</span>: <span class="hljs-title">NSTextViewDelegate</span> </span>{
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">textView</span><span class="hljs-params">(<span class="hljs-number">_</span> textView: NSTextView, shouldChangeTextIn affectedCharRange: NSRange, replacementString: String?)</span></span> -&gt; <span class="hljs-type">Bool</span> {
    <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> replacementString = replacementString <span class="hljs-keyword">else</span> { <span class="hljs-keyword">return</span> <span class="hljs-literal">true</span> }
    <span class="hljs-keyword">let</span> currentText = textView.string
    <span class="hljs-keyword">let</span> proposed = (currentText <span class="hljs-keyword">as</span> <span class="hljs-type">NSString</span>).replacingCharacters(<span class="hljs-keyword">in</span>: affectedCharRange, with: replacementString)
    <span class="hljs-keyword">return</span> proposed.isValidLength()
  }
}
</pre>
    <p>
        最后，在
        <em>
            Main.storyboard
        </em>
        中改变每个
        <em>
            Window
        </em>
        的名称已匹配他们的目标，让用户更加的清晰。选择initial的
        <em>
            Window Controller
        </em>
        ，并在
        <em>
            Attributes Inspector
        </em>
        中将它的title改为
        <em>
            BeerTracker
        </em>
        。从Preferences窗口中选择
        <em>
            Window Controller
        </em>
        ，并将它的title修改为
        <em>
            Preferences
        </em>
        。
    </p>
    <p>
        运行你的app。选择Preferences菜单项，现在你应当能够看到带有偏好项的新Preferences窗口了。勾选这里，然后找到一些较长的文本来粘贴到
        <em>
            Text View
        </em>
        中，如果超过了1024个字符的话，就无法做到，就像在iOS app中一样。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/06/Screen-Shot-2017-06-12-at-6.31.32-PM.png"
        alt="Build and Run with Preferences" width="484" height="297" class="alignnone size-full wp-image-164558"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/06/Screen-Shot-2017-06-12-at-6.31.32-PM.png 484w, https://koenig-media.raywenderlich.com/uploads/2017/06/Screen-Shot-2017-06-12-at-6.31.32-PM-480x295.png 480w"
        sizes="(max-width: 484px) 100vw, 484px">
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
        你可以从
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/06/BeerTracker-Port_Finished-2.zip"
        sl-processed="1">
            这里
        </a>
        下载最终完成的项目。
    </p>
    <p>
        在本教程中，你已学到了：
    </p>
    <ul>
        <li>
            如何将一个现有的iOS项目迁移到macOS上去。
        </li>
        <li>
            如何根据你的平台所需来拆分代码。
        </li>
        <li>
            如何在项目之间复用已存在的代码。
        </li>
        <li>
            Xcode在两个平台上的一些不同的表现。
        </li>
    </ul>
    <p>
        关于更多移植的你的app到macOS中的内容，请访问
        <a href="https://developer.apple.com/library/content/documentation/MacOSX/Conceptual/OSX_Technology_Overview/MigratingFromCocoaTouch/MigratingFromCocoaTouch.html"
        sl-processed="1">
            Apple's Migrating from Cocoa Touch Overview
        </a>
        。
    </p>
</div>