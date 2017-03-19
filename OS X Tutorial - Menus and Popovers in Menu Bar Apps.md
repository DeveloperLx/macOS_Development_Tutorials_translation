# OS X教程：在Menu Bar App中的Menus和Popover

#### [原文地址](https://www.raywenderlich.com/98178/os-x-tutorial-menus-popovers-menu-bar-apps) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div id="attachment_105403" style="width: 260px" class="wp-caption alignright">
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/05/Popover.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/05/Popover.png"
            alt="Learn how to make a menu bar OS X app with a popover!" width="250"
            height="250" class="size-full wp-image-105403" srcset="https://koenig-media.raywenderlich.com/uploads/2015/05/Popover.png 250w, https://koenig-media.raywenderlich.com/uploads/2015/05/Popover-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/05/Popover-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2015/05/Popover-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2015/05/Popover-128x128.png 128w"
            sizes="(max-width: 250px) 100vw, 250px">
        </a>
        <p class="wp-caption-text">
            Learn how to make a menu bar OS X app with a popover!
        </p>
    </div>
    <p>
        Menu bar apps have been staple of OS X for along time. Many apps like
        <a href="https://agilebits.com/onepassword/mac" target="_blank" sl-processed="1">
            1Password
        </a>
        and
        <a href="http://dayoneapp.com" target="_blank" sl-processed="1">
            Day One
        </a>
        have companion menu bar apps. Others like
        <a href="http://flexibits.com/fantastical" target="_blank" sl-processed="1">
            Fantastical
        </a>
        live exclusively in OS X’s menu bar.
    </p>
    <p>
        In this tutorial, you’ll build a menu bar app that shows inspirational
        quotes in a popover. While you do this, you’ll learn:
    </p>
    <ul>
        <li>
            How to create a menu bar icon
        </li>
        <li>
            How to make the app live exclusively in the menu bar
        </li>
        <li>
            How to add a menu for the user
        </li>
        <li>
            How to make a popover that shows on demand and hides when the user moves
            on — aka Event Monitoring
        </li>
        <li>
            How to add essential UI
        </li>
    </ul>
    <div class="note">
        <em>
            Note:
        </em>
        This tutorial assumes you’re familiar with Swift and OS X. If you need
        a refresher, start with our
        <a href="http://www.raywenderlich.com/87002/getting-started-with-os-x-and-swift-tutorial-part-1"
        target="_blank" sl-processed="1">
            Getting Started With OS X and Swift
        </a>
        tutorial for a great introduction.
    </div>
    <h2>
        Getting Started
    </h2>
    <p>
        Fire up Xcode. Go to
        <em>
            File/New/Project…
        </em>
        then select the
        <em>
            OS X/Application/Cocoa Application
        </em>
        template and click
        <em>
            Next
        </em>
        .
    </p>
    <p>
        On the next screen, enter
        <em>
            Quotes
        </em>
        as the
        <em>
            Product Name
        </em>
        , choose your desired
        <em>
            Organization Name
        </em>
        and
        <em>
            Organization Identifier
        </em>
        . Then make sure that
        <em>
            Swift
        </em>
        is selected as the language, and uncheck
        <em>
            Use Storyboards
        </em>
        ,
        <em>
            Create Document-Based Application
        </em>
        and
        <em>
            Use Core Data
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/05/QuotesOptions.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/05/QuotesOptions-700x410.png"
            alt="QuotesOptions" width="600" height="410" class="aligncenter wp-image-105401 bordered">
        </a>
    </p>
    <p>
        Finally, click
        <em>
            Next
        </em>
        again, choose a place to save the project and click
        <em>
            Create
        </em>
        .
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        On iOS, and as of Yosemite, on OS X you will mostly be preferring to use
        storyboards. But in the case of this menu bar app, using a storyboard would
        have made it more complicated to have the app live exclusively in the menu
        bar. That’s why you will use xibs to build the user interface of the app.
    </div>
    <p>
        Once the new project is set up, open
        <em>
            AppDelegate.swift
        </em>
        and add the following property to the class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p981781">
                    <td class="code" id="p98178code1">
                        <pre class="swift" style="font-family:monospace;">
                            let statusItem = NSStatusBar.systemStatusBar().statusItemWithLength(-2)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This creates a
        <em>
            Status Item
        </em>
        — aka application icon — in the menu bar with a fixed length that the
        user will see and use.
    </p>
    <div class="note">
        <p>
            <em>
                Note
            </em>
            : At the time of writing, there is a bug in Xcode that prevents it from
            recognizing
            <code>
                NSSquareStatusItemLength
            </code>
            , but since it’s just a constant that’s defined as
            <code>
                -2
            </code>
            , you just use
            <code>
                -2
            </code>
            in it’s place.
        </p>
    </div>
    <p>
        Next, you’ll need to associate an image to the status item to make your
        app recognizable in the menu bar.
    </p>
    <p>
        Go to
        <code>
            Images.xcassets
        </code>
        . Then download this image
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/03/StatusBarButtonImage@2x.png"
        sl-processed="1">
            StatusBarButtonImage@2x.png
        </a>
        and drag it into the asset catalog.
    </p>
    <p>
        Select the image and open the attributes inspector. Set
        <em>
            Devices
        </em>
        to Device Specific, and then make sure the
        <em>
            Mac
        </em>
        option is checked. Change the
        <em>
            Render As
        </em>
        option to Template Image.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2015/04/StatusBarButtonImage-3.png"
        alt="StatusBarButtonImage-3" width="258" height="222" class="aligncenter size-full wp-image-103449 bordered">
    </p>
    <p>
        If you use your own custom image, make sure that the image is black and
        white and configured as a template image so the Status Item looks great
        against both light and dark menu bars.
    </p>
    <p>
        Back in
        <em>
            AppDelegate.swift
        </em>
        , add the following code to
        <code>
            applicationDidFinishLaunching(_:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p981782">
                    <td class="code" id="p98178code2">
                        <pre class="swift" style="font-family:monospace;">
                            if let button = statusItem.button { button.image = NSImage(named: "StatusBarButtonImage")
                            button.action = Selector("printQuote:") }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This will configure the status item with an icon of the image you just
        added, and an action for when you click on the item.
    </p>
    <p>
        Before you get to test the app, you’ll need to add that button action
        method. Add the following method to the class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p981783">
                    <td class="code" id="p98178code3">
                        <pre class="swift" style="font-family:monospace;">
                            func printQuote(sender: AnyObject) { let quoteText = "Never put off until
                            tomorrow what you can do the day after tomorrow." let quoteAuthor = "Mark
                            Twain" &nbsp; println("\(quoteText) — \(quoteAuthor)") }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This method will simply log out a nice Mark Twain quote to the console.
    </p>
    <p>
        Build and run the app, and you should see a new menu bar app available.
        You did it!
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2015/03/MenuBar-Light.png"
        width="600" class="aligncenter wp-image-98940">
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2015/03/MenuBar-Dark.png"
        width="600" class="aligncenter wp-image-98940">
    </p>
    <div class="note">
        <p>
            <em>
                Note
            </em>
            : If you have too many menu bar apps, you might not be able to see your
            button. Switch to an app with fewer menus than Xcode (like Finder) and
            you should be able to see it.
        </p>
    </div>
    <p>
        Every time you click on the menu bar icon, you’ll see the quote printed
        out in the Xcode console.
    </p>
    <h2>
        Hiding the Dock Icon and Main Window
    </h2>
    <p>
        There are still two small things to do before you have a functional menu
        bar app: hide the dock icon and kill off the main window.
    </p>
    <p>
        To disable the dock icon, open
        <em>
            Info.plist
        </em>
        . Add a new key
        <em>
            Application is agent (UIElement)
        </em>
        and set its value to
        <em>
            YES
        </em>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2015/03/Application-Is-Agent-YES.png"
        class="aligncenter wp-image-98940" width="650">
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        If you’re an expert plist editor, feel free to set this manually with
        the key
        <code>
            LSUIElement
        </code>
        .
    </div>
    <p>
        Now it’s time to handle the main window. Open
        <code>
            MainMenu.xib
        </code>
        and select the window object. Then, in the attributes inspector, set the
        window so it’s not visible at launch.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2015/03/Visible-at-Launch-NO1.png"
        width="600" class="aligncenter wp-image-98940">
    </p>
    <p>
        Build and run. You’ll see the app has no main window, no pesky dock icon
        and only a tidy status item in the menu bar!
    </p>
    <h2>
        Adding a Menu to the Status Item
    </h2>
    <p>
        Usually, a measly single action on click is not enough for a menu bar
        app. The easiest way to add more functionality to your app is to add a
        menu. Add the following code to the end of
        <code>
            applicationDidFinishLaunching(_:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p981784">
                    <td class="code" id="p98178code4">
                        <pre class="swift" style="font-family:monospace;">
                            let menu = NSMenu() &nbsp; menu.addItem(NSMenuItem(title: "Print Quote",
                            action: Selector("printQuote:"), keyEquivalent: "P")) menu.addItem(NSMenuItem.separatorItem())
                            menu.addItem(NSMenuItem(title: "Quit Quotes", action: Selector("terminate:"),
                            keyEquivalent: "q")) &nbsp; statusItem.menu = menu
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here you create an
        <code>
            NSMenu
        </code>
        , add multiple instances of
        <code>
            NSMenuItem
        </code>
        to it, and then set the status item’s menu to that new menu.
    </p>
    <p>
        A few things to note here:
    </p>
    <ul>
        <li>
            The title of a menu item is clear; it’s just the text that appears on
            the menu item.
        </li>
        <li>
            The action, like the action of a button or any control, is the method
            that gets called when you click the menu item.
        </li>
        <li>
            The
            <code>
                KeyEquivalent
            </code>
            is a keyboard shortcut that you can use to activate the menu item. A lowercase
            letter uses
            <em>
                Cmd
            </em>
            as the modifier key and an uppercase letter uses
            <em>
                Cmd+Shift
            </em>
            . This keyboard shortcut only works if the application is front-most and
            active. So, in this case, the menu or any other window needs to be visible,
            since the app has no dock icon.
        </li>
        <li>
            A
            <code>
                separatorItem
            </code>
            is an inactive menu item that appears as a simple gray line between other
            menu items. Use it to group functionality in the menu.
        </li>
        <li>
            The
            <code>
                printQuote:
            </code>
            action is the method you already defined in
            <code>
                AppDelegate
            </code>
            . On the other hand,
            <code>
                terminate:
            </code>
            is an action method defined in the shared application instance. Because
            you don’t implement it, the action gets sent up the responder chain until
            it arrives at the shared application, in which case the application quits.
        </li>
    </ul>
    <p>
        Build and run, and you should see a menu when clicking on the status item.
        Progress!
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2015/03/The-Menu.png"
        class="aligncenter wp-image-98940" width="600">
    </p>
    <p>
        Try out your options –&nbsp;selecting
        <em>
            Print Quote
        </em>
        will display the quote in the Xcode console, while
        <em>
            Quit Quotes
        </em>
        will quit the app.
    </p>
    <h2 id="addingapopovertothestatusitem">
        Adding a Popover to the Status Item
    </h2>
    <p>
        You’ve seen how easy it is to set up a menu from code, but showing the
        quote in the Xcode console won’t cut it for your end users. The next step
        is to replace the menu with a simple view controller to show a quote right
        in place.
    </p>
    <p>
        Go to
        <em>
            File/New/File…
        </em>
        , select the
        <em>
            OS X/Source/Cocoa Class
        </em>
        template and click
        <em>
            Next
        </em>
        .
    </p>
    <p>
        Name the class
        <code>
            QuotesViewController
        </code>
        , make it a subclass of
        <code>
            NSViewController
        </code>
        , check the option
        <em>
            Also create XIB file for user interface
        </em>
        , and set the language to
        <em>
            Swift
        </em>
        .
    </p>
    <p>
        Finally, click
        <em>
            Next
        </em>
        again, choose a place to save the file (In the
        <em>
            Quotes
        </em>
        subfolder of the project folder is a good place) and click
        <em>
            Create
        </em>
        .
    </p>
    <p>
        Now, leave the new files alone and go back to
        <em>
            AppDelegate.swift
        </em>
        . Start by adding a new property declaration to the class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p981785">
                    <td class="code" id="p98178code5">
                        <pre class="swift" style="font-family:monospace;">
                            let popover = NSPopover()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Next, replace
        <code>
            applicationDidFinishLaunching(_:)
        </code>
        with the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p981786">
                    <td class="code" id="p98178code6">
                        <pre class="swift" style="font-family:monospace;">
                            func applicationDidFinishLaunching(notification: NSNotification) { if
                            let button = statusItem.button { button.image = NSImage(named: "StatusBarButtonImage")
                            button.action = Selector("togglePopover:") } &nbsp; popover.contentViewController
                            = QuotesViewController(nibName: "QuotesViewController", bundle: nil) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        You’ve changed the button action to
        <code>
            togglePopover:
        </code>
        which you’ll implement next. Also, rather than set up a menu, you’re setting
        up the popover to show whatever’s in QuotesViewController.
    </p>
    <p>
        Finally, remove
        <code>
            printQuote()
        </code>
        , and add the following three methods in its place:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p981787">
                    <td class="code" id="p98178code7">
                        <pre class="swift" style="font-family:monospace;">
                            func showPopover(sender: AnyObject?) { if let button = statusItem.button
                            { popover.showRelativeToRect(button.bounds, ofView: button, preferredEdge:
                            NSMinYEdge) } } &nbsp; func closePopover(sender: AnyObject?) { popover.performClose(sender)
                            } &nbsp; func togglePopover(sender: AnyObject?) { if popover.shown { closePopover(sender)
                            } else { showPopover(sender) } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        <code>
            showPopover()
        </code>
        displays the popover to the user. Similar to popovers on iOS, you just
        need to supply a source rect and OS X will position the popover and arrow
        so it looks like it’s coming out of the menu bar icon.
    </p>
    <p>
        <code>
            closePopover()
        </code>
        simply closes the popover, and
        <code>
            togglePopover()
        </code>
        is the action method that will either open or close the popover depending
        on its current state.
    </p>
    <p>
        Build and run, and then click on the menu bar icon to check that it shows
        and then hides an empty popover.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2015/03/The-Popover.png"
        width="600" class="aligncenter wp-image-98940">
    </p>
    <p>
        Your popover works great, but where’s all the inspiration? All you see
        is an empty view and no quotes. Guess what you’ll fix next?
    </p>
    <h2>
        Implementing the Quote View Controller
    </h2>
    <p>
        First, you’ll need model to store the quotes and attributions. Go to
        <em>
            File/New/File…
        </em>
        and select the
        <em>
            OS X/Source/Swift File
        </em>
        template, then click
        <em>
            Next
        </em>
        . Name the file
        <em>
            Quote
        </em>
        and click
        <em>
            Create
        </em>
        .
    </p>
    <p>
        Open
        <em>
            Quote.swift
        </em>
        and add the following code to the file:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p981788">
                    <td class="code" id="p98178code8">
                        <pre class="swift" style="font-family:monospace;">
                            struct Quote { let text: String let author: String &nbsp; static let all:
                            [Quote] = [ Quote(text: "Never put off until tomorrow what you can do the
                            day after tomorrow.", author: "Mark Twain"), Quote(text: "Efficiency is
                            doing better what is already being done.", author: "Peter Drucker"), Quote(text:
                            "To infinity and beyond!", author: "Buzz Lightyear"), Quote(text: "May
                            the Force be with you.", author: "Han Solo"), Quote(text: "Simplicity is
                            the ultimate sophistication", author: "Leonardo da Vinci"), Quote(text:
                            "It’s not just what it looks like and feels like. Design is how it works.",
                            author: "Steve Jobs") ] } &nbsp; // MARK: - Printable &nbsp; extension
                            Quote: Printable { var description: String { return "\"\(text)\" — \(author)"
                            } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This defines a simple quote structure and a static property that returns
        all the quotes. Since you also make
        <code>
            Quote
        </code>
        conform to
        <code>
            Printable
        </code>
        , you can easily get a nice formatted string.
    </p>
    <p>
        You’re making progress, but you still need some more function in the UI.
        How about some wrapping and auto constraints to make it pretty?
    </p>
    <p>
        Open
        <code>
            QuotesViewController.xib
        </code>
        and drag two
        <em>
            bevel button
        </em>
        instances, a
        <em>
            label
        </em>
        and a
        <em>
            push button
        </em>
        into the custom view.
    </p>
    <p>
        Set the first bevel button’s image to
        <code>
            NSGoLeftTemplate
        </code>
        and the second button’s image to
        <code>
            NSGoRightTemplate
        </code>
        , set the label’s text alignment to Center and its line break mode to
        <em>
            Word Wrap
        </em>
        . Finally, set the title of the push button to
        <em>
            Quit Quotes
        </em>
        .
    </p>
    <p>
        Here’s what the final layout should look like:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2015/03/Quote-View-Controller-IB.png"
        width="600" class="aligncenter wp-image-98940">
    </p>
    <p>
        Can you add the auto layout constraints to make the user interface match?
        Give it a few good attempts before you open the spoiler below. If you get
        it right, skip the spoiler and give yourself a gold star.
    </p>
    <div class="easySpoilerWrapper" style="">
        <table class="easySpoilerTable" border="0" style="text-align:center;"
        align="center" bgcolor="FFFFFF">
            <tbody>
                <tr style="white-space:normal;">
                    <th class="easySpoilerTitleA" style="white-space:normal;font-weight:normal;text-align:left;vertical-align:middle;font-size:120%;color:#000000;">
                        Solution Inside
                    </th>
                    <th class="easySpoilerTitleB" style="text-align:right;vertical-align:middle;font-size:100%; white-space:nowrap;">
                        <a href="" onclick="wpSpoilerSelect(&quot;spoilerDiv1bdd8001&quot;); return false;"
                        class="easySpoilerButtonOther" style="font-size:100%;color:#000000;background-color:#fcfcfc;background-image:none;border: 1px inset;border-style:solid;border-color:#cccccc; margin: 3px 0px 3px; padding: 4px; "
                        align="right" sl-processed="1">
                            Select
                        </a>
                        <a href="" onclick="wpSpoilerToggle(&quot;spoilerDiv1bdd8001&quot;,true,&quot;Show&quot;,&quot;Hide&quot;,&quot;fast&quot;,false); return false;"
                        id="spoilerDiv1bdd8001_action" class="easySpoilerButton" value="Show" align="right"
                        style="font-size:100%;color:#000000;background-color:#fcfcfc;background-image:none;border: 1px inset;border-style:solid;border-color:#cccccc; margin: 3px 0px 3px 5px; padding: 4px;"
                        sl-processed="1">
                            Show
                        </a>
                    </th>
                </tr>
                <tr>
                    <td class="easySpoilerRow" colspan="2" style="">
                        <div id="spoilerDiv1bdd8001" class="easySpoilerSpoils" style="display:none; white-space:wrap; overflow:auto; vertical-align:middle;">
                            <br>
                            Here are the auto layout constraints you need to get the correct layout:
                            <p>
                            </p>
                            <ol>
                                <li>
                                    Pin the go-left and go-right buttons to the top and bottom, and give them
                                    a fixed width of 32. The go-left button should also be pinned to the leading
                                    edge, and the go-right should be pinned to the trailing edge.
                                </li>
                                <li>
                                    Place the label between the buttons and add trailing and leading space
                                    constraints. Set the label to be centered vertically as well.
                                </li>
                                <li>
                                    Pin the Quit button to the bottom, center it horizontally.
                                </li>
                            </ol>
                            <p>
                            </p>
                        </div>
                    </td>
                </tr>
            </tbody>
        </table>
        <div class="easySpoilerConclude" style="">
            <table class="easySpoilerTable" border="0" style="text-align:center;"
            frame="box" align="center" bgcolor="FFFFFF">
                <tbody>
                    <tr>
                        <th class="easySpoilerEnd" style="width:100%;">
                        </th>
                        <td class="easySpoilerEnd" style="white-space:nowrap;" colspan="2">
                        </td>
                    </tr>
                    <tr>
                        <td class="easySpoilerGroupWrapperLastRow" colspan="2" style="">
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
    <p>
        After you’ve perfected the constraints, select
        <em>
            Update Constraints
        </em>
        by selecting
        <em>
            Resolve Auto Layout Issues
        </em>
        in the bottom-right corner of the canvas.
    </p>
    <p>
        Now open
        <em>
            QuotesViewController.swift
        </em>
        and replace the file contents with the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p981789">
                    <td class="code" id="p98178code9">
                        <pre class="swift" style="font-family:monospace;">
                            import Cocoa &nbsp; class QuotesViewController: NSViewController { @IBOutlet
                            var textLabel: NSTextField! } &nbsp; // MARK: Actions &nbsp; extension
                            QuotesViewController { @IBAction func goLeft(sender: NSButton) { } &nbsp;
                            @IBAction func goRight(sender: NSButton) { } &nbsp; @IBAction func quit(sender:
                            NSButton) { } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This starter implementation is for a standard
        <code>
            NSViewController
        </code>
        instance. There’s one outlet for the text label, which you’ll need to
        update with the inspirational quote. The three actions are for the three
        buttons.
    </p>
    <p>
        Then go back to
        <em>
            QuotesViewController.xib
        </em>
        and connect the outlet to the text label by control-dragging from
        <em>
            File’s Owner
        </em>
        to the label. Connect the actions by contro-dragging from each button
        to
        <em>
            File’s Owner
        </em>
        .
    </p>
    <div class="note">
        <p>
            <em>
                Note
            </em>
            : If you have trouble with any of the above steps, refer to our library
            of
            <a href="http://www.raywenderlich.com/os-x-tutorials" target="_blank"
            title="OS X tutorials" sl-processed="1">
                OS X tutorials
            </a>
            , where you’ll find introductory tutorials that will walk you through
            many aspects of OS X development, including adding views/constraints in
            interface builder and connecting outlets and actions.
        </p>
    </div>
    <p>
        Stand up, stretch and maybe do a quick victory lap around your desk because
        you just flew through a bunch of interface builder work.
    </p>
    <p>
        Build and run, and your popover should look like this now:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2015/03/The-Popover-2.png"
        width="600" class="aligncenter wp-image-98940">
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        You used the default size of the view controller for the popover above.
        If you want a smaller or bigger popover, all you need to do is resize the
        view controller in the xib. Go for it!
    </div>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2015/05/Quote-View-Controller-IB-Small-480x290.png"
        class="aligncenter size-full wp-image-105504" srcset="https://koenig-media.raywenderlich.com/uploads/2015/05/Quote-View-Controller-IB-Small-480x290.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/05/Quote-View-Controller-IB-Small-700x423.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/05/Quote-View-Controller-IB-Small.png 710w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2015/05/The-Popover-2-Small-480x308.png"
        class="aligncenter size-full wp-image-105505" srcset="https://koenig-media.raywenderlich.com/uploads/2015/05/The-Popover-2-Small-480x308.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/05/The-Popover-2-Small.png 700w"
        sizes="(max-width: 480px) 100vw, 480px">
    </p>
    <p>
        The interface is finished, but you’re not done yet. Those buttons are
        waiting on you to know what to do when the user clicks them — don’t leave
        them hanging.
    </p>
    <p>
        Open
        <em>
            QuotesViewController.swift
        </em>
        and add the following properties to the class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p9817810">
                    <td class="code" id="p98178code10">
                        <pre class="swift" style="font-family:monospace;">
                            let quotes = Quote.all &nbsp; var currentQuoteIndex: Int = 0 { didSet
                            { updateQuote() } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The first property holds all the quotes, and the second holds the index
        of the current quote.
        <code>
            currentQuoteIndex
        </code>
        also has a property observer to update the text label string with the
        new quote when the index changes.
    </p>
    <p>
        Next, add the following methods to the class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p9817811">
                    <td class="code" id="p98178code11">
                        <pre class="swift" style="font-family:monospace;">
                            override func viewWillAppear() { super.viewWillAppear() &nbsp; currentQuoteIndex
                            = 0 } &nbsp; func updateQuote() { textLabel.stringValue = toString(quotes[currentQuoteIndex])
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        When the view appears, you set the current quote index to 0, which in
        turn updates the user interface.
        <code>
            updateQuote()
        </code>
        simply updates the text label to show whichever quote is currently selected
        according to
        <code>
            currentQuoteIndex
        </code>
        .
    </p>
    <p>
        To tie it all together, implement the three action methods as follows;
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p9817812">
                    <td class="code" id="p98178code12">
                        <pre class="swift" style="font-family:monospace;">
                            @IBAction func goLeft(sender: NSButton) { currentQuoteIndex = (currentQuoteIndex
                            - 1 + quotes.count) % quotes.count } &nbsp; @IBAction func goRight(sender:
                            NSButton) { currentQuoteIndex = (currentQuoteIndex + 1) % quotes.count
                            } &nbsp; @IBAction func quit(sender: NSButton) { NSApplication.sharedApplication().terminate(sender)
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        In
        <code>
            goLeft()
        </code>
        and
        <code>
            goRight()
        </code>
        , you cycle through the all the quotes and wrap around when you reach
        the ends of the array.
        <code>
            quit()
        </code>
        terminates the app as explained before.
    </p>
    <p>
        Build and run again, and
        <i>
            now
        </i>
        you can see all the quotes and quit the app!
    </p>
    <h2 id="eventmonitoring">
        Event Monitoring
    </h2>
    <p>
        There is one feature you’ll want in your unobtrusive, small menu bar app,
        and it’s when you click anywhere outside the app, the popover automatically
        closes.
    </p>
    <p>
        Menu bar apps should open the popover on click or hover, and then disappear
        once the user moves onto the next thing. For that, you need an OS X global
        event monitor.
    </p>
    <p>
        Here’s where you’ll take the concept to the next level. You’ll make the
        event monitor reusable in all your projects, and to keep the example app
        modular, you’ll define a Swift wrapper class and then use it when showing
        the popover.
    </p>
    <p>
        Bet you’re feeling smarter already!
    </p>
    <div id="attachment_92137" style="width: 157px" class="wp-caption aligncenter">
        <img src="https://koenig-media.raywenderlich.com/uploads/2014/12/victorious-e1419192669236.png"
        alt="I feel S-M-R-T!" width="147" height="300" class="size-full wp-image-92137">
        <p class="wp-caption-text">
            I feel S-M-R-T!
        </p>
    </div>
    <p>
        Create a new Swift File and name it
        <em>
            EventMonitor
        </em>
        , and then replace its contents with the following class definition:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p9817813">
                    <td class="code" id="p98178code13">
                        <pre class="swift" style="font-family:monospace;">
                            import Cocoa &nbsp; public class EventMonitor { private var monitor: AnyObject?
                            private let mask: NSEventMask private let handler: NSEvent? -&gt; () &nbsp;
                            public init(mask: NSEventMask, handler: NSEvent? -&gt; ()) { self.mask
                            = mask self.handler = handler } &nbsp; deinit { stop() } &nbsp; public
                            func start() { monitor = NSEvent.addGlobalMonitorForEventsMatchingMask(mask,
                            handler: handler) } &nbsp; public func stop() { if monitor != nil { NSEvent.removeMonitor(monitor!)
                            monitor = nil } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        You initialize an instance of this class by passing in a mask of events
        to listen for –&nbsp;things like key down, scroll wheel moved, left mouse
        button click, etc –&nbsp;and an event handler.
    </p>
    <p>
        When you’re ready to start listening,
        <code>
            start()
        </code>
        calls
        <code>
            addGlobalMonitorForEventsMatchingMask(_:handler:)
        </code>
        , which returns an object for you to hold on to. Any time the event specified
        in the mask occurs, the system calls your handler.
    </p>
    <p>
        To remove the global event monitor, you call
        <code>
            removeMonitor()
        </code>
        in
        <code>
            stop()
        </code>
        and delete the returned object by setting it to
        <code>
            nil
        </code>
        .
    </p>
    <p>
        All that’s left is calling
        <code>
            start()
        </code>
        and
        <code>
            stop()
        </code>
        when needed. How easy is that? The class also calls
        <code>
            stop()
        </code>
        for you in the deinitializer, to clean up after itself.
    </p>
    <p>
        Open
        <em>
            AppDelegate.swift
        </em>
        one last time, and add a new property declaration to the class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p9817814">
                    <td class="code" id="p98178code14">
                        <pre class="swift" style="font-family:monospace;">
                            var eventMonitor: EventMonitor?
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Next, add the code to configure the event monitor at the end of
        <code>
            applicationDidFinishLaunching(_:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p9817815">
                    <td class="code" id="p98178code15">
                        <pre class="swift" style="font-family:monospace;">
                            eventMonitor = EventMonitor(mask: .LeftMouseDownMask | .RightMouseDownMask)
                            { [unowned self] event in if self.popover.shown { self.closePopover(event)
                            } } eventMonitor?.start()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This notifies your app of any left or right mouse down event and closes
        the popover when the system event occurs. Note that your handler will not
        be called for events that are sent to your own application. That’s why
        the popover doesn’t close when you click around inside of it. :]
    </p>
    <p>
        Add the following code to the end of
        <code>
            showPopover(_:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p9817816">
                    <td class="code" id="p98178code16">
                        <pre class="swift" style="font-family:monospace;">
                            eventMonitor?.start()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This will start the event monitor when the popover appears.
    </p>
    <p>
        Then, you’ll need to add the following code to the end of
        <code>
            closePopover(_:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p9817817">
                    <td class="code" id="p98178code17">
                        <pre class="swift" style="font-family:monospace;">
                            eventMonitor?.stop()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This will stop the event monitor when the popover closes.
    </p>
    <p>
        All done! Build and run the app one more time. Click on the menu bar icon
        to show the popover, and then click anywhere else and the popover closes.
        Awesome!
    </p>
    <h2 id="wheretogofromhere">
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
        Here is the
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/04/Quotes-Final.zip"
        sl-processed="1">
            downloadable final project
        </a>
        with all of the code you’ve developed in the above tutorial.
    </p>
    <p>
        You’ve seen how to set up both menus and popovers in your menu bar status
        items –&nbsp;why not keep experimenting with showing a randomized quote,
        connecting to a web backend to pull new quotes, or even some kind of “pro”
        version to open the door to monetization?
    </p>
    <p>
        A good place to look for other possibilities is reading the official documentation
        for
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ApplicationKit/Classes/NSMenu_Class/index.html"
        target="_blank" sl-processed="1">
            <code>
                NSMenu
            </code>
        </a>
        ,
        <a href="https://developer.apple.com/library/mac/documentation/AppKit/Reference/NSPopover_Class/index.html"
        target="_blank" sl-processed="1">
            <code>
                NSPopover
            </code>
        </a>
        and
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ApplicationKit/Classes/NSStatusItem_Class/index.html"
        target="_blank" sl-processed="1">
            <code>
                NSStatusItem
            </code>
        </a>
        .
    </p>
    <div class="note">
        <p>
            <em>
                Pro tip
            </em>
            : Be careful with the
            <code>
                NSStatusItem
            </code>
            documentation. The API changes significantly in Yosemite, and sadly, the
            documentation marks all old methods as deprecated, but doesn’t document
            the new alternative methods. For that, you need to command click on
            <code>
                NSStatusItem
            </code>
            in Xcode to look at the generated Swift header. There are only a few methods
            now and all the functionality is inside an
            <code>
                NSButton
            </code>
            , so it’s pretty easy to comprehend.
        </p>
    </div>
    <p>
        Thanks for taking the time to learn how to make a cool popover menu app
        for OS X. For now, it’s pretty simple, but you can see that the concepts
        you’ve learned here are an excellent foundation for a variety of apps.
    </p>
</div>