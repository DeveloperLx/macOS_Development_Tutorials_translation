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
            通过使用路径、填充、裁剪及文本，来用代码进行绘制
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
            draw(_:)
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
        TL/DR:
        <i>
            That
        </i>
        is how you draw a rectangle. Here’s a more comprehensive explanation:
    </p>
    <ol>
        <li>
            Create a mutable path.
        </li>
        <li>
            Form the rounded rectangle path, following these steps:
        </li>
        <ul>
            <li>
                Move to the center point at the bottom of the rectangle.
            </li>
            <li>
                Add the lower line segment at the bottom-right corner using
                <code>
                    addArc(tangent1End:tangent2End:radius)
                </code>
                . This method draws the horizontal line and the rounded corner.
            </li>
            <li>
                Add the right line segment and the top-right corner.
            </li>
            <li>
                Add the top line segment and the top-left corner.
            </li>
            <li>
                Add the right line segment and the bottom-left corner.
            </li>
            <li>
                Close the path, which adds a line from the last point to the starter point.
            </li>
        </ul>
        <li>
            Set the drawing attributes: line width, fill color and border color.
        </li>
        <li>
            Add the path to the context and draw it using the
            <code>
                .fillStroke
            </code>
            parameter, which tells Core Graphics to fill the rectangle and draw the
            border.
        </li>
    </ol>
    <p>
        You’ll never look at a rectangle the same way! Here’s the humble result
        of all that code:
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
                Note
            </em>
            : For more information about how path drawing works, check out Paths &amp;
            Arcs in Apple’s
            <a href="https://developer.apple.com/library/mac/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/dq_paths/dq_paths.html"
            target="_blank" title="Quartz 2D Programming Guide">
                Quartz 2D Programming Guide
            </a>
            .
        </p>
    </div>
    <h3>
        Calculate the Bar Chart’s Position
    </h3>
    <p>
        Drawing with Core Graphics is all about calculating the positions of the
        visual elements in your view. It’s important to plan where to locate the
        different elements and think through they should behave when the size of
        the view changes.
    </p>
    <p>
        Here’s the layout for your custom view:
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
        Open
        <em>
            GraphView.swift
        </em>
        and add this extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1286146">
                    <td class="code" id="p128614code6">
                        <pre class="swift" style="font-family:monospace;">
                            // MARK: - Calculations extension &nbsp; extension GraphView { // 1 func
                            pieChartRectangle() -&gt; CGRect { let width = bounds.size.width * Constants.pieChartWidthPercentage
                            - 2 * Constants.marginSize let height = bounds.size.height - 2 * Constants.marginSize
                            let diameter = max(min(width, height), Constants.pieChartMinRadius) let
                            rect = CGRect(x: Constants.marginSize, y: bounds.midY - diameter / 2.0,
                            width: diameter, height: diameter) return rect } &nbsp; // 2 func barChartRectangle()
                            -&gt; CGRect { let pieChartRect = pieChartRectangle() let width = bounds.size.width
                            - pieChartRect.maxX - 2 * Constants.marginSize let rect = CGRect(x: pieChartRect.maxX
                            + Constants.marginSize, y: pieChartRect.midY + Constants.marginSize, width:
                            width, height: barHeight) return rect } &nbsp; // 3 func barChartLegendRectangle()
                            -&gt; CGRect { let barchartRect = barChartRectangle() let rect = barchartRect.offsetBy(dx:
                            0.0, dy: -(barchartRect.size.height + Constants.marginSize)) return rect
                            } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The above code does all of these required calculations:
    </p>
    <ol>
        <li>
            Start by calculating the position of the pie chart — it’s in the center
            vertically and occupies one third of the view’s width.
        </li>
        <li>
            Here you calculate the position of the bar chart. It takes two thirds
            of the width and it’s located above the vertical center of the view.
        </li>
        <li>
            Then you calculate the position of the graphics legend, based on the minimum
            Y position of the pie chart and the margins.
        </li>
    </ol>
    <p>
        Time to draw it in your view. Add this method inside the
        <code>
            GraphView
        </code>
        drawing extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1286147">
                    <td class="code" id="p128614code7">
                        <pre class="swift" style="font-family:monospace;">
                            func drawBarGraphInContext(context: CGContext?) { let barChartRect = barChartRectangle()
                            drawRoundedRect(rect: barChartRect, inContext: context, radius: Constants.barChartCornerRadius,
                            borderColor: barChartAvailableLineColor.cgColor, fillColor: barChartAvailableFillColor.cgColor)
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        You’ve added a helper method that will draw the bar chart. It draws a
        rounded rectangle as a background, using the fill and stroke colors for
        the available space. You can find those colors in the
        <em>
            NSColor+DiskInfo
        </em>
        extension.
    </p>
    <p>
        Replace all the code inside
        <code>
            draw(_:)
        </code>
        with this:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1286148">
                    <td class="code" id="p128614code8">
                        <pre class="swift" style="font-family:monospace;">
                            super.draw(dirtyRect) &nbsp; let context = NSGraphicsContext.current()?.cgContext
                            drawBarGraphInContext(context: context)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here is where the actual drawing takes place. First, you get the view’s
        current graphics context by invoking
        <code>
            NSGraphicsContext.current()
        </code>
        , and then you call the method to draw the bar chart.
    </p>
    <p>
        Build and run. You’ll see the bar chart in it’s proper position.
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
        Now, open
        <em>
            Main.storyboard
        </em>
        and select the
        <em>
            View Controller
        </em>
        scene.
    </p>
    <p>
        You’ll see this:
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
        Interface Builder now renders the view in real time. You can also change
        the colors and the view responds to those changes. How awesome is that?
    </p>
    <h2>
        Clipping Areas
    </h2>
    <p>
        You’re at the part where you make the distribution chart, a bar chart
        that looks like this:
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
        Take a step back here and dabble in a bit of theory. As you know, each
        file type has its own color, and somehow, the app needs to calculate each
        bar’s width based on the corresponding file type’s percentage, and then
        draw each type with a unique color.
    </p>
    <p>
        You could create a special shape, such as a filled rectangle with two
        lines at bottom and top of the rectangle, and then draw it. However, there
        is another technique that will let you reuse your code and get the same
        result:
        <em>
            clipping areas
        </em>
        .
    </p>
    <p>
        You can think of a clipping area as a sheet of paper with a hole cut out
        of it, which you place over your drawing: you can only see the part of
        the drawing which shows through the hole. This hole is known as the clipping
        mask, and is specified as a path within Core Graphics.
    </p>
    <p>
        In the case of the bar chart, you can create an identical fully-filled
        bar for each filetype, and then use a clipping-mask to only display the
        correct proportion, as shown in the following diagram:
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
        With an understanding of how clipping areas work, you’re ready to make
        this bar chart happen.
    </p>
    <p>
        Before drawing, you need to set the value for
        <code>
            fileDistribution
        </code>
        when a disk is selected. Open
        <em>
            Main.storyboard
        </em>
        and go to the
        <em>
            View Controller
        </em>
        scene to create an outlet.
    </p>
    <p>
        <em>
            Option-click
        </em>
        on
        <em>
            ViewController.swift
        </em>
        in the Project Navigator to open it in the
        <em>
            Assistant Editor
        </em>
        , and
        <em>
            Control-Drag
        </em>
        from the graph view into the view controller class source code to create
        an outlet for it.
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
        In the popup, name the outlet
        <code>
            graphView
        </code>
        and click
        <em>
            Connect
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-2.png"
        rel="attachment wp-att-128921">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-2-480x269.png"
            alt="image-outlet-2" width="280" height="140" class="aligncenter size-medium wp-image-128921">
        </a>
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add this code at the end of
        <code>
            showVolumeInfo(_:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1286149">
                    <td class="code" id="p128614code9">
                        <pre class="swift" style="font-family:monospace;">
                            graphView.fileDistribution = volume.fileDistribution
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This code sets the
        <code>
            fileDistribution
        </code>
        value with the distribution of the selected disk.
    </p>
    <p>
        Open
        <em>
            GraphView.swift
        </em>
        and add this code at the end of
        <code>
            drawBarGraphInContext(context:)
        </code>
        to draw the bar chart:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12861410">
                    <td class="code" id="p128614code10">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 if let fileTypes = fileDistribution?.distribution, let capacity =
                            fileDistribution?.capacity, capacity &gt; 0 { var clipRect = barChartRect
                            // 2 for (index, fileType) in fileTypes.enumerated() { // 3 let fileTypeInfo
                            = fileType.fileTypeInfo let clipWidth = floor(barChartRect.width * CGFloat(fileTypeInfo.percent))
                            clipRect.size.width = clipWidth &nbsp; // 4 context?.saveGState() context?.clip(to:
                            clipRect) &nbsp; let fileTypeColors = colorsForFileType(fileType: fileType)
                            drawRoundedRect(rect: barChartRect, inContext: context, radius: Constants.barChartCornerRadius,
                            borderColor: fileTypeColors.strokeColor.cgColor, fillColor: fileTypeColors.fillColor.cgColor)
                            context?.restoreGState() &nbsp; // 5 clipRect.origin.x = clipRect.maxX
                            } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This is what the code above does:
    </p>
    <ol>
        <li>
            Makes sure there is a valid
            <code>
                fileDistribution
            </code>
            .
        </li>
        <li>
            Iterates through all the file types in the distribution.
        </li>
        <li>
            Calculates the clipping rect, based on the file type percentage and previous
            file types.
        </li>
        <li>
            Saves the state of the context, sets the clipping area and draws the rectangle
            using the colors configured for the file type. Then it restores the state
            of the context.
        </li>
        <li>
            Moves the
            <i>
                x
            </i>
            origin of the clipping rect before the next iteration.
        </li>
    </ol>
    <p>
        You might wonder why you need to save and restore the state of the context.
        Remember the painter’s model? Everything you add to the context stays there.
    </p>
    <p>
        If you add multiple clipping areas, you are in fact creating a clipping
        area that acts as the unifying force for all of them. To avoid that, you
        save the state before adding the clipping area, and when you’ve used it,
        you restore the context to that state, disposing of that clipping area.
    </p>
    <p>
        At this point,
        <em>
            Xcode
        </em>
        shows a warning because
        <code>
            index
        </code>
        is never used. Don’t worry about it for now. You’ll fix it later on.
    </p>
    <p>
        Build and run, or open
        <em>
            Main.storyboard
        </em>
        and check it out in Interface Builder.
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
        It’s beginning to look functional. The bar chart is almost finished and
        you just need to add the legend.
    </p>
    <h3>
        Drawing Strings
    </h3>
    <p>
        Drawing a string in a custom view is super easy. You just need to create
        a dictionary with the string attributes — for instance the font, size,
        color, alignment — calculate the rectangle where it will be drawn, and
        invoke
        <code>
            String
        </code>
        ‘s method
        <code>
            draw(in:withAttributes:)
        </code>
        .
    </p>
    <p>
        Open
        <em>
            GraphView.swift
        </em>
        and add the following property to the class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12861411">
                    <td class="code" id="p128614code11">
                        <pre class="swift" style="font-family:monospace;">
                            fileprivate var bytesFormatter = ByteCountFormatter()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This creates an
        <em>
            ByteCountFormatter
        </em>
        . It does all the heavy work of transforming bytes into a human-friendly
        string.
    </p>
    <p>
        Now, add this inside
        <code>
            drawBarGraphInContext(context:)
        </code>
        . Make sure you add it inside the
        <code>
            for (index,fileType) in fileTypes.enumerated()
        </code>
        loop:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12861412">
                    <td class="code" id="p128614code12">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 let legendRectWidth = (barChartRect.size.width / CGFloat(fileTypes.count))
                            let legendOriginX = barChartRect.origin.x + floor(CGFloat(index) * legendRectWidth)
                            let legendOriginY = barChartRect.minY - 2 * Constants.marginSize let legendSquareRect
                            = CGRect(x: legendOriginX, y: legendOriginY, width: Constants.barChartLegendSquareSize,
                            height: Constants.barChartLegendSquareSize) &nbsp; let legendSquarePath
                            = CGMutablePath() legendSquarePath.addRect( legendSquareRect ) context?.addPath(legendSquarePath)
                            context?.setFillColor(fileTypeColors.fillColor.cgColor) context?.setStrokeColor(fileTypeColors.strokeColor.cgColor)
                            context?.drawPath(using: .fillStroke) &nbsp; // 2 let paragraphStyle =
                            NSMutableParagraphStyle() paragraphStyle.lineBreakMode = .byTruncatingTail
                            paragraphStyle.alignment = .left let nameTextAttributes = [ NSFontAttributeName:
                            NSFont.barChartLegendNameFont, NSParagraphStyleAttributeName: paragraphStyle]
                            &nbsp; // 3 let nameTextSize = fileType.name.size(withAttributes: nameTextAttributes)
                            let legendTextOriginX = legendSquareRect.maxX + Constants.legendTextMargin
                            let legendTextOriginY = legendOriginY - 2 * Constants.pieChartBorderWidth
                            let legendNameRect = CGRect(x: legendTextOriginX, y: legendTextOriginY,
                            width: legendRectWidth - legendSquareRect.size.width - 2 * Constants.legendTextMargin,
                            height: nameTextSize.height) &nbsp; // 4 fileType.name.draw(in: legendNameRect,
                            withAttributes: nameTextAttributes) &nbsp; // 5 let bytesText = bytesFormatter.string(fromByteCount:
                            fileTypeInfo.bytes) let bytesTextAttributes = [ NSFontAttributeName: NSFont.barChartLegendSizeTextFont,
                            NSParagraphStyleAttributeName: paragraphStyle, NSForegroundColorAttributeName:
                            NSColor.secondaryLabelColor] let bytesTextSize = bytesText.size(withAttributes:
                            bytesTextAttributes) let bytesTextRect = legendNameRect.offsetBy(dx: 0.0,
                            dy: -bytesTextSize.height) bytesText.draw(in: bytesTextRect, withAttributes:
                            bytesTextAttributes)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        That was quite a bit of code, but it’s easy to follow:
    </p>
    <ol>
        <li>
            You’re already familiar with this code: calculate the position of the
            legend’s colored square, create a path for it and draw with the appropriate
            colors.
        </li>
        <li>
            Create a dictionary of attributes that includes the font and a paragraph
            style
            <code>
                NSMutableParagraphStyle
            </code>
            . The paragraph defines how the string should be drawn inside the given
            rectangle. In this case, it’s left aligned with a truncated tail.
        </li>
        <li>
            Calculate the position and size of the rectangle to draw the text in.
        </li>
        <li>
            Draw the text invoking
            <code>
                draw(in:withAttributes:)
            </code>
            .
        </li>
        <li>
            Get the size string using the
            <code>
                bytesFormatter
            </code>
            and create the attributes for the file size text. The main difference
            from the previous code is that this sets a different text color in the
            attributes dictionary via
            <code>
                NSFontAttributeName
            </code>
            .
        </li>
    </ol>
    <p>
        Build and run, or open
        <em>
            Main.storyboard
        </em>
        , to see the results).
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
        The bar chart is complete! You can resize the window to see how it adapts
        to the new size. Watch how the text properly truncates when there isn’t
        enough space to draw it.
    </p>
    <p>
        Looking great so far!
    </p>
    <h2>
        Cocoa Drawing
    </h2>
    <p>
        <em>
            macOS
        </em>
        apps come with the option to use
        <em>
            AppKit
        </em>
        framework to draw instead. It provides a higher level of abstraction.
        It uses classes instead of
        <em>
            C
        </em>
        functions and includes helper methods that make it easier to perform common
        tasks. The concepts are equivalent in both frameworks, and Cocoa Drawing
        is very easy to adopt if you’re familiar with Core Graphics.
    </p>
    <p>
        As it goes in Core Graphics, you need to create and draw paths, using
        <code>
            NSBezierPath
        </code>
        , the equivalent of
        <code>
            CGPathRef
        </code>
        in Cocoa Drawing:
    </p>
    <p>
        This is how the pie chart will look:
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
        You’ll draw it in three steps:
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
            First, you create a circle path for the available space circle, and then
            you fill and stroke it with the configured colors.
        </li>
        <li>
            Then you create a path for the used space circle segment and stroke it.
        </li>
        <li>
            Finally, you draw a gradient that only fills the used space path.
        </li>
    </ul>
    <p>
        Open
        <em>
            GraphView.swift
        </em>
        and add this method into the drawing extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12861413">
                    <td class="code" id="p128614code13">
                        <pre class="swift" style="font-family:monospace;">
                            func drawPieChart() { guard let fileDistribution = fileDistribution else
                            { return } &nbsp; // 1 let rect = pieChartRectangle() let circle = NSBezierPath(ovalIn:
                            rect) pieChartAvailableFillColor.setFill() pieChartAvailableLineColor.setStroke()
                            circle.stroke() circle.fill() &nbsp; // 2 let path = NSBezierPath() let
                            center = CGPoint(x: rect.midX, y: rect.midY) let usedPercent = Double(fileDistribution.capacity
                            - fileDistribution.available) / Double(fileDistribution.capacity) let endAngle
                            = CGFloat(360 * usedPercent) let radius = rect.size.width / 2.0 path.move(to:
                            center) path.line(to: CGPoint(x: rect.maxX, y: center.y)) path.appendArc(withCenter:
                            center, radius: radius, startAngle: 0, endAngle: endAngle) path.close()
                            &nbsp; // 3 pieChartUsedLineColor.setStroke() path.stroke() }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        There are a few things to go through here:
    </p>
    <ol>
        <li>
            Create a circle path using the constructor
            <code>
                init(ovalIn:)
            </code>
            , set the fill and stroke color, and then draw the path.
        </li>
        <li>
            Create a path for the used space circle segment. First, calculate the
            ending angle based on the used space. Then create the path in four steps:
            <ol>
                <li>
                    Move to the center point of the circle.
                </li>
                <li>
                    Add an horizontal line from the center to the right side of the circle.
                </li>
                <li>
                    Add an arc from current point to the calculated angle.
                </li>
                <li>
                    Close the path. This adds a line from the arc’s end point back to the
                    center of the circle.
                </li>
            </ol>
        </li>
        <li>
            Set the stroke color and stroke the path by calling its
            <code>
                stroke()
            </code>
            method.
        </li>
    </ol>
    <p>
        You may have noticed a couple of differences compared to Core Graphics:
    </p>
    <ul>
        <li>
            There aren’t any reference to the graphics context in the code. That’s
            because these methods automatically get the current context, and in this
            case, it’s the view’s context.
        </li>
        <li>
            Angles are measured in degrees, not radians.
            <em>
                CGFloat+Radians.swift
            </em>
            extends CGFloat to do conversions if needed.
        </li>
    </ul>
    <p>
        Now, add the following code inside
        <code>
            draw(_:)
        </code>
        to draw the pie chart:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12861414">
                    <td class="code" id="p128614code14">
                        <pre class="swift" style="font-family:monospace;">
                            drawPieChart()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run.
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
        Looking good so far!
    </p>
    <h3>
        Drawing Gradients
    </h3>
    <p>
        <em>
            Cocoa Drawing
        </em>
        uses
        <code>
            NSGradient
        </code>
        to draw a gradient.
    </p>
    <p>
        You need to draw the gradient inside the used space segment of the circle,
        and you already know how to do it.
    </p>
    <p>
        How will you do it? Exactly, clipping areas!
    </p>
    <p>
        You’ve already created a path to draw it, and you can use it as a clipping
        path before you draw the gradient.
    </p>
    <p>
        Add this code at the end of
        <code>
            drawPieChart()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12861415">
                    <td class="code" id="p128614code15">
                        <pre class="swift" style="font-family:monospace;">
                            if let gradient = NSGradient(starting: pieChartGradientStartColor, ending:
                            pieChartGradientEndColor) { gradient.draw(in: path, angle: Constants.pieChartGradientAngle)
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        In the first line, you try to create a gradient with two colors. If this
        works, you call
        <code>
            draw(in:angle:)
        </code>
        to draw it. Internally, this method sets the clipping path for you and
        draws the gradient inside it. How nice is that?
    </p>
    <p>
        Build and run.
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
        The custom view is looking better and better. There’s only one thing left
        to do: Draw the available and used space text strings inside the pie chart.
    </p>
    <p>
        You already know how to do it. Are you up to the challenge? :]
    </p>
    <p>
        This is what you need to do:
    </p>
    <ol>
        <li>
            Use the
            <code>
                bytesFormatter
            </code>
            to get the text string for the available space (
            <code>
                fileDistribution.available
            </code>
            property ) and full space (
            <code>
                fileDistribution.capacity
            </code>
            property).
        </li>
        <li>
            Calculate the position of the text so that you draw it in the middle point
            of the available and used segments.
        </li>
        <li>
            Draw the text in that position with these attributes:
        </li>
        <ul>
            <li>
                Font:
                <code>
                    NSFont.pieChartLegendFont
                </code>
            </li>
            <li>
                Used space text color:
                <code>
                    NSColor.pieChartUsedSpaceTextColor
                </code>
            </li>
            <li>
                Available space text color:
                <code>
                    NSColor.pieChartAvailableSpaceTextColor
                </code>
            </li>
        </ul>
    </ol>
    <div class="easySpoilerWrapper" style="">
        <table class="easySpoilerTable" border="0" style="text-align:center;"
        align="center" bgcolor="FFFFFF">
            <tbody>
                <tr style="white-space:normal;">
                    <th class="easySpoilerTitleA" style="white-space:normal;font-weight:normal;text-align:left;vertical-align:middle;font-size:120%;color:#000000;">
                        Solution Inside: Draw Pie Chart Legend
                    </th>
                    <th class="easySpoilerTitleB" style="text-align:right;vertical-align:middle;font-size:100%; white-space:nowrap;">
                        <a href="" onclick="wpSpoilerSelect(&quot;spoilerDiv87b8001&quot;); return false;"
                        class="easySpoilerButtonOther" style="font-size:100%;color:#000000;background-color:#fcfcfc;background-image:none;border: 1px inset;border-style:solid;border-color:#cccccc; margin: 3px 0px 3px; padding: 4px; "
                        align="right">
                            Select
                        </a>
                        <a href="" onclick="wpSpoilerToggle(&quot;spoilerDiv87b8001&quot;,true,&quot;Show&quot;,&quot;Hide&quot;,&quot;fast&quot;,false); return false;"
                        id="spoilerDiv87b8001_action" class="easySpoilerButton" value="Show" align="right"
                        style="font-size:100%;color:#000000;background-color:#fcfcfc;background-image:none;border: 1px inset;border-style:solid;border-color:#cccccc; margin: 3px 0px 3px 5px; padding: 4px;">
                            Show
                        </a>
                    </th>
                </tr>
                <tr>
                    <td class="easySpoilerRow" colspan="2" style="">
                        <div id="spoilerDiv87b8001" class="easySpoilerSpoils" style="display:none; white-space:wrap; overflow:auto; vertical-align:middle;">
                            <p>
                                Add this code inside the
                                <code>
                                    drawPieChart()
                                </code>
                                method:
                            </p>
                            <div class="wp_codebox">
                                <table>
                                    <tbody>
                                        <tr id="p12861416">
                                            <td class="code" id="p128614code16">
                                                <pre class="swift" style="font-family:monospace;">
                                                    // 1 let usedMidAngle = endAngle / 2.0 let availableMidAngle = (360.0
                                                    - endAngle) / 2.0 let halfRadius = radius / 2.0 &nbsp; // 2 let usedSpaceText
                                                    = bytesFormatter.string(fromByteCount: fileDistribution.capacity) let usedSpaceTextAttributes
                                                    = [ NSFontAttributeName: NSFont.pieChartLegendFont, NSForegroundColorAttributeName:
                                                    NSColor.pieChartUsedSpaceTextColor] let usedSpaceTextSize = usedSpaceText.size(withAttributes:
                                                    usedSpaceTextAttributes) let xPos = rect.midX + CGFloat(cos(usedMidAngle.radians))
                                                    * halfRadius - (usedSpaceTextSize.width / 2.0) let yPos = rect.midY + CGFloat(sin(usedMidAngle.radians))
                                                    * halfRadius - (usedSpaceTextSize.height / 2.0) usedSpaceText.draw(at:
                                                    CGPoint(x: xPos, y: yPos), withAttributes: usedSpaceTextAttributes) &nbsp;
                                                    // 3 let availableSpaceText = bytesFormatter.string(fromByteCount: fileDistribution.available)
                                                    let availableSpaceTextAttributes = [ NSFontAttributeName: NSFont.pieChartLegendFont,
                                                    NSForegroundColorAttributeName: NSColor.pieChartAvailableSpaceTextColor]
                                                    let availableSpaceTextSize = availableSpaceText.size(withAttributes: availableSpaceTextAttributes)
                                                    let availableXPos = rect.midX + cos(-availableMidAngle.radians) * halfRadius
                                                    - (availableSpaceTextSize.width / 2.0) let availableYPos = rect.midY +
                                                    sin(-availableMidAngle.radians) * halfRadius - (availableSpaceTextSize.height
                                                    / 2.0) availableSpaceText.draw(at: CGPoint(x: availableXPos, y: availableYPos),
                                                    withAttributes: availableSpaceTextAttributes)
                                                </pre>
                                            </td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                            <p>
                                This code does the following:
                            </p>
                            <ol>
                                <li>
                                    Calculates the angles where you’ll draw used and available texts.
                                </li>
                                <li>
                                    Creates the text attributes and calculates the
                                    <i>
                                        x
                                    </i>
                                    and
                                    <i>
                                        y
                                    </i>
                                    position of the used space text – then it draws.
                                </li>
                                <li>
                                    Creates the text attributes and calculates the
                                    <i>
                                        x
                                    </i>
                                    and
                                    <i>
                                        y
                                    </i>
                                    position of the available space, and then it draws.
                                </li>
                            </ol>
                            <p>
                                Now, build and run and see the final result of your handiwork.
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
                            </p>
                        </div>
                    </td>
                </tr>
            </tbody>
        </table>
        <div class="easySpoilerConclude" style="">
            <table class="easySpoilerTable" border="0" style="text-align:center;"
            frame="box" align="center" bgcolor="FFFFFF">
                <tbody>
                    <tr>
                        <th class="easySpoilerEnd" style="width:100%;">
                        </th>
                        <td class="easySpoilerEnd" style="white-space:nowrap;" colspan="2">
                        </td>
                    </tr>
                    <tr>
                        <td class="easySpoilerGroupWrapperLastRow" colspan="2" style="">
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
    <br>
    Congratulations! You’ve built a beautiful app using Core Graphics and
    Cocoa Drawing!
    <p>
    </p>
    <h2>
        Where to Go From Here
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
        You can download the completed project
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/06/DiskInfo-Final.zip">
            here
        </a>
        .
    </p>
    <p>
        This Core Graphics on macOS tutorial covered the basics of the different
        frameworks available to use for drawing custom views in
        <em>
            macOS
        </em>
        . You just covered:
    </p>
    <ul>
        <li>
            How to create and draw paths using Core Graphics and Cocoa Drawing
        </li>
        <li>
            How to use clipping areas
        </li>
        <li>
            How to draw text strings
        </li>
        <li>
            How to draw gradients
        </li>
    </ul>
    <p>
        You should now feel confident in your abilities to use Core Graphics and
        Cocoa Drawing next time you need clean, responsive graphics.
    </p>
    <p>
        If you’re looking to learn more, consider the following resources:
    </p>
    <li>
        Apple’s
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CocoaDrawingGuide/Introduction/Introduction.html"
        target="_blank" title="Introduction to Cocoa Drawing Guide">
            Introduction to Cocoa Drawing Guide
        </a>
    </li>
    <li>
        Apple’s
        <a href="https://developer.apple.com/library/mac/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/Introduction/Introduction.html"
        target="_blank" title="Quartz" 2d="" programming="" guide="">
            Quartz 2D Programming Guide
        </a>
    </li>
</div>