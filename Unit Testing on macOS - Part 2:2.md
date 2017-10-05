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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1420901">
                    <td class="code" id="p142090code1">
                        <pre class="swift" style="font-family:monospace;">
                            @testable import High_Roller
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        插入下列的代码到
        <code>
            ViewControllerTests
        </code>
        类中：
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1420902">
                    <td class="code" id="p142090code2">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 var vc: ViewController! &nbsp; override func setUp() { super.setUp()
                            &nbsp; // 2 let storyboard = NSStoryboard(name: "Main", bundle: nil) vc
                            = storyboard.instantiateController(withIdentifier: "ViewController") as!
                            ViewController &nbsp; // 3 _ = vc.view }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1420903">
                    <td class="code" id="p142090code3">
                        <pre class="swift" style="font-family:monospace;">
                            func testViewControllerIsCreated() { XCTAssertNotNil(vc) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1420904">
                    <td class="code" id="p142090code4">
                        <pre class="swift" style="font-family:monospace;">
                            func testControlsHaveDefaultData() { XCTAssertEqual(vc.numberOfDiceTextField.stringValue,
                            String(2)) XCTAssertEqual(vc.numberOfDiceStepper.integerValue, 2) XCTAssertEqual(vc.numberOfSidesPopup.titleOfSelectedItem,
                            String(6)) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1420905">
                    <td class="code" id="p142090code5">
                        <pre class="swift" style="font-family:monospace;">
                            func testChangingTextFieldChangesStepper() { vc.numberOfDiceTextField.stringValue
                            = String(4) vc.numberOfDiceTextFieldChanged(vc.numberOfDiceTextField) &nbsp;
                            XCTAssertEqual(vc.numberOfDiceTextField.stringValue, String(4)) XCTAssertEqual(vc.numberOfDiceStepper.integerValue,
                            4) } &nbsp; func testChangingStepperChangesTextField() { vc.numberOfDiceStepper.integerValue
                            = 10 vc.numberOfDiceStepperChanged(vc.numberOfDiceStepper) &nbsp; XCTAssertEqual(vc.numberOfDiceTextField.stringValue,
                            String(10)) XCTAssertEqual(vc.numberOfDiceStepper.integerValue, 10) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Run the tests to see the result. You should also test the view controller’s
        variables and confirm that they are being changed as expected by events
        from the interface elements.
    </p>
    <p>
        The view controller has a
        <code>
            Roll
        </code>
        object which has its own properties. Add the following test to check that
        the
        <code>
            Roll
        </code>
        object exists and has the expected default properties:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1420906">
                    <td class="code" id="p142090code6">
                        <pre class="swift" style="font-family:monospace;">
                            func testViewControllerHasRollObject() { XCTAssertNotNil(vc.roll) } &nbsp;
                            func testRollHasDefaultSettings() { XCTAssertEqual(vc.roll.numberOfSides,
                            6) XCTAssertEqual(vc.roll.dice.count, 2) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Next, you need to confirm that changing a setting using one of the interface
        elements actually changes the setting in the
        <code>
            Roll
        </code>
        object. Add the following tests:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1420907">
                    <td class="code" id="p142090code7">
                        <pre class="swift" style="font-family:monospace;">
                            func testChangingNumberOfDiceInTextFieldChangesRoll() { vc.numberOfDiceTextField.stringValue
                            = String(4) vc.numberOfDiceTextFieldChanged(vc.numberOfDiceTextField) &nbsp;
                            XCTAssertEqual(vc.roll.dice.count, 4) } &nbsp; func testChangingNumberOfDiceInStepperChangesRoll()
                            { vc.numberOfDiceStepper.integerValue = 10 vc.numberOfDiceStepperChanged(vc.numberOfDiceStepper)
                            &nbsp; XCTAssertEqual(vc.roll.dice.count, 10) } &nbsp; func testChangingNumberOfSidesPopupChangesRoll()
                            { vc.numberOfSidesPopup.selectItem(withTitle: "20") vc.numberOfSidesPopupChanged(vc.numberOfSidesPopup)
                            &nbsp; XCTAssertEqual(vc.roll.numberOfSides, 20) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        These three tests operate the text field, the stepper and the popup. After
        each change, they check that the
        <code>
            roll
        </code>
        property has changed to match.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        in the assistant editor and look at
        <code>
            rollButtonClicked(\_:)
        </code>
        . It does three things:
    </p>
    <ol>
        <li>
            Makes sure that any ongoing edit in the number of dice text field is processed.
        </li>
        <li>
            Tells the
            <code>
                Roll
            </code>
            struct to roll all the dice.
        </li>
        <li>
            Displays the results.
        </li>
    </ol>
    <p>
        You have already written tests to confirm that
        <code>
            rollAll()
        </code>
        works as expected, but
        <code>
            displayDiceFromRoll(diceRolls:numberOfSides:)
        </code>
        needs to be tested as part of the interface tests. The display methods
        are all in
        <em>
            ViewControllerDisplay.swift
        </em>
        , which is a separate file containing an extension to
        <code>
            ViewController
        </code>
        . This is just an organizational split to keep
        <em>
            ViewController.swift
        </em>
        smaller and to keep the display functions all collected in one place.
    </p>
    <p>
        Look in
        <em>
            ViewControllerDisplay.swift
        </em>
        and you’ll see a bunch of private functions and one public function:
        <code>
            displayDiceFromRoll(diceRolls:numberOfSides:)
        </code>
        , This clears the display, fills in the textual information and then populates
        a stack view with a series of sub-views, one for each die.
    </p>
    <p>
        As with all testing, it is important to start in the right place. The
        first test to write is one that checks that the results text view and stack
        view are empty at the start.
    </p>
    <p>
        Go to
        <em>
            ViewControllerTests.swift
        </em>
        and add this test:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1420908">
                    <td class="code" id="p142090code8">
                        <pre class="swift" style="font-family:monospace;">
                            func testDisplayIsBlankAtStart() { XCTAssertEqual(vc.resultsTextView.string,
                            "") XCTAssertEqual(vc.resultsStackView.views.count, 0) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Run this test to confirm that the display starts off as expected.
    </p>
    <p>
        Next, add the test below to check if data appears after the Roll button
        is clicked:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1420909">
                    <td class="code" id="p142090code9">
                        <pre class="swift" style="font-family:monospace;">
                            func testDisplayIsFilledInAfterRoll() { vc.rollButtonClicked(vc.rollButton)
                            &nbsp; XCTAssertNotEqual(vc.resultsTextView.string, "") XCTAssertEqual(vc.resultsStackView.views.count,
                            2) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Since the default setting for the number of dice is 2, it’s safe to check
        that the stack view has two views. But if you don’t know what the settings
        might be, you can’t test to see whether the data displayed is correct.
    </p>
    <p>
        Look back at
        <code>
            rollButtonClicked(\_:)
        </code>
        in
        <em>
            ViewController.swift
        </em>
        . See how it rolls the dice and then displays the result? What if you
        called
        <code>
            displayDiceFromRoll(diceRolls:numberOfSides:)
        </code>
        directly with known data? That would allow exact checking of the display.
    </p>
    <p>
        Add the following test to
        <em>
            ViewControllerTests.swift
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209010">
                    <td class="code" id="p142090code10">
                        <pre class="swift" style="font-family:monospace;">
                            func testTextResultDisplayIsCorrect() { let testRolls = [1, 2, 3, 4, 5,
                            6] vc.displayDiceFromRoll(diceRolls: testRolls) &nbsp; var expectedText
                            = "Total rolled: 21\n" expectedText += "Dice rolled: 1, 2, 3, 4, 5, 6 (6
                            x 6 sided dice)\n" expectedText += "You rolled: 1 x 1s, 1 x 2s, 1 x 3s,
                            1 x 4s, 1 x 5s, 1 x 6s" &nbsp; XCTAssertEqual(vc.resultsTextView.string,
                            expectedText) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Run it to confirm that the test result is as expected for a roll with
        6 six-sided dice showing one of each possible sides.
    </p>
    <p>
        The stack view shows the results in a more graphical way using dice emojis
        if possible. Insert this test into
        <em>
            ViewControllerTests.swift
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209011">
                    <td class="code" id="p142090code11">
                        <pre class="swift" style="font-family:monospace;">
                            func testGraphicalResultDisplayIsCorrect() { let testRolls = [1, 2, 3,
                            4, 5, 6] vc.displayDiceFromRoll(diceRolls: testRolls) &nbsp; let diceEmojis
                            = ["\u{2680}", "\u{2681}", "\u{2682}", "\u{2683}", "\u{2684}", "\u{2685}"
                            ] &nbsp; XCTAssertEqual(vc.resultsStackView.views.count, 6) &nbsp; for
                            (index, diceView) in vc.resultsStackView.views.enumerated() { guard let
                            diceView = diceView as? NSTextField else { XCTFail("View \(index) is not
                            NSTextField") return } let diceViewContent = diceView.stringValue XCTAssertEqual(diceViewContent,
                            diceEmojis[index], "View \(index) is not showing the correct emoji.") }
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Run the tests again to check that the interface is acting as you expect.
        These last two tests demonstrate a very useful technique for testing, by
        supplying known data to a method and checking the result.
    </p>
    <p>
        If you’re feeling keen, it looks like there is some re-factoring that
        could be done here! :]
    </p>
    <h3>
        UI Testing
    </h3>
    <p>
        Time to move on to the UITests. Close the assistant editor and open
        <em>
            High_RollerUITests.swift
        </em>
        . The default code is very similar to the testing code you’ve been using
        so far, with just a couple of extra lines in
        <code>
            setup()
        </code>
        .
    </p>
    <p>
        One interesting thing about UITests is their ability to record interface
        interactions. Remove the comments from inside
        <code>
            testExample()
        </code>
        , place the cursor on a blank line inside the function and click the red
        dot at the bottom left of the edit pane to start recording:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/Record-650x293.png"
        alt="Record-UI-Test" width="650" height="293" class="aligncenter size-large wp-image-142096"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/Record-650x293.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/Record-480x217.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/Record.png 700w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        When the app starts, follow this sequence of interactions, pausing after
        each step to let Xcode write at least one new line:
    </p>
    <ol>
        <li>
            Click the up arrow on the “Number of dice” stepper.
        </li>
        <li>
            Click the up arrow on the “Number of dice” stepper again.
        </li>
        <li>
            Double-click inside the “Number of dice” text field.
        </li>
        <li>
            Type 6 and press Tab.
        </li>
        <li>
            Open the “Number of sides” popup and select 12.
        </li>
        <li>
            Click the “Roll” button.
        </li>
    </ol>
    <p>
        Click the record button again to stop recording.
    </p>
    <p>
        Xcode will have filled in the function with details of your actions, but
        you will see one odd thing where you selected 12 from the popup. Xcode
        can’t quite decide what option to use, so it shows you a number of possibilities.
        In a complex interface, this might be important to distinguish between
        different controls, but in this case the first option is sufficient for
        your needs.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/RecordUITest2.png"
        alt="Record-UI-Test2" width="700" height="223" class="aligncenter size-full wp-image-142151"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/RecordUITest2.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/08/RecordUITest2-480x153.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/RecordUITest2-650x207.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Click on the down arrow beside
        <em>
            menuItems[“12”]
        </em>
        to see the popup. Choosing the one to use is easy enough, but convincing
        Xcode of your choice is not so straightforward.
    </p>
    <p>
        Select the first option in the list which will dismiss the popup. Then
        click on the item which will still have a pale blue background. When it’s
        selected, the background will have a slightly darker shade of blue; you
        can then press Return to accept this choice, which will leave your code
        looking like this:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209012">
                    <td class="code" id="p142090code12">
                        <pre class="swift" style="font-family:monospace;">
                            func testExample() { &nbsp; let highRollerWindow = XCUIApplication().windows["High
                            Roller"] let incrementArrow = highRollerWindow.steppers.children(matching:
                            .incrementArrow).element incrementArrow.click() incrementArrow.click()
                            &nbsp; let textField = highRollerWindow.children(matching: .textField).element
                            textField.doubleClick() textField.typeText("6\t") highRollerWindow.children(matching:
                            .popUpButton).element.click() highRollerWindow.menuItems["12"].click()
                            highRollerWindow.buttons["Roll"].click() &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The main use for recording is to show the syntax for accessing the interface
        elements. The unexpected thing is that you aren’t getting
        <code>
            NSButton
        </code>
        or
        <code>
            NSTextField
        </code>
        references; you’re getting
        <code>
            XCUIElement
        </code>
        s instead. This gives you the ability to send messages and test a limited
        number of properties.
        <code>
            value
        </code>
        is an
        <code>
            Any
        </code>
        that will usually hold the most important content of the
        <code>
            XCUIElement
        </code>
        .
    </p>
    <p>
        Using the information in the recording to work out how to access the elements,
        this test function checks to see that editing the number of dice using
        the stepper also changes the text field:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209013">
                    <td class="code" id="p142090code13">
                        <pre class="swift" style="font-family:monospace;">
                            func testIncreasingNumberOfDice() { let highRollerWindow = XCUIApplication().windows["High
                            Roller"] &nbsp; let incrementArrow = highRollerWindow.steppers.children(matching:
                            .incrementArrow).element incrementArrow.click() incrementArrow.click()
                            &nbsp; let textField = highRollerWindow.children(matching: .textField).element
                            let textFieldValue = textField.value as? String &nbsp; XCTAssertEqual(textFieldValue,
                            "4") }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Save the file and run the test by clicking in the little diamond in the
        margin beside it. The app will run, the mouse pointer will be moved to
        the stepper’s up arrow and it will click twice. This is fun, like having
        a robot operate your app!
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/robot.png"
        alt="robot" width="400" height="375" class="aligncenter size-full wp-image-142097"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/robot.png 400w, https://koenig-media.raywenderlich.com/uploads/2016/08/robot-341x320.png 341w"
        sizes="(max-width: 400px) 100vw, 400px">
    </p>
    <p>
        It’s a lot slower than the previous tests, though, so UITesting is not
        for everyday use.
    </p>
    <h2>
        Network and Asynchronous Tests
    </h2>
    <p>
        So far, everyone is happy. Family games night is going ahead, your role-playing
        friends have the option to roll all their weird dice, your tests prove
        that everything is working correctly…. but there is always someone who
        causes trouble:
    </p>
    <p>
        <i>
            “I still don’t trust your app to roll the dice. I found a web page that
            generates dice rolls using atmospheric noise. I want your app to use that
            instead.”
        </i>
    </p>
    <p>
        Sigh. Head to
        <a href="https://www.random.org/dice/" sl-processed="1">
            Random.org
        </a>
        to see how this works. If the URL contains a
        <code>
            num
        </code>
        parameter, the page shows the results of rolling that many 6-sided dice.
        Inspecting the source code for the page, it looks like this is the relevant
        section:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209014">
                    <td class="code" id="p142090code14">
                        <pre class="html" style="font-family:monospace;">
                            &lt;p&gt;You rolled 2 dice:&lt;/p&gt; &lt;p&gt; &lt;img src="dice6.png"
                            alt="6" /&gt; &lt;img src="dice1.png" alt="1" /&gt; &lt;/p&gt;
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        So you could parse the data returned and use that data for the roll. Check
        out
        <em>
            WebSource.swift
        </em>
        and you’ll see this is exactly what it does. But how do you test this?
    </p>
    <p>
        The first thing is to make a
        <em>
            WebSourceTests.swift
        </em>
        test file. Select the
        <em>
            High RollerTests
        </em>
        group in the
        <em>
            File Navigator
        </em>
        and use
        <em>
            File\New\File…
        </em>
        to make a new
        <em>
            macOS\Unit Test Case Class
        </em>
        and name it
        <code>
            WebSourceTests
        </code>
        .
    </p>
    <p>
        Delete the contents of the class and add the following import statement:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209015">
                    <td class="code" id="p142090code15">
                        <pre class="swift" style="font-family:monospace;">
                            @testable import High_Roller
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Open
        <em>
            WebSource.swift
        </em>
        in the assistant editor.
    </p>
    <p>
        Look at
        <code>
            findRollOnline(numberOfDice:completion:)
        </code>
        in
        <em>
            WebSource.swift
        </em>
        . This function creates a
        <code>
            URLRequest
        </code>
        and a
        <code>
            URLSession
        </code>
        and then combines them into a
        <code>
            URLSessionDataTask
        </code>
        which tries to download the web page for the selected number of dice.
    </p>
    <p>
        If data arrives, it parses the result and calls the completion handler
        with the dice results or an empty array.
    </p>
    <p>
        As a first attempt at testing, try adding the following to
        <em>
            WebSourceTests.swift
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209016">
                    <td class="code" id="p142090code16">
                        <pre class="swift" style="font-family:monospace;">
                            func testDownloadingOnlineRollPage() { let webSource = WebSource() webSource.findRollOnline(numberOfDice:
                            2) { (result) in XCTAssertEqual(result.count, 2) } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        When you run this test, it passes suspiciously fast. Click in the margin
        to add a breakpoint to the
        <code>
            XCTAssertEqual()
        </code>
        line.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/breakpoint-650x128.png"
        alt="breakpoint" width="650" height="128" class="aligncenter size-large wp-image-142098"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/breakpoint-650x128.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/breakpoint-480x95.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/breakpoint.png 700w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        Run the test again, and your breakpoint never gets triggered. The test
        is completing without waiting for the results to come back. This is a bit
        of a trap, as you could have erroneously assumed that the test passed.
        Never worry, XCTests has the solution to this: expectations!
    </p>
    <p>
        Replace the previous test with this one:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209017">
                    <td class="code" id="p142090code17">
                        <pre class="swift" style="font-family:monospace;">
                            func testDownloadingPageUsingExpectation() { // 1 let expect = expectation(description:
                            "waitForWebSource") var diceRollsReceived = 0 &nbsp; let webSource = WebSource()
                            webSource.findRollOnline(numberOfDice: 2) { (result) in diceRollsReceived
                            = result.count // 2 expect.fulfill() } &nbsp; // 3 waitForExpectations(timeout:
                            10, handler: nil) XCTAssertEqual(diceRollsReceived, 2) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        There are several new things to look at here:
    </p>
    <ol>
        <li>
            Create an
            <code>
                XCTestExpectation
            </code>
            with a human-readable description.
        </li>
        <li>
            When the closure is called after the data has been returned, fulfill this
            expectation by indicating whatever it’s been waiting for has now happened.
        </li>
        <li>
            Set up a timeout for the test function to wait until the expectation has
            been fulfilled. In this case, if the web page hasn’t returned the data
            within 10 seconds, the expectation will timeout.
        </li>
    </ol>
    <p>
        This time, put a breakpoint on the
        <code>
            XCTAssertEqual()
        </code>
        line, and it should trigger and the test will pass for real. If you want
        to see what happens when an expectation times out, set the timeout to something
        really small (0.1 works for me) and run the test again.
    </p>
    <p>
        Now you know how to test asynchronously, which is really useful for network
        access and long background tasks. But what if you want to test your network
        code and you don’t have access to the internet, or the site is down, or
        you just want your tests to run faster?
    </p>
    <p>
        In this case, you can use a testing technique called
        <em>
            mocking
        </em>
        to simulate your network call.
    </p>
    <h3>
        Mocking
    </h3>
    <p>
        In the real code,
        <code>
            URLSession
        </code>
        was used to start a
        <code>
            URLSessionDataTask
        </code>
        which returned the response. Since you don’t want to access the internet,
        you can test that the
        <code>
            URLRequest
        </code>
        is configured correctly, that the
        <code>
            URLSessionDataTask
        </code>
        is created and that the
        <code>
            URLSessionDataTask
        </code>
        is started.
    </p>
    <p>
        You’re going to create mock versions of the classes involved:
        <code>
            MockURLSession
        </code>
        and
        <code>
            MockURLSessionDataTask
        </code>
        , which you can use instead of the real classes.
    </p>
    <p>
        At the bottom of the
        <em>
            WebSourcesTests.swift
        </em>
        file, outside the
        <code>
            WebSourceTests
        </code>
        class, add the following two new classes:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209018">
                    <td class="code" id="p142090code18">
                        <pre class="swift" style="font-family:monospace;">
                            class MockURLSession: URLSession { var url: URL? var dataTask = MockURLSessionTask()
                            &nbsp; override func dataTask(with request: URLRequest, completionHandler:
                            @escaping (Data?, URLResponse?, Error?) -&gt; Void) -&gt; MockURLSessionTask
                            { self.url = request.url return dataTask } } &nbsp; class MockURLSessionTask:
                            URLSessionDataTask { var resumeGotCalled = false &nbsp; override func resume()
                            { resumeGotCalled = true } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        <code>
            MockURLSession
        </code>
        sub-classes
        <code>
            URLSession
        </code>
        , supplying an alternative version of
        <code>
            dataTask(with:completionHandler:)
        </code>
        that stores the URL from the supplied
        <code>
            URLRequest
        </code>
        and returns a
        <code>
            MockURLSessionTask
        </code>
        instead of a
        <code>
            URLSessionDataTask
        </code>
        .
    </p>
    <p>
        <code>
            MockURLSessionTask
        </code>
        sub-classes
        <code>
            URLSessionDataTask
        </code>
        and when
        <code>
            resume()
        </code>
        is called, does not go online but instead sets a flag to show that this
        has happened.
    </p>
    <p>
        Add the following to the
        <code>
            WebSourceTests
        </code>
        class and run the new test:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209019">
                    <td class="code" id="p142090code19">
                        <pre class="swift" style="font-family:monospace;">
                            func testUsingMockURLSession() { // 1 let address = "https://www.random.org/dice/?num=2"
                            guard let url = URL(string: address) else { XCTFail() return } let request
                            = URLRequest(url: url) &nbsp; // 2 let mockSession = MockURLSession() XCTAssertFalse(mockSession.dataTask.resumeGotCalled)
                            XCTAssertNil(mockSession.url) &nbsp; // 3 let task = mockSession.dataTask(with:
                            request) { (data, response, error) in } task.resume() &nbsp; // 4 XCTAssertTrue(mockSession.dataTask.resumeGotCalled)
                            XCTAssertEqual(mockSession.url, url) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        What’s going on in this test?
    </p>
    <ol>
        <li>
            Construct the
            <code>
                URLRequest
            </code>
            as before.
        </li>
        <li>
            Create a
            <code>
                MockURLSession
            </code>
            and confirm the initial properties.
        </li>
        <li>
            Create the
            <code>
                MockURLSessionTask
            </code>
            and call
            <code>
                resume()
            </code>
            .
        </li>
        <li>
            Test that the properties have changed as expected.
        </li>
    </ol>
    <p>
        This test checks the first part of the process: the
        <code>
            URLRequest
        </code>
        , the
        <code>
            URLSession
        </code>
        and the
        <code>
            URLSessionDataTask
        </code>
        , and it tests that the data task is started. What is missing is any test
        for parsing the returned data.
    </p>
    <p>
        There are two test cases you need to cover here: if the data returns matches
        the expected format, and if it does not.
    </p>
    <p>
        Add these two tests to
        <em>
            WebSourcesTests.swift
        </em>
        and run them:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209020">
                    <td class="code" id="p142090code20">
                        <pre class="swift" style="font-family:monospace;">
                            func testParsingGoodData() { let webSource = WebSource() let goodDataString
                            = "&lt;p&gt;You rolled 2 dice:&lt;/p&gt;\n&lt;p&gt;\n&lt;img src=\"dice6.png\"
                            alt=\"6\" /&gt;\n&lt;img src=\"dice1.png\" alt=\"1\" /&gt;\n&lt;/p&gt;"
                            guard let goodData = goodDataString.data(using: .utf8) else { XCTFail()
                            return } &nbsp; let diceArray = webSource.parseIncomingData(data: goodData)
                            XCTAssertEqual(diceArray, [6, 1]) } &nbsp; func testParsingBadData() {
                            let webSource = WebSource() let badDataString = "This string is not the
                            expected result" guard let badData = badDataString.data(using: .utf8) else
                            { XCTFail() return } &nbsp; let diceArray = webSource.parseIncomingData(data:
                            badData) XCTAssertEqual(diceArray, []) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here you have used expectations to test the network connection, mocking
        to simulate the networking to allow tests independent of the network and
        a third-party web site, and finally supplied data to test the data parsing,
        again independently.
    </p>
    <h2>
        Performance Testing
    </h2>
    <p>
        Xcode also offers performance testing to check how fast your code executes.
        In
        <em>
            Roll.swift
        </em>
        ,
        <code>
            totalForDice()
        </code>
        uses
        <code>
            flatMap
        </code>
        and
        <code>
            reduce
        </code>
        to calculate the total for the dice, allowing for the fact that
        <code>
            value
        </code>
        is an optional. But is this the fastest approach?
    </p>
    <p>
        To test performance, select the
        <em>
            High RollerTests
        </em>
        group in the
        <em>
            File Navigator
        </em>
        and use
        <em>
            File\New\File…
        </em>
        to create a new
        <em>
            macOS\Unit Test Case Class
        </em>
        named
        <code>
            PerformanceTests
        </code>
        .
    </p>
    <p>
        Delete the contents of the class and — you guessed it — add the following
        import as you’ve done before:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209021">
                    <td class="code" id="p142090code21">
                        <pre class="swift" style="font-family:monospace;">
                            @testable import High_Roller
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Insert this test function:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209022">
                    <td class="code" id="p142090code22">
                        <pre class="swift" style="font-family:monospace;">
                            func testPerformanceTotalForDice_FlatMap_Reduce() { // 1 var roll = Roll()
                            roll.changeNumberOfDice(newDiceCount: 20) roll.rollAll() &nbsp; // 2 self.measure
                            { // 3 _ = roll.totalForDice() } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The sections of this function are as follows:
    </p>
    <ol>
        <li>
            Set up a
            <code>
                Roll
            </code>
            with 20
            <code>
                Dice
            </code>
            .
        </li>
        <li>
            <code>
                self.measure
            </code>
            defines the timing block.
        </li>
        <li>
            This is the code being measured.
        </li>
    </ol>
    <p>
        Run the test and you will see a result like this:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/PerformanceTest-650x239.png"
        alt="PerformanceTest" width="650" height="239" class="aligncenter size-large wp-image-141412"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/PerformanceTest-650x239.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/PerformanceTest-480x176.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/PerformanceTest.png 700w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        As well as getting the green checkmark symbol, you will see a speed indicator
        which in my test shows “Time: 0.000 sec (98% STDEV)”. The standard deviation
        (STDEV) will indicate if there are any significant changes from the previous
        results. In this case, there is only one result —&nbsp;zero — so STDEV
        is meaningless. Also meaningless is a result of 0.000 seconds, so the test
        needs to be longer. The easiest way to do this is to add a loop that repeats
        the measure block enough times to get an actual time.
    </p>
    <p>
        Replace the test with the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209023">
                    <td class="code" id="p142090code23">
                        <pre class="swift" style="font-family:monospace;">
                            func testPerformanceTotalForDice_FlatMap_Reduce() { var roll = Roll()
                            roll.changeNumberOfDice(newDiceCount: 20) roll.rollAll() &nbsp; self.measure
                            { for _ in 0 ..&lt; 10_000 { _ = roll.totalForDice() } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Run the test again; the result you get will depend on your processor,
        but I get about 0.2 seconds. Adjust the loop counter from
        <code>
            10_000
        </code>
        until you get around 0.2.
    </p>
    <p>
        Here are three other possible ways of adding up the total of the dice.
        Open
        <em>
            Roll.swift
        </em>
        in the assistant editor and add them as follows:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209024">
                    <td class="code" id="p142090code24">
                        <pre class="swift" style="font-family:monospace;">
                            func totalForDice2() -&gt; Int { let total = dice .filter { $0.value !=
                            nil } .reduce(0) { $0 + $1.value! } return total } &nbsp; func totalForDice3()
                            -&gt; Int { let total = dice .reduce(0) { $0 + ($1.value ?? 0) } return
                            total } &nbsp; func totalForDice4() -&gt; Int { var total = 0 for d in
                            dice { if let dieValue = d.value { total += dieValue } } return total }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        And here are the matching performance tests which you should add to
        <em>
            PerformanceTests.swift
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14209025">
                    <td class="code" id="p142090code25">
                        <pre class="swift" style="font-family:monospace;">
                            func testPerformanceTotalForDice2_Filter_Reduce() { var roll = Roll()
                            roll.changeNumberOfDice(newDiceCount: 20) roll.rollAll() &nbsp; self.measure
                            { for _ in 0 ..&lt; 10_000 { _ = roll.totalForDice2() } } } &nbsp; func
                            testPerformanceTotalForDice3_Reduce() { var roll = Roll() roll.changeNumberOfDice(newDiceCount:
                            20) roll.rollAll() &nbsp; self.measure { for _ in 0 ..&lt; 10_000 { _ =
                            roll.totalForDice3() } } } &nbsp; func testPerformanceTotalForDice4_Old_Style()
                            { var roll = Roll() roll.changeNumberOfDice(newDiceCount: 20) roll.rollAll()
                            &nbsp; self.measure { for _ in 0 ..&lt; 10_000 { _ = roll.totalForDice4()
                            } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Run these tests and work out which option is the fastest. Did you guess
        which one would win? I didn’t!
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/tortoise.png"
        alt="tortoise" width="500" height="274" class="aligncenter size-full wp-image-142099"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/tortoise.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/08/tortoise-480x263.png 480w"
        sizes="(max-width: 500px) 100vw, 500px">
    </p>
    <h2>
        Code Coverage
    </h2>
    <p>
        The final Xcode test tool to discuss is code coverage, which is the measure
        of how much of your code is covered during a series of tests. It’s turned
        off by default. To turn it on, select
        <em>
            Edit Scheme…
        </em>
        in the schemes popup at the top of the window. Select
        <em>
            Test
        </em>
        in the column on the left and then check
        <em>
            Gather coverage data
        </em>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/TurnOnCodeCoverage-650x362.png"
        alt="Turn-On-Code-Coverage" width="650" height="362" class="aligncenter size-large wp-image-141417"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/TurnOnCodeCoverage-650x362.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/TurnOnCodeCoverage-480x267.png 480w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        Close that window and press
        <em>
            Command-U
        </em>
        to re-run all the tests. Once the tests are complete, go to the
        <em>
            Report Navigator
        </em>
        and select the latest entry.
    </p>
    <p>
        You’ll see the test report showing a series of green checkmarks, plus
        some timings for the performance tests. If you don’t see this, make sure
        both
        <em>
            All
        </em>
        toggles are selected at the top left.
    </p>
    <p>
        Click on
        <em>
            Coverage
        </em>
        at the top of this display and mouse over the top of the blue bars to
        see that your tests cover nearly 80% of your code. Amazing work! :]
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/CodeCoverage4.png"
        alt="Code-Coverage-4" width="700" height="341" class="aligncenter size-full wp-image-142193"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/CodeCoverage4.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/08/CodeCoverage4-480x234.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/CodeCoverage4-650x317.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        The two model objects (
        <code>
            Dice
        </code>
        and
        <code>
            Roll
        </code>
        ) are very well covered. If you are only going to add some tests, the
        model is the best place to start.
    </p>
    <p>
        There is another good, fast way to improve code coverage: delete code
        that isn’t being used. Look at the coverage for
        <em>
            AppDelegate.swift
        </em>
        , it’s at 50%.
    </p>
    <p>
        Go to the
        <em>
            AppDelegate.swift
        </em>
        file. On the gutter on the right-hand side, mouse up and down and you’ll
        see it shows green for methods called during the tests, and red for methods
        that are not called.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/Code_not_covered-650x161.png"
        alt="Uncovered-code" width="650" height="161" class="aligncenter size-large wp-image-142100"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/Code_not_covered-650x161.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/Code_not_covered-480x119.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/Code_not_covered.png 700w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        In this case,
        <code>
            applicationWillTerminate(\_:)
        </code>
        is not used at all; it’s dramatically decreasing the code coverage for
        this file. Since the app is not using this function, delete it. Now run
        all the tests again and
        <em>
            AppDelegate.swift
        </em>
        has jumped to 100% coverage.
    </p>
    <p>
        This may seem to be cheating the system, but it is actually good practice
        to remove any dead code that is cluttering up your app. Xcode tries to
        be helpful when you make a new file and supplies lots of boilerplate code
        by default, but if you don’t need any of this, delete it.
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        If you find the code coverage gutter and flashes of red and green distracting,
        turn them off by selecting
        <em>
            Hide Code Coverage
        </em>
        from the
        <em>
            Editor
        </em>
        menu. This doesn’t stop Xcode gathering the code coverage data, but stops
        it being displayed while you edit.
    </div>
    <p>
        Now for the warning about code coverage: it is a tool, not a goal! Some
        developers and employers treat it as a goal and insist on a certain percentage.
        But it is possible to get a good percentage without testing meaningfully.
        Tests have to be well thought out and not just added for the sake of increasing
        your code coverage.
    </p>
    <p>
        Tests may call numerous functions in your code without actually checking
        the result. While a high code coverage number is probably better than a
        low one, it doesn’t say anything about the quality of the tests.
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
        You can download the final version of the
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/08/HighRoller-final.zip"
        sl-processed="1">
            sample project here
        </a>
        .
    </p>
    <p>
        Apple has a set of docs about
        <a href="https://developer.apple.com/library/content/documentation/DeveloperTools/Conceptual/testing_with_xcode/"
        sl-processed="1">
            Testing with Xcode
        </a>
        with links to relevant WWDC videos.
    </p>
    <p>
        <a href="http://nshipster.com/xctestcase/" sl-processed="1">
            NSHipster
        </a>
        has a useful summary of the various assertions and what you really need
        to know to write tests.
    </p>
    <p>
        For information about Test Driven Development, check out
        <a href="http://www.butunclebob.com/ArticleS.UncleBob.TheThreeRulesOfTdd"
        sl-processed="1">
            Uncle Bob’s excellent site
        </a>
        .
    </p>
    <p>
        Interested in learning more about UITests? Check out the
        <a href="http://masilotti.com/ui-testing-cheat-sheet/" sl-processed="1">
            Joe Masilotti’s excellent cheat sheet
        </a>
        .
    </p>
    <p>
        I hope you enjoyed this Unit testing tutorial; if you have any questions
        or comments, please join the forum discussion below!
    </p>
</div>