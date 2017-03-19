# macOS控件教程：1/2部分

#### [原文地址](https://www.raywenderlich.com/149295/macos-controls-tutorial-part-12) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div id="attachment_153233" style="width: 260px" class="wp-caption alignright">
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-250x250.png"
            alt="Get started with macOS controls!" width="250" height="250" class="size-thumbnail wp-image-153233"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-128x128.png 128w"
            sizes="(max-width: 250px) 100vw, 250px">
        </a>
        <p class="wp-caption-text">
            Get started with macOS controls!
        </p>
    </div>
    <p>
        <em>
            Update Note:
        </em>
        Updated for Xcode 8.2 / Swift 3 by Ernesto García.
        <a href="https://www.raywenderlich.com/82046/introduction-to-os-x-tutorial-core-controls-and-swift-part-1">
            Previous update
        </a>
        to Xcode 6.3 / Swift 1.2 by
        <a href="https://www.raywenderlich.com/u/skyrocketsw">
            Michael Briscoe
        </a>
        .
        <a href="https://www.raywenderlich.com/27388/core-controls-in-mac-os-x-part-12">
            Original post
        </a>
        by
        <a href="http://www.raywenderlich.com/u/ernesto">
            Ernesto García
        </a>
        .
    </p>
    <p>
        If you’re an iOS developer and you’re interested in learning about Mac
        development, you’re in luck – with your iOS skills, you’ll find it quite
        easy to learn!
    </p>
    <p>
        Many of the Cocoa classes and design patterns you know and love like strings,
        dictionaries and delegates have direct equivalents in Mac development.
        You’ll feel right at home!
    </p>
    <p>
        However, one big difference with macOS development are there are different
        controls. Gone are
        <code>
            UIButton
        </code>
        and
        <code>
            UITextField
        </code>
        – instead there are similar (but slightly different) variants.
    </p>
    <p>
        This tutorial will introduce you to some of the more common macOS controls
        of the user interface — the foundation upon which most Mac apps are built.
        You’ll learn about these controls, as well as the methods and properties
        you’ll need to understand in order to get up and running as a developer!
        :]
    </p>
    <p>
        In this tutorial, you’ll be creating a simple Mac application like the
        popular game
        <a href="http://en.wikipedia.org/wiki/Mad_Libs" title="Mad Libs" target="_blank">
            Mad Libs
        </a>
        . Mad Libs is a word game where you can insert different words in a block
        of text in order to create a story — which often has hilarious results!
    </p>
    <p>
        Once you’ve completed both parts of this tutorial, you’ll have a fundamental
        understanding of the following macOS controls:
    </p>
    <ul>
        <li>
            Labels and Text Fields
        </li>
        <li>
            Combo Boxes
        </li>
        <li>
            Popup Buttons
        </li>
        <li>
            Text Views
        </li>
        <li>
            Sliders
        </li>
        <li>
            Date Pickers
        </li>
        <li>
            Buttons
        </li>
        <li>
            Radio Buttons
        </li>
        <li>
            Check Buttons
        </li>
        <li>
            Image Views
        </li>
    </ul>
    <div class="note">
        <em>
            Note:
        </em>
        Following this tutorial requires some knowledge of macOS development.
        If this is the first time you’re developing for macOS, you may want to
        go through our
        <a href="https://www.raywenderlich.com/110170/mac-os-x-development-tutorial-for-beginners-part-1-intro-to-xcode"
        target="_blank">
            macOS Development Tutorial for Beginners
        </a>
        series to learn the basics.
    </div>
    <p>
        The best way to learn any new programming platform is to dive right in
        and get started — so without further ado, here’s your introduction to macOS
        Controls! :]
    </p>
    <h2>
        Getting Started with macOS Controls
    </h2>
    <p>
        Open
        <em>
            Xcode
        </em>
        , and choose
        <em>
            File/New/Project
        </em>
        . In the
        <em>
            Choose a template
        </em>
        dialog, select
        <em>
            macOS/Application/Cocoa
        </em>
        , which is the template you use to create an app with a GUI on macOS.
        Then click
        <em>
            Next
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/macos-template.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/macos-template-650x455.png"
            alt="macos-template" width="650" height="455" class="aligncenter size-large wp-image-149748"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/macos-template-650x455.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/12/macos-template-458x320.png 458w, https://koenig-media.raywenderlich.com/uploads/2016/12/macos-template.png 1424w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        In the next screen, type
        <em>
            MadLibs
        </em>
        as the product name, and enter a unique Organization name and identifier.
        Make sure that
        <em>
            Use Storyboards
        </em>
        is checked and
        <em>
            Swift
        </em>
        is the selected language.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/macos-projectname.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/macos-projectname-650x457.png"
            alt="macos-projectname" width="650" height="457" class="aligncenter size-large wp-image-149749"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/macos-projectname-650x457.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/12/macos-projectname-455x320.png 455w, https://koenig-media.raywenderlich.com/uploads/2016/12/macos-projectname.png 1434w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Click
        <em>
            Next
        </em>
        and choose the location where you’d like to save your new project. Click
        <em>
            Create
        </em>
        .
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        .
        <em>
            Xcode
        </em>
        has created for you the basic skeleton of a macOS app: a Window controller
        and a content View controller.
    </p>
    <p>
        Select the window in the
        <em>
            Window Controller Scene
        </em>
        and open the
        <em>
            Attributes Inspector
        </em>
        . Change the window
        <em>
            Title
        </em>
        to
        <em>
            MadLibs
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibsWindowTitle.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibsWindowTitle-650x400.png"
            alt="MadLibsWindowTitle" width="650" height="400" class="aligncenter size-large wp-image-153685"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibsWindowTitle-650x400.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibsWindowTitle-480x295.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibsWindowTitle.png 1084w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        A macOS app usually has a resizable window and its content has to adapt
        to the window size. The best tool for that is
        <em>
            Auto Layout
        </em>
        . To add Auto Layout to all the controls in this tutorial would create
        a major distraction; we want you to focus strictly on the macOS controls.
    </p>
    <p>
        Accordingly, only the default autoresizing is applied, which means that
        all controls will maintain a fixed position and size, regardless of any
        window resizing the user performs —&nbsp;including the possibility that
        some of the controls fully or partially will be out of the window’s visible
        rectangle.
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            If you want to learn more about Auto Layout and how to use it in your
            macOS apps, you can follow our
            <a href="https://www.raywenderlich.com/110269/mac-os-x-development-tutorial-beginners-part-3-first-os-x-app"
            target="_blank">
                macOS Development Tutorial for Beginners, Part 3
            </a>
            .
        </p>
    </div>
    <p>
        During the tutorial, you’ll need to add some macOS controls to this view,
        and the default height may not be enough to fit them all. If you need to
        resize it, drag down the bottom edge of the content view, or set the view’s
        <em>
            Height
        </em>
        property in the
        <em>
            Size Inspector
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-resize-1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-resize-1-480x290.png"
            alt="drag-resize" width="480" height="290" class="aligncenter size-medium wp-image-153172"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-resize-1-480x290.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/drag-resize-1-650x393.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/drag-resize-1.png 1471w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Build and run.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/empty-window.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/empty-window-353x320.png"
            alt="empty-window" width="353" height="320" class="aligncenter size-medium wp-image-153163"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/empty-window-353x320.png 353w, https://koenig-media.raywenderlich.com/uploads/2017/01/empty-window-552x500.png 552w, https://koenig-media.raywenderlich.com/uploads/2017/01/empty-window.png 672w"
            sizes="(max-width: 353px) 100vw, 353px">
        </a>
    </p>
    <p>
        You’ve built a working application — without any coding at all. The window
        is empty right now, but you’re going to fill it up with some macOS controls
        and make it look great! :]
    </p>
    <p>
        Now that the basic framework has been laid down, you can move on to the
        main focus of this tutorial — adding macOS controls to your app.
    </p>
    <p>
        Each of the remaining steps in this tutorial will focus on a single, different
        control. You’ll learn the basics of each control and how to use each one
        in the MadLibs app to try it out.
    </p>
    <h2>
        NSControl – The Building Block of MacOS Controls
    </h2>
    <p>
        <a href="http://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Classes/NSControl_Class/Reference/Reference.html"
        title="NSControl" target="_blank">
            NSControl
        </a>
        is the foundation upon which all other macOS controls are built.
        <code>
            NSControl
        </code>
        provides three features which are pretty fundamental for user interface
        elements: drawing on the screen, responding to user events, and sending
        action messages.
    </p>
    <p>
        As
        <code>
            NSControl
        </code>
        is an abstract superclass, it’s entirely possible that you’ll never need
        to use it directly within your own apps unless you want to create your
        own custom macOS controls. All of the common controls are descendants of
        <code>
            NSControl
        </code>
        , and therefore inherit the properties and methods defined in that.
    </p>
    <p>
        The most common methods used for a control are getting and setting its
        value, as well as enabling or disabling the control itself. Have a look
        at the details behind these methods below:
    </p>
    <h3>
        Set the Value of macOS Controls
    </h3>
    <p>
        If you need to display information you’ll usually change the control’s
        value. Depending on your needs, the value can be a string, a number or
        even an object. In most circumstances, you’ll use a value which matches
        the type of information being displayed, but
        <code>
            NSControl
        </code>
        allows you to go beyond this and set several different value types!
    </p>
    <p>
        The methods for getting and setting a control’s value are:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492951">
                    <td class="code" id="p149295code1">
                        <pre class="swift" style="font-family:monospace;">
                            // getting &amp; setting a string let myString = myControl.stringValue
                            myControl.stringValue = myString &nbsp; // getting &amp; setting an integer
                            let myInteger = myControl.integerValue myControl.integerValue = myInteger
                            &nbsp; // getting &amp; setting a float let myFloat = myControl.floatValue
                            myControl.floatValue = myFloat &nbsp; // getting &amp; setting a double
                            let myDouble = myControl.doubleValue myControl.doubleValue = myDouble &nbsp;
                            // getting &amp; setting an object let myObject: Any? = myControl.objectValue
                            myControl.objectValue = myObject
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        You can see how the different setters and getters fit with the type-safety
        of Swift.
    </p>
    <h3>
        Enable &amp; Disable macOS Controls
    </h3>
    <p>
        Enabling or disabling macOS controls based on the state of an app is a
        very common UI task. When a control is disabled, it will not respond to
        mouse and keyboard events, and will usually update its graphical representation
        to provide some visual cues that it is disabled, such as drawing itself
        in a lighter “greyed out” color.
    </p>
    <p>
        The methods for enabling and disabling a control are:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492952">
                    <td class="code" id="p149295code2">
                        <pre class="swift" style="font-family:monospace;">
                            // disable a control myControl.isEnabled = false &nbsp; // enable a control
                            myControl.isEnabled = true &nbsp; // get a control's enabled state let
                            isEnabled = myControl.isEnabled
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Okay, that seems pretty easy — and the great thing is that these methods
        are common to all macOS controls. They’ll all work the same way for any
        control you use in your UI.
    </p>
    <p>
        Now it’s time to take a look at the more common macOS Controls.
    </p>
    <h2>
        Field of Dreams – NSTextField
    </h2>
    <p>
        One of the most common controls in any UI is a field that can be used
        to display or edit text. The control responsible for this functionality
        in macOS is
        <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Classes/NSTextField_Class/Reference/Reference.html"
        title="NSTextField Class Reference">
            NSTextField
        </a>
        .
    </p>
    <p>
        <code>
            NSTextField
        </code>
        is used for both displaying and editing text. You’ll notice this differs
        from iOS, where
        <code>
            UILabel
        </code>
        is used to display fixed text, and
        <code>
            UITextField
        </code>
        for editable text. In macOS these controls are combined into one, and
        its behavior changes according to the value of its
        <code>
            isEditable
        </code>
        property.
    </p>
    <p>
        If you want a text field to be a label, you simply set its
        <code>
            isEditable
        </code>
        property to
        <code>
            false
        </code>
        . To make it behave like a text field — yup, you simply set
        <code>
            isEditable
        </code>
        to
        <code>
            true
        </code>
        ! You can change this property programmatically or from Interface Builder.
    </p>
    <p>
        To make your coding life just a little easier, Interface Builder actually
        provides several pre-configured macOS controls to display and edit text
        which are all based on
        <code>
            NSTextField
        </code>
        . These pre-configured macOS controls can be found in the
        <em>
            Object Library
        </em>
        :
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/textfields-catalog.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/textfields-catalog-253x500.png"
            alt="textfields-catalog" width="253" height="500" class="aligncenter size-large wp-image-150177"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/textfields-catalog-253x500.png 253w, https://koenig-media.raywenderlich.com/uploads/2016/12/textfields-catalog-162x320.png 162w, https://koenig-media.raywenderlich.com/uploads/2016/12/textfields-catalog.png 522w"
            sizes="(max-width: 253px) 100vw, 253px">
        </a>
    </p>
    <p>
        So now that you’ve learned the basics about
        <code>
            NSTextField
        </code>
        , you can add it to your Mad Libs application! :]
    </p>
    <h2>
        Living in the Past — A Past Tense Verb
    </h2>
    <p>
        You will add various macOS controls to the MadLibs app, which will allow
        you to blindly construct a funny sentence. Once you’ve finished, you will
        combine all the different parts and display the result, hopefully with
        some comedic value. The more creative the you are, the more fun they’ll
        be!
    </p>
    <p>
        The first control you’ll add is a text field where you can enter a verb
        to add it to the sentence, as well as a label that informs what the text
        field is for.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        . Locate the
        <em>
            Label
        </em>
        control in the
        <em>
            Object Library
        </em>
        and drag it onto the view in the
        <em>
            View Controller Scene
        </em>
        . Double-click the label to edit the default text, and change it to
        <em>
            Past Tense Verb:
        </em>
        .
    </p>
    <p>
        Next, locate the
        <em>
            Text Field
        </em>
        control and drag it onto the view, placing it to the right of the label,
        like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-label.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-label-650x480.png"
            alt="drag-label" width="650" height="480" class="aligncenter size-large wp-image-153173"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-label-650x480.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/drag-label-434x320.png 434w, https://koenig-media.raywenderlich.com/uploads/2017/01/drag-label.png 1476w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Now, you’ll create an outlet to the text field in the view controller.
        While the
        <em>
            Main.storyboard
        </em>
        is open, go to the
        <em>
            Assistant editor
        </em>
        . Make sure that
        <em>
            ViewController.swift
        </em>
        is selected and
        <em>
            Ctrl-Drag
        </em>
        from the text field in the storyboard into the pane containing
        <em>
            ViewController.swift
        </em>
        , and release the mouse just below the class definition to create a new
        property:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-1-650x371.png"
            alt="textoutlet-1" width="650" height="371" class="aligncenter size-large wp-image-150118"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-1-650x371.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-1-480x274.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-1-266x151.png 266w, https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-1.png 1066w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        In the popup window that appears, name the Outlet
        <em>
            pastTenseVerbTextField
        </em>
        , and click
        <em>
            Connect
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-popup.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/textoutlet-popup-480x270.png"
            alt="textoutlet-popup" width="400" height="225" class="aligncenter size-medium wp-image-150119">
        </a>
    </p>
    <p>
        And that’s it! You now have an
        <code>
            NSTextField
        </code>
        property in your view controller that is connected to the text field in
        the main window.
    </p>
    <p>
        You know, it would be great to display some default text when the app
        launches to give an idea of what to put in the field. Since everyone loves
        to eat, and food related Mad Libs are always the most entertaining, the
        word
        <em>
            ate
        </em>
        would be a tasty choice here.
    </p>
    <p>
        A good place to put this is inside
        <code>
            viewDidLoad()
        </code>
        . Now, simply set the
        <code>
            stringValue
        </code>
        property you learned about earlier.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add the following code to the end of
        <code>
            viewDidLoad()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492953">
                    <td class="code" id="p149295code3">
                        <pre class="swift" style="font-family:monospace;">
                            // Sets the default text for the pastTenseVerbTextField property pastTenseVerbTextField.stringValue
                            = "ate"
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-textfield.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-textfield-409x320.png"
            alt="buildrun-textfield" width="409" height="320" class="aligncenter size-medium wp-image-153174"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-textfield-409x320.png 409w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-textfield-639x500.png 639w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-textfield.png 672w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <p>
        Okay, that takes care of a single input with a default value. But what
        if you want to provide a list of values to select from?
    </p>
    <p>
        Combo Boxes to the rescue!
    </p>
    <h2>
        The Value Combo – NSComboBox
    </h2>
    <p>
        A combo box is interesting — and quite handy — as it allows the user to
        choose one value from an array of options, as well as enter their own text.
    </p>
    <p>
        It looks similar to a text field in which the user can type freely, but
        it also contains a button that allows the user to display a list of selectable
        items. You can find a solid example of this in macOS’s Date &amp; Time
        preferences panel:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/date-sshot.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/date-sshot.png"
            alt="date-sshot" width="655" height="161" class="aligncenter size-full wp-image-150148"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/date-sshot.png 655w, https://koenig-media.raywenderlich.com/uploads/2016/12/date-sshot-480x118.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/date-sshot-650x160.png 650w"
            sizes="(max-width: 655px) 100vw, 655px">
        </a>
    </p>
    <p>
        Here, the user can select from a predefined list, or enter their own server
        name, if they wish.
    </p>
    <p>
        The macOS control responsible for this is
        <a href="http://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Classes/NSComboBox_Class/Reference/Reference.html"
        title="NSComboBox Class reference">
            NSComboBox.
        </a>
    </p>
    <p>
        <code>
            NSComboBox
        </code>
        has two distinct components: the text field where you can type, and the
        list of options which appear when the embedded button is clicked. You can
        control the data in both parts separately.
    </p>
    <p>
        To get or set the value in the text field, simply use the
        <code>
            stringValue
        </code>
        property covered earlier. Hooray for keeping things simple and consistent!
        :]
    </p>
    <p>
        Providing options for the list is a little more involved, but still relatively
        straightforward. You can call methods directly on the control to add elements
        in a manner similar to mutable
        <code>
            Array
        </code>
        , or you can use a data source — anyone with experience on iOS programming
        and
        <code>
            UITableViewDataSource
        </code>
        will feel right at home!
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            If you are not familiar with the concept of Data Sources, you can learn
            about it in Apple’s
            <a href="https://developer.apple.com/library/content/documentation/General/Conceptual/CocoaEncyclopedia/DelegatesandDataSources/DelegatesandDataSources.html"
            target="_blank">
                Delegates and Data Sources
            </a>
            documentation.
        </p>
    </div>
    <h3>
        Method 1 – Calling Methods Directly On The Control
    </h3>
    <p>
        <code>
            NSComboBox
        </code>
        contains an internal list of items, and exposes several methods that allow
        you to manipulate this list, as follows:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492954">
                    <td class="code" id="p149295code4">
                        <pre class="swift" style="font-family:monospace;">
                            // Add an object to the list myComboBox.addItem(withObjectValue: anObject)
                            &nbsp; // Add an array of objects to the list myComboBox.addItems(withObjectValues:
                            [objectOne, objectTwo, objectThree]) &nbsp; // Remove all objects from
                            the list myComboBox.removeAllItems() &nbsp; // Remove an object from the
                            list at a specific index myComboBox.removeItem(at: 2) &nbsp; // Get the
                            index of the currently selected object let selectedIndex = myComboBox.indexOfSelectedItem
                            &nbsp; // Select an object at a specific index myComboBox.selectItem(at:
                            1)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        That’s relatively straightforward, but what if you don’t want your options
        hardcoded in the app — such as a dynamic list that is stored outside of
        the app? That’s when using a datasource comes in really handy! :]
    </p>
    <h3>
        Method 2 – Using A Data Source
    </h3>
    <p>
        When using a data source the combo box will query the data source for
        the items it needs to display as well, as any necessary metadata, such
        as the number of items in the list. To obtain this information, you’ll
        need to implement the
        <a href="http://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Protocols/NSComboBoxDataSource_Protocol/Reference/Reference.html"
        title="NSComboBoxDataSource Protocol Reference">
            NSComboBoxDataSource
        </a>
        protocol in one of your classes, normally the View Controller hosting
        the control. From there, it’s a two-step process to configure the combo
        box to use the data source.
    </p>
    <p>
        First, set the control’s
        <code>
            usesDataSource
        </code>
        property to
        <code>
            true
        </code>
        . Then set the control’s
        <code>
            dataSource
        </code>
        property, passing an instance of the class implementing the protocol;
        when the class implementing the data source is the hosting View Controller
        a good place for this setup is
        <code>
            viewDidLoad()
        </code>
        , and then you set the
        <code>
            dataSource
        </code>
        property to
        <code>
            self
        </code>
        as shown below:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492955">
                    <td class="code" id="p149295code5">
                        <pre class="swift" style="font-family:monospace;">
                            class ViewController: NSViewController, NSComboBoxDataSource { ..... override
                            func viewDidLoad() { super.viewDidLoad() myComboBox.usesDataSource = true
                            myComboBox.dataSource = self } ..... }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            The order of the instructions in the code above is important. An attempt
            to set the
            <code>
                dataSource
            </code>
            property when
            <code>
                useDataSource
            </code>
            is
            <code>
                false
            </code>
            (which is the default) will fail and your data source will not be used.
        </p>
    </div>
    <p>
        In order to conform to the protocol, you’ll need to implement the following
        two methods from the data source protocol:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492956">
                    <td class="code" id="p149295code6">
                        <pre class="swift" style="font-family:monospace;">
                            // Returns the number of items that the data source manages for the combo
                            box func numberOfItems(in comboBox: NSComboBox) -&gt; Int { // anArray
                            is an Array variable containing the objects return anArray.count } &nbsp;
                            // Returns the object that corresponds to the item at the specified index
                            in the combo box func comboBox(_ comboBox: NSComboBox, objectValueForItemAt
                            index: Int) -&gt; Any? { return anArray[index] }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Finally, whenever your data source changes, to update the control, just
        call
        <code>
            reloadData()
        </code>
        on the combo box.
    </p>
    <h3>
        Which Method To Use?
    </h3>
    <p>
        If your list of items is relatively small and you don’t expect it to change
        that often, adding items once to the internal list is probably the best
        choice. But if your list of items is large or dynamic, it can often be
        more efficient to handle it yourself using a data source. For this tutorial
        you’ll be using method 1.
    </p>
    <p>
        Now that you’ve covered the fundamentals of the combo box, move on to
        implement one in your app! :]
    </p>
    <h2>
        The Singles Bar — A Singular Noun
    </h2>
    <p>
        In this section you’ll add a combo box to enter a singular noun. You can
        either choose from the list or enter your own.
    </p>
    <p>
        First, add a label that describes what the control is for.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        . Locate the
        <em>
            Label
        </em>
        control in the the
        <em>
            Object Library
        </em>
        palette, and drag it onto the content view. Change its alignment to
        <em>
            Right
        </em>
        and its title to
        <em>
            Singular Noun:
        </em>
        .
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            Alternatively as a shortcut, hold down the
            <em>
                Option
            </em>
            key and drag an existing label to duplicate it. This is handy so you can
            keep the same size and properties of an existing label.
        </p>
    </div>
    <p>
        Locate the
        <em>
            Combo Box
        </em>
        control and drag it onto the content view, placing it to the right of
        the label.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/addcombo.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/addcombo-650x481.png"
            alt="addcombo" width="650" height="481" class="aligncenter size-large wp-image-153175"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/addcombo-650x481.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/addcombo-433x320.png 433w, https://koenig-media.raywenderlich.com/uploads/2017/01/addcombo.png 1471w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Now you need to add an
        <code>
            NSComboBox
        </code>
        outlet to the view controller. Use the same technique you used for the
        text field: select the
        <em>
            Assistant Editor
        </em>
        (making sure
        <em>
            ViewController.swift
        </em>
        is selected) and
        <em>
            Ctrl-Drag
        </em>
        the combo box to the
        <code>
            ViewController
        </code>
        class just below the
        <code>
            NSTextField
        </code>
        :
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/combo-outlet.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/combo-outlet-650x382.png"
            alt="combo-outlet" width="650" height="382" class="aligncenter size-large wp-image-153176"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/combo-outlet-650x382.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/combo-outlet-480x282.png 480w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
        In the popup window that appears, name the outlet
        <em>
            singularNounCombo
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/combo-outlet-2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/combo-outlet-2.png"
            alt="combo-outlet-2" width="400" height="227" class="aligncenter size-full wp-image-150151"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/combo-outlet-2.png 496w, https://koenig-media.raywenderlich.com/uploads/2016/12/combo-outlet-2-480x273.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/combo-outlet-2-266x151.png 266w"
            sizes="(max-width: 400px) 100vw, 400px">
        </a>
    </p>
    <p>
        Now the
        <code>
            NSComboBox
        </code>
        property is connected to the combo box control. Next you are going to
        add some data to populate the list.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add this code under the outlets:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492957">
                    <td class="code" id="p149295code7">
                        <pre class="swift" style="font-family:monospace;">
                            fileprivate let singularNouns = ["dog", "muppet", "ninja", "pirate", "dev"
                            ]
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now, add the following code at the end of
        <em>
            viewDidLoad()
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492958">
                    <td class="code" id="p149295code8">
                        <pre class="swift" style="font-family:monospace;">
                            // Setup the combo box with singular nouns singularNounCombo.removeAllItems()
                            singularNounCombo.addItems(withObjectValues: singularNouns) singularNounCombo.selectItem(at:
                            singularNouns.count-1)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The first line removes any items added by default. Next, it adds the names
        from
        <code>
            singularNouns
        </code>
        to the combo box using
        <code>
            addItems()
        </code>
        . Then, it selects the last item of the list.
    </p>
    <p>
        Build and run the application to see your combo box in action!
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-combo.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-combo-409x320.png"
            alt="buildrun-combo" width="409" height="320" class="aligncenter size-medium wp-image-153178"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-combo-409x320.png 409w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-combo-639x500.png 639w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-combo.png 672w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <p>
        Great — it looks as though everything is working just right. If you click
        on the combo box, you can then view and select any of the other items.
    </p>
    <p>
        Now, what if you wanted to present a list of choices, but not allow you
        to enter your own? Read on, there’s a control for that as well!
    </p>
    <h2>
        Pop Goes the Weasel — NSPopupButton
    </h2>
    <p>
        The pop up button allows the user to choose from an array of options,
        but without giving the user the option of entering their own value in the
        control. The macOS control responsible for this is
        <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Classes/NSPopUpButton_Class/Reference/Reference.html"
        title="NSPopupButton Class Reference">
            NSPopupButton
        </a>
        .
    </p>
    <p>
        Pop up buttons are incredibly common in macOS, and you can find them in
        almost every application — including the one that you’re using right now:
        Xcode! :] You’re using the pop up button to set many of the properties
        on the macOS controls you’re using in this tutorial, as in the screenshot
        below:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/popup-example.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/popup-example-445x320.png"
            alt="popup-example" width="445" height="320" class="aligncenter size-medium wp-image-150155"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/popup-example-445x320.png 445w, https://koenig-media.raywenderlich.com/uploads/2016/12/popup-example.png 614w"
            sizes="(max-width: 445px) 100vw, 445px">
        </a>
    </p>
    <h3>
        Filling the Spaces — Adding Items To Pop Up Buttons
    </h3>
    <p>
        As you might expect, adding items to
        <code>
            NSPopUpButton
        </code>
        is similar to adding items to
        <code>
            NSComboBox
        </code>
        — except that
        <code>
            NSPopUpButton
        </code>
        doesn’t support using a data source for the content of the control.
        <code>
            NSPopUpButton
        </code>
        maintains an internal list of items and exposes several methods to manipulate
        it:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492959">
                    <td class="code" id="p149295code9">
                        <pre class="swift" style="font-family:monospace;">
                            // Add an item to the list myPopUpbutton.addItem(withTitle: "Pop up buttons
                            rock") &nbsp; // Add an array of items to the list myPopUpbutton.addItems(withTitles:
                            ["Item 1", "Item 2", "Item 3"]) &nbsp; // Remove all items from the list
                            myPopUpbutton.removeAllItems() &nbsp; // Get the index of the currently
                            selected item let selectedIndex = myPopUpbutton.indexOfSelectedItem &nbsp;
                            // Select an item at a specific index myPopUpbutton.selectItem(at: 1)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Pretty straightforward, isn’t it? That’s the beauty of macOS controls
        — there are a lot of similarities between them in terms of the methods
        used to manipulate the controls.
    </p>
    <p>
        Time to implement a pop up button in your app! :]
    </p>
    <h2>
        The More the Merrier — A Plural Noun
    </h2>
    <p>
        You’ll now add a pop up button to your Mad Libs application to choose
        between different plural nouns to populate your comical sentence.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        . Drag a label just below the
        <em>
            Singular Noun
        </em>
        label.
    </p>
    <p>
        Change the alignment to
        <em>
            Right
        </em>
        and the title to
        <em>
            Plural Noun:
        </em>
        . Next, locate the
        <em>
            Pop Up Button
        </em>
        control and drag it onto the window, placing it to the right of the label.
    </p>
    <p>
        The content view should look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/add-popup.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/add-popup-650x478.png"
            alt="add-popup" width="650" height="478" class="aligncenter size-large wp-image-153180"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/add-popup-650x478.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/add-popup-435x320.png 435w, https://koenig-media.raywenderlich.com/uploads/2017/01/add-popup.png 1033w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Now you need to add an outlet to the popup button, which should be fairly
        familiar by now: open the
        <em>
            Assistant editor
        </em>
        , make sure
        <em>
            ViewController.swift
        </em>
        is selected, and then
        <em>
            Ctrl-Drag
        </em>
        the pop up button to the
        <code>
            ViewController
        </code>
        class to create a new outlet:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-popup.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-popup-650x424.png"
            alt="drag-popup" width="650" height="424" class="aligncenter size-large wp-image-153181"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/drag-popup-650x424.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/drag-popup-480x313.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/drag-popup.png 1495w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
        In the popup window, name the outlet
        <em>
            pluralNounPopup
        </em>
        :
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/popup-outlet-2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/popup-outlet-2.png"
            alt="popup-outlet-2" width="400" height="244" class="aligncenter size-full wp-image-150159">
        </a>
    </p>
    <p>
        Now you just need some data to populate the control!
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add this property inside the class implementation.
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929510">
                    <td class="code" id="p149295code10">
                        <pre class="swift" style="font-family:monospace;">
                            fileprivate let pluralNouns = ["tacos", "rainbows", "iPhones", "gold coins"]
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now, add the following code to the bottom of
        <code>
            viewDidLoad()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929511">
                    <td class="code" id="p149295code11">
                        <pre class="swift" style="font-family:monospace;">
                            // Setup the pop up button with plural nouns pluralNounPopup.removeAllItems()
                            pluralNounPopup.addItems(withTitles: pluralNouns) pluralNounPopup.selectItem(at:
                            0)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The first line removes any existing items from the pop up button. The
        second line adds the array of nouns to the pop up button using
        <code>
            addItems()
        </code>
        . Finally, it selects the first item in the list.
    </p>
    <p>
        Build and run the application to see the result:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-popup.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-popup-407x320.png"
            alt="buildrun-popup" width="407" height="320" class="aligncenter size-medium wp-image-153182"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-popup-407x320.png 407w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-popup-635x500.png 635w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-popup.png 672w"
            sizes="(max-width: 407px) 100vw, 407px">
        </a>
    </p>
    <p>
        Once the app has launched, note that the pop up button shows the initial
        item,
        <em>
            tacos
        </em>
        , and if you click on the pop up button, you’ll see all the other items
        in the list.
    </p>
    <p>
        Okay, so you now have two macOS controls that allow the user to select
        from lists, as well as a control that allows the user to enter a single
        line of text. But what if you need to type more than a few words in a text
        field?
    </p>
    <p>
        Read on to learn about text views!
    </p>
    <h2>
        Text is Next – NSTextView
    </h2>
    <p>
        Text views, unlike text fields, are usually the control of choice for
        displaying rich text. Some implementations even allow for more advanced
        features such as displaying inline images.
    </p>
    <p>
        The macOS Control responsible for this is
        <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Classes/NSTextView_Class/Reference/Reference.html"
        title="NSTextView Class Reference">
            NSTextView
        </a>
        .
    </p>
    <p>
        A great example of an application using all of what
        <code>
            NSTextView
        </code>
        has to offer is TextEdit:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/textedit.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/textedit-650x210.png"
            alt="textedit" width="650" height="210" class="aligncenter size-large wp-image-150163"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/textedit-650x210.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/12/textedit-480x155.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/textedit.png 1430w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        <code>
            NSTextView
        </code>
        is so feature-rich that to cover everything would warrant a tutorial of
        its own, so here you’ll just see a few of the basic features in order to
        get you up and running! (Did you just breathe a sigh of relief?) :]
    </p>
    <p>
        Here are the basic methods you’ll need to work with text views:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929512">
                    <td class="code" id="p149295code12">
                        <pre class="swift" style="font-family:monospace;">
                            // Get the text from a text view let text = myTextView.string &nbsp; //
                            Set the text of a text view myTextView.string = "Text views rock too!"
                            &nbsp; // Set the background color of a text view myTextView.backgroundColor
                            = NSColor.white &nbsp; // Set the text color of a text view myTextView.textColor
                            = NSColor.black
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Relatively simple — nothing too shocking here.
    </p>
    <p>
        <code>
            NSTextView
        </code>
        also has built-in support for
        <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Reference/Foundation/Classes/NSAttributedString_Class/Reference/Reference.html"
        title="NSAttributedString Class Reference">
            NSAttributedString
        </a>
        . If you pass an attributed string to a text view, the string will be
        displayed correctly using all the appropriate attributes such as font,
        font size, and font color.
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            An attributed string is a special type of string where you can tag subsets
            of the string with different attributes – such as its font, its color,
            whether its bolded, and so on. To learn all about attributed strings, check
            out our
            <a href="/?page_id=77092" target="_blank">
                TextKit Tutorial
            </a>
            . It’s an iOS tutorial, but the information about
            <code>
                NSAttributedString
            </code>
            applies to Mac development as well.
        </p>
    </div>
    <h2>
        The Phrase that Pays – Adding a Text View
    </h2>
    <p>
        Looks like you have everything you need in order to add a text view to
        your Mad Libs application! This text view will allow the user to enter
        a multi-word phrase that will be used in the final rendered Mad Lib.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and drag a label just below the
        <em>
            Plural Noun
        </em>
        label (or duplicate an existing label, as mentioned earlier). Change its
        alignment to
        <em>
            Right
        </em>
        and its title to
        <em>
            Phrase:
        </em>
        .
    </p>
    <p>
        Next, locate the
        <em>
            Text View
        </em>
        control and drag it onto the window, placing it beside the label you just
        created.
    </p>
    <p>
        Your window should now look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/add-textview.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/add-textview-650x491.png"
            alt="add-textview" width="650" height="491" class="aligncenter size-large wp-image-153184"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/add-textview-650x491.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/add-textview-423x320.png 423w, https://koenig-media.raywenderlich.com/uploads/2017/01/add-textview.png 1439w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Now, if you try to resize the view and make it taller, you’ll notice something
        quite particular. The text view moves along, and changes its position when
        you resize the window.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-error.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-error-304x320.png"
            alt="textview-error" width="304" height="320" class="aligncenter size-medium wp-image-153185"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-error-304x320.png 304w, https://koenig-media.raywenderlich.com/uploads/2017/01/textview-error-474x500.png 474w, https://koenig-media.raywenderlich.com/uploads/2017/01/textview-error.png 683w"
            sizes="(max-width: 304px) 100vw, 304px">
        </a>
    </p>
    <p>
        That’s because by default, Xcode adds Auto resizing constraints to the
        text view, so that it repositions itself when its parent view is resized.
        Since you want the text view to stay put, you’ll need to disable some of
        those.
    </p>
    <p>
        Select the
        <em>
            Bordered Scroll View – Text View
        </em>
        from the Document Outline and go to the
        <em>
            Size Inspector
        </em>
        .
    </p>
    <p>
        In the
        <em>
            AutoResizing
        </em>
        section, you’ll see a rectangle which has four red lines connected to
        the parent view. Each one of these red connectors represents an Auto resizing
        constraint. You just need to click on the
        <em>
            Right
        </em>
        and
        <em>
            Bottom
        </em>
        red connectors to disable those, the solid red lines will turn to broken
        lines with a faded red color as shown below:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/add-autores.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/add-autores.png"
            alt="add-autores" width="344" height="109" class="aligncenter size-full wp-image-153187">
        </a>
    </p>
    <p>
        Now, the text view stays put and aligned with the label even if you resize
        the window.
    </p>
    <p>
        Next, add an
        <code>
            NSTextView
        </code>
        outlet to the view controller. Select the textview, open the
        <em>
            Assistant editor
        </em>
        and make sure
        <em>
            ViewController.swift
        </em>
        is selected.
        <em>
            Ctrl-Drag
        </em>
        from the text view to the
        <code>
            ViewController
        </code>
        class under the existing outlets.
    </p>
    <div class="note">
        <p>
            <em>
                Important:
            </em>
            Text views are contained inside scroll views. It’s important you make
            sure you’ve actually selected the text view before creating the outlet.
            To do so, simply click three times on the text view or select it in the
            <em>
                Document Outline
            </em>
            .
        </p>
    </div>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-drag.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-drag-650x447.png"
            alt="textview-drag" width="650" height="447" class="aligncenter size-large wp-image-153188"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-drag-650x447.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/textview-drag-465x320.png 465w, https://koenig-media.raywenderlich.com/uploads/2017/01/textview-drag.png 1393w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        In the popup window, make sure the type is
        <code>
            NSTextView
        </code>
        , and name the outlet
        <em>
            phraseTextView
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/textview-outlet2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/textview-outlet2.png"
            alt="textview-outlet2" width="400" height="227" class="aligncenter size-full wp-image-150166"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/textview-outlet2.png 496w, https://koenig-media.raywenderlich.com/uploads/2016/12/textview-outlet2-480x273.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/textview-outlet2-266x151.png 266w"
            sizes="(max-width: 400px) 100vw, 400px">
        </a>
    </p>
    <p>
        Now, add the following code to the end of
        <em>
            viewDidLoad()
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929513">
                    <td class="code" id="p149295code13">
                        <pre class="swift" style="font-family:monospace;">
                            // Setup the default text to display in the text view phraseTextView.string
                            = "Me coding Mac Apps!!!"
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run the application to see the result:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-result.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-result-355x320.png"
            alt="textview-result" width="355" height="320" class="aligncenter size-medium wp-image-153189"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/textview-result-355x320.png 355w, https://koenig-media.raywenderlich.com/uploads/2017/01/textview-result-554x500.png 554w, https://koenig-media.raywenderlich.com/uploads/2017/01/textview-result.png 672w"
            sizes="(max-width: 355px) 100vw, 355px">
        </a>
    </p>
    <p>
        Superb! The Mad Libs application is really starting to take shape now.
    </p>
    <h2>
        Pushing Your Buttons — NSButton
    </h2>
    <p>
        Buttons are macOS controls designed to send a message to the app whenever
        they’re clicked.
    </p>
    <p>
        The control responsible for this on macOS is
        <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Classes/NSButton_Class/Reference/Reference.html"
        title="NSButton Class Reference">
            NSButton
        </a>
        .
    </p>
    <p>
        There are many different styles of buttons (you can view them in Interface
        Builder’s Object Library). They all work in much the same way, the only
        difference being their visual representation.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/button-catalog-1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/button-catalog-1-476x500.png"
            alt="button-catalog" width="476" height="500" class="aligncenter size-large wp-image-150182"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/button-catalog-1-476x500.png 476w, https://koenig-media.raywenderlich.com/uploads/2016/12/button-catalog-1-305x320.png 305w, https://koenig-media.raywenderlich.com/uploads/2016/12/button-catalog-1.png 1090w"
            sizes="(max-width: 476px) 100vw, 476px">
        </a>
        You should use the style of button that best suits your application’s
        design — refer to the
        <a href="https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/OSXHIGuidelines/ControlsButtons.html#//apple_ref/doc/uid/20000957-CH48-SW1">
            macOS Human Interface Guidelines
        </a>
        for advice and guidance on best design practices for your app.
    </p>
    <p>
        Typically, when working with a button, you’ll simply need to associate
        an action with the button and set its title. However, there may be times
        when you need to disable the button, or change its appearance. The following
        methods allow you to perform those actions:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929514">
                    <td class="code" id="p149295code14">
                        <pre class="swift" style="font-family:monospace;">
                            // disable a button myButton.isEnabled = false &nbsp; // enable a button
                            myButton.isEnabled = true &nbsp; // getting &amp; setting a button's title
                            let theTitle = myButton.title myButton.title = theTitle &nbsp; // getting
                            &amp; setting a button's image let theImage = myButton.image myButton.image
                            = theImage
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Looks fairly simple — adding a button to your app in the next section
        should be a breeze.
    </p>
    <h2>
        Buttoning Things Down — Adding a Button
    </h2>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        . Find the
        <em>
            Push Button
        </em>
        in the Object Library palette and drag it onto the content view. Double-click
        on it to change its title to
        <em>
            Go!
        </em>
        :
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/button-add.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/button-add-614x500.png"
            alt="button-add" width="614" height="500" class="aligncenter size-large wp-image-153191"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/button-add-614x500.png 614w, https://koenig-media.raywenderlich.com/uploads/2017/01/button-add-393x320.png 393w, https://koenig-media.raywenderlich.com/uploads/2017/01/button-add.png 1474w"
            sizes="(max-width: 614px) 100vw, 614px">
        </a>
    </p>
    <p>
        This time you don’t need to create an outlet for the button. However,
        you do need to create an action and associate it with the button, so that
        your app knows when the button has been clicked! :]
    </p>
    <p>
        Open the
        <em>
            Assistant Editor
        </em>
        and
        <em>
            Ctrl+Drag
        </em>
        from the button to the
        <code>
            ViewController
        </code>
        implementation.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/button-addaction.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/button-addaction-650x373.png"
            alt="button-addaction" width="650" height="373" class="aligncenter size-large wp-image-153194"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/button-addaction-650x373.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/button-addaction-480x276.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/button-addaction.png 1435w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        In the popup window that appears, make sure that the connection is set
        to
        <em>
            Action
        </em>
        . Name the action
        <em>
            goButtonClicked
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/button-action-2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/button-action-2-480x229.png"
            alt="button-action-2" width="400" height="190" class="aligncenter size-medium wp-image-150171"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/button-action-2-480x229.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/button-action-2.png 504w"
            sizes="(max-width: 400px) 100vw, 400px">
        </a>
    </p>
    <p>
        Whenever the user clicks on the button the action method
        <code>
            goButtonClicked()
        </code>
        will be called. For now you’ll add some debug code, just to make sure
        everything’s working.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add the following code inside
        <code>
            goButtonClicked()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929515">
                    <td class="code" id="p149295code15">
                        <pre class="swift" style="font-family:monospace;">
                            let pastTenseVerb = pastTenseVerbTextField.stringValue let singularNoun
                            = singularNounCombo.stringValue let pluralNoun = pluralNouns[pluralNounPopup.indexOfSelectedItem]
                            let phrase = phraseTextView.string ?? "" &nbsp; let madLibSentence = "A
                            \(singularNoun) \(pastTenseVerb) \(pluralNoun) and said, \(phrase)!" &nbsp;
                            print("\(madLibSentence)")
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This code gets the strings from the text field, the combo box, the popup
        button and the text view and forms the Mad Lib sentence.
    </p>
    <p>
        Note that for the text view, the
        <code>
            string
        </code>
        property is actually an optional, so it could be
        <code>
            nil
        </code>
        . To guard against that case, you’re using the nil coalescing operator
        <code>
            ??
        </code>
        so if
        <code>
            string
        </code>
        is nil, you’ll get the empty string
        <code>
            ""
        </code>
        instead.
    </p>
    <p>
        That’s all the code you need for now — build and run your app.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/button-buildrun.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/button-buildrun-458x320.png"
            alt="button-buildrun" width="458" height="320" class="aligncenter size-medium wp-image-153195"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/button-buildrun-458x320.png 458w, https://koenig-media.raywenderlich.com/uploads/2017/01/button-buildrun-650x455.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/button-buildrun.png 672w"
            sizes="(max-width: 458px) 100vw, 458px">
        </a>
        <br>
        Every time you click the button, you should see a short and silly sentence
        appear in Xcode’s console.
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929516">
                    <td class="code" id="p149295code16">
                        <pre class="bash" style="font-family:monospace;">
                            A dev ate tacos and said: Me coding Mac Apps
                            <span style="color: #000000; font-weight: bold;">
                                !!!!
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        That’s great, but how could you make it even funnier?
    </p>
    <p>
        How about making your computer read the sentence? Steve Jobs made the
        first Macintosh say hello to the world in its presentation. You can make
        your computer talk too… Let’s get at it!
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add this code inside the
        <code>
            ViewController
        </code>
        implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929517">
                    <td class="code" id="p149295code17">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 fileprivate enum VoiceRate: Int { case slow case normal case fast
                            &nbsp; var speed: Float { switch self { case .slow: return 60 case .normal:
                            return 175; case .fast: return 360; } } } //2 fileprivate let synth = NSSpeechSynthesizer()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        First, you declare an
        <code>
            enum
        </code>
        to represent the voice rate. Then you create and instance of
        <code>
            NSSpeechSynthesizer
        </code>
        which is the class that will convert the text to speech.
    </p>
    <p>
        Now, add this method inside the
        <code>
            ViewController
        </code>
        implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929518">
                    <td class="code" id="p149295code18">
                        <pre class="swift" style="font-family:monospace;">
                            fileprivate func readSentence(_ sentence: String, rate: VoiceRate ) {
                            synth.rate = rate.speed synth.stopSpeaking() synth.startSpeaking(sentence)
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This method starts the
        <code>
            synth
        </code>
        object speaking a string at the determined speed.
    </p>
    <p>
        Time to call it! Add this code at the end of
        <code>
            goButtonClicked()
        </code>
        to read the Mad Libs sentence:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929519">
                    <td class="code" id="p149295code19">
                        <pre class="swift" style="font-family:monospace;">
                            readSentence(madLibSentence, rate: .normal)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run; click
        <em>
            Go!
        </em>
        and listen to your Mac saying your sentence out loud!
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
        You can the
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibs-part1-final-1.zip">
            download
        </a>
        the final project containing all the source code from this tutorial up
        to this point.
    </p>
    <p>
        In the
        <a href="https://www.raywenderlich.com/149297/macos-controls-tutorial-part-22"
        target="_blank" title="Core Controls in macOS: Part 2/2">
            second part of this tutorial
        </a>
        , you’ll learn about more macOS controls, including sliders, date pickers,
        radio buttons, check boxes and image views — each of which will be added
        to your Mad Libs application in order to complete it.
    </p>
    <p>
        In the meantime, if you have any questions or comments about what you’ve
        done so far, join in the forum discussion below!
    </p>
</div>
