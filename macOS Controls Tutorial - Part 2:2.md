# macOS控件教程：2/2部分

#### [原文地址](https://www.raywenderlich.com/149297/macos-controls-tutorial-part-22) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div id="attachment_153233" style="width: 260px" class="wp-caption alignright">
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-250x250.png"
            alt="Get started with macOS controls!" width="250" height="250" class="size-thumbnail wp-image-153233"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2017/01/CoreControls-feature-128x128.png 128w"
            sizes="(max-width: 250px) 100vw, 250px">
        </a>
        <p class="wp-caption-text">
            More macOS Controls!
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
        Welcome back to the second and final part of this macOS Controls tutorial
        series!
    </p>
    <p>
        In the
        <a href="https://www.raywenderlich.com/149295/macos-controls-tutorial-part-12"
        title="first part">
            first part of this tutorial
        </a>
        , you started building a Mad Libs style macOS application, where the user
        enters various words and phrases to create a funny sentence.
    </p>
    <p>
        Along the way, you learned about some of the core UI macOS controls —
        namely, Text Fields, Combo Boxes, Pop Up Buttons, Push Buttons and Text
        Views.
    </p>
    <h2>
        More macOS Controls
    </h2>
    <p>
        In this final part of the tutorial, you’ll finish off your application,
        and learn how to use the following:
    </p>
    <ul>
        <li>
            Sliders
        </li>
        <li>
            Date Pickers
        </li>
        <li>
            Radio Buttons
        </li>
        <li>
            Check Boxes
        </li>
        <li>
            Image Views
        </li>
    </ul>
    <p>
        At the end of this two-part tutorial you’ll have a solid understanding
        of macOS controls.
    </p>
    <p>
        This tutorial will pick up where you left off. If you don’t have it already,
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibs-part1-final-1.zip">
            here’s the final project
        </a>
        of the first part.
    </p>
    <p>
        It’s time to get to work!
    </p>
    <h2>
        Slipping and Sliding — NSSlider
    </h2>
    <p>
        A slider is a control that lets the user choose from a range of values.
        A slider has a minimum and a maximum value, and by moving the control’s
        knob, the user can choose a value between those two limits. Sliders can
        be either linear or radial. What’s the difference between the two, you
        ask?
    </p>
    <p>
        Linear sliders can be either vertical or horizontal, and they let you
        choose a value by moving the knob along the track. A really great example
        of linear sliders is in macOS’ Mouse preferences panel:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/slider-mouse.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/slider-mouse.png"
            alt="slider-mouse" width="340" height="148" class="aligncenter size-full wp-image-150213">
        </a>
    </p>
    <p>
        Radial sliders are a little different — they are displayed as a small
        circle with a knob, which can be rotated a full 360 degrees. To select
        a value, you click and drag the knob to the required position. You can
        find a great example of radial sliders in Adobe Photoshop, where they’re
        used to define the angle of a gradient, as such:
    </p>
    <p>
        <a href="https://www.raywenderlich.com/slider-example-radial" rel="attachment wp-att-27039">
            <img src="https://koenig-media.raywenderlich.com/uploads/2012/12/slider-example-radial.png"
            alt="" title="slider-example-radial" width="339" height="144" class="aligncenter size-full wp-image-27039">
        </a>
    </p>
    <p>
        The control responsible for this on macOS is an
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ApplicationKit/Classes/NSSlider_Class/Reference/Reference.html"
        title="NSSlider Class Reference">
            NSSlider
        </a>
        .
    </p>
    <p>
        All three types of sliders (horizontal, vertical and radial) are in fact
        the same control,
        <code>
            NSSlider
        </code>
        . The only difference is how they’re displayed. Interface Builder has
        an object in the Object Library for each of the three types, as shown below:
    </p>
    <p>
        <a href="http://www.raywenderlich.com/82047/introduction-to-os-x-tutorial-core-controls-and-swift-part-2/sliders-ib-2"
        rel="attachment wp-att-83305">
            <img src="https://koenig-media.raywenderlich.com/uploads/2014/09/sliders-ib.png"
            alt="sliders-ib" width="295" height="282" class="aligncenter size-full wp-image-83305"
            srcset="https://koenig-media.raywenderlich.com/uploads/2014/09/sliders-ib.png 295w, https://koenig-media.raywenderlich.com/uploads/2014/09/sliders-ib-32x32.png 32w"
            sizes="(max-width: 295px) 100vw, 295px">
        </a>
    </p>
    <h3>
        Slider Semantics
    </h3>
    <p>
        There are two common tasks you’re likely to perform when working with
        sliders: getting or setting the current value, and getting and setting
        the high and low limits of the slider’s range. These properties are outlined
        here:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492971">
                    <td class="code" id="p149297code1">
                        <pre class="swift" style="font-family:monospace;">
                            // getting &amp; setting an integer value let theInteger = mySlider.integerValue
                            mySlider.integerValue = theInteger &nbsp; // getting &amp; setting a float
                            value let theFloat = mySlider.floatValue mySlider.floatValue = theFloat
                            &nbsp; // getting &amp; setting a double value let theDouble = mySlider.doubleValue
                            mySlider.doubleValue = theDouble &nbsp; // getting &amp; setting the minimum
                            value of the range let theMinimumValue = mySlider.minValue mySlider.minValue
                            = theMinimumValue &nbsp; // getting &amp; setting the maximum value of
                            the range let theMaximumValue = mySlider.maxValue mySlider.maxValue = theMaximumValue
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Again, nothing too surprising here — if you’ve learned anything by now,
        it’s that implementing standard UI macOS controls is a fairly straightforward
        exercise. Move on to the next section to include an
        <code>
            NSSlider
        </code>
        in your app!
    </p>
    <h2>
        Pick a Number, Any Number
    </h2>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        . Locate the
        <em>
            Label
        </em>
        control In the Object Library palette and drag it onto the content view
        below the Phrase label. Resize the window vertically and move the
        <em>
            Go!
        </em>
        button down if you need to make space for it.
    </p>
    <p>
        Double-click the control to edit its default text, and change it to
        <em>
            Amount: [10]
        </em>
        . Find the
        <em>
            Horizontal Slider
        </em>
        control and drag it onto the window, placing it to the right of the label.
    </p>
    <p>
        Click on the slider to select it. Open the
        <em>
            Attributes Inspector
        </em>
        and set the Minimum value to 2, and the Maximum value to 10. Change the
        Current value to 5. This will be the default value of the slider when the
        user first runs the app.
    </p>
    <p>
        Make sure that
        <em>
            Continuous
        </em>
        is checked. This tells the slider to notify
        <em>
            any
        </em>
        change in the slider’s value.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-add-1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-add-1-650x439.png"
            alt="slider-add" width="650" height="439" class="aligncenter size-large wp-image-153200"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-add-1-650x439.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/slider-add-1-474x320.png 474w, https://koenig-media.raywenderlich.com/uploads/2017/01/slider-add-1.png 1421w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Now you need to create two outlets; one for the slider, and one for the
        label. Wait, you may say — that’s a little different. Why are you adding
        a property for the label?
    </p>
    <p>
        That’s so you can update the label’s text to list the current amount whenever
        the value of the slider is changed; hence why you set the
        <em>
            Continuous
        </em>
        property on the slider. Aha! Makes sense now, doesn’t it?
    </p>
    <p>
        Open the Assistant editor and make sure
        <em>
            ViewController.swift
        </em>
        is open.
        <em>
            Ctrl-Drag
        </em>
        from label to
        <em>
            ViewController.swift
        </em>
        to create a new outlet.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-drag-1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-drag-1-650x455.png"
            alt="slider-drag" width="650" height="455" class="aligncenter size-large wp-image-153201"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-drag-1-650x455.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/slider-drag-1-457x320.png 457w, https://koenig-media.raywenderlich.com/uploads/2017/01/slider-drag-1.png 1364w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        In the popup screen, name the outlet
        <em>
            amountLabel
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/amountlabel-drag2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/amountlabel-drag2-480x269.png"
            alt="amountlabel-drag2" width="480" height="269" class="aligncenter size-medium wp-image-150235"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/amountlabel-drag2-480x269.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/amountlabel-drag2.png 504w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Repeat the above process with the slider, naming the outlet
        <em>
            amountSlider
        </em>
        .
    </p>
    <p>
        Now you need to add an
        <em>
            action
        </em>
        that will be called when the slider value changes. You already created
        an action for your button in Part 1; adding an action is very much like
        creating an outlet, so you’ll get a little more practice!
    </p>
    <p>
        Select the slider and
        <em>
            Ctrl-Drag
        </em>
        to
        <em>
            ViewController.swift
        </em>
        anywhere within the class definition:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-action-drag.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-action-drag-650x365.png"
            alt="slider-action-drag" width="650" height="365" class="aligncenter size-large wp-image-153202"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/slider-action-drag-650x365.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/slider-action-drag-480x269.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/slider-action-drag.png 1381w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        In the popup window, be sure to set the connection as an
        <em>
            action
        </em>
        rather than a outlet. Name it
        <em>
            sliderChanged
        </em>
        , like so:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/slider-action2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/slider-action2-480x228.png"
            alt="slider-action2" width="400" height="190" class="aligncenter size-medium wp-image-150237"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/slider-action2-480x228.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/slider-action2.png 500w"
            sizes="(max-width: 400px) 100vw, 400px">
        </a>
    </p>
    <p>
        Now you need to update the label whenever the action is called.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add the following code inside
        <code>
            sliderChanged()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492972">
                    <td class="code" id="p149297code2">
                        <pre class="swift" style="font-family:monospace;">
                            let amount = amountSlider.integerValue amountLabel.stringValue = "Amount:
                            [\(amount)]"
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        A quick review of the code above shows that you first read the slider’s
        current value. Then you set the value of the label to a string containing
        the slider’s value. Please note, that although
        <code>
            amountLabel
        </code>
        cannot be edited by the user from the UI, it is still editable programmatically.
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            This example uses
            <code>
                integerValue
            </code>
            to get a nice round number, but if you need more precision you could use
            either
            <code>
                floatValue
            </code>
            or
            <code>
                doubleValue
            </code>
            for your slider.
        </p>
    </div>
    <p>
        Build and run the app. Try moving the slider back and forth to see the
        label update with the slider’s current value:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-slider.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-slider-386x320.png"
            alt="buildrun-slider" width="386" height="320" class="aligncenter size-medium wp-image-153203"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-slider-386x320.png 386w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-slider-603x500.png 603w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-slider.png 672w"
            sizes="(max-width: 386px) 100vw, 386px">
        </a>
    </p>
    <p>
        There’s one small problem. Did you notice it? The label doesn’t display
        the correct value when the app first launches! While it’s not a big problem,
        it makes the app look unfinished. It’s because the label is only updating
        when the slider’s knob is moved.
    </p>
    <p>
        Fear not — it’s very easy to fix.
    </p>
    <p>
        Add the following code to the end of
        <code>
            viewDidLoad()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492973">
                    <td class="code" id="p149297code3">
                        <pre class="swift" style="font-family:monospace;">
                            // Update the amount slider sliderChanged(self)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now the app will call
        <code>
            sliderChanged()
        </code>
        at launch, and that will update the label. Neat!
    </p>
    <p>
        Build and run. The label now displays the correct value at first run,
        which is a small touch, but is one of those “fit and finish” elements that
        make your app look polished.
    </p>
    <p>
        What about more complicated values, such as calendar dates? Yup, macOS
        has those handled too! :]
    </p>
    <h2>
        Hot Date Tonight — NSDatePicker
    </h2>
    <p>
        Date Picker is a macOS control that display date and time values, as well
        as providing a method for the user to edit those values. Date Pickers can
        be configured to display a date, a time or both a date and time. The control
        responsible for this on macOS is
        <a href="http://developer.apple.com/library/mac/#documentation/Cocoa/Reference/ApplicationKit/Classes/NSDatePicker_Class/Reference/Reference.html"
        title="NSDatePicker Class Reference">
            NSDatePicker
        </a>
        .
    </p>
    <p>
        Date Pickers can be displayed in one of two styles: textual, where the
        date and time information is shown in text fields, and graphical, where
        the date is represented by a calendar and the time by a clock. You can
        find examples of all these styles in macOS’ Date &amp; Time preferences
        panel, as in the screenshot below:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/date-macos.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/date-macos-480x232.png"
            alt="date-macos" width="480" height="232" class="aligncenter size-medium wp-image-150214"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/date-macos-480x232.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/date-macos-650x314.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/12/date-macos.png 974w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        The most common tasks you’ll perform with a date picker are getting and
        setting the date or time value, and setting the minimum and maximum date
        or time values that are permitted in your control. The properties to do
        this are set out below!
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492974">
                    <td class="code" id="p149297code4">
                        <pre class="swift" style="font-family:monospace;">
                            // getting &amp; setting the date/time value let myDate = myDatePicker.dateValue
                            myDatePicker.dateValue = myDate &nbsp; // getting &amp; setting the minimum
                            date of the range let theMinimumDate = myDatePicker.minDate myDatePicker.minDate
                            = theMinimumDate &nbsp; // getting &amp; setting the maximum date of the
                            range let theMaximumDate = myDatePicker.maxDate myDatePicker.maxDate =
                            theMaximumDate
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Again — the controls have a very simple getter and setter style interface
        to update these values. Now it’s time (pardon the pun!) to put this control
        to work.
    </p>
    <h2>
        I’m Late for a Very Important Date
    </h2>
    <p>
        Following the usual procedure, add a new
        <em>
            Label
        </em>
        to your window. Change its title to
        <em>
            Date:
        </em>
        and its alignment to
        <em>
            Right
        </em>
        . Find the
        <em>
            Date Picker
        </em>
        control in the Object palette, and drag it onto the window, placing it
        to the right of the label. Resize the window and move the
        <em>
            Go!
        </em>
        button down if needed:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/add-datepicker.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/add-datepicker-650x374.png"
            alt="add-datepicker" width="650" height="374" class="aligncenter size-large wp-image-153206"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/add-datepicker-650x374.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/add-datepicker-480x276.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/add-datepicker.png 1441w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Create an outlet for the date picker, just as you’ve done for each of
        the previous macOS controls. In the popup window, name the property
        <em>
            datePicker
        </em>
        .
    </p>
    <p>
        Just like the other macOS controls in your app, it’s nice to display a
        default value to the user when they first run your application. Picking
        today’s date as the default sounds like a good choice! :]
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
                <tr id="p1492975">
                    <td class="code" id="p149297code5">
                        <pre class="swift" style="font-family:monospace;">
                            // Set the date picker to display the current date datePicker.dateValue
                            = Date()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run the app! You should see your shiny new date picker displaying
        current date, like in the screenshot below:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-datepicker.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-datepicker-386x320.png"
            alt="buildrun-datepicker" width="386" height="320" class="aligncenter size-medium wp-image-153207"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-datepicker-386x320.png 386w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-datepicker-603x500.png 603w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-datepicker.png 672w"
            sizes="(max-width: 386px) 100vw, 386px">
        </a>
    </p>
    <h2>
        Video Killed the Radio…Button
    </h2>
    <p>
        Radio buttons are a special type of control that always appear in groups;
        they are typically displayed as a list of options with selectable buttons
        alongside. Their behavior is also somewhat unique; any button within the
        group can be selected, but selecting one button will deselect all other
        buttons in the group. Only a single button, within the same group, can
        be selected at one time.
    </p>
    <p>
        A good example of radio buttons that are used to present a set of options
        is the iTunes Back Up options, as shown below:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2012/12/radio-example.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2012/12/radio-example.png"
            alt="" title="radio-example" width="369" height="121" class="aligncenter size-full wp-image-27114">
        </a>
    </p>
    <p>
        Radio buttons are organized in radio groups.
    </p>
    <p>
        When you click a radio button in a group, it is selected and the system
        automatically deselects the rest of the buttons within that group. You
        only need to worry about getting and setting the proper values. How convenient!
    </p>
    <p>
        But how do you define a group? Quoting the documentation:
    </p>
    <p>
        <i>
            “Radio buttons automatically act as a group (selecting one button will
            unselect all other related buttons) when they have the same superview and
            -action method.”
        </i>
        .
    </p>
    <p>
        So, all you need to do is add the radio buttons to a view, create an action,
        and assign that action to all the buttons in the group.
    </p>
    <p>
        Then you just need to change the state of one button (On / Off) and the
        system will take care of deselecting the others.
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492976">
                    <td class="code" id="p149297code6">
                        <pre class="swift" style="font-family:monospace;">
                            // Select a radio button radioButton.state = NSOnState &nbsp; // Deselect
                            a radio button radioButton.state = NSOffState &nbsp; // Check if a radio
                            button is selected. let selected = (radioButton.state == NSOnState)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Once again, a complicated control is reduced to some very simple methods.
        Read on to see how to implement a radio button control in your app!
    </p>
    <h2>
        A Place to Call Home – Adding Radio Buttons
    </h2>
    <p>
        Add a new
        <em>
            Label
        </em>
        to your app (you should be getting pretty comfortable with this by now!),
        and change its title to
        <em>
            Place:
        </em>
        . Locate the
        <em>
            Radio Button
        </em>
        in the Object Library palette, and drag three onto the content view, just
        beside the label. Double click on the radio buttons to change their titles
        to:
        <em>
            RWDevCon
        </em>
        ,
        <em>
            360iDev
        </em>
        and
        <em>
            WWDC
        </em>
        respectively.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/radioadd.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/radioadd-638x500.png"
            alt="radioadd" width="638" height="500" class="aligncenter size-large wp-image-153209"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/radioadd-638x500.png 638w, https://koenig-media.raywenderlich.com/uploads/2017/01/radioadd-408x320.png 408w, https://koenig-media.raywenderlich.com/uploads/2017/01/radioadd.png 1599w"
            sizes="(max-width: 638px) 100vw, 638px">
        </a>
    </p>
    <p>
        Now, you need to create a new outlet for every radio button — another
        action you should be quite familiar with by now! Open the
        <em>
            Assistant Editor
        </em>
        and
        <em>
            Ctrl-Drag
        </em>
        the first radio button into the
        <em>
            ViewController.swift
        </em>
        source file, just below the existing properties. Name the outlet
        <em>
            rwDevConRadioButton
        </em>
        . Repeat the process for the other two radio buttons, naming the outlets
        <em>
            threeSixtyRadioButton
        </em>
        and
        <em>
            wwdcRadioButton
        </em>
        respectively.
    </p>
    <p>
        Build and run.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-error.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-error-469x500.png"
            alt="buildrun-radio-error" width="469" height="500" class="aligncenter size-large wp-image-153210"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-error-469x500.png 469w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-error-300x320.png 300w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-error.png 672w"
            sizes="(max-width: 469px) 100vw, 469px">
        </a>
    </p>
    <p>
        Click on the radio buttons, and you’ll immediately notice a problem. You
        can select all of them. They’re not behaving as a group. Why? Because there
        are two conditions for different radio buttons to act as a group: They
        must have the same superview (which is the case), and they need to have
        a common action. The second condition is not met in our app.
    </p>
    <p>
        To solve that, you need to create a common action for those buttons.
    </p>
    <p>
        You are already an expert creating actions using Interface Builder, right?
        So, to learn an alternative way to do it, you’re going to create the action
        in code and assign it to the radio buttons in Interface Builder.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add the following code inside the class implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492977">
                    <td class="code" id="p149297code7">
                        <pre class="swift" style="font-family:monospace;">
                            @IBAction func radioButtonChanged(_ sender: AnyObject) { &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        That’s a typical action method which includes the
        <code>
            @IBAction
        </code>
        annotation so that Interface Builder can find it and use it. Now, open
        <em>
            Main.storyBoard
        </em>
        to assign this action to the radio buttons.
    </p>
    <p>
        Go to the
        <em>
            Document Outline
        </em>
        and
        <em>
            Control-Click
        </em>
        (or right click) on the View Controller. Go to the
        <em>
            Received Actions
        </em>
        section in the popup window, and drag from the circle next to
        <code>
            radioButtonChanged:
        </code>
        onto the
        <em>
            RWDevCon
        </em>
        radio button. With that simple action you’ve just assigned the action
        to that radio button.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/radio-addaction.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/radio-addaction-548x500.png"
            alt="radio-addaction" width="548" height="500" class="aligncenter size-large wp-image-153211"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/radio-addaction-548x500.png 548w, https://koenig-media.raywenderlich.com/uploads/2017/01/radio-addaction-351x320.png 351w, https://koenig-media.raywenderlich.com/uploads/2017/01/radio-addaction.png 1072w"
            sizes="(max-width: 548px) 100vw, 548px">
        </a>
    </p>
    <p>
        Repeat the process to assign the same action to the other two radio buttons.
        Your received actions section should look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/radio-actions-all.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/radio-actions-all-480x218.png"
            alt="radio-actions-all" width="300" height="136" class="aligncenter size-medium wp-image-150253"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/radio-actions-all-480x218.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/radio-actions-all.png 512w"
            sizes="(max-width: 300px) 100vw, 300px">
        </a>
    </p>
    <p>
        Build and run:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-469x500.png"
            alt="buildrun-radio" width="469" height="500" class="aligncenter size-large wp-image-153212"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-469x500.png 469w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio-300x320.png 300w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-radio.png 672w"
            sizes="(max-width: 469px) 100vw, 469px">
        </a>
    </p>
    <p>
        Now the radio buttons are behaving like a group.
    </p>
    <p>
        Now you’ll need to to make the
        <em>
            RWDevCon
        </em>
        radio button the default when the app starts. You just need to set the
        radio button state to On, and then the other buttons will be automatically
        deselected.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        . Add the following code to the end of
        <code>
            viewDidLoad()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492978">
                    <td class="code" id="p149297code8">
                        <pre class="swift" style="font-family:monospace;">
                            // Set the radio group's initial selection rwDevConRadioButton.state =
                            NSOnState
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run the application. You should see the
        <em>
            RWDevCon
        </em>
        radio button selected when the app starts.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/radio-rwdev.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/radio-rwdev.png"
            alt="radio-rwdev" width="300" height="121" class="aligncenter size-full wp-image-150255">
        </a>
    </p>
    <p>
        Radio buttons are one way to toggle values in your app, but there’s another
        class of macOS controls that perform a similar function — check boxes!
    </p>
    <h2>
        Ticking all the Boxes — Check Box Button
    </h2>
    <p>
        You typically use check boxes in an app to display the state of some boolean
        value. That state tends to influence the app in some way such as enabling
        or disabling a feature.
    </p>
    <p>
        You will likely find check boxes where the user can enable or disable
        a functionality. You can find them in almost every screen of the Settings
        app. For instance, in the Energy Saver window you use them to enable or
        disable the different energy options.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/check-example.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/check-example-480x138.png"
            alt="check-example" width="480" height="138" class="aligncenter size-medium wp-image-153214"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/check-example-480x138.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/check-example-650x187.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/check-example.png 790w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Working with check boxes is relatively easy; most of the time you’ll only
        be concerned with getting and setting the state of the control. The state
        of the check box can be one of these:
        <em>
            NSOnState
        </em>
        (feature on everywhere),
        <em>
            NSOffState
        </em>
        (feature off everywhere) and
        <em>
            NSMixedState
        </em>
        (feature on somewhere, but not everywhere).
    </p>
    <p>
        Here’s how you can use it:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1492979">
                    <td class="code" id="p149297code9">
                        <pre class="swift" style="font-family:monospace;">
                            // Set the state to On myCheckBox.state = NSOnState &nbsp; // Set the
                            state to Off myCheckBox.state = NSOffState &nbsp; // Get the state of a
                            check box let state = myCheckBox.state
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Super simple! Time to add a checkbox to your app.
    </p>
    <h2>
        Check and Double Check – Adding Checkboxes
    </h2>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        . Find the
        <em>
            Check Box Button
        </em>
        in the Object Library and drag it onto the content view. Double-click
        on it to change its title to
        <em>
            Yell!!
        </em>
        as in the image below:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/check-add.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/check-add-650x447.png"
            alt="check-add" width="650" height="447" class="aligncenter size-large wp-image-153215"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/check-add-650x447.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/check-add-465x320.png 465w, https://koenig-media.raywenderlich.com/uploads/2017/01/check-add.png 1572w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Now add an outlet for the check box and name it
        <em>
            yellCheck
        </em>
        . You are now officially an expert creating outlets!
    </p>
    <p>
        Now, you’ll make the check box default to the off state when the app launches.
        To do that, add the following at the end of
        <code>
            viewDidLoad()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929710">
                    <td class="code" id="p149297code10">
                        <pre class="swift" style="font-family:monospace;">
                            // set check button state yellCheck.state = NSOffState
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run the application! You should see the check box, and it’s
        state should be unchecked. Click it to see it in action:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-check.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-check-477x500.png"
            alt="buildrun-check" width="477" height="500" class="aligncenter size-large wp-image-153217"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-check-477x500.png 477w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-check-305x320.png 305w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-check.png 672w"
            sizes="(max-width: 477px) 100vw, 477px">
        </a>
    </p>
    <h2>
        Choices, Choices – NSSegmentedControl
    </h2>
    <p>
        A segmented control, represented by the
        <a href="https://developer.apple.com/reference/appkit/nssegmentedcontrol"
        target="_blank">
            NSSegmentedControl
        </a>
        class , represents an alternative to radio buttons when you need to make
        a selection from a number of options. You can see it in Xcode’s Attributes
        Inspector:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/segmented-alignment.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/segmented-alignment.png"
            alt="segmented-alignment" width="504" height="190" class="aligncenter size-full wp-image-150265"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/segmented-alignment.png 504w, https://koenig-media.raywenderlich.com/uploads/2016/12/segmented-alignment-480x181.png 480w"
            sizes="(max-width: 504px) 100vw, 504px">
        </a>
    </p>
    <p>
        It’s very easy to use. You just need to get or set the selected segment
        to find out the user’s selection.
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929711">
                    <td class="code" id="p149297code11">
                        <pre class="swift" style="font-family:monospace;">
                            &nbsp; // Select the first segment segmentedControl.selectedSegment =
                            0 &nbsp; // Get the selected segment let selected = segmentedControl.selectedSegment
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <h2>
        Tuning the Voice – Adding Segmented Controls
    </h2>
    <p>
        If you remember, the
        <code>
            readSentence()
        </code>
        had a parameter to control the voice speed (Normal, Fast, Slow). You’ll
        use a segmented control to change the speed of the voice.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and add a Label to the content view. Change its title to
        <em>
            Voice Speed:
        </em>
        . Locate a
        <em>
            Segmented Control
        </em>
        and drag it onto the content view. You can double click on every segment
        of the control to set its title. Change the titles to
        <em>
            Slow
        </em>
        ,
        <em>
            Normal
        </em>
        and
        <em>
            Fast
        </em>
        respectively.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/segmented-add-1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/segmented-add-1-650x400.png"
            alt="segmented-add" width="650" height="400" class="aligncenter size-large wp-image-153219"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/segmented-add-1-650x400.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/segmented-add-1-480x295.png 480w, https://koenig-media.raywenderlich.com/uploads/2017/01/segmented-add-1.png 1536w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Create an outlet for that segmented control in
        <code>
            ViewController
        </code>
        , and name it
        <em>
            voiceSegmentedControl
        </em>
        . Now, you want to select the Normal segment when the app starts, which
        is the segment number 1 (segment numbers are zero based). Open
        <em>
            ViewController.swift
        </em>
        and add the following code to
        <code>
            viewDidLoad()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929712">
                    <td class="code" id="p149297code12">
                        <pre class="swift" style="font-family:monospace;">
                            // Set the segmented control initial selection voiceSegmentedControl.selectedSegment
                            = 1
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        As easy as it looks. Just set the
        <code>
            selectedSegment
        </code>
        property to 1. Build and run now and see how the Normal segment is selected.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-selected.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-selected-286x320.png"
            alt="buildrun-selected" width="286" height="320" class="aligncenter size-medium wp-image-153220"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-selected-286x320.png 286w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-selected-446x500.png 446w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-selected.png 672w"
            sizes="(max-width: 286px) 100vw, 286px">
        </a>
    </p>
    <p>
        Okay! You’ve finally added all the controls you need to create your funny
        mad lib sentences. All you’re missing is a way to collect the value of
        each control, combine those values into a sentence, and display it on-screen!
    </p>
    <h2>
        Pulling it All Together
    </h2>
    <p>
        You need two more controls to show the results: a label to display the
        complete sentence, and an image view to display a picture, which should
        liven up the user interface!
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        . Find the
        <em>
            Wrapping Label
        </em>
        in the Object Library palette and drag it onto the window, just below
        the
        <em>
            Go!!
        </em>
        button. Make it look a little more attractive by using the
        <em>
            Attributes Inspector
        </em>
        to change the border of the label to Frame, which is the first of the
        four buttons.
    </p>
    <p>
        After that, remove the default text of the label by double-clicking it,
        selecting the text and deleting it.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/resulttext-add.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/resulttext-add-650x456.png"
            alt="resulttext-add" width="650" height="456" class="aligncenter size-large wp-image-153222"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/resulttext-add-650x456.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/resulttext-add-457x320.png 457w, https://koenig-media.raywenderlich.com/uploads/2017/01/resulttext-add.png 1508w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Now you have to create an outlet to set the value of this new label to
        contain your new hilarious sentence! As before,
        <em>
            Ctrl-Drag
        </em>
        the label to the
        <em>
            ViewController.swift
        </em>
        file and name the property
        <em>
            resultTextField
        </em>
        .
    </p>
    <p>
        Leave this control as it is for now; you’ll write the code that populates
        it in just a bit.
    </p>
    <h2>
        Room with a View — NSImageView
    </h2>
    <p>
        An Image View is a simple and easy to use control that — surprise! — displays
        an image. Bet you didn’t expect that! :]
    </p>
    <p>
        <a href="https://www.raywenderlich.com/obvious" rel="attachment wp-att-27048">
            <img src="https://koenig-media.raywenderlich.com/uploads/2012/12/OBVIOUS.png"
            alt="" title="OBVIOUS" width="400" height="250" class="aligncenter size-full wp-image-27048">
        </a>
    </p>
    <p>
        There are very few properties you need to interact with an Image View
        at runtime:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929713">
                    <td class="code" id="p149297code13">
                        <pre class="swift" style="font-family:monospace;">
                            // Get the image from an image view let myImage = myImageView.image &nbsp;
                            // Set the image of an image view myImageView.image = myImage
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        At design time, you can configure the visual aspects: the border, scaling
        and alignment. Yes, these properties can be set in code as well, but it’s
        far easier to set them in Interface Builder at design time, as below:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/imageview-props.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/imageview-props-393x320.png"
            alt="imageview-props" width="300" height="244" class="aligncenter size-medium wp-image-150261"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/imageview-props-393x320.png 393w, https://koenig-media.raywenderlich.com/uploads/2016/12/imageview-props.png 508w"
            sizes="(max-width: 300px) 100vw, 300px">
        </a>
    </p>
    <h2>
        Just a Pretty Face – Populating the Image Well
    </h2>
    <p>
        Time to add an image view to your application! Find the
        <em>
            Image Well
        </em>
        in the
        <em>
            Object Library
        </em>
        and drag it onto view, to the left of the wrapping label. Feel free to
        resize the app window if necessary.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/imagewell-add.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/imagewell-add-650x468.png"
            alt="imagewell-add" width="650" height="468" class="aligncenter size-large wp-image-153223"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/imagewell-add-650x468.png 650w, https://koenig-media.raywenderlich.com/uploads/2017/01/imagewell-add-445x320.png 445w, https://koenig-media.raywenderlich.com/uploads/2017/01/imagewell-add.png 1467w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Create a new outlet for the image view in the same way you’ve done for
        all the previous controls:
        <em>
            Ctrl-Drag
        </em>
        the image view to the
        <em>
            ViewController.swift
        </em>
        file, and in the popup window name the property
        <em>
            imageView
        </em>
        .
    </p>
    <p>
        Build and run. Your app should now look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-uifinished.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-uifinished-247x320.png"
            alt="buildrun-uifinished" width="247" height="320" class="aligncenter size-medium wp-image-153224"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-uifinished-247x320.png 247w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-uifinished-386x500.png 386w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-uifinished.png 672w"
            sizes="(max-width: 247px) 100vw, 247px">
        </a>
    </p>
    <p>
        Phew! Your user interface is finally finished — the only thing that’s
        left to do is to create the code that will assemble your hilarious sentence
        and populate the image view that you added above!
    </p>
    <h2>
        Time To Make It Work
    </h2>
    <p>
        Now you need to construct the sentence based on those inputs.
    </p>
    <p>
        When the user clicks the
        <em>
            Go!
        </em>
        button, you’ll collect all the values from the different controls and
        combine them to construct the full sentence, and then display that sentence
        in the wrapping label you added previously.
    </p>
    <p>
        Then, to spice up your all-text interface, you will display a picture
        in the image view that you added in the last section.
    </p>
    <p>
        Download the
        <a href="http://www.raywenderlich.com/downloads/MadLibs_face.zip">
            resources file
        </a>
        for this project (normally goes into your
        <em>
            Download
        </em>
        folder). If the downloaded zip file was not unzipped automatically, unzip
        it to get the
        <em>
            face.png
        </em>
        image file. Select
        <em>
            Assets.xcassets
        </em>
        in the
        <em>
            Project Navigator
        </em>
        , and drag the image file into the assets list.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/12/assets.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/12/assets-650x266.png"
            alt="assets" width="650" height="266" class="aligncenter size-large wp-image-150272"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/12/assets-650x266.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/12/assets-480x196.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/12/assets.png 1580w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        It’s finally time to add the core of the application — the code which
        constructs the Mad Lib sentence!
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add the following property inside the class implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929714">
                    <td class="code" id="p149297code14">
                        <pre class="swift" style="font-family:monospace;">
                            fileprivate var selectedPlace: String { var place = "home" if rwDevConRadioButton.state
                            == NSOnState { place = "RWDevCon" } else if threeSixtyRadioButton.state
                            == NSOnState { place = "360iDev" } else if wwdcRadioButton.state == NSOnState
                            { place = "WWDC" } return place }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This code adds a computed property that returns the name of the place
        based on which radio button is selected.
    </p>
    <p>
        Now, replace all the code inside
        <code>
            goButtonClicked()
        </code>
        with this:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14929715">
                    <td class="code" id="p149297code15">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 let pastTenseVerb = pastTenseVerbTextField.stringValue &nbsp; //
                            2 let singularNoun = singularNounCombo.stringValue &nbsp; // 3 let amount
                            = amountSlider.integerValue &nbsp; // 4 let pluralNoun = pluralNouns[pluralNounPopup.indexOfSelectedItem]
                            &nbsp; // 5 let phrase = phraseTextView.string ?? "" &nbsp; // 6 let dateFormatter
                            = DateFormatter() dateFormatter.dateStyle = .long let date = dateFormatter.string(from:
                            datePicker.dateValue) &nbsp; // 7 var voice = "said" if yellCheck.state
                            == NSOnState { voice = "yelled" } &nbsp; // 8 let sentence = "On \(date),
                            at \(selectedPlace) a \(singularNoun) \(pastTenseVerb) \(amount) \(pluralNoun)
                            and \(voice), \(phrase)" &nbsp; // 9 resultTextField.stringValue = sentence
                            imageView.image = NSImage(named: "face") &nbsp; // 10 let selectedSegment
                            = voiceSegmentedControl.selectedSegment let voiceRate = VoiceRate(rawValue:
                            selectedSegment) ?? .normal readSentence(sentence, rate: voiceRate)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        That may seem like a lot of code, but it’s fairly straightforward when
        you break it down:
    </p>
    <ol>
        <li>
            Here you’re getting the text from
            <code>
                pastTenseVerbTextField
            </code>
        </li>
        <li>
            In this section of code, you get the string from the combo box by calling
            its
            <code>
                stringValue
            </code>
            property. You might ask why you don’t just look up the selected row, and
            then retrieve the string associated with that row. Quite simply, it’s because
            the user can enter their own text into the combo box. So use the
            <code>
                stringValue
            </code>
            to get the current string, which could have been either selected or typed.
        </li>
        <li>
            Next, read the slider’s current value using its
            <code>
                integerValue
            </code>
            method. Remember that if you need more precision with this control, you
            could also use
            <code>
                floatValue
            </code>
            or
            <code>
                doubleValue
            </code>
            .
        </li>
        <li>
            Here you get the plural noun, selected from the popup button. How is this
            done? Look up the appropriate plural noun in your
            <code>
                pluralNouns
            </code>
            array using array subscript syntax and getting the
            <code>
                indexOfSelectedItem
            </code>
            property.
        </li>
        <li>
            Next up is the phrase the user typed. To acquire it, simply retrieve the
            string value of our text view by getting its
            <code>
                string
            </code>
            property. Again, you’re using nil coalescing since the property is an
            optional and could be
            <code>
                nil
            </code>
            .
        </li>
        <li>
            To get the date, call the date picker’s
            <code>
                dateValue
            </code>
            method. Then, convert the returned date to a human-readable string using
            an
            <a href="http://developer.apple.com/library/mac/#documentation/Cocoa/Reference/Foundation/Classes/NSDateFormatter_Class/Reference/Reference.html"
            title="NSDateFormatter">
                NSDateFormatter
            </a>
            .
        </li>
        <li>
            Should you speak or shout? Simply get the checkbox state: if it’s
            <code>
                NSOnState
            </code>
            , assign
            <em>
                yelled
            </em>
            to the string variable. Otherwise, leave it as the default
            <em>
                said
            </em>
            .
        </li>
        <li>
            At this point, you’ve collected all the information you need to construct
            the mad lib sentence! This is where the magic happens. The results constant
            uses string interpolation, and the different values read from the controls
            to build a string, based on the user’s input.
        </li>
        <li>
            Now you can display the results of all your hard work! First, display
            the sentence in the results label by setting its
            <code>
                stringValue
            </code>
            property. Then, add some pizazz to the app by displaying an image to the
            user, which is as easy as loading the image and setting the property of
            the image view control.
        </li>
        <li>
            And finally, say it out loud! Get the voice speed based on the currently
            selected segment, and call the method that converts the text to speech
        </li>
    </ol>
    <p>
        That’s it! You’re done! Build and run the app, so you can construct some
        hilarious sentences for yourself!
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-final.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-final-247x320.png"
            alt="buildrun-final" width="247" height="320" class="aligncenter size-medium wp-image-153225"
            srcset="https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-final-247x320.png 247w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-final-386x500.png 386w, https://koenig-media.raywenderlich.com/uploads/2017/01/buildrun-final.png 672w"
            sizes="(max-width: 247px) 100vw, 247px">
        </a>
    </p>
    <p>
        Congratulations — you’ve finished building the Mad Libs application, and
        have learned a ton about the most common macOS controls along the way.
    </p>
    <p>
        Feel free to play with the controls, select different values, type funny
        nouns or verbs and see the results each time you click the
        <em>
            Go!
        </em>
        button, and see what funny stories you can create! :]
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
        Here is the
        <a href="https://koenig-media.raywenderlich.com/uploads/2017/01/MadLibs-part2-final-1.zip">
            final project
        </a>
        containing all the code from this tutorial.
    </p>
    <p>
        In order to gain a deeper understanding of the controls provided by macOS,
        I recommend you have a read through the different programming guides available
        from Apple listed below, which contain a wealth of information about how
        to use the available controls.
    </p>
    <p>
        In particular, I highly recommend you read the
        <a href="https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/OSXHIGuidelines/"
        title="macOS Human Interface Guidelines">
            macOS Human Interface Guidelines
        </a>
        . This guide explains the concepts and theories of user interfaces on
        macOS, and Apple’s expectations of how developers should use the controls
        and design their UI’s to provide a consistent and pleasurable experience.
        It’s essential reading for anyone intending to develop for the Mac platform,
        especially if they plan to distribute their applications via the Mac App
        Store.
    </p>
    <p>
        Here are some useful links to reinforce or further explore the concepts
        you’ve learned in this tutorial:
    </p>
    <ul>
        <li>
            <a href="https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/OSXHIGuidelines/"
            title="macOS Human Interface Guidelines" target="_blank">
                macOS Human Interface Guidelines
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/Button/Button.html#//apple_ref/doc/uid/10000019i"
            title="Button Programming Topics" target="_blank">
                Button Programming Topics
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/AttributedStrings/AttributedStrings.html"
            title="Attributed String Programming Guide" target="_blank">
                Attributed String Programming Guide
            </a>
        </li>
        <li>
            <a href="http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/ComboBox/ComboBox.html#//apple_ref/doc/uid/10000020i"
            title="Combobox Guide" target="_blank">
                Combo Box Programming Topics
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/SegmentedControl/Articles/SegmentedControlBasics.html"
            title="Segmented Control Guide" target="_blank">
                Segmented control Programming Topics
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/MenuList/MenuList.html#//apple_ref/doc/uid/10000032i"
            title="Application Menu and Popup Programming Topics" target="_blank">
                Application Menu and PopUp Programming Topics
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/mac/documentation/GraphicsImaging/Conceptual/ImageKitProgrammingGuide/Introduction/Introduction.html"
            title="Image Kit Programming Guide" target="_blank">
                Image Kit Programming Guide
            </a>
        </li>
    </ul>
</div>
