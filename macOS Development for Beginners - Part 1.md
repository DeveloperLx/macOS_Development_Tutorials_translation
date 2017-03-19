# macOS新手开发：第一部分

#### [原文地址](https://www.raywenderlich.com/151741/macos-development-beginners-part-1) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-250x250.png"
            alt="macOSBeginner-feature" width="250" height="250" class="alignright size-thumbnail wp-image-154235"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-128x128.png 128w"
            sizes="(max-width: 250px) 100vw, 250px">
        </a>
    </p>
    <p>
        Do you want to learn how to develop your own apps for macOS?
    </p>
    <p>
        Good news! Apple makes developing for macOS incredibly easy, and in this
        tutorial series you’ll learn how. You’ll learn how to create your first
        app for macOS — even if you’re a complete beginner.
    </p>
    <ul>
        <li>
            In this first part you’ll first learn about how to obtain the tools you
            need to develop for macOS. Then, while creating a simple “Hello, World!”
            app, you’ll take a tour of Xcode, discovering how to run an app, edit code,
            design the UI and debug your code.
        </li>
        <li>
            In Parts 2 &amp; 3 of this series, you’ll create a more complex Egg Timer
            app and learn about the components that make up a macOS app, from how an
            app starts, to constructing the UI, all the way to handling user interaction.
        </li>
    </ul>
    <p>
        So what are you waiting for? The world of desktop apps awaits!
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            Here’s some guidance of where to begin with this series:
        </p>
        <ul>
            <li>
                If you are new to Swift, this series assumes some Swift knowledge, so
                first check out our
                <a href="https://www.raywenderlich.com/category/swift">
                    Swift tutorials
                </a>
                to get a great introduction.
            </li>
            <li>
                If you already have iOS experience, this first part of the series will
                be a review. Take a quick look through the topics to make sure and then
                skip straight ahead to the next part of the series.
            </li>
            <li>
                Otherwise, keep reading. This series is for complete beginners – no experience
                of developing for iOS or macOS is required!
            </li>
        </ul>
    </div>
    <h2>
        Getting Started
    </h2>
    <p>
        To become a macOS developer, you will need two things:
    </p>
    <ol>
        <li>
            A Mac running macOS Sierra: The macOS operating system only runs on Apple
            computers, so you need a Mac both to develop and run macOS apps.
        </li>
        <li>
            Xcode: This is the IDE used to create macOS apps. You’ll learn how to
            install this later in this section.
        </li>
    </ol>
    <p>
        Once you’ve built your app, if you want to upload it to the App Store
        for distribution, you’ll also need to pay for an Apple developer account.
        But this is not a requirement until you are ready to send your app out
        to the world, and even then, only if you want to distribute through the
        Mac App Store. If you already have a developer account for distributing
        iOS apps, then you are all set – Apple has merged the developer accounts
        so that you only need a single account to distribute apps for any Apple
        devices.
    </p>
    <p>
        Unlike some other platforms, developing for macOS requires the installation
        of just one tool: Xcode. Xcode is an IDE (Integrated Development Environment)
        that includes everything you need to develop macOS, iOS, watchOS and tvOS
        apps.
    </p>
    <p>
        If you don’t have Xcode already, click on the Apple icon in the upper
        left of your menu and select
        <em>
            App Store…
        </em>
        to open the Mac App Store. You will need an App Store account to download
        Xcode even though Xcode is free.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/AppStore.png"
        alt="AppStore" width="300" height="298" class="alignleft size-full wp-image-152485"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/AppStore.png 300w, https://koenig-media.raywenderlich.com/uploads/2017/01/AppStore-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2017/01/AppStore-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2017/01/AppStore-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2017/01/AppStore-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2017/01/AppStore-128x128.png 128w"
        sizes="(max-width: 300px) 100vw, 300px">
    </p>
    <p>
        Search for Xcode and click the
        <em>
            Install
        </em>
        button to start the download. Once it has downloaded and installed (which
        may take a while – it is quite large) open it from your
        <em>
            Applications
        </em>
        folder. The first time you run Xcode, and after every major update, it
        will ask you for permission to install additional components. Enter your
        password and allow Xcode to install these components.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/GetXcode.png"
        alt="GetXcode" width="700" height="320" class="aligncenter size-full wp-image-152486"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/GetXcode.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/GetXcode-480x219.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/GetXcode-650x297.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        Hello World!
    </h2>
    <p>
        Following the long-standing tradition when learning a new programming
        language or platform, you are going to start by creating a Hello World!
        app for macOS.
    </p>
    <p>
        Open Xcode if it is not already running. You should see a Welcome to Xcode
        window – if you don’t see it, choose
        <em>
            Welcome to Xcode
        </em>
        from the
        <em>
            Window
        </em>
        menu.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Welcome.png"
        alt="Welcome" width="500" height="293" class="aligncenter size-full wp-image-152487"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Welcome.png 500w, https://koenig-media.raywenderlich.com/uploads/2017/01/Welcome-480x281.png 480w"
        sizes="(max-width: 500px) 100vw, 500px">
    </p>
    <p>
        Click
        <em>
            Create a new Xcode project
        </em>
        and when the next dialog appears, choose
        <em>
            macOS
        </em>
        from the tabs across the top. Select
        <em>
            Cocoa Application
        </em>
        from inside the
        <em>
            Application
        </em>
        section and click
        <em>
            Next
        </em>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Template.png"
        alt="Template" width="700" height="496" class="aligncenter size-full wp-image-152488"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Template.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/Template-452x320.png 452w, https://koenig-media.raywenderlich.com/uploads/2017/01/Template-650x461.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Give your new app a name –
        <em>
            HelloWorld
        </em>
        – make sure that the language is set to
        <em>
            Swift
        </em>
        and that
        <em>
            Use Storyboards
        </em>
        is checked. Uncheck all the other options.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Options.png"
        alt="Options" width="700" height="503" class="aligncenter size-full wp-image-152489"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Options.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/Options-445x320.png 445w, https://koenig-media.raywenderlich.com/uploads/2017/01/Options-650x467.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Click
        <em>
            Next
        </em>
        and
        <em>
            Create
        </em>
        to save your new app project.
    </p>
    <h2>
        Running Your App
    </h2>
    <p>
        Xcode has created the basic template for your app with all the required
        files. At this stage, it is fun to run the app and see how much you get
        for free.
    </p>
    <p>
        Click the
        <em>
            Play
        </em>
        button in the toolbar to run the app or use the
        <em>
            Command-R
        </em>
        shortcut. Xcode will now compile all of the code into machine code, bundle
        up the resources required by the app and then execute it.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Run.png"
        alt="Run" width="675" height="72" class="aligncenter size-full wp-image-152490"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Run.png 675w, https://koenig-media.raywenderlich.com/uploads/2017/01/Run-480x51.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/Run-650x69.png 650w"
        sizes="(max-width: 675px) 100vw, 675px">
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            The first time you ever build and run an app in Xcode, you might be asked
            whether you want to
            <em>
                Enable Developer Mode on this Mac
            </em>
            . You’re safe to select
            <em>
                Enable
            </em>
            , at which point you may have to enter your password. Developer mode allows
            Xcode to attach a debugger to running processes – which will be extremely
            useful when building your application!
        </p>
    </div>
    <p>
        You should now see a blank window but don’t be disappointed – have a look
        at what you can already do:
    </p>
    <ul>
        <li>
            The window is resizable, it can be minimized and made full screen.
        </li>
        <li>
            There is a complete set of menus, many of which already work without you
            doing anything.
        </li>
        <li>
            The Dock icon has the usual menus.
        </li>
    </ul>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/FirstRun.png"
        alt="FirstRun" width="500" height="328" class="aligncenter size-full wp-image-152491"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/FirstRun.png 500w, https://koenig-media.raywenderlich.com/uploads/2017/01/FirstRun-480x315.png 480w"
        sizes="(max-width: 500px) 100vw, 500px">
    </p>
    <p>
        But now it’s time for you to make the display a bit more interesting,
        so quit the app and go back to Xcode.
    </p>
    <h2>
        The Xcode Interface
    </h2>
    <p>
        Xcode packs a lot of features into a small package, so not everything
        is visible at one time. To be an efficient Xcode user, you need to know
        where everything is —&nbsp;and how to get to it.
    </p>
    <p>
        When you open a new project in Xcode, you have a window with a toolbar
        and three main panels.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Xcode1.png"
        alt="Xcode1" width="700" height="395" class="aligncenter size-full wp-image-152492"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Xcode1.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/Xcode1-480x271.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/Xcode1-650x367.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/Xcode1-266x151.png 266w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        The left panel is the
        <em>
            Navigator
        </em>
        panel and has 8 display options across the top. The one you will mostly
        use is the first one –
        <em>
            Project
        </em>
        – which lists all the files in your project and allows you to click on
        any one to edit it.
    </p>
    <p>
        The center panel is the
        <em>
            Editor
        </em>
        panel and will display whatever you have selected from the
        <em>
            Project Navigator
        </em>
        .
    </p>
    <p>
        The right panel is the
        <em>
            Utilities
        </em>
        panel and it will vary depending on what you are looking at in the
        <em>
            Editor
        </em>
        panel.
    </p>
    <h2>
        Adding the UI
    </h2>
    <p>
        You design the user interface using a Storyboard. Your app already has
        a storyboard, so go to the
        <em>
            Project Navigator
        </em>
        and click on
        <em>
            Main.storyboard
        </em>
        to show it in the Editor panel.
    </p>
    <p>
        Your display has just changed dramatically! In the Editor panel, you can
        now see the Document Outline and the visual editor for the UI.
    </p>
    <p>
        Have a look at the things you can see in the visual editor. There are
        three main areas, each of which also has a textual representation in the
        Document Outline:
    </p>
    <ul>
        <li>
            <em>
                Application Scene
            </em>
            : The menu bar and items.
        </li>
        <li>
            <em>
                Window Controller Scene
            </em>
            : Configures how the window will behave.
        </li>
        <li>
            <em>
                View Controller Scene
            </em>
            : Where your UI elements will go.
        </li>
    </ul>
    <p>
        In the
        <em>
            Utilities
        </em>
        panel, you see a top section with 8 tabs and a bottom section with 4 tabs.
    </p>
    <p>
        The bottom section switches between various things you can insert into
        your project. Right now you want to insert UI elements, so select the
        <em>
            Object library
        </em>
        which is the third from the left.
    </p>
    <p>
        In the filter at the bottom, type “text” to reduce the number of choices,
        and drag a
        <em>
            Text Field
        </em>
        into your
        <em>
            View Controller Scene
        </em>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Xcode2.png"
        alt="Xcode2" width="700" height="498" class="aligncenter size-full wp-image-152493"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Xcode2.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/Xcode2-450x320.png 450w, https://koenig-media.raywenderlich.com/uploads/2017/01/Xcode2-650x462.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Now filter for “button” and drag a
        <em>
            Push Button
        </em>
        into the
        <em>
            View Controller Scene
        </em>
        . Finally, add a
        <em>
            Label
        </em>
        .
    </p>
    <p>
        Now, build and run the app using the
        <em>
            Play
        </em>
        button or
        <em>
            Command-R
        </em>
        . You will see these 3 UI elements. Try typing in the text field – it
        already supports all the standard editing shortcuts: copy, paste, cut,
        select all, undo, redo and so on. But the button does nothing, and the
        label just shows “Label”, so it is time to make things more interactive.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Run2.png"
        alt="Run2" width="500" height="304" class="aligncenter size-full wp-image-152494"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Run2.png 500w, https://koenig-media.raywenderlich.com/uploads/2017/01/Run2-480x292.png 480w"
        sizes="(max-width: 500px) 100vw, 500px">
    </p>
    <h2>
        Configuring the UI
    </h2>
    <p>
        Go back to
        <em>
            Main.storyboard
        </em>
        and click on the button to select it. In the
        <em>
            Utilities
        </em>
        panel on the right, make sure the
        <em>
            Attributes Inspector
        </em>
        is showing – the 4th button across the top.
    </p>
    <p>
        Change the title of the button to “Say Hello”. The button may not be wide
        enough to show all the text, so go to the
        <em>
            Editor
        </em>
        menu and select
        <em>
            Size to Fit Content
        </em>
        which should fix that. (If Size to Fit Content is disabled, click somewhere
        to de-select the button, then re-select it and try again.)
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Button.png"
        alt="Button" width="700" height="251" class="aligncenter size-full wp-image-152495"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Button.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/Button-480x172.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/Button-650x233.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Now click in the text field to select it. For this app, the user is going
        to type their name in here, and when they click the button, the app will
        show “Hello name-goes-here!” in the label. To help the users, add some
        placeholder text to the text field using the
        <em>
            Attributes Inspector
        </em>
        .
    </p>
    <p>
        Stretch the text field out a bit to allow for long names and position
        the button to the right of it. When dragging objects around in the
        <em>
            View Controller Scene
        </em>
        , blue lines will appear to help you align and position the objects based
        on Apple’s Human Interface Guidelines.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/TextField.png"
        alt="TextField" width="700" height="398" class="aligncenter size-full wp-image-152496"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/TextField.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/TextField-480x273.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/TextField-650x370.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/TextField-266x151.png 266w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Position the label below the text field and button. Since the label is
        going to be important, make it use a larger font. Select the label and
        in the
        <em>
            Attributes Inspector
        </em>
        , change the font to
        <em>
            System Regular 30
        </em>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/FontSize.png"
        alt="FontSize" width="700" height="225" class="aligncenter size-full wp-image-152497"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/FontSize.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/FontSize-480x154.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/FontSize-650x209.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        How about making the text red to add even more excitement?
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Color.png"
        alt="Color" width="700" height="461" class="aligncenter size-full wp-image-152498"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Color.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/Color-480x316.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/Color-650x428.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        You can’t tell how long a name a user might enter, so resize the field
        to fit the height of that font and to almost fill the width of the window.
    </p>
    <p>
        Build &amp; run the app to check that your UI changes have taken effect.
        Once you are happy with the look of the text in the label, delete the label’s
        <em>
            Title
        </em>
        so that the label starts off empty.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/RunWithUI.png"
        alt="RunWithUI" width="700" height="426" class="aligncenter size-full wp-image-152499"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/RunWithUI.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/RunWithUI-480x292.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/RunWithUI-650x396.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        Connecting the UI to the code
    </h2>
    <p>
        Your app still doesn’t do what you want, but in order for that to work,
        you need to start adding code and that code has to be able to communicate
        with the UI. To make those linkages, you are going to use Xcode’s
        <em>
            Assistant Editor
        </em>
        . With the
        <em>
            Main.storyboard
        </em>
        visible, option-click on
        <em>
            ViewController.swift
        </em>
        in the
        <em>
            Project Navigator
        </em>
        . This will create a second editor panel containing the ViewController
        code.
    </p>
    <p>
        Depending on the size of your monitor, things may be looking a bit cramped
        now, so use the rightmost button in the Toolbar to hide the Utilities.
        If you need even more space, hide the Navigator.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Assistant.png"
        alt="Assistant" width="700" height="330" class="aligncenter size-full wp-image-152500"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Assistant.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/Assistant-480x226.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/Assistant-650x306.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Select the text field. Hold down the Control key and drag from the text
        field into the top of the
        <code>
            ViewController
        </code>
        class definition. Let go and enter
        <code>
            nameField
        </code>
        in the name box of the popup, then click
        <em>
            Connect
        </em>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/AddOutlet.png"
        alt="AddOutlet" width="700" height="258" class="aligncenter size-full wp-image-152501"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/AddOutlet.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/AddOutlet-480x177.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/AddOutlet-650x240.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Do the same with the label, naming it
        <code>
            helloLabel
        </code>
        .
    </p>
    <p>
        Looking at the code that Xcode has generated, you see that these are both
        marked with
        <code>
            @IBOutlet
        </code>
        . This is short for Interface Builder Outlet and is how you tell the storyboard
        editor that these object names are available for linking to a visual object.
    </p>
    <p>
        For the button, the code does not need to have a name for it, but it does
        need to know when a user clicks the button. This calls for an
        <code>
            @IBAction
        </code>
        instead of an
        <code>
            @IBOutlet
        </code>
        .
    </p>
    <p>
        Select the button and Control-Drag into
        <em>
            ViewController.swift
        </em>
        as before. This time, change the
        <em>
            Connection
        </em>
        popup to
        <em>
            Action
        </em>
        and set the name to
        <code>
            sayButtonClicked
        </code>
        . This creates the function that will be called when the button is clicked.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/AddAction.png"
        alt="AddAction" width="700" height="265" class="aligncenter size-full wp-image-152502"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/AddAction.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/AddAction-480x182.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/AddAction-650x246.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Everything is now in place to edit the code. Close the
        <em>
            Assistant Editor
        </em>
        using the X in the top right corner and switch to
        <em>
            ViewController.swift
        </em>
        . If you had hidden the
        <em>
            Navigator
        </em>
        , click the toggle button in the top right, or press
        <em>
            Command-1
        </em>
        to jump directly to the
        <em>
            Project Navigator
        </em>
        .
    </p>
    <p>
        Enter the following code into
        <code>
            sayButtonClicked
        </code>
        .
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1517411">
                    <td class="code" id="p151741code1">
                        <pre class="swift" style="font-family:monospace;">
                            var name = nameField.stringValue if name.isEmpty { name = "World" } let
                            greeting = "Hello \(name)!" helloLabel.stringValue = greeting
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The complete code in
        <em>
            ViewController.swift
        </em>
        now looks like this (after deleting the usual copyright notices at the
        top). The blobs beside the line numbers indicate a connection to the interface
        in the storyboard.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/ViewControllerSwift.png"
        alt="ViewControllerSwift" width="965" height="836" class="aligncenter size-full wp-image-152503"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/ViewControllerSwift.png 965w, https://koenig-media.raywenderlich.com/uploads/2017/01/ViewControllerSwift-369x320.png 369w, https://koenig-media.raywenderlich.com/uploads/2017/01/ViewControllerSwift-577x500.png 577w"
        sizes="(max-width: 965px) 100vw, 965px">
    </p>
    <p>
        Build and run the app.
    </p>
    <p>
        Click the
        <em>
            Say Hello
        </em>
        button without entering anything and you will see “Hello World!”. Now
        type in your name and click the button again to see your own personal greeting.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/HelloWorld.png"
        alt="HelloWorld" width="500" height="304" class="aligncenter size-full wp-image-152504"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/HelloWorld.png 500w, https://koenig-media.raywenderlich.com/uploads/2017/01/HelloWorld-480x292.png 480w"
        sizes="(max-width: 500px) 100vw, 500px">
    </p>
    <h2>
        Debugging
    </h2>
    <p>
        Sometimes, we programmers make mistakes – hard to believe I know, but
        trust me, it happens. And when it does, we need to be able to debug our
        code. Xcode allows us to stop the code at any point and step through line
        by line, checking the values of the variables at each point so that we
        can find the error.
    </p>
    <p>
        Go to
        <code>
            sayButtonClicked
        </code>
        in
        <em>
            ViewController.swift
        </em>
        and click on the line number beside the
        <code>
            var name =
        </code>
        line. A blue pointed rectangle will appear. This is an active breakpoint
        and when you click the button, the debugger will stop here. Click it again
        and it will turn pale blue. It is now an inactive breakpoint and will not
        stop the code and start the debugger. To remove the breakpoint completely,
        drag it out of the line numbers gutter.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Breakpoint.png"
        alt="Breakpoint" width="700" height="221" class="aligncenter size-full wp-image-152505"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Breakpoint.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/Breakpoint-480x152.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/Breakpoint-650x205.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Add the breakpoint again and run the app. Click the
        <em>
            Say Hello
        </em>
        button. Xcode will come to the front with the breakpoint line of code
        highlighted. In the bottom of the
        <em>
            Editor
        </em>
        panel, there will now be two new sections:
        <em>
            Variables
        </em>
        and
        <em>
            Console
        </em>
        . The
        <em>
            Variables
        </em>
        section shows the variables used in this function as well as
        <code>
            self
        </code>
        – the View Controller, and
        <code>
            sender
        </code>
        – the button.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Stopped.png"
        alt="Stopped" width="700" height="384" class="aligncenter size-full wp-image-152506"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Stopped.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/Stopped-480x263.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/Stopped-650x357.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Above the
        <em>
            Variables
        </em>
        display is a set of buttons for controlling the debugger. Mouse over each
        one and read the tooltop to see what it does. Click the
        <em>
            Step Over
        </em>
        button to move to the next line.
    </p>
    <p>
        In the
        <em>
            Variables
        </em>
        display, you can check that
        <code>
            name
        </code>
        is an empty string, so click
        <em>
            Step Over
        </em>
        twice more. The debugger will move into and through the
        <code>
            if
        </code>
        statement and set the
        <code>
            name
        </code>
        variable to “World”.
    </p>
    <p>
        Select the
        <code>
            name
        </code>
        variable in the
        <em>
            Variables
        </em>
        display and click the
        <em>
            Quick Look
        </em>
        button below to see the contents. Now click the
        <em>
            Print Description
        </em>
        button to see the information printed in the
        <em>
            Console
        </em>
        . If the “World” value had not been set correctly, you would have been
        able to see that here and work out how to fix your code.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/PrintVariable.png"
        alt="PrintVariable" width="700" height="384" class="aligncenter size-full wp-image-152507"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/PrintVariable.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrintVariable-480x263.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrintVariable-650x357.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        When you have checked the contents of the name variable, click the
        <em>
            Continue program execution
        </em>
        button to stop debugging and let the program move on. Use the button in
        the top right to hide the Debug area.
    </p>
    <h2>
        Images
    </h2>
    <p>
        In addition to code and user interfaces, your app will also need some
        artwork. Due to the different screen types (Retina and non-Retina), you
        often need to provide multiple versions of each asset. To simplify this
        process, Xcode uses
        <em>
            Asset Libraries
        </em>
        to store and organize the assets that accompany the app.
    </p>
    <p>
        In the
        <em>
            Project Navigator
        </em>
        , click on
        <em>
            Assets.xcassets
        </em>
        . The only item there so far is
        <em>
            AppIcon
        </em>
        which will contain the various images needed to display the app icon in
        all the required resolutions. Click on
        <em>
            AppIcon
        </em>
        – you can see that it wants 10 different images to cover all the possibilities,
        but if you supply any one of these, Xcode will use it as best it can. This
        is not good practice, as you should supply all the required icon sizes,
        but for this tutorial one icon will be sufficient.
    </p>
    <p>
        Download the
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/02/rw_logo.png.zip">
            sample icon
        </a>
        which is a 512 x 512 pixel image. Drag it into the
        <em>
            Mac 512pt 1x
        </em>
        box.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/AppIcon.png"
        alt="AppIcon" width="700" height="443" class="aligncenter size-full wp-image-152508"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/AppIcon.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/AppIcon-480x304.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/AppIcon-650x411.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Build and run the app to see the icon in the Dock menu. If you still see
        the default app icon, quit the HelloWorld app, go back to Xcode and choose
        <em>
            Clean
        </em>
        from the
        <em>
            Product
        </em>
        menu, then run the app again.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/DockIcon.png"
        alt="DockIcon" width="128" height="134" class="aligncenter size-full wp-image-152509">
    </p>
    <h2>
        Getting Help
    </h2>
    <p>
        As well as being an editor, Xcode also contains all the documentation
        you will need for writing macOS apps.
    </p>
    <p>
        Go to the
        <em>
            Help
        </em>
        menu and choose
        <em>
            Documentation and API Reference
        </em>
        . Search for
        <em>
            NSButton
        </em>
        . Make sure Swift is the selected language, then click the top search
        result so that you can read all the details about buttons and button properties.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Docs.png"
        alt="Docs" width="600" height="485" class="aligncenter size-full wp-image-152511"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Docs.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/01/Docs-396x320.png 396w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <p>
        There is also a way to get to relevant documentation directly from your
        code. Go back to
        <em>
            ViewController.swift
        </em>
        and find the first line in
        <code>
            sayButtonClicked
        </code>
        .
        <em>
            Option-click
        </em>
        on the word
        <code>
            stringValue
        </code>
        . A popup appears with a short description. At the bottom of the popup
        is a link to
        <em>
            Property Reference
        </em>
        . Click this link and the documentation will open to show more information.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/OptionClick.png"
        alt="OptionClick" width="600" height="412" class="aligncenter size-full wp-image-152512"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/OptionClick.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/01/OptionClick-466x320.png 466w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <p>
        <em>
            Option-clicking
        </em>
        is often a really good way to learn, and you can even add documentation
        to your own functions so that it shows up in the same way.
    </p>
    <p>
        The
        <em>
            Help
        </em>
        menu also includes
        <em>
            Xcode Help
        </em>
        for specific information about the Xcode environment.
    </p>
    <h2>
        Where to Go From Here?
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
        In the
        <a href="https://www.raywenderlich.com/151746/macos-development-beginners-part-2">
            next part
        </a>
        of this tutorial series, you will start to create a more complicated app.
        Hope to see you there!
    </p>
    <p>
        If you have any questions or comments on this tutorial series, please
        join the discussion below!
    </p>
</div>