# macOS新手开发：第三部分

#### [原文地址](https://www.raywenderlich.com/151748/macos-development-beginners-part-3) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-250x250.png"
            alt="macOSBeginner-feature" width="250" height="250" class="alignright size-thumbnail wp-image-154235"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-128x128.png 128w"
            sizes="(max-width: 250px) 100vw, 250px">
        </a>
        Welcome back to the final and third part in our 3-part macOS Development
        tutorial for beginner series!
    </p>
    <p>
        In
        <a href="https://www.raywenderlich.com/151741/macos-development-beginners-part-1"
        sl-processed="1">
            Part 1
        </a>
        , you learned how to install Xcode and how to create a simple app. In
        <a href="https://www.raywenderlich.com/151746/macos-development-beginners-part-2"
        sl-processed="1">
            Part 2
        </a>
        , you created the user interface for a more complex app, but it doesn’t
        work yet as you have not coded anything. In this part, you are going to
        add the Swift code that will make your app come to life!
    </p>
    <h2>
        Getting Started
    </h2>
    <p>
        If you haven’t completed Part 2 or want to start with a clean slate, you
        can
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/EggTimer-Part2-3.zip"
        sl-processed="1">
            download the project files
        </a>
        with the app UI laid out as it was at the end of Part 2. Open this project
        or your own project from Part 2 and run it to confirm that the UI is all
        in place. Open the Preferences window to check it as well.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/RunPrefs-2.png"
        alt="RunPrefs" width="700" height="611" class="aligncenter size-full wp-image-152776"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/RunPrefs-2.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/RunPrefs-2-367x320.png 367w, https://koenig-media.raywenderlich.com/uploads/2017/01/RunPrefs-2-573x500.png 573w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        Sandboxing
    </h2>
    <p>
        Before you dive into the code, take a minute to consider sandboxing. If
        you are an iOS developer, you will already be familiar with this concept
        – if not, read on.
    </p>
    <p>
        A sandboxed app has its own space to work in with separate file storage
        areas, no access to the files created by other apps and limited access
        and permissions. For iOS apps, this is the only way to operate. For macOS
        apps, this is optional; however, if you want to distribute your apps through
        the Mac App Store, they must be sandboxed. As a general rule, you should
        sandbox your apps, as this gives your apps less potential to cause problems.
    </p>
    <p>
        To turn on sandboxing for the Egg Timer app, select the project in the
        <em>
            Project Navigator
        </em>
        — this is the top entry with the blue icon. Select
        <em>
            EggTimer
        </em>
        in the
        <em>
            Targets
        </em>
        list (there will only be one target listed), then click
        <em>
            Capabilities
        </em>
        in the tabs across the top. Click the switch to turn on
        <em>
            App Sandbox
        </em>
        . The display will expand to show the various permissions you can now
        request for your app. This app doesn’t need any of these, so leave them
        all unchecked.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Sandbox.png"
        alt="Sandbox" width="700" height="427" class="aligncenter size-full wp-image-152795"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Sandbox.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/Sandbox-480x293.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/Sandbox-650x397.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        Organizing Your Files
    </h2>
    <p>
        Look at the
        <em>
            Project Navigator
        </em>
        . All the files are listed with no particular organization. This app will
        not have very many files, but grouping similar files together is good practice
        and allows for more efficient navigation, especially with larger projects.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/ProjectNavigatorStart.png"
        alt="ProjectNavigatorStart" width="300" height="316" class="aligncenter size-full wp-image-152796">
    </p>
    <p>
        Select the two view controller files by clicking on one and Shift-clicking
        on the next. Right-click and choose
        <em>
            New Group from Selection
        </em>
        from the popup menu. Name the new group
        <em>
            View Controllers
        </em>
        .
    </p>
    <p>
        The project is about to get some model files, so select the top
        <em>
            EggTimer
        </em>
        group, right-click and choose
        <em>
            New Group
        </em>
        . Call this one
        <em>
            Model
        </em>
        .
    </p>
    <p>
        Finally, select
        <em>
            Info.plist
        </em>
        and
        <em>
            EggTimer.entitlements
        </em>
        and put them into a group called
        <em>
            Supporting Files
        </em>
        .
    </p>
    <p>
        Drag the groups and files around until your Project Navigator looks like
        this:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/ProjectNavigatorEnd.png"
        alt="ProjectNavigatorEnd" width="483" height="541" class="aligncenter size-full wp-image-152798"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/ProjectNavigatorEnd.png 483w, https://koenig-media.raywenderlich.com/uploads/2017/01/ProjectNavigatorEnd-286x320.png 286w, https://koenig-media.raywenderlich.com/uploads/2017/01/ProjectNavigatorEnd-446x500.png 446w"
        sizes="(max-width: 483px) 100vw, 483px">
    </p>
    <h2>
        MVC
    </h2>
    <p>
        This app is using the MVC pattern: Model View Controller.
    </p>
    <p>
        The main model object type for the app is going to be a class called
        <code>
            EggTimer
        </code>
        . This class will have properties for the start time of the timer, the
        requested duration and the elapsed time. It will also have a
        <code>
            Timer
        </code>
        object that fires every second to update itself. Methods will start, stop,
        resume or reset the
        <code>
            EggTimer
        </code>
        object.
    </p>
    <p>
        The
        <code>
            EggTimer
        </code>
        model class holds data and performs actions, but has no knowledge of how
        this is displayed. The Controller (in this case
        <code>
            ViewController
        </code>
        ), knows about the
        <code>
            EggTimer
        </code>
        class (the Model) and has a
        <code>
            View
        </code>
        that it can use to display the data.
    </p>
    <p>
        To communicate back to the
        <code>
            ViewController
        </code>
        ,
        <code>
            EggTimer
        </code>
        uses a delegate protocol. When something changes, the
        <code>
            EggTimer
        </code>
        sends a message to its
        <code>
            delegate
        </code>
        . The
        <code>
            ViewController
        </code>
        assigns itself as the
        <code>
            EggTimer's delegate
        </code>
        , so it is the one that receives the message and then it can display the
        new data in its own View.
    </p>
    <h2>
        Coding the EggTimer
    </h2>
    <p>
        Select the
        <em>
            Model
        </em>
        group in the
        <em>
            Project Navigator
        </em>
        and choose
        <em>
            File/New/File…
        </em>
        Select
        <em>
            macOS/Swift File
        </em>
        and click
        <em>
            Next
        </em>
        . Give the file a name of
        <em>
            EggTimer.swift
        </em>
        and click
        <em>
            Create
        </em>
        to save it.
    </p>
    <p>
        Add the following code:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1517481">
                    <td class="code" id="p151748code1">
                        <pre class="swift" style="font-family:monospace;">
                            class EggTimer { &nbsp; var timer: Timer? = nil var startTime: Date? var
                            duration: TimeInterval = 360 // default = 6 minutes var elapsedTime: TimeInterval
                            = 0 &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This sets up the
        <code>
            EggTimer
        </code>
        class and its properties.
        <code>
            TimeInterval
        </code>
        really means
        <code>
            Double
        </code>
        , but is used when you want to show that you mean seconds.
    </p>
    <p>
        The next thing is to add two computed properties inside the class, just
        after the previous properties:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1517482">
                    <td class="code" id="p151748code2">
                        <pre class="swift" style="font-family:monospace;">
                            var isStopped: Bool { return timer == nil &amp;&amp; elapsedTime == 0
                            } var isPaused: Bool { return timer == nil &amp;&amp; elapsedTime &gt;
                            0 }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        These are convenient shortcuts that can be used to determine the state
        of the
        <code>
            EggTimer
        </code>
        .
    </p>
    <p>
        Insert the definition for the delegate protocol into the
        <em>
            EggTimer.swift
        </em>
        file but outside the
        <code>
            EggTimer
        </code>
        class – I like to put protocol definitions at the top of the file, after
        the import.
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1517483">
                    <td class="code" id="p151748code3">
                        <pre class="swift" style="font-family:monospace;">
                            protocol EggTimerProtocol { func timeRemainingOnTimer(_ timer: EggTimer,
                            timeRemaining: TimeInterval) func timerHasFinished(_ timer: EggTimer) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        A protocol sets out a contract and any object that is defined as conforming
        to the
        <code>
            EggTimerProtocol
        </code>
        must supply these 2 functions.
    </p>
    <p>
        Now that you have defined a protocol, the
        <code>
            EggTimer
        </code>
        can get an optional
        <code>
            delegate
        </code>
        property which is set to any object that conforms to this protocol.
        <code>
            EggTimer
        </code>
        does not know or care what type of object the delegate is, because it
        is certain that the delegate has those two functions.
    </p>
    <p>
        Add this line to the existing properties in the
        <code>
            EggTimer
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1517484">
                    <td class="code" id="p151748code4">
                        <pre class="swift" style="font-family:monospace;">
                            var delegate: EggTimerProtocol?
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Starting the
        <code>
            EggTimer
        </code>
        ‘s timer object will fire off a function call every second. Insert this
        code which defines the function that will be called by the timer. The
        <code>
            dynamic
        </code>
        keyword is essential for the
        <code>
            Timer
        </code>
        to be able to find it.
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1517485">
                    <td class="code" id="p151748code5">
                        <pre class="swift" style="font-family:monospace;">
                            dynamic func timerAction() { // 1 guard let startTime = startTime else
                            { return } &nbsp; // 2 elapsedTime = -startTime.timeIntervalSinceNow &nbsp;
                            // 3 let secondsRemaining = (duration - elapsedTime).rounded() &nbsp; //
                            4 if secondsRemaining &lt;= 0 { resetTimer() delegate?.timerHasFinished(self)
                            } else { delegate?.timeRemainingOnTimer(self, timeRemaining: secondsRemaining)
                            } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        So what’s happening here?
    </p>
    <ol>
        <li>
            <code>
                startTime
            </code>
            is an
            <code>
                Optional Date
            </code>
            – if it is
            <code>
                nil
            </code>
            , the timer cannot be running so nothing happens.
        </li>
        <li>
            Re-calculate the
            <code>
                elapsedTime
            </code>
            property.
            <code>
                startTime
            </code>
            is earlier than now, so
            <em>
                timeIntervalSinceNow
            </em>
            produces a negative value. The minus sign changes it so that
            <em>
                elapsedTime
            </em>
            is a positive number.
        </li>
        <li>
            Calculate the seconds remaining for the timer, rounded to give a whole
            number of seconds.
        </li>
        <li>
            If the timer has finished, reset it and tell the
            <code>
                delegate
            </code>
            it has finished. Otherwise, tell the
            <code>
                delegate
            </code>
            the number of seconds remaining. As
            <code>
                delegate
            </code>
            is an optional property, the ? is used to perform optional chaining. If
            the
            <code>
                delegate
            </code>
            is not set, these methods will not be called but nothing bad will happen.
        </li>
    </ol>
    <p>
        You will see an error until you add the final bit of code needed for the
        <code>
            EggTimer
        </code>
        class: the methods for starting, stopping, resuming and resetting the
        timer.
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1517486">
                    <td class="code" id="p151748code6">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 func startTimer() { startTime = Date() elapsedTime = 0 &nbsp; timer
                            = Timer.scheduledTimer(timeInterval: 1, target: self, selector: #selector(timerAction),
                            userInfo: nil, repeats: true) timerAction() } &nbsp; // 2 func resumeTimer()
                            { startTime = Date(timeIntervalSinceNow: -elapsedTime) &nbsp; timer = Timer.scheduledTimer(timeInterval:
                            1, target: self, selector: #selector(timerAction), userInfo: nil, repeats:
                            true) timerAction() } &nbsp; // 3 func stopTimer() { // really just pauses
                            the timer timer?.invalidate() timer = nil &nbsp; timerAction() } &nbsp;
                            // 4 func resetTimer() { // stop the timer &amp; reset back to start timer?.invalidate()
                            timer = nil &nbsp; startTime = nil duration = 360 elapsedTime = 0 &nbsp;
                            timerAction() }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        What are these functions doing?
    </p>
    <ol>
        <li>
            <code>
                startTimer
            </code>
            sets the start time to now using
            <code>
                Date()
            </code>
            and sets up the repeating
            <code>
                Timer
            </code>
            .
        </li>
        <li>
            <code>
                resumeTimer
            </code>
            is what gets called when the timer has been paused and is being re-started.
            The start time is re-calculated based on the elapsed time.
        </li>
        <li>
            <code>
                stopTimer
            </code>
            stops the repeating timer.
        </li>
        <li>
            <code>
                resetTimer
            </code>
            stops the repeating timer and sets the properties back to the defaults.
        </li>
    </ol>
    <p>
        All these functions also call
        <code>
            timerAction
        </code>
        so that the display can update immediately.
    </p>
    <h2>
        ViewController
    </h2>
    <p>
        Now that the
        <code>
            EggTimer
        </code>
        object is working, its time to go back to
        <em>
            ViewController.swift
        </em>
        and make the display change to reflect this.
    </p>
    <p>
        <code>
            ViewController
        </code>
        already has the
        <code>
            @IBOutlet
        </code>
        properties, but now give it a property for the
        <code>
            EggTimer
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1517487">
                    <td class="code" id="p151748code7">
                        <pre class="swift" style="font-family:monospace;">
                            var eggTimer = EggTimer()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Add this line to
        <code>
            viewDidLoad
        </code>
        , replacing the comment line:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1517488">
                    <td class="code" id="p151748code8">
                        <pre class="swift" style="font-family:monospace;">
                            eggTimer.delegate = self
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This is going to cause an error because
        <code>
            ViewController
        </code>
        does not conform to the
        <code>
            EggTimerProtocol
        </code>
        . When conforming to a protocol, it makes your code neater if you create
        a separate extension for the protocol functions. Add this code below the
        <code>
            ViewController
        </code>
        class definition:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1517489">
                    <td class="code" id="p151748code9">
                        <pre class="swift" style="font-family:monospace;">
                            extension ViewController: EggTimerProtocol { &nbsp; func timeRemainingOnTimer(_
                            timer: EggTimer, timeRemaining: TimeInterval) { updateDisplay(for: timeRemaining)
                            } &nbsp; func timerHasFinished(_ timer: EggTimer) { updateDisplay(for:
                            0) } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The error disappears because
        <code>
            ViewController
        </code>
        now has the two functions required by
        <code>
            EggTimerProtocol
        </code>
        . However both these functions are calling
        <code>
            updateDisplay
        </code>
        which doesn’t exist yet.
    </p>
    <p>
        Here is another extension for
        <code>
            ViewController
        </code>
        which contains the display functions:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174810">
                    <td class="code" id="p151748code10">
                        <pre class="swift" style="font-family:monospace;">
                            extension ViewController { &nbsp; // MARK: - Display &nbsp; func updateDisplay(for
                            timeRemaining: TimeInterval) { timeLeftField.stringValue = textToDisplay(for:
                            timeRemaining) eggImageView.image = imageToDisplay(for: timeRemaining)
                            } &nbsp; private func textToDisplay(for timeRemaining: TimeInterval) -&gt;
                            String { if timeRemaining == 0 { return "Done!" } &nbsp; let minutesRemaining
                            = floor(timeRemaining / 60) let secondsRemaining = timeRemaining - (minutesRemaining
                            * 60) &nbsp; let secondsDisplay = String(format: "%02d", Int(secondsRemaining))
                            let timeRemainingDisplay = "\(Int(minutesRemaining)):\(secondsDisplay)"
                            &nbsp; return timeRemainingDisplay } &nbsp; private func imageToDisplay(for
                            timeRemaining: TimeInterval) -&gt; NSImage? { let percentageComplete =
                            100 - (timeRemaining / 360 * 100) &nbsp; if eggTimer.isStopped { let stoppedImageName
                            = (timeRemaining == 0) ? "100" : "stopped" return NSImage(named: stoppedImageName)
                            } &nbsp; let imageName: String switch percentageComplete { case 0 ..&lt;
                            25: imageName = "0" case 25 ..&lt; 50: imageName = "25" case 50 ..&lt;
                            75: imageName = "50" case 75 ..&lt; 100: imageName = "75" default: imageName
                            = "100" } &nbsp; return NSImage(named: imageName) } &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        <code>
            updateDisplay
        </code>
        uses private functions to get the text and the image for the supplied
        remaining time, and display these in the text field and image view.
    </p>
    <p>
        <code>
            textToDisplay
        </code>
        converts the seconds remaining to M:SS format.
        <code>
            imageToDisplay
        </code>
        calculates how much the egg is done as a percentage of the total and picks
        the image to match.
    </p>
    <p>
        So the
        <code>
            ViewController
        </code>
        has an
        <code>
            EggTimer
        </code>
        object and it has the functions to receive data from
        <code>
            EggTimer
        </code>
        and display the result, but the buttons have no code yet. In Part 2, you
        set up the
        <code>
            @IBActions
        </code>
        for the buttons.
    </p>
    <p>
        Here is the code for these action functions, so you can replace them with
        this:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174811">
                    <td class="code" id="p151748code11">
                        <pre class="swift" style="font-family:monospace;">
                            @IBAction func startButtonClicked(_ sender: Any) { if eggTimer.isPaused
                            { eggTimer.resumeTimer() } else { eggTimer.duration = 360 eggTimer.startTimer()
                            } } &nbsp; @IBAction func stopButtonClicked(_ sender: Any) { eggTimer.stopTimer()
                            } &nbsp; @IBAction func resetButtonClicked(_ sender: Any) { eggTimer.resetTimer()
                            updateDisplay(for: 360) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        These 3 actions call the
        <code>
            EggTimer
        </code>
        methods you added earlier.
    </p>
    <p>
        Build and run the app now and then click the
        <em>
            Start
        </em>
        button.
    </p>
    <p>
        There are a couple of features missing still: the Stop &amp; Reset buttons
        are always disabled and you can only have a 6 minute egg. You can use the
        <em>
            Timer
        </em>
        menu to control the app; try stopping, starting and resetting using the
        menu and the keyboard shortcuts.
    </p>
    <p>
        If you are patient enough to wait for it, you will see the egg change
        color as it cooks and finally show “DONE!” when it is ready.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Cooking.png"
        alt="Cooking" width="400" height="570" class="aligncenter size-full wp-image-152799"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Cooking.png 400w, https://koenig-media.raywenderlich.com/uploads/2017/01/Cooking-225x320.png 225w, https://koenig-media.raywenderlich.com/uploads/2017/01/Cooking-351x500.png 351w"
        sizes="(max-width: 400px) 100vw, 400px">
    </p>
    <h2>
        Buttons and Menus
    </h2>
    <p>
        The buttons should become enabled or disabled depending on the timer state
        and the Timer menu items should match that.
    </p>
    <p>
        Add this function to the
        <code>
            ViewController
        </code>
        , inside the extension with the Display functions:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174812">
                    <td class="code" id="p151748code12">
                        <pre class="swift" style="font-family:monospace;">
                            func configureButtonsAndMenus() { let enableStart: Bool let enableStop:
                            Bool let enableReset: Bool &nbsp; if eggTimer.isStopped { enableStart =
                            true enableStop = false enableReset = false } else if eggTimer.isPaused
                            { enableStart = true enableStop = false enableReset = true } else { enableStart
                            = false enableStop = true enableReset = false } &nbsp; startButton.isEnabled
                            = enableStart stopButton.isEnabled = enableStop resetButton.isEnabled =
                            enableReset &nbsp; if let appDel = NSApplication.shared().delegate as?
                            AppDelegate { appDel.enableMenus(start: enableStart, stop: enableStop,
                            reset: enableReset) } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This function uses the
        <code>
            EggTimer
        </code>
        status (remember the computed variables you added to
        <code>
            EggTimer
        </code>
        ) to work out which buttons should be enabled.
    </p>
    <p>
        In Part 2, you set up the Timer menu items as properties of the
        <code>
            AppDelegate
        </code>
        , so the
        <code>
            AppDelegate
        </code>
        is where they can be configured.
    </p>
    <p>
        Switch to
        <em>
            AppDelegate.swift
        </em>
        and add this function:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174813">
                    <td class="code" id="p151748code13">
                        <pre class="swift" style="font-family:monospace;">
                            func enableMenus(start: Bool, stop: Bool, reset: Bool) { startTimerMenuItem.isEnabled
                            = start stopTimerMenuItem.isEnabled = stop resetTimerMenuItem.isEnabled
                            = reset }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        So that your menus are correctly configured when the app first launches,
        add this line to the
        <code>
            applicationDidFinishLaunching
        </code>
        method:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174814">
                    <td class="code" id="p151748code14">
                        <pre class="swift" style="font-family:monospace;">
                            enableMenus(start: true, stop: false, reset: false)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The buttons and menus needs to be changed whenever a button or menu item
        action changes the state of the
        <code>
            EggTimer
        </code>
        . Switch back to
        <em>
            ViewController.swift
        </em>
        and add this line to the end of each of the 3 button action functions:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174815">
                    <td class="code" id="p151748code15">
                        <pre class="swift" style="font-family:monospace;">
                            configureButtonsAndMenus()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run the app again and you can see that the buttons enable and
        disable as expected. Check the menu items; they should mirror the state
        of the buttons.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/ButtonsMenus.png"
        alt="ButtonsMenus" width="600" height="895" class="aligncenter size-full wp-image-152800"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/ButtonsMenus.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/01/ButtonsMenus-215x320.png 215w, https://koenig-media.raywenderlich.com/uploads/2017/01/ButtonsMenus-335x500.png 335w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <h2>
        Preferences
    </h2>
    <p>
        There is really only one big problem left for this app – what if you don’t
        like your eggs boiled for 6 minutes?
    </p>
    <p>
        In Part 2, you designed a Preferences window to allow selection of a different
        time. This window is controlled by the
        <code>
            PrefsViewController
        </code>
        , but it needs a model object to handle the data storage and retrieval.
    </p>
    <p>
        Preferences are going be stored using
        <code>
            UserDefaults
        </code>
        which is a key-value way of storing small pieces of data in the Preferences
        folder in your app’s Container.
    </p>
    <p>
        Right-click on the
        <em>
            Model
        </em>
        group in the
        <em>
            Project Navigator
        </em>
        and choose
        <em>
            New File…
        </em>
        Select
        <em>
            macOS/Swift File
        </em>
        and click
        <em>
            Next
        </em>
        . Name the file
        <em>
            Preferences.swift
        </em>
        and click
        <em>
            Create
        </em>
        . Add this code to the
        <em>
            Preferences.swift
        </em>
        file:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174816">
                    <td class="code" id="p151748code16">
                        <pre class="swift" style="font-family:monospace;">
                            struct Preferences { &nbsp; // 1 var selectedTime: TimeInterval { get
                            { // 2 let savedTime = UserDefaults.standard.double(forKey: "selectedTime")
                            if savedTime &gt; 0 { return savedTime } // 3 return 360 } set { // 4 UserDefaults.standard.set(newValue,
                            forKey: "selectedTime") } } &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        So what does this code do?
    </p>
    <ol>
        <li>
            A computed variable called
            <code>
                selectedTime
            </code>
            is defined as a
            <code>
                TimeInterval
            </code>
            .
        </li>
        <li>
            When the value of the variable is requested, the
            <code>
                UserDefaults
            </code>
            singleton is asked for the
            <code>
                Double
            </code>
            value assigned to the key “selectedTime”. If the value has not been defined,
            <code>
                UserDefaults
            </code>
            will return zero, but if the value is greater than 0, return that as the
            value of
            <code>
                selectedTime
            </code>
            .
        </li>
        <li>
            If
            <code>
                selectedTime
            </code>
            has not been defined, use the default value of 360 (6 minutes).
        </li>
        <li>
            Whenever the value of
            <code>
                selectedTime
            </code>
            is changed, write the new value to
            <code>
                UserDefaults
            </code>
            with the key “selectedTime”.
        </li>
    </ol>
    <p>
        So by using a computed variable with a getter and a setter, the
        <code>
            UserDefaults
        </code>
        data storage will be handled automatically.
    </p>
    <p>
        Now switch the
        <em>
            PrefsViewController.swift
        </em>
        , where the first task is to update the display to reflect any existing
        preferences or the defaults.
    </p>
    <p>
        First, add this property just below the outlets:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174817">
                    <td class="code" id="p151748code17">
                        <pre class="swift" style="font-family:monospace;">
                            var prefs = Preferences()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here you create an instance of
        <code>
            Preferences
        </code>
        so the
        <code>
            selectedTime
        </code>
        computed variable is accessible.
    </p>
    <p>
        Then, add these methods:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174818">
                    <td class="code" id="p151748code18">
                        <pre class="swift" style="font-family:monospace;">
                            func showExistingPrefs() { // 1 let selectedTimeInMinutes = Int(prefs.selectedTime)
                            / 60 &nbsp; // 2 presetsPopup.selectItem(withTitle: "Custom") customSlider.isEnabled
                            = true &nbsp; // 3 for item in presetsPopup.itemArray { if item.tag ==
                            selectedTimeInMinutes { presetsPopup.select(item) customSlider.isEnabled
                            = false break } } &nbsp; // 4 customSlider.integerValue = selectedTimeInMinutes
                            showSliderValueAsText() } &nbsp; // 5 func showSliderValueAsText() { let
                            newTimerDuration = customSlider.integerValue let minutesDescription = (newTimerDuration
                            == 1) ? "minute" : "minutes" customTextField.stringValue = "\(newTimerDuration)
                            \(minutesDescription)" }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This looks like a lot of code, so just go through it step by step:
    </p>
    <ol>
        <li>
            Ask the prefs object for its
            <code>
                selectedTime
            </code>
            and convert it from seconds to whole minutes.
        </li>
        <li>
            Set the defaults to “Custom” in case no matching preset value is found.
        </li>
        <li>
            Loop through the menu items in the
            <code>
                presetsPopup
            </code>
            checking their tags. Remember in Part 2 how you set the tags to the number
            of minutes for each option? If a match is found, enable that item and get
            out of the loop.
        </li>
        <li>
            Set the value for the slider and call
            <code>
                showSliderValueAsText
            </code>
            .
        </li>
        <li>
            <code>
                showSliderValueAsText
            </code>
            adds “minute” or “minutes” to the number and shows it in the text field.
        </li>
    </ol>
    <p>
        Now, add this to
        <code>
            viewDidLoad
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174819">
                    <td class="code" id="p151748code19">
                        <pre class="swift" style="font-family:monospace;">
                            showExistingPrefs()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        When the view loads, call the method that shows the preferences in the
        display. Remember, using the MVC pattern, the
        <code>
            Preferences
        </code>
        model object has no idea about how or when it might be displayed – that
        is for the
        <code>
            PrefsViewController
        </code>
        to manage.
    </p>
    <p>
        So now you have the ability to display the set time, but changing the
        time in the popup doesn’t do anything yet. You need a method that saves
        the new data and tells anyone who is interested that the data has changed.
    </p>
    <p>
        In the
        <code>
            EggTimer
        </code>
        object, you used the delegate pattern to pass data to whatever needed
        it. This time (just to be different), you are going to broadcast a
        <code>
            Notification
        </code>
        when the data changes. Any object that choses can listen for this notification
        and act on it when received.
    </p>
    <p>
        Insert this method into
        <code>
            PrefsViewController
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174820">
                    <td class="code" id="p151748code20">
                        <pre class="swift" style="font-family:monospace;">
                            func saveNewPrefs() { prefs.selectedTime = customSlider.doubleValue *
                            60 NotificationCenter.default.post(name: Notification.Name(rawValue: "PrefsChanged"),
                            object: nil) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This gets the data from the custom slider (you will see in a minute that
        any changes are reflected there). Setting the
        <code>
            selectedTime
        </code>
        property will automatically save the new data to
        <code>
            UserDefaults
        </code>
        . Then a notification with the name “PrefsChanged” is posted to the
        <code>
            NotificationCenter
        </code>
        .
    </p>
    <p>
        In a minute, you will see how the
        <code>
            ViewController
        </code>
        can be set to listen for this
        <code>
            Notification
        </code>
        and react to it.
    </p>
    <p>
        The final step in coding the
        <code>
            PrefsViewController
        </code>
        is to set the code for the
        <code>
            @IBActions
        </code>
        you added in Part 2:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174821">
                    <td class="code" id="p151748code21">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 @IBAction func popupValueChanged(_ sender: NSPopUpButton) { if sender.selectedItem?.title
                            == "Custom" { customSlider.isEnabled = true return } &nbsp; let newTimerDuration
                            = sender.selectedTag() customSlider.integerValue = newTimerDuration showSliderValueAsText()
                            customSlider.isEnabled = false } &nbsp; // 2 @IBAction func sliderValueChanged(_
                            sender: NSSlider) { showSliderValueAsText() } &nbsp; // 3 @IBAction func
                            cancelButtonClicked(_ sender: Any) { view.window?.close() } &nbsp; // 4
                            @IBAction func okButtonClicked(_ sender: Any) { saveNewPrefs() view.window?.close()
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <ol>
        <li>
            When a new item is chosen from the popup, check to see if it is the Custom
            menu item. If so, enable the slider and get out. If not, use the tag to
            get the number of minutes, use them to set the slider value and text and
            disable the slider.
        </li>
        <li>
            Whenever the slider changes, update the text.
        </li>
        <li>
            Clicking Cancel just closes the window but does not save the changes.
        </li>
        <li>
            Clicking OK calls
            <code>
                saveNewPrefs
            </code>
            first and then closes the window.
        </li>
    </ol>
    <p>
        Build and run the app now and go to
        <em>
            Preferences
        </em>
        . Try choosing different options in the popup – notice how the slider
        and text change to match. Choose Custom and pick your own time. Click
        <em>
            OK
        </em>
        , then come back to
        <em>
            Preferences
        </em>
        and confirm that your chosen time is still displayed.
    </p>
    <p>
        Now try quitting the app and restarting. Go back to
        <em>
            Preferences
        </em>
        and see that it has saved your setting.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsChanges-1.png"
        alt="PrefsChanges" width="600" height="343" class="aligncenter size-full wp-image-152930"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsChanges-1.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsChanges-1-480x274.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsChanges-1-266x151.png 266w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <h2>
        Implementing Selected Preferences
    </h2>
    <p>
        The Preferences window is looking good – saving and restoring your selected
        time as expected. But when you go back to the main window, you are still
        getting a 6 minute egg! :[
    </p>
    <p>
        So you need to edit
        <em>
            ViewController.swift
        </em>
        to use the stored value for the timing and to listen for the Notification
        of change so the timer can be changed or reset.
    </p>
    <p>
        Add this extension to
        <em>
            ViewController.swift
        </em>
        outside any existing class definition or extension – it groups all the
        preferences functionality into a separate package for neater code:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174822">
                    <td class="code" id="p151748code22">
                        <pre class="swift" style="font-family:monospace;">
                            extension ViewController { &nbsp; // MARK: - Preferences &nbsp; func setupPrefs()
                            { updateDisplay(for: prefs.selectedTime) &nbsp; let notificationName =
                            Notification.Name(rawValue: "PrefsChanged") NotificationCenter.default.addObserver(forName:
                            notificationName, object: nil, queue: nil) { (notification) in self.updateFromPrefs()
                            } } &nbsp; func updateFromPrefs() { self.eggTimer.duration = self.prefs.selectedTime
                            self.resetButtonClicked(self) } &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This will give errors, because
        <code>
            ViewController
        </code>
        has no object called
        <code>
            prefs
        </code>
        . In the main
        <code>
            ViewController
        </code>
        class definition, where you defined the
        <code>
            eggTimer
        </code>
        property, add this line:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174823">
                    <td class="code" id="p151748code23">
                        <pre class="swift" style="font-family:monospace;">
                            var prefs = Preferences()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now
        <code>
            PrefsViewController
        </code>
        has a prefs object and so does
        <code>
            ViewController
        </code>
        – is this a problem? No, for a couple of reasons.
    </p>
    <ol>
        <li>
            <code>
                Preferences
            </code>
            is a struct, so it is value-based not reference-based. Each View Controller
            gets its own copy.
        </li>
        <li>
            The
            <code>
                Preferences
            </code>
            struct interacts with
            <code>
                UserDefaults
            </code>
            through a singleton, so both copies are using the same
            <code>
                UserDefaults
            </code>
            and getting the same data.
        </li>
    </ol>
    <p>
        At the end of the ViewController
        <code>
            viewDidLoad
        </code>
        function, add this call which will set up the
        <code>
            Preferences
        </code>
        connection:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174824">
                    <td class="code" id="p151748code24">
                        <pre class="swift" style="font-family:monospace;">
                            setupPrefs()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        There is one final set of edits needed. Earlier, you were using hard-coded
        values for timings – 360 seconds or 6 minutes. Now that
        <code>
            ViewController
        </code>
        has access to
        <code>
            Preferences
        </code>
        , you want to change these hard-coded 360’s to
        <code>
            prefs.selectedTime
        </code>
        .
    </p>
    <p>
        Search for 360 in
        <em>
            ViewController.swift
        </em>
        and change each one to
        <code>
            prefs.selectedTime
        </code>
        – you should be able to find 3 of them.
    </p>
    <p>
        Build and run the app. If you have changed your preferred egg time earlier,
        the time remaining will display whatever you chose. Go to
        <em>
            Preferences
        </em>
        , chose a different time and click
        <em>
            OK
        </em>
        – your new time will immediately be shown as
        <code>
            ViewController
        </code>
        receives the
        <code>
            Notification
        </code>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsUpdating.png"
        alt="PrefsUpdating" width="700" height="516" class="aligncenter size-full wp-image-152802"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsUpdating.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsUpdating-434x320.png 434w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsUpdating-650x479.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Start the timer, then go to
        <em>
            Preferences
        </em>
        . The countdown continues in the back window. Change your egg timing and
        click
        <em>
            OK
        </em>
        . The timer applies your new time, but stops the timer and resets the
        counter. This is OK, I suppose, but it would be better if the app warned
        you this was going to happen. How about adding a dialog that asks if that
        is really what you want to do?
    </p>
    <p>
        In the ViewController extension that deals with Preferences, add this
        function:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174825">
                    <td class="code" id="p151748code25">
                        <pre class="swift" style="font-family:monospace;">
                            func checkForResetAfterPrefsChange() { if eggTimer.isStopped || eggTimer.isPaused
                            { // 1 updateFromPrefs() } else { // 2 let alert = NSAlert() alert.messageText
                            = "Reset timer with the new settings?" alert.informativeText = "This will
                            stop your current timer!" alert.alertStyle = .warning &nbsp; // 3 alert.addButton(withTitle:
                            "Reset") alert.addButton(withTitle: "Cancel") &nbsp; // 4 let response
                            = alert.runModal() if response == NSAlertFirstButtonReturn { self.updateFromPrefs()
                            } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        So what’s going on here?
    </p>
    <ol>
        <li>
            If the timer is stopped or paused, just do the reset without asking.
        </li>
        <li>
            Create an
            <code>
                NSAlert
            </code>
            which is the class that displays a dialog box. Configure its text and
            style.
        </li>
        <li>
            Add 2 buttons: Reset &amp; Cancel. They will appear from right to left
            in the order you add them and the first one will be the default.
        </li>
        <li>
            Show the alert as a modal dialog and wait for the answer. Check if the
            user clicked the first button (Reset) and reset the timer if so.
        </li>
    </ol>
    <p>
        In the
        <code>
            setupPrefs
        </code>
        method, change the line
        <code>
            self.updateFromPrefs()
        </code>
        to:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174826">
                    <td class="code" id="p151748code26">
                        <pre class="swift" style="font-family:monospace;">
                            self.checkForResetAfterPrefsChange()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run the app, start the timer, go to
        <em>
            Preferences
        </em>
        , change the time and click
        <em>
            OK
        </em>
        . You will see the dialog and get the choice of resetting or not.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Dialog.png"
        alt="Dialog" width="400" height="146" class="aligncenter size-full wp-image-152803">
    </p>
    <h2>
        Sound
    </h2>
    <p>
        The only part of the app that we haven’t covered so far is the sound.
        An egg timer isn’t an egg timer if is doesn’t go DINGGGGG!.
    </p>
    <p>
        In part 2, you downloaded a folder of assets for the app. Most of them
        were images and you have already used them, but there was also a sound
        file:
        <em>
            ding.mp3
        </em>
        . If you need to download it again, here is a link to the
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/ding.mp3.zip"
        sl-processed="1">
            sound file
        </a>
        on its own.
    </p>
    <p>
        Drag the
        <em>
            ding.mp3
        </em>
        file into the
        <em>
            Project Navigator
        </em>
        inside the
        <em>
            EggTimer
        </em>
        group – just under
        <em>
            Main.storyboard
        </em>
        seems a logical place for it. Make sure that
        <em>
            Copy items if needed
        </em>
        is checked and that the EggTimer target is checked. Then click
        <em>
            Finish
        </em>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/AddFile.png"
        alt="AddFile" width="600" height="353" class="aligncenter size-full wp-image-152804"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/AddFile.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/01/AddFile-480x282.png 480w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <p>
        To play a sound, you need to use the
        <code>
            AVFoundation
        </code>
        library. The
        <code>
            ViewController
        </code>
        will be playing the sound when the
        <code>
            EggTimer
        </code>
        tells its delegate that the timer has finished, so switch to
        <em>
            ViewController.swift
        </em>
        . At the top, you will see where the
        <code>
            Cocoa
        </code>
        library is imported.
    </p>
    <p>
        Just below that line, add this:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174827">
                    <td class="code" id="p151748code27">
                        <pre class="swift" style="font-family:monospace;">
                            import AVFoundation
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        <code>
            ViewController
        </code>
        will need a player to play the sound file, so add this to its properties:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174828">
                    <td class="code" id="p151748code28">
                        <pre class="swift" style="font-family:monospace;">
                            var soundPlayer: AVAudioPlayer?
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        It seems like a good idea to make a separate extension to
        <code>
            ViewController
        </code>
        to hold the sound-related functions, so add this to
        <em>
            ViewController.swift
        </em>
        , outside any existing definition or extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174829">
                    <td class="code" id="p151748code29">
                        <pre class="swift" style="font-family:monospace;">
                            extension ViewController { &nbsp; // MARK: - Sound &nbsp; func prepareSound()
                            { guard let audioFileUrl = Bundle.main.url(forResource: "ding", withExtension:
                            "mp3") else { return } &nbsp; do { soundPlayer = try AVAudioPlayer(contentsOf:
                            audioFileUrl) soundPlayer?.prepareToPlay() } catch { print("Sound player
                            not available: \(error)") } } &nbsp; func playSound() { soundPlayer?.play()
                            } &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        <code>
            prepareSound
        </code>
        is doing most of the work here – it first checks to see whether the ding.mp3
        file is available in the app bundle. If the file is there, it tries to
        initialize an
        <code>
            AVAudioPlayer
        </code>
        with the sound file URL and prepares it to play. This pre-buffers the
        sound file so it can play immediately when needed.
    </p>
    <p>
        <code>
            playSound
        </code>
        just sends a play message to the player if it exists, but if
        <code>
            prepareSound
        </code>
        has failed,
        <code>
            soundPlayer
        </code>
        will be nil so this will do nothing.
    </p>
    <p>
        The sound only needs to be prepared once the Start button is clicked,
        so insert this line at the end of
        <code>
            startButtonClicked
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174830">
                    <td class="code" id="p151748code30">
                        <pre class="swift" style="font-family:monospace;">
                            prepareSound()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        And in
        <em>
            timerHasFinished
        </em>
        in the
        <em>
            EggTimerProtocol
        </em>
        extension, add this:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p15174831">
                    <td class="code" id="p151748code31">
                        <pre class="swift" style="font-family:monospace;">
                            playSound()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run the app, choose a conveniently short time for your egg and
        start the timer. Did you hear the ding when the timer ended?
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Ding.png"
        alt="Ding" width="400" height="570" class="aligncenter size-full wp-image-152805"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Ding.png 400w, https://koenig-media.raywenderlich.com/uploads/2017/01/Ding-225x320.png 225w, https://koenig-media.raywenderlich.com/uploads/2017/01/Ding-351x500.png 351w"
        sizes="(max-width: 400px) 100vw, 400px">
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
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/EggTimer-Final2.zip"
        sl-processed="1">
            completed project
        </a>
        here.
    </p>
    <p>
        This macOS development tutorial introductory series has given you a basic
        level of knowledge to get started with macOS apps–but there’s so much more
        to learn!
    </p>
    <p>
        Apple has some great
        <a href="https://developer.apple.com/library/content/navigation/#section=Platforms&amp;topic=macOS"
        sl-processed="1">
            documentation
        </a>
        covering all aspects of macOS development.
    </p>
    <p>
        I also highly recommend checking out the other macOS tutorials at
        <a href="https://www.raywenderlich.com/category/macos" sl-processed="1">
            raywenderlich.com
        </a>
        .
    </p>
    <p>
        If you have any questions or comments, please join the forum discussion
        below!
    </p>
</div>