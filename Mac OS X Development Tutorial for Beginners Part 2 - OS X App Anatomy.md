# macOS X 初学者开发教程 第二部分 OS X App剖析

#### [原文地址](https://www.raywenderlich.com/110267/mac-os-x-development-tutorial-beginners-part-2-os-x-app-anatomy) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <img class="alignright size-full wp-image-110249 bordered" src="https://koenig-media.raywenderlich.com/uploads/2015/07/250x250.png"
        alt="250x250" width="250" height="250" srcset="https://koenig-media.raywenderlich.com/uploads/2015/07/250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2015/07/250x250-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/07/250x250-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2015/07/250x250-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2015/07/250x250-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
        欢迎回到我们三个部分的Mac OS X新手开发教程系列！
    </p>
    <ol>
        <li>
            在
            <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Mac%20OS%20X%20Development%20Tutorial%20for%20Beginners%20Part%201%20-%20Intro%20to%20Xcode.md"
            sl-processed="1">
                第一部分
                part 1
            </a>
            你学到了怎样获取你需要的用来OS X开发的工具。接下来，使用了一个你下载的app作为例子，你进行了一次OS X的游览，发现了怎么执行app，编辑代码，设计UI和调试它。
        </li>
        <li>
            在第二部分，你将从Xcode退回一步来了解一下构成OS X app的组件。从一个app怎么启动，到UI怎么构建，直到处理用户的交互
        </li>
        <li>
            在<a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Mac%20OS%20X%20Development%20Tutorial%20for%20Beginners%20Part%203%20-%20Your%20First%20OS%20X%20App.md"
            sl-processed="1">最后一部分</a>， 你将亲自动手（get your hands dirty）- 构建你史无前例的第一个OS X app。从一无所有开始，你将很快地拥有一个简单的app，并运行在你的mac上！
        </li>
    </ol>
    <p>
        这篇文章是定位于那些完成了这个系列
        <a href="http://www.raywenderlich.com/110170/mac-os-x-development-tutorial-for-beginners-part-1-intro-to-xcode"
        sl-processed="1">
            part one
            第一部分
        </a>
        ，或拥有使用Xcode经验的人。它假设你没有或很少关于OS X app的知识，并且如果你早已熟悉OS X app的架构，你可以略过这里直到
        <a href="http://www.raywenderlich.com/110269/mac-os-x-development-tutorial-for-beginners-part-3-your-first-os-x-app"
        sl-processed="1">
            最后一部分
        </a>
        之前。
    </p>
    <p>
        到这篇文章最后的时候，你将有一个对于OS X app不同的部分怎么配合到一起的很好的掌控，尽管不必理解他们中的每一个都是怎么工作的。
    </p>
    <div class="note">
        <p>
            <em>
                注意：
            </em>
            系列的这一部分，仅仅是你需要知道的OS X app怎么工作的背景信息；不涉及到写代码。
        </p>
        <p>
            休息一下，放松，然后学习 - 你将在下一个，也是这个系列的最后一部分，回到编码并制作你的第一个OS X app！
        </p>
    </div>
    <h2>
        OS X App怎么启动？
    </h2>
    <p>
    	你的OS X app旅程已开始 - 着眼于一个app实际上上是怎么
        <i>
            启动
        </i>
        的。
    </p>
    <p>
    	当考虑到OS X app启动进程时，你需要考虑到三个组件：
    </p>
    <ul>
        <li>
            <em>
                App Delegate
            </em>
            ：代码的入口。App Delegate提供了关连于app生命循环的方法，并与操作系统进行交互。这是你的第一次执行代码的机会，并提供了你来自OS X的通知，例如Handoff请求，命令行参数和推送通知。
        </li>
        <li>
            <em>
                Storyboard
            </em>
            ：Storyboards有一个指定的“入口点”，他让系统在app启动时构建UI。entrypoint看起来像一个在场景（scene）左手边的箭头：
            <br>
            <img class="aligncenter size-full wp-image-111915" src="https://koenig-media.raywenderlich.com/uploads/2015/08/storyboard_entry.png"
            alt="storyboard_entry" width="264" height="164">
            <br>
            这表示storyboard中的这个场景将构成你的app的初始UI。
        </li>
        <li>
            <em>
                Info.plist
            </em>
            ：在你的app中，你可以有多个storyboard，OS X怎么知道该使用哪一个作为初始的UI？这个信息（和大量其它有用的东西）保存在
            <em>
                Info.plist
            </em>
            文件中。你可以在下面看到关联的入口：
            <img class="aligncenter size-medium wp-image-111908" src="https://koenig-media.raywenderlich.com/uploads/2015/08/info_plist-480x245.png"
            alt="info_plist" width="480" height="245" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/info_plist-480x245.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/info_plist-700x357.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/info_plist.png 1238w"
            sizes="(max-width: 480px) 100vw, 480px">
            <p>
            	这个文件包含了大量有用的配置选项，其中很多被暴露在Xcode的target配置的界面中。下面的图片展示了相同的storyboard设置位于更对用户友好的位置上：
            </p>
            <p>
                <img class="aligncenter wp-image-111912 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/08/project_config-700x436.png"
                alt="project_config" width="700" height="436" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/project_config-700x436.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/project_config-480x299.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/project_config.png 1448w"
                sizes="(max-width: 700px) 100vw, 700px">
            </p>
        </li>
    </ul>
    <p>
    	启动一个app比这要
        <i>
        	稍
        </i>
        复杂些。但这三个地方解释了，你可以在什么地方交互和配置你的app的启动。现在你建立起了你的app，并运行起来，是时候来看一个重要的方面了 - 它的用户交互。
    </p>
    <h2>
    	用户界面
    </h2>
    <p>
    	你早已认识到UI可以由storyboard提供这个事实，但这实际上意味着什么？在这个部分你将cover到不同的UI组件 - 他们代表什么及它们怎么配合在一起。
    </p>
    <p>
        <img class="aligncenter size-large wp-image-111919" src="https://koenig-media.raywenderlich.com/uploads/2015/08/app_components-632x500.png"
        alt="app_components" width="632" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/app_components-632x500.png 632w, https://koenig-media.raywenderlich.com/uploads/2015/08/app_components-405x320.png 405w, https://koenig-media.raywenderlich.com/uploads/2015/08/app_components.png 1442w"
        sizes="(max-width: 632px) 100vw, 632px">
    </p>
    <h3>
        Window
    </h3>
    <p>
    	你的app的UI将被一个或多个window对象包含。这些表现了你的app，负责提供UI的屏幕上的区域。操作系统会执行一个window管理器来处理移动和缩放这些window，在用户做出改变时更新你的app。
    </p>
    <p>
    	除了可视化你的app之外，window对象也处理传递通过用户和鼠标键盘交互到你的app中而触发的事件。
    </p>
    <p>
    	尽管你可以直接和window对象交互，但通常它们是被window controller控制的 - 尤其当结合storyboard使用的时候。
    </p>
    <p>
    	window controller负责加载它自己的window，让你能够hook贯穿于window生命周期的不同的事件。
    </p>
    <p>
    	一个storyboard会包含至少一个window controller，就像下面这样：
    </p>
    <p>
        <img class="aligncenter wp-image-111918 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/08/window_controller-475x320.png"
        alt="window_controller" width="475" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/window_controller-475x320.png 475w, https://koenig-media.raywenderlich.com/uploads/2015/08/window_controller-700x471.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/window_controller.png 1078w"
        sizes="(max-width: 475px) 100vw, 475px">
    </p>
    <p>
    	<code>
            NSWindowController
        </code>
    	这个类代表了Window controller，因此当你需要配置不同的window时，你通常就需要创建不同的子类来管理它们各自的行为。
    </p>
    <h3>
        Views
    </h3>
    <p>
        window指定了你的app在屏幕上负责绘制的区域，但不是要绘制的东西。这就是view的主要职责之一 - 为你提供在屏幕上绘制的功能。
    </p>
    <p>
        View是矩形的，由
        <code>
            NSView
        </code>
        来表示。View存在在层级中 - 也就是说，任何view都可以包含0个或多个subview - 让你能够用更简单，可重用的view组件来构成复杂的布局。
    </p>
    <h3>
        View Controllers
    </h3>
    <p>
        就如同window在storyboard中是被一个window controller来管理的，view是被window controller类来管理的。这就使用模型层通过直接操作property，或通过Cocoa绑定来连接了view的层级。
    </p>
    <p>
        在一个典型的应用中，view controller是一个可重用的组件，当对一个特定的类型提供了模型的对象，就会更新所有构成它的view，来表现相关的模型对象的值。
    </p>
    <p>
        例如，在之前的教程中，你“闲逛”（poke around）了
        <em>
            HubEvent
        </em>
        这个app。
    </p>
    <p>
        <img class="aligncenter wp-image-111920 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/08/view_controllers-480x311.png"
        alt="view_controllers" width="480" height="311" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/view_controllers-480x311.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/view_controllers-700x453.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/view_controllers.png 1232w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        在上面的截图中，你可以看到它是由两个主要的view controller构成的 - 一个管理在顶部的table view，另一个管理详细的text view。当你的table view中选择一行，它设置了模型对象在较低细节的view controller，然后更新text view去展示了正确的JSON。
    </p>
    <p>
        View controller是由
        <code>
            NSViewController
        </code>
        来表现的，它提供了全范围的生命周期的事件 - 允许你在不同的时刻执行定制的动作。例如你可以在当view将要出现在屏幕上时，用这个方法
        <code>
            viewWillAppear()
        </code>
        来启动动画，或在view的层次已正确地装载时，使用填数据充相关的view在这个方法中
        <code>
            viewDidLoad()
        </code>
        。
    </p>
    <p>
        你的app有可能是由一系列
        <code>
            NSViewController
        </code>
        定制的子类来构成的，每一个都负责window中不同的部分。它们是一个app中非常重要的一方面 - 形成允许你展示基础的（underlying）数据给用户的连接。
    </p>
    <h3>
        View组件
    </h3>
    <p>
        你已知道了view是用来被绘制到屏幕上的 - 但它实际上是怎么实现的？在最低层你可以创建一个
        <code>
            NSView
        </code>
        定制的子类并重写
        <code>
            drawRect()
        </code>
        方法来手动地绘制你的view的内容。
    </p>
    <p>
        这是极其强大的 - 允许你创建完全定制的view，如果你不得不绘制一些文本到屏幕上去，将会非常费劲！
    </p>
    <p>
        幸运的是，你不必这么做。AppKit包含一系列常用的
        <code>
            NSView
        </code>
        的子类，可以用来在屏幕上展示内容。
    </p>
    <p>
        一些最有用的例子是：
    </p>
    <ul>
        <li>
            <em>
                Label
            </em>
            ：展示静态的文本。配置字体和外观
            <br>
            <img class="aligncenter wp-image-111909 size-full" src="https://koenig-media.raywenderlich.com/uploads/2015/08/label.png"
            alt="" width="430" height="120">
        </li>
        <li>
            <em>
                Text Field
            </em>
            ：用户可编辑的文本控制器。用来从用户那里手机字符串。
            <br>
            <img class="aligncenter size-full wp-image-111917" src="https://koenig-media.raywenderlich.com/uploads/2015/08/text_field.png"
            alt="text_field" width="474" height="110">
        </li>
        <li>
            <em>
                Image View
            </em>
            ：绘制一副图像 - 由
            <code>
                NSImage
            </code>
            对象提供。
            <br>
            <img class="aligncenter size-full wp-image-111907" src="https://koenig-media.raywenderlich.com/uploads/2015/08/image_view.png"
            alt="image_view" width="468" height="108">
        </li>
        <li>
            <em>
                Push Button
            </em>
            ：是众多按钮类型中的一种 - 相应用户点击事件的那个。
            <br>
            <img class="aligncenter size-full wp-image-111913" src="https://koenig-media.raywenderlich.com/uploads/2015/08/push_button.png"
            alt="push_button" width="470" height="88">
        </li>
        <li>
            <em>
                Table View
            </em>
            ：一个用来展示不止
            <i>
                一
            </i>
            个数据对象，而是展示它们的集合的例子，它是view的很多子类中的一个。
            <br>
            <img class="aligncenter size-full wp-image-111916" src="https://koenig-media.raywenderlich.com/uploads/2015/08/table_view.png"
            alt="table_view" width="490" height="112" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/table_view.png 490w, https://koenig-media.raywenderlich.com/uploads/2015/08/table_view-480x110.png 480w"
            sizes="(max-width: 490px) 100vw, 490px">
        </li>
    </ul>
    <p>
        这些只是几个不同的对你可用的view的子类，你可以用来构建你的app的用户界面。在Interface Builder，你可以在对象库中发现所有的子类：
    </p>
    <p>
        <img class="aligncenter size-large wp-image-111911" src="https://koenig-media.raywenderlich.com/uploads/2015/08/object_library-383x500.png"
        alt="object_library" width="383" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/object_library-383x500.png 383w, https://koenig-media.raywenderlich.com/uploads/2015/08/object_library-245x320.png 245w, https://koenig-media.raywenderlich.com/uploads/2015/08/object_library.png 522w"
        sizes="(max-width: 383px) 100vw, 383px">
    </p>
    <p>
        raywenderlich.com OS X教程团队也将在未来几个月中，打造一个快速的对于不同UI组建的参考指南 - 所以请确保回来查阅。
    </p>
    <h3>
        Viewing collections
    </h3>
    <p>
        你经常想要你的app的UI同时展示多个模型对象 - 例如一个即将到来的约会的列表，或一个相册中照片的集合。
    </p>
    <p>
        OS X提供两个不同的view用来展示模型对象的集合 - 以table view的形式和collection view的形式。
    </p>
    <p>
        如同它的名字，table view用来展示扁平的数据，使用行来表示个体的数据模型，列来表示那些对象的属性。
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-111922" src="https://koenig-media.raywenderlich.com/uploads/2015/08/table_view_sample-480x145.png"
        alt="table_view_sample" width="480" height="145" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/table_view_sample-480x145.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/table_view_sample-700x212.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/table_view_sample.png 1220w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        Table view由可以在被滚入和滚出屏幕时，可以被回收利用的cell构成。数据可以通过数据源协议或使用Cocoa Bindings来提供。
    </p>
    <p>
        Table支持排序，编辑和定制cell，给你一个强有力的view来展示数据。
    </p>
    <p>
        更通用的collection view也是由cell的集合构成的，但这次，每个cell代表全部的模型对象。这些cell的布局是完全可定制的。
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-111902" src="https://koenig-media.raywenderlich.com/uploads/2015/08/collection_view-475x320.png"
        alt="collection_view" width="475" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/collection_view-475x320.png 475w, https://koenig-media.raywenderlich.com/uploads/2015/08/collection_view-700x472.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/collection_view.png 1314w"
        sizes="(max-width: 475px) 100vw, 475px">
        <img class="aligncenter wp-image-111903 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/08/collection_view_circle-480x308.png"
        alt="collection_view_circle" width="480" height="308" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/collection_view_circle-480x308.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/collection_view_circle-700x449.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/collection_view_circle.png 1234w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        类似table view，collection view可以通过数据源或Cocoa Bindings来提供。它的cell也是可以回收利用的 - 当它们从view中消失的时候，以此减少内存的占用。
    </p>
    <p>
        Collection view内置了cell选择的支持，带动画的重新排序，以及将cell分组到部分中。
    </p>
    <h3>
        处理用户交互
    </h3>
    <p>
        对于任何OS X，一个关键的部分就是通过鼠标、触控板、键盘和任何其它大量的输入设备来进行用户交互。为了帮助设计用户的输入到你的app，OS X提供了一个统一的事件派发模型，构建于一个响应者链的概念下。
    </p>
    <p>
        生成自键盘的事件称作
        <em>
            Key Events
        </em>
        ，这些会跟随一个相当复杂的路径到达你的app。一些键的点击甚至不会将事件传递给你的app - 它们被拦截在操作系统的层级上（例如：电源按钮，屏幕亮度，音量）。
    </p>
    <p>
        键的事件可以表示一个单独的键，或一个键的组合 - 当事件到达你的app时，它们会首先被检查是不是一个对应于菜单项的快捷键。
    </p>
    <p>
        如果不是的话，它们就会被检查是不是用来引导你的app的用户交互的 - 例如：在输入框之间切换。如果这个不是这种情况，window会在传递键事件前，确定出哪个view当前是活跃的（所谓的第一响应者）。这些可以被打断作为每个视图的命令，或作为字符来插入。
    </p>
    <p>
        键盘输入确实相当复杂，因为它可以影响到很多层的系统和app架构，但OS X走了一大段路来帮助这个处理。在很多情形下，你会发现它表现的就像你期望的一样的“开箱即用”（out of the box）。
    </p>
    <p>
        类鼠标事件（mouse-like event）传递到你的应用中，在传递它们到你定制的子类，使你能够恰当地操作它们之前，确立它们执行在哪个window和相应view上。响应者类（view继承自的）包含你可以重写的，在点击或移动鼠标时会调用的方法。
    </p>
    <p>
        触控板相对于传统的鼠标，提供了很多额外的手势，因此gesture recognizer的概念是从iOS借来的。这些可以用来将一系列的多指触控解释为一个语义上的动作，例如移动和旋转。
    </p>
    <p>
        Gesture recognizer对类鼠标事件提供了更高水平的解释，它们被关联到view，并拦截所有关联到那个view的类鼠标事件。
    </p>
    <p>
        在OS X中，事件处理架构相当地复杂，但默认走了一大段路来处理很多共同的情形。相应者链的力量使其在最高水平的可能上，让操纵事件变得容易。
    </p>
    <h3>
        Menus
    </h3>
    <p>
        Menus是关联到你的app的不同动作的集合。Menus可以出现在不同的地方，包括：
    </p>
    <ul>
        <li>
            <em>
                Menu Bar
            </em>
            这是沿着屏幕顶部的“条”
            <br>
            <img class="aligncenter size-medium wp-image-111910" src="https://koenig-media.raywenderlich.com/uploads/2015/08/menu_bar-480x283.png"
            alt="menu_bar" width="480" height="283" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/menu_bar-480x283.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/menu_bar-700x412.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/menu_bar.png 842w"
            sizes="(max-width: 480px) 100vw, 480px">
        </li>
        <li>
            <em>
                Context Menus（交互菜单）
            </em>
            出现在用户右击时
            <br>
            <img class="aligncenter size-medium wp-image-111904" src="https://koenig-media.raywenderlich.com/uploads/2015/08/context_menu-480x291.png"
            alt="context_menu" width="480" height="291" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/context_menu-480x291.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/context_menu.png 578w"
            sizes="(max-width: 480px) 100vw, 480px">
        </li>
        <li>
            <em>
                Dock Menu
            </em>
            当用户长按dock的图标时
            <br>
            <img class="aligncenter size-medium wp-image-111905" src="https://koenig-media.raywenderlich.com/uploads/2015/08/dock_menu-270x320.png"
            alt="dock_menu" width="270" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/dock_menu-270x320.png 270w, https://koenig-media.raywenderlich.com/uploads/2015/08/dock_menu-422x500.png 422w, https://koenig-media.raywenderlich.com/uploads/2015/08/dock_menu.png 466w"
            sizes="(max-width: 270px) 100vw, 270px">
        </li>
    </ul>
    <p>
        所有的menus可以在Interface Builder中被配置，允许你配置它们的外观，它们出现的层级，和每一项关联的动作。
    </p>
    <p>
        <img class="aligncenter size-medium wp-image-111906" src="https://koenig-media.raywenderlich.com/uploads/2015/08/ib_menu-480x127.png"
        alt="ib_menu" width="480" height="127" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/ib_menu-480x127.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/ib_menu-700x185.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/ib_menu.png 884w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <h2>
        数据层
    </h2>
    <p>
        用户界面是你OS X app的一个巨大的部分，但它大概不是你app的
        <i>
            全部
        </i>
        。大多app提供一个用户界面，来让用户可以和背后的数据模型交互。
    </p>
    <p>
        数据模型高度依赖于你的app存在的域（domain） - 并没有魔术的办法来build一个数据层。事实上，通常的情形是，你会使用Swift中可用的，面向对象语言的特性来创建一套模拟你app的域（domain）的对象。
    </p>
    <p>
        让数据层和用户界面分类是极其重要的，让你的软件更易维护和不易出错。OS X通过Cocoa Bindings支持这种架构 - 一种接通模型对象到UI，并确保它们自动保持互相同步的技术。
    </p>
    <p>
        你可以穿件一个完全隔离的动态framework来包含你的数据层 - 完全和UI隔离。这可以让相同的数据层在多个app中被使用 - 甚至再OS X和iOS app之间，增强可测试性。
    </p>
    <p>
        尽管你可以创建你自己的数据层，苹果提供了一个名叫Core Data的框架。这是一个综合框架，用来创建对象图（object graph）来完成你全部数据层的模型。它支持持久化到磁盘，数据校验，撤销等。
    </p>
    <p>
        Core Data很好地支持了Cocoa Bindings，意味着整合你的模型编辑UI和Core Data后端真的容易，这使得build你大部分的app相当得快。
    </p>
    <h2>
        其它有用的Cocoa功能
    </h2>
    <p>
    	这篇文章给了你一些可以被用到每个OS Xapp的Cocoa概念的非常简短的概述。这仅仅触碰到了这个非常丰富的平台的表面。
    </p>
    <p>
    	一些Cocoa的其它突出的部分，在build强大的OS X app时也是非常有用的：
    </p>
    <ul>
        <li>
            <em>
                Networking
            </em>
            ：除了访问最底层的网络功能，OS X提供了一个更高层的API来处理HTTP请求。networking构建在一个异步的session上 - 无缝地将上传和下载处理成一个任务的列表。
        </li>
        <li>
            <em>
                Location
            </em>
            ：你可能主要在移动设备上关联到基于位置的服务，但你有完全的访问权限，来通过Core Location访问很多关于位置的强大的功能，并使用MapKit处理地图。
        </li>
        <li>
            <em>
                WebKit
            </em>
            ：Safari是顶级的web浏览器之一，你可以通过WebKit来整合强有力的渲染引擎（rendering engine）到你自己的app中。它也包含了与内容交互的能力，并可以从一系列的来源中渲染HTML的内容。
        </li>
    </ul>
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
        这篇文章给了你OS X的app怎么配合在一起的概述，但它没有给你你改怎么实际地使用这些来启动创建app的好主意。不要担心 - 这恰是这个引导性系列中
        <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Mac%20OS%20X%20Development%20Tutorial%20for%20Beginners%20Part%203%20-%20Your%20First%20OS%20X%20App.md"
        sl-processed="1">
            下一篇文章
        </a>
        的目标。
    </p>
    <p>
        如果你想学习更多关于build OS X app理论方面的内容，苹果提供了一个好的Cocoa app的引导作为文档引导的一部分。它在实际build app上并不是特别有用，但是你如果全部读过它，你将对Cocoa拥有可怕的知识！
    </p>
</div>
