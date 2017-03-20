# macOS教程：Core Graphics

#### [原文地址](https://www.raywenderlich.com/128614/core-graphics-os-x-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div class="note">
        <p>
            <em>
                Update 9/22/16:
            </em>
            This tutorial has been updated for Xcode 8 and Swift 3.
        </p>
    </div>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature-250x250.png"
        alt="OSXCoreGraphics-feature" width="250" height="250" class="alignright size-thumbnail wp-image-135093 bordered"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/06/OSXCoreGraphics-feature-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
        You’ve seen a lot of apps that depict beautiful graphics and stylish custom
        views. The best of them make a lasting impression, and you always remember
        them because they are just
        <i>
            so
        </i>
        pretty.
    </p>
    <p>
        <em>
            Core Graphics
        </em>
        is Apple’s 2D drawing engine, and is one of the coolest frameworks in
        macOS and iOS. It has capacity to draw anything you can imagine, from simple
        shapes and text to more complex visual effects that include shadows and
        gradients.
    </p>
    <p>
        In this Core Graphics on macOS tutorial, you’ll build up an app named
        <em>
            DiskInfo
        </em>
        to create a custom view that displays the available space and file distribution
        of a hard drive. It’s a solid example of how you can use Core Graphics
        to make a dull, text-based interface beautiful:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/graphview.png"
        rel="attachment wp-att-128931">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/graphview-480x166.png"
            alt="Disc information drawn with Core Graphics" width="480" height="166"
            class="aligncenter size-medium wp-image-128931" srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/graphview-480x166.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/graphview.png 695w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Along the way you’ll discover how to:
    </p>
    <ul>
        <li>
            Create and configure a custom view, the base layer for any graphical element
        </li>
        <li>
            Implement live rendering so that you don’t have to build and run every
            time you change your graphics
        </li>
        <li>
            Paint with code by working with paths, fills, clipping areas and strings
        </li>
        <li>
            Use
            <em>
                Cocoa Drawing
            </em>
            , a tool available to
            <em>
                AppKit
            </em>
            apps, which defines higher level classes and functions
        </li>
    </ul>
    <p>
        In the first part of this Core Graphics on macOS tutorial, you’ll implement
        the bar chart using Core Graphics, before moving on to learn how to draw
        the pie chart using Cocoa Drawing.
    </p>
    <p>
        So put on your painter’s hat and get ready to learn how to color your
        world.
    </p>
    <h2>
        Getting Started
    </h2>
    <p>
        First, download the starter project for DiskInfo
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/06/DiskInfo-Starter.zip">
            here
        </a>
        . Build and run it now.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-diskinfo-build-run1.png"
        rel="attachment wp-att-128902">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-diskinfo-build-run1-480x259.png"
            alt="Original view without any Core Graphics drawing" width="480" height="259"
            class="aligncenter size-medium wp-image-128902" srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-diskinfo-build-run1-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-diskinfo-build-run1-768x414.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-diskinfo-build-run1-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-diskinfo-build-run1.png 1258w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        The app lists all your hard drives, and when you click on one it shows
        detailed information.
    </p>
    <p>
        Before going any further, have a look at the structure of the project
        to become familiar with the lay of the land:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-starterproject-structure-xcode-edit.png"
        rel="attachment wp-att-129857">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-starterproject-structure-xcode-edit-312x500.png"
            alt="sshot-starterproject-structure-xcode-edit" width="312" height="500"
            class="aligncenter size-large wp-image-129857" srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-starterproject-structure-xcode-edit-312x500.png 312w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-starterproject-structure-xcode-edit-200x320.png 200w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-starterproject-structure-xcode-edit.png 537w"
            sizes="(max-width: 312px) 100vw, 312px">
        </a>
    </p>
    <p>
        How about a guided tour?
    </p>
    <ul>
        <li>
            <em>
                ViewController.swift
            </em>
            : The main view controller of the application
        </li>
        <li>
            <em>
                VolumeInfo.swift
            </em>
            : Contains the implementation of the
            <code>
                VolumeInfo
            </code>
            class, which reads the information from the hard drive, and the
            <code>
                FilesDistribution
            </code>
            struct that handles the split between file types
        </li>
        <li>
            <em>
                NSColor+DiskInfo.swift
            </em>
            and
            <em>
                NSFont+DiskInfo.swift
            </em>
            : Extensions that define constants with the default colors and fonts
        </li>
        <li>
            <em>
                CGFloat+Radians.swift
            </em>
            : Extension that converts between degrees and radians via some helper
            functions
        </li>
        <li>
            <em>
                MountedVolumesDataSource.swift
            </em>
            and
            <em>
                MountedVolumesDelegate.swift
            </em>
            : Implement the required methods to show disk information in the outline
            view
        </li>
    </ul>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            The app shows the correct disk usage information, but for the sake this
            tutorial, it creates a random file distribution.
        </p>
        <p>
            Calculating the real file distribution each time you run the app will
            quickly become a time drain and spoil all your fun, and nobody wants that.
        </p>
    </div>
    <h2>
        Creating a Custom View
    </h2>
    <p>
        Your first to-do is to create a custom view named
        <code>
            GraphView
        </code>
        . It’s where you’ll draw the pie and bar charts, so it’s pretty important.
    </p>
    <p>
        You need to accomplish two objectives to create a custom view:
    </p>
    <ol>
        <li>
            Create an
            <code>
                NSView
            </code>
            subclass.
        </li>
        <li>
            Override
            <code>
                draw(_:)
            </code>
            and add some drawing code.
        </li>
    </ol>
    <p>
        On a high level, it’s as easy as that. Follow the next steps to learn
        how to get there.
    </p>
    <h3>
        Make the NSView Subclass
    </h3>
    <p>
        Select the
        <em>
            Views
        </em>
        group in the Project Navigator. Choose
        <em>
            File \ New \ File…
        </em>
        and select the
        <em>
            macOS \ Source \ Cocoa Class
        </em>
        file template.
    </p>
    <p>
        Click
        <em>
            Next
        </em>
        , and in the ensuing screen, name the new class
        <code>
            GraphView
        </code>
        . Make it a subclass of
        <code>
            NSView
        </code>
        , and make sure that the language is
        <em>
            Swift
        </em>
        .
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
        to save your new file.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        , and go the the
        <em>
            View Controller
        </em>
        Scene. Drag a
        <em>
            Custom View
        </em>
        from the
        <em>
            Objects Inspector
        </em>
        into the custom view as shown:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-drag-customview.png"
        rel="attachment wp-att-128905">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-drag-customview-700x236.png"
            alt="sshot-drag-customview" width="700" height="236" class="aligncenter size-large wp-image-128905"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-drag-customview-700x236.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-drag-customview-480x162.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-drag-customview-768x259.png 768w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Select that new custom view, and in the
        <em>
            Identity Inspector
        </em>
        , set the class name to
        <code>
            GraphView
        </code>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-attrinspector-change-class.png"
        rel="attachment wp-att-128907">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-attrinspector-change-class-480x189.png"
            alt="sshot-attrinspector-change-class" width="350" height="138" class="aligncenter size-medium wp-image-128907"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-attrinspector-change-class-480x189.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-attrinspector-change-class.png 512w"
            sizes="(max-width: 350px) 100vw, 350px">
        </a>
    </p>
    <p>
        You need some constraints, so with the graph view selected, click on the
        <em>
            Pin
        </em>
        button in the Auto Layout toolbar. On the popup, set 0 for the
        <em>
            Top
        </em>
        ,
        <em>
            Bottom
        </em>
        ,
        <em>
            Leading
        </em>
        and
        <em>
            Trailing
        </em>
        constraints, and click the
        <em>
            Add 4 Constraints
        </em>
        button.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-addconstraints-trim.png"
        rel="attachment wp-att-129849">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-addconstraints-trim-220x320.png"
            alt="sshot-addconstraints-trim" width="220" height="320" class="aligncenter size-medium wp-image-129849"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-addconstraints-trim-220x320.png 220w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-addconstraints-trim-344x500.png 344w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-addconstraints-trim.png 527w"
            sizes="(max-width: 220px) 100vw, 220px">
        </a>
    </p>
    <p>
        Click the triangular
        <em>
            Resolve Auto Layout Issues
        </em>
        button in the Auto Layout toolbar, and under the
        <em>
            Selected Views
        </em>
        section, click on
        <em>
            Update Frames
        </em>
        — should it show as disabled, click anywhere to deselect the new GraphView,
        and then re-select it.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-updateframes-2-trim.png"
        rel="attachment wp-att-129852">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-updateframes-2-trim-375x320.png"
            alt="sshot-updateframes-2-trim" width="375" height="320" class="aligncenter size-medium wp-image-129852"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-updateframes-2-trim-375x320.png 375w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-updateframes-2-trim-586x500.png 586w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-updateframes-2-trim.png 590w"
            sizes="(max-width: 375px) 100vw, 375px">
        </a>
    </p>
    <h3>
        Override draw(_:)
    </h3>
    <p>
        Open
        <em>
            GraphView.swift
        </em>
        . You’ll see that
        <em>
            Xcode
        </em>
        created a default implementation of
        <code>
            draw(_:)
        </code>
        . Replace the existing comment with the following, ensuring that you leave
        the call to the superclass method:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1286141">
                    <td class="code" id="p128614code1">
                        <pre class="swift" style="font-family:monospace;">
                            NSColor.white.setFill() NSRectFill(bounds)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        First you set the fill color to white, and then you call the
        <code>
            NSRectFill
        </code>
        method to fill the view background with that color.
    </p>
    <p>
        Build and run.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-whitecolor.png"
        rel="attachment wp-att-128910">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-whitecolor-700x377.png"
            alt="sshot-build-run-whitecolor" width="450" height="242" class="aligncenter size-medium wp-image-128910"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-whitecolor-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-whitecolor-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-whitecolor-768x414.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-whitecolor.png 1258w"
            sizes="(max-width: 450px) 100vw, 450px">
        </a>
    </p>
    <p>
        Your custom view’s background has changed from standard gray to white.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/first-custom-view.png"
        rel="attachment wp-att-128963">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/first-custom-view-289x320.png"
            alt="first-custom-view" width="289" height="320" class="aligncenter size-medium wp-image-128963"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/first-custom-view-289x320.png 289w, https://koenig-media.raywenderlich.com/uploads/2016/03/first-custom-view-452x500.png 452w, https://koenig-media.raywenderlich.com/uploads/2016/03/first-custom-view.png 606w"
            sizes="(max-width: 289px) 100vw, 289px">
        </a>
    </p>
    <p>
        Yes, it’s that easy to create a custom drawn view.
    </p>
    <h2>
        Live Rendering: @IBDesignable and @IBInspectable
    </h2>
    <p>
        Xcode 6 introduced an amazing feature: live rendering. It allows you to
        see how your custom view looks in Interface Builder — without the need
        to build and run.
    </p>
    <p>
        To enable it, you just need to add the
        <code>
            @IBDesignable
        </code>
        annotation to your class, and optionally, implement
        <code>
            prepareForInterfaceBuilder()
        </code>
        to provide some sample data.
    </p>
    <p>
        Open
        <em>
            GraphView.swift
        </em>
        and add this just before the class declaration:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1286142">
                    <td class="code" id="p128614code2">
                        <pre class="swift" style="font-family:monospace;">
                            @IBDesignable
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now, you need to provide sample data. Add this inside the
        <code>
            GraphView
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1286143">
                    <td class="code" id="p128614code3">
                        <pre class="swift" style="font-family:monospace;">
                            var fileDistribution: FilesDistribution? { didSet { needsDisplay = true
                            } } &nbsp; override func prepareForInterfaceBuilder() { let used = Int64(100000000000)
                            let available = used / 3 let filesBytes = used / 5 let distribution: [FileType]
                            = [ .apps(bytes: filesBytes / 2, percent: 0.1), .photos(bytes: filesBytes,
                            percent: 0.2), .movies(bytes: filesBytes * 2, percent: 0.15), .audio(bytes:
                            filesBytes, percent: 0.18), .other(bytes: filesBytes, percent: 0.2) ] fileDistribution
                            = FilesDistribution(capacity: used + available, available: available, distribution:
                            distribution) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This defines the property
        <code>
            fileDistribution
        </code>
        that will store hard drive information. When the property changes, it
        sets the
        <code>
            needsDisplay
        </code>
        property of the view to
        <em>
            true
        </em>
        to force the view to redraw its content.
    </p>
    <p>
        Then it implements
        <code>
            prepareForInterfaceBuilder()
        </code>
        to create a sample file distribution that Xcode will use to render the
        view.
    </p>
    <div class="note">
        <p>
            <em>
                Note
            </em>
            : You can also change the visual attributes of your custom views in real
            time inside Interface Builder. You just need to add the
            <code>
                @IBInspectable
            </code>
            annotation to a property.
        </p>
    </div>
    <p>
        Next up: make all the visual properties of the graph view inspectable.
        Add the following code inside the
        <code>
            GraphView
        </code>
        implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1286144">
                    <td class="code" id="p128614code4">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 fileprivate struct Constants { static let barHeight: CGFloat = 30.0
                            static let barMinHeight: CGFloat = 20.0 static let barMaxHeight: CGFloat
                            = 40.0 static let marginSize: CGFloat = 20.0 static let pieChartWidthPercentage:
                            CGFloat = 1.0 / 3.0 static let pieChartBorderWidth: CGFloat = 1.0 static
                            let pieChartMinRadius: CGFloat = 30.0 static let pieChartGradientAngle:
                            CGFloat = 90.0 static let barChartCornerRadius: CGFloat = 4.0 static let
                            barChartLegendSquareSize: CGFloat = 8.0 static let legendTextMargin: CGFloat
                            = 5.0 } &nbsp; // 2 @IBInspectable var barHeight: CGFloat = Constants.barHeight
                            { didSet { barHeight = max(min(barHeight, Constants.barMaxHeight), Constants.barMinHeight)
                            } } @IBInspectable var pieChartUsedLineColor: NSColor = NSColor.pieChartUsedStrokeColor
                            @IBInspectable var pieChartAvailableLineColor: NSColor = NSColor.pieChartAvailableStrokeColor
                            @IBInspectable var pieChartAvailableFillColor: NSColor = NSColor.pieChartAvailableFillColor
                            @IBInspectable var pieChartGradientStartColor: NSColor = NSColor.pieChartGradientStartColor
                            @IBInspectable var pieChartGradientEndColor: NSColor = NSColor.pieChartGradientEndColor
                            @IBInspectable var barChartAvailableLineColor: NSColor = NSColor.availableStrokeColor
                            @IBInspectable var barChartAvailableFillColor: NSColor = NSColor.availableFillColor
                            @IBInspectable var barChartAppsLineColor: NSColor = NSColor.appsStrokeColor
                            @IBInspectable var barChartAppsFillColor: NSColor = NSColor.appsFillColor
                            @IBInspectable var barChartMoviesLineColor: NSColor = NSColor.moviesStrokeColor
                            @IBInspectable var barChartMoviesFillColor: NSColor = NSColor.moviesFillColor
                            @IBInspectable var barChartPhotosLineColor: NSColor = NSColor.photosStrokeColor
                            @IBInspectable var barChartPhotosFillColor: NSColor = NSColor.photosFillColor
                            @IBInspectable var barChartAudioLineColor: NSColor = NSColor.audioStrokeColor
                            @IBInspectable var barChartAudioFillColor: NSColor = NSColor.audioFillColor
                            @IBInspectable var barChartOthersLineColor: NSColor = NSColor.othersStrokeColor
                            @IBInspectable var barChartOthersFillColor: NSColor = NSColor.othersFillColor
                            &nbsp; // 3 func colorsForFileType(fileType: FileType) -&gt; (strokeColor:
                            NSColor, fillColor: NSColor) { switch fileType { case .audio(_, _): return
                            (strokeColor: barChartAudioLineColor, fillColor: barChartAudioFillColor)
                            case .movies(_, _): return (strokeColor: barChartMoviesLineColor, fillColor:
                            barChartMoviesFillColor) case .photos(_, _): return (strokeColor: barChartPhotosLineColor,
                            fillColor: barChartPhotosFillColor) case .apps(_, _): return (strokeColor:
                            barChartAppsLineColor, fillColor: barChartAppsFillColor) case .other(_,
                            _): return (strokeColor: barChartOthersLineColor, fillColor: barChartOthersFillColor)
                            } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This is what the code above does:
    </p>
    <ol>
        <li>
            Declares a struct with constants — magic numbers in code are a no-no —
            you’ll use them throughout the tutorial.
        </li>
        <li>
            Declares all the configurable properties of the view as
            <em>
                @IBInspectable
            </em>
            and sets them using the values in
            <em>
                NSColor+DiskInfo.swift
            </em>
            . Pro tip: To make a property inspectable, you must declare its type,
            even when it’s obvious from the contents.
        </li>
        <li>
            Defines a helper method that returns the stroke and fill colors to use
            for a file type. It’ll come in handy when you draw the file distribution.
        </li>
    </ol>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and have a look at the graph view. It’s now white instead of the default
        view color, meaning that live rendering is working. Have patience if it’s
        not there right away; it may take a second or two to render.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-render-white-trim.png"
        rel="attachment wp-att-129854">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-render-white-trim-480x267.png"
            alt="sshot-render-white-trim" width="480" height="267" class="aligncenter size-medium wp-image-129854"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-render-white-trim-480x267.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-render-white-trim-768x427.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-render-white-trim-700x389.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-render-white-trim.png 1262w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Select the graph view and open the
        <em>
            Attributes Inspector
        </em>
        . You’ll see all of the inspectable properties you’ve added.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim.png"
        rel="attachment wp-att-129855">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-318x320.png"
            alt="sshot-ibdesignable-trim" width="318" height="320" class="aligncenter size-medium wp-image-129855"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-318x320.png 318w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-768x772.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-497x500.png 497w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim-128x128.png 128w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-ibdesignable-trim.png 775w"
            sizes="(max-width: 318px) 100vw, 318px">
        </a>
    </p>
    <p>
        From now on, you can choose to build and run the app to see the results,
        or just check it in Interface Builder.
    </p>
    <p>
        Time to do some drawing.
    </p>
    <h2>
        Graphics Contexts
    </h2>
    <p>
        When you use Core Graphics, you don’t draw directly into the view. You
        use a
        <em>
            Graphics Context
        </em>
        , and that’s where the system renders the drawing and displays it in the
        view.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/image-rendering.png"
        rel="attachment wp-att-128912">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/image-rendering-591x500.png"
            alt="image-rendering" width="300" height="254" class="aligncenter size-medium wp-image-128912"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/image-rendering-591x500.png 591w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-rendering-378x320.png 378w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-rendering.png 674w"
            sizes="(max-width: 300px) 100vw, 300px">
        </a>
    </p>
    <p>
        Core Graphics uses a “painter’s model”, so when you draw into a context,
        think of it as if you were swooshing paint across a canvas. You lay down
        a path and fill it, and then lay down another path on top and fill it.
        You can’t change the pixels that have been laid down, but you can paint
        over them.
    </p>
    <p>
        This concept is very important, because ordering affects the final result.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/drawing-order-aligned.png"
        rel="attachment wp-att-128913">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/drawing-order-aligned.png"
            alt="image-drawing-order" width="500" height="302" class="aligncenter size-medium wp-image-128913">
        </a>
    </p>
    <h2>
        Drawing Shapes with Paths
    </h2>
    <p>
        To draw a shape in Core Graphics, you need to define a
        <em>
            path
        </em>
        , represented in Core Graphics by the type
        <code>
            CGPathRef
        </code>
        and its mutable representation
        <code>
            CGMutablePathRef
        </code>
        . A path is simply a vectorial representation of a shape. It does not
        draw itself.
    </p>
    <p>
        When your path is ready, you add it to the context, which uses the path
        information and drawing attributes to render the desired graphic.
    </p>
    <h3>
        Make a Path…For The Bar Chart
    </h3>
    <p>
        A rounded rectangle is the basic shape of the bar chart, so start there.
    </p>
    <p>
        Open
        <em>
            GraphView.swift
        </em>
        and add the following extension at the end of the file, outside of the
        class definition:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1286145">
                    <td class="code" id="p128614code5">
                        <pre class="swift" style="font-family:monospace;">
                            // MARK: - Drawing extension &nbsp; extension GraphView { func drawRoundedRect(rect:
                            CGRect, inContext context: CGContext?, radius: CGFloat, borderColor: CGColor,
                            fillColor: CGColor) { // 1 let path = CGMutablePath() &nbsp; // 2 path.move(
                            to: CGPoint(x: rect.midX, y:rect.minY )) path.addArc( tangent1End: CGPoint(x:
                            rect.maxX, y: rect.minY ), tangent2End: CGPoint(x: rect.maxX, y: rect.maxY),
                            radius: radius) path.addArc( tangent1End: CGPoint(x: rect.maxX, y: rect.maxY
                            ), tangent2End: CGPoint(x: rect.minX, y: rect.maxY), radius: radius) path.addArc(
                            tangent1End: CGPoint(x: rect.minX, y: rect.maxY ), tangent2End: CGPoint(x:
                            rect.minX, y: rect.minY), radius: radius) path.addArc( tangent1End: CGPoint(x:
                            rect.minX, y: rect.minY ), tangent2End: CGPoint(x: rect.maxX, y: rect.minY),
                            radius: radius) path.closeSubpath() &nbsp; // 3 context?.setLineWidth(1.0)
                            context?.setFillColor(fillColor) context?.setStrokeColor(borderColor) &nbsp;
                            // 4 context?.addPath(path) context?.drawPath(using: .fillStroke) } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        TL/DR:
        <i>
            That
        </i>
        is how you draw a rectangle. Here’s a more comprehensive explanation:
    </p>
    <ol>
        <li>
            Create a mutable path.
        </li>
        <li>
            Form the rounded rectangle path, following these steps:
        </li>
        <ul>
            <li>
                Move to the center point at the bottom of the rectangle.
            </li>
            <li>
                Add the lower line segment at the bottom-right corner using
                <code>
                    addArc(tangent1End:tangent2End:radius)
                </code>
                . This method draws the horizontal line and the rounded corner.
            </li>
            <li>
                Add the right line segment and the top-right corner.
            </li>
            <li>
                Add the top line segment and the top-left corner.
            </li>
            <li>
                Add the right line segment and the bottom-left corner.
            </li>
            <li>
                Close the path, which adds a line from the last point to the starter point.
            </li>
        </ul>
        <li>
            Set the drawing attributes: line width, fill color and border color.
        </li>
        <li>
            Add the path to the context and draw it using the
            <code>
                .fillStroke
            </code>
            parameter, which tells Core Graphics to fill the rectangle and draw the
            border.
        </li>
    </ol>
    <p>
        You’ll never look at a rectangle the same way! Here’s the humble result
        of all that code:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/image-roundedrect.png"
        rel="attachment wp-att-128914">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/image-roundedrect-480x150.png"
            alt="image-roundedrect" width="480" height="150" class="aligncenter size-medium wp-image-128914"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/image-roundedrect-480x150.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-roundedrect-768x240.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-roundedrect-700x219.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-roundedrect.png 1304w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <div class="note">
        <p>
            <em>
                Note
            </em>
            : For more information about how path drawing works, check out Paths &amp;
            Arcs in Apple’s
            <a href="https://developer.apple.com/library/mac/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/dq_paths/dq_paths.html"
            target="_blank" title="Quartz 2D Programming Guide">
                Quartz 2D Programming Guide
            </a>
            .
        </p>
    </div>
    <h3>
        Calculate the Bar Chart’s Position
    </h3>
    <p>
        Drawing with Core Graphics is all about calculating the positions of the
        visual elements in your view. It’s important to plan where to locate the
        different elements and think through they should behave when the size of
        the view changes.
    </p>
    <p>
        Here’s the layout for your custom view:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/image-viewlayout.png"
        rel="attachment wp-att-128916">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/image-viewlayout-480x275.png"
            alt="image-viewlayout" width="480" height="275" class="aligncenter size-medium wp-image-128916"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/image-viewlayout-480x275.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-viewlayout-768x440.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-viewlayout-700x401.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-viewlayout-266x151.png 266w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-viewlayout.png 1444w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Open
        <em>
            GraphView.swift
        </em>
        and add this extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1286146">
                    <td class="code" id="p128614code6">
                        <pre class="swift" style="font-family:monospace;">
                            // MARK: - Calculations extension &nbsp; extension GraphView { // 1 func
                            pieChartRectangle() -&gt; CGRect { let width = bounds.size.width * Constants.pieChartWidthPercentage
                            - 2 * Constants.marginSize let height = bounds.size.height - 2 * Constants.marginSize
                            let diameter = max(min(width, height), Constants.pieChartMinRadius) let
                            rect = CGRect(x: Constants.marginSize, y: bounds.midY - diameter / 2.0,
                            width: diameter, height: diameter) return rect } &nbsp; // 2 func barChartRectangle()
                            -&gt; CGRect { let pieChartRect = pieChartRectangle() let width = bounds.size.width
                            - pieChartRect.maxX - 2 * Constants.marginSize let rect = CGRect(x: pieChartRect.maxX
                            + Constants.marginSize, y: pieChartRect.midY + Constants.marginSize, width:
                            width, height: barHeight) return rect } &nbsp; // 3 func barChartLegendRectangle()
                            -&gt; CGRect { let barchartRect = barChartRectangle() let rect = barchartRect.offsetBy(dx:
                            0.0, dy: -(barchartRect.size.height + Constants.marginSize)) return rect
                            } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The above code does all of these required calculations:
    </p>
    <ol>
        <li>
            Start by calculating the position of the pie chart — it’s in the center
            vertically and occupies one third of the view’s width.
        </li>
        <li>
            Here you calculate the position of the bar chart. It takes two thirds
            of the width and it’s located above the vertical center of the view.
        </li>
        <li>
            Then you calculate the position of the graphics legend, based on the minimum
            Y position of the pie chart and the margins.
        </li>
    </ol>
    <p>
        Time to draw it in your view. Add this method inside the
        <code>
            GraphView
        </code>
        drawing extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1286147">
                    <td class="code" id="p128614code7">
                        <pre class="swift" style="font-family:monospace;">
                            func drawBarGraphInContext(context: CGContext?) { let barChartRect = barChartRectangle()
                            drawRoundedRect(rect: barChartRect, inContext: context, radius: Constants.barChartCornerRadius,
                            borderColor: barChartAvailableLineColor.cgColor, fillColor: barChartAvailableFillColor.cgColor)
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        You’ve added a helper method that will draw the bar chart. It draws a
        rounded rectangle as a background, using the fill and stroke colors for
        the available space. You can find those colors in the
        <em>
            NSColor+DiskInfo
        </em>
        extension.
    </p>
    <p>
        Replace all the code inside
        <code>
            draw(_:)
        </code>
        with this:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1286148">
                    <td class="code" id="p128614code8">
                        <pre class="swift" style="font-family:monospace;">
                            super.draw(dirtyRect) &nbsp; let context = NSGraphicsContext.current()?.cgContext
                            drawBarGraphInContext(context: context)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here is where the actual drawing takes place. First, you get the view’s
        current graphics context by invoking
        <code>
            NSGraphicsContext.current()
        </code>
        , and then you call the method to draw the bar chart.
    </p>
    <p>
        Build and run. You’ll see the bar chart in it’s proper position.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-barchart-first.png"
        rel="attachment wp-att-128917">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-barchart-first-480x259.png"
            alt="sshot-build-run-barchart-first" width="480" height="259" class="aligncenter size-medium wp-image-128917"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-barchart-first-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-barchart-first-768x414.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-barchart-first-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-barchart-first.png 1258w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
        <br>
        Now, open
        <em>
            Main.storyboard
        </em>
        and select the
        <em>
            View Controller
        </em>
        scene.
    </p>
    <p>
        You’ll see this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-live-render-barchart-first.png"
        rel="attachment wp-att-128918">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-live-render-barchart-first-480x216.png"
            alt="sshot-live-render-barchart-first" width="480" height="216" class="aligncenter size-medium wp-image-128918"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-live-render-barchart-first-480x216.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-live-render-barchart-first-768x345.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-live-render-barchart-first-700x315.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Interface Builder now renders the view in real time. You can also change
        the colors and the view responds to those changes. How awesome is that?
    </p>
    <h2>
        Clipping Areas
    </h2>
    <p>
        You’re at the part where you make the distribution chart, a bar chart
        that looks like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/barchart.png"
        rel="attachment wp-att-128936">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/barchart-480x52.png"
            alt="barchart" width="480" height="52" class="aligncenter size-medium wp-image-128936"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/barchart-480x52.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/barchart-768x84.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/barchart-700x76.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/barchart.png 882w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Take a step back here and dabble in a bit of theory. As you know, each
        file type has its own color, and somehow, the app needs to calculate each
        bar’s width based on the corresponding file type’s percentage, and then
        draw each type with a unique color.
    </p>
    <p>
        You could create a special shape, such as a filled rectangle with two
        lines at bottom and top of the rectangle, and then draw it. However, there
        is another technique that will let you reuse your code and get the same
        result:
        <em>
            clipping areas
        </em>
        .
    </p>
    <p>
        You can think of a clipping area as a sheet of paper with a hole cut out
        of it, which you place over your drawing: you can only see the part of
        the drawing which shows through the hole. This hole is known as the clipping
        mask, and is specified as a path within Core Graphics.
    </p>
    <p>
        In the case of the bar chart, you can create an identical fully-filled
        bar for each filetype, and then use a clipping-mask to only display the
        correct proportion, as shown in the following diagram:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/image-clippingarea.png"
        rel="attachment wp-att-128919">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/image-clippingarea-411x320.png"
            alt="image-clippingarea" width="411" height="320" class="aligncenter size-medium wp-image-128919"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/image-clippingarea-411x320.png 411w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-clippingarea-768x598.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-clippingarea-643x500.png 643w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-clippingarea.png 1064w"
            sizes="(max-width: 411px) 100vw, 411px">
        </a>
    </p>
    <p>
        With an understanding of how clipping areas work, you’re ready to make
        this bar chart happen.
    </p>
    <p>
        Before drawing, you need to set the value for
        <code>
            fileDistribution
        </code>
        when a disk is selected. Open
        <em>
            Main.storyboard
        </em>
        and go to the
        <em>
            View Controller
        </em>
        scene to create an outlet.
    </p>
    <p>
        <em>
            Option-click
        </em>
        on
        <em>
            ViewController.swift
        </em>
        in the Project Navigator to open it in the
        <em>
            Assistant Editor
        </em>
        , and
        <em>
            Control-Drag
        </em>
        from the graph view into the view controller class source code to create
        an outlet for it.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-1.png"
        rel="attachment wp-att-128920">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-1-480x242.png"
            alt="image-outlet-1" width="500" height="252" class="aligncenter size-medium wp-image-128920"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-1-480x242.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-1-768x388.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-1-700x354.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-1.png 998w"
            sizes="(max-width: 500px) 100vw, 500px">
        </a>
    </p>
    <p>
        In the popup, name the outlet
        <code>
            graphView
        </code>
        and click
        <em>
            Connect
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-2.png"
        rel="attachment wp-att-128921">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/image-outlet-2-480x269.png"
            alt="image-outlet-2" width="280" height="140" class="aligncenter size-medium wp-image-128921">
        </a>
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add this code at the end of
        <code>
            showVolumeInfo(_:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1286149">
                    <td class="code" id="p128614code9">
                        <pre class="swift" style="font-family:monospace;">
                            graphView.fileDistribution = volume.fileDistribution
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This code sets the
        <code>
            fileDistribution
        </code>
        value with the distribution of the selected disk.
    </p>
    <p>
        Open
        <em>
            GraphView.swift
        </em>
        and add this code at the end of
        <code>
            drawBarGraphInContext(context:)
        </code>
        to draw the bar chart:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12861410">
                    <td class="code" id="p128614code10">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 if let fileTypes = fileDistribution?.distribution, let capacity =
                            fileDistribution?.capacity, capacity &gt; 0 { var clipRect = barChartRect
                            // 2 for (index, fileType) in fileTypes.enumerated() { // 3 let fileTypeInfo
                            = fileType.fileTypeInfo let clipWidth = floor(barChartRect.width * CGFloat(fileTypeInfo.percent))
                            clipRect.size.width = clipWidth &nbsp; // 4 context?.saveGState() context?.clip(to:
                            clipRect) &nbsp; let fileTypeColors = colorsForFileType(fileType: fileType)
                            drawRoundedRect(rect: barChartRect, inContext: context, radius: Constants.barChartCornerRadius,
                            borderColor: fileTypeColors.strokeColor.cgColor, fillColor: fileTypeColors.fillColor.cgColor)
                            context?.restoreGState() &nbsp; // 5 clipRect.origin.x = clipRect.maxX
                            } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This is what the code above does:
    </p>
    <ol>
        <li>
            Makes sure there is a valid
            <code>
                fileDistribution
            </code>
            .
        </li>
        <li>
            Iterates through all the file types in the distribution.
        </li>
        <li>
            Calculates the clipping rect, based on the file type percentage and previous
            file types.
        </li>
        <li>
            Saves the state of the context, sets the clipping area and draws the rectangle
            using the colors configured for the file type. Then it restores the state
            of the context.
        </li>
        <li>
            Moves the
            <i>
                x
            </i>
            origin of the clipping rect before the next iteration.
        </li>
    </ol>
    <p>
        You might wonder why you need to save and restore the state of the context.
        Remember the painter’s model? Everything you add to the context stays there.
    </p>
    <p>
        If you add multiple clipping areas, you are in fact creating a clipping
        area that acts as the unifying force for all of them. To avoid that, you
        save the state before adding the clipping area, and when you’ve used it,
        you restore the context to that state, disposing of that clipping area.
    </p>
    <p>
        At this point,
        <em>
            Xcode
        </em>
        shows a warning because
        <code>
            index
        </code>
        is never used. Don’t worry about it for now. You’ll fix it later on.
    </p>
    <p>
        Build and run, or open
        <em>
            Main.storyboard
        </em>
        and check it out in Interface Builder.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-graphbar-drawn.png"
        rel="attachment wp-att-128922">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-graphbar-drawn-480x259.png"
            alt="sshot-build-rung-graphbar-drawn" width="480" height="259" class="aligncenter size-medium wp-image-128922"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-graphbar-drawn-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-graphbar-drawn-768x414.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-graphbar-drawn-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-graphbar-drawn.png 1258w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        It’s beginning to look functional. The bar chart is almost finished and
        you just need to add the legend.
    </p>
    <h3>
        Drawing Strings
    </h3>
    <p>
        Drawing a string in a custom view is super easy. You just need to create
        a dictionary with the string attributes — for instance the font, size,
        color, alignment — calculate the rectangle where it will be drawn, and
        invoke
        <code>
            String
        </code>
        ‘s method
        <code>
            draw(in:withAttributes:)
        </code>
        .
    </p>
    <p>
        Open
        <em>
            GraphView.swift
        </em>
        and add the following property to the class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12861411">
                    <td class="code" id="p128614code11">
                        <pre class="swift" style="font-family:monospace;">
                            fileprivate var bytesFormatter = ByteCountFormatter()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This creates an
        <em>
            ByteCountFormatter
        </em>
        . It does all the heavy work of transforming bytes into a human-friendly
        string.
    </p>
    <p>
        Now, add this inside
        <code>
            drawBarGraphInContext(context:)
        </code>
        . Make sure you add it inside the
        <code>
            for (index,fileType) in fileTypes.enumerated()
        </code>
        loop:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12861412">
                    <td class="code" id="p128614code12">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 let legendRectWidth = (barChartRect.size.width / CGFloat(fileTypes.count))
                            let legendOriginX = barChartRect.origin.x + floor(CGFloat(index) * legendRectWidth)
                            let legendOriginY = barChartRect.minY - 2 * Constants.marginSize let legendSquareRect
                            = CGRect(x: legendOriginX, y: legendOriginY, width: Constants.barChartLegendSquareSize,
                            height: Constants.barChartLegendSquareSize) &nbsp; let legendSquarePath
                            = CGMutablePath() legendSquarePath.addRect( legendSquareRect ) context?.addPath(legendSquarePath)
                            context?.setFillColor(fileTypeColors.fillColor.cgColor) context?.setStrokeColor(fileTypeColors.strokeColor.cgColor)
                            context?.drawPath(using: .fillStroke) &nbsp; // 2 let paragraphStyle =
                            NSMutableParagraphStyle() paragraphStyle.lineBreakMode = .byTruncatingTail
                            paragraphStyle.alignment = .left let nameTextAttributes = [ NSFontAttributeName:
                            NSFont.barChartLegendNameFont, NSParagraphStyleAttributeName: paragraphStyle]
                            &nbsp; // 3 let nameTextSize = fileType.name.size(withAttributes: nameTextAttributes)
                            let legendTextOriginX = legendSquareRect.maxX + Constants.legendTextMargin
                            let legendTextOriginY = legendOriginY - 2 * Constants.pieChartBorderWidth
                            let legendNameRect = CGRect(x: legendTextOriginX, y: legendTextOriginY,
                            width: legendRectWidth - legendSquareRect.size.width - 2 * Constants.legendTextMargin,
                            height: nameTextSize.height) &nbsp; // 4 fileType.name.draw(in: legendNameRect,
                            withAttributes: nameTextAttributes) &nbsp; // 5 let bytesText = bytesFormatter.string(fromByteCount:
                            fileTypeInfo.bytes) let bytesTextAttributes = [ NSFontAttributeName: NSFont.barChartLegendSizeTextFont,
                            NSParagraphStyleAttributeName: paragraphStyle, NSForegroundColorAttributeName:
                            NSColor.secondaryLabelColor] let bytesTextSize = bytesText.size(withAttributes:
                            bytesTextAttributes) let bytesTextRect = legendNameRect.offsetBy(dx: 0.0,
                            dy: -bytesTextSize.height) bytesText.draw(in: bytesTextRect, withAttributes:
                            bytesTextAttributes)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        That was quite a bit of code, but it’s easy to follow:
    </p>
    <ol>
        <li>
            You’re already familiar with this code: calculate the position of the
            legend’s colored square, create a path for it and draw with the appropriate
            colors.
        </li>
        <li>
            Create a dictionary of attributes that includes the font and a paragraph
            style
            <code>
                NSMutableParagraphStyle
            </code>
            . The paragraph defines how the string should be drawn inside the given
            rectangle. In this case, it’s left aligned with a truncated tail.
        </li>
        <li>
            Calculate the position and size of the rectangle to draw the text in.
        </li>
        <li>
            Draw the text invoking
            <code>
                draw(in:withAttributes:)
            </code>
            .
        </li>
        <li>
            Get the size string using the
            <code>
                bytesFormatter
            </code>
            and create the attributes for the file size text. The main difference
            from the previous code is that this sets a different text color in the
            attributes dictionary via
            <code>
                NSFontAttributeName
            </code>
            .
        </li>
    </ol>
    <p>
        Build and run, or open
        <em>
            Main.storyboard
        </em>
        , to see the results).
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-graphbar-legend.png"
        rel="attachment wp-att-128923">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-graphbar-legend-480x259.png"
            alt="sshot-build-run-graphbar-legend" width="480" height="259" class="aligncenter size-medium wp-image-128923"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-graphbar-legend-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-graphbar-legend-768x414.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-graphbar-legend-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-graphbar-legend.png 1258w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        The bar chart is complete! You can resize the window to see how it adapts
        to the new size. Watch how the text properly truncates when there isn’t
        enough space to draw it.
    </p>
    <p>
        Looking great so far!
    </p>
    <h2>
        Cocoa Drawing
    </h2>
    <p>
        <em>
            macOS
        </em>
        apps come with the option to use
        <em>
            AppKit
        </em>
        framework to draw instead. It provides a higher level of abstraction.
        It uses classes instead of
        <em>
            C
        </em>
        functions and includes helper methods that make it easier to perform common
        tasks. The concepts are equivalent in both frameworks, and Cocoa Drawing
        is very easy to adopt if you’re familiar with Core Graphics.
    </p>
    <p>
        As it goes in Core Graphics, you need to create and draw paths, using
        <code>
            NSBezierPath
        </code>
        , the equivalent of
        <code>
            CGPathRef
        </code>
        in Cocoa Drawing:
    </p>
    <p>
        This is how the pie chart will look:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/piechart.png"
        rel="attachment wp-att-128924">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/piechart-320x320.png"
            alt="piechart" width="280" height="280" class="aligncenter size-medium wp-image-128924"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/piechart-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/03/piechart-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/03/piechart-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/03/piechart-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/03/piechart-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/03/piechart-128x128.png 128w, https://koenig-media.raywenderlich.com/uploads/2016/03/piechart.png 375w"
            sizes="(max-width: 280px) 100vw, 280px">
        </a>
    </p>
    <p>
        You’ll draw it in three steps:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/pichart-steps.png"
        rel="attachment wp-att-128941">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/pichart-steps-480x111.png"
            alt="pichart-steps" width="480" height="111" class="aligncenter size-medium wp-image-128941"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/pichart-steps-480x111.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/pichart-steps-768x178.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/pichart-steps-700x163.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <ul>
        <li>
            First, you create a circle path for the available space circle, and then
            you fill and stroke it with the configured colors.
        </li>
        <li>
            Then you create a path for the used space circle segment and stroke it.
        </li>
        <li>
            Finally, you draw a gradient that only fills the used space path.
        </li>
    </ul>
    <p>
        Open
        <em>
            GraphView.swift
        </em>
        and add this method into the drawing extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12861413">
                    <td class="code" id="p128614code13">
                        <pre class="swift" style="font-family:monospace;">
                            func drawPieChart() { guard let fileDistribution = fileDistribution else
                            { return } &nbsp; // 1 let rect = pieChartRectangle() let circle = NSBezierPath(ovalIn:
                            rect) pieChartAvailableFillColor.setFill() pieChartAvailableLineColor.setStroke()
                            circle.stroke() circle.fill() &nbsp; // 2 let path = NSBezierPath() let
                            center = CGPoint(x: rect.midX, y: rect.midY) let usedPercent = Double(fileDistribution.capacity
                            - fileDistribution.available) / Double(fileDistribution.capacity) let endAngle
                            = CGFloat(360 * usedPercent) let radius = rect.size.width / 2.0 path.move(to:
                            center) path.line(to: CGPoint(x: rect.maxX, y: center.y)) path.appendArc(withCenter:
                            center, radius: radius, startAngle: 0, endAngle: endAngle) path.close()
                            &nbsp; // 3 pieChartUsedLineColor.setStroke() path.stroke() }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        There are a few things to go through here:
    </p>
    <ol>
        <li>
            Create a circle path using the constructor
            <code>
                init(ovalIn:)
            </code>
            , set the fill and stroke color, and then draw the path.
        </li>
        <li>
            Create a path for the used space circle segment. First, calculate the
            ending angle based on the used space. Then create the path in four steps:
            <ol>
                <li>
                    Move to the center point of the circle.
                </li>
                <li>
                    Add an horizontal line from the center to the right side of the circle.
                </li>
                <li>
                    Add an arc from current point to the calculated angle.
                </li>
                <li>
                    Close the path. This adds a line from the arc’s end point back to the
                    center of the circle.
                </li>
            </ol>
        </li>
        <li>
            Set the stroke color and stroke the path by calling its
            <code>
                stroke()
            </code>
            method.
        </li>
    </ol>
    <p>
        You may have noticed a couple of differences compared to Core Graphics:
    </p>
    <ul>
        <li>
            There aren’t any reference to the graphics context in the code. That’s
            because these methods automatically get the current context, and in this
            case, it’s the view’s context.
        </li>
        <li>
            Angles are measured in degrees, not radians.
            <em>
                CGFloat+Radians.swift
            </em>
            extends CGFloat to do conversions if needed.
        </li>
    </ul>
    <p>
        Now, add the following code inside
        <code>
            draw(_:)
        </code>
        to draw the pie chart:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12861414">
                    <td class="code" id="p128614code14">
                        <pre class="swift" style="font-family:monospace;">
                            drawPieChart()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run.
        <br>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-pie-stroke.png"
        rel="attachment wp-att-128925">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-pie-stroke-480x259.png"
            alt="sshot-build-rung-pie-stroke" width="480" height="259" class="aligncenter size-medium wp-image-128925"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-pie-stroke-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-pie-stroke-768x414.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-pie-stroke-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-rung-pie-stroke.png 1258w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Looking good so far!
    </p>
    <h3>
        Drawing Gradients
    </h3>
    <p>
        <em>
            Cocoa Drawing
        </em>
        uses
        <code>
            NSGradient
        </code>
        to draw a gradient.
    </p>
    <p>
        You need to draw the gradient inside the used space segment of the circle,
        and you already know how to do it.
    </p>
    <p>
        How will you do it? Exactly, clipping areas!
    </p>
    <p>
        You’ve already created a path to draw it, and you can use it as a clipping
        path before you draw the gradient.
    </p>
    <p>
        Add this code at the end of
        <code>
            drawPieChart()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12861415">
                    <td class="code" id="p128614code15">
                        <pre class="swift" style="font-family:monospace;">
                            if let gradient = NSGradient(starting: pieChartGradientStartColor, ending:
                            pieChartGradientEndColor) { gradient.draw(in: path, angle: Constants.pieChartGradientAngle)
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        In the first line, you try to create a gradient with two colors. If this
        works, you call
        <code>
            draw(in:angle:)
        </code>
        to draw it. Internally, this method sets the clipping path for you and
        draws the gradient inside it. How nice is that?
    </p>
    <p>
        Build and run.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-gradient.png"
        rel="attachment wp-att-128926">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-gradient-480x259.png"
            alt="sshot-build-run-gradient" width="480" height="259" class="aligncenter size-medium wp-image-128926"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-gradient-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-gradient-768x414.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-gradient-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-gradient.png 1258w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        The custom view is looking better and better. There’s only one thing left
        to do: Draw the available and used space text strings inside the pie chart.
    </p>
    <p>
        You already know how to do it. Are you up to the challenge? :]
    </p>
    <p>
        This is what you need to do:
    </p>
    <ol>
        <li>
            Use the
            <code>
                bytesFormatter
            </code>
            to get the text string for the available space (
            <code>
                fileDistribution.available
            </code>
            property ) and full space (
            <code>
                fileDistribution.capacity
            </code>
            property).
        </li>
        <li>
            Calculate the position of the text so that you draw it in the middle point
            of the available and used segments.
        </li>
        <li>
            Draw the text in that position with these attributes:
        </li>
        <ul>
            <li>
                Font:
                <code>
                    NSFont.pieChartLegendFont
                </code>
            </li>
            <li>
                Used space text color:
                <code>
                    NSColor.pieChartUsedSpaceTextColor
                </code>
            </li>
            <li>
                Available space text color:
                <code>
                    NSColor.pieChartAvailableSpaceTextColor
                </code>
            </li>
        </ul>
    </ol>
    <div class="easySpoilerWrapper" style="">
        <table class="easySpoilerTable" border="0" style="text-align:center;"
        align="center" bgcolor="FFFFFF">
            <tbody>
                <tr style="white-space:normal;">
                    <th class="easySpoilerTitleA" style="white-space:normal;font-weight:normal;text-align:left;vertical-align:middle;font-size:120%;color:#000000;">
                        Solution Inside: Draw Pie Chart Legend
                    </th>
                    <th class="easySpoilerTitleB" style="text-align:right;vertical-align:middle;font-size:100%; white-space:nowrap;">
                        <a href="" onclick="wpSpoilerSelect(&quot;spoilerDiv87b8001&quot;); return false;"
                        class="easySpoilerButtonOther" style="font-size:100%;color:#000000;background-color:#fcfcfc;background-image:none;border: 1px inset;border-style:solid;border-color:#cccccc; margin: 3px 0px 3px; padding: 4px; "
                        align="right">
                            Select
                        </a>
                        <a href="" onclick="wpSpoilerToggle(&quot;spoilerDiv87b8001&quot;,true,&quot;Show&quot;,&quot;Hide&quot;,&quot;fast&quot;,false); return false;"
                        id="spoilerDiv87b8001_action" class="easySpoilerButton" value="Show" align="right"
                        style="font-size:100%;color:#000000;background-color:#fcfcfc;background-image:none;border: 1px inset;border-style:solid;border-color:#cccccc; margin: 3px 0px 3px 5px; padding: 4px;">
                            Show
                        </a>
                    </th>
                </tr>
                <tr>
                    <td class="easySpoilerRow" colspan="2" style="">
                        <div id="spoilerDiv87b8001" class="easySpoilerSpoils" style="display:none; white-space:wrap; overflow:auto; vertical-align:middle;">
                            <p>
                                Add this code inside the
                                <code>
                                    drawPieChart()
                                </code>
                                method:
                            </p>
                            <div class="wp_codebox">
                                <table>
                                    <tbody>
                                        <tr id="p12861416">
                                            <td class="code" id="p128614code16">
                                                <pre class="swift" style="font-family:monospace;">
                                                    // 1 let usedMidAngle = endAngle / 2.0 let availableMidAngle = (360.0
                                                    - endAngle) / 2.0 let halfRadius = radius / 2.0 &nbsp; // 2 let usedSpaceText
                                                    = bytesFormatter.string(fromByteCount: fileDistribution.capacity) let usedSpaceTextAttributes
                                                    = [ NSFontAttributeName: NSFont.pieChartLegendFont, NSForegroundColorAttributeName:
                                                    NSColor.pieChartUsedSpaceTextColor] let usedSpaceTextSize = usedSpaceText.size(withAttributes:
                                                    usedSpaceTextAttributes) let xPos = rect.midX + CGFloat(cos(usedMidAngle.radians))
                                                    * halfRadius - (usedSpaceTextSize.width / 2.0) let yPos = rect.midY + CGFloat(sin(usedMidAngle.radians))
                                                    * halfRadius - (usedSpaceTextSize.height / 2.0) usedSpaceText.draw(at:
                                                    CGPoint(x: xPos, y: yPos), withAttributes: usedSpaceTextAttributes) &nbsp;
                                                    // 3 let availableSpaceText = bytesFormatter.string(fromByteCount: fileDistribution.available)
                                                    let availableSpaceTextAttributes = [ NSFontAttributeName: NSFont.pieChartLegendFont,
                                                    NSForegroundColorAttributeName: NSColor.pieChartAvailableSpaceTextColor]
                                                    let availableSpaceTextSize = availableSpaceText.size(withAttributes: availableSpaceTextAttributes)
                                                    let availableXPos = rect.midX + cos(-availableMidAngle.radians) * halfRadius
                                                    - (availableSpaceTextSize.width / 2.0) let availableYPos = rect.midY +
                                                    sin(-availableMidAngle.radians) * halfRadius - (availableSpaceTextSize.height
                                                    / 2.0) availableSpaceText.draw(at: CGPoint(x: availableXPos, y: availableYPos),
                                                    withAttributes: availableSpaceTextAttributes)
                                                </pre>
                                            </td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                            <p>
                                This code does the following:
                            </p>
                            <ol>
                                <li>
                                    Calculates the angles where you’ll draw used and available texts.
                                </li>
                                <li>
                                    Creates the text attributes and calculates the
                                    <i>
                                        x
                                    </i>
                                    and
                                    <i>
                                        y
                                    </i>
                                    position of the used space text – then it draws.
                                </li>
                                <li>
                                    Creates the text attributes and calculates the
                                    <i>
                                        x
                                    </i>
                                    and
                                    <i>
                                        y
                                    </i>
                                    position of the available space, and then it draws.
                                </li>
                            </ol>
                            <p>
                                Now, build and run and see the final result of your handiwork.
                            </p>
                            <p>
                                <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-final-1.png"
                                rel="attachment wp-att-128927">
                                    <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-final-1-480x242.png"
                                    alt="Final app made using Core Graphics on macOS" width="480" height="242"
                                    class="aligncenter size-medium wp-image-128927" srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-final-1-480x242.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-final-1-768x388.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-final-1-700x354.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/03/sshot-build-run-final-1.png 1568w"
                                    sizes="(max-width: 480px) 100vw, 480px">
                                </a>
                            </p>
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
    <br>
    Congratulations! You’ve built a beautiful app using Core Graphics and
    Cocoa Drawing!
    <p>
    </p>
    <h2>
        Where to Go From Here
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
        You can download the completed project
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/06/DiskInfo-Final.zip">
            here
        </a>
        .
    </p>
    <p>
        This Core Graphics on macOS tutorial covered the basics of the different
        frameworks available to use for drawing custom views in
        <em>
            macOS
        </em>
        . You just covered:
    </p>
    <ul>
        <li>
            How to create and draw paths using Core Graphics and Cocoa Drawing
        </li>
        <li>
            How to use clipping areas
        </li>
        <li>
            How to draw text strings
        </li>
        <li>
            How to draw gradients
        </li>
    </ul>
    <p>
        You should now feel confident in your abilities to use Core Graphics and
        Cocoa Drawing next time you need clean, responsive graphics.
    </p>
    <p>
        If you’re looking to learn more, consider the following resources:
    </p>
    <li>
        Apple’s
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CocoaDrawingGuide/Introduction/Introduction.html"
        target="_blank" title="Introduction to Cocoa Drawing Guide">
            Introduction to Cocoa Drawing Guide
        </a>
    </li>
    <li>
        Apple’s
        <a href="https://developer.apple.com/library/mac/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/Introduction/Introduction.html"
        target="_blank" title="Quartz" 2d="" programming="" guide="">
            Quartz 2D Programming Guide
        </a>
    </li>
</div>