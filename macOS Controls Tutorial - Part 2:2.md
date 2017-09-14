# macOS控件教程：2/2部分

#### [原文地址](https://www.raywenderlich.com/149297/macos-controls-tutorial-part-22) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <em>
            更新日志：
        </em>
        已由Ernesto García更新至 Xcode 8.2 / Swift 3 版。
        <a href="https://www.raywenderlich.com/82046/introduction-to-os-x-tutorial-core-controls-and-swift-part-1">
            之前
        </a>
        由
        <a href="https://www.raywenderlich.com/u/skyrocketsw">
            Michael Briscoe
        </a>
        更新至Xcode 6.3 / Swift 1.2。
        <a href="https://www.raywenderlich.com/27388/core-controls-in-mac-os-x-part-12">
            初始版本
        </a>
        作者为
        <a href="http://www.raywenderlich.com/u/ernesto">
            Ernesto García
        </a>
        。
    </p>
    <p>
        欢迎回到macOS控件教程的系列的第二部分，也就是最后一部分。
    </p>
    <p>
        在
        <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/macOS%20Controls%20Tutorial%20-%20Part%201:2.md"
        title="first part">
            这个教程的第一部分
        </a>
        ，你开始了构建一个Mad Lib风格的macOS app，在这里用户可以输入单词和短语来创建有趣的桔子。
    </p>
    <p>
        继续下去，你会学到一些核心的macOS UI控件 - 也就是Text Fields，Combo Boxes，Pop Up Buttons，Push Buttons和Text Views.
    </p>
    <h2>
        更多macOS控件
    </h2>
    <p>
        在这个教程中的最后一部分，你会完成你的app，并学会如何使用下面的控件：
    </p>
    <ul>
        <li>
            Sliders
        </li>
        <li>
            Date Pickers
        </li>
        <li>
            Radio Buttons
        </li>
        <li>
            Check Boxes
        </li>
        <li>
            Image Views
        </li>
    </ul>
    <p>
        在这个两部分的教程的末尾，你会对macOS的控件有一个很好的理解。
    </p>
    <p>
        这个教程将从你中断的地方再捡起来。如果你还没有之前的项目，这里是第一部分的
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibs-part1-final-1.zip">
            最后的项目
        </a>
        。
    </p>
    <p>
        是时候开始工作了！
    </p>
    <h2>
        滑动 - NSSlider
    </h2>
    <p>
        slider是一个控件，让用户可以从一个范围中进行选择。slider有一个最小值和最大值，通过移动控件的“把手”，用户可以在两个限制中进行选择。slider可以是线性或径向的。你会问，两者间的区别是什么？
    </p>
    <p>
        线性的slider可以是垂直的或水平的，他们让你可以通过沿着轨迹移动把手来选择一个值。关于线性slider的一个很好的例子，就是macOS中的鼠标偏好面板了：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/slider-mouse.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/slider-mouse.png"
            alt="slider-mouse" width="340" height="148" class="aligncenter size-full wp-image-150213">
        </a>
    </p>
    <p>
        径向slider有一点的不同 - 它是一个小小的带有把手的圆心，它可以360度地进行旋转。你可以点击和拖拽把手到要求的位置来选择一个值。关于径向slider，你可以在Adobe Photoshop中来找到一个很棒的例子，它用来定义一个渐变的角度，就像下面这样：
    </p>
    <p>
        <a href="https://www.raywenderlich.com/slider-example-radial" rel="attachment wp-att-27039">
            <img src="https://koenig-media.raywenderlich.com/uploads/2012/12/slider-example-radial.png"
            alt="" title="slider-example-radial" width="339" height="144" class="aligncenter size-full wp-image-27039">
        </a>
    </p>
    <p>
        在macOS中负责这个的控件是
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ApplicationKit/Classes/NSSlider_Class/Reference/Reference.html"
        title="NSSlider Class Reference">
            NSSlider
        </a>
        。
    </p>
    <p>
        全部三种类型的slider（水平、垂直和径向）实际上都是一个控件
        <code>
            NSSlider
        </code>
        。唯一的区别只是它们的外表。Interface Builder对于每种类型的slider在Object Library中都有一个对象，如同下面展示的这样：
    </p>
    <p>
        <a href="http://www.raywenderlich.com/82047/introduction-to-os-x-tutorial-core-controls-and-swift-part-2/sliders-ib-2"
        rel="attachment wp-att-83305">
            <img src="https://koenig-media.raywenderlich.com/uploads/2014/09/sliders-ib.png"
            alt="sliders-ib" width="295" height="282" class="aligncenter size-full wp-image-83305"
            srcset="https://koenig-media.raywenderlich.com/uploads/2014/09/sliders-ib.png 295w, https://koenig-media.raywenderlich.com/uploads/2014/09/sliders-ib-32x32.png 32w"
            sizes="(max-width: 295px) 100vw, 295px">
        </a>
    </p>
    <h3>
        Slider语义
    </h3>
    <p>
        当使用slider的时候，通常你会执行两个任务，获取或设置当前的值，以及获取和设置slider让位的最高值和最低值。这些property被展示如下：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-comment">// getting &amp; setting an integer value</span>
<span class="hljs-keyword">let</span> theInteger = mySlider.integerValue
mySlider.integerValue = theInteger

<span class="hljs-comment">// getting &amp; setting a float value</span>
<span class="hljs-keyword">let</span> theFloat = mySlider.floatValue
mySlider.floatValue = theFloat

<span class="hljs-comment">// getting &amp; setting a double value</span>
<span class="hljs-keyword">let</span> theDouble = mySlider.doubleValue
mySlider.doubleValue = theDouble

<span class="hljs-comment">// getting &amp; setting the minimum value of the range</span>
<span class="hljs-keyword">let</span> theMinimumValue = mySlider.minValue
mySlider.minValue = theMinimumValue

<span class="hljs-comment">// getting &amp; setting the maximum value of the range</span>
<span class="hljs-keyword">let</span> theMaximumValue = mySlider.maxValue
mySlider.maxValue = theMaximumValue
</pre>
    <p>
        再一次，这里没有什么好奇怪的 - 如果你现在已学到了什么，它就是实现标准macOS控件的一个相当简单的练习。移步到下一部分，让你的app包含一个
        <code>
            NSSlider
        </code>
        ！
    </p>
    <h2>
        选择一个数字，任何数字
    </h2>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        。在Object Library的面板中定位到
        <em>
            Label
        </em>
        控件，并将它拖拽到content view上Phrase label的下面。改变窗口的垂直方向的大小，并将
        <em>
            Go!
        </em>
        按钮向下拖拽，如果你需要给它空间的话。
    </p>
    <p>
        双击控件来编辑它的默认文本，改变为
        <em>
            Amount: [10]
        </em>
        。找到
        <em>
            水平Slider
        </em>
        控件并将它拖拽到窗口上，并将它放置到label的右边。
    </p>
    <p>
        点击slider并选择它。打开
        <em>
            Attributes Inspector
        </em>
        并设置最小值为2，最大值为10。改变当前的值为5。这会作为当用户首次运行app时，slider的默认的值。
    </p>
    <p>
        确保
        <em>
            Continuous
        </em>
        已选中。这告诉slider来通知
        <em>
            any
        </em>
        slider值的任何变化。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-add-1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-add-1-650x439.png"
            alt="slider-add" width="650" height="439" class="aligncenter size-large wp-image-153200"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-add-1-650x439.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/slider-add-1-474x320.png 474w, https://koenig-media.raywenderlich.com/uploads/2017/01/slider-add-1.png 1421w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        现在你创建两个outlet；一个是slider的，另一个则是label。稍等，你可能会说 - 有一点的不同。为何要给label添加一个label？
    </p>
    <p>
        这是因为，这样就可以在slider的值发生变化的时候，更新label的文本来列出当前的数量；因此为何要给slider的
        <em>
            Continuous
        </em>
        property。哈哈，现在就有意义了吧，不是吗？
    </p>
    <p>
        打开Assistant editor并确保
        <em>
            ViewController.swift
        </em>
        已打开。
        <em>
            按住Ctrl拖拽label
        </em>
        到
        <em>
            ViewController.swift
        </em>
        上来创建一个新的outlet。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-drag-1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-drag-1-650x455.png"
            alt="slider-drag" width="650" height="455" class="aligncenter size-large wp-image-153201"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-drag-1-650x455.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/slider-drag-1-457x320.png 457w, https://koenig-media.raywenderlich.com/uploads/2017/01/slider-drag-1.png 1364w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        在弹出的屏幕中，将outlet命名为
        <em>
            amountLabel
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/amountlabel-drag2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/amountlabel-drag2-480x269.png"
            alt="amountlabel-drag2" width="480" height="269" class="aligncenter size-medium wp-image-150235"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/amountlabel-drag2-480x269.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/amountlabel-drag2.png 504w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        对slider重复上面的过程，将outlet命名为
        <em>
            amountSlider
        </em>
        。
    </p>
    <p>
        现在你需要添加一个
        <em>
            action
        </em>
        ，当slider的值发生变化的时候进行调用。你早已在第一部分中为你的button创建了action，因此你会获得更多的实践！
    </p>
    <p> 
        选择slider并
        <em>
            按住Ctrl拖拽
        </em>
        到
        <em>
            ViewController.swift
        </em>
        中类定义中的任何地方：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-action-drag.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-action-drag-650x365.png"
            alt="slider-action-drag" width="650" height="365" class="aligncenter size-large wp-image-153202"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-action-drag-650x365.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/slider-action-drag-480x269.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/slider-action-drag.png 1381w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        在弹出的窗口中，确认设置connection为一个
        <em>
            action
        </em>
        而不是一个outlet。将它命名为
        <em>
            sliderChanged
        </em>
        ，就像下面这样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/slider-action2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/slider-action2-480x228.png"
            alt="slider-action2" width="400" height="190" class="aligncenter size-medium wp-image-150237"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/slider-action2-480x228.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/slider-action2.png 500w"
            sizes="(max-width: 400px) 100vw, 400px">
        </a>
    </p>
    <p>
        现在你需要在action被调用时更新label。
    </p>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        并添加下面的代码到
        <code>
            sliderChanged()
        </code>
        中：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-keyword">let</span> amount = amountSlider.integerValue
amountLabel.stringValue = <span class="hljs-string">"Amount: [<span class="hljs-subst">\(amount)</span>]"</span>
</pre>
    <p>
        快速回顾上面展示的代码，你第一次读取了slider当前的值，然后你label的值为一个包含slider的值的字符串。请注意，用户不能从UI中编辑
        <code>
            amountLabel
        </code>
        的值，但仍然可以通过编程的方式来编辑它。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            这个例子使用
            <code>
                integerValue
            </code>
            获取了一个很好的整数，但如果你需要更加精确，你可以为你的slider使用
            <code>
                floatValue
            </code>
            或
            <code>
                doubleValue
            </code>
            的值。
        </p>
    </div>
    <p>
        运行项目。尝试来回滑动slider，来查看label的值跟随slider当前的值变化而变化：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-slider.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-slider-386x320.png"
            alt="buildrun-slider" width="386" height="320" class="aligncenter size-medium wp-image-153203"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-slider-386x320.png 386w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-slider-603x500.png 603w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-slider.png 672w"
            sizes="(max-width: 386px) 100vw, 386px">
        </a>
    </p>
    <p>
        有一个小问题。你注意到了么？当app第一次运行的时候，标签并不会展示正确的值！虽然这不是一个大问题，但看起来app并未完成。这是因为label仅会在slider的把手挪动的时候才会更新。
    </p>
    <p>
        不要害怕 - 这很容易解决。
    </p>
    <p>
        添加下列的代码到
        <code>
            viewDidLoad()
        </code>
        尾部：
    </p>
    <pre lang="swift" class="hljs objectivec"><span class="hljs-comment">// Update the amount slider</span>
sliderChanged(<span class="hljs-keyword">self</span>)
</pre>
    <p>
        现在app就会在启动时调用
        <code>
            sliderChanged()
        </code>
        ，它就会更新label。Neat！
    </p>
    <p>
        运行项目。现在label就在一运行时展示正确的值，这是一个很小的接触，但这是“配合和完成”，让你的app看起来更优美的元素。
    </p>
    <p>
        更复杂的值，例如日历日期呢？是的，macOS也有那些的处理了！:]
    </p>
    <h2>
        今夜的“热日期” - NSDatePicker
    </h2>
    <p>
        Date Picker是一个展示日期和时间的macOS控件，提供了一个方法来让用户编辑这些值。Date Picker可以被指定来展示一个日期，一个时间或同时展示日期和时间。在macOS中负责这个的控件是
        <a href="http://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Classes/NSDatePicker_Class/Reference/Reference.html"
        title="NSDatePicker Class Reference">
            NSDatePicker
        </a>
        。
    </p>
    <p>
        Date Picker可以以两种风格的样式来展示：文本的，它的日期和时间信息将会被展示到text field中；以及图形的，它的日期会以一个日历的形式展现，时间则以一个时钟的形式来展现。你可以在macOS的日期&时间偏好面板中找到全部风格的例子：就像下面截图中展示的这样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/date-macos.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/date-macos-480x232.png"
            alt="date-macos" width="480" height="232" class="aligncenter size-medium wp-image-150214"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/date-macos-480x232.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/date-macos-650x314.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/12/date-macos.png 974w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        对于date picker，你最常见的要执行的任务就是获取和设置它的日期和时间了，已经设置在你的控件中所允许的最小和最大的日期/时间的值。用来实现这些的property已展示在下面！
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-comment">// getting &amp; setting the date/time value</span>
<span class="hljs-keyword">let</span> myDate = myDatePicker.dateValue
myDatePicker.dateValue = myDate

<span class="hljs-comment">// getting &amp; setting the minimum date of the range</span>
<span class="hljs-keyword">let</span> theMinimumDate = myDatePicker.minDate
myDatePicker.minDate = theMinimumDate

<span class="hljs-comment">// getting &amp; setting the maximum date of the range</span>
<span class="hljs-keyword">let</span> theMaximumDate = myDatePicker.maxDate
myDatePicker.maxDate = theMaximumDate
</pre>
    <p>
        再一次的 - 这个控件拥有非常简单的getter和setter风格的接口来更新这些值。现在是时候（原谅我的调皮！）把这个控件放到你的项目上了。
    </p>
    <h2>
        我误了一个非常重要的日期
    </h2>
    <p>
        跟着习惯的步骤，添加一个
        <em>
            Label
        </em>
        到你的窗口上。将它的标题改为
        <em>
            Date:
        </em>
        ，对齐方式改为
        <em>
            向右
        </em>
        。在对象面板中找到
        <em>
            Date Picker
        </em>
        ，并把它拖拽到窗口上，将它放到label的右边。如果需要的话，改变窗口的大小，并将
        <em>
            Go!
        </em>
        按钮向下移动：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/add-datepicker.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/add-datepicker-650x374.png"
            alt="add-datepicker" width="650" height="374" class="aligncenter size-large wp-image-153206"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/add-datepicker-650x374.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/add-datepicker-480x276.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/add-datepicker.png 1441w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        为date picker创建一个outlet，就在之前你完成的每个控件的outlet的下面。在弹出的窗口中，将property命名为
        <em>
            datePicker
        </em>
        。
    </p>
    <p>
        就像app中的其它控件一样，当运行你的app时，向用户展示一个默认的值会比较好。选取当前的日期作为默认值听起来是一个不错的选择！:]
    </p>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        并添加下面的代码到
        <code>
            viewDidLoad()
        </code>
        方法的末尾：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-comment">// Set the date picker to display the current date</span>
datePicker.dateValue = <span class="hljs-built_in">Date</span>()
</pre>
    <p>
        运行项目！你应该会看到你漂亮的新date picker正在展示当前的日期，就像下面截图中的一样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-datepicker.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-datepicker-386x320.png"
            alt="buildrun-datepicker" width="386" height="320" class="aligncenter size-medium wp-image-153207"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-datepicker-386x320.png 386w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-datepicker-603x500.png 603w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-datepicker.png 672w"
            sizes="(max-width: 386px) 100vw, 386px">
        </a>
    </p>
    <h2>
        视频杀掉了音频...按钮
    </h2>
    <p>
        Radio buttons是一个特殊类型的控件，经常以组的形式出现；典型地，它们会展示为一个带有在一边的可选按钮的选项的列表。它们的表现在某种程度上时独一无二的；在组中的任意按钮都可以被选择，但只要选择了其中一个按钮，就会将组中其它按钮的选择都取消掉。在相同的组中，同时只有一个按钮可以被选中。
    </p>
    <p>
        关于radio buttons的一个展示一系列选项的很好的例子，就是iTunes的备份的选项，就像下面这样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2012/12/radio-example.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2012/12/radio-example.png"
            alt="" title="radio-example" width="369" height="121" class="aligncenter size-full wp-image-27114">
        </a>
    </p>
    <p>
        Radio buttons是以radio groups的形式组织起来的。
    </p>
    <p>
        当你点击了组中的一个按钮，它就会被选中，并且系统会自动将组中其余的按钮取消选择。你只需要考虑获取和设置合适的值。多么得方便！
    </p>
    <p>
        但你该怎么定义一个组？引用文档中所说的：
    </p>
    <p>
        <i>
            “Radio buttons自动地作为了一个组（选择一个按钮将取消全部其它相关的按钮），当它们拥有相同的父view和动作方法。”
        </i>
    </p>
    <p>
        因此，所有你需要做的就是添加radio buttons到一个view上，创建一个动作，并设计这个组中所有按钮的动作。
    </p>
    <p>
        然后你只需要改变按钮的状态（On/Off），系统自己会管理取消选择其它的按钮。
    </p>
    <pre lang="swift" class="hljs objectivec"><span class="hljs-comment">// Select a radio button </span>
radioButton.state = <span class="hljs-built_in">NSOnState</span>

<span class="hljs-comment">// Deselect a radio button</span>
radioButton.state = <span class="hljs-built_in">NSOffState</span>

<span class="hljs-comment">// Check if a radio button is selected.</span>
let selected = (radioButton.state == <span class="hljs-built_in">NSOnState</span>)

</pre>
    <p>
        再一次地，一个复杂的控件被削减为一些非常简单的方法。继续阅读，来了解如何在你的app中实现一个radio button控件！
    </p>
    <h2>
        呼叫家的地方 - 添加Radio Buttons
    </h2>
    <p>
        添加一个新的
        <em>
            Label
        </em>
        到你的app上（你现在应该对此感到非常舒服了！），并将它的标题改为
        <em>
            Place:
        </em>
        。在Object Library面板中找到
        <em>
            Radio Button
        </em>
        ，并将它拖拽到content view上，就在label的旁边。双击radio buttons，来将他们的标题分别改为：
        <em>
            RWDevCon
        </em>
        ，
        <em>
            360iDev
        </em>
        和
        <em>
            WWDC
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/radioadd.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/radioadd-638x500.png"
            alt="radioadd" width="638" height="500" class="aligncenter size-large wp-image-153209"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/radioadd-638x500.png 638w, https://koenig-media.raywenderlich.com/uploads/2017/01/radioadd-408x320.png 408w, https://koenig-media.raywenderlich.com/uploads/2017/01/radioadd.png 1599w"
            sizes="(max-width: 638px) 100vw, 638px">
        </a>
    </p>
    <p>
        现在，你需要为每个radio button创建一个新的outlet - 现在你应当相当熟悉另一个动作了！打开
        <em>
            Assistant Editor
        </em>
        并
        <em>
            按住Ctrl拖拽
        </em>
        第一个radio button到
        <em>
            ViewController.swift
        </em>
        的源文件中，就在已存在的property的下面。将outlet命名为
        <em>
            rwDevConRadioButton
        </em>
        。对另外两个radio buttons重复同样的过程，将outlet分别命名为
        <em>
            threeSixtyRadioButton
        </em>
        和
        <em>
            wwdcRadioButton
        </em>
        。
    </p>
    <p>
        运行项目。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-error.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-error-469x500.png"
            alt="buildrun-radio-error" width="469" height="500" class="aligncenter size-large wp-image-153210"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-error-469x500.png 469w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-error-300x320.png 300w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-error.png 672w"
            sizes="(max-width: 469px) 100vw, 469px">
        </a>
    </p>
    <p>
        点击radio button，你会立刻注意到一个问题。你可以选择全部的radio button。它们并没有表现得像一个组。为什么？因为要让不同radio button成为一个组，需要有两个条件：它们必须拥有相同的父view（这是关键），他们需要有一个共同的动作。在我们的app中并不满足第二个条件。
    </p>
    <p>
        为了解决上述情况，你需要为这些按钮创建一个共同的动作。
    </p>
    <p>
        你早已是个使用Interface Builder创建动作的专家了吧，对么？所以，我们来学习一种替代的方法，在代码中创建动作，并将其指派到Interface Builder的radio buttons上。
    </p>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        并在类的实现中添加下列的代码：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-meta">@IBAction</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">radioButtonChanged</span><span class="hljs-params">(<span class="hljs-number">_</span> sender: AnyObject)</span></span> {
    
}
</pre>
    <p>
        这是一个典型的动作方法，它包含一个
        <code>
            @IBAction
        </code>
        的标注，因此Interface Builder就可以找到并使用它。现在，打开
        <em>
            Main.storyBoard
        </em>
        并指派这个动作给radio button。
    </p>
    <p>
        前往
        <em>
            Document Outline
        </em>
        并
        <em>
            按住Control单击
        </em>
        （或右击）View Controller。在弹出的窗口中，找到
        <em>
            Received Actions
        </em>
        区，并从靠近
        <code>
            radioButtonChanged:
        </code>
        的圈拖拽到
        <em>
            RWDevCon
        </em>
        radio button的上面。只需简单的动作，你就将动作指派到了radio button的上面。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/radio-addaction.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/radio-addaction-548x500.png"
            alt="radio-addaction" width="548" height="500" class="aligncenter size-large wp-image-153211"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/radio-addaction-548x500.png 548w, https://koenig-media.raywenderlich.com/uploads/2017/01/radio-addaction-351x320.png 351w, https://koenig-media.raywenderlich.com/uploads/2017/01/radio-addaction.png 1072w"
            sizes="(max-width: 548px) 100vw, 548px">
        </a>
    </p>
    <p>
        重复上述过程，将相同的动作指派到另外两个radio button上面。你的received action现在应当看起来就像是这样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/radio-actions-all.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/radio-actions-all-480x218.png"
            alt="radio-actions-all" width="300" height="136" class="aligncenter size-medium wp-image-150253"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/radio-actions-all-480x218.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/radio-actions-all.png 512w"
            sizes="(max-width: 300px) 100vw, 300px">
        </a>
    </p>
    <p>
        运行项目：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-469x500.png"
            alt="buildrun-radio" width="469" height="500" class="aligncenter size-large wp-image-153212"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-469x500.png 469w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-300x320.png 300w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio.png 672w"
            sizes="(max-width: 469px) 100vw, 469px">
        </a>
    </p>
    <p>
        现在radio buttons就应该表现得像一个组了。
    </p>
    <p>
        现在，你需要让
        <em>
            RWDevCon
        </em>
        radio button成为app启动时的默认项。你只需要设置radio button的state为On，然后其它的按钮就会被自动地取消选择。
    </p>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        。并添加下列的代码到
        <code>
            viewDidLoad()
        </code>
        方法的尾部：
    </p>
    <pre lang="swift" class="hljs objectivec"><span class="hljs-comment">// Set the radio group's initial selection</span>
rwDevConRadioButton.state = <span class="hljs-built_in">NSOnState</span>
</pre>
    <p>
        运行项目。你会看到在app启动时，
        <em>
            RWDevCon
        </em>
        radio button已被选中。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/radio-rwdev.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/radio-rwdev.png"
            alt="radio-rwdev" width="300" height="121" class="aligncenter size-full wp-image-150255">
        </a>
    </p>
    <p>
        Radio button是在你的app中切换值的一种方法，但还有着执行类似功能的一个另外的macOS控件 - check boxes！
    </p>
    <h2>
        勾选全部的盒子 - Check Box Button
    </h2>
    <p>
        通常，你会在app中使用check box来展示一些布尔值的状态。这些状态常常会以某种方式影响app的一个特性的打开或关闭。
    </p>
    <p>
        你会在当用户打开或关闭一个功能的地方找到check box。你会在Settings app中几乎每一个屏幕中找到它。例如，在Energy Saver窗口中，你会使用check box来打开或关闭不同的选项。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/check-example.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/check-example-480x138.png"
            alt="check-example" width="480" height="138" class="aligncenter size-medium wp-image-153214"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/check-example-480x138.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/check-example-650x187.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/check-example.png 790w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        使用check box相当容易；大多数情况下，你只需要关心获取和设置这个控件的状态。check box的状态可以是下列之一：
        <em>
            NSOnState
        </em>
        （在所有地方打开特性），
        <em>
            NSOffState
        </em>
        （在所有地方关闭特性）以及
        <em>
            NSMixedState
        </em>
        （在部分地方打开特性，但并非全部）。
    </p>
    <p>
        这里是你使用它的方式：
    </p>
    <pre lang="swift" class="hljs objectivec"><span class="hljs-comment">// Set the state to On</span>
myCheckBox.state = <span class="hljs-built_in">NSOnState</span>

<span class="hljs-comment">// Set the state to Off</span>
myCheckBox.state = <span class="hljs-built_in">NSOffState</span>

<span class="hljs-comment">// Get the state of a check box</span>
let state = myCheckBox.state
</pre>
    <p>
        超级得简单！是时候添加一个checkbox到你的app上。
    </p>
    <h2>
        单击和双击 - 添加Checkboxes
    </h2>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        。在Object Library中找到
        <em>
            Check Box Button
        </em>
        并将它拖拽到content view上。双击它，并将标题改为
        <em>
            Yell!!
        </em>
        就像下面图中展示的这样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/check-add.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/check-add-650x447.png"
            alt="check-add" width="650" height="447" class="aligncenter size-large wp-image-153215"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/check-add-650x447.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/check-add-465x320.png 465w, https://koenig-media.raywenderlich.com/uploads/2017/01/check-add.png 1572w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        现在，为check box添加一个outlet并将它命名为
        <em>
            yellCheck
        </em>
        。你现在已经正式地成为一个创建outlet的专家了！
    </p>
    <p>
        现在，你会将check box在app启动时的默认值设为off。为了做到这点，添加下列的代码到
        <code>
            viewDidLoad()
        </code>
        的尾部：
    </p>
    <pre lang="swift" class="hljs objectivec"><span class="hljs-comment">// set check button state</span>
yellCheck.state = <span class="hljs-built_in">NSOffState</span>
</pre>
    <p>
        运行项目！你应当看到check box的状态是未勾选的。点击它来查看其行为：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-check.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-check-477x500.png"
            alt="buildrun-check" width="477" height="500" class="aligncenter size-large wp-image-153217"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-check-477x500.png 477w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-check-305x320.png 305w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-check.png 672w"
            sizes="(max-width: 477px) 100vw, 477px">
        </a>
    </p>
    <h2>
        选择，选择 - NSSegmentedControl
    </h2>
    <p>
        一个segmented control，是由
        <a href="https://developer.apple.com/reference/appkit/nssegmentedcontrol"
        target="_blank">
            NSSegmentedControl
        </a>
        类所代表的，它是当你需要从一些选项中做出一些选择时，对radio button的替代品。你可以在Xcode的Attributes Inspector中找到它：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/segmented-alignment.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/segmented-alignment.png"
            alt="segmented-alignment" width="504" height="190" class="aligncenter size-full wp-image-150265"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/segmented-alignment.png 504w, https://koenig-media.raywenderlich.com/uploads/2016/12/segmented-alignment-480x181.png 480w"
            sizes="(max-width: 504px) 100vw, 504px">
        </a>
    </p>
    <p>
        它是非常容易被使用的。你只需要获取或设置被选择的segment来找出用户的选择。
    </p>
    <pre lang="swift" class="hljs javascript">
<span class="hljs-comment">// Select the first segment</span>
segmentedControl.selectedSegment = <span class="hljs-number">0</span>

<span class="hljs-comment">// Get the selected segment</span>
<span class="hljs-keyword">let</span> selected = segmentedControl.selectedSegment
</pre>
    <h2>
        调节声音 - 添加Segmented Controls
    </h2>
    <p>
        如果你还记得，
        <code>
            readSentence()
        </code>
        方法含有一个控制语速（Normal, Fast, Slow）的参数。你将使用一个segmented control来改变语速。
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        并添加一个label到content view上面。将它的标题改为
        <em>
            Voice Speed:
        </em>
        。找到
        <em>
            Segmented Control
        </em>
        并将它拖拽到content view上面。你可以双击控件的每个segment来改变他的标题。将标题分别改为
        <em>
            Slow
        </em>
        ，
        <em>
            Normal
        </em>
        以及
        <em>
            Fast
        </em>
        。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/segmented-add-1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/segmented-add-1-650x400.png"
            alt="segmented-add" width="650" height="400" class="aligncenter size-large wp-image-153219"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/segmented-add-1-650x400.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/segmented-add-1-480x295.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/segmented-add-1.png 1536w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        在
        <code>
            ViewController
        </code>
        中为segmented control创建一个outlet，并命名为
        <em>
            voiceSegmentedControl
        </em>
        。现在，你想要在app一启动时选择Normal segment，它对应的序号是1（segment的序号是从0开始计算的）。打开
        <em>
            ViewController.swift
        </em>
        并添加下面的代码到
        <code>
            viewDidLoad()
        </code>
        ：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-comment">// Set the segmented control initial selection</span>
voiceSegmentedControl.selectedSegment = <span class="hljs-number">1</span>
</pre>
    <p>
        就像它看起来一样得容易。只需将
        <code>
            selectedSegment
        </code>
        的property设置为1。现在，运行项目，查看Normal segment是否已选中。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-selected.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-selected-286x320.png"
            alt="buildrun-selected" width="286" height="320" class="aligncenter size-medium wp-image-153220"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-selected-286x320.png 286w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-selected-446x500.png 446w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-selected.png 672w"
            sizes="(max-width: 286px) 100vw, 286px">
        </a>
    </p>
    <p>
        OK！你已经添加了所有创建你有趣的mad lib句子所需的控件。你所缺少的只是收集每一个控件的值，并将它们连接成一个句子，并将它们展示到屏幕上！
    </p>
    <h2>
        全部拉到一起
    </h2>
    <p>
        你需要再来两个控件展示结果：一个label用来展示完整的句子，已经用来展示图片的image view，使用户的交互显得更加有生气！
    </p>
    <p>
        打开
        <em>
            Main.storyboard
        </em>
        。在Object Library面板中找到
        <em>
            Wrapping Label
        </em>
        并将它拖拽到窗口上，就在
        <em>
            Go!!
        </em>
        按钮的下方。通过
        <em>
            Attributes Inspector
        </em>
        来让它看起来更漂亮：将border改为Frame，就是那四个按钮中的第一个。
    </p>
    <p>
        之后，双击label移除它的默认文本，选择文本并删除它。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/resulttext-add.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/resulttext-add-650x456.png"
            alt="resulttext-add" width="650" height="456" class="aligncenter size-large wp-image-153222"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/resulttext-add-650x456.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/resulttext-add-457x320.png 457w, https://koenig-media.raywenderlich.com/uploads/2017/01/resulttext-add.png 1508w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        现在你必须创建一个outlet以方便设置这个新的label的值，来容纳你的新的滑稽的桔子！就像之前一样，
        <em>
            按着Ctrl拖拽
        </em>
        label到
        <em>
            ViewController.swift
        </em>
        文件中并将property命名为
        <em>
            resultTextField
        </em>
        。
    </p>
    <p>
        现在，离开这个控件，让它停留在现在的样子；你将在稍候编写一些代码来填充它。
    </p>
    <h2>
        看到风景的房间 - NSImageView
    </h2>
    <p>
        Image View是一个非常简单易用的控件 - 惊喜！ - 展示一个图像。我敢打赌你都想不到是这样！:]
    </p>
    <p>
        <a href="https://www.raywenderlich.com/obvious" rel="attachment wp-att-27048">
            <img src="https://koenig-media.raywenderlich.com/uploads/2012/12/OBVIOUS.png"
            alt="" title="OBVIOUS" width="400" height="250" class="aligncenter size-full wp-image-27048">
        </a>
    </p>
    <p>
        在运行时，你需要和Image View的几个property进行交互：
    </p>
    <pre lang="swift" class="hljs javascript"><span class="hljs-comment">// Get the image from an image view</span>
<span class="hljs-keyword">let</span> myImage = myImageView.image

<span class="hljs-comment">// Set the image of an image view</span>
myImageView.image = myImage
</pre>
    <p>
        在设计的时候，你可以配置其外观：border, scaling和alignment。是的，这些property也可以在代码中进行设置，但在设计时在Interface Builder中设置它会更加容易，就像下面这样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/imageview-props.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/imageview-props-393x320.png"
            alt="imageview-props" width="300" height="244" class="aligncenter size-medium wp-image-150261"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/imageview-props-393x320.png 393w, https://koenig-media.raywenderlich.com/uploads/2016/12/imageview-props.png 508w"
            sizes="(max-width: 300px) 100vw, 300px">
        </a>
    </p>
    <h2>
        只为一个漂亮的脸 - 填充图像的“井”
    </h2>
    <p>
        是时候添加一个image view到你的app上了！在
        <em>
            Object Library
        </em>
        中找到
        <em>
            Image Well
        </em>
        并拖拽到view上，放到wrapping label的左边。如果必须的话，放心地去调整app窗口的大小。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/imagewell-add.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/imagewell-add-650x468.png"
            alt="imagewell-add" width="650" height="468" class="aligncenter size-large wp-image-153223"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/imagewell-add-650x468.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/imagewell-add-445x320.png 445w, https://koenig-media.raywenderlich.com/uploads/2017/01/imagewell-add.png 1467w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        用和你之前创建其它控件相同的方法，为image view创建一个新的outlet：
        <em>
            按着Ctrl拖拽
        </em>
        image view到
        <em>
            ViewController.swift
        </em>
        文件上，在弹出的窗口中将property命名为
        <em>
            imageView
        </em>
        。
    </p>
    <p>
        运行项目。你的app现在看起来应该是这样：
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-uifinished.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-uifinished-247x320.png"
            alt="buildrun-uifinished" width="247" height="320" class="aligncenter size-medium wp-image-153224"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-uifinished-247x320.png 247w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-uifinished-386x500.png 386w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-uifinished.png 672w"
            sizes="(max-width: 247px) 100vw, 247px">
        </a>
    </p>
    <p>
        哇！你的UI已经最终完成了 - 剩余的唯一一件事就是撰写代码来组装欢闹的句子，并填充你上面添加的image view！
    </p>
    <h2>
        是时候让它工作起来了
    </h2>
    <p>
        现在你需要基于那些输出来组装句子。
    </p>
    <p>
        当用户点击
        When the user clicks the
        <em>
            Go!
        </em>
        按钮的时候，你会从不同的控件中收集全部的值，来组装成完整的句子，然后在你之前添加的wrapping label中展示出来。
    </p>
    <p>
        然后，为了装饰全文界面，你会在你上一部分添加的image view上展示一个图片。
    </p>
    <p>
        为这个项目（正常地进入你的
        <em>
            下载
        </em>
        目录）。下载
        <a href="http://www.raywenderlich.com/downloads/MadLibs_face.zip">
            资源文件
        </a>
        。如果下载到的zip文件没有自动解压，就解压它，得到
        <em>
            face.png
        </em>
        图像文件。在
        <em>
            Project Navigator
        </em>
        中选择
        <em>
            Assets.xcassets
        </em>
        ，并将图片文件拖拽到assets列表中。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/assets.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/assets-650x266.png"
            alt="assets" width="650" height="266" class="aligncenter size-large wp-image-150272"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/assets-650x266.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/12/assets-480x196.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/assets.png 1580w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        现在是最终的时间来添加app的核心了 - 构建Mad Lib句子的代码！
    </p>
    <p>
        打开
        <em>
            ViewController.swift
        </em>
        并添加下列的property到类的实现中：
    </p>
    <pre lang="swift" class="hljs javascript">fileprivate <span class="hljs-keyword">var</span> selectedPlace: <span class="hljs-built_in">String</span> {
  <span class="hljs-keyword">var</span> place = <span class="hljs-string">"home"</span>
  <span class="hljs-keyword">if</span> rwDevConRadioButton.state == NSOnState {
    place = <span class="hljs-string">"RWDevCon"</span>
  }
  <span class="hljs-keyword">else</span> <span class="hljs-keyword">if</span> threeSixtyRadioButton.state == NSOnState {
    place = <span class="hljs-string">"360iDev"</span>
  }
  <span class="hljs-keyword">else</span> <span class="hljs-keyword">if</span> wwdcRadioButton.state == NSOnState {
    place = <span class="hljs-string">"WWDC"</span>
  }
  <span class="hljs-keyword">return</span> place
}
</pre>
    <p>
        上面的代码添加了一个计算型的property，它会根据哪个radio button被选中返回place的名称。
    </p>
    <p>
        现在，用以下的代码替换
        <code>
            goButtonClicked()
        </code>
        方法中的全部内容：
    </p>
    <pre lang="swift" class="hljs swift"><span class="hljs-comment">// 1</span>
<span class="hljs-keyword">let</span> pastTenseVerb = pastTenseVerbTextField.stringValue

<span class="hljs-comment">// 2</span>
<span class="hljs-keyword">let</span> singularNoun = singularNounCombo.stringValue
    
<span class="hljs-comment">// 3</span>
<span class="hljs-keyword">let</span> amount = amountSlider.integerValue
    
<span class="hljs-comment">// 4</span>
<span class="hljs-keyword">let</span> pluralNoun = pluralNouns[pluralNounPopup.indexOfSelectedItem]
    
<span class="hljs-comment">// 5</span>
<span class="hljs-keyword">let</span> phrase = phraseTextView.string ?? <span class="hljs-string">""</span>
    
<span class="hljs-comment">// 6</span>
<span class="hljs-keyword">let</span> dateFormatter = <span class="hljs-type">DateFormatter</span>()
dateFormatter.dateStyle = .long
<span class="hljs-keyword">let</span> date = dateFormatter.string(from: datePicker.dateValue)
    
<span class="hljs-comment">// 7</span>
<span class="hljs-keyword">var</span> voice = <span class="hljs-string">"said"</span>
<span class="hljs-keyword">if</span> yellCheck.state == <span class="hljs-type">NSOnState</span> {
  voice = <span class="hljs-string">"yelled"</span>
}
    
<span class="hljs-comment">// 8</span>
<span class="hljs-keyword">let</span> sentence = <span class="hljs-string">"On <span class="hljs-subst">\(date)</span>, at <span class="hljs-subst">\(selectedPlace)</span> a <span class="hljs-subst">\(singularNoun)</span> <span class="hljs-subst">\(pastTenseVerb)</span> <span class="hljs-subst">\(amount)</span> <span class="hljs-subst">\(pluralNoun)</span> and <span class="hljs-subst">\(voice)</span>, <span class="hljs-subst">\(phrase)</span>"</span>
    
<span class="hljs-comment">// 9</span>
resultTextField.stringValue = sentence
imageView.image = <span class="hljs-type">NSImage</span>(named: <span class="hljs-string">"face"</span>)

<span class="hljs-comment">// 10</span>
<span class="hljs-keyword">let</span> selectedSegment = voiceSegmentedControl.selectedSegment
<span class="hljs-keyword">let</span> voiceRate = <span class="hljs-type">VoiceRate</span>(rawValue: selectedSegment) ?? .normal
readSentence(sentence, rate: voiceRate)
</pre>
    <p>
        看起来有好多的代码，但当你把它拆开一部分一部分看时，每部分都是相当明确的：
    </p>
    <ol>
        <li>
            从
            <code>
                pastTenseVerbTextField
            </code>
            获取文本。
        </li>
        <li>
            在这部分代码中，你通过 
            <code>
                stringValue
            </code>
            property从combo box中或取字符串。你可能会问，为何不只在选中的行进行查阅，然后检索关联到这行的字符串。非常简单，这是因为用户可以输入它们自己的文本到combo box中，因此选择使用
            <code>
                stringValue
            </code>
            来获取当前的字符串，它既可以被选择，也可以被输入。
        </li>
        <li>
            接下来，使用
            <code>
                integerValue
            </code>
            方法读取slider当前的值。记住，如果你需要更精确的控件，你还可以使用
            <code>
                floatValue
            </code>
            或
            <code>
                doubleValue
            </code>
            。
        </li>
        <li>
            这里，你从popup button中获取了复数名词。这如何做到？在你的
            <code>
                pluralNouns
            </code>
            数组中使用下标语法，找到恰当的复数名词，并获取其
            <code>
                indexOfSelectedItem
            </code>
            property。
        </li>
        <li>
            接下来是用户输入的短语。要获取它，只需从
            <code>
                string
            </code>
            property中获取我们的text view的字符串的值。再一次，你使用了nil coalescing语法，因为这个property是可选的，它的值可能是
            <code>
                nil
            </code>
            。
        </li>
        <li>
            调用date picker的
            <code>
                dateValue
            </code>
            方法获取日期。然后使用
            <a href="http://developer.apple.com/library/mac/#documentation/Cocoa/Reference/Foundation/Classes/NSDateFormatter_Class/Reference/Reference.html"
            title="NSDateFormatter">
                NSDateFormatter
            </a>
            将其妆花为一个人类可读的字符串。
        </li>
        <li>
            你应该说还是喊？只需获取checkbox的状态：如果它是
            <code>
                NSOnState
            </code>
            ，指派
            <em>
                yelled
            </em>
            到字符串变量中。否则，让它使用默认的
            <em>
                said
            </em>
            。
        </li>
        <li>
            现在，你已经收集了所有你构建mad lib句子所需要的信息！这是神奇的事将发生的地方，基于用户的输出，从各种控件中的不同的值构建成了一个字符串。
        </li>
        <li>
            现在你所有你努力工作所得出的结果了可以进行展示了！首先，通过设置results label的
            <code>
                stringValue
            </code>
            property来展示最终的句子。然后，通过向用户展示一副图像，来给app添加一些魅力，这和加载图像并设置image view控件的property一样得简单。
        </li>
        <li>
            最后，大声地说出来吧！从当前被选择的segment获取语速，并调用将文本转换为朗读的方法。
        </li>
    </ol>
    <p>
        就是这个！你已经完成了！运行项目app，你已可以为自己构建一些欢闹的句子。
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-final.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-final-247x320.png"
            alt="buildrun-final" width="247" height="320" class="aligncenter size-medium wp-image-153225"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-final-247x320.png 247w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-final-386x500.png 386w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-final.png 672w"
            sizes="(max-width: 247px) 100vw, 247px">
        </a>
    </p>
    <p>
        祝贺 - 你已经完成了构建Mad Lib app，并沿途学习了大量关于最常用macOS控件的知识。
    </p>
    <p>
        随意玩弄控件，选择不同的值，输入有趣的名称或动词，每次点击
        <em>
            Go!
        </em>
        按钮时来查看你创建了一个多么有趣的故事！:]
    </p>
    <h2>
        从这儿去向哪里？
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
        这里是包含这篇教程中全部代码的
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibs-part2-final-1.zip">
            最终项目
        </a>
        。
    </p>
    <p>
        为了获得对macOS控件的更深的理解，我推荐你去阅读下表列出的苹果编程指南，它们包含了大量的关于如何使用可用的控件的信息。
    </p>
    <p>
        特别低，我强烈地推荐你阅读
        <a href="https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/OSXHIGuidelines/"
        title="macOS Human Interface Guidelines">
            macOS人机交互指南
        </a>
        。这篇指导解释了关于macOS用户交互的概念和理论，以及苹果对于开发人员如何使用控件和设计他们UI的期望，来提供一致和令人愉快的体验。任何想要为Mac平台进行开发的人都应当去阅读一下，尤其计划要通过Mac App Store发布它们的应用的时候。
    </p>
    <p>
        这里有一些有用的链接来增强，或更进一步地探索你在这篇教程中学到的概念：
    </p>
    <ul>
        <li>
            <a href="https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/OSXHIGuidelines/"
            title="macOS Human Interface Guidelines" target="_blank">
                macOS Human Interface Guidelines
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/Button/Button.html#//apple_ref/doc/uid/10000019i"
            title="Button Programming Topics" target="_blank">
                Button Programming Topics
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/AttributedStrings/AttributedStrings.html"
            title="Attributed String Programming Guide" target="_blank">
                Attributed String Programming Guide
            </a>
        </li>
        <li>
            <a href="http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/ComboBox/ComboBox.html#//apple_ref/doc/uid/10000020i"
            title="Combobox Guide" target="_blank">
                Combo Box Programming Topics
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/SegmentedControl/Articles/SegmentedControlBasics.html"
            title="Segmented Control Guide" target="_blank">
                Segmented control Programming Topics
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/MenuList/MenuList.html#//apple_ref/doc/uid/10000032i"
            title="Application Menu and Popup Programming Topics" target="_blank">
                Application Menu and PopUp Programming Topics
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/mac/documentation/GraphicsImaging/Conceptual/ImageKitProgrammingGuide/Introduction/Introduction.html"
            title="Image Kit Programming Guide" target="_blank">
                Image Kit Programming Guide
            </a>
        </li>
    </ul>
</div>
