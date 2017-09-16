# macOS教程：Core Graphics

#### [原文地址](https://www.raywenderlich.com/128614/core-graphics-os-x-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div class="note">
        <p>
            <em>
                更新于2016年9月22日：
            </em>
            本教程已更新以适配Xcode 8及Swift 3。
        </p>
    </div>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature-250x250.png"
        alt="OSXCoreGraphics-feature" width="250" height="250" class="alignright size-thumbnail wp-image-135093 bordered"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
        你一定见到过很多app带有美丽的图形和时髦的view。它们会带给你深刻的影响，因为它们是
        <i>
            so
            如此
        </i>
        得漂亮。
    </p>
    <p>
        <em>
            Core Graphics
        </em>
        是苹果的2D绘制引擎，它是macOS和iOS中最酷的框架之一。它能够绘制任何你可以想象到的东西，从最简单的形状，文本，到最复杂的视觉效果，包括阴影，渐变效果等。
    </p>
    <p>
        在这篇macOS的Core Graphics教程中，你将会创建一个名为
        <em>
            DiskInfo
        </em>
        的app，在其中包含一个可以展示某硬盘可用空间及文件分布的view。这将是一个很好的例子，来说明如何使用Core Graphics来讲一个枯燥无味，基于文本的界面变得漂亮起来：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/graphview.png"
        rel="attachment wp-att-128931">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/graphview-480x166.png"
            alt="Disc information drawn with Core Graphics" width="480" height="166"
            class="aligncenter size-medium wp-image-128931" srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/graphview-480x166.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/graphview.png 695w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        跟随教程你可以了解到如何：
    </p>
    <ul>
        <li>
            创建及配置一个标准的view，它是任何图形元素的基础的层
        </li>
        <li>
            实现实时的渲染，这样你就不必每次改变图形的时候，都重新运行项目了
        </li>
        <li>
            通过使用路径、填充、裁切及文本，来用代码进行绘制
        </li>
        <li>
            使用
            <em>
                Cocoa Drawing
            </em>
            ，一个可以在
            <em>
                AppKit
            </em>
            的app下可用的工具，它给出了更高层级的类和方法
        </li>
    </ul>
    <p>
        在本教程的第一部分，你将使用Core Graphics来实现条状的图表，之后再来学习如何使用Cocoa Drawing来绘制饼状图。
    </p>
    <p>
        所以戴上你的画家帽子，开始学习如何绘制你的世界吧。
    </p>
    <h2>
        入门
    </h2>
    <p>
        首先，从
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/06/DiskInfo-Starter.zip">
            here
            这里
        </a>
        下载DiskInfo的初始项目。运行它。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-diskinfo-build-run1.png"
        rel="attachment wp-att-128902">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-diskinfo-build-run1-480x259.png"
            alt="Original view without any Core Graphics drawing" width="480" height="259"
            class="aligncenter size-medium wp-image-128902" srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-diskinfo-build-run1-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-diskinfo-build-run1-768x414.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-diskinfo-build-run1-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-diskinfo-build-run1.png 1258w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        这个app列出了你全部的硬盘，当你点击其中一个的时候，详细的信息就会被展示出来。
    </p>
    <p>
        在继续下一步之前，查看一下项目的结构，来熟悉代码的分布：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-starterproject-structure-xcode-edit.png"
        rel="attachment wp-att-129857">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-starterproject-structure-xcode-edit-312x500.png"
            alt="sshot-starterproject-structure-xcode-edit" width="312" height="500"
            class="aligncenter size-large wp-image-129857" srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-starterproject-structure-xcode-edit-312x500.png 312w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-starterproject-structure-xcode-edit-200x320.png 200w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-starterproject-structure-xcode-edit.png 537w"
            sizes="(max-width: 312px) 100vw, 312px">
        </a>
    </p>
    <p>
        需要进行一下指导？
    </p>
    <ul>
        <li>
            <em>
                ViewController.swift
            </em>
            ：app的主view controller
        </li>
        <li>
            <em>
                VolumeInfo.swift
            </em>
            ：包含了
            <code>
                VolumeInfo
            </code>
            类的实现，它可以从硬盘中读取信息，而
            <code>
                FilesDistribution
            </code>
            结构体则用来处理文件类型间的拆分
        </li>
        <li>
            <em>
                NSColor+DiskInfo.swift
            </em>
            和
            <em>
                NSFont+DiskInfo.swift
            </em>
            ：extension，定义了默认颜色和字体常量
        </li>
        <li>
            <em>
                CGFloat+Radians.swift
            </em>
            ：extension提供了助手方法，以便在角度和弧度之间转换
        </li>
        <li>
            <em>
                MountedVolumesDataSource.swift
            </em>
            和
            <em>
                MountedVolumesDelegate.swift
            </em>
            ：实现了要求的方法，在outline
            view中展示硬盘的信息
        </li>
    </ul>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            这个app展示了正确的硬盘使用信息，但由于教程本身的原因，它只是提供了随机的文件分布。
        </p>
        <p>
            在每次运行app时，计算真实的文件分布，这将耗尽所有的时间，破坏你的乐趣，没有人想要这样。
        </p>
    </div>
    <h2>
        创建自定义的view
    </h2>
    <p>
        你要做的第一件事是创建一个自定义的view，名为
        <code>
            GraphView
        </code>
        。你将在这里绘制饼状和条状的图表，因此它相当得重要。
    </p>
    <p>
        你需要完成两个目标来创建自定义的view：
    </p>
    <ol>
        <li>
            创建一个
            <code>
                NSView
            </code>
            的子类。
        </li>
        <li>
            重写
            <code>
                draw(\_:)
            </code>
            ，添加一些绘制的代码。
        </li>
    </ol>
    <p>
        在一个较高的层面看，它就是如此得容易。继续下列的步骤来了解如何实现这点。
    </p>
    <h3>
        创建NSView的子类
    </h3>
    <p>
        在Project Navigator中选择
        <em>
            Views
        </em>
        组。依次选择
        <em>
            File \ New \ File…
        </em>
        ，并选择
        <em>
            macOS \ Source \ Cocoa Class
        </em>
        文件模板。
    </p>
    <p>
        点击
        <em>
            Next
        </em>
        ，并在确认界面中，将新的类命名为
        <code>
            GraphView
        </code>
        ，并将其作为
        <code>
            NSView
        </code>
        的子类，并确保语言为
        <em>
            Swift
        </em>
        。
    </p>
    <p>
        点击
        <em>
            Next
        </em>
        来
        <em>
            创建
        </em>
        并保存你的新文件。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        ，并找到
        <em>
            View Controller
        </em>
        场景。从
        <em>
            Objects Inspector
        </em>
        中拖拽一个
        <em>
            Custom View
        </em>
        到它上面，就像下面这样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-drag-customview.png"
        rel="attachment wp-att-128905">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-drag-customview-700x236.png"
            alt="sshot-drag-customview" width="700" height="236" class="aligncenter size-large wp-image-128905"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-drag-customview-700x236.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-drag-customview-480x162.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-drag-customview-768x259.png 768w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        选择这个view，并在
        <em>
            Identity Inspector
        </em>
        中。将类名设置为
        <code>
            GraphView
        </code>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-attrinspector-change-class.png"
        rel="attachment wp-att-128907">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-attrinspector-change-class-480x189.png"
            alt="sshot-attrinspector-change-class" width="350" height="138" class="aligncenter size-medium wp-image-128907"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-attrinspector-change-class-480x189.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-attrinspector-change-class.png 512w"
            sizes="(max-width: 350px) 100vw, 350px">
        </a>
    </p>
    <p>
        现在你需要一些约束来进行布局，所以选中这个view，在自动布局工具栏中点击
        <em>
            Pin
        </em>
        按钮。在弹出的面板中，将
        <em>
            Top
        </em>
        ，
        <em>
            Bottom
        </em>
        ，
        <em>
            Leading
        </em>
        和
        <em>
            Trailing
        </em>
        约束都设置为0，然后点击
        <em>
            Add 4 Constraints
        </em>
        按钮。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-addconstraints-trim.png"
        rel="attachment wp-att-129849">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-addconstraints-trim-220x320.png"
            alt="sshot-addconstraints-trim" width="220" height="320" class="aligncenter size-medium wp-image-129849"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-addconstraints-trim-220x320.png 220w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-addconstraints-trim-344x500.png 344w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-addconstraints-trim.png 527w"
            sizes="(max-width: 220px) 100vw, 220px">
        </a>
    </p>
    <p>
        点击自动布局工具栏中三角形的
        <em>
            Resolve Auto Layout Issues
        </em>
        按钮，在
        <em>
            Selected Views
        </em>
        部分中，点击
        <em>
            Update Frames
        </em>
        - 它现在看起来是被禁用的，所以点击其它任意地方来取消选择GraphView，然后在重新选择它。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-updateframes-2-trim.png"
        rel="attachment wp-att-129852">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-updateframes-2-trim-375x320.png"
            alt="sshot-updateframes-2-trim" width="375" height="320" class="aligncenter size-medium wp-image-129852"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-updateframes-2-trim-375x320.png 375w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-updateframes-2-trim-586x500.png 586w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-updateframes-2-trim.png 590w"
            sizes="(max-width: 375px) 100vw, 375px">
        </a>
    </p>
    <h3>
        重写draw(\_:)
    </h3>
    <p>
        打开
        <em>
            GraphView.swift
        </em>
        。你将看到
        <em>
            Xcode
        </em>
        已创建了
        <code>
            draw(\_:)
        </code>
        的默认的实现。将其中的注释替换为下列的代码，并确保你保留着对父类方法的调用：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-type">NSColor</span>.white.setFill()
<span class="hljs-type">NSRectFill</span>(bounds)
</pre>
    <p>
        首先你将填充颜色设置为白色，然后调用
        <code>
            NSRectFill
        </code>
        方法来填充这个view的背景。
    </p>
    <p>
        运行项目。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-whitecolor.png"
        rel="attachment wp-att-128910">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-whitecolor-700x377.png"
            alt="sshot-build-run-whitecolor" width="450" height="242" class="aligncenter size-medium wp-image-128910"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-whitecolor-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-whitecolor-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-whitecolor-768x414.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-whitecolor.png 1258w"
            sizes="(max-width: 450px) 100vw, 450px">
        </a>
    </p>
    <p>
        你自定义的view的背景现在已由标准灰变为了白色。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/first-custom-view.png"
        rel="attachment wp-att-128963">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/first-custom-view-289x320.png"
            alt="first-custom-view" width="289" height="320" class="aligncenter size-medium wp-image-128963"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/first-custom-view-289x320.png 289w, https://koenig-media.raywenderlich.com/uploads/2016/03/first-custom-view-452x500.png 452w, https://koenig-media.raywenderlich.com/uploads/2016/03/first-custom-view.png 606w"
            sizes="(max-width: 289px) 100vw, 289px">
        </a>
    </p>
    <p>
        是的，创建自定义绘制的view就是如此的容易。
    </p>
    <h2>
        实时渲染：@IBDesignable 和 @IBInspectable
    </h2>
    <p>
        Xcode 6引入了一个令人震惊的特性：实时渲染。它让你可以在Interface Builder中查看你自定义view的样子 - 无需运行项目。
    </p>
    <p>
        要打开这个特性，你只需在你的类中添加
        <code>
            @IBDesignable
        </code>
        标注，且可选择的，你可以实现
        <code>
            prepareForInterfaceBuilder()
        </code>
        方法来提供一些样本的数据。
    </p>
    <p>
        打开
        <em>
            GraphView.swift
        </em>
        ，并在类的声明前添加下列的代码：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@IBDesignable</span>
</pre>
    <p>
        现在，你需要提供一些样本数据。在
        <code>
            GraphView
        </code>
        类中添加下列代码：
    </p>
    <pre lang="swift" class="language-swift hljs">  
<span class="hljs-keyword">var</span> fileDistribution: <span class="hljs-type">FilesDistribution</span>? {
  <span class="hljs-keyword">didSet</span> {
    needsDisplay = <span class="hljs-literal">true</span>
  }
}

<span class="hljs-keyword">override</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">prepareForInterfaceBuilder</span><span class="hljs-params">()</span></span> {
  <span class="hljs-keyword">let</span> used = <span class="hljs-type">Int64</span>(<span class="hljs-number">100000000000</span>)
  <span class="hljs-keyword">let</span> available = used / <span class="hljs-number">3</span>
  <span class="hljs-keyword">let</span> filesBytes = used / <span class="hljs-number">5</span>
  <span class="hljs-keyword">let</span> distribution: [<span class="hljs-type">FileType</span>] = [
    .apps(bytes: filesBytes / <span class="hljs-number">2</span>, percent: <span class="hljs-number">0.1</span>),
    .photos(bytes: filesBytes, percent: <span class="hljs-number">0.2</span>),
    .movies(bytes: filesBytes * <span class="hljs-number">2</span>, percent: <span class="hljs-number">0.15</span>),
    .audio(bytes: filesBytes, percent: <span class="hljs-number">0.18</span>),
    .other(bytes: filesBytes, percent: <span class="hljs-number">0.2</span>)
  ]
  fileDistribution = <span class="hljs-type">FilesDistribution</span>(capacity: used + available,
                                       available: available,
                                       distribution: distribution)
}
</pre>
    <p>
        这定义了
        <code>
            fileDistribution
        </code>
        属性，用来储存硬盘信息。当这个property发生变化的时候，就将这个view的
        <code>
            needsDisplay
        </code>
        property设置为
        <em>
            true
        </em>
        ，来强制这个view重新绘制它的内容。
    </p>
    <p>
        然后实现
        <code>
            prepareForInterfaceBuilder()
        </code>
        方法来创建一个样本的文件分布，Xcode就会用它来渲染这个view。
    </p>
    <div class="note">
        <p>
            <em>
                注意
            </em>
            ：你也可以在Interface Builder中实时地改变你自定义view的可视的属性。你只需添加
            <code>
                @IBInspectable
            </code>
            这个标注到这个property上。
        </p>
    </div>
    <p>
        接下来：让这个view中所有的可视的property标注@IBInspectable。在
        <code>
            GraphView
        </code>
        的实现中添加下列的代码：
    </p>
    <pre lang="swift" class="language-swift hljs">  
<span class="hljs-comment">// 1</span>
<span class="hljs-keyword">fileprivate</span> <span class="hljs-class"><span class="hljs-keyword">struct</span> <span class="hljs-title">Constants</span> </span>{
  <span class="hljs-keyword">static</span> <span class="hljs-keyword">let</span> barHeight: <span class="hljs-type">CGFloat</span> = <span class="hljs-number">30.0</span>
  <span class="hljs-keyword">static</span> <span class="hljs-keyword">let</span> barMinHeight: <span class="hljs-type">CGFloat</span> = <span class="hljs-number">20.0</span>
  <span class="hljs-keyword">static</span> <span class="hljs-keyword">let</span> barMaxHeight: <span class="hljs-type">CGFloat</span> = <span class="hljs-number">40.0</span>
  <span class="hljs-keyword">static</span> <span class="hljs-keyword">let</span> marginSize: <span class="hljs-type">CGFloat</span> = <span class="hljs-number">20.0</span>
  <span class="hljs-keyword">static</span> <span class="hljs-keyword">let</span> pieChartWidthPercentage: <span class="hljs-type">CGFloat</span> = <span class="hljs-number">1.0</span> / <span class="hljs-number">3.0</span>
  <span class="hljs-keyword">static</span> <span class="hljs-keyword">let</span> pieChartBorderWidth: <span class="hljs-type">CGFloat</span> = <span class="hljs-number">1.0</span>
  <span class="hljs-keyword">static</span> <span class="hljs-keyword">let</span> pieChartMinRadius: <span class="hljs-type">CGFloat</span> = <span class="hljs-number">30.0</span>
  <span class="hljs-keyword">static</span> <span class="hljs-keyword">let</span> pieChartGradientAngle: <span class="hljs-type">CGFloat</span> = <span class="hljs-number">90.0</span>
  <span class="hljs-keyword">static</span> <span class="hljs-keyword">let</span> barChartCornerRadius: <span class="hljs-type">CGFloat</span> = <span class="hljs-number">4.0</span>
  <span class="hljs-keyword">static</span> <span class="hljs-keyword">let</span> barChartLegendSquareSize: <span class="hljs-type">CGFloat</span> = <span class="hljs-number">8.0</span>
  <span class="hljs-keyword">static</span> <span class="hljs-keyword">let</span> legendTextMargin: <span class="hljs-type">CGFloat</span> = <span class="hljs-number">5.0</span>
}

<span class="hljs-comment">// 2</span>
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> barHeight: <span class="hljs-type">CGFloat</span> = <span class="hljs-type">Constants</span>.barHeight {
  <span class="hljs-keyword">didSet</span> {
    barHeight = <span class="hljs-built_in">max</span>(<span class="hljs-built_in">min</span>(barHeight, <span class="hljs-type">Constants</span>.barMaxHeight), <span class="hljs-type">Constants</span>.barMinHeight)
  }
}
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> pieChartUsedLineColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.pieChartUsedStrokeColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> pieChartAvailableLineColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.pieChartAvailableStrokeColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> pieChartAvailableFillColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.pieChartAvailableFillColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> pieChartGradientStartColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.pieChartGradientStartColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> pieChartGradientEndColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.pieChartGradientEndColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> barChartAvailableLineColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.availableStrokeColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> barChartAvailableFillColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.availableFillColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> barChartAppsLineColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.appsStrokeColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> barChartAppsFillColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.appsFillColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> barChartMoviesLineColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.moviesStrokeColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> barChartMoviesFillColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.moviesFillColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> barChartPhotosLineColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.photosStrokeColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> barChartPhotosFillColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.photosFillColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> barChartAudioLineColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.audioStrokeColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> barChartAudioFillColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.audioFillColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> barChartOthersLineColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.othersStrokeColor
<span class="hljs-meta">@IBInspectable</span> <span class="hljs-keyword">var</span> barChartOthersFillColor: <span class="hljs-type">NSColor</span> = <span class="hljs-type">NSColor</span>.othersFillColor

<span class="hljs-comment">// 3</span>
<span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">colorsForFileType</span><span class="hljs-params">(fileType: FileType)</span></span> -&gt; (strokeColor: <span class="hljs-type">NSColor</span>, fillColor: <span class="hljs-type">NSColor</span>) {
  <span class="hljs-keyword">switch</span> fileType {
  <span class="hljs-keyword">case</span> .audio(<span class="hljs-number">_</span>, <span class="hljs-number">_</span>):
    <span class="hljs-keyword">return</span> (strokeColor: barChartAudioLineColor, fillColor: barChartAudioFillColor)
  <span class="hljs-keyword">case</span> .movies(<span class="hljs-number">_</span>, <span class="hljs-number">_</span>):
    <span class="hljs-keyword">return</span> (strokeColor: barChartMoviesLineColor, fillColor: barChartMoviesFillColor)
  <span class="hljs-keyword">case</span> .photos(<span class="hljs-number">_</span>, <span class="hljs-number">_</span>):
    <span class="hljs-keyword">return</span> (strokeColor: barChartPhotosLineColor, fillColor: barChartPhotosFillColor)
  <span class="hljs-keyword">case</span> .apps(<span class="hljs-number">_</span>, <span class="hljs-number">_</span>):
    <span class="hljs-keyword">return</span> (strokeColor: barChartAppsLineColor, fillColor: barChartAppsFillColor)
  <span class="hljs-keyword">case</span> .other(<span class="hljs-number">_</span>, <span class="hljs-number">_</span>):
    <span class="hljs-keyword">return</span> (strokeColor: barChartOthersLineColor, fillColor: barChartOthersFillColor)
  }
}
</pre>
    <p>
        上述代码：
    </p>
    <ol>
        <li>
            使用常量来声明一个结构体 - magic number是代码中的禁忌 - 你在整个教程中都会使用到它们。
        </li>
        <li>
            将这个view中全部可配置的property标注为
            <em>
                @IBInspectable
            </em>
            的，并使用在
            <em>
                NSColor+DiskInfo.swift
            </em>
            中的值来设置它们。专业提示：要让一个property可检视化，你必须声明它的类型，即使这个显然可以从它的内容中推断出来。
        </li>
        <li>
            声明一个助手方法，来依据文件的类型返回线条和填充的颜色。它会让你在绘制文件分布时非常方便。
        </li>
    </ol>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        并查看graph view。它现在已使用白色提换了默认的颜色，意味着实时渲染已可以work。如果没看马上看到效果的话，请保持耐心；它可能需要一两秒的时间来进行渲染。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-render-white-trim.png"
        rel="attachment wp-att-129854">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-render-white-trim-480x267.png"
            alt="sshot-render-white-trim" width="480" height="267" class="aligncenter size-medium wp-image-129854"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-render-white-trim-480x267.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-render-white-trim-768x427.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-render-white-trim-700x389.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-render-white-trim.png 1262w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        选择graph view并打开
        <em>
            Attributes Inspector
        </em>
        。你就可以看到刚刚添加的所有inspectable的property了。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim.png"
        rel="attachment wp-att-129855">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-318x320.png"
            alt="sshot-ibdesignable-trim" width="318" height="320" class="aligncenter size-medium wp-image-129855"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-318x320.png 318w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-768x772.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-497x500.png 497w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-128x128.png 128w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim.png 775w"
            sizes="(max-width: 318px) 100vw, 318px">
        </a>
    </p>
    <p>
        现在，你就既可以运行app来查看效果，也可以直接在Interface Builder来查看了。
    </p>
    <p>
        是时候来进行绘制了。
    </p>
    <h2>
        图形的上下文
    </h2>
    <p>
        当你使用Core Graphics，你不会直接绘制到view上，而是使用一个
        <em>
            Graphics Context
        </em>
        ，系统会在这里把绘制的内容渲染出来并展示到view上。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/image-rendering.png"
        rel="attachment wp-att-128912">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/image-rendering-591x500.png"
            alt="image-rendering" width="300" height="254" class="aligncenter size-medium wp-image-128912"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/image-rendering-591x500.png 591w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-rendering-378x320.png 378w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-rendering.png 674w"
            sizes="(max-width: 300px) 100vw, 300px">
        </a>
    </p>
    <p>
        Core Graphics应用了一个“画家模型”，因此当你在上下文中进行绘制的时候，请想象你正在一张画布上嗖嗖地进行绘图。你画下一条条的路径，并进行填充，然后又画下另一条路径，又进行填充。你已经画下的像素是不可以被擦除的，但可以再画下另外的像素来覆盖它。
    </p>
    <p>
        这里的概念是非常重要的，因为这个顺序将影响到最终的结果。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/drawing-order-aligned.png"
        rel="attachment wp-att-128913">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/drawing-order-aligned.png"
            alt="image-drawing-order" width="500" height="302" class="aligncenter size-medium wp-image-128913">
        </a>
    </p>
    <h2>
        用路径来绘制形状
    </h2>
    <p>
        要在Core Graphics中绘制一个形状，你就需要设定它的
        <em>
            path
        </em>
        ，在Core Graphics中它是由
        <code>
            CGPathRef
        </code>
        类型所代表的，相应地，它的可变版本的类型则是
        <code>
            CGMutablePathRef
        </code>
        。path只是形状的一个向量的表示。它无法自己去绘制自己。
    </p>
    <p>
        当你的路径完成后，你就可以把它添加到上下文中了。上下文就会使用路径和绘制属性等信息来渲染出你所期待的图形。
    </p>
    <h3>
        为条状图表绘制路径
    </h3>
    <p>
        圆角矩形是条状图表中的基本形状，所以就从这里开始吧。
    </p>
    <p>
        打开
        <em>
            GraphView.swift
        </em>
        并添加下列的extension到文件尾部，类定义的外部：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-comment">// MARK: - Drawing extension</span>

<span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">GraphView</span> </span>{
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">drawRoundedRect</span><span class="hljs-params">(rect: CGRect, inContext context: CGContext?,
                       radius: CGFloat, borderColor: CGColor, fillColor: CGColor)</span></span> {
    <span class="hljs-comment">// 1</span>
    <span class="hljs-keyword">let</span> path = <span class="hljs-type">CGMutablePath</span>()
    <span class="hljs-comment">// 2</span>
    path.move( to: <span class="hljs-type">CGPoint</span>(x:  rect.midX, y:rect.minY ))
    path.addArc( tangent1End: <span class="hljs-type">CGPoint</span>(x: rect.maxX, y: rect.minY ), 
                 tangent2End: <span class="hljs-type">CGPoint</span>(x: rect.maxX, y: rect.maxY), radius: radius)
    path.addArc( tangent1End: <span class="hljs-type">CGPoint</span>(x: rect.maxX, y: rect.maxY ), 
                 tangent2End: <span class="hljs-type">CGPoint</span>(x: rect.minX, y: rect.maxY), radius: radius)
    path.addArc( tangent1End: <span class="hljs-type">CGPoint</span>(x: rect.minX, y: rect.maxY ), 
                 tangent2End: <span class="hljs-type">CGPoint</span>(x: rect.minX, y: rect.minY), radius: radius)
    path.addArc( tangent1End: <span class="hljs-type">CGPoint</span>(x: rect.minX, y: rect.minY ), 
                 tangent2End: <span class="hljs-type">CGPoint</span>(x: rect.maxX, y: rect.minY), radius: radius)
    path.closeSubpath()
    <span class="hljs-comment">// 3</span>
    context?.setLineWidth(<span class="hljs-number">1.0</span>)
    context?.setFillColor(fillColor)
    context?.setStrokeColor(borderColor)
    <span class="hljs-comment">// 4</span>
    context?.addPath(path)
    context?.drawPath(using: .fillStroke)
  }
}
</pre>
    <p>
        <i>
            这
        </i>
        就是你绘制圆角矩形的方法。以下是更容易理解的解释：
    </p>
    <ol>
        <li>
            创建一个可变的path。
        </li>
        <li>
            构建圆角矩形的path，跟随以下步骤：
        </li>
        <ul>
            <li>
                首先移动到矩形底部的中心点。
            </li>
            <li>
                使用
                <code>
                    addArc(tangent1End:tangent2End:radius)
                </code>
                方法来绘制矩形右下侧的部分。这个方法将会绘制水平的线及圆角。
            </li>
            <li>
                添加右侧的线段及右上角的弧线。
            </li>
            <li>
                添加顶部的线段及左上角的弧线。
            </li>
            <li>
                添加左侧的线段及左下角的弧线。
            </li>
            <li>
                闭合路径，这将在最后一个点到起始的点之间绘制一条线段。
            </li>
        </ul>
        <li>
            设置绘制属性：线条粗细，填充颜色和边界颜色。
        </li>
        <li>
            将路径添加到上下文中，并使用
            <code>
                .fillStroke
            </code>
            参数来绘制它，该参数会告知Core Graphics去填充矩形并绘制边框。
        </li>
    </ol>
    <p>
        你再也不会以同样的方式来看矩形了！以下是上述代码运行的结果：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/image-roundedrect.png"
        rel="attachment wp-att-128914">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/image-roundedrect-480x150.png"
            alt="image-roundedrect" width="480" height="150" class="aligncenter size-medium wp-image-128914"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/image-roundedrect-480x150.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-roundedrect-768x240.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-roundedrect-700x219.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-roundedrect.png 1304w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <div class="note">
        <p>
            <em>
                注意
            </em>
            ：更多有关path绘制如何工作的内容，请参考苹果官方文档
            <a href="https://developer.apple.com/library/mac/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/dq_paths/dq_paths.html"
            target="_blank" title="Quartz 2D Programming Guide">
                Quartz 2D Programming Guide
            </a>
            中Paths &amp; Arcs部分。
        </p>
    </div>
    <h3>
        计算条状图表的位置
    </h3>
    <p>
        用Core Graphics进行绘制，基本上全都在是计算在你的view上可视元素的位置。规划将不同的元素放在什么地方，以及当所在view的尺寸发生变化时，如何做出相应的改变，是非常得重要的。
    </p>
    <p>
        这里是你自定义的view的布局：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/image-viewlayout.png"
        rel="attachment wp-att-128916">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/image-viewlayout-480x275.png"
            alt="image-viewlayout" width="480" height="275" class="aligncenter size-medium wp-image-128916"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/image-viewlayout-480x275.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-viewlayout-768x440.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-viewlayout-700x401.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-viewlayout-266x151.png 266w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-viewlayout.png 1444w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        打开
        <em>
            GraphView.swift
        </em>
        并添加下列的extension：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-comment">// MARK: - Calculations extension</span>

<span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">GraphView</span> </span>{
  <span class="hljs-comment">// 1</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">pieChartRectangle</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">CGRect</span> {
    <span class="hljs-keyword">let</span> width = bounds.size.width * <span class="hljs-type">Constants</span>.pieChartWidthPercentage - <span class="hljs-number">2</span> * <span class="hljs-type">Constants</span>.marginSize
    <span class="hljs-keyword">let</span> height = bounds.size.height - <span class="hljs-number">2</span> * <span class="hljs-type">Constants</span>.marginSize
    <span class="hljs-keyword">let</span> diameter = <span class="hljs-built_in">max</span>(<span class="hljs-built_in">min</span>(width, height), <span class="hljs-type">Constants</span>.pieChartMinRadius)
    <span class="hljs-keyword">let</span> rect = <span class="hljs-type">CGRect</span>(x: <span class="hljs-type">Constants</span>.marginSize,
                      y: bounds.midY - diameter / <span class="hljs-number">2.0</span>,
                      width: diameter, height: diameter)
    <span class="hljs-keyword">return</span> rect
  }
  
  <span class="hljs-comment">// 2</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">barChartRectangle</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">CGRect</span> {
    <span class="hljs-keyword">let</span> pieChartRect = pieChartRectangle()
    <span class="hljs-keyword">let</span> width = bounds.size.width - pieChartRect.maxX - <span class="hljs-number">2</span> * <span class="hljs-type">Constants</span>.marginSize
    <span class="hljs-keyword">let</span> rect = <span class="hljs-type">CGRect</span>(x: pieChartRect.maxX + <span class="hljs-type">Constants</span>.marginSize,
                      y: pieChartRect.midY + <span class="hljs-type">Constants</span>.marginSize,
                      width: width, height: barHeight)
    <span class="hljs-keyword">return</span> rect
  }
  
  <span class="hljs-comment">// 3</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">barChartLegendRectangle</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">CGRect</span> {
    <span class="hljs-keyword">let</span> barchartRect = barChartRectangle()
    <span class="hljs-keyword">let</span> rect = barchartRect.offsetBy(dx: <span class="hljs-number">0.0</span>, dy: -(barchartRect.size.height + <span class="hljs-type">Constants</span>.marginSize))
    <span class="hljs-keyword">return</span> rect
  }
}
</pre>
    <p>
        上述的代码实现了以下所需求的计算：
    </p>
    <ol>
        <li>
            从计算饼状图表的位置开始 - 它位于垂直居中的位置，并占据了此view宽度的三分之一。
        </li>
        <li>
            计算条状图表的位置。它占据了三分之二的宽度，并位于此view垂直中心靠上的位置。
        </li>
        <li>
            接下来计算图形说明的位置，基于饼状图最小的Y位置以及此view的边缘。
        </li>
    </ol>
    <p>
        现在该将它绘制到你的view上了。在
        <code>
            GraphView
        </code>
        的绘制extension中添加下面的方法：
    </p>
    <pre lang="swift" class="language-swift hljs">  
<span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">drawBarGraphInContext</span><span class="hljs-params">(context: CGContext?)</span></span> {
  <span class="hljs-keyword">let</span> barChartRect = barChartRectangle()
  drawRoundedRect(rect: barChartRect, inContext: context,
                  radius: <span class="hljs-type">Constants</span>.barChartCornerRadius,
                  borderColor: barChartAvailableLineColor.cgColor,
                  fillColor: barChartAvailableFillColor.cgColor)
}
</pre>
    <p>
        上面的代码添加了一个用来绘制条状图表的助手方法。它使用可用空间的填充和线条的颜色，绘制了一个圆角矩形作为背景。你可以在
        <em>
            NSColor+DiskInfo
        </em>
        extension中找到这些颜色。
    </p>
    <p>
        使用下列代码替换
        <code>
            draw(\_:)
        </code>
        方法中的全部内容：
    </p>
    <pre lang="swift" class="language-swift hljs">    
<span class="hljs-keyword">super</span>.draw(dirtyRect)
      
<span class="hljs-keyword">let</span> context = <span class="hljs-type">NSGraphicsContext</span>.current()?.cgContext
drawBarGraphInContext(context: context)
</pre>
    <p>
        此处才是绘制真正发生的地方。首先，你通过调用
        <code>
            NSGraphicsContext.current()
        </code>
        方法获取到了这个view当前的图形上下文，接着调用drawBarGraphInContext(context:)绘制出条状的图表。
    </p>
    <p>
        运行项目。你会看到条状图表已出现在了合适的位置上。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-barchart-first.png"
        rel="attachment wp-att-128917">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-barchart-first-480x259.png"
            alt="sshot-build-run-barchart-first" width="480" height="259" class="aligncenter size-medium wp-image-128917"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-barchart-first-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-barchart-first-768x414.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-barchart-first-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-barchart-first.png 1258w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
        <br>
        现在，打开
        <em>
            Main.storyboard
        </em>
        并选择
        <em>
            View Controller
        </em>
        场景。
    </p>
    <p>
        你会看到：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-live-render-barchart-first.png"
        rel="attachment wp-att-128918">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-live-render-barchart-first-480x216.png"
            alt="sshot-live-render-barchart-first" width="480" height="216" class="aligncenter size-medium wp-image-128918"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-live-render-barchart-first-480x216.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-live-render-barchart-first-768x345.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-live-render-barchart-first-700x315.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Interface Builder现在已经实时地将这个view绘制出来了。你也可以换一些颜色，这个view就会做出相应的变化。是不是很酷？
    </p>
    <h2>
        裁切区域
    </h2>
    <p>
        这一部分将会完成分布图表，也就是一个看起来像这样子的图表：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/barchart.png"
        rel="attachment wp-att-128936">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/barchart-480x52.png"
            alt="barchart" width="480" height="52" class="aligncenter size-medium wp-image-128936"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/barchart-480x52.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/barchart-768x84.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/barchart-700x76.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/barchart.png 882w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        先来扯一通理论吧。正如你所知道的，每个文件类型都有它自己的颜色，因此app需要基于相应文件大小所占的百分比，计算其对应的条的宽度，然后用相应的颜色绘制出来。
    </p>
    <p>
        你可以创建一个特定的形状，例如用顶部和底部的两条线构成的填充好的矩形，然后绘制出来。然而，有另一种技术可以让你复用你的代码来获得相同的结果：
        <em>
            裁切区域
        </em>
        。
    </p>
    <p>
        你可以吧裁切区域看做是一张被挖过一个洞的纸，然后把你放到你的画布上方：这样你就只能看到洞中透出来的部分了。这个“洞”被称作是裁切蒙版，在Core Graphics中由一个path来指定。
    </p>
    <p>
        在条状图表中，你就可以为每种文件类型创建被完全填充的相同的条，然后使用裁切蒙版来只展示正确的比例，就像下图中所示的一样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/image-clippingarea.png"
        rel="attachment wp-att-128919">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/image-clippingarea-411x320.png"
            alt="image-clippingarea" width="411" height="320" class="aligncenter size-medium wp-image-128919"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/image-clippingarea-411x320.png 411w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-clippingarea-768x598.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-clippingarea-643x500.png 643w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-clippingarea.png 1064w"
            sizes="(max-width: 411px) 100vw, 411px">
        </a>
    </p>
    <p>
        了解了裁切区域的工作原理，你就可以把条状图表搞出来了。
    </p>
    <p>
        在绘制之前，你需要设置当一个一篇被选中时
        <code>
            fileDistribution
        </code>
        的值。打开
        <em>
            Main.storyboard
        </em>
        ，并前往
        <em>
            View Controller
        </em>
        来创建一个outlet。
    </p>
    <p>
        在Project Navigator中
        <em>
            按住Option点击
        </em>
        <em>
            ViewController.swift
        </em>
        ，在
        <em>
            Assistant Editor
        </em>
        中打开它，然后
        <em>
            按住Control
        </em>
        把graph view拖拽到view controller的源码中来为它创建一个outlet。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-1.png"
        rel="attachment wp-att-128920">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-1-480x242.png"
            alt="image-outlet-1" width="500" height="252" class="aligncenter size-medium wp-image-128920"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-1-480x242.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-1-768x388.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-1-700x354.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-1.png 998w"
            sizes="(max-width: 500px) 100vw, 500px">
        </a>
    </p>
    <p>
        在弹出的面板中，将outlet命名为
        <code>
            graphView
        </code>
        ，并点击
        <em>
            Connect
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-2.png"
        rel="attachment wp-att-128921">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-2-480x269.png"
            alt="image-outlet-2" width="280" height="140" class="aligncenter size-medium wp-image-128921">
        </a>
    </p>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        ，并在
        <code>
            showVolumeInfo(\_:)
        </code>
        的尾部添加下列代码：
    </p>
    <pre lang="swift" class="language-swift hljs">    
graphView.fileDistribution = volume.fileDistribution
</pre>
    <p>
        根据被选择的硬盘，设置
        <code>
            fileDistribution
        </code>
        的值。
    </p>
    <p>
        打开
        <em>
            GraphView.swift
        </em>
        ，并在
        <code>
            drawBarGraphInContext(context:)
        </code>
        方法的尾部添加下列代码以绘制条状图表：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-comment">// 1</span>
<span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> fileTypes = fileDistribution?.distribution, <span class="hljs-keyword">let</span> capacity = fileDistribution?.capacity, capacity &gt; <span class="hljs-number">0</span> {
  <span class="hljs-keyword">var</span> clipRect = barChartRect
  <span class="hljs-comment">// 2</span>
  <span class="hljs-keyword">for</span> (index, fileType) <span class="hljs-keyword">in</span> fileTypes.enumerated() {
    <span class="hljs-comment">// 3</span>
    <span class="hljs-keyword">let</span> fileTypeInfo = fileType.fileTypeInfo
    <span class="hljs-keyword">let</span> clipWidth = floor(barChartRect.width * <span class="hljs-type">CGFloat</span>(fileTypeInfo.percent))
    clipRect.size.width = clipWidth
    <span class="hljs-comment">// 4</span>
    context?.saveGState()
    context?.clip(to: clipRect)
    <span class="hljs-keyword">let</span> fileTypeColors = colorsForFileType(fileType: fileType)
    drawRoundedRect(rect: barChartRect, inContext: context,
                    radius: <span class="hljs-type">Constants</span>.barChartCornerRadius,
                    borderColor: fileTypeColors.strokeColor.cgColor,
                    fillColor: fileTypeColors.fillColor.cgColor)
    context?.restoreGState()
    <span class="hljs-comment">// 5</span>
    clipRect.origin.x = clipRect.maxX
  }
}
</pre>
    <p>
        上述代码：
    </p>
    <ol>
        <li>
            确保这里的
            <code>
                fileDistribution
            </code>
            有效。
        </li>
        <li>
            迭代全部的文件类型。
        </li>
        <li>
            基于文件类型的百分比和前一文件类型，计算裁切的rect。
        </li>
        <li>
            保存上下文的状态，设置裁切的区域，并使用对应文件类似的颜色绘制矩形。然后再恢复上下文的状态。
        </li>
        <li>
            在下一次迭代之前移动裁切rect的
            <i>
                x
            </i>
            位置。
        </li>
    </ol>
    <p>
        你可能会好奇为什么要保存及恢复上下文的状态。还记的画家模式么？你添加到上下文的任何内容都会保留到这里。
    </p>
    <p>
        如果你添加多个裁切区域，你实际上就会创建一个涵盖所有裁切区域的大的裁切区域。为了避免这样，你就要在添加裁切区域之前，保存状态，然后当你用到的时候，再恢复上下文到这个状态，如此来处理裁切区域。
    </p>
    <p>
        现在，由于
        <code>
            index
        </code>
        从未被使用过，
        <em>
            Xcode
        </em>
        会提示一个warning。不必担心，我们将在后面修复它。
    </p>
    <p>
        运行项目，或打开
        <em>
            Main.storyboard
        </em>
        以在Interface Builder中查看它。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-graphbar-drawn.png"
        rel="attachment wp-att-128922">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-graphbar-drawn-480x259.png"
            alt="sshot-build-rung-graphbar-drawn" width="480" height="259" class="aligncenter size-medium wp-image-128922"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-graphbar-drawn-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-graphbar-drawn-768x414.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-graphbar-drawn-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-graphbar-drawn.png 1258w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        看起来我们已经实现了一些功能了。条状的图表已几乎完成，你只需要为它添加一些标记说明。
    </p>
    <h3>
        绘制文本
    </h3>
    <p>
        在自定义的view中绘制文本超级得简单。你只需要创建一个文本属性的字典 - 例如字体，大小，颜色，对齐方式 - 计算好要绘制到的rect的位置，然后调用
        <code>
            String
        </code>
        的
        <code>
            draw(in:withAttributes:)
        </code>
        方法就可以了。
    </p>
    <p>
        打开
        <em>
            GraphView.swift
        </em>
        并添加下列的property到类中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">fileprivate</span> <span class="hljs-keyword">var</span> bytesFormatter = <span class="hljs-type">ByteCountFormatter</span>()
</pre>
    <p>
        这就创建了一个
        <em>
            ByteCountFormatter
        </em>
        。它承担了将字节转换为人类可读的文本的重要工作。
    </p>
    <p>
        现在，添加下列的代码到
        <code>
            drawBarGraphInContext(context:)
        </code>
        中。确保添加到
        <code>
            for (index,fileType) in fileTypes.enumerated()
        </code>
        的循环中：
    </p>
    <pre lang="swift" class="language-swift hljs"> 
<span class="hljs-comment">// 1</span>
<span class="hljs-keyword">let</span> legendRectWidth = (barChartRect.size.width / <span class="hljs-type">CGFloat</span>(fileTypes.<span class="hljs-built_in">count</span>))
<span class="hljs-keyword">let</span> legendOriginX = barChartRect.origin.x + floor(<span class="hljs-type">CGFloat</span>(index) * legendRectWidth)
<span class="hljs-keyword">let</span> legendOriginY = barChartRect.minY - <span class="hljs-number">2</span> * <span class="hljs-type">Constants</span>.marginSize
<span class="hljs-keyword">let</span> legendSquareRect = <span class="hljs-type">CGRect</span>(x: legendOriginX, y: legendOriginY,
                              width: <span class="hljs-type">Constants</span>.barChartLegendSquareSize,
                              height: <span class="hljs-type">Constants</span>.barChartLegendSquareSize)

<span class="hljs-keyword">let</span> legendSquarePath = <span class="hljs-type">CGMutablePath</span>()
legendSquarePath.addRect( legendSquareRect )
context?.addPath(legendSquarePath)
context?.setFillColor(fileTypeColors.fillColor.cgColor)
context?.setStrokeColor(fileTypeColors.strokeColor.cgColor)
context?.drawPath(using: .fillStroke)

<span class="hljs-comment">// 2</span>
<span class="hljs-keyword">let</span> paragraphStyle = <span class="hljs-type">NSMutableParagraphStyle</span>()
paragraphStyle.lineBreakMode = .byTruncatingTail
paragraphStyle.alignment = .<span class="hljs-keyword">left</span>
<span class="hljs-keyword">let</span> nameTextAttributes = [
  <span class="hljs-type">NSFontAttributeName</span>: <span class="hljs-type">NSFont</span>.barChartLegendNameFont,
  <span class="hljs-type">NSParagraphStyleAttributeName</span>: paragraphStyle]

<span class="hljs-comment">// 3</span>
<span class="hljs-keyword">let</span> nameTextSize = fileType.name.size(withAttributes: nameTextAttributes)
<span class="hljs-keyword">let</span> legendTextOriginX = legendSquareRect.maxX + <span class="hljs-type">Constants</span>.legendTextMargin
<span class="hljs-keyword">let</span> legendTextOriginY = legendOriginY - <span class="hljs-number">2</span> * <span class="hljs-type">Constants</span>.pieChartBorderWidth
<span class="hljs-keyword">let</span> legendNameRect = <span class="hljs-type">CGRect</span>(x: legendTextOriginX, y: legendTextOriginY,
                            width: legendRectWidth - legendSquareRect.size.width - <span class="hljs-number">2</span> *
                              <span class="hljs-type">Constants</span>.legendTextMargin,
                            height: nameTextSize.height)

<span class="hljs-comment">// 4</span>
fileType.name.draw(<span class="hljs-keyword">in</span>: legendNameRect, withAttributes: nameTextAttributes)

<span class="hljs-comment">// 5</span>
<span class="hljs-keyword">let</span> bytesText = bytesFormatter.string(fromByteCount: fileTypeInfo.bytes)
<span class="hljs-keyword">let</span> bytesTextAttributes = [
  <span class="hljs-type">NSFontAttributeName</span>: <span class="hljs-type">NSFont</span>.barChartLegendSizeTextFont,
  <span class="hljs-type">NSParagraphStyleAttributeName</span>: paragraphStyle,
  <span class="hljs-type">NSForegroundColorAttributeName</span>: <span class="hljs-type">NSColor</span>.secondaryLabelColor]
<span class="hljs-keyword">let</span> bytesTextSize = bytesText.size(withAttributes: bytesTextAttributes)
<span class="hljs-keyword">let</span> bytesTextRect = legendNameRect.offsetBy(dx: <span class="hljs-number">0.0</span>, dy: -bytesTextSize.height)
bytesText.draw(<span class="hljs-keyword">in</span>: bytesTextRect, withAttributes: bytesTextAttributes)

</pre>
    <p>
        相当多的代码，但要看看懂并不困难：
    </p>
    <ol>
        <li>
            你早已熟悉了这个代码：计算说明颜色块的位置，创建它的路径并使用合适的颜色进行绘制。
        </li>
        <li>
            创建一个包含有字体和段落格式
            <code>
                NSMutableParagraphStyle
            </code>
            的属性的字典。这个段落格式会确定文本如何被绘制到给定的矩形中。在本例中，它被设定为靠左对齐及过长时省略尾部。
        </li>
        <li>
            计算文本将要被绘制到的矩形的范围。
        </li>
        <li>
            使用
            <code>
                draw(in:withAttributes:)
            </code>
            方法绘制文本。
        </li>
        <li>
            使用
            <code>
                bytesFormatter
            </code>
            获取文本的尺寸大小，并为文件大小的文本创建属性。这里相对于之前的代码，主要的区别是它通过
            <code>
                NSFontAttributeName
            </code>
            在属性字典中设置了一个不同的文本颜色。
        </li>
    </ol>
    <p>
        运行项目，或直接打开
        <em>
            Main.storyboard
        </em>
        来查看效果。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-graphbar-legend.png"
        rel="attachment wp-att-128923">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-graphbar-legend-480x259.png"
            alt="sshot-build-run-graphbar-legend" width="480" height="259" class="aligncenter size-medium wp-image-128923"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-graphbar-legend-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-graphbar-legend-768x414.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-graphbar-legend-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-graphbar-legend.png 1258w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        条状的图表完成了！你可以调整窗口的大小，看查看它如何适配新的尺寸。注意观察当没有足够大的空间时，文本如何被绘制。
    </p>
    <p>
        是不是很酷！
    </p>
    <h2>
        Cocoa Drawing
    </h2>
    <p>
        <em>
            macOS
        </em>
        提供了使用
        <em>
            AppKit
        </em>
        框架来完成绘制的替代选项。它提供了更高层次抽象的方法。他用类来替换
        <em>
            C
        </em>
        的函数，并提供助手方法来使得执行一些常见的任务变得更加容易。概念在两个框架中都是相同的，如果你熟悉Core Graphics的话，Cocoa Drawing是非常容易上手的。
    </p>
    <p>
        正如在Core Graphics中所做的一样，你需要使用
        <code>
            NSBezierPath
        </code>
        来创建和绘制路径，它是在Cocoa Drawing中等价于
        <code>
            CGPathRef
        </code>
        的对象：
    </p>
    <p>
        饼状图看起来应该是这样的：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/piechart.png"
        rel="attachment wp-att-128924">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/piechart-320x320.png"
            alt="piechart" width="280" height="280" class="aligncenter size-medium wp-image-128924"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/piechart-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/03/piechart-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/03/piechart-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/03/piechart-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/03/piechart-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/03/piechart-128x128.png 128w, https://koenig-media.raywenderlich.com/uploads/2016/03/piechart.png 375w"
            sizes="(max-width: 280px) 100vw, 280px">
        </a>
    </p>
    <p>
        你会分三步来绘制它：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/pichart-steps.png"
        rel="attachment wp-att-128941">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/pichart-steps-480x111.png"
            alt="pichart-steps" width="480" height="111" class="aligncenter size-medium wp-image-128941"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/pichart-steps-480x111.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/pichart-steps-768x178.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/pichart-steps-700x163.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <ul>
        <li>
            首先，你创建了一个圆形的路径来表示可用的空间，然后用配置好的颜色来描边和填充它。
        </li>
        <li>
            然后为已用的空间创建相应的path，并描出来。
        </li>
        <li>
            最后，基于已用部分路径，绘制出渐变的效果。
        </li>
    </ul>
    <p>
        打开
        <em>
            GraphView.swift
        </em>
        并添加下列的方法到绘制的extension中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">drawPieChart</span><span class="hljs-params">()</span></span> {
  <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> fileDistribution = fileDistribution <span class="hljs-keyword">else</span> {
    <span class="hljs-keyword">return</span>
  }
  
  <span class="hljs-comment">// 1</span>
  <span class="hljs-keyword">let</span> rect = pieChartRectangle()
  <span class="hljs-keyword">let</span> circle = <span class="hljs-type">NSBezierPath</span>(ovalIn: rect)
  pieChartAvailableFillColor.setFill()
  pieChartAvailableLineColor.setStroke()
  circle.stroke()
  circle.fill()
  
  <span class="hljs-comment">// 2</span>
  <span class="hljs-keyword">let</span> path = <span class="hljs-type">NSBezierPath</span>()
  <span class="hljs-keyword">let</span> center = <span class="hljs-type">CGPoint</span>(x: rect.midX, y: rect.midY)
  <span class="hljs-keyword">let</span> usedPercent = <span class="hljs-type">Double</span>(fileDistribution.capacity - fileDistribution.available) /
    <span class="hljs-type">Double</span>(fileDistribution.capacity)
  <span class="hljs-keyword">let</span> endAngle = <span class="hljs-type">CGFloat</span>(<span class="hljs-number">360</span> * usedPercent)
  <span class="hljs-keyword">let</span> radius = rect.size.width / <span class="hljs-number">2.0</span>
  path.move(to: center)
  path.line(to: <span class="hljs-type">CGPoint</span>(x: rect.maxX, y: center.y))
  path.appendArc(withCenter: center, radius: radius,
                                         startAngle: <span class="hljs-number">0</span>, endAngle: endAngle)
  path.close()
  
  <span class="hljs-comment">// 3</span>
  pieChartUsedLineColor.setStroke()
  path.stroke()
}
</pre>
    <p>
        上述代码：
    </p>
    <ol>
        <li>
            使用构造器
            <code>
                init(ovalIn:)
            </code>
            来创建一个圆形的path，设定好笔划和填充的颜色，然后绘制path。
        </li>
        <li>
            为已用部分的圆创建相应的路径。首先，基于已用的空间计算结束处的角度。然后分四步来创建path：
            <ol>
                <li>
                    移动到圆形的中点。
                </li>
                <li>
                    从中心到圆形的右侧添加一条线。
                </li>
                <li>
                    从当前的点添加一条弧线到刚计算出的角度。
                </li>
                <li>
                    闭合路径。然后再从弧形结束的点处连接一条线到圆形的中心。
                </li>
            </ol>
        </li>
        <li>
            设定好笔划的颜色，并使用
            <code>
                stroke()
            </code>
            方法来绘制path。
        </li>
    </ol>
    <p>
        你会发现很多相对于Core Graphics不同的情况：
    </p>
    <ul>
        <li>
            在代码中没有对图形上下文的引用。这是因为这些方法会自动获取当前的上下文，在这个case中，它就是当前view的上下文了。
        </li>
        <li>
            这里需要的是角度，而不是弧度。所以需要的话，可使用
            <em>
                CGFloat+Radians.swift
            </em>
            中的方法来进行转换。
        </li>
    </ul>
    <p>
        现在，添加下列的代码到
        <code>
            draw(\_:)
        </code>
        中来绘制饼状图表：
    </p>
    <pre lang="swift" class="language-swift hljs">drawPieChart()</pre>
    <p>
        运行项目。
        <br>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-pie-stroke.png"
        rel="attachment wp-att-128925">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-pie-stroke-480x259.png"
            alt="sshot-build-rung-pie-stroke" width="480" height="259" class="aligncenter size-medium wp-image-128925"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-pie-stroke-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-pie-stroke-768x414.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-pie-stroke-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-pie-stroke.png 1258w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        看起来是不好赞！
    </p>
    <h3>
        绘制渐变效果
    </h3>
    <p>
        <em>
            Cocoa Drawing
        </em>
        使用
        <code>
            NSGradient
        </code>
        来绘制渐变效果。
    </p>
    <p>
        你需要把渐变的效果绘制到可用部分的圆中，你早已知道该怎么做了。
    </p>
    <p>
        没错，就是裁切区域！
    </p>
    <p>
        你早已创建了一条用来进行绘制的路径，在绘制渐变效果之前，你就可以把它当做一个裁切区域来用。
    </p>
    <p>
        添加下列的代码到
        <code>
            drawPieChart()
        </code>
        的尾部：
    </p>
    <pre lang="swift" class="language-swift hljs">     
<span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> gradient = <span class="hljs-type">NSGradient</span>(starting: pieChartGradientStartColor,
                             ending: pieChartGradientEndColor) {
  gradient.draw(<span class="hljs-keyword">in</span>: path, angle: <span class="hljs-type">Constants</span>.pieChartGradientAngle)
}
</pre>
    <p>
        在第一行代码中，你尝试用两种颜色来创建一个渐变效果。如果创建成功的话，就调用
        <code>
            draw(in:angle:)
        </code>
        方法来绘制它。这个方法在内部设置了裁切区域，并绘制渐变的效果。这样子是不很棒？
    </p>
    <p>
        运行项目。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-gradient.png"
        rel="attachment wp-att-128926">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-gradient-480x259.png"
            alt="sshot-build-run-gradient" width="480" height="259" class="aligncenter size-medium wp-image-128926"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-gradient-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-gradient-768x414.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-gradient-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-gradient.png 1258w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        现在这个自定义的view已经看起来越来越棒了。现在就剩一件事需要做了：在饼状图表中绘制可用和已用空间的标记文本。
    </p>
    <p>
        你早就知道该怎么做了吧。想不想挑战一下？:]
    </p>
    <p>
        下面是你需要做的事：
    </p>
    <ol>
        <li>
            使用
            <code>
                bytesFormatter
            </code>
            来获取可用空间的文本（
            <code>
                fileDistribution.available
            </code>
            property）以及全部空间（
            <code>
                fileDistribution.capacity
            </code>
            property）。
        </li>
        <li>
            计算文本的位置，把它放到可用和已用部分的中点处。
        </li>
        <li>
            使用下列的熟悉绘制文本：
        </li>
        <ul>
            <li>
                字体：
                <code>
                    NSFont.pieChartLegendFont
                </code>
            </li>
            <li>
                已用空间文本的颜色：
                <code>
                    NSColor.pieChartUsedSpaceTextColor
                </code>
            </li>
            <li>
                可用空间文本的颜色：
                <code>
                    NSColor.pieChartAvailableSpaceTextColor
                </code>
            </li>
        </ul>
    </ol>
    <h3>
        绘制饼状图的标注
    </h3>
    <p>
        添加下面的代码到
        <code>
            drawPieChart()
        </code>
        方法中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-comment">// 1</span>
<span class="hljs-keyword">let</span> usedMidAngle = endAngle / <span class="hljs-number">2.0</span>
<span class="hljs-keyword">let</span> availableMidAngle = (<span class="hljs-number">360.0</span> - endAngle) / <span class="hljs-number">2.0</span>
<span class="hljs-keyword">let</span> halfRadius = radius / <span class="hljs-number">2.0</span>

<span class="hljs-comment">// 2</span>
<span class="hljs-keyword">let</span> usedSpaceText = bytesFormatter.string(fromByteCount: fileDistribution.capacity)
<span class="hljs-keyword">let</span> usedSpaceTextAttributes = [
<span class="hljs-type">NSFontAttributeName</span>: <span class="hljs-type">NSFont</span>.pieChartLegendFont,
<span class="hljs-type">NSForegroundColorAttributeName</span>: <span class="hljs-type">NSColor</span>.pieChartUsedSpaceTextColor]
<span class="hljs-keyword">let</span> usedSpaceTextSize = usedSpaceText.size(withAttributes: usedSpaceTextAttributes)
<span class="hljs-keyword">let</span> xPos = rect.midX + <span class="hljs-type">CGFloat</span>(cos(usedMidAngle.radians)) *
halfRadius - (usedSpaceTextSize.width / <span class="hljs-number">2.0</span>)
<span class="hljs-keyword">let</span> yPos = rect.midY + <span class="hljs-type">CGFloat</span>(sin(usedMidAngle.radians)) *
halfRadius - (usedSpaceTextSize.height / <span class="hljs-number">2.0</span>)
usedSpaceText.draw(at: <span class="hljs-type">CGPoint</span>(x: xPos, y: yPos),
        withAttributes: usedSpaceTextAttributes)

<span class="hljs-comment">// 3</span>
<span class="hljs-keyword">let</span> availableSpaceText = bytesFormatter.string(fromByteCount: fileDistribution.available)
<span class="hljs-keyword">let</span> availableSpaceTextAttributes = [
<span class="hljs-type">NSFontAttributeName</span>: <span class="hljs-type">NSFont</span>.pieChartLegendFont,
<span class="hljs-type">NSForegroundColorAttributeName</span>: <span class="hljs-type">NSColor</span>.pieChartAvailableSpaceTextColor]
<span class="hljs-keyword">let</span> availableSpaceTextSize = availableSpaceText.size(withAttributes: availableSpaceTextAttributes)
<span class="hljs-keyword">let</span> availableXPos = rect.midX + cos(-availableMidAngle.radians) *
halfRadius - (availableSpaceTextSize.width / <span class="hljs-number">2.0</span>)
<span class="hljs-keyword">let</span> availableYPos = rect.midY + sin(-availableMidAngle.radians) *
halfRadius - (availableSpaceTextSize.height / <span class="hljs-number">2.0</span>)
availableSpaceText.draw(at: <span class="hljs-type">CGPoint</span>(x: availableXPos, y: availableYPos),
            withAttributes: availableSpaceTextAttributes)
</pre>
    <p>
        上述代码：
    </p>
    <ol>
        <li>
            计算你绘制已用和可用部分文本位置相应的角度。
        </li>
        <li>
            创建文本的属性，并计算已用空间文本的位置
            <i>
                x
            </i>
            和
            <i>
                y
            </i>
            - 然后绘制出来。
        </li>
        <li>
            创建文本的属性，并计算可用空间文本的位置
            <i>
                x
            </i>
            和
            <i>
                y
            </i>
            - 然后绘制出来。
        </li>
    </ol>
    <p>
        现在，运行项目来查看你最终的作品吧。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-final-1.png"
        rel="attachment wp-att-128927">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-final-1-480x242.png"
            alt="Final app made using Core Graphics on macOS" width="480" height="242"
            class="aligncenter size-medium wp-image-128927" srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-final-1-480x242.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-final-1-768x388.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-final-1-700x354.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-final-1.png 1568w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        祝贺！你已经用Core Graphics和Cocoa Drawing构建了一个超美的app！
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
        你可以从
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/06/DiskInfo-Final.zip">
            这里
        </a>
        下载最终完整的项目。
    </p>
    <p>
        本教程已覆盖了在
        <em>
            macOS
        </em>
        中，可用来在定制的view上进行绘制的不同的框架。你已经了解了：
    </p>
    <ul>
        <li>
            如何使用Core Graphics和Cocoa Drawing创建及绘制path
        </li>
        <li>
            如何使用裁切区域
        </li>
        <li>
            如何绘制文本
        </li>
        <li>
            如何绘制渐变效果
        </li>
    </ul>
    <p>
        现在，你应当非常自信地使用Core Graphics和Cocoa Drawing去绘制漂亮的、相应式的图形了。
    </p>
    <p>
        如果你想要学到更多相关的内容，可以参考下列的资源：
    </p>
    <li>
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CocoaDrawingGuide/Introduction/Introduction.html"
        target="_blank" title="Introduction to Cocoa Drawing Guide">
            Introduction to Cocoa Drawing Guide
        </a>
    </li>
    <li>
        <a href="https://developer.apple.com/library/mac/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/Introduction/Introduction.html"
        target="_blank" title="Quartz">
            Quartz 2D Programming Guide
        </a>
    </li>
</div>