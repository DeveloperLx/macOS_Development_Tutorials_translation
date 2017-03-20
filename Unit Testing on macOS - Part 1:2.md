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
        This uses
        <code>
            arc4random_uniform()
        </code>
        to produce what should be a number between 1 and 6. It looks simple, but
        you still have to test! Press
        <em>
            Command-U
        </em>
        again; all the tests pass. You can now be sure that the
        <code>
            Dice
        </code>
        struct is producing numbers in roughly the expected ratios. If anyone
        says your app is cheating, you can show them the test results to prove
        it isn’t!
    </p>
    <p>
        Job well done! The
        <code>
            Dice
        </code>
        struct is complete, time for a cup of tea…
    </p>
    <p>
        Until your friend, who plays a lot of role-playing games, has just asked
        if your app could support different types of dice: 4-sided, 8-sided, 12-sided,
        20-sided, even 100-sided…
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/Dice.jpg"
        alt="Dice" width="400" height="469" class="aligncenter size-large wp-image-141427"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/Dice.jpg 400w, https://koenig-media.raywenderlich.com/uploads/2016/08/Dice-273x320.jpg 273w"
        sizes="(max-width: 400px) 100vw, 400px">
    </p>
    <h3>
        Modifying Existing Code
    </h3>
    <p>
        You don’t want to ruin your friend’s D&amp;D nights, so head back to
        <em>
            DiceTests.swift
        </em>
        and add another test:
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
        The compiler complains because
        <code>
            rollDie()
        </code>
        doesn’t take any parameters. Switch over to the
        <em>
            assistant editor
        </em>
        and in
        <em>
            Dice.swift
        </em>
        change the function declaration of
        <code>
            rollDie()
        </code>
        to expect a
        <code>
            numberOfSides
        </code>
        parameter:
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
        But that will make the old test fail because they don’t supply a parameter.
        You
        <i>
            could
        </i>
        edit them all, but most dice rolls are for 6-sided dice (no need to tell
        your role-playing friend that). How about giving the
        <code>
            numberOfSides
        </code>
        parameter a default value?
    </p>
    <p>
        Change the
        <code>
            rollDie(numberOfSides:)
        </code>
        definition to this:
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
        All the tests now pass, but you are in the same position as before: the
        tests don’t check that the 20-sided dice roll is really producing values
        from 1 to 20.
    </p>
    <p>
        Time to write another test similar to
        <code>
            testRollsAreSpreadRoughlyEvenly()
        </code>
        , but only for 20-sided dice.
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
        This test gives seven failures: the number of keys is only 6, and the
        distribution isn’t even. Have a look in the
        <em>
            Issue Navigator
        </em>
        for all the details.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/IssueNavigator2-213x500.png"
        alt="IssueNavigator2" width="213" height="500" class="aligncenter size-large wp-image-142116"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/IssueNavigator2-213x500.png 213w, https://koenig-media.raywenderlich.com/uploads/2016/08/IssueNavigator2.png 515w"
        sizes="(max-width: 213px) 100vw, 213px">
    </p>
    <p>
        You should expect this:
        <code>
            rollDie(numberOfSides:)
        </code>
        isn’t using the
        <code>
            numberOfSides
        </code>
        parameter yet.
    </p>
    <p>
        Replace the
        <code>
            6
        </code>
        in the
        <code>
            arc4random_uniform()
        </code>
        function call with
        <code>
            numberOfSides
        </code>
        and
        <em>
            Command-U
        </em>
        again.
    </p>
    <p>
        Success! All the tests pass — even the old ones that call the function
        you just changed.
    </p>
    <h3>
        Refactoring Tests
    </h3>
    <p>
        For the first time, you have some code worth re-factoring.
        <code>
            testRollsAreSpreadRoughlyEvenly()
        </code>
        and
        <code>
            testTwentySidedRollsAreSpreadRoughlyEvenly()
        </code>
        use very similar code, so you could separate that out into a private function.
    </p>
    <p>
        Add the following extension to the end of the
        <em>
            DiceTests.swift
        </em>
        file, outside the class:
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
        This function name doesn’t start with
        <code>
            test
        </code>
        , as it’s never run on its own as a test.
    </p>
    <p>
        Go back to the main
        <code>
            DiceTests
        </code>
        class and replace
        <code>
            testRollsAreSpreadRoughlyEvenly()
        </code>
        and
        <code>
            testTwentySidedRollsAreSpreadRoughlyEvenly()
        </code>
        with the following:
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
        Run all the tests again to confirm that this works.
    </p>
    <h3>
        Using #line
    </h3>
    <p>
        To demonstrate another useful testing technique, go back to
        <em>
            Dice.swift
        </em>
        and undo the 20-sided dice change you made to
        <code>
            rollDie(numberOfSides:)
        </code>
        : replace
        <code>
            numberOfSides
        </code>
        with
        <code>
            6
        </code>
        inside the
        <code>
            arc4random_uniform()
        </code>
        call. Now run the tests again.
    </p>
    <p>
        <code>
            testTwentySidedRollsAreSpreadRoughlyEvenly()
        </code>
        has failed, but the failure messages are in
        <code>
            performMultipleRollTests(numberOfSides:)
        </code>
        — not a terribly useful spot.
    </p>
    <p>
        Xcode can solve this for you. When defining a helper function, you can
        supply a parameter with a special default value —
        <code>
            #line
        </code>
        — that contains the line number of the calling function. This line number
        can be used in the
        <code>
            XCTAssert
        </code>
        function to send the error somewhere useful.
    </p>
    <p>
        In the
        <code>
            DiceTests
        </code>
        extension, change the function definition of
        <code>
            performMultipleRollTests(numberOfSides:)
        </code>
        to the following:
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
        And change the
        <code>
            XCTAsserts
        </code>
        like this:
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
        You don’t have to change the code that calls
        <code>
            performMultipleRollTests(numberOfSides:line:)
        </code>
        because the new parameter is filled in by default. Run the tests again,
        and you’ll see the error markers are on the line that calls
        <code>
            performMultipleRollTests(numberOfSides:line:)
        </code>
        — not inside the helper function.
    </p>
    <p>
        Change
        <code>
            rollDie(numberOfSides:)
        </code>
        back again by putting
        <code>
            numberOfSides
        </code>
        in the
        <code>
            arc4random_uniform()
        </code>
        call, and
        <em>
            Command-U
        </em>
        to confirm that everything works.
    </p>
    <p>
        Pat yourself on the back — you’ve learned how to use TDD to develop a
        fully-tested model class.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/victory.png"
        alt="victory" width="475" height="313" class="aligncenter size-full wp-image-142118">
    </p>
    <h2>
        Adding Unit Tests to Existing Code
    </h2>
    <p>
        TDD can be great when developing new code, but often you’ll have to retrofit
        tests into existing code that you didn’t write. The process is much the
        same, except that you’re writing tests to confirm that existing code works
        as expected.
    </p>
    <p>
        To learn how to do this, you’ll add tests for the
        <code>
            Roll
        </code>
        struct. In this app, the
        <code>
            Roll
        </code>
        contains an array of
        <code>
            Dice
        </code>
        and a
        <code>
            numberOfSides
        </code>
        property. It handles rolling all the dice as well as totaling the result.
    </p>
    <p>
        Back in the
        <em>
            File Navigator
        </em>
        , select
        <code>
            Roll.swift
        </code>
        . Delete all the placeholder code and replace it with the following code:
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
        (Did you spot the error? Ignore it for now; that’s what the tests are
        for. :])
    </p>
    <p>
        Select the
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
        to add a new
        <em>
            macOS\Unit Test Case Class
        </em>
        called
        <code>
            RollTests
        </code>
        . Delete all the code inside the test class.
    </p>
    <p>
        Add the following import to
        <em>
            RollTests.swift
        </em>
        :
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
        Open
        <em>
            Roll.swift
        </em>
        in the assistant editor, and you’ll be ready to write more tests.
    </p>
    <p>
        First, you want to test that a
        <code>
            Roll
        </code>
        can be created, and that it can have
        <code>
            Dice
        </code>
        added to its
        <code>
            dice
        </code>
        array. Arbitrarily, the test uses five dice.
    </p>
    <p>
        Add this test to
        <em>
            RollTests.swift
        </em>
        :
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
        Run the tests; so far, so good — the first test passes. Unlike TDD, a
        failing test is not an essential first step in a retrofit as the code should
        (theoretically) already work properly.
    </p>
    <p>
        Next, use the following test to check that the total is zero before the
        dice are rolled:
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
        Again this succeeds, but it looks like there is some refactoring to be
        done. The first section of each test sets up a
        <code>
            Roll
        </code>
        object and populates it with five dice. If this was moved to
        <code>
            setup()
        </code>
        it would happen before every test.
    </p>
    <p>
        Not only that, but
        <code>
            Roll
        </code>
        has a method of its own for changing the number of
        <code>
            Dice
        </code>
        in the array, so the tests might as well use and test that.
    </p>
    <p>
        Replace the contents of the
        <code>
            RollTests
        </code>
        class with this:
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
        As always, run the tests again to check that everything still works.
    </p>
    <p>
        With five 6-sided dice, the minimum total is 5 and the maximum is 30,
        so add the following test to check that the total falls between those limits:
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
        Run this test — it fails! It looks like the tests have discovered a bug
        in the code. The problem must be in either
        <code>
            rollAll()
        </code>
        or
        <code>
            totalForDice()
        </code>
        , since those are the only two functions called by this test. If
        <code>
            rollAll()
        </code>
        was failing, the total would be zero. However, returned total is a negative
        number, so have a look at
        <code>
            totalForDice()
        </code>
        instead.
    </p>
    <p>
        There’s the problem:
        <code>
            reduce
        </code>
        is subtracting instead of adding the values. Change the minus sign to
        a plus sign:
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
        Run your tests again — everything should run perfectly.
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
        You can download the
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/08/HighRoller-part1.zip"
        sl-processed="1">
            sample project here
        </a>
        with all the tests from this part of the tutorial in it.
    </p>
    <p>
        Carry on to the
        <a href="https://www.raywenderlich.com/142090/unit-testing-macos-part-22"
        sl-processed="1">
            second half of this Unit testing on macOS tutorial
        </a>
        for more goodness, including interface testing, network testing, performance
        testing and code coverage. Hope to see you there! :]
    </p>
    <p>
        If you have any questions or comments about this part of the tutorial,
        please join the discussion below!
    </p>
</div>