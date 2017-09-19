# 在macOS中怎样使用NSTouchBar

#### [原文地址](https://www.raywenderlich.com/147118/use-nstouchbar-macos) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <img class="wp-image-147148 size-full alignright" src="https://koenig-media.raywenderlich.com/uploads/2016/10/NSTouchBar-feature-500x500.png"
        alt="" width="250" height="250" srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/NSTouchBar-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/10/NSTouchBar-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/10/NSTouchBar-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/10/NSTouchBar-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/10/NSTouchBar-feature-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2016/10/NSTouchBar-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/10/NSTouchBar-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/10/NSTouchBar-feature-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
        After years of waiting and rumors, Apple finally released a set of new
        MacBook Pros. One of the new exciting things announced was the inclusion
        of a touch screen. Well… sort of.
    </p>
    <p>
        The new Touch Bar replaces the traditional function keys found on all
        MacBooks in the past for a dynamic, multi-touch screen. And the best part
        is it’s fully open to developers, so you can use it to offer new ways to
        interact with your macOS applications.
    </p>
    <p>
        If you’re a macOS developer, you’ll want to take full advantage of this
        new technology right away. In this tutorial, I’ll show you how you can
        use the new
        <code>
            NSTouchBar
        </code>
        API to easily create a dynamic touch bar for your macOS app.
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            This tutorial requires Xcode version 8.1 or later. You will also need
            to ensure that you have macOS 10.12.1, build 16B2657 installed on your
            computer first. If you do not have this version, you will not be able to
            show the Touch Bar Simulator. To check, go to
            <em>
                 &gt; About This Mac
            </em>
            , and click where you see 10.12.1. This will then show your build number.
        </p>
        <p>
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/About-Mac.png"
            alt="About Mac" width="588" height="140" class="alignnone size-full wp-image-147122"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/About-Mac.png 588w, https://koenig-media.raywenderlich.com/uploads/2016/10/About-Mac-480x114.png 480w"
            sizes="(max-width: 588px) 100vw, 588px">
        </p>
        <p>
            If you do not see 16B2657, you can download the update from
            <a href="https://support.apple.com/kb/dl1897" target="_blank" sl-processed="1">
                Apple
            </a>
            .
        </p>
    </div>
    <h2>
        What is the Touch Bar?
    </h2>
    <p>
        As mentioned, the Touch Bar is a small touch screen that allows users
        to interact with apps (and their computer) in a whole new way.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/Screen-Shot-2016-10-31-at-12.44.31-PM-650x106.png"
        alt="Screen Shot 2016-10-31 at 12.44.31 PM" width="650" height="106" class="alignnone size-large wp-image-147140"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/Screen-Shot-2016-10-31-at-12.44.31-PM-650x106.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/Screen-Shot-2016-10-31-at-12.44.31-PM-480x78.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/10/Screen-Shot-2016-10-31-at-12.44.31-PM.png 1132w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        There are three default sections on the Touch Bar:
    </p>
    <ul>
        <li>
            <em>
                System Button
            </em>
            : Depending on context, this will show a system level button, like Esc.
        </li>
        <li>
            <em>
                App Region
            </em>
            : The default area provided for your app to show items.
        </li>
        <li>
            <em>
                Control Strip
            </em>
            : This is a replacement of your familiar keys that you’d use to control
            screen brightness, volume, or music playback.
        </li>
    </ul>
    <p>
        As with every new technology from Apple, there are a set of Human Interface
        Guidelines that you should follow when working with the Touch Bar. You
        should familiarize yourself with them
        <a href="https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/OSXHIGuidelines/AbouttheTouchBar.html"
        sl-processed="1">
            here
        </a>
        , as they are very important to maintaining a consistent pattern to your
        users.
    </p>
    <p>
        Very briefly, here are a few sections of the guide that really stand out:
    </p>
    <ul>
        <li>
            <em>
                Don’t expose functionality just in the Touch Bar
            </em>
            : This isn’t the place to keep things secret from users that haven’t upgraded
            their hardware yet. If you’re going to put it in the Touch Bar, make sure
            you can perform the action somewhere else in your app. Apple says that
            the Touch Bar can even be disabled, so don’t count on your users to always
            see it.
        </li>
        <li>
            <em>
                The Touch Pad is an extension of the Keyboard and Trackpad, not a display
            </em>
            : Yes, it’s a screen, but it’s not a secondary display. Don’t distract
            the user with scrolling content or alerts.
        </li>
        <li>
            <em>
                Respond Immediately
            </em>
            : When users tap a key on the keyboard, they expect immediate results.
            Similarly, when someone taps a virtual button on the touch bar, they also
            expect immediate results.
        </li>
    </ul>
    <h2>
        How Do I Support the Touch Bar?
    </h2>
    <p>
        To add support for the TouchBar in your apps, you use some new classes
        provided by Apple:
        <code>
            NSTouchBar
        </code>
        and
        <code>
            NSTouchBarItem
        </code>
        (and its subclasses).
    </p>
    <p>
        Some of the
        <code>
            NSTouchBarItem
        </code>
        subclasses include features like:
    </p>
    <ul>
        <li>
            <em>
                Slider
            </em>
            : Adjusts a value
        </li>
        <li>
            <em>
                Popover
            </em>
            : Hide more functionality behind another item.
        </li>
        <li>
            <em>
                Color Picker
            </em>
            : Pretty much says it all (a color picker if you didn’t catch it ;] ).
        </li>
        <li>
            <em>
                Custom
            </em>
            : This is probably going to be your go-to item for a lot of things. It
            allows you to add simple labels, buttons, and all sorts of other controls.
        </li>
    </ul>
    <p>
        You can customize your items quite a bit. From text size and color, to
        images, you can offer your users a modern approach to the keyboard that
        hasn’t been available before. Just remember the guidelines, and you should
        be good to go.
    </p>
    <h2>
        Getting Started
    </h2>
    <p>
        You’re probably ready to get started! To follow along, download this sample
        project
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/TouchBar-Starter-2.zip"
        sl-processed="1">
            here
        </a>
        .
    </p>
    <p>
        The application is a very simple Travel Log, that only does what is needed
        for the purposes of our tutorial. With the project open, go to
        <em>
            Window &gt; Show Touch Bar
        </em>
        . You’ll now see the Touch Bar Simulator on your screen.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/Initial-Bar-650x36.png"
        alt="Initial Bar" width="650" height="36" class="alignnone size-large wp-image-147125"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/Initial-Bar-650x36.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/Initial-Bar-480x27.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/10/Initial-Bar.png 1096w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        Build and run the app, you’ll notice the Touch Bar is empty, aside from
        the System Button and Control Strip.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/Starter-App.png"
        alt="Starter App" width="593" height="317" class="alignnone size-full wp-image-147128"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/Starter-App.png 593w, https://koenig-media.raywenderlich.com/uploads/2016/10/Starter-App-480x257.png 480w"
        sizes="(max-width: 593px) 100vw, 593px">
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/First-Bar-1-650x36.png"
        alt="First Bar" width="650" height="36" class="alignnone size-large wp-image-147127"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/First-Bar-1-650x36.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/First-Bar-1-480x26.png 480w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <p>
        Before you can add anything to the Touch Bar, you’ll need to tell the
        system your application can customize the Touch Bar. Open
        <em>
            AppDelegate.swift
        </em>
        , and paste the following into
        <code>
            applicationDidFinishLaunching(\_:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1471181">
                    <td class="code" id="p147118code1">
                        <pre class="swift" style="font-family:monospace;">
                            func applicationDidFinishLaunching(_ aNotification: Notification) { if
                            #available(OSX 10.12.1, *) { NSApplication.shared().isAutomaticCustomizeTouchBarMenuItemEnabled
                            = true } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This takes care of all the necessary validations and activation of your
        Touch Bar menu items for you. At the time of this writing the current version
        of Xcode does not have macOS 10.12.1 available as a deployment target,
        so you will need to place
        <code>
            #available(OS X 10.12.1, *)
        </code>
        around code or extensions dealing with the Touch Bar. Luckily, Xcode will
        give you a friendly error if you forget ;]
    </p>
    <p>
        Open
        <em>
            WindowController.swift
        </em>
        , and look at
        <code>
            makeTouchBar()
        </code>
        . This method is checking if
        <code>
            ViewController
        </code>
        has a Touch Bar that can be returned. If so, it will send that Touch Bar
        to the
        <em>
            Window
        </em>
        , and be presented to the user. Right now, there is no Touch Bar being
        created, so nothing is shown.
    </p>
    <p>
        Before you can go making your own touch bars, and touch bar items, you
        need to be aware that instances of these classes all require unique identifiers.
        Open
        <em>
            TouchBarIdentifiers.swift
        </em>
        to see how these have been created for this project. There are extensions
        for both
        <code>
            NSTouchBarCustomizationIdentifier
        </code>
        , and
        <code>
            NSTouchBarItemIdentifier
        </code>
        .
    </p>
    <p>
        Go to
        <em>
            ViewController.swift
        </em>
        , and add the following at the end of the file, where the
        <em>
            TouchBar Delegate
        </em>
        is marked:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1471182">
                    <td class="code" id="p147118code2">
                        <pre class="swift" style="font-family:monospace;">
                            @available(OSX 10.12.1, *) extension ViewController: NSTouchBarDelegate
                            { override func makeTouchBar() -&gt; NSTouchBar? { // 1 let touchBar =
                            NSTouchBar() touchBar.delegate = self // 2 touchBar.customizationIdentifier
                            = .travelBar // 3 touchBar.defaultItemIdentifiers = [.infoLabelItem] //
                            4 touchBar.customizationAllowedItemIdentifiers = [.infoLabelItem] return
                            touchBar } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here, you override
        <code>
            makeTouchBar()
        </code>
        , which is required for your view or window to create a touch bar. You
        also did the following:
    </p>
    <ol>
        <li>
            Create a new
            <code>
                TouchBar
            </code>
            and set the delegate.
        </li>
        <li>
            Set the customizationIdentifier. Remember, every
            <code>
                TouchBar
            </code>
            and
            <code>
                TouchBarItem
            </code>
            need to have unique identifiers.
        </li>
        <li>
            Set the Touch Bar’s default item identifiers. This tells the Touch Bar
            what items it will contain.
        </li>
        <li>
            Here, you set what order the items should be presented to the user.
        </li>
    </ol>
    <p>
        You’re still not quite ready to see anything in your Touch Bar yet. You’ll
        need to tell the Touch Bar what the
        <code>
            .infoLabelItem
        </code>
        should look like. In the same extension, add the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1471183">
                    <td class="code" id="p147118code3">
                        <pre class="swift" style="font-family:monospace;">
                            func touchBar(_ touchBar: NSTouchBar, makeItemForIdentifier identifier:
                            NSTouchBarItemIdentifier) -&gt; NSTouchBarItem? { switch identifier { case
                            NSTouchBarItemIdentifier.infoLabelItem: let customViewItem = NSCustomTouchBarItem(identifier:
                            identifier) customViewItem.view = NSTextField(labelWithString: "\u{1F30E}
                            \u{1F4D3}") return customViewItem default: return nil } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        By implementing
        <code>
            touchBar(\_:makeItemForIdentifier:)
        </code>
        , you can customize your touch bar items anyway you’d like. Here, you’ve
        created a simple
        <code>
            NSCustomTouchBarItem
        </code>
        , and set its
        <code>
            view
        </code>
        to an
        <code>
            NSTextField
        </code>
        . Build and run your application, and you’ll now see the Touch Bar has
        a new item.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/First-Item--650x35.png"
        alt="TouchBar FirstItem" width="650" height="35" class="alignnone size-large wp-image-147158">
    </p>
    <p>
        Yay! You got a… label. That’s not super helpful, though. It’s time to
        add some controls.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/touchbar_ragecomic-650x480.png"
        alt="touchbar_ragecomic" width="650" height="480" class="alignnone size-large wp-image-147142"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/touchbar_ragecomic-650x480.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/touchbar_ragecomic-433x320.png 433w, https://koenig-media.raywenderlich.com/uploads/2016/10/touchbar_ragecomic.png 651w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <h2>
        Text Fields and Scrubbers
    </h2>
    <p>
        In
        <code>
            makeTouchBar()
        </code>
        , change the
        <code>
            defaultItemIdentifiers
        </code>
        to the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1471184">
                    <td class="code" id="p147118code4">
                        <pre class="swift" style="font-family:monospace;">
                            touchBar.defaultItemIdentifiers = [.infoLabelItem, .flexibleSpace, .ratingLabel,
                            .ratingScrubber]
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This will allow the Touch Bar to show three new items: a label and a scrubber.
        You’ve also added a
        <code>
            .flexibleSpace
        </code>
        . This is a dynamically sized space put in the Touch Bar to keeps things
        grouped together nicely. You can also take advantage of
        <code>
            .fixedSpaceSmall
        </code>
        , and
        <code>
            .fixedSpaceLarge
        </code>
        for more static sized spacing.
    </p>
    <p>
        You’ll still need to customize these items, just like the label you added.
        Add the following
        <code>
            cases
        </code>
        to the
        <code>
            switch
        </code>
        in
        <code>
            touchBar(\_:makeItemForIdentifier:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1471185">
                    <td class="code" id="p147118code5">
                        <pre class="swift" style="font-family:monospace;">
                            case NSTouchBarItemIdentifier.ratingLabel: // 1 let customViewItem = NSCustomTouchBarItem(identifier:
                            identifier) customViewItem.view = NSTextField(labelWithString: "Rating")
                            return customViewItem case NSTouchBarItemIdentifier.ratingScrubber: //
                            2 let scrubberItem = NSCustomTouchBarItem(identifier: identifier) let scrubber
                            = NSScrubber() scrubber.scrubberLayout = NSScrubberFlowLayout() scrubber.register(NSScrubberTextItemView.self,
                            forItemIdentifier: "RatingScrubberItemIdentifier") scrubber.mode = .fixed
                            scrubber.selectionBackgroundStyle = .roundedBackground scrubber.delegate
                            = self scrubber.dataSource = self scrubberItem.view = scrubber scrubber.bind("selectedIndex",
                            to: self, withKeyPath: #keyPath(rating), options: nil) return scrubberItem
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Step by step:
    </p>
    <ol>
        <li>
            A new item was created to show a label for ratings.
        </li>
        <li>
            Here, a custom item is created to hold an
            <code>
                NSScrubber
            </code>
            . This is a new control introduced for the Touch Bar. They behave similar
            to a slider, but can be customized specifically for working in the bar.
            Since scrubbers require a delegate to handle events, all you need to do
            here is set the
            <code>
                delegate
            </code>
            , which
            <em>
                ViewController
            </em>
            already has implemented for you.
        </li>
    </ol>
    <p>
        Build and run, and you’ll now see two new items in your Touch Bar. Notice
        that when you select an item from the scrubber, it will adjust the value
        in the app’s window.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/Rating-Items-650x35.png"
        alt="Rating Items" width="650" height="35" class="alignnone size-large wp-image-147132"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/Rating-Items-650x35.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/Rating-Items-480x26.png 480w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <h2>
        Segmented Controls
    </h2>
    <p>
        Next, you’re going to add a segmented control to the application. Since
        this doesn’t work using the delegate pattern, you’ll get a chance to see
        how to set up a
        <em>
            Target-Action
        </em>
        within the Touch Bar. Back in
        <code>
            makeTouchBar()
        </code>
        , you’ll need to add the last three items to
        <code>
            defaultItemIdentifiers
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1471186">
                    <td class="code" id="p147118code6">
                        <pre class="swift" style="font-family:monospace;">
                            touchBar.defaultItemIdentifiers = [.infoLabelItem, .flexibleSpace, .ratingLabel,
                            .ratingScrubber, .flexibleSpace, .visitedLabelItem, .visitedItem, .visitSegmentedItem]
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        And add the last three
        <code>
            cases
        </code>
        to
        <code>
            touchBar(\_:makeItemForIdentifier:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1471187">
                    <td class="code" id="p147118code7">
                        <pre class="swift" style="font-family:monospace;">
                            case NSTouchBarItemIdentifier.visitedLabelItem: // 1 let customViewItem
                            = NSCustomTouchBarItem(identifier: identifier) customViewItem.view = NSTextField(labelWithString:
                            "Times Visited") return customViewItem case NSTouchBarItemIdentifier.visitedItem:
                            // 2 let customViewItem = NSCustomTouchBarItem(identifier: identifier)
                            customViewItem.view = NSTextField(labelWithString: "--") customViewItem.view.bind("value",
                            to: self, withKeyPath: #keyPath(visited), options: nil) return customViewItem
                            case NSTouchBarItemIdentifier.visitSegmentedItem: // 3 let customActionItem
                            = NSCustomTouchBarItem(identifier: identifier) let segmentedControl = NSSegmentedControl(images:
                            [NSImage(named: NSImageNameRemoveTemplate)!, NSImage(named: NSImageNameAddTemplate)!],
                            trackingMode: .momentary, target: self, action: #selector(changevisitedAmount(\_:)))
                            segmentedControl.setWidth(40, forSegment: 0) segmentedControl.setWidth(40,
                            forSegment: 1) customActionItem.view = segmentedControl return customActionItem
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        For each step:
    </p>
    <ol>
        <li>
            This creates a simple label, just like in previous steps.
        </li>
        <li>
            Here, you create another label, but you
            <em>
                bind
            </em>
            the value of the text to a property. Just like the scrubber, binding values
            to make updating Touch Bar items very easy.
        </li>
        <li>
            Finally, you create a segmented control to be displayed in a touch bar
            item. You can see that setting up a target and action is just the same
            as it always is.
        </li>
    </ol>
    <p>
        Build and run, and you’ll see that you can interact with not only the
        scrubber, but the segmented control as well. Not only that, values changed
        in the Touch Bar are reflected in the window, and vice-versa.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/Final-Touch-Bar-650x279.png"
        alt="Final Touch Bar" width="650" height="279" class="alignnone size-large wp-image-147136"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/Final-Touch-Bar-650x279.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/Final-Touch-Bar-480x206.png 480w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <h2>
        Colored Buttons
    </h2>
    <p>
        Finally, it would be nice to give the user a chance to save using the
        Touch Bar. Since this button has a different outcome from the others, you’ll
        take advantage of the new
        <code>
            bezelColor
        </code>
        property of
        <code>
            NSButton
        </code>
        to give it some color.
    </p>
    <p>
        To do this, open
        <em>
            TouchBarIdentifiers.swift
        </em>
        , and in the
        <code>
            NSTouchBarItemIdentifier
        </code>
        extension, add the following to the end:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1471188">
                    <td class="code" id="p147118code8">
                        <pre class="swift" style="font-family:monospace;">
                            static let saveItem = NSTouchBarItemIdentifier("com.razeware.SaveItem")
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This creates a new identifier from scratch, which will allow you to add
        a new button to the Touch Bar.
    </p>
    <p>
        Go back to
        <em>
            ViewController.swift
        </em>
        , and add a new
        <code>
            .flexSpace
        </code>
        and
        <code>
            .saveItem
        </code>
        to the touch bar’s
        <code>
            defaultItemIdentifiers
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1471189">
                    <td class="code" id="p147118code9">
                        <pre class="swift" style="font-family:monospace;">
                            touchBar.defaultItemIdentifiers = [.infoLabelItem, .flexibleSpace, .ratingLabel,
                            .ratingScrubber, .flexibleSpace, .visitedLabelItem, .visitedItem, .visitSegmentedItem,
                            .flexibleSpace, .saveItem]
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        You’re almost done – all you have left is to handle configuring the new
        item. In
        <code>
            touchBar(\_:makeItemForIdentifier:)
        </code>
        , add a final
        <code>
            case
        </code>
        before
        <code>
            default
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14711810">
                    <td class="code" id="p147118code10">
                        <pre class="swift" style="font-family:monospace;">
                            case NSTouchBarItemIdentifier.saveItem: let saveItem = NSCustomTouchBarItem(identifier:
                            identifier) let button = NSButton(title: "Save", target: self, action:
                            #selector(save(\_:))) button.bezelColor = NSColor(red:0.35, green:0.61,
                            blue:0.35, alpha:1.00) saveItem.view = button return saveItem
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Everything here should look pretty familiar to this point. All that is
        new is setting the
        <code>
            bezelColor
        </code>
        to a familiar green :].
    </p>
    <p>
        Build and run, and you’ll see that you have a nice green button, and it
        has the same behavior as the
        <em>
            Save
        </em>
        button in the window.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/Screen-Shot-2016-10-31-at-5.33.58-PM-2-650x260.png"
        alt="Screen Shot 2016-10-31 at 5.33.58 PM (2)" width="650" height="260"
        class="alignnone size-large wp-image-147175" srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/Screen-Shot-2016-10-31-at-5.33.58-PM-2-650x260.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/Screen-Shot-2016-10-31-at-5.33.58-PM-2-480x192.png 480w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <h2>
        Where To Go From Here?
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
        You can download the final sample project
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/TouchBar-Final-3.zip"
        sl-processed="1">
            here
        </a>
        .
    </p>
    <p>
        That’s it for learning the basics of the Touch Bar. It should be pretty
        clear Apple wanted to make this easy for you to get started to quickly
        make these features available to your users.
    </p>
    <p>
        In this tutorial, you learned the following:
    </p>
    <ol>
        <li>
            How to setup your app to show a Touch Bar
        </li>
        <li>
            How to present static labels in a Touch Bar
        </li>
        <li>
            How to add dynamic labels in a Touch Bar using binding
        </li>
        <li>
            How to add controls to a Touch Bar, and handle their events
        </li>
    </ol>
    <p>
        Don’t stop with these examples! There are plenty of exciting features
        to be found within
        <code>
            NSTouchBar
        </code>
        and
        <code>
            NSTouchBarItem
        </code>
        . Try adding a popover to your Touch Bar, or see how easy it is to format
        text in your app. You can also check out creating Touch Bars in Interface
        Builder.
    </p>
    <p>
        If you have any questions, comments, or want to just want to rave (or
        complain) about the new MacBook Pro, please join the forum discussion below!
    </p>
</div>