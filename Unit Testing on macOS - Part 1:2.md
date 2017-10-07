# 单元测试：1/2部分

#### [原文地址](https://www.raywenderlich.com/141405/unit-testing-macos-part-12) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-250x250.png"
            alt="Unit-Testing-macOS" width="250" height="250" class="alignright size-thumbnail wp-image-142750"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-128x128.png 128w"
            sizes="(max-width: 250px) 100vw, 250px">
        </a>
    </p>
    <p>
        单元测试是我们都深深知道需要去做的事之一，但看起来非常得困难和无聊，是一个很辛苦的工作。
    </p>
    <p>
        编写代码去完成令人激动的事情是多么得有趣，为何人们要花费一半的时间编写代码只是为了进行测试？
    </p>
    <p>
        为了
        <em>
            把握性
        </em>
        ！在本教程中，你将学习如何测试你的代码，以此增强对代码能够正确完成你所期望事情，适应变化，不造成问题的把握力。
    </p>
    <h2>
        入门
    </h2>
    <p>
        本项目使用Swift 3语言，Xcode 8 beta 6以上版本。下载
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/08/HighRoller-starter.zip"
        sl-processed="1">
            起始项目
        </a>
        并打开。
    </p>
    <p>
        假如你已完成过raywenderlich.com中这里的其它教程，你可能会期望拿到这里运行。但这次不会去测试这些。点击
        <em>
            Product
        </em>
        菜单并选择
        <em>
            Test
        </em>
        。注意快捷键 —
        <em>
            Command-U
        </em>
        — 你将在本教程中使用多次。
    </p>
    <p>
        当你运行测试时，Xcode将构建app，你会看到几秒钟app的窗口，然后才给出信息“Test Succeeded”。在左侧的
        <em>
            Navigator
        </em>
        面板中，选择
        <em>
            Test navigator
        </em>
        。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/TestNavigator2.png"
        alt="TestNavigator2" width="513" height="346" class="aligncenter size-full wp-image-141436"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/TestNavigator2.png 513w, https://koenig-media.raywenderlich.com/uploads/2016/08/TestNavigator2-474x320.png 474w"
        sizes="(max-width: 513px) 100vw, 513px">
    </p>
    <p>
        这里展示了默认添加的三个测试；每个的旁边都有一个绿色的标记，表示该测试已通过。要查看包含这些测试的文件，可以点击
        <em>
            Test Navigator
        </em>
        中的第二行
        <em>
            High RollerTests
        </em>
        ，它带有一个大写T的图标，表示其层级更高。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/DefaultTests3.png"
        alt="DefaultTests3" width="700" height="395" class="aligncenter size-full wp-image-142138"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/DefaultTests3.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/08/DefaultTests3-480x271.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/DefaultTests3-650x367.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/DefaultTests3-266x151.png 266w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        这里有一些很重要的事值得注意：
    </p>
    <ul>
        <li>
            导入的
            <em>
                XCTest
            </em>
            是由Xcode提供的测试框架。
            <code>
                @testable import High_Roller
            </code>
            则让代码可以访问
            <code>
                High_Roller
            </code>
            模块中的所有代码。每个测试文件都需要这样的两个导入。
        </li>
        <li>
            <code>
                setup()
            </code>
            和
            <code>
                tearDown()
            </code>
            ：两个方法会在:
            <em>
                每个单个的
            </em>
            测试方法被调用之前和之后调用。
        </li>
        <li>
            <code>
                testExample()
            </code>
            和
            <code>
                testPerformanceExample()
            </code>
            ：实际的测试。第一个测试功能，第二个则测试性能。每个测试方法的名称都必须以: 
            <code>
                test
            </code>
            开头，这样才能被Xcode识别为一个测试的方法去执行。
        </li>
    </ul>
    <h3>
        神马是单元测试？
    </h3>
    <p>
        在你开始编写你的测试之前，我们需要进行一个简短的讨论，单元测试到底是什么，你为何应当使用它。
    </p>
    <p>
        单元测试是用来测试你的一段代码的功能。它并不包含在你的app之中，但可以在开发期间测试代码是否符合你的期望。
    </p>
    <p>
        对于单元测试，常见的第一反应是：“你要我写
        <i>
            两次
        </i>
        的代码？一次为了app本身，
        <i>
            另一次
        </i>
        则用来测试这个方法？”实际上有可能比这更糟 — 一些项目的测试代码可能会比产品本身的代码
        <i>
            更多
        </i>
        。
    </p>
    <p>
        首先，看起来这非常浪费时间和精力 — 但当一个测试捕捉到了你之前未注意过的问题，或警告你出现了副作用的时候，你就会明白它是一个多么棒的工具了。慢慢地，你就会感到一个没有单元测试的项目是多么得脆弱，你做出任何的改动都会顾虑重重，因为你无法确定将会发生什么。
    </p>
    <h2>
        测试驱动开发
    </h2>
    <p>
        测试驱动开发（Test Driven Development TDD）是单元测试的一个分支，你会从这里开始测试，且只编写测试所需求的代码。这一开始看起来是个非常奇怪的处理方式，且会产生一些非常奇怪的代码。但最终你会发现，它可以在你编码之前帮助你思考编码的目的。
    </p>
    <p>
        TDD有三个重复的步骤：
    </p>
    <ol>
        <li>
            <em>
                红色
            </em>
            ：编写一个失败的测试。
        </li>
        <li>
            <em>
                绿色
            </em>
            ：编写可以使测试通过的最小代码集。
        </li>
        <li>
            <em>
                重构
            </em>
            ：可选的步骤；如果一个任何的app或测试代码可以通过重构来让它变得更好，那就这么做。
        </li>
    </ol>
    <p>
        对于有效的TDD，顺序是非常重要和关键的。修复一个失败的测试，可以帮助你了解代码到底在做什么。如果你的测试在没有任何新编写代码的情况下，第一次就通过了，你就无法确知下一阶段的开发该做些什么。
    </p>
    <p>
        开始，你将使用TDD编写一系列测试和伴随的代码。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/dog-239x320.png"
        alt="dog" width="239" height="320" class="alignright size-medium wp-image-142110"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/dog-239x320.png 239w, https://koenig-media.raywenderlich.com/uploads/2016/08/dog-373x500.png 373w, https://koenig-media.raywenderlich.com/uploads/2016/08/dog.png 954w"
        sizes="(max-width: 239px) 100vw, 239px">
    </p>
    <h2>
        测试项目
    </h2>
    <p>
        这个项目是棋盘玩家的投骰子工具。有过和家人坐在一起玩游戏，但发现骰子却被狗吃了的经历么？这个App可以帮助你解决烦恼。如果有人说“我不相信计算机不会作弊！”你就可以自豪地说这个app已通过了单元测试，证明它可以正确地工作。这一定会给你的家人留下深刻的印象 — 让你们今晚的游戏可以继续下去。:]
    </p>
    <p>
        这个app的model包含两个主要的对象类型：一个是
        <code>
            Dice
        </code>
        ，它包含一个
        <code>
            value
        </code>
        property和一个用来生成任意值的方法；另一个是
        <code>
            Roll
        </code>
        ，它含有一个
        <code>
            Dice
        </code>
        对象的集合，并附有一起滚动骰子，计算总值等等的方法。
    </p>
    <p>
        第一个测试类针对的是
        <code>
            Dice
        </code>
        对象类型。
    </p>
    <h2>
        Dice测试类
    </h2>
    <p>
        在Xcode中切到
        <em>
            File Navigator
        </em>
        并选择
        <em>
            High RollerTests
        </em>
        组。选择
        <em>
            File/New/File…
        </em>
        ，然后点击
        <em>
            macOS/Unit Test Case Class
        </em>
        。点击
        <em>
            Next
        </em>
        并将类命名为
        <code>
            DiceTests
        </code>
        。语言设为Swift。点击
        <em>
            Next
        </em>
        及
        <em>
            Create
        </em>
        。
    </p>
    <p>
        选择类内部的全部代码并删除。添加下列的代码到
        <em>
            DiceTests.swift
        </em>
        中，就在
        <code>
            import XCTest
        </code>
        这行的下方：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@testable</span> <span class="hljs-keyword">import</span> High_Roller
</pre>
    <p>
        现在你就可以删除
        <em>
            HighRollerTests.swift
        </em>
        了，因为你不再需要默认的测试。
    </p>
    <p>
        第一件要测试的事是
        <code>
            Dice
        </code>
        对象可否被创建。
    </p>
    <h3>
        你的第一个测试
    </h3>
    <p>
        在
        <em>
            DiceTests
        </em>
        类中，添加下列的测试方法：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testForDice</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">let</span> <span class="hljs-number">_</span> = <span class="hljs-type">Dice</span>()
  }
</pre>
    <p>
        在你运行测试之前，这里会爆出一个编译错误：
        <code>
            "Use of unresolved identifier 'Dice'"
        </code>
        。在TDD中，一个未能编译通过的测试会被认做是失败的测试，因此你现在只是完成了TDD顺序中的第一步。
    </p>
    <p>
        要用最少的代码使这里的代码测试通过，切到
        <em>
            File Navigator
        </em>
        ，并在主
        <em>
            High Roller
        </em>
        组中选择
        <em>
            Model
        </em>
        组。点击
        <em>
            File/New/File…
        </em>
        创建一个新的Swift文件并命名为
        <em>
            Dice.swift
        </em>
        。
    </p>
    <p>
        添加下列的代码到文件中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">struct</span> <span class="hljs-title">Dice</span> </span>{

}
</pre>
    <p>
        回到
        <em>
            DiceTests.swift
        </em>
        ，在下次构建之前，错误并不会消失。然而，你现在可以以几种不同的方式来运行测试。
    </p>
    <p>
        如果你点击测试方法旁边的菱形，就
        <em>
            只会运行这一个测试
        </em>
        。现在尝试一把，菱形就会变成绿色的勾，表示这个测试已通过。
    </p>
    <p>
        任何时候，你都可以点击这个绿色的标记（或表示失败测试的红色标记）来运行测试。这时在类名旁边就会出现另一个绿色的标记。点击它就会运行
        <em>
            在这个类中的
        </em>
        所有测试。此刻点击它和运行单个测试还没有什么区别，但很快就会发生变化。
    </p>
    <p>
        测试你代码的最后一种方式就是运行所有的测试。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/RunningTests-650x152.png"
        alt="RunningTests" width="650" height="152" class="aligncenter size-large wp-image-142112"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/RunningTests-650x152.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/RunningTests-480x112.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/RunningTests.png 700w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        按下
        <em>
            Command-U
        </em>
        键就可以运行全部的测试，然后切到
        <em>
            Test Navigator
        </em>
        ，你就可以在High RollerTests部分看到你单个的测试。可能你需要将此部分展开才能看到。绿色的勾会出现在每个测试的旁边。如果你将鼠标指针在列表中上下移动，你就会看到出现了小小的播放按钮，你可以点击它来运行任意测试或测试的集合。
    </p>
    <p>
        在
        <em>
            Test Navigator
        </em>
        中，你看到
        <em>
            High RollerUITests
        </em>
        也会被运行。带有UI测试的问题是会变慢。你希望你的测试能够尽可能地快，以便频繁地进行测试。要解决这个问题，就需要编辑scheme来使得UI测试不会自动运行。
    </p>
    <p>
        在工具栏scheme的弹出菜单中选择
        <em>
            Edit scheme…
        </em>
        。点击左侧面板中的. Click
        <em>
            Test
        </em>
        ，然后取消勾选
        <em>
            High RollerUITests
        </em>
        。关闭scheme的窗口，然后按
        <em>
            Command-U
        </em>
        键再次运行你的测试。这时在
        <em>
            Test Navigator
        </em>
        中，你就会发现UI测试不会再被自动执行了，但仍然可以手动地让它执行。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/TurnOffUITests-650x362.png"
        alt="TurnOffUITests" width="650" height="362" class="aligncenter size-large wp-image-141411"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/TurnOffUITests-650x362.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/TurnOffUITests-480x267.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/TurnOffUITests.png 700w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <h3>
        选择运行哪个测试
    </h3>
    <p>
        我们应当选择哪个方法来运行测试？单个，类中，或是全部？
    </p>
    <p>
        如果你正基于某一个测试工作，通常就选择测试它本身或所在的整个类。通过一个测试后，检查它是否对其它的东西造成了破坏就变得非常关键，因此你应当在这时执行一次完整的测试。
    </p>
    <p>
        为了进展得更容易些，在
        <em>
            primary editor
        </em>
        中打开
        <em>
            DiceTests.swift
        </em>
        ，而在
        <em>
            assistant editor
        </em>
        中打开
        <em>
            Dice.swift
        </em>
        。这是一个非常方便的工作方式，便于完成TDD的序列。
    </p>
    <p>
        这就完成了TDD序列的第二个步骤。由于没有进行过重构，因此现在就应当返回步骤一，来编写另一个失败的测试。
    </p>
    <h3>
        测试nil
    </h3>
    <p>
        每个
        <em>
            Dice
        </em>
        对象都有一个
        <code>
            value
        </code>
        ，当
        <em>
            Dice
        </em>
        被初始化时，它的值应当为
        <code>
            nil
        </code>
        。
    </p>
    <p>
        添加下列的测试到
        <em>
            DiceTests.swift
        </em>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-comment">// 1</span>
  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testValueForNewDiceIsNil</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">let</span> testDie = <span class="hljs-type">Dice</span>()
    <span class="hljs-comment">// 2</span>
    <span class="hljs-type">XCTAssertNil</span>(testDie.value, <span class="hljs-string">"Die value should be nil after init"</span>)
  }
</pre>
    <p>
        上述的测试：
    </p>
    <ol>
        <li>
            方法的名称以
            <code>
                'test'
            </code>
            开头，而剩余的部分则表明测试什么。
        </li>
        <li>
            本测试使用
            <code>
                XCTAssert
            </code>
            方法之一来确认value是
            <code>
                nil
            </code>
            。
            <code>
                XCTAssertNil()
            </code>
            方法的第二个参数是一个可选的字符串，当测试失败的时候，用来提供错误信息。我通常偏好使用描述性较强的方法名称，而将这个参数置空，来保持实际测试的代码整洁易读。
        </li>
    </ol>
    <p>
        这个测试代码会产生一个编译错误：
        <code>
            “Value of type 'Dice' has no member 'value'”
        </code>
        。
    </p>
    <p>
        为修复这个错误，在
        <em>
            Dice.swift
        </em>
        中添加下列的property声明到
        <code>
            Dice
        </code>
        的结构体中：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-keyword">var</span> value: <span class="hljs-type">Int</span>?
</pre>
    <p>
        在app构建之前，
        <em>
            DiceTests.swift
        </em>
        中的编译错误并不会消失。按下
        <em>
            Command-U
        </em>
        键来构建app并运行测试，这时测试就应该通过了。此时这里就没有需要重构的地方了。
    </p>
    <p>
        每个
        <code>
            Dice
        </code>
        对象都应该可以“滚动”并生成它的value。添加下一个测试到
        <em>
            DiceTests.swift
        </em>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testRollDie</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">var</span> testDie = <span class="hljs-type">Dice</span>()
    testDie.rollDie()
    <span class="hljs-type">XCTAssertNotNil</span>(testDie.value)
  }
</pre>
    <p>
        这个测试使用了
        <code>
            XCTAssertNotNil()
        </code>
        方法来替换之前测试中的
        <code>
            XCTAssertNil()
        </code>
        。
    </p>
    <p>
        由于Dice结构体还没有
        <code>
            rollDie()
        </code>
        方法，此时必然就会出现另一个编译错误。为了修复它，切回到
        <em>
            Assistant Editor
        </em>
        中，并添加下列代码到
        <em>
            Dice.swift
        </em>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">rollDie</span><span class="hljs-params">()</span></span> {

  }
</pre>
    <p>
        运行测试，你会看到一个警告，关于使用
        <code>
            var
        </code>
        来替换
        <code>
            let
        </code>
        ，以及一个
        <code>
            XCTAssert
        </code>
        这次将会失败的提示。这是讲得通的，因为
        <code>
            rollDie()
        </code>
        到现在还未做任何事。将
        <code>
            rollDie()
        </code>
        修改为如下的代码：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-keyword">mutating</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">rollDie</span><span class="hljs-params">()</span></span> {
    value = <span class="hljs-number">0</span>
  }
</pre>
    <p>
        现在你已明白了TDD如何产生一些奇怪的代码。你很清楚
        <code>
            Dice
        </code>
        结构体最终产生的是随机的值，但由于目前为止，你还没有编写测试来验证这点，因此这个方法还是能够通过目前测试的最小代码集。再次运行测试来证明这点。
    </p>
    <h3>
        Developing to Tests
    </h3>
    <p>
        拓宽你的思路 — 接下来的几个测试旨在塑造你代码的组织方式。开始你会感到是不又要返工了，但实际上这是让你可以聚焦在你代码真实意图的强有力的方式。
    </p>
    <p>
        一个标准的骰子有6个面，因此任意一次滚动得出的值都应该在一和六之间。切到
        <em>
            DiceTests.swift
        </em>
        并添加下列的测试，现在又引入了两个
        <code>
            XCTAssert
        </code>
        方法：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testDiceRoll_ShouldBeFromOneToSix</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">var</span> testDie = <span class="hljs-type">Dice</span>()
    testDie.rollDie()
    <span class="hljs-type">XCTAssertTrue</span>(testDie.value! &gt;= <span class="hljs-number">1</span>)
    <span class="hljs-type">XCTAssertTrue</span>(testDie.value! &lt;= <span class="hljs-number">6</span>)
    <span class="hljs-type">XCTAssertFalse</span>(testDie.value == <span class="hljs-number">0</span>)
  }
</pre>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/one-sided_dice2.png"
        alt="one-sided_dice2" width="100" height="116" class="alignright size-full wp-image-142143">
    </p>
    <p>
        运行测试，现在两个断言都会失败。修改
        <code>
            rollDie()
        </code>
        方法，将
        <code>
            value
        </code>
        设置为1。这次就可以通过测试了，但这样的骰子仍没神马用处！:]
    </p>
    <p>
        换一个思路，我们何不测试滚动骰子多次，然后统计生成的每种value的个数？可能无法做到完美，但一个足够大的样本数量应该可以足够接近你的测试意图。
    </p>
    <p>
        在
        <em>
            DiceTests.swift
        </em>
        中添加另一个测试：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testRollsAreSpreadRoughlyEvenly</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">var</span> testDie = <span class="hljs-type">Dice</span>()
    <span class="hljs-keyword">var</span> rolls: [<span class="hljs-type">Int</span>: <span class="hljs-type">Double</span>] = [:]
    <span class="hljs-comment">// 1</span>
    <span class="hljs-keyword">let</span> rollCounter = <span class="hljs-number">600.0</span>
    <span class="hljs-keyword">for</span> <span class="hljs-number">_</span> <span class="hljs-keyword">in</span> <span class="hljs-number">0</span> ..&lt; <span class="hljs-type">Int</span>(rollCounter) {
      testDie.rollDie()
      <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> newRoll = testDie.value <span class="hljs-keyword">else</span> {
        <span class="hljs-comment">// 2</span>
        <span class="hljs-type">XCTFail</span>()
        <span class="hljs-keyword">return</span>
      }
      <span class="hljs-comment">// 3</span>
      <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> existingCount = rolls[newRoll] {
        rolls[newRoll] = existingCount + <span class="hljs-number">1</span>
      } <span class="hljs-keyword">else</span> {
        rolls[newRoll] = <span class="hljs-number">1</span>
      }
    }
    <span class="hljs-comment">// 4</span>
    <span class="hljs-type">XCTAssertEqual</span>(rolls.keys.<span class="hljs-built_in">count</span>, <span class="hljs-number">6</span>)
    <span class="hljs-comment">// 5</span>
    <span class="hljs-keyword">for</span> (key, roll) <span class="hljs-keyword">in</span> rolls {
      <span class="hljs-type">XCTAssertEqualWithAccuracy</span>(roll,
                                 rollCounter / <span class="hljs-number">6</span>,
                                 accuracy: rollCounter / <span class="hljs-number">6</span> * <span class="hljs-number">0.3</span>,
                                 <span class="hljs-string">"Dice gave <span class="hljs-subst">\(roll)</span> x <span class="hljs-subst">\(key)</span>"</span>)
    }
  }
</pre>
    <p>
        上述的测试代码：
    </p>
    <ol>
        <li>
            <code>
                rollCounter
            </code>
            指示骰子将被滚动的次数。我们认为相应于每个期望的数字滚动100次是一个大致合理的样本数量。
        </li>
        <li>
            如果任何一次循环后value没有值，测试会失败并立刻退出。
            <code>
                XCTFail()
            </code>
            类似于一个断言，它永远都不会通过，非常适合于
            <code>
                guard
            </code>
            语句搭配使用。
        </li>
        <li>
            每次滚动之后，你都将结果保存到一个字典中。
        </li>
        <li>
            这个断言确定字典中有六个key，它们都是滚动骰子所期望得到的数字。
        </li>
        <li>
            这个测试使用了一个新的断言：
            <code>
                XCTAssertEqualWithAccuracy()
            </code>
            ，它可以进行不精确的比较。由于
            <code>
                XCTAssertEqualWithAccuracy()
            </code>
            会被调用非常多次，因此用可选的信息来表示哪一部分的循环失败了。
        </li>
    </ol>
    <p>
        运行测试，如你所料，测试因为每次滚动都得到的是1失败了。切到
        <em>
            Issue Navigator
        </em>
        可以查看更多详细的错误信息。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/IssueNavigator.png"
        alt="IssueNavigator" width="515" height="462" class="aligncenter size-full wp-image-142115"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/IssueNavigator.png 515w, https://koenig-media.raywenderlich.com/uploads/2016/08/IssueNavigator-357x320.png 357w"
        sizes="(max-width: 515px) 100vw, 515px">
    </p>
    <p>
        最后，添加随机数字生成器到
        <code>
            rollDie()
        </code>
        中。在
        <em>
            Dice.swift
        </em>
        中，将该方法修改成如下的样子：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-keyword">mutating</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">rollDie</span><span class="hljs-params">()</span></span> {
    value = <span class="hljs-type">Int</span>(arc4random_uniform(<span class="hljs-type">UInt32</span>(<span class="hljs-number">6</span>))) + <span class="hljs-number">1</span>
  }
</pre>
    <p>
        上述代码使用了
        <code>
            arc4random_uniform()
        </code>
        产生一个1到6之间的数字。看起来非常得简单，但仍然需要进行测试！再次按下
        <em>
            Command-U
        </em>
        键，所有的测试都通过了。你现在就可以确信
        <code>
            Dice
        </code>
        结构体大致是以你所期望的比例产生数字了。如果有人说你的app作弊，你就可以把测试结果给它们看说不是的！
    </p>
    <p>
        完工大吉了！
        <code>
            Dice
        </code>
        结构体已完成，喝茶时间...
    </p>
    <p>
        如果你有这样的朋友，他玩过很多的角色扮演游戏，说你的app不支持多种类型的骰子：四面的，8面的，12面的，20面的甚至100面的...该怎么办？
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/Dice.jpg"
        alt="Dice" width="400" height="469" class="aligncenter size-large wp-image-141427"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/Dice.jpg 400w, https://koenig-media.raywenderlich.com/uploads/2016/08/Dice-273x320.jpg 273w"
        sizes="(max-width: 400px) 100vw, 400px">
    </p>
    <h3>
        修改代码
    </h3>
    <p>
        你不想让你的朋友扫兴，因此回到
        <em>
            DiceTests.swift
        </em>
        并添加另一个测试：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testRollingTwentySidedDice</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">var</span> testDie = <span class="hljs-type">Dice</span>()
    testDie.rollDie(numberOfSides: <span class="hljs-number">20</span>)
    <span class="hljs-type">XCTAssertNotNil</span>(testDie.value)
    <span class="hljs-type">XCTAssertTrue</span>(testDie.value! &gt;= <span class="hljs-number">1</span>)
    <span class="hljs-type">XCTAssertTrue</span>(testDie.value! &lt;= <span class="hljs-number">20</span>)
  }
</pre>
    <p>
        编译器会抱怨说
        <code>
            rollDie()
        </code>
        不可以传任何参数。切到
        <em>
            assistant editor
        </em>
        并在
        <em>
            Dice.swift
        </em>
        中修改
        <code>
            rollDie()
        </code>
        的声明，来添加一个
        <code>
            numberOfSides
        </code>
        的形参：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-keyword">mutating</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">rollDie</span><span class="hljs-params">(numberOfSides: Int)</span></span> {
</pre>
    <p>
        但这会导致之前的测试失败，因为它们并没有提供参数。你
        <i>
            可以
        </i>
        将它们全部修改，但大多数的骰子都是6个面的（无需告知你角色扮演的朋友这点）。那么何不给
        <code>
            numberOfSides
        </code>
        参数一个默认值？
    </p>
    <p>
        将
        <code>
            rollDie(numberOfSides:)
        </code>
        的声明修改为：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-keyword">mutating</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">rollDie</span><span class="hljs-params">(numberOfSides: Int = <span class="hljs-number">6</span>)</span></span> {
</pre>
    <p>
        现在所有的测试就都通过了，但你还在处在之前相同的位置：测试并不会检查当20个面的骰子滚动的时候，产生的值是1到20之间的。
    </p>
    <p>
        因此现在需要写另一个类似于
        <code>
            testRollsAreSpreadRoughlyEvenly()
        </code>
        的测试了，但针对的是20个面的骰子。
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testTwentySidedRollsAreSpreadRoughlyEvenly</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">var</span> testDie = <span class="hljs-type">Dice</span>()
    <span class="hljs-keyword">var</span> rolls: [<span class="hljs-type">Int</span>: <span class="hljs-type">Double</span>] = [:]
    <span class="hljs-keyword">let</span> rollCounter = <span class="hljs-number">2000.0</span>
    <span class="hljs-keyword">for</span> <span class="hljs-number">_</span> <span class="hljs-keyword">in</span> <span class="hljs-number">0</span> ..&lt; <span class="hljs-type">Int</span>(rollCounter) {
      testDie.rollDie(numberOfSides: <span class="hljs-number">20</span>)
      <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> newRoll = testDie.value <span class="hljs-keyword">else</span> {
        <span class="hljs-type">XCTFail</span>()
        <span class="hljs-keyword">return</span>
      }
      <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> existingCount = rolls[newRoll] {
        rolls[newRoll] = existingCount + <span class="hljs-number">1</span>
      } <span class="hljs-keyword">else</span> {
        rolls[newRoll] = <span class="hljs-number">1</span>
      }
    }
    <span class="hljs-type">XCTAssertEqual</span>(rolls.keys.<span class="hljs-built_in">count</span>, <span class="hljs-number">20</span>)
    <span class="hljs-keyword">for</span> (key, roll) <span class="hljs-keyword">in</span> rolls {
      <span class="hljs-type">XCTAssertEqualWithAccuracy</span>(roll,
                                 rollCounter / <span class="hljs-number">20</span>,
                                 accuracy: rollCounter / <span class="hljs-number">20</span> * <span class="hljs-number">0.3</span>,
                                 <span class="hljs-string">"Dice gave <span class="hljs-subst">\(roll)</span> x <span class="hljs-subst">\(key)</span>"</span>)
    }
  }
</pre>
    <p>
        这个测试给出了7个失败：key的数量只有6个，且它们的分布并不相等。使用
        <em>
            Issue Navigator
        </em>
        来查看全部的细节。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/IssueNavigator2-213x500.png"
        alt="IssueNavigator2" width="213" height="500" class="aligncenter size-large wp-image-142116"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/IssueNavigator2-213x500.png 213w, https://koenig-media.raywenderlich.com/uploads/2016/08/IssueNavigator2.png 515w"
        sizes="(max-width: 213px) 100vw, 213px">
    </p>
    <p>
        你应当期望：
        <code>
            rollDie(numberOfSides:)
        </code>
        还不使用
        <code>
            numberOfSides
        </code>
        参数。
    </p>
    <p>
        用
        <code>
            numberOfSides
        </code>
        来替换
        <code>
            arc4random_uniform()
        </code>
        中的6，然后再次按下
        <em>
            Command-U
        </em>
        键。
    </p>
    <p>
        成功了！所有的测试都通过了 - 甚至包括之前调用了你刚修改过的方法的那些测试。
    </p>
    <h3>
        重构测试
    </h3>
    <p>
        你有一些很值得去重构的代码。
        <code>
            testRollsAreSpreadRoughlyEvenly()
        </code>
        和
        <code>
            testTwentySidedRollsAreSpreadRoughlyEvenly()
        </code>
        中的代码非常相似，因此你可以将其分离出来作为一个私有方法。
    </p>
    <p>
        添加下列的extension到
        <em>
            DiceTests.swift
        </em>
        文件的尾部，要在类的外部：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">extension</span> <span class="hljs-title">DiceTests</span> </span>{

  <span class="hljs-keyword">fileprivate</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">performMultipleRollTests</span><span class="hljs-params">(numberOfSides: Int = <span class="hljs-number">6</span>)</span></span> {
    <span class="hljs-keyword">var</span> testDie = <span class="hljs-type">Dice</span>()
    <span class="hljs-keyword">var</span> rolls: [<span class="hljs-type">Int</span>: <span class="hljs-type">Double</span>] = [:]
    <span class="hljs-keyword">let</span> rollCounter = <span class="hljs-type">Double</span>(numberOfSides) * <span class="hljs-number">100.0</span>
    <span class="hljs-keyword">let</span> expectedResult = rollCounter / <span class="hljs-type">Double</span>(numberOfSides)
    <span class="hljs-keyword">let</span> allowedAccuracy = rollCounter / <span class="hljs-type">Double</span>(numberOfSides) * <span class="hljs-number">0.3</span>
    <span class="hljs-keyword">for</span> <span class="hljs-number">_</span> <span class="hljs-keyword">in</span> <span class="hljs-number">0</span> ..&lt; <span class="hljs-type">Int</span>(rollCounter) {
      testDie.rollDie(numberOfSides: numberOfSides)
      <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> newRoll = testDie.value <span class="hljs-keyword">else</span> {
        <span class="hljs-type">XCTFail</span>()
        <span class="hljs-keyword">return</span>
      }
      <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> existingCount = rolls[newRoll] {
        rolls[newRoll] = existingCount + <span class="hljs-number">1</span>
      } <span class="hljs-keyword">else</span> {
        rolls[newRoll] = <span class="hljs-number">1</span>
      }
    }
    <span class="hljs-type">XCTAssertEqual</span>(rolls.keys.<span class="hljs-built_in">count</span>, numberOfSides)
    <span class="hljs-keyword">for</span> (key, roll) <span class="hljs-keyword">in</span> rolls {
      <span class="hljs-type">XCTAssertEqualWithAccuracy</span>(roll,
                                 expectedResult,
                                 accuracy: allowedAccuracy,
                                 <span class="hljs-string">"Dice gave <span class="hljs-subst">\(roll)</span> x <span class="hljs-subst">\(key)</span>"</span>)
    }
  }

}
</pre>
    <p>
        这个方法的名称并不以
        <code>
            test
        </code>
        开头，因此不会被当做一个测试去运行。
    </p>
    <p>
        回到主
        <code>
            DiceTests
        </code>
        类，并将
        <code>
            testRollsAreSpreadRoughlyEvenly()
        </code>
        和
        <code>
            testTwentySidedRollsAreSpreadRoughlyEvenly()
        </code>
        方法替换为下列的代码：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testRollsAreSpreadRoughlyEvenly</span><span class="hljs-params">()</span></span> {
    performMultipleRollTests()
  }

  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testTwentySidedRollsAreSpreadRoughlyEvenly</span><span class="hljs-params">()</span></span> {
    performMultipleRollTests(numberOfSides: <span class="hljs-number">20</span>)
  }
</pre>
    <p>
        再次运行所有的测试，来证实上述重构正确。
    </p>
    <h3>
        使用 #line
    </h3>
    <p>
        为了演示另一项非常有用的测试技术，切回
        <em>
            Dice.swift
        </em>
        并撤销你在
        <code>
            rollDie(numberOfSides:)
        </code>
        中做的有关于20面的骰子的改动：将调用
        <code>
            arc4random_uniform()
        </code>
        中的
        <code>
            numberOfSides
        </code>
        替换为
        <code>
            6
        </code>
        。现在再次运行测试。
    </p>
    <p>
        <code>
            testTwentySidedRollsAreSpreadRoughlyEvenly()
        </code>
        失败了，但错误信息却位于
        <code>
            performMultipleRollTests(numberOfSides:)
        </code>
        中 — 不是一个非常有用的地点。
    </p>
    <p>
        Xcode可以帮助你解决这个问题。当定义一个助手方法的时候，你可以提供一个带有特定默认值
        <code>
            #line
        </code>
        的参数 - 它会包含调用这个方法时的代码的行序号。这个行序号就可以被用到
        <code>
            XCTAssert
        </code>
        方法中，使得错误的信息更有价值。
    </p>
    <p>
        在
        <code>
            DiceTests
        </code>
        的extension中，将方法的定义
        <code>
            performMultipleRollTests(numberOfSides:)
        </code>
        修改为如下的代码：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-keyword">fileprivate</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">performMultipleRollTests</span><span class="hljs-params">(numberOfSides: Int = <span class="hljs-number">6</span>, line: UInt = #line)</span></span> {
</pre>
    <p>
        将
        <code>
            XCTAsserts
        </code>
        修改为如下的样子：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-type">XCTAssertEqual</span>(rolls.keys.<span class="hljs-built_in">count</span>, numberOfSides, line: line)

<span class="hljs-keyword">for</span> (key, roll) <span class="hljs-keyword">in</span> rolls {
  <span class="hljs-type">XCTAssertEqualWithAccuracy</span>(roll,
                             expectedResult,
                             accuracy: allowedAccuracy,
                             <span class="hljs-string">"Dice gave <span class="hljs-subst">\(roll)</span> x <span class="hljs-subst">\(key)</span>"</span>,
                             line: line)
}
</pre>
    <p>
        你无需修改调用
        <code>
            performMultipleRollTests(numberOfSides:line:)
        </code>
        方法的代码，因为新的参数会被默认值自动地填充。再次运行测试，你就会发现现在错误的记号位于调用
        <code>
            performMultipleRollTests(numberOfSides:line:)
        </code>
        方法这行了 - 而不是在助手方法之中。
    </p>
    <p>
        将
        <code>
            rollDie(numberOfSides:)
        </code>
        方法恢复原状，然后按
        <em>
            Command-U
        </em>
        键确认一切工作正常。
    </p>
    <p>
        给自己点个赞吧 - 你已学会了如何使用TDD来开发一个经过完整测试的model类。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/victory.png"
        alt="victory" width="475" height="313" class="aligncenter size-full wp-image-142118">
    </p>
    <h2>
        添加单元测试到已存在的代码中
    </h2>
    <p>
        TDD在开发新的代码时很棒，但你经常会不得不在之前已有的代码中加入测试。步骤和之前基本相同，除了你现在是编写测试，来确认已存在的代码如同期望中的方式工作。
    </p>
    <p>
        要学习该怎么做，你要为
        <code>
            Roll
        </code>
        结构体添加测试。在这个app中，
        <code>
            Roll
        </code>
        包含了一个
        <code>
            Dice
        </code>
        的数组和一个
        <code>
            numberOfSides
        </code>
        的property。它用来处理滚动所有的筛子及统计滚动的结果。
    </p>
    <p>
        回到
        <em>
            File Navigator
        </em>
        ，选择
        <code>
            Roll.swift
        </code>
        。将全部占位的代码替换为如下内容：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">struct</span> <span class="hljs-title">Roll</span> </span>{

  <span class="hljs-keyword">var</span> dice: [<span class="hljs-type">Dice</span>] = []
  <span class="hljs-keyword">var</span> numberOfSides = <span class="hljs-number">6</span>

  <span class="hljs-keyword">mutating</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">changeNumberOfDice</span><span class="hljs-params">(newDiceCount: Int)</span></span> {
    dice = []
    <span class="hljs-keyword">for</span> <span class="hljs-number">_</span> <span class="hljs-keyword">in</span> <span class="hljs-number">0</span> ..&lt; newDiceCount {
      dice.append(<span class="hljs-type">Dice</span>())
    }
  }

  <span class="hljs-keyword">var</span> allDiceValues: [<span class="hljs-type">Int</span>] {
    <span class="hljs-keyword">return</span> dice.flatMap { $<span class="hljs-number">0</span>.value}
  }

  <span class="hljs-keyword">mutating</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">rollAll</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">for</span> index <span class="hljs-keyword">in</span> <span class="hljs-number">0</span> ..&lt; dice.<span class="hljs-built_in">count</span> {
      dice[index].rollDie(numberOfSides: numberOfSides)
    }
  }

  <span class="hljs-keyword">mutating</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">changeValueForDie</span><span class="hljs-params">(at diceIndex: Int, to newValue: Int)</span></span> {
    <span class="hljs-keyword">if</span> diceIndex &lt; dice.<span class="hljs-built_in">count</span> {
      dice[diceIndex].value = newValue
    }
  }

  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">totalForDice</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">Int</span> {
    <span class="hljs-keyword">let</span> total = dice
      .flatMap { $<span class="hljs-number">0</span>.value }
      .<span class="hljs-built_in">reduce</span>(<span class="hljs-number">0</span>) { $<span class="hljs-number">0</span> - $<span class="hljs-number">1</span> }
    <span class="hljs-keyword">return</span> total
  }

}
</pre>
    <p>
        （发现错误了么？现在先忽略它，这就是我们将要测试的地方。:]）
    </p>
    <p>
        在
        <em>
            File Navigator
        </em>
        中选择
        <em>
            High RollerTests
        </em>
        组，并使用
        <em>
            File/New/File…
        </em>
        中的
        <em>
            macOS/Unit Test Case Class
        </em>
        来添加一个叫做
        <code>
            RollTests
        </code>
        的类。删除其中所有的测试代码。
    </p>
    <p>
        添加下列的import到
        <em>
            RollTests.swift
        </em>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@testable</span> <span class="hljs-keyword">import</span> High_Roller
</pre>
    <p>
        在assistant editor中打开
        <em>
            Roll.swift
        </em>
        ，你将在其中编写更多的测试。
    </p>
    <p>
        首先，你想去测试
        <code>
            Roll
        </code>
        可否被创建，且可以添加
        <code>
            Dice
        </code>
        到
        <code>
            dice
        </code>
        数组中。测试使用5个骰子。
    </p>
    <p>
        添加测试到
        <em>
            RollTests.swift
        </em>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testCreatingRollOfDice</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">var</span> roll = <span class="hljs-type">Roll</span>()
    <span class="hljs-keyword">for</span> <span class="hljs-number">_</span> <span class="hljs-keyword">in</span> <span class="hljs-number">0</span> ..&lt; <span class="hljs-number">5</span> {
      roll.dice.append(<span class="hljs-type">Dice</span>())
    }
    <span class="hljs-type">XCTAssertNotNil</span>(roll)
    <span class="hljs-type">XCTAssertEqual</span>(roll.dice.<span class="hljs-built_in">count</span>, <span class="hljs-number">5</span>)
  }
</pre>
    <p>
        运行测试。目前一切都好 - 第一个测试通过了。和TDD不同，一个失败的测试并非是基本的第一步，因为代码（理论上）早已可以正常地工作。
    </p>
    <p>
        接下来，使用下列的测试，来检查在滚动之前，点数的总数为0：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testTotalForDiceBeforeRolling_ShouldBeZero</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">var</span> roll = <span class="hljs-type">Roll</span>()
    <span class="hljs-keyword">for</span> <span class="hljs-number">_</span> <span class="hljs-keyword">in</span> <span class="hljs-number">0</span> ..&lt; <span class="hljs-number">5</span> {
      roll.dice.append(<span class="hljs-type">Dice</span>())
    }
    <span class="hljs-keyword">let</span> total = roll.totalForDice()
    <span class="hljs-type">XCTAssertEqual</span>(total, <span class="hljs-number">0</span>)
  }
</pre>
    <p>
        再次成功了，但看起来似乎需要进行一些重构。每个测试的第一部分都设置了一个
        <code>
            Roll
        </code>
        对象，并使用5个骰子来填充它。如果将它移到
        <code>
            setup()
        </code>
        方法中，它就会在每个测试前执行。
    </p>
    <p>
        不仅如此，
        <code>
            Roll
        </code>
        有一个方法来改变自身数组中
        <code>
            Dice
        </code>
        的个数，因此测试也可以使用和测试这里。
    </p>
    <p>
        将
        <code>
            RollTests
        </code>
        类的内容替换为：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-keyword">var</span> roll: <span class="hljs-type">Roll</span>!

  <span class="hljs-keyword">override</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">setUp</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">super</span>.setUp()
    roll = <span class="hljs-type">Roll</span>()
    roll.changeNumberOfDice(newDiceCount: <span class="hljs-number">5</span>)
  }

  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testCreatingRollOfDice</span><span class="hljs-params">()</span></span> {
    <span class="hljs-type">XCTAssertNotNil</span>(roll)
    <span class="hljs-type">XCTAssertEqual</span>(roll.dice.<span class="hljs-built_in">count</span>, <span class="hljs-number">5</span>)
  }

  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testTotalForDiceBeforeRolling_ShouldBeZero</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">let</span> total = roll.totalForDice()
    <span class="hljs-type">XCTAssertEqual</span>(total, <span class="hljs-number">0</span>)
  }
</pre>
    <p>
        按照惯例，再次运行测试，来检查一切是否正常工作。
    </p>
    <p> 
        在6面骰子的情况下，最小的总数应当是5，而最大的总数则应是30，因此添加下列的测试来验证总数是否处于这个范围之中：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testTotalForDiceAfterRolling_ShouldBeBetween5And30</span><span class="hljs-params">()</span></span> {
    roll.rollAll()
    <span class="hljs-keyword">let</span> total = roll.totalForDice()
    <span class="hljs-type">XCTAssertGreaterThanOrEqual</span>(total, <span class="hljs-number">5</span>)
    <span class="hljs-type">XCTAssertLessThanOrEqual</span>(total, <span class="hljs-number">30</span>)
  }
</pre>
    <p>
        运行测试 - 它失败了！看起来测试已经发现了一个代码中的bug。问题应该是在
        <code>
            rollAll()
        </code>
        或
        <code>
            totalForDice()
        </code>
        中，因为这个测试中只调用过这两个方法。如果
        <code>
            rollAll()
        </code>
        失败的话，总数应该是0.然而，返回的总数是一个负值，因此让我们来看一看
        <code>
            totalForDice()
        </code>
        方法。
    </p>
    <p>
        问题就在这里：
        <code>
            reduce
        </code>
        是减而不是加value。将减号改为加号：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">totalForDice</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">Int</span> {
  <span class="hljs-keyword">let</span> total = dice
    .flatMap { $<span class="hljs-number">0</span>.value }
    <span class="hljs-comment">// .reduce(0) { $0 - $1 }       // bug line</span>
    .<span class="hljs-built_in">reduce</span>(<span class="hljs-number">0</span>) { $<span class="hljs-number">0</span> + $<span class="hljs-number">1</span> }          <span class="hljs-comment">// fixed</span>
  <span class="hljs-keyword">return</span> total
}
</pre>
    <p>
        再次运行你的测试 - 现在一切都完美地运行了。
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
        你可以在
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/08/HighRoller-part1.zip"
        sl-processed="1">
            这里
        </a>
        下载本教程中，这一部分的完整的测试。
    </p>
    <p>
        请继续阅读
        <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Unit%20Testing%20on%20macOS%20-%20Part%202:2.md"
        sl-processed="1">
            单元测试：2/2部分
        </a>
        ，来学习更多优秀的特性，包括交互测试，网络测试，性能测试和代码覆盖。希望可以在这里看到你！:]
    </p>
</div>