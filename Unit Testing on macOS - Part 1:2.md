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
        Unit testing is one of those things that we all know deep down we should
        be doing, but it seems too difficult, too boring, or too much like hard
        work.
    </p>
    <p>
        It’s so much fun creating code that does exciting things; why would anyone
        want to spend half the time writing code that just checks things?
    </p>
    <p>
        The reason is
        <em>
            confidence
        </em>
        ! In this Unit testing on macOS tutorial, you’ll learn how to test your
        code and you will gain confidence that your code is doing what you want
        it to do, confidence that you can make major changes to your code and confidence
        that you won’t break anything.
    </p>
    <h2>
        Getting Started
    </h2>
    <p>
        This project uses Swift 3 and requires, at a minimum, Xcode 8 beta 6.
        Download the
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/08/HighRoller-starter.zip"
        sl-processed="1">
            starter project
        </a>
        and open it in Xcode.
    </p>
    <p>
        If you have done any other tutorials here at raywenderlich.com, you are
        probably expecting to build and run at this stage, but not this time —
        you are going to test. Go to the
        <em>
            Product
        </em>
        menu and choose
        <em>
            Test
        </em>
        . Note the shortcut —
        <em>
            Command-U
        </em>
        — you’ll be using it a lot.
    </p>
    <p>
        When you run the tests, Xcode will build the app and you will see the
        app window appear a couple of times before you get a message saying “Test
        Succeeded”. In the
        <em>
            Navigator
        </em>
        pane on the left, select
        <em>
            Test navigator
        </em>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/TestNavigator2.png"
        alt="TestNavigator2" width="513" height="346" class="aligncenter size-full wp-image-141436"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/TestNavigator2.png 513w, https://koenig-media.raywenderlich.com/uploads/2016/08/TestNavigator2-474x320.png 474w"
        sizes="(max-width: 513px) 100vw, 513px">
    </p>
    <p>
        This shows you the three tests added by default; each one has a green
        tick beside it, showing that the test passed. To see the file containing
        those tests, click on the second line in the
        <em>
            Test Navigator
        </em>
        where it says
        <em>
            High RollerTests
        </em>
        preceded by an uppercase T icon.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/DefaultTests3.png"
        alt="DefaultTests3" width="700" height="395" class="aligncenter size-full wp-image-142138"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/DefaultTests3.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/08/DefaultTests3-480x271.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/DefaultTests3-650x367.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/DefaultTests3-266x151.png 266w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        There are a few important things to note here:
    </p>
    <ul>
        <li>
            The imports:
            <em>
                XCTest
            </em>
            is the testing framework provided by Xcode.
            <code>
                @testable import High_Roller
            </code>
            is the import that gives the testing code access to all the code in the
            <code>
                High_Roller
            </code>
            module. Every test file will need these two imports.
        </li>
        <li>
            <code>
                setup()
            </code>
            and
            <code>
                tearDown()
            </code>
            : these are called before and after
            <em>
                every single
            </em>
            test method.
        </li>
        <li>
            <code>
                testExample()
            </code>
            and
            <code>
                testPerformanceExample()
            </code>
            : actual tests. The first one tests functionality, and the second one
            tests performance. Every test function name must begin with
            <code>
                test
            </code>
            so that Xcode can recognize it as a test to perform.
        </li>
    </ul>
    <h3>
        What Is Unit Testing?
    </h3>
    <p>
        Before you get into writing your own tests, it’s time for a brief discussion
        about unit testing, what it actually is and why you should use it.
    </p>
    <p>
        A unit test is a function that tests a single piece — or unit — of your
        code. It doesn’t get included in the code of your application, but is used
        during development to check that your code does what you expected.
    </p>
    <p>
        A common first reaction to unit tests is: “Are you telling me I should
        write
        <i>
            twice
        </i>
        as much code? One function for the app itself and
        <i>
            another
        </i>
        to test that function?” Actually, it can be worse than that — some projects
        end up with
        <i>
            more
        </i>
        testing code than production code.
    </p>
    <p>
        At first, this seems like a terrible waste of time and effort — but wait
        until a test catches something that you didn’t spot, or alerts you to a
        side-effect of re-factoring. That’s when you realize what an amazing tool
        this is. After a while, any project without unit tests feels very fragile,
        and you’ll hesitate to make any changes because you cannot be sure what
        will happen.
    </p>
    <h2>
        Test Driven Development
    </h2>
    <p>
        Test Driven Development (TDD) is a branch of unit testing where you start
        with the tests and only write code as required by the tests. Again, this
        seems like a very strange way to proceed at first and can produce some
        very peculiar code as you’ll see in a minute. The upshot is that this process
        really makes you think about the purpose of the code before coding begins.
    </p>
    <p>
        Test Driven Development has three repeating steps:
    </p>
    <ol>
        <li>
            <em>
                Red
            </em>
            : Write a failing test.
        </li>
        <li>
            <em>
                Green
            </em>
            : Write the minimum code needed to make the test pass.
        </li>
        <li>
            <em>
                Refactor
            </em>
            : Optional; if any app or test code can be re-factored to make it better,
            do it now.
        </li>
    </ol>
    <p>
        This sequence is important and the key to effective TDD. Fixing a failing
        test gives you a clear indication you know exactly what your code is doing.
        If your test passes the first time, without any new code being written,
        then you have not correctly pin-pointed the next stage of development.
    </p>
    <p>
        To start, you’ll write a series of tests and the accompanying code using
        TDD.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/dog-239x320.png"
        alt="dog" width="239" height="320" class="alignright size-medium wp-image-142110"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/dog-239x320.png 239w, https://koenig-media.raywenderlich.com/uploads/2016/08/dog-373x500.png 373w, https://koenig-media.raywenderlich.com/uploads/2016/08/dog.png 954w"
        sizes="(max-width: 239px) 100vw, 239px">
    </p>
    <h2>
        The Test Project
    </h2>
    <p>
        This project is a dice rolling utility for board gamers. Ever sit down
        to play a game with the family and discover that the dog ate the dice?
        Now your app can come to the rescue. And if anyone says “I don’t trust
        a computer not to cheat!” you can proudly say that the app has been unit
        tested to prove that it works correctly. That’s bound to impress the family
        — and you will have saved games night. :]
    </p>
    <p>
        The model for this app will have two main object types:
        <code>
            Dice
        </code>
        , which will have a
        <code>
            value
        </code>
        property and a method for generating a random value, and
        <code>
            Roll
        </code>
        , which will be a collection of
        <code>
            Dice
        </code>
        objects with methods for rolling them all, totaling the values and so
        on.
    </p>
    <p>
        This first test class is for the
        <code>
            Dice
        </code>
        object type.
    </p>
    <h2>
        The Dice Test Class
    </h2>
    <p>
        In Xcode go to the
        <em>
            File Navigator
        </em>
        and select the
        <em>
            High RollerTests
        </em>
        group. Select
        <em>
            File\New\File…
        </em>
        and choose
        <em>
            macOS\Unit Test Case Class
        </em>
        . Click
        <em>
            Next
        </em>
        and name the class
        <code>
            DiceTests
        </code>
        . Make sure the language is set to Swift. Click
        <em>
            Next
        </em>
        and
        <em>
            Create
        </em>
        .
    </p>
    <p>
        Select all the code inside the class and delete it. Add the following
        statement to
        <em>
            DiceTests.swift
        </em>
        just under the
        <code>
            import XCTest
        </code>
        line:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1414051">
                    <td class="code" id="p141405code1">
                        <pre class="swift" style="font-family:monospace;">
                            @testable import High_Roller
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now you can delete
        <em>
            HighRollerTests.swift
        </em>
        as you don’t need the default tests any longer.
    </p>
    <p>
        The first thing to test is whether a
        <code>
            Dice
        </code>
        object can be created.
    </p>
    <h3>
        Your First Test
    </h3>
    <p>
        Inside the
        <em>
            DiceTests
        </em>
        class, add the following test function:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1414052">
                    <td class="code" id="p141405code2">
                        <pre class="swift" style="font-family:monospace;">
                            func testForDice() { let _ = Dice() }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This gives a compile error before you can even run the test:
        <code>
            "Use of unresolved identifier 'Dice'"
        </code>
        . In TDD, a test that fails to compile is considered a failing test, so
        you have just completed step 1 of the TDD sequence.
    </p>
    <p>
        To make this test pass with the minimum of code, go to the
        <em>
            File Navigator
        </em>
        and select the
        <em>
            Model
        </em>
        group in the main
        <em>
            High Roller
        </em>
        group. Use
        <em>
            File\New\File…
        </em>
        to create a new Swift file and name it
        <em>
            Dice.swift
        </em>
        .
    </p>
    <p>
        Add the following code to the file:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1414053">
                    <td class="code" id="p141405code3">
                        <pre class="swift" style="font-family:monospace;">
                            struct Dice { &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Go back to
        <em>
            DiceTests.swift
        </em>
        ; the error will still be visible until the next build. However, you can
        now run the test in several different ways.
    </p>
    <p>
        If you click the diamond in the margin beside the test function,
        <em>
            only that single test
        </em>
        will run. Try that now, and the diamond will turn into a green checkmark
        symbol, showing that the test has passed.
    </p>
    <p>
        You can click a green symbol (or a red symbol that shows a failed test)
        at any time to run a test. There will now be another green symbol beside
        the class name. Clicking this will run all the tests
        <em>
            in the class
        </em>
        . At the moment, this is the same as running the single test, but that
        will soon change.
    </p>
    <p>
        The final way to test your code is to run all the tests.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/RunningTests-650x152.png"
        alt="RunningTests" width="650" height="152" class="aligncenter size-large wp-image-142112"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/RunningTests-650x152.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/RunningTests-480x112.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/RunningTests.png 700w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        Press
        <em>
            Command-U
        </em>
        to run all the tests and then go to the
        <em>
            Test Navigator
        </em>
        where you will see your single test in the High RollerTests section; you
        may need to expand the sections to see it. The green checkmark symbols
        appear beside every test. If you move the mouse pointer up and down the
        list of tests, you will see small play buttons appear which you can use
        to run any test or set of tests.
    </p>
    <p>
        In the
        <em>
            Test Navigator
        </em>
        , you can see that the
        <em>
            High RollerUITests
        </em>
        ran as well. The problem with UI Tests are that they’re slow. You want
        your tests to be fast as possible so that there is no drawback to testing
        frequently. To solve this problem, edit the scheme so that the UI Tests
        don’t run automatically.
    </p>
    <p>
        Go to the scheme popup in the toolbar and select
        <em>
            Edit scheme…
        </em>
        . Click
        <em>
            Test
        </em>
        in the pane on the left and un-check
        <em>
            High RollerUITests
        </em>
        . Close the scheme window and run your tests again with
        <em>
            Command-U
        </em>
        . The UI Tests are faded out in the
        <em>
            Test Navigator
        </em>
        , but they can still be run manually.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/TurnOffUITests-650x362.png"
        alt="TurnOffUITests" width="650" height="362" class="aligncenter size-large wp-image-141411"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/TurnOffUITests-650x362.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/TurnOffUITests-480x267.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/TurnOffUITests.png 700w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <h3>
        Choosing Which Tests to Run
    </h3>
    <p>
        So which method should you use for running your tests? Single, class or
        all?
    </p>
    <p>
        If you are working on a test, it is often useful to test it on its own
        or in its class. Once you have a passing test, it is vital to check that
        it hasn’t broken anything else, so you should do a complete test run after
        that.
    </p>
    <p>
        To make things easier as you progress, open
        <em>
            DiceTests.swift
        </em>
        in the
        <em>
            primary editor
        </em>
        and
        <em>
            Dice.swift
        </em>
        in the
        <em>
            assistant editor
        </em>
        . This is a very convenient way to work as you cycle through the TDD sequence.
    </p>
    <p>
        That completes the second step of the TDD sequence; since there is no
        refactoring to be done, it’s time to go back to step 1 and write another
        failing test.
    </p>
    <h3>
        Testing for nil
    </h3>
    <p>
        Every
        <em>
            Dice
        </em>
        object should have a
        <code>
            value
        </code>
        which should be
        <code>
            nil
        </code>
        when the
        <em>
            Dice
        </em>
        object is instantiated.
    </p>
    <p>
        Add the following test to
        <em>
            DiceTests.swift
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1414054">
                    <td class="code" id="p141405code4">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 func testValueForNewDiceIsNil() { let testDie = Dice() &nbsp; //
                            2 XCTAssertNil(testDie.value, "Die value should be nil after init") }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s what this test does:
    </p>
    <ol>
        <li>
            The function name starts with
            <code>
                'test'
            </code>
            , and the remainder of the function name expresses what the test checks.
        </li>
        <li>
            The test uses one of the many
            <code>
                XCTAssert
            </code>
            functions to confirm that the value is
            <code>
                nil
            </code>
            . The second parameter of
            <code>
                XCTAssertNil()
            </code>
            is an optional string that provides the error message if the test fails.
            I generally prefer to use descriptive function names and leave this parameter
            blank in the interests of keeping the actual test code clean and easy to
            read.
        </li>
    </ol>
    <p>
        This test code produces a compile error:
        <code>
            "Value of type 'Dice' has no member 'value'"
        </code>
        .
    </p>
    <p>
        To fix this error, add the following property definition to the
        <code>
            Dice
        </code>
        struct within
        <em>
            Dice.swift
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1414055">
                    <td class="code" id="p141405code5">
                        <pre class="swift" style="font-family:monospace;">
                            var value: Int?
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        In
        <em>
            DiceTests.swift
        </em>
        , the compile error will not disappear until the app is built. Press
        <em>
            Command-U
        </em>
        to build the app and run the tests which should pass. Again there is nothing
        to re-factor.
    </p>
    <p>
        Each
        <code>
            Dice
        </code>
        object has to be able to “roll” itself and generate its value. Add this
        next test to
        <em>
            DiceTests.swift
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1414056">
                    <td class="code" id="p141405code6">
                        <pre class="swift" style="font-family:monospace;">
                            func testRollDie() { var testDie = Dice() testDie.rollDie() &nbsp; XCTAssertNotNil(testDie.value)
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This test uses
        <code>
            XCTAssertNotNil()
        </code>
        instead of
        <code>
            XCTAssertNil()
        </code>
        from the previous test.
    </p>
    <p>
        As the Dice struct has no
        <code>
            rollDie()
        </code>
        method, this will inevitably cause another compile error. To fix it, switch
        back to the
        <em>
            Assistant Editor
        </em>
        and add the following to
        <em>
            Dice.swift
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1414057">
                    <td class="code" id="p141405code7">
                        <pre class="swift" style="font-family:monospace;">
                            func rollDie() { &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Run the tests; you’ll see a warning about using
        <code>
            var
        </code>
        instead of
        <code>
            let
        </code>
        along with a note that
        <code>
            XCTAssert
        </code>
        has failed this time. That makes sense, since
        <code>
            rollDie()
        </code>
        isn’t doing anything yet. Change
        <code>
            rollDie()
        </code>
        as shown below:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1414058">
                    <td class="code" id="p141405code8">
                        <pre class="swift" style="font-family:monospace;">
                            mutating func rollDie() { value = 0 }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now you are seeing how TDD can produce some odd code. You know that eventually
        the
        <code>
            Dice
        </code>
        struct has to produce random dice values, but you haven’t written a test
        asking for that yet, so this function is the minimum code need to pass
        the test. Run all the tests again to prove this.
    </p>
    <h3>
        Developing to Tests
    </h3>
    <p>
        Put your thinking cap on — these next tests are designed to shape the
        way your code comes together. This can feel backwards at first, but it’s
        a very powerful way to make you focus on the true intent of your code.
    </p>
    <p>
        You know that a standard die has six sides, so the value of any die after
        rolling should be between 1 and 6 inclusive. Go back to
        <em>
            DiceTests.swift
        </em>
        and add this test, which introduces two more
        <code>
            XCTAssert
        </code>
        functions:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1414059">
                    <td class="code" id="p141405code9">
                        <pre class="swift" style="font-family:monospace;">
                            func testDiceRoll_ShouldBeFromOneToSix() { var testDie = Dice() testDie.rollDie()
                            &nbsp; XCTAssertTrue(testDie.value! &gt;= 1) XCTAssertTrue(testDie.value!
                            &lt;= 6) XCTAssertFalse(testDie.value == 0) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/one-sided_dice2.png"
        alt="one-sided_dice2" width="100" height="116" class="alignright size-full wp-image-142143">
    </p>
    <p>
        Run the tests; two of the assertions will fail. Change
        <code>
            rollDie()
        </code>
        in
        <em>
            Dice.swift
        </em>
        so that it sets
        <code>
            value
        </code>
        to 1 and try again. This time all the tests pass, but this dice roller
        won’t be of much use! :]
    </p>
    <p>
        Instead of testing a single value, what about making the test roll the
        die multiple times and count how many of each number it gets? There won’t
        be a perfectly even distribution of all numbers, but a large enough sample
        should be close enough for your tests.
    </p>
    <p>
        Time for another test in
        <em>
            DiceTests.swift
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140510">
                    <td class="code" id="p141405code10">
                        <pre class="swift" style="font-family:monospace;">
                            func testRollsAreSpreadRoughlyEvenly() { var testDie = Dice() var rolls:
                            [Int: Double] = [:] &nbsp; // 1 let rollCounter = 600.0 &nbsp; for _ in
                            0 ..&lt; Int(rollCounter) { testDie.rollDie() guard let newRoll = testDie.value
                            else { // 2 XCTFail() return } &nbsp; // 3 if let existingCount = rolls[newRoll]
                            { rolls[newRoll] = existingCount + 1 } else { rolls[newRoll] = 1 } } &nbsp;
                            // 4 XCTAssertEqual(rolls.keys.count, 6) &nbsp; // 5 for (key, roll) in
                            rolls { XCTAssertEqualWithAccuracy(roll, rollCounter / 6, accuracy: rollCounter
                            / 6 * 0.3, "Dice gave \(roll) x \(key)") } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s what’s going on in this test:
    </p>
    <ol>
        <li>
            <code>
                rollCounter
            </code>
            specifies how many times the dice will be rolled. 100 for each expected
            number seems like a reasonable sample size.
        </li>
        <li>
            If the die has no value at any time during the loop, the test will fail
            and exit immediately.
            <code>
                XCTFail()
            </code>
            is like an assertion that can never pass, which works very well with
            <code>
                guard
            </code>
            statements.
        </li>
        <li>
            After each roll, you add the result to a dictionary.
        </li>
        <li>
            This assertion confirms that there are 6 keys in the dictionary, one for
            each of the expected numbers.
        </li>
        <li>
            The test uses a new assertion:
            <code>
                XCTAssertEqualWithAccuracy()
            </code>
            which allows inexact comparisons. Since
            <code>
                XCTAssertEqualWithAccuracy()
            </code>
            is called numerous times, the optional message is used to show which part
            of the loop failed.
        </li>
    </ol>
    <p>
        Run the test; as you would expect, it fails as every roll is 1. To see
        the errors in more detail, go to the
        <em>
            Issue Navigator
        </em>
        where you can read what the test results were, and what was expected.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/IssueNavigator.png"
        alt="IssueNavigator" width="515" height="462" class="aligncenter size-full wp-image-142115"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/IssueNavigator.png 515w, https://koenig-media.raywenderlich.com/uploads/2016/08/IssueNavigator-357x320.png 357w"
        sizes="(max-width: 515px) 100vw, 515px">
    </p>
    <p>
        It is finally time to add the random number generator to
        <code>
            rollDie()
        </code>
        . In
        <em>
            Dice.swift
        </em>
        , change the function as shown below:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140511">
                    <td class="code" id="p141405code11">
                        <pre class="swift" style="font-family:monospace;">
                            mutating func rollDie() { value = Int(arc4random_uniform(UInt32(6))) +
                            1 }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140512">
                    <td class="code" id="p141405code12">
                        <pre class="swift" style="font-family:monospace;">
                            func testRollingTwentySidedDice() { var testDie = Dice() testDie.rollDie(numberOfSides:
                            20) &nbsp; XCTAssertNotNil(testDie.value) XCTAssertTrue(testDie.value!
                            &gt;= 1) XCTAssertTrue(testDie.value! &lt;= 20) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140513">
                    <td class="code" id="p141405code13">
                        <pre class="swift" style="font-family:monospace;">
                            mutating func rollDie(numberOfSides: Int) {
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140514">
                    <td class="code" id="p141405code14">
                        <pre class="swift" style="font-family:monospace;">
                            mutating func rollDie(numberOfSides: Int = 6) {
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140515">
                    <td class="code" id="p141405code15">
                        <pre class="swift" style="font-family:monospace;">
                            func testTwentySidedRollsAreSpreadRoughlyEvenly() { var testDie = Dice()
                            var rolls: [Int: Double] = [:] let rollCounter = 2000.0 &nbsp; for _ in
                            0 ..&lt; Int(rollCounter) { testDie.rollDie(numberOfSides: 20) guard let
                            newRoll = testDie.value else { XCTFail() return } &nbsp; if let existingCount
                            = rolls[newRoll] { rolls[newRoll] = existingCount + 1 } else { rolls[newRoll]
                            = 1 } } &nbsp; XCTAssertEqual(rolls.keys.count, 20) &nbsp; for (key, roll)
                            in rolls { XCTAssertEqualWithAccuracy(roll, rollCounter / 20, accuracy:
                            rollCounter / 20 * 0.3, "Dice gave \(roll) x \(key)") } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140516">
                    <td class="code" id="p141405code16">
                        <pre class="swift" style="font-family:monospace;">
                            extension DiceTests { &nbsp; fileprivate func performMultipleRollTests(numberOfSides:
                            Int = 6) { var testDie = Dice() var rolls: [Int: Double] = [:] let rollCounter
                            = Double(numberOfSides) * 100.0 let expectedResult = rollCounter / Double(numberOfSides)
                            let allowedAccuracy = rollCounter / Double(numberOfSides) * 0.3 &nbsp;
                            for _ in 0 ..&lt; Int(rollCounter) { testDie.rollDie(numberOfSides: numberOfSides)
                            guard let newRoll = testDie.value else { XCTFail() return } &nbsp; if let
                            existingCount = rolls[newRoll] { rolls[newRoll] = existingCount + 1 } else
                            { rolls[newRoll] = 1 } } &nbsp; XCTAssertEqual(rolls.keys.count, numberOfSides)
                            &nbsp; for (key, roll) in rolls { XCTAssertEqualWithAccuracy(roll, expectedResult,
                            accuracy: allowedAccuracy, "Dice gave \(roll) x \(key)") } } &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140517">
                    <td class="code" id="p141405code17">
                        <pre class="swift" style="font-family:monospace;">
                            func testRollsAreSpreadRoughlyEvenly() { performMultipleRollTests() }
                            &nbsp; func testTwentySidedRollsAreSpreadRoughlyEvenly() { performMultipleRollTests(numberOfSides:
                            20) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140518">
                    <td class="code" id="p141405code18">
                        <pre class="swift" style="font-family:monospace;">
                            fileprivate func performMultipleRollTests(numberOfSides: Int = 6, line:
                            UInt = #line) {
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        将
        <code>
            XCTAsserts
        </code>
        修改为如下的样子：
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140519">
                    <td class="code" id="p141405code19">
                        <pre class="swift" style="font-family:monospace;">
                            XCTAssertEqual(rolls.keys.count, numberOfSides, line: line) &nbsp; for
                            (key, roll) in rolls { XCTAssertEqualWithAccuracy(roll, expectedResult,
                            accuracy: allowedAccuracy, "Dice gave \(roll) x \(key)", line: line) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140520">
                    <td class="code" id="p141405code20">
                        <pre class="swift" style="font-family:monospace;">
                            struct Roll { &nbsp; var dice: [Dice] = [] var numberOfSides = 6 &nbsp;
                            mutating func changeNumberOfDice(newDiceCount: Int) { dice = [] for _ in
                            0 ..&lt; newDiceCount { dice.append(Dice()) } } &nbsp; var allDiceValues:
                            [Int] { return dice.flatMap { $0.value} } &nbsp; mutating func rollAll()
                            { for index in 0 ..&lt; dice.count { dice[index].rollDie(numberOfSides:
                            numberOfSides) } } &nbsp; mutating func changeValueForDie(at diceIndex:
                            Int, to newValue: Int) { if diceIndex &lt; dice.count { dice[diceIndex].value
                            = newValue } } &nbsp; func totalForDice() -&gt; Int { let total = dice
                            .flatMap { $0.value } .reduce(0) { $0 - $1 } return total } &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140521">
                    <td class="code" id="p141405code21">
                        <pre class="swift" style="font-family:monospace;">
                            @testable import High_Roller
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140522">
                    <td class="code" id="p141405code22">
                        <pre class="swift" style="font-family:monospace;">
                            func testCreatingRollOfDice() { var roll = Roll() for _ in 0 ..&lt; 5
                            { roll.dice.append(Dice()) } &nbsp; XCTAssertNotNil(roll) XCTAssertEqual(roll.dice.count,
                            5) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        运行测试。目前一切都好 - 第一个测试通过了。和TDD不同，一个失败的测试并非是基本的第一步，因为代码（理论上）早已可以正常地工作。
    </p>
    <p>
        接下来，使用下列的测试，来检查在滚动之前，点数的总数为0：
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140523">
                    <td class="code" id="p141405code23">
                        <pre class="swift" style="font-family:monospace;">
                            func testTotalForDiceBeforeRolling_ShouldBeZero() { var roll = Roll()
                            for _ in 0 ..&lt; 5 { roll.dice.append(Dice()) } &nbsp; let total = roll.totalForDice()
                            XCTAssertEqual(total, 0) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140524">
                    <td class="code" id="p141405code24">
                        <pre class="swift" style="font-family:monospace;">
                            var roll: Roll! &nbsp; override func setUp() { super.setUp() &nbsp; roll
                            = Roll() roll.changeNumberOfDice(newDiceCount: 5) } &nbsp; func testCreatingRollOfDice()
                            { XCTAssertNotNil(roll) XCTAssertEqual(roll.dice.count, 5) } &nbsp; func
                            testTotalForDiceBeforeRolling_ShouldBeZero() { let total = roll.totalForDice()
                            XCTAssertEqual(total, 0) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        按照惯例，再次运行测试，来检查一切是否正常工作。
    </p>
    <p> 
        在6面骰子的情况下，最小的总数应当是5，而最大的总数则应是30，因此添加下列的测试来验证总数是否处于这个范围之中：
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140525">
                    <td class="code" id="p141405code25">
                        <pre class="swift" style="font-family:monospace;">
                            func testTotalForDiceAfterRolling_ShouldBeBetween5And30() { roll.rollAll()
                            let total = roll.totalForDice() XCTAssertGreaterThanOrEqual(total, 5) XCTAssertLessThanOrEqual(total,
                            30) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14140526">
                    <td class="code" id="p141405code26">
                        <pre class="swift" style="font-family:monospace;">
                            func totalForDice() -&gt; Int { let total = dice .flatMap { $0.value }
                            // .reduce(0) { $0 - $1 } // bug line .reduce(0) { $0 + $1 } // fixed return
                            total }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
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