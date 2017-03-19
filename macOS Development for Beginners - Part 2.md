# macOS新手开发：第二部分

#### [原文地址](https://www.raywenderlich.com/151746/macos-development-beginners-part-2) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-250x250.png"
            alt="macOSBeginner-feature" width="250" height="250" class="alignright size-thumbnail wp-image-154235"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2017/01/macOSBeginner-feature-128x128.png 128w"
            sizes="(max-width: 250px) 100vw, 250px">
        </a>
        Welcome back to Part 2 of our 3-part macOS Development tutorial for beginner
        series!
    </p>
    <p>
        In
        <a href="https://www.raywenderlich.com/151741/macos-development-beginners-part-1">
            Part 1
        </a>
        of this series, you learned how to install Xcode, how to create a new
        app, add UI, connect the UI to the code, run the app, debug the app and
        how to get help. If you are unsure of any of this, go back and run through
        Part 1 again.
    </p>
    <p>
        In this part, you are going to create the user interface for a more complex
        app. You will learn how to allow for resizable windows, as well as designing
        and navigating to a second window to display your app’s preferences.
    </p>
    <h2>
        Getting Started
    </h2>
    <p>
        Open Xcode and click
        <em>
            Create a new Xcode project
        </em>
        from the Welcome window or select
        <em>
            File/New/Project…
        </em>
        Just as you did in Part 1, select
        <em>
            macOS/Application/Cocoa Application
        </em>
        . Click
        <em>
            Next
        </em>
        , give your app a name of
        <em>
            EggTimer
        </em>
        , make sure the language is
        <em>
            Swift
        </em>
        and that
        <em>
            Use Storyboards
        </em>
        is checked. Click
        <em>
            Next
        </em>
        and choose where to save your project.
    </p>
    <p>
        Build and run your new app just to make sure that everything is working
        correctly.
    </p>
    <h2>
        EggTimer App
    </h2>
    <p>
        The app that you are about to build is
        <em>
            EggTimer
        </em>
        ; it counts down from the selected time showing the time remaining. There
        is a graphic that changes as your egg boils and a sound that plays when
        your egg is ready. A second window will show the app’s preferences.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/EggTimer-1.png"
        alt="EggTimer" width="300" height="427" class="aligncenter size-full wp-image-152594"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/EggTimer-1.png 300w, https://koenig-media.raywenderlich.com/uploads/2017/01/EggTimer-1-225x320.png 225w"
        sizes="(max-width: 300px) 100vw, 300px">
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        from the
        <em>
            Project Navigator
        </em>
        . As you saw in part 1 of this series, you already have three components:
    </p>
    <ul>
        <li>
            Application Scene
        </li>
        <li>
            Window Controller Scene
        </li>
        <li>
            View Controller Scene
        </li>
    </ul>
    <p>
        Application Scene contains the menu bar and menus that appear whenever
        the app is running. Window Controller is the part of the app that defines
        how the window will behave: how it will resize, how new windows will appear,
        whether the app will save the window size and location and so forth. A
        window controller can manage more than one window, but if they need different
        properties, you will need to add another window controller.
    </p>
    <p>
        View Controller displays the user interface inside the window —&nbsp;that
        is where you will layout the UI for the main display.
    </p>
    <p>
        Notice that the Window Controller has an arrow pointing into it. This
        indicates it will control the initial display when the app starts up. You
        can check this by selecting the
        <em>
            Window Controller
        </em>
        in the
        <em>
            Document Outline
        </em>
        and going to the
        <em>
            Attributes Inspector
        </em>
        . Uncheck
        <em>
            Is Initial Controller
        </em>
        and the arrow will disappear. Check it again as you do want this to be
        the initial controller.
    </p>
    <h2>
        Window Controller
    </h2>
    <p>
        Before you start on the user interface, make sure you have selected
        <em>
            Main.storyboard
        </em>
        in the
        <em>
            Project Navigator
        </em>
        . Click inside the
        <em>
            Window Controller
        </em>
        to select its window. The Window Controller in the Visual Editor shows
        the text “View Controller” because this is what it contains. For this app,
        you do not want to allow the window to shrink below 346 x 471 pixels. This
        will also be the starting size of the window.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/WindowControllerSize.png"
        alt="WindowControllerSize" width="700" height="674" class="aligncenter size-full wp-image-152596"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/WindowControllerSize.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/WindowControllerSize-332x320.png 332w, https://koenig-media.raywenderlich.com/uploads/2017/01/WindowControllerSize-519x500.png 519w, https://koenig-media.raywenderlich.com/uploads/2017/01/WindowControllerSize-32x32.png 32w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Go to the
        <em>
            Size Inspector
        </em>
        in
        <em>
            Utilities
        </em>
        and set the
        <em>
            Content Size Width
        </em>
        to 346 and the
        <em>
            Content Size Height
        </em>
        to 471. Check the
        <em>
            Minimum Content Size
        </em>
        checkbox and make sure the width and height values are the same as for
        the content size. The Window Controller in the Visual Editor will have
        resized. You may want to move it now so that it is not overlapping other
        objects.
    </p>
    <p>
        While not strictly necessary, it is easier to visualize if you adjust
        the View Controller to the same dimensions as its containing Window Controller.
        Click the
        <em>
            View Controller
        </em>
        making sure that its View is selected in the Document Outline. In the
        <em>
            Size Inspector
        </em>
        set the width and height to 346 and 471 respectively. Re-position as needed
        to see all the objects. Now the WindowController and the ViewController
        are shown at the same size in the Visual Editor.
    </p>
    <p>
        Select the window in the WindowController and change its title to
        <em>
            Egg Timer
        </em>
        in the
        <em>
            Attributes Inspector
        </em>
        . Set the
        <em>
            Autosave name
        </em>
        to
        <em>
            EggTimerMainWindow
        </em>
        so that the size and positioning of the window will be saved automatically
        between launches.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/VCNaming.png"
        alt="VCNaming" width="700" height="418" class="aligncenter size-full wp-image-152597"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/VCNaming.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/VCNaming-480x287.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/VCNaming-650x388.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        If you are an iOS programmer, you will have dealt with various screen
        sizes for different device types and rotations. In macOS programming, you
        have to deal with an infinite variety of window sizes and aspect ratios,
        which is why I made the initial dimensions for this window a bit weird.
        Luckily, Auto Layout handles all this for you.
    </p>
    <h2>
        Laying out the UI – part 1
    </h2>
    <p>
        The basic UI consists of 2 stack views. The first one contains the time
        remaining text and the egg image. The second one contains the 3 buttons
        along the bottom. Start with the buttons:
    </p>
    <ul>
        <li>
            Search for “Button” in the Object Library.
        </li>
        <li>
            Drag a Gradient button into the View Controller.
        </li>
        <li>
            Using the Attributes Inspector, delete its image and set its title to
            Start.
        </li>
        <li>
            Change the font to System 24.
        </li>
        <p>
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/ButtonProps.png"
            alt="ButtonProps" width="515" height="852" class="aligncenter size-full wp-image-152778"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/ButtonProps.png 515w, https://koenig-media.raywenderlich.com/uploads/2017/01/ButtonProps-193x320.png 193w, https://koenig-media.raywenderlich.com/uploads/2017/01/ButtonProps-302x500.png 302w"
            sizes="(max-width: 515px) 100vw, 515px">
        </p>
        <li>
            Expand the button to show all the text.
        </li>
        <li>
            With the Start button selected, press
            <em>
                Command-D
            </em>
            twice to create 2 more copies.
        </li>
        <li>
            Drag the new buttons out so you can see them all.
        </li>
        <li>
            Edit the titles of the new buttons to Stop and Reset.
        </li>
        <li>
            Select all 3 buttons and choose
            <em>
                Editor/Embed In/Stack View
            </em>
            .
        </li>
    </ul>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/StackView.png"
        alt="StackView" width="700" height="423" class="aligncenter size-full wp-image-152598"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/StackView.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/StackView-480x290.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/StackView-650x393.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        To make the buttons fill the stack view, select the new
        <em>
            Stack View
        </em>
        and make the following changes in the
        <em>
            Attributes Inspector
        </em>
        :
    </p>
    <ul>
        <li>
            Distribution: Fill Equally
        </li>
        <li>
            Spacing: 0
        </li>
    </ul>
    <p>
        Click the
        <em>
            Add New Constraints
        </em>
        button at the bottom of the
        <em>
            Visual Editor
        </em>
        and set the left, right, bottom and height constraints as shown. Select
        <em>
            Update Frames: Items of New Constraints
        </em>
        and then click
        <em>
            Apply 4 Constraints
        </em>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/StackViewConstraints.png"
        alt="StackViewConstraints" width="700" height="435" class="aligncenter size-full wp-image-152599"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/StackViewConstraints.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/StackViewConstraints-480x298.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/StackViewConstraints-650x404.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        The stack view is now positioned correctly, but the buttons are shorter
        than the stack view. In the
        <em>
            Document Outline
        </em>
        , Control-Drag from the
        <em>
            Start
        </em>
        button to the
        <em>
            Stack View
        </em>
        and select
        <em>
            Equal Heights
        </em>
        . Do the same for the other two buttons.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/EqualHeights.png"
        alt="EqualHeights" width="700" height="420" class="aligncenter size-full wp-image-152600"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/EqualHeights.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/EqualHeights-480x288.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/EqualHeights-650x390.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        The button stack view is now exactly as you wanted it.
    </p>
    <p>
        Build and run the app. Try resizing the window: the buttons stick to the
        bottom of the window and resize to fill the width evenly.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/ResizedWindow.png"
        alt="ResizedWindow" width="1687" height="983" class="aligncenter size-full wp-image-152601"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/ResizedWindow.png 1687w, https://koenig-media.raywenderlich.com/uploads/2017/01/ResizedWindow-480x280.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/ResizedWindow-650x379.png 650w"
        sizes="(max-width: 1687px) 100vw, 1687px">
    </p>
    <p>
        As a final touch, disable the Stop and Reset buttons by unchecking
        <em>
            Enabled
        </em>
        in the
        <em>
            Attributes Inspector
        </em>
        . It makes no sense to have them enabled before the timer has started.
    </p>
    <h2>
        Laying out the UI – Part 2
    </h2>
    <p>
        The second stack view contains the time remaining text and the image.
        Drag a Label into the View Controller, set its
        <em>
            Title
        </em>
        to 6:00 and its
        <em>
            Alignment
        </em>
        to center. The current system font (San Francisco) uses proportional spacing
        for digits which means that if you have a counter, the digits appear to
        leap around as they change — which is really annoying.
    </p>
    <p>
        Switch the font to
        <em>
            Helvetica Neue
        </em>
        to avoid this and set the font size to
        <em>
            100
        </em>
        . This will make the text too large to display, so expand the label field
        until you can see it.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/FontAdjust.png"
        alt="FontAdjust" width="500" height="530" class="aligncenter size-full wp-image-152602"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/FontAdjust.png 500w, https://koenig-media.raywenderlich.com/uploads/2017/01/FontAdjust-302x320.png 302w, https://koenig-media.raywenderlich.com/uploads/2017/01/FontAdjust-472x500.png 472w"
        sizes="(max-width: 500px) 100vw, 500px">
    </p>
    <p>
        To add the image, search the
        <em>
            Object Library
        </em>
        by typing “image” in the filter field. This will bring up several possibilities
        but the one you want is
        <em>
            Image View
        </em>
        . Drag this into the
        <em>
            View Controller
        </em>
        underneath the time remaining label.
    </p>
    <p>
        Download the
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/EggTimerAssets-1.zip">
            assets for this project
        </a>
        (images and a sound file). Unzip the file and open the
        <em>
            Egg Images
        </em>
        folder. In Xcode, click in
        <em>
            Assets.xcassets
        </em>
        in the
        <em>
            Project Navigator
        </em>
        .
    </p>
    <p>
        Drag the 6 image files into the Assets library. They will now be available
        to your app. Because the image file names included “@2x”, they have been
        automatically allocated to the 2x section for each image asset.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/ImageAssets-1.png"
        alt="ImageAssets" width="700" height="430" class="aligncenter size-full wp-image-152779"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/ImageAssets-1.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/ImageAssets-1-480x295.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/ImageAssets-1-650x399.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Go back to
        <em>
            Main.storyboard
        </em>
        , select the
        <em>
            Image View
        </em>
        you just added and click the
        <em>
            Image
        </em>
        popup in the
        <em>
            Attributes Inspector
        </em>
        . You can see the images you just added as well as the built-in images.
        Select
        <em>
            stopped
        </em>
        .
    </p>
    <p>
        Make the second stack view: select the time remaining label and the image
        view. Choose
        <em>
            Editor/Embed In/Stack View
        </em>
        . Now you need to configure this stack view to fill the free space. Click
        the
        <em>
            Add New Constraints
        </em>
        button at the bottom of the Visual Editor and set these constraints:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/SV2Constraints.png"
        alt="SV2Constraints" width="700" height="752" class="aligncenter size-full wp-image-152604"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/SV2Constraints.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/SV2Constraints-298x320.png 298w, https://koenig-media.raywenderlich.com/uploads/2017/01/SV2Constraints-465x500.png 465w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        The stack view has expanded as required, but the image view is still too
        small. Select the image view and set its left and right constraints to
        the
        <em>
            Standard Value
        </em>
        as shown.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/ImageConstraints.png"
        alt="ImageConstraints" width="700" height="655" class="aligncenter size-full wp-image-152605"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/ImageConstraints.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/ImageConstraints-342x320.png 342w, https://koenig-media.raywenderlich.com/uploads/2017/01/ImageConstraints-534x500.png 534w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        In the
        <em>
            Attributes Inspector
        </em>
        , set
        <em>
            Scaling
        </em>
        to
        <em>
            Proportionally Up or Down
        </em>
        .
    </p>
    <p>
        Build and run the app. Resize the window to check that all the UI elements
        are resizing and positioning as expected.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/RunWithConstraints.png"
        alt="RunWithConstraints" width="700" height="440" class="aligncenter size-full wp-image-152606"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/RunWithConstraints.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/RunWithConstraints-480x302.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/RunWithConstraints-650x409.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        Connecting the UI to the code
    </h2>
    <p>
        As you learned in part 1 of this series, you need to set up
        <code>
            @IBOutlets
        </code>
        and
        <code>
            @IBActions
        </code>
        to connect your UI to your code. For this window, you need
        <code>
            @IBOutlets
        </code>
        for the following elements:
    </p>
    <ul>
        <li>
            Time remaining label
        </li>
        <li>
            Egg image view
        </li>
        <li>
            The 3 buttons
        </li>
    </ul>
    <p>
        The 3 buttons also need
        <code>
            @IBActions
        </code>
        to trigger a function when a user clicks them. In the
        <em>
            Project Navigator
        </em>
        , select
        <em>
            Main.storyboard
        </em>
        . Option-click on
        <em>
            ViewController.swift
        </em>
        in the
        <em>
            Project Navigator
        </em>
        to open it in the
        <em>
            Assistant Editor
        </em>
        . If you are running out of space, use the buttons in the top right to
        hide the
        <em>
            Utilities
        </em>
        and
        <em>
            Navigator
        </em>
        panels.
    </p>
    <p>
        Select the
        <em>
            countdown timer label
        </em>
        and Control-drag into the
        <code>
            ViewController
        </code>
        class, just as you did in part 1. Set the name of the label to
        <code>
            timeLeftField
        </code>
        . Repeat for the
        <em>
            egg image view
        </em>
        , setting its name to
        <code>
            eggImageView
        </code>
        . Set up outlets for the buttons naming them
        <code>
            startButton
        </code>
        ,
        <code>
            stopButton
        </code>
        and
        <code>
            resetButton
        </code>
        .
    </p>
    <p>
        The buttons also need
        <code>
            @IBActions
        </code>
        . Control-drag from the
        <em>
            Start
        </em>
        button but this time change the
        <em>
            Connection
        </em>
        popup to
        <em>
            Action
        </em>
        and set the name to
        <code>
            startButtonClicked
        </code>
        . Repeat for the other buttons creating actions called
        <code>
            stopButtonClicked
        </code>
        and
        <code>
            resetButtonClicked
        </code>
        .
    </p>
    <p>
        If you do what I often do and forget to change the Connection popup to
        Action, you will end up with two
        <code>
            @IBOutlets
        </code>
        and no
        <code>
            @IBAction
        </code>
        . To remove the extra
        <code>
            @IBOutlet
        </code>
        , firstly delete the extra line of code in the
        <code>
            ViewController
        </code>
        . Then go to the
        <em>
            Connections Inspector
        </em>
        in
        <em>
            Utilities
        </em>
        .
    </p>
    <p>
        You will see the two entries under
        <em>
            Referencing Outlets
        </em>
        . Click the
        <em>
            X
        </em>
        beside the incorrect one to remove it. Then go back and make the
        <code>
            @IBAction
        </code>
        remembering to change the
        <em>
            Connection
        </em>
        popup this time.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/FixConnection.png"
        alt="FixConnection" width="700" height="266" class="aligncenter size-full wp-image-152630"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/FixConnection.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/FixConnection-480x182.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/FixConnection-650x247.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        The
        <code>
            ViewController
        </code>
        code should now look like this:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/OutletsActions.png"
        alt="OutletsActions" width="600" height="600" class="aligncenter size-full wp-image-152607"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/OutletsActions.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/01/OutletsActions-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2017/01/OutletsActions-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2017/01/OutletsActions-500x500.png 500w, https://koenig-media.raywenderlich.com/uploads/2017/01/OutletsActions-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2017/01/OutletsActions-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2017/01/OutletsActions-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2017/01/OutletsActions-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2017/01/OutletsActions-128x128.png 128w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <p>
        In Part 3 of this series, you will add the code to these functions to
        make them work. Close the
        <em>
            Assistant Editor
        </em>
        now and re-open the
        <em>
            Navigator
        </em>
        and
        <em>
            Utilities
        </em>
        panels if you had closed them.
    </p>
    <h2>
        Menus
    </h2>
    <p>
        In
        <em>
            Main.storyboard
        </em>
        , click on the
        <em>
            menu bar
        </em>
        or
        <em>
            Application Scene
        </em>
        to select it. The app template provides a default set of menus, but for
        this app, most of them are unnecessary. The easiest way to explore the
        menus is using the
        <em>
            Document Outline
        </em>
        . Use the disclosure triangles to display the
        <em>
            View
        </em>
        menu and its contents.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/ViewMenu.png"
        alt="ViewMenu" width="300" height="364" class="aligncenter size-full wp-image-152608"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/ViewMenu.png 300w, https://koenig-media.raywenderlich.com/uploads/2017/01/ViewMenu-264x320.png 264w"
        sizes="(max-width: 300px) 100vw, 300px">
    </p>
    <p>
        The structure of the menu bar is a series of nested menus and menu items.
        Switch to the
        <em>
            Identity Inspector
        </em>
        in the
        <em>
            Utilities
        </em>
        panel so that you can see what each entry in the list really is as you
        click on it.
        <em>
            Main Menu
        </em>
        is an instance of class
        <code>
            NSMenu
        </code>
        . It contains an array of
        <code>
            NSMenuItems
        </code>
        : View is one of these.
    </p>
    <p>
        The View menu item contains a sub-menu (
        <code>
            NSMenu
        </code>
        ) with its own
        <code>
            NSMenuItems
        </code>
        . Notice the
        <code>
            Separator
        </code>
        item which is just a specialized form of
        <code>
            NSMenuItem
        </code>
        .
    </p>
    <p>
        The first thing to do is to delete the menus that you do not need for
        this app. Select the
        <em>
            File
        </em>
        menu in the
        <em>
            Document Outline
        </em>
        and press
        <em>
            Delete
        </em>
        to remove it. If you select it in the
        <em>
            Visual Editor
        </em>
        and delete, you will only have deleted the menu inside the
        <em>
            File
        </em>
        menu item, so you will be left with a space in the menu bar. If this happens,
        select the space and press
        <em>
            Delete
        </em>
        again to remove it.
    </p>
    <p>
        Keep deleting menus until you only have EggTimer, Window and Help.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/MenusAfterDeletion.png"
        alt="MenusAfterDeletion" width="200" height="49" class="aligncenter size-full wp-image-152609">
    </p>
    <p>
        Now you are going to add a new menu which will mimic the operations of
        the 3 buttons. Search for “menu” in the
        <em>
            Object Library
        </em>
        . Remembering that each menu starts with a menu item, drag a
        <em>
            Menu Item
        </em>
        into the menu bar between
        <em>
            EggTimer
        </em>
        and
        <em>
            Window
        </em>
        . It will appear as a blue box, but that is because it doesn’t have a
        menu with a title yet.
    </p>
    <p>
        Now drag a
        <em>
            Menu
        </em>
        into the blue box. If you find it difficult to target the blue box, drag
        into the
        <em>
            Document Outline
        </em>
        instead, just under the new
        <em>
            Item
        </em>
        . The new menu still doesn’t have a title, but it now has three items.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/NewMenu.png"
        alt="NewMenu" width="500" height="251" class="aligncenter size-full wp-image-152610"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/NewMenu.png 500w, https://koenig-media.raywenderlich.com/uploads/2017/01/NewMenu-480x241.png 480w"
        sizes="(max-width: 500px) 100vw, 500px">
    </p>
    <p>
        With the menu selected (not the item), switch to the
        <em>
            Attributes Inspector
        </em>
        and change the title to
        <em>
            Timer
        </em>
        . This will allocate a name to your new menu. Select
        <em>
            Item 1
        </em>
        and change its title to
        <em>
            Start
        </em>
        either by double-clicking and editing it in place or by using the
        <em>
            Attributes Inspector
        </em>
        .
    </p>
    <p>
        Click in the
        <em>
            Key Equivalent
        </em>
        field in the
        <em>
            Attributes Inspector
        </em>
        and press
        <em>
            Command-S
        </em>
        to assign a keyboard shortcut. Normally Command-S means Save, but as you
        have deleted the File menu this isn’t a conflict, although it is not best
        practice to re-use common shortcuts for other purposes.
    </p>
    <p>
        Use the same methods to set the title for the second item to
        <em>
            Stop
        </em>
        with a shortcut of
        <em>
            Command-X
        </em>
        and the third item’s title to
        <em>
            Reset
        </em>
        with
        <em>
            Command-R
        </em>
        as its shortcut.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/TimerMenu.png"
        alt="TimerMenu" width="700" height="227" class="aligncenter size-full wp-image-152611"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/TimerMenu.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/TimerMenu-480x156.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/TimerMenu-650x211.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        You can see three buttons across the top of the menu bar in the Visual
        Editor. Switch to the
        <em>
            Identity Inspector
        </em>
        . Clicking on each of these in turn shows that they are links to the
        <em>
            Application
        </em>
        , the
        <em>
            First Responder
        </em>
        and the
        <em>
            AppDelegate
        </em>
        . First Responder is usually the view controller that is currently frontmost,
        and it can receive actions from the menu items.
    </p>
    <p>
        <em>
            Option-click
        </em>
        on
        <em>
            ViewController.swift
        </em>
        and add the following code below the
        <code>
            @IBActions
        </code>
        you have for the buttons:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1517461">
                    <td class="code" id="p151746code1">
                        <pre class="swift" style="font-family:monospace;">
                            // MARK: - IBActions - menus &nbsp; @IBAction func startTimerMenuItemSelected(_
                            sender: Any) { startButtonClicked(sender) } &nbsp; @IBAction func stopTimerMenuItemSelected(_
                            sender: Any) { stopButtonClicked(sender) } &nbsp; @IBAction func resetTimerMenuItemSelected(_
                            sender: Any) { resetButtonClicked(sender) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        These functions will be called by the menus and they will call the button
        action functions. You could have the menu items calling the button action
        functions directly, but I chose to do it this way to make the sequence
        of events more obvious when debugging. Save the file and close the Assistant
        Editor.
    </p>
    <p>
        Control-drag from the
        <em>
            Start
        </em>
        menu item up to the orange block that indicates the
        <em>
            First Responder
        </em>
        . A popup will appear showing an enormous list of options. Type “sta”
        to scroll quickly to the correct section and select
        <em>
            startTimerMenuItemSelected
        </em>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/MenuAction.png"
        alt="MenuAction" width="600" height="500" class="aligncenter size-full wp-image-152612"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/MenuAction.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/01/MenuAction-384x320.png 384w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <p>
        Connect the
        <em>
            Stop
        </em>
        menu item to
        <code>
            stopTimerMenuItemSelected
        </code>
        and the
        <em>
            Reset
        </em>
        menu item to
        <code>
            resetTimerMenuItemSelected
        </code>
        in the same way. Now when the EggTimer window is at the front, selecting
        the menu items will call these functions.
    </p>
    <p>
        However the 3 buttons are not all going to be enabled at the same time,
        and the menu items need to reflect the status of the buttons. This cannot
        happen in the
        <code>
            ViewController
        </code>
        as it will not always be the First Responder, so the menu items will be
        controlled in the
        <code>
            AppDelegate
        </code>
        .
    </p>
    <p>
        With the
        <em>
            Main.storyboard
        </em>
        open and the menus visible, option-click on
        <em>
            AppDelegate.swift
        </em>
        in the
        <em>
            Project Navigator
        </em>
        . Control-drag from the
        <em>
            Start
        </em>
        menu into the
        <code>
            AppDelegate
        </code>
        and assign an outlet name of
        <code>
            startTimerMenuItem
        </code>
        .
    </p>
    <p>
        Do the same for the other items, assigning titles of
        <code>
            stopTimerMenuItem
        </code>
        and
        <code>
            resetTimerMenuItem
        </code>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/MenuOutlet.png"
        alt="MenuOutlet" width="700" height="255" class="aligncenter size-full wp-image-152613"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/MenuOutlet.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/MenuOutlet-480x175.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/MenuOutlet-650x237.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        In Part 3 you will add code to enable and disable these menu items as
        required, but for now, you need to turn off the automatic enabling and
        disabling. Usually, the app will check to see if the current First Responder
        has an action for the menu item and disables it does not. For this app,
        you want to control this yourself. Select the
        <em>
            Timer
        </em>
        menu and uncheck
        <em>
            Auto Enables Items
        </em>
        in the
        <em>
            Attributes Inspector
        </em>
        .
    </p>
    <h2>
        Preferences Window
    </h2>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Prefs-2.png"
        alt="Prefs" width="600" height="340" class="aligncenter size-full wp-image-152773"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Prefs-2.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/01/Prefs-2-480x272.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/Prefs-2-266x151.png 266w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <p>
        The main window for the EggTimer app is looking good now, but it needs
        a Preferences window so that the user can choose how well they want their
        egg cooked.
    </p>
    <p>
        The Preferences will appear in a separate window with its own window controller.
        This is because the Preferences window will have a different default size
        and will not be resizable. It is possible to have more than one view controller
        displayed by the same window controller, but they then would share the
        properties of that window controller.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        , closing the Assistant Editor if it is still open, and search for “window”
        in the
        <em>
            Objects Library
        </em>
        . Drag a new
        <em>
            Window Controller
        </em>
        into the
        <em>
            Visual Editor
        </em>
        . It will create a
        <em>
            View Controller
        </em>
        as well to display its content. Arrange them in the window so they are
        easy to see and so that the new window controller is close to the menu
        bar.
    </p>
    <p>
        Open the
        <em>
            EggTimer
        </em>
        menu and Control-drag from
        <em>
            Preferences…
        </em>
        to the new window controller. Choose
        <em>
            Show
        </em>
        from the popup that appears. This creates a segue so that whenever a user
        selects
        <em>
            Preferences…
        </em>
        from the
        <em>
            EggTimer
        </em>
        menu, this window controller will display the new view controller.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsConnect.png"
        alt="PrefsConnect" width="700" height="378" class="aligncenter size-full wp-image-152615"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsConnect.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsConnect-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsConnect-650x351.png 650w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        The Preferences window controller will display a new view controller,
        so now you need to make the class for that view controller. In the
        <em>
            Project Navigator
        </em>
        , select the existing
        <em>
            ViewController.swift
        </em>
        file; this makes sure your new file will be in a logical place in the
        Project Navigator. Choose
        <em>
            File/New/File…
        </em>
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/NewFile.png"
        alt="NewFile" width="500" height="354" class="aligncenter size-full wp-image-152616"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/NewFile.png 500w, https://koenig-media.raywenderlich.com/uploads/2017/01/NewFile-452x320.png 452w"
        sizes="(max-width: 500px) 100vw, 500px">
    </p>
    <p>
        Choose
        <em>
            macOS/Cocoa Class
        </em>
        and click
        <em>
            Next
        </em>
        . Set the class name to
        <code>
            PrefsViewController
        </code>
        and make it a subclass of
        <code>
            NSViewController
        </code>
        . Check that the language is set to
        <em>
            Swift
        </em>
        and uncheck
        <em>
            Also create XIB file for user interface
        </em>
        . Click
        <em>
            Next
        </em>
        and
        <em>
            Create
        </em>
        to save the file.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/NewVC.png"
        alt="NewVC" width="500" height="355" class="aligncenter size-full wp-image-152617"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/NewVC.png 500w, https://koenig-media.raywenderlich.com/uploads/2017/01/NewVC-451x320.png 451w"
        sizes="(max-width: 500px) 100vw, 500px">
    </p>
    <p>
        Back in
        <em>
            Main.storyboard
        </em>
        , select the new view controller. Make sure you select the view controller
        itself, not its view; this is easier using the
        <em>
            Document Outline
        </em>
        . In the
        <em>
            Identity Inspector
        </em>
        , set its class to
        <code>
            PrefsViewController
        </code>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsVC.png"
        alt="PrefsVC" width="300" height="211" class="aligncenter size-full wp-image-152618">
    </p>
    <p>
        Select the window in the preferences window controller and use the
        <em>
            Attributes Inspector
        </em>
        to set its title to
        <em>
            Preferences
        </em>
        . Do not set an autosave name, as this window is going to be centered
        in the screen every time it appears. Uncheck the
        <em>
            Minimize
        </em>
        and
        <em>
            Resize
        </em>
        controls so that the window size is fixed.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsWindow.png"
        alt="PrefsWindow" width="300" height="306" class="aligncenter size-full wp-image-152619"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsWindow.png 300w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsWindow-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsWindow-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsWindow-64x64.png 64w"
        sizes="(max-width: 300px) 100vw, 300px">
    </p>
    <p>
        Go to the
        <em>
            Size Inspector
        </em>
        and enter a width of 416 and a height of 214 for the
        <em>
            Content Size
        </em>
        .
        <br>
        Under
        <em>
            Initial Position
        </em>
        , select
        <em>
            Center Horizontally
        </em>
        and
        <em>
            Center Vertically
        </em>
        from the 2 popups.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsSizeLoc.png"
        alt="PrefsSizeLoc" width="300" height="622" class="aligncenter size-full wp-image-152620"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsSizeLoc.png 300w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsSizeLoc-154x320.png 154w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsSizeLoc-241x500.png 241w"
        sizes="(max-width: 300px) 100vw, 300px">
    </p>
    <p>
        Select the
        <em>
            View
        </em>
        in the
        <em>
            PrefsViewController
        </em>
        and change its width to 416 and height to 214 using the
        <em>
            Size Inspector
        </em>
        .
    </p>
    <p>
        The
        <code>
            PrefsViewController
        </code>
        is going to display a popup for selecting from a preset time and a slider
        for selecting a custom time. It will have labels for each of these and
        two buttons: Cancel and OK. There will also be a dynamic label that shows
        the currently selected time.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsLayout-2.png"
        alt="PrefsLayout" width="600" height="340" class="aligncenter size-full wp-image-152774"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsLayout-2.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsLayout-2-480x272.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsLayout-2-266x151.png 266w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <p>
        Drag the following controls into the view controller arranging them as
        shown:
    </p>
    <ul>
        <li>
            <em>
                Label
            </em>
            – set title to “Preset Egg Timings:”
        </li>
        <li>
            <em>
                Pop Up Button
            </em>
        </li>
        <li>
            <em>
                Label
            </em>
            – set title to “Custom Egg Timing:”
        </li>
        <li>
            <em>
                Label
            </em>
            – set title to “6 minutes”
        </li>
        <li>
            <em>
                Horizontal Slider
            </em>
        </li>
        <li>
            <em>
                Push Button
            </em>
            – set title to “Cancel”
        </li>
        <li>
            <em>
                Push Button
            </em>
            – set title to “OK”
        </li>
    </ul>
    <p>
        Because this window does not resize, there is no need to apply any auto-layout
        constraints – the objects will always appear as you have arranged them.
        Drag the objects around to position them, using the blue guidelines to
        help you. Extend the width of the “6 minutes” label to near the right side
        of the window as it may contain more text. Double-click the
        <em>
            Pop Up Button
        </em>
        to see the first three items and set their titles to:
    </p>
    <ul>
        <li>
            For runny soft-boiled eggs (barely set whites): 3 minutes
        </li>
        <li>
            For slightly runny soft-boiled eggs: 4 minutes
        </li>
        <li>
            For custardy yet firm soft-boiled eggs: 6 minutes
        </li>
    </ul>
    <p>
        Drag in two more
        <em>
            Menu Items
        </em>
        from the
        <em>
            Objects Library
        </em>
        , then a
        <em>
            Separator Menu Item
        </em>
        and finally another
        <em>
            Menu Item
        </em>
        . If you are having any trouble positioning them, use the
        <em>
            Document Outline
        </em>
        .
    </p>
    <p>
        Set the titles for the remaining menu items to:
    </p>
    <ul>
        <li>
            For firm yet still creamy hard-boiled eggs: 10 minutes
        </li>
        <li>
            For very firm hard-boiled eggs: 15 minutes
        </li>
        <li>
            Custom
        </li>
    </ul>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/PresetPopup-1.png"
        alt="PresetPopup" width="600" height="348" class="aligncenter size-full wp-image-152784"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/PresetPopup-1.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/01/PresetPopup-1-480x278.png 480w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <p>
        I don’t pretend to have any great knowledge in regard to boiling eggs,
        so I got these times and descriptions from
        <a href="http://www.thekitchn.com/how-to-boil-eggs-perfectly-every-time-cooking-lessons-from-the-kitchn-202415"
        target="_blank">
            The Kitchn
        </a>
        .
    </p>
    <p>
        Select the popup itself, not any of the items, and set its
        <em>
            Selected Item
        </em>
        to the 6 minute option.
    </p>
    <p>
        Now here is where you are going to do a very neat trick that will allow
        the app to know exactly how many minutes have been selected. For each of
        the menu items in the popup, set its tag to the number of minutes: 3, 4,
        6, 10, 15 in the
        <em>
            Attributes Inspector
        </em>
        . Leave the tag for the Custom menu item at 0.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/Tags.png"
        alt="Tags" width="400" height="343" class="aligncenter size-full wp-image-152758"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/Tags.png 400w, https://koenig-media.raywenderlich.com/uploads/2017/01/Tags-373x320.png 373w"
        sizes="(max-width: 400px) 100vw, 400px">
    </p>
    <p>
        Now select the
        <em>
            Slider
        </em>
        and in the
        <em>
            Attributes Inspector
        </em>
        set
        <em>
            Tick marks
        </em>
        to 25,
        <em>
            Minimum Value
        </em>
        to 1,
        <em>
            Maximum Value
        </em>
        to 25,
        <em>
            Current Value
        </em>
        to 6 and check
        <em>
            Only stop on tick marks
        </em>
        . Once the tick marks are visible, you may want to move the slider down
        a few pixels. Disable the slider by unchecking
        <em>
            Enabled
        </em>
        – it will only be enabled if
        <em>
            Custom
        </em>
        is selected in the popup.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/SliderSettings-1.png"
        alt="SliderSettings" width="300" height="360" class="aligncenter size-full wp-image-152636"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/SliderSettings-1.png 300w, https://koenig-media.raywenderlich.com/uploads/2017/01/SliderSettings-1-267x320.png 267w"
        sizes="(max-width: 300px) 100vw, 300px">
    </p>
    <h2>
        Connecting up the Preferences Objects
    </h2>
    <p>
        Option-click on
        <em>
            PrefsViewController.swift
        </em>
        in the
        <em>
            Project Navigator
        </em>
        and hide the side panels if you need the room. You need
        <code>
            @IBOutlets
        </code>
        for the popup, the slider and the label showing “6 minutes”. Control-drag
        from each of these into the
        <code>
            PrefsViewController
        </code>
        giving them the following outlet names:
    </p>
    <ul>
        <li>
            Popup:
            <code>
                presetsPopup
            </code>
        </li>
        <li>
            Slider:
            <code>
                customSlider
            </code>
        </li>
        <li>
            Label:
            <code>
                customTextField
            </code>
        </li>
    </ul>
    <p>
        Next, Control-drag to create the
        <code>
            @IBActions
        </code>
        , remembering to set the
        <em>
            Connection
        </em>
        popup to
        <em>
            Action
        </em>
        each time:
    </p>
    <ul>
        <li>
            Popup:
            <code>
                popupValueChanged
            </code>
        </li>
        <li>
            Slider:
            <code>
                sliderValueChanged
            </code>
        </li>
        <li>
            Cancel button:
            <code>
                cancelButtonClicked
            </code>
        </li>
        <li>
            OK button:
            <code>
                okButtonClicked
            </code>
        </li>
    </ul>
    <p>
        Your code should now look like this:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsOutletsActions-1.png"
        alt="PrefsOutletsActions" width="600" height="431" class="aligncenter size-full wp-image-152775"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsOutletsActions-1.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/01/PrefsOutletsActions-1-445x320.png 445w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <p>
        The layout of the Preferences window is now complete. Build and run the
        app and select
        <em>
            Preferences
        </em>
        from the
        <em>
            EggTimer
        </em>
        menu. Click the red close blob in the title bar button to close the window
        when you are done giving it a look.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/RunPrefs-2.png"
        alt="RunPrefs" width="700" height="611" class="aligncenter size-full wp-image-152776"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/RunPrefs-2.png 700w, https://koenig-media.raywenderlich.com/uploads/2017/01/RunPrefs-2-367x320.png 367w, https://koenig-media.raywenderlich.com/uploads/2017/01/RunPrefs-2-573x500.png 573w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        App Icon
    </h2>
    <p>
        The only part left in the UI now is to add an icon for your app. You already
        downloaded a folder of assets for the app and installed some of the images
        into Assets.xcassets. Open the folder again and find the
        <em>
            egg-icon.png
        </em>
        file.
    </p>
    <p>
        Select
        <em>
            Assests.xcassets
        </em>
        from the
        <em>
            Project Navigator
        </em>
        , click on
        <em>
            AppIcon
        </em>
        and drag
        <em>
            egg-icon.png
        </em>
        into the
        <em>
            Mac 256pt 1x
        </em>
        box. As discussed in Part 1, for a production app you would supply all
        the sizes shown in AppIcon, but for this app, a single size is sufficient.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/EggTimerAppIcon.png"
        alt="EggTimerAppIcon" width="600" height="243" class="aligncenter size-full wp-image-152625"
        srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/EggTimerAppIcon.png 600w, https://koenig-media.raywenderlich.com/uploads/2017/01/EggTimerAppIcon-480x194.png 480w"
        sizes="(max-width: 600px) 100vw, 600px">
    </p>
    <p>
        Build and run your app to confirm that the new icon appears in the Dock.
        If you still see the default icon, chose
        <em>
            Clean
        </em>
        from Xcode’s
        <em>
            Product
        </em>
        menu and try again.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/EggTimerDockIcon.png"
        alt="EggTimerDockIcon" width="226" height="247" class="aligncenter size-full wp-image-152626">
    </p>
    <h2>
        Where To Go From Here?
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
        You now have the UI fully implemented for your app, but the app doesn’t
        do anything yet. If you got lost anywhere, you can
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/EggTimer-Part2-3.zip">
            download the Xcode project
        </a>
        which has all the UI implemented ready for the next part.
    </p>
    <p>
        In
        <a href="https://www.raywenderlich.com/151748/macos-development-beginners-part-3">
            Part 3
        </a>
        of this tutorial series, you will add the code that makes the app work.
    </p>
</div>