# 单元测试：2/2部分

#### [原文地址](https://www.raywenderlich.com/142090/unit-testing-macos-part-22) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-250x250.png"
        alt="Unit-Testing-macOS" width="250" height="250" class="alignright size-thumbnail wp-image-142750"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/08/UnitTesting-1-feature-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
        在本教程的
        <a href="https://github.com/DeveloperLx/macOS_Development_Tutorials_translation/blob/master/Unit%20Testing%20on%20macOS%20-%20Part%201:2.md" sl-processed="1">
            第一部分
        </a>
        ，你已经学习了如何使用TDD来测试新添加的代码，及添加单元测试到已存在的代码中。在这一部分，你将学习如何测试UI，如何测试网络代码，以及一些帮助你进行测试的Xcode工具。
    </p>
    <p>
        如果你还未完成第一部分，或是想要一个新的开始，可以从
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/08/HighRoller-part1.zip"
        sl-processed="1">
            这里
        </a>
        下载第一部分完整的项目。该项目使用Swift 3，最低Xcode 8 beta 6以上的版本。在Xcode中打开它并按下
        <em>
            Command-U
        </em>
        键来运行所有的测试，确认一切如你期望中一样得工作正常。
    </p>
    <h2>
        测试交互
    </h2>
    <p>
        正如你在第一部分中所看到的一样，Xcode包含了运行UITests的能力。尽管这个非常有用，单用编程的方式来测试view和view controller可以更加快速。在测试中我们会创建一个view或view controller的实例去直接测试，而不是运行app并发送模拟点击事件到交互对象上。你可以获取和设置property，调用方法 - 包括IBAction方法 - 来更加快速地测试出结果。
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
        来创建一个名为
        <code>
            ViewControllerTests
        </code>
        的类。添加全部的代码并添加下列的import到文件的顶部：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@testable</span> <span class="hljs-keyword">import</span> High_Roller
</pre>
    <p>
        插入下列的代码到
        <code>
            ViewControllerTests
        </code>
        类中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-comment">// 1</span>
<span class="hljs-keyword">var</span> vc: <span class="hljs-type">ViewController</span>!

<span class="hljs-keyword">override</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">setUp</span><span class="hljs-params">()</span></span> {
  <span class="hljs-keyword">super</span>.setUp()

  <span class="hljs-comment">// 2</span>
  <span class="hljs-keyword">let</span> storyboard = <span class="hljs-type">NSStoryboard</span>(name: <span class="hljs-string">"Main"</span>, bundle: <span class="hljs-literal">nil</span>)
  vc = storyboard.instantiateController(withIdentifier: <span class="hljs-string">"ViewController"</span>) <span class="hljs-keyword">as</span>! <span class="hljs-type">ViewController</span>

  <span class="hljs-comment">// 3</span>
  <span class="hljs-number">_</span> = vc.view
}
</pre>
    <p>
        上述的代码：
    </p>
    <ol>
        <li>
            整个的类会使用一个名为
            <em>
            File Navigator
            </em>
            的property访问
            <code>
                ViewController
            </code>
            。可以将它设为非可选的，因为如果它崩溃掉的话，仍然是一个非常有用的测试结果。
        </li>
        <li>
            这个view controller是从storyboard的
            <code>
                setup()
            </code>
            中实例化的。
        </li>
        <li>
            为了触发view的生命周期，获取view controller的
            <code>
                view
            </code>
            property。你无需去保存，因为获取它的动作就已是的创建view controller的动作正确地执行。
        </li>
    </ol>
    <p>
        以这种方式实例化view controller，必须保证它有一个storyboard ID。打开
        <em>
            Main.storyboard
        </em>
        ，选择
        <em>
            ViewController
        </em>
        ，并在右侧打开
        <em>
            Identity Inspector
        </em>
        。将Storyboard ID设置为
        <em>
            ViewController
        </em>
        。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/AddStoryboardID.png"
        alt="Add-Storyboard-ID-for-ViewController" width="512" height="481" class="aligncenter size-full wp-image-141413"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/AddStoryboardID.png 512w, https://koenig-media.raywenderlich.com/uploads/2016/08/AddStoryboardID-341x320.png 341w"
        sizes="(max-width: 512px) 100vw, 512px">
    </p>
    <p>
        第一个测试将用来确认
        <em>
            ViewController
        </em>
        正确地被创建。切回
        <em>
            ViewControllerTests.swift
        </em>
        并添加下列的测试方法：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testViewControllerIsCreated</span><span class="hljs-params">()</span></span> {
  <span class="hljs-type">XCTAssertNotNil</span>(vc)
}
</pre>
    <p>
        运行测试。如果出现失败或崩溃的话，返回
        <em>
            Main.storyboard
        </em>
        并检查你的storyboard ID是否设置正确。
    </p>
    <p>
        运行app来查看一下界面。所有的控件都是有功能的，因此点击
        <em>
            Roll
        </em>
        按钮来滚动骰子；修改设置并再次滚动，注意骰子的数量可以使用一个text field或stepper来设定，而骰子的面数则使用一个弹出菜单来设定。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/BuildRun2.png"
        alt="BuildRun2" width="658" height="500" class="aligncenter size-full wp-image-142153"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/BuildRun2.png 658w, https://koenig-media.raywenderlich.com/uploads/2016/08/BuildRun2-421x320.png 421w, https://koenig-media.raywenderlich.com/uploads/2016/08/BuildRun2-650x494.png 650w"
        sizes="(max-width: 658px) 100vw, 658px">
    </p>
    <p>
        在测试之前，控件的操作都如同期望中一样地执行，你需要首先确认交互元素是以期望中的值开始的。
    </p>
    <p>
        添加下列的测试到
        <em>
            ViewControllerTests
        </em>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testControlsHaveDefaultData</span><span class="hljs-params">()</span></span> {
  <span class="hljs-type">XCTAssertEqual</span>(vc.numberOfDiceTextField.stringValue, <span class="hljs-type">String</span>(<span class="hljs-number">2</span>))
  <span class="hljs-type">XCTAssertEqual</span>(vc.numberOfDiceStepper.integerValue, <span class="hljs-number">2</span>)
  <span class="hljs-type">XCTAssertEqual</span>(vc.numberOfSidesPopup.titleOfSelectedItem, <span class="hljs-type">String</span>(<span class="hljs-number">6</span>))
}
</pre>
    <p>
        运行测试，以确认初始化的设置是正确的。
    </p>
    <p>
        确认之后，下一步你就该测试，当通过交互改变参数之后发生了什么。当你在text field中修改了文本框之后，stepper的值就应当发出相应的改变，反之亦然。
    </p>
    <p>
        如果你在使用app的过程中，通过点击向上或向下的箭头改变了stepper的值，
        <code>
            numberOfDiceStepperChanged(\_:)
        </code>
        方法就会被自动地调用。类似的，如果你编辑text field的话，
        <code>
            numberOfDiceTextFieldChanged(\_:)
        </code>
        就会被调用。在测试的时候，你必须手动地来调用这IBAction方法。
    </p>
    <p>
        插入下列的两个测试到
        <em>
            ViewControllerTests
        </em>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testChangingTextFieldChangesStepper</span><span class="hljs-params">()</span></span> {
  vc.numberOfDiceTextField.stringValue = <span class="hljs-type">String</span>(<span class="hljs-number">4</span>)
  vc.numberOfDiceTextFieldChanged(vc.numberOfDiceTextField)

  <span class="hljs-type">XCTAssertEqual</span>(vc.numberOfDiceTextField.stringValue, <span class="hljs-type">String</span>(<span class="hljs-number">4</span>))
  <span class="hljs-type">XCTAssertEqual</span>(vc.numberOfDiceStepper.integerValue, <span class="hljs-number">4</span>)
}

<span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testChangingStepperChangesTextField</span><span class="hljs-params">()</span></span> {
  vc.numberOfDiceStepper.integerValue = <span class="hljs-number">10</span>
  vc.numberOfDiceStepperChanged(vc.numberOfDiceStepper)

  <span class="hljs-type">XCTAssertEqual</span>(vc.numberOfDiceTextField.stringValue, <span class="hljs-type">String</span>(<span class="hljs-number">10</span>))
  <span class="hljs-type">XCTAssertEqual</span>(vc.numberOfDiceStepper.integerValue, <span class="hljs-number">10</span>)
}
</pre>
    <p>
        运行测试来查看结果。你还应当测试view controller中的变量，以确认它们如同期望中的方式进行变化。
    </p>
    <p>
        view controller含有一个
        <code>
            Roll
        </code>
        对象，它含有自己的property。添加下列的测试以确认
        <code>
            Roll
        </code>
        存在对象，并含有期望的默认property：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testViewControllerHasRollObject</span><span class="hljs-params">()</span></span> {
  <span class="hljs-type">XCTAssertNotNil</span>(vc.roll)
}

<span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testRollHasDefaultSettings</span><span class="hljs-params">()</span></span> {
  <span class="hljs-type">XCTAssertEqual</span>(vc.roll.numberOfSides, <span class="hljs-number">6</span>)
  <span class="hljs-type">XCTAssertEqual</span>(vc.roll.dice.<span class="hljs-built_in">count</span>, <span class="hljs-number">2</span>)
}
</pre>
    <p>
        接下来，你需要确认通过界面中的元素改变一项设置后，确实可以改变
        <code>
            Roll
        </code>
        对象中的设置。添加下列的设置：
    </p>
    <pre lang="swift" class="language-swift hljs">    <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testChangingNumberOfDiceInTextFieldChangesRoll</span><span class="hljs-params">()</span></span> {
      vc.numberOfDiceTextField.stringValue = <span class="hljs-type">String</span>(<span class="hljs-number">4</span>)
      vc.numberOfDiceTextFieldChanged(vc.numberOfDiceTextField)
      <span class="hljs-type">XCTAssertEqual</span>(vc.roll.dice.<span class="hljs-built_in">count</span>, <span class="hljs-number">4</span>)
    }
    <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testChangingNumberOfDiceInStepperChangesRoll</span><span class="hljs-params">()</span></span> {
      vc.numberOfDiceStepper.integerValue = <span class="hljs-number">10</span>
      vc.numberOfDiceStepperChanged(vc.numberOfDiceStepper)
      <span class="hljs-type">XCTAssertEqual</span>(vc.roll.dice.<span class="hljs-built_in">count</span>, <span class="hljs-number">10</span>)
    }
    <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testChangingNumberOfSidesPopupChangesRoll</span><span class="hljs-params">()</span></span> {
      vc.numberOfSidesPopup.selectItem(withTitle: <span class="hljs-string">"20"</span>)
      vc.numberOfSidesPopupChanged(vc.numberOfSidesPopup)
      <span class="hljs-type">XCTAssertEqual</span>(vc.roll.numberOfSides, <span class="hljs-number">20</span>)
    }
</pre>
    <p>
        这三个测试会分别操作text field，stepper和弹出菜单。在每次UI元素发生变化之后，它们就会检查
        <code>
            roll
        </code>
        这个property是否匹配于相应的值。
    </p>
    <p>
        在assistant editor中打开
        <em>
            ViewController.swift
        </em>
        ，并查看
        <code>
            rollButtonClicked(\_:)
        </code>
        。它做了三件事：
    </p>
    <ol>
        <li>
            确保任何正在骰子text field中编辑的值都被处理过。
        </li>
        <li>
            告知
            <code>
                Roll
            </code>
            结构体滚动所有骰子。
        </li>
        <li>
            展示结果。
        </li>
    </ol>
    <p>
        你早已编写了测试来确认
        <code>
            rollAll()
        </code>
        的功能如同期望中一样，但
        <code>
            displayDiceFromRoll(diceRolls:numberOfSides:)
        </code>
        需要被当做交互的一部分进行测试。展示的方法全在
        <em>
            ViewControllerDisplay.swift
        </em>
        中，它是包含
        <code>
            ViewController
        </code>
        的一个extension的单独的文件。这是组织代码的一种方式，以保持
        <em>
            ViewController.swift
        </em>
        尽量得小，并将所有的展示方法收集到一个地方。
    </p>
    <p>
        查看
        <em>
            ViewControllerDisplay.swift
        </em>
        文件，你会看到一堆私有方法和一个公有方法：
        <code>
            displayDiceFromRoll(diceRolls:numberOfSides:)
        </code>
        ，它可以清空展示的内容，填入文本信息，然后用一系列的子view来填充一个stack view，每个子view对应于一个骰子。
    </p>
    <p>
        和所有的测试一样，在正确的地方开始非常重要。第一个测试就是检查结果text view和stack view在开始的时候是空的。
    </p>
    <p>
        切到
        <em>
            ViewControllerTests.swift
        </em>
        并添加下列的测试：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testDisplayIsBlankAtStart</span><span class="hljs-params">()</span></span> {
  <span class="hljs-type">XCTAssertEqual</span>(vc.resultsTextView.string, <span class="hljs-string">""</span>)
  <span class="hljs-type">XCTAssertEqual</span>(vc.resultsStackView.views.<span class="hljs-built_in">count</span>, <span class="hljs-number">0</span>)
}
</pre>
    <p>
        运行测试来确认开始的展示如同期望一般。
    </p>
    <p>
        接下来，添加下面的测试来检查Roll按钮被点击之后，数据是否出现：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testDisplayIsFilledInAfterRoll</span><span class="hljs-params">()</span></span> {
  vc.rollButtonClicked(vc.rollButton)

  <span class="hljs-type">XCTAssertNotEqual</span>(vc.resultsTextView.string, <span class="hljs-string">""</span>)
  <span class="hljs-type">XCTAssertEqual</span>(vc.resultsStackView.views.<span class="hljs-built_in">count</span>, <span class="hljs-number">2</span>)
}
</pre>
    <p>
        由于默认的设置中，骰子的数量为2，因此检查stack view有两个view是安全的。但如果你不知道设置是什么，你就无法测试展示的数据是否正确了。
    </p>
    <p>
        查看
        <em>
            ViewController.swift
        </em>
        中的
        <code>
            rollButtonClicked(\_:)
        </code>
        。看看它是如何滚动骰子，然后来展示结果？如果你直接使用已知的数据调用
        <code>
            displayDiceFromRoll(diceRolls:numberOfSides:)
        </code>
        呢？这将允许精确地检查展示。
    </p>
    <p>
        添加下列的测试到
        <em>
            ViewControllerTests.swift
        </em>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testTextResultDisplayIsCorrect</span><span class="hljs-params">()</span></span> {
  <span class="hljs-keyword">let</span> testRolls = [<span class="hljs-number">1</span>, <span class="hljs-number">2</span>, <span class="hljs-number">3</span>, <span class="hljs-number">4</span>, <span class="hljs-number">5</span>, <span class="hljs-number">6</span>]
  vc.displayDiceFromRoll(diceRolls: testRolls)

  <span class="hljs-keyword">var</span> expectedText = <span class="hljs-string">"Total rolled: 21\n"</span>
  expectedText += <span class="hljs-string">"Dice rolled: 1, 2, 3, 4, 5, 6 (6 x 6 sided dice)\n"</span>
  expectedText += <span class="hljs-string">"You rolled: 1 x 1s,  1 x 2s,  1 x 3s,  1 x 4s,  1 x 5s,  1 x 6s"</span>

  <span class="hljs-type">XCTAssertEqual</span>(vc.resultsTextView.string, expectedText)
}
</pre>
    <p>
        运行以验证测试结果如同预期中一样。即6个六面的骰子各自展示可能的一个面。
    </p>
    <p>
        stack view会以一个更加图形化的方式来展示结果，如果可能的话，则使用骰子emoji。将下列的测试插入到
        <em>
            ViewControllerTests.swift
        </em>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testGraphicalResultDisplayIsCorrect</span><span class="hljs-params">()</span></span> {
  <span class="hljs-keyword">let</span> testRolls = [<span class="hljs-number">1</span>, <span class="hljs-number">2</span>, <span class="hljs-number">3</span>, <span class="hljs-number">4</span>, <span class="hljs-number">5</span>, <span class="hljs-number">6</span>]
  vc.displayDiceFromRoll(diceRolls: testRolls)

  <span class="hljs-keyword">let</span> diceEmojis = [<span class="hljs-string">"\u{2680}"</span>, <span class="hljs-string">"\u{2681}"</span>, <span class="hljs-string">"\u{2682}"</span>, <span class="hljs-string">"\u{2683}"</span>, <span class="hljs-string">"\u{2684}"</span>, <span class="hljs-string">"\u{2685}"</span> ]

  <span class="hljs-type">XCTAssertEqual</span>(vc.resultsStackView.views.<span class="hljs-built_in">count</span>, <span class="hljs-number">6</span>)

  <span class="hljs-keyword">for</span> (index, diceView) <span class="hljs-keyword">in</span> vc.resultsStackView.views.enumerated() {
    <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> diceView = diceView <span class="hljs-keyword">as</span>? <span class="hljs-type">NSTextField</span> <span class="hljs-keyword">else</span> {
      <span class="hljs-type">XCTFail</span>(<span class="hljs-string">"View <span class="hljs-subst">\(index)</span> is not NSTextField"</span>)
      <span class="hljs-keyword">return</span>
    }
    <span class="hljs-keyword">let</span> diceViewContent = diceView.stringValue
    <span class="hljs-type">XCTAssertEqual</span>(diceViewContent, diceEmojis[index], <span class="hljs-string">"View <span class="hljs-subst">\(index)</span> is not showing the correct emoji."</span>)
  }
}
</pre>
    <p>
        再次运行测试，以检查交互是否如你所预期一样地执行。剩下的两个测试将展示测试中一个非常有用的技术，通过提供已知的数据给一个方法，再检查结果。
    </p>
    <p>
        如果你感到好奇，有一些重构看起来可以在这里完成！:]
    </p>
    <h3>
        UI测试
    </h3>
    <p>
        是时候去进行UI测试了。关闭assistant editor并打开
        <em>
            High_RollerUITests.swift
        </em>
        。默认的代码非常类似于目前为止你所看到的测试代码，仅仅是在
        <code>
            setup()
        </code>
        中额外的几行有所不同。
    </p>
    <p>
        关于UI测试的一件很有趣的事，就是它可以记录界面的交互。从
        <code>
            testExample()
        </code>
        中移除注释，将光标置于方法内的空白行上，并点击编辑面板左下角的红点以开始录制：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/Record-650x293.png"
        alt="Record-UI-Test" width="650" height="293" class="aligncenter size-large wp-image-142096"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/Record-650x293.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/Record-480x217.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/Record.png 700w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        当app启动的时候，跟随这个交互的顺序，在每一个步骤后稍停一下，让Xcode至少写下一行新的代码：
    </p>
    <ol>
        <li>
            点击“骰子数量”stepper的向上的箭头。
        </li>
        <li>
            再次点击“骰子数量”stepper的向上的箭头。
        </li>
        <li>
            双击“骰子数量”内的text field。
        </li>
        <li>
            输入6并按下Tab键。
        </li>
        <li>
            打开“面数”下拉菜单并选择12。
        </li>
        <li>
            点击“Roll”按钮。
        </li>
    </ol>
    <p>
        再次点击记录按钮以停止记录。
    </p>
    <p>
        Xcode将在该方法中，自动生成对应你的操作的动作。但当你从下拉菜单中选择12的时候，会看到一些奇怪的事情的发送。Xcode无法确定使用哪个选项，因此会将可能的选项都展示给你。在一个复杂的界面中，这个机制对于区分不同的控件是非常重要的，但在本例中第一个选择就可以满足你的需求。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/RecordUITest2.png"
        alt="Record-UI-Test2" width="700" height="223" class="aligncenter size-full wp-image-142151"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/RecordUITest2.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/08/RecordUITest2-480x153.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/RecordUITest2-650x207.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        点击
        <em>
            menuItems[“12”]
        </em>
        旁的向下箭头以查看下拉菜单。选择一项来用足够得容易，但使Xcode相信你的选择并非如此得简单。
    </p>
    <p>
        选择列表中第一个选项，下拉的菜单会消失。然后点击其中一项，这时它仍然会有淡蓝色的背景。当它被选中之后，背景就会带有一个略深一些的蓝色阴影，你可以按Return键来接收这个选择，之后你的代码看起来就类似如下的样子：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testExample</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">let</span> highRollerWindow = <span class="hljs-type">XCUIApplication</span>().windows[<span class="hljs-string">"High Roller"</span>]
    <span class="hljs-keyword">let</span> incrementArrow = highRollerWindow.steppers.children(matching: .incrementArrow).element
    incrementArrow.click()
    incrementArrow.click()
    <span class="hljs-keyword">let</span> textField = highRollerWindow.children(matching: .textField).element
    textField.doubleClick()
    textField.typeText(<span class="hljs-string">"6\t"</span>)
    highRollerWindow.children(matching: .popUpButton).element.click()
    highRollerWindow.menuItems[<span class="hljs-string">"12"</span>].click()
    highRollerWindow.buttons[<span class="hljs-string">"Roll"</span>].click()

  }
</pre>
    <p>
        记录的主要用途，是为了展示访问界面元素的语法。但意料之外的事却是你无法获取到
        <code>
            NSButton
        </code>
        或
        <code>
            NSTextField
        </code>
        的引用，只能通过获取
        <code>
            XCUIElement
        </code>
        来代替。以此来赋予你发送消息和测试一些property的能力。
        <code>
            value
        </code>
        则是
        <code>
            Any
        </code>
        类型的，用来持有
        <code>
            XCUIElement
        </code>
        中最重要的内容。
    </p>
    <p>
        使用记录中的信息来确定如何访问元素。此测试方法将用来检查使用stepper编辑骰子的数量后，text field中的值也可以发生相应的改变：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testIncreasingNumberOfDice</span><span class="hljs-params">()</span></span> {
  <span class="hljs-keyword">let</span> highRollerWindow = <span class="hljs-type">XCUIApplication</span>().windows[<span class="hljs-string">"High Roller"</span>]

  <span class="hljs-keyword">let</span> incrementArrow = highRollerWindow.steppers.children(matching: .incrementArrow).element
  incrementArrow.click()
  incrementArrow.click()

  <span class="hljs-keyword">let</span> textField = highRollerWindow.children(matching: .textField).element
  <span class="hljs-keyword">let</span> textFieldValue = textField.value <span class="hljs-keyword">as</span>? <span class="hljs-type">String</span>

  <span class="hljs-type">XCTAssertEqual</span>(textFieldValue, <span class="hljs-string">"4"</span>)
}
</pre>
    <p>
        保存文件，并点击旁边的小菱形来运行测试。app会运行起来，鼠标指针这时会移动到stepper的向上箭头处，并点击两次。这很有趣，就好像是一个机器人在操作你的app！
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/robot.png"
        alt="robot" width="400" height="375" class="aligncenter size-full wp-image-142097"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/robot.png 400w, https://koenig-media.raywenderlich.com/uploads/2016/08/robot-341x320.png 341w"
        sizes="(max-width: 400px) 100vw, 400px">
    </p>
    <p>
        这比之前的测试会慢很多，但UI测试并非是每天都会被使用的。
    </p>
    <h2>
        网络和异步测试
    </h2>
    <p>
        目前为止，每个人都是高兴的。家庭游戏之夜得以继续，角色扮演的朋友可以滚动所有奇怪的骰子，你的测试也证明了所有的一切都可以正确地工作...但总有些人会造成麻烦：
    </p>
    <p>
        <i>
            “我仍然不相信你的app可以滚动骰子。我发现了一个可以使用大气噪声来滚动骰子的网页。我希望你的app可以使用它。”
        </i>
    </p>
    <p>
        头疼。前往
        <a href="https://www.random.org/dice/" sl-processed="1">
            Random.org
        </a>
        来查看它如何工作。如果URL包含有一个
        <code>
            num
        </code>
        参数，这个网页就会展示滚动很多六面的骰子的结果。似乎和下面这部分的内容相关：
    </p>
    <pre lang="html" class="language-html hljs xml"><span class="hljs-tag">&lt;<span class="hljs-name">p</span>&gt;</span>You rolled 2 dice:<span class="hljs-tag">&lt;/<span class="hljs-name">p</span>&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-name">p</span>&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-name">img</span> <span class="hljs-attr">src</span>=<span class="hljs-string">"dice6.png"</span> <span class="hljs-attr">alt</span>=<span class="hljs-string">"6"</span> /&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-name">img</span> <span class="hljs-attr">src</span>=<span class="hljs-string">"dice1.png"</span> <span class="hljs-attr">alt</span>=<span class="hljs-string">"1"</span> /&gt;</span>
<span class="hljs-tag">&lt;/<span class="hljs-name">p</span>&gt;</span>
</pre>
    <p>
        所以你就可以解析返回的数据，并将其用于骰子的滚动上。打开
        <em>
            WebSource.swift
        </em>
        ，你就可以看到它到底是如何实现的。但你如何测试这点？
    </p>
    <p>
        第一件事就是创建
        <em>
            WebSourceTests.swift
        </em>
        测试文件。选择
        <em>
            File Navigator
        </em>
        中的
        <em>
            High RollerTests
        </em>
        这组，并使用
        <em>
            File/New/File…
        </em>
        中的
        <em>
            macOS/Unit Test Case Class
        </em>
        创建一个名为
        <code>
            WebSourceTests
        </code>
        的类。
    </p>
    <p>
        删除类的内容，并添加下列的import语句：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@testable</span> <span class="hljs-keyword">import</span> High_Roller
</pre>
    <p>
        在assistant editor中打开
        <em>
            WebSource.swift
        </em>
        。
    </p>
    <p>
        在
        <em>
            WebSource.swift
        </em>
        中查看
        <code>
            findRollOnline(numberOfDice:completion:)
        </code>
        方法。这个方法会创建一个
        <code>
            URLRequest
        </code>
        和一个
        <code>
            URLSession
        </code>
        ，然后将它们连接到
        <code>
            URLSessionDataTask
        </code>
        中，它会尝试基于选定骰子的数量，尝试下载相应的网页。
    </p>
    <p>
        收到数据后，它就会解析结果并调用completion handler，并带有骰子的结果或空数组作为参数。
    </p>
    <p>
        作为测试的第一个尝试，添加下列的内容到
        <em>
            WebSourceTests.swift
        </em>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testDownloadingOnlineRollPage</span><span class="hljs-params">()</span></span> {
  <span class="hljs-keyword">let</span> webSource = <span class="hljs-type">WebSource</span>()
  webSource.findRollOnline(numberOfDice: <span class="hljs-number">2</span>) { (result) <span class="hljs-keyword">in</span>
    <span class="hljs-type">XCTAssertEqual</span>(result.<span class="hljs-built_in">count</span>, <span class="hljs-number">2</span>)
  }
}
</pre>
    <p>
        当你运行测试的时候，它会以令人怀疑的速度快速通过。点击左边的位置来添加一个断点在
        <code>
            XCTAssertEqual()
        </code>
        这行。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/breakpoint-650x128.png"
        alt="breakpoint" width="650" height="128" class="aligncenter size-large wp-image-142098"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/breakpoint-650x128.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/breakpoint-480x95.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/breakpoint.png 700w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        再次运行测试，你会发现断点永远不会触发。测试在没有结果返回的情况下就完成了。无需担心，XCTests有办法解决这点，那就是expectation！
    </p>
    <p>
        将之前的测试替换为如下这样：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testDownloadingPageUsingExpectation</span><span class="hljs-params">()</span></span> {
  <span class="hljs-comment">// 1</span>
  <span class="hljs-keyword">let</span> expect = expectation(description: <span class="hljs-string">"waitForWebSource"</span>)
  <span class="hljs-keyword">var</span> diceRollsReceived = <span class="hljs-number">0</span>

  <span class="hljs-keyword">let</span> webSource = <span class="hljs-type">WebSource</span>()
  webSource.findRollOnline(numberOfDice: <span class="hljs-number">2</span>) { (result) <span class="hljs-keyword">in</span>
    diceRollsReceived = result.<span class="hljs-built_in">count</span>
    <span class="hljs-comment">// 2</span>
    expect.fulfill()
  }

  <span class="hljs-comment">// 3</span>
  waitForExpectations(timeout: <span class="hljs-number">10</span>, handler: <span class="hljs-literal">nil</span>)
  <span class="hljs-type">XCTAssertEqual</span>(diceRollsReceived, <span class="hljs-number">2</span>)
}
</pre>
    <p>
        这里有几件新鲜的事值得去关注：
    </p>
    <ol>
        <li>
            用人类可读的描述创建一个
            <code>
                XCTestExpectation
            </code>
            。
        </li>
        <li>
            当数据返回之后，闭包就会被调用，并通过指明现在等待的事情来实现这个期望。
        </li>
        <li>
            为这个测试方法设置一个超时时间，以等待期望被实现。在本例中，如果网页不能在10秒之内返回数据，期望就会超时。
        </li>
    </ol>
    <p>
        这次，在
        <code>
            XCTAssertEqual()
        </code>
        这行设置一个断点，它应当会触发，测试就可以真正地通过了。如果你想看到一个期望超时时会发生什么，可以将超时时间设置为一个非常小的值（比方说0.1秒），并再次运行测试。
    </p>
    <p>
        现在你就了解如何进行异步的测试了，这对于测试网络连接，和长时间的后台任务非常得有用。但如果在未连接到网络的情况下，你想测试网络的代码，或是这个网站已关闭，或是你只想测试地更快一些，该怎么办？
    </p>
    <p>
        在本例中，你可以使用一种叫做
        <em>
            mocking
        </em>
        的测试技术，来模拟你的网络调用。
    </p>
    <h3>
        Mocking
    </h3>
    <p>
        在实际的代码中，
        <code>
            URLSession
        </code>
        是用来启动
        <code>
            URLSessionDataTask
        </code>
        的，用它来返回响应。由于不想访问网络，你可以测试
        <code>
            URLRequest
        </code>
        是正确配置的，而
        <code>
            URLSessionDataTask
        </code>
        可以被创建，
        <code>
            URLSessionDataTask
        </code>
        可以被启动。
    </p>
    <p>
        你将要创建的mock版本的类包括：
        <code>
            MockURLSession
        </code>
        和
        <code>
            MockURLSessionDataTask
        </code>
        ，你可以用它们来代替真实的类。
    </p>
    <p>
        在
        <em>
            WebSourcesTests.swift
        </em>
        文件的底部，
        <code>
            WebSourceTests
        </code>
        类的外部，添加下面的两个新的类：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">MockURLSession</span>: <span class="hljs-title">URLSession</span> </span>{
  <span class="hljs-keyword">var</span> url: <span class="hljs-type">URL</span>?
  <span class="hljs-keyword">var</span> dataTask = <span class="hljs-type">MockURLSessionTask</span>()

  <span class="hljs-keyword">override</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">dataTask</span><span class="hljs-params">(with request: URLRequest, completionHandler: @escaping <span class="hljs-params">(Data?, URLResponse?, Error?)</span></span></span> -&gt; <span class="hljs-type">Void</span>) -&gt; <span class="hljs-type">MockURLSessionTask</span> {
      <span class="hljs-keyword">self</span>.url = request.url
      <span class="hljs-keyword">return</span> dataTask
  }
}

<span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">MockURLSessionTask</span>: <span class="hljs-title">URLSessionDataTask</span> </span>{
  <span class="hljs-keyword">var</span> resumeGotCalled = <span class="hljs-literal">false</span>

  <span class="hljs-keyword">override</span> <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">resume</span><span class="hljs-params">()</span></span> {
    resumeGotCalled = <span class="hljs-literal">true</span>
  }
}
</pre>
    <p>
        <code>
            MockURLSession
        </code>
        继承自
        <code>
            URLSession
        </code>
        ，提供了一个替代版本的
        <code>
            dataTask(with:completionHandler:)
        </code>
        ，它会储存来自提供的
        <code>
            URLRequest
        </code>
        的URL并返回一个
        <code>
            MockURLSessionTask
        </code>
        来替代
        <code>
            URLSessionDataTask
        </code>
        。
    </p>
    <p>
        <code>
            MockURLSessionTask
        </code>
        则继承自
        <code>
            URLSessionDataTask
        </code>
        ，当
        <code>
            resume()
        </code>
        被调用时，并不会真正地访问网络，而是标记一个flag表示此事已发生。
    </p>
    <p>
        添加下列代码到
        <code>
            WebSourceTests
        </code>
        类中，并运行新的测试：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testUsingMockURLSession</span><span class="hljs-params">()</span></span> {
  <span class="hljs-comment">// 1</span>
  <span class="hljs-keyword">let</span> address = <span class="hljs-string">"https://www.random.org/dice/?num=2"</span>
  <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> url = <span class="hljs-type">URL</span>(string: address) <span class="hljs-keyword">else</span> {
    <span class="hljs-type">XCTFail</span>()
    <span class="hljs-keyword">return</span>
  }
  <span class="hljs-keyword">let</span> request = <span class="hljs-type">URLRequest</span>(url: url)

  <span class="hljs-comment">// 2</span>
  <span class="hljs-keyword">let</span> mockSession = <span class="hljs-type">MockURLSession</span>()
  <span class="hljs-type">XCTAssertFalse</span>(mockSession.dataTask.resumeGotCalled)
  <span class="hljs-type">XCTAssertNil</span>(mockSession.url)

  <span class="hljs-comment">// 3</span>
  <span class="hljs-keyword">let</span> task = mockSession.dataTask(with: request) { (data, response, error) <span class="hljs-keyword">in</span> }
  task.resume()

  <span class="hljs-comment">// 4</span>
  <span class="hljs-type">XCTAssertTrue</span>(mockSession.dataTask.resumeGotCalled)
  <span class="hljs-type">XCTAssertEqual</span>(mockSession.url, url)
}
</pre>
    <p>
        这个测试中做了些什么？
    </p>
    <ol>
        <li>
            如同之前一样地构建
            <code>
                URLRequest
            </code>
            。
        </li>
        <li>
            创建一个
            <code>
                MockURLSession
            </code>
            并配置初始的property。
        </li>
        <li>
            创建
            <code>
                MockURLSessionTask
            </code>
            并调用
            <code>
                resume()
            </code>
            。
        </li>
        <li>
            测试这些property发生了如预期中的变化。
        </li>
    </ol>
    <p>
        这就完成了第一部分的测试：
        <code>
            URLRequest
        </code>
        ，
        <code>
            URLSession
        </code>
        ，和
        <code>
            URLSessionDataTask
        </code>
        ，以及data task的启动。现在缺少的测试是解析返回的数据。
    </p>
    <p>
        这里你需要覆盖两个测试的case：返回的数据是否为期望中的格式。
    </p>
    <p>
        添加下列的两个测试到
        <em>
            WebSourcesTests.swift
        </em>
        中并运行：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testParsingGoodData</span><span class="hljs-params">()</span></span> {
  <span class="hljs-keyword">let</span> webSource = <span class="hljs-type">WebSource</span>()
  <span class="hljs-keyword">let</span> goodDataString = <span class="hljs-string">"&lt;p&gt;You rolled 2 dice:&lt;/p&gt;\n&lt;p&gt;\n&lt;img src=\"dice6.png\" alt=\"6\" /&gt;\n&lt;img src=\"dice1.png\" alt=\"1\" /&gt;\n&lt;/p&gt;"</span>
  <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> goodData = goodDataString.data(using: .utf8) <span class="hljs-keyword">else</span> {
    <span class="hljs-type">XCTFail</span>()
    <span class="hljs-keyword">return</span>
  }

  <span class="hljs-keyword">let</span> diceArray = webSource.parseIncomingData(data: goodData)
  <span class="hljs-type">XCTAssertEqual</span>(diceArray, [<span class="hljs-number">6</span>, <span class="hljs-number">1</span>])
}

<span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testParsingBadData</span><span class="hljs-params">()</span></span> {
  <span class="hljs-keyword">let</span> webSource = <span class="hljs-type">WebSource</span>()
  <span class="hljs-keyword">let</span> badDataString = <span class="hljs-string">"This string is not the expected result"</span>
  <span class="hljs-keyword">guard</span> <span class="hljs-keyword">let</span> badData = badDataString.data(using: .utf8) <span class="hljs-keyword">else</span> {
    <span class="hljs-type">XCTFail</span>()
    <span class="hljs-keyword">return</span>
  }

  <span class="hljs-keyword">let</span> diceArray = webSource.parseIncomingData(data: badData)
  <span class="hljs-type">XCTAssertEqual</span>(diceArray, [])
}
</pre>
    <p>
        这里你使用期望来测试了网络连接，mocking来模拟网络，来使得测试可以独立于网络和第三方的网站，最后则提供数据来测试数据的解析，增强独立的能力。
    </p>
    <h2>
        性能测试
    </h2>
    <p>
        Xcode还提供了性能的测试，来检测你代码运行的速度。在
        <em>
            Roll.swift
        </em>
        中的
        <code>
            totalForDice()
        </code>
        ，使用
        <code>
            flatMap
        </code>
        和
        <code>
            reduce
        </code>
        来计算骰子的总数，且允许
        <code>
            value
        </code>
        是可选类型的。但这是最快的方法么？
    </p>
    <p>
        为了测试性能，在
        <em>
            File Navigator
        </em>
        中选择
        <em>
            High RollerTests
        </em>
        这组，并使用
        <em>
            File/New/File...
        </em>
        中的
        <em>
            macOS/Unit Test Case Class
        </em>
        创建一个名为
        <code>
            PerformanceTests
        </code>
        的类。
    </p>
    <p>
        如你所想，和之前一样，删除类中的内容，并添加下列的import：
    </p>
    <pre lang="swift" class="language-swift hljs"><span class="hljs-meta">@testable</span> <span class="hljs-keyword">import</span> High_Roller
</pre>
    <p>
        插入下列的测试方法：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testPerformanceTotalForDice_FlatMap_Reduce</span><span class="hljs-params">()</span></span> {
    <span class="hljs-comment">// 1</span>
    <span class="hljs-keyword">var</span> roll = <span class="hljs-type">Roll</span>()
    roll.changeNumberOfDice(newDiceCount: <span class="hljs-number">20</span>)
    roll.rollAll()
    <span class="hljs-comment">// 2</span>
    <span class="hljs-keyword">self</span>.measure {
      <span class="hljs-comment">// 3</span>
      <span class="hljs-number">_</span> = roll.totalForDice()
    }
  }
</pre>
    <p>
        上述的测试：
    </p>
    <ol>
        <li>
            用20个
            <code>
                Dice
            </code>
            设置
            <code>
                Roll
            </code>
            。
        </li>
        <li>
            <code>
                self.measure
            </code>
            则定义了定时的block。
        </li>
        <li>
            这里就是将被测量的代码。
        </li>
    </ol>
    <p>
        运行测试，你将会看到类似如下的结果：
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/PerformanceTest-650x239.png"
        alt="PerformanceTest" width="650" height="239" class="aligncenter size-large wp-image-141412"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/PerformanceTest-650x239.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/PerformanceTest-480x176.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/PerformanceTest.png 700w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        在获得绿色的勾的标记的同时，你还会看到一个速度的标识，显示“Time: 0.000 sec (98% STDEV)”。
        STDEV（标注偏差）会表明这里和之前的结果是否存在有重大的差别。在本例中，这里就一个结果 - 0 - 因此STDEV是无意义的。无意义的结果就是0.000秒了，因此需要更长的测试。要做到这点，最简单的方式就是添加循环来重复measure block足够多的次数，以此获取到实际的时间。
    </p>
    <p>
        将测试替换为如下的代码：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testPerformanceTotalForDice_FlatMap_Reduce</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">var</span> roll = <span class="hljs-type">Roll</span>()
    roll.changeNumberOfDice(newDiceCount: <span class="hljs-number">20</span>)
    roll.rollAll()
    <span class="hljs-keyword">self</span>.measure {
      <span class="hljs-keyword">for</span> <span class="hljs-number">_</span> <span class="hljs-keyword">in</span> <span class="hljs-number">0</span> ..&lt; <span class="hljs-number">10_000</span> {
        <span class="hljs-number">_</span> = roll.totalForDice()
      }
    }
  }
</pre>
    <p>
        再次运行测试。你得到的结果会依赖于你的处理器，在我这里大约是0.2秒。可以调整循环的次数，让你最后所得到的时间接近0.2秒。
    </p>
    <p>
        还有三种可能的方式来增加total。在assistant editor中打开
        <em>
            Roll.swift
        </em>
        并添加下列的代码：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">totalForDice2</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">Int</span> {
    <span class="hljs-keyword">let</span> total = dice
      .<span class="hljs-built_in">filter</span> { $<span class="hljs-number">0</span>.value != <span class="hljs-literal">nil</span> }
      .<span class="hljs-built_in">reduce</span>(<span class="hljs-number">0</span>) { $<span class="hljs-number">0</span> + $<span class="hljs-number">1</span>.value! }
    <span class="hljs-keyword">return</span> total
  }

  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">totalForDice3</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">Int</span> {
    <span class="hljs-keyword">let</span> total = dice
      .<span class="hljs-built_in">reduce</span>(<span class="hljs-number">0</span>) { $<span class="hljs-number">0</span> + ($<span class="hljs-number">1</span>.value ?? <span class="hljs-number">0</span>) }
    <span class="hljs-keyword">return</span> total
  }

  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">totalForDice4</span><span class="hljs-params">()</span></span> -&gt; <span class="hljs-type">Int</span> {
    <span class="hljs-keyword">var</span> total = <span class="hljs-number">0</span>
    <span class="hljs-keyword">for</span> d <span class="hljs-keyword">in</span> dice {
      <span class="hljs-keyword">if</span> <span class="hljs-keyword">let</span> dieValue = d.value {
        total += dieValue
      }
    }
    <span class="hljs-keyword">return</span> total
  }
</pre>
    <p>
        下面则是相应的性能测试，你可以将它们添加到
        <em>
            PerformanceTests.swift
        </em>
        中：
    </p>
    <pre lang="swift" class="language-swift hljs">  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testPerformanceTotalForDice2_Filter_Reduce</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">var</span> roll = <span class="hljs-type">Roll</span>()
    roll.changeNumberOfDice(newDiceCount: <span class="hljs-number">20</span>)
    roll.rollAll()
    <span class="hljs-keyword">self</span>.measure {
      <span class="hljs-keyword">for</span> <span class="hljs-number">_</span> <span class="hljs-keyword">in</span> <span class="hljs-number">0</span> ..&lt; <span class="hljs-number">10_000</span> {
        <span class="hljs-number">_</span> = roll.totalForDice2()
      }
    }
  }

  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testPerformanceTotalForDice3_Reduce</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">var</span> roll = <span class="hljs-type">Roll</span>()
    roll.changeNumberOfDice(newDiceCount: <span class="hljs-number">20</span>)
    roll.rollAll()
    <span class="hljs-keyword">self</span>.measure {
      <span class="hljs-keyword">for</span> <span class="hljs-number">_</span> <span class="hljs-keyword">in</span> <span class="hljs-number">0</span> ..&lt; <span class="hljs-number">10_000</span> {
        <span class="hljs-number">_</span> = roll.totalForDice3()
      }
    }
  }

  <span class="hljs-function"><span class="hljs-keyword">func</span> <span class="hljs-title">testPerformanceTotalForDice4_Old_Style</span><span class="hljs-params">()</span></span> {
    <span class="hljs-keyword">var</span> roll = <span class="hljs-type">Roll</span>()
    roll.changeNumberOfDice(newDiceCount: <span class="hljs-number">20</span>)
    roll.rollAll()
    <span class="hljs-keyword">self</span>.measure {
      <span class="hljs-keyword">for</span> <span class="hljs-number">_</span> <span class="hljs-keyword">in</span> <span class="hljs-number">0</span> ..&lt; <span class="hljs-number">10_000</span> {
        <span class="hljs-number">_</span> = roll.totalForDice4()
      }
    }
  }
</pre>
    <p>
        运行这些测试，看下那种方式是最快的。你能猜出那种是最快的么？反正我不能！
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/tortoise.png"
        alt="tortoise" width="500" height="274" class="aligncenter size-full wp-image-142099"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/tortoise.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/08/tortoise-480x263.png 480w"
        sizes="(max-width: 500px) 100vw, 500px">
    </p>
    <h2>
        代码覆盖
    </h2>
    <p>
        我们要讨论的最后一个Xcode测试工具就是代码覆盖了，它会用来统计这一系列的测试覆盖了你多少的代码。默认它是关闭的，要将其打开，只需在窗口顶部的schemes下拉菜单中选择
        <em>
            Edit Scheme…
        </em>
        ，然后选择左侧一列的
        <em>
            Test
        </em>
        并勾选
        <em>
            Gather coverage data
        </em>
        。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/TurnOnCodeCoverage-650x362.png"
        alt="Turn-On-Code-Coverage" width="650" height="362" class="aligncenter size-large wp-image-141417"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/TurnOnCodeCoverage-650x362.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/TurnOnCodeCoverage-480x267.png 480w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        关闭这个窗口并按下
        <em>
            Command-U
        </em>
        键来重新运行所有的测试。完成之后，切到
        <em>
            Report Navigator
        </em>
        并选择latest这项。
    </p>
    <p>
        你会看到测试报告展示了一系列绿色的勾的标记，以及一些性能测试的计时。如果你无法看到这些，请确认在左上角选择了
        <em>
            All
        </em>
        开关。
    </p>
    <p>
        点击这里顶部的
        <em>
            Coverage
        </em>
        ，并使鼠标经过蓝条之上，你会看到你的测试覆盖了你将近80%的代码。令人惊奇的工作！:]
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/CodeCoverage4.png"
        alt="Code-Coverage-4" width="700" height="341" class="aligncenter size-full wp-image-142193"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/CodeCoverage4.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/08/CodeCoverage4-480x234.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/CodeCoverage4-650x317.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        两个model对象（
        <code>
            Dice
        </code>
        和
        <code>
            Roll
        </code>
        ）都被很好地覆盖了。如果你只想添加一些测试，model就是开始的最好的地方。
    </p>
    <p>
        还有一种很好的，并且可以快速提高代码覆盖率的方法：删除未使用过的代码。如
        <em>
            AppDelegate.swift
        </em>
        ，它的代码覆盖率仅为50%。
    </p>
    <p>
        切到
        <em>
            AppDelegate.swift
        </em>
        。在右侧的“沟”上，上下移动鼠标，你会看到在测试过程中调用过的代码被标记成了绿色，未调用过的则标记成了红色。
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/Code_not_covered-650x161.png"
        alt="Uncovered-code" width="650" height="161" class="aligncenter size-large wp-image-142100"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/Code_not_covered-650x161.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/Code_not_covered-480x119.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/Code_not_covered.png 700w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        在本例中，
        <code>
            applicationWillTerminate(\_:)
        </code>
        方法从未被使用过，但却显著地减小了代码覆盖率。由于本app用不到这个方法，就可以将它直接删除。再次运行所有的测试，
        <em>
            AppDelegate.swift
        </em>
        就变到100%了。
    </p>
    <p>
        这个看起来像是在骗系统，但移除任何会使你app变杂乱的无用代码确实是一个很好的实践。Xcode为了使用方便，会在新建文件时提供很多的模板代码，但如果你不需要的话，删除即可。
    </p>
    <div class="note">
        <em>
            注意：
        </em>
        如果你觉得代码的“沟”，和红色绿色的标记会让你分心，可以通过
        <em>
            Editor
        </em>
        菜单中的
        <em>
            Hide Code Coverage
        </em>
        来将它们关闭。这并不会让Xcode停止收集代码覆盖的数据，只是让它在你编辑的时候先不要展示出来。
    </div>
    <p>
        关于代码覆盖有一些小小的提示：它只是一个工具，而不是一个目标！一些开发者会将它看做是一个目标，必须保持一个很高的代码覆盖率才可以，但也有可能是通过无意义的测试来获得的较高百分比。测试应当要经过很好的考虑，而不是仅仅为了增加你的代码覆盖率。
    </p>
    <p>
        测试可能在调用了你大量代码的情况下，并没有实际地检查它们的结果是否正确。尽管一个较高的代码覆盖率的数据可能会比较低的好一些，但这并不能完全地代表了代码的质量就会更好。
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
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/08/HighRoller-final.zip"
        sl-processed="1">
            这里
        </a>
        下载最终版本的项目。
    </p>
    <p>
        关于使用Xcode测试，苹果有一系列的
        <a href="https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/testing_with_xcode/"
        sl-processed="1">
            文档
        </a>
        及相关的WWDC视频。
    </p>
    <p>
        <a href="http://nshipster.com/xctestcase/" sl-processed="1">
            NSHipster
        </a>
        中有关于各种断言，以及编写测试你需要知道的地方非常有用的总结。
    </p>
    <p>
        关于TDD的更多信息，可以参考
        <a href="http://www.butunclebob.com/ArticleS.UncleBob.TheThreeRulesOfTdd"
        sl-processed="1">
            Uncle Bob’s excellent site
        </a>
        。
    </p>
    <p>
        如果感兴趣于UITests的更多内容？请访问
        <a href="http://masilotti.com/ui-testing-cheat-sheet/" sl-processed="1">
            Joe Masilotti’s excellent cheat sheet
        </a>
        。
    </p>
</div>