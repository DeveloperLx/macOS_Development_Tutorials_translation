# NSCollectionView教程

#### [原文地址](https://www.raywenderlich.com/145978/nscollectionview-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div class="note">
        <p>
            <em>
                Update note:
            </em>
            This NSCollectionView tutorial has been updated to Xcode 8 and Swift 3
            by Gabriel Miro.
        </p>
    </div>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/CollectionViews-2-feature.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/CollectionViews-2-feature-250x250.png"
            alt="CollectionViews-2-feature" width="250" height="250" class="alignright size-thumbnail wp-image-151580"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/CollectionViews-2-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/10/CollectionViews-2-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/10/CollectionViews-2-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/10/CollectionViews-2-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/10/CollectionViews-2-feature-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2016/10/CollectionViews-2-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/10/CollectionViews-2-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/10/CollectionViews-2-feature-128x128.png 128w"
            sizes="(max-width: 250px) 100vw, 250px">
        </a>
    </p>
    <p>
        A collection view is a powerful mechanism for laying out an ordered set
        of data items in a visual way. Finder and Photos both do this: they let
        you tab through files in a gallery layout.
    </p>
    <p>
        Introduced in OS X 10.5,
        <code>
            NSCollectionView
        </code>
        offered a handy means of arranging a group of objects in a grid of identically-sized
        items displayed in a scrollable view.
    </p>
    <p>
        OS X 10.11 El Capitan gave
        <code>
            NSCollectionView
        </code>
        a major overhaul inspired by
        <code>
            UICollectionView
        </code>
        from iOS.
    </p>
    <p>
        macOS 10.12 added two additional features to close the gap with iOS: collapsible
        sections (like in Finder) and sticky headers.
    </p>
    <p>
        In this NSCollectionView tutorial, you’ll build
        <em>
            SlidesMagic
        </em>
        — your own grid-based image browsing app.
    </p>
    <p>
        This tutorial assumes that you know the basics of writing macOS apps.
        If you’re new to macOS, you should take a look at the
        <a href="http://www.raywenderlich.com/category/macos" target="_blank"
        title="macOS tutorials">
            macOS tutorials
        </a>
        available here, and then come back to learn about collection views.
    </p>
    <h2>
        Getting Started
    </h2>
    <p>
        The
        <em>
            SlidesMagic
        </em>
        app you’re going to build is a simple image browser. It’s pretty cool,
        but don’t get all excited and delete Photos from your Mac just yet. :]
    </p>
    <p>
        It retrieves all image files from a folder on the file system and displays
        them with their names in an elegant collection view. The finished app will
        look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/SlidesMagicSections1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/SlidesMagicSections1-409x500.png"
            alt="NSCollectionView tutorial SlidesMagicSections" width="409" height="500"
            class="aligncenter size-large wp-image-121165" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/SlidesMagicSections1-409x500.png 409w, https://koenig-media.raywenderlich.com/uploads/2015/11/SlidesMagicSections1-262x320.png 262w, https://koenig-media.raywenderlich.com/uploads/2015/11/SlidesMagicSections1.png 960w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/SlidesMagic8V2-Starter.zip">
            Download the starter project here
        </a>
        . Build and run:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/empty-app.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/empty-app-415x500.png"
            alt="NSCollectionView tutorial empty-app" width="415" height="500" class="aligncenter size-large wp-image-122803"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/empty-app-415x500.png 415w, https://koenig-media.raywenderlich.com/uploads/2015/12/empty-app-265x320.png 265w, https://koenig-media.raywenderlich.com/uploads/2015/12/empty-app.png 1136w"
            sizes="(max-width: 415px) 100vw, 415px">
        </a>
    </p>
    <p>
        At this point, it appears to be an empty window, but it has hidden features
        that will become the foundation of an image browser.
    </p>
    <p>
        When
        <em>
            SlidesMagic
        </em>
        launches, it automatically loads all the images from the system’s
        <em>
            Desktop Pictures
        </em>
        folder. From
        <em>
            Xcode
        </em>
        ‘s console log, you can see the file names.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/desktop-photos.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/desktop-photos-401x320.png"
            alt="desktop photos" width="401" height="320" class="aligncenter size-medium wp-image-122805"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/desktop-photos-401x320.png 401w, https://koenig-media.raywenderlich.com/uploads/2015/12/desktop-photos-627x500.png 627w, https://koenig-media.raywenderlich.com/uploads/2015/12/desktop-photos.png 772w"
            sizes="(max-width: 401px) 100vw, 401px">
        </a>
    </p>
    <p>
        That list in the console is an indicator that the model-loading logic
        is in place. You can choose another folder by selecting
        <em>
            File/Open Another Folder…
        </em>
        menu.
    </p>
    <h3>
        The Starter Project Code
    </h3>
    <p>
        The starter project provides functionality that is not directly related
        to collection views, but is specific to
        <em>
            SlidesMagic
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionProjectNav.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionProjectNav.png"
            alt="CollectionProjectNav" width="254" height="395" class="aligncenter size-full wp-image-121179"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionProjectNav.png 254w, https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionProjectNav-206x320.png 206w"
            sizes="(max-width: 254px) 100vw, 254px">
        </a>
    </p>
    <h3>
        Model
    </h3>
    <ul>
        <li>
            <em>
                ImageFile.swift
            </em>
            : Encapsulates a single image file
        </li>
        <li>
            <em>
                ImageDirectoryLoader.swift
            </em>
            : Helper class that loads image files from the disk
        </li>
    </ul>
    <h3>
        Controllers
    </h3>
    <p>
        The application has two main controllers:
    </p>
    <ul>
        <li>
            <em>
                WindowController.swift
            </em>
            –
            <code>
                windowDidLoad()
            </code>
            : Sets the initial size of the window on the left half of the screen.
            <code>
                openAnotherFolder(_:)
            </code>
            presents a standard open dialog to choose a different folder.
        </li>
        <li>
            <em>
                ViewController.swift
            </em>
            –
            <code>
                viewDidLoad()
            </code>
            opens the Desktop Pictures folder as the initial folder to browse.
        </li>
    </ul>
    <h2>
        Behind the Scenes of Collection Views
    </h2>
    <p>
        <code>
            NSCollectionView
        </code>
        is the main view; it displays visual items and is assisted by several
        key components.
    </p>
    <h3>
        Layouts
    </h3>
    <p>
        <code>
            NSCollectionViewLayout
        </code>
        : Specifies the layout of the collection view. It’s an abstract class
        from which all concrete layout classes inherit.
    </p>
    <p>
        <code>
            NSCollectionViewFlowLayout
        </code>
        : Provides a flexible grid-like layout. For most apps, this layout can
        be used to achieve your desired results.
    </p>
    <p>
        <code>
            NSCollectionViewGridLayout
        </code>
        : A pre-OS X 10.11 compatibility class, and not recommended for new apps.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/Layouts.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/Layouts-700x220.png"
            alt="Layouts" width="700" height="220" class="aligncenter size-large wp-image-120979"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/Layouts-700x220.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/Layouts-480x151.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/Layouts.png 894w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        <em>
            Sections and
        </em>
        <code>
            IndexPath
        </code>
        : Allows for grouping of items into sections. The items form an ordered
        list of sections, each containing an ordered list of items. Each item is
        associated with an index that comprises of a pair of integers (section,
        item) encapsulated in an
        <code>
            IndexPath
        </code>
        instance. When grouping of items into sections isn’t required, you still
        have at least one section (by default).
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/IndexPath-650x424.png"
        alt="IndexPath" width="650" height="424" class="aligncenter size-large wp-image-145590"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/IndexPath-650x424.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/IndexPath-480x313.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/10/IndexPath.png 839w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <h3>
        The Collection View Items
    </h3>
    <p>
        Like many other
        <em>
            Cocoa
        </em>
        frameworks, items in the collection view follow the
        <em>
            MVC
        </em>
        design pattern.
    </p>
    <p>
        <em>
            The Model and the View
        </em>
        : The items’ content comes from your model’s data objects. Each individual
        object that becomes visible gets its own view in the larger collection
        view. The structure of these individual views are defined in a separate
        nib with file extension .xib.
    </p>
    <p>
        <em>
            The Controller
        </em>
        : The nib mentioned above is owned by an instance of
        <em>
            NSCollectionViewItem
        </em>
        , which is a descendant of
        <code>
            NSViewController
        </code>
        . It mediates the flow of information between the items’ views and model
        objects. Generally, you subclass
        <code>
            NSCollectionViewItem
        </code>
        . When items are not of the same kind, you define a different subclass
        and nib for each variant.
    </p>
    <h3>
        Supplementary Views
    </h3>
    <p>
        To display extra information in the collection view that’s not part of
        an individual item, you’d use supplementary views. Some common implementations
        of these are section headers and footers.
    </p>
    <h3>
        The Collection View Data Source and Delegates
    </h3>
    <ul>
        <li>
            <code>
                NSCollectionViewDataSource
            </code>
            : Populates the collection view with items and supplementary views.
        </li>
        <li>
            <code>
                NSCollectionViewDelegate
            </code>
            : Handles events related to drag-and-drop, selection and highlighting.
        </li>
        <li>
            <code>
                NSCollectionViewDelegateFlowLayout
            </code>
            : Lets you customize a flow layout.
        </li>
    </ul>
    <div class="note">
        <em>
            Note
        </em>
        : You can populate a table view by using a data source or Cocoa Bindings.
        This NSCollectionView tutorial covers the data source.
    </div>
    <h2>
        Creating the Collection View
    </h2>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        . Go to the
        <em>
            Object Library
        </em>
        , and drag a
        <em>
            Collection View
        </em>
        into the view of the
        <em>
            View Controller Scene
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/AddCollectionView.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/AddCollectionView-700x424.png"
            alt="AddCollectionView" width="700" height="424" class="aligncenter size-large wp-image-121242"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/AddCollectionView-700x424.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/AddCollectionView-480x291.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/AddCollectionView.png 1298w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <div class="note">
        <em>
            Note
        </em>
        : You may have noticed
        <em>
            Interface Builder
        </em>
        added three views instead of just one. That’s because the
        <em>
            Collection View
        </em>
        is embedded inside a
        <em>
            Scroll View
        </em>
        , which also has another subview named
        <em>
            Clip View
        </em>
        . When you’re instructed to select the
        <em>
            Collection View
        </em>
        , make sure you’re
        <i>
            not
        </i>
        selecting the
        <em>
            Scroll View
        </em>
        or the
        <em>
            Clip View
        </em>
        .
    </div>
    <p>
        Resize the
        <em>
            Bordered Scroll View
        </em>
        so it takes up the entire area of the parent view. Then, select
        <em>
            Editor/Resolve Auto Layout Issues/Add Missing Constraints
        </em>
        to add the
        <em>
            Auto Layout
        </em>
        constraints.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionZeroConstraints.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionZeroConstraints-700x427.png"
            alt="CollectionZeroConstraints" width="700" height="427" class="aligncenter size-large wp-image-121245"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionZeroConstraints-700x427.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionZeroConstraints-480x293.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/CollectionZeroConstraints.png 1336w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        You need to add an outlet in
        <em>
            ViewController
        </em>
        to access the collection view. Open
        <em>
            ViewController.swift
        </em>
        and add the following inside the
        <code>
            ViewController
        </code>
        class definition:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1459781">
                    <td class="code" id="p145978code1">
                        <pre class="swift" style="font-family:monospace;">
                            @IBOutlet weak var collectionView: NSCollectionView!
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        , and select the
        <em>
            View Controller
        </em>
        inside the
        <em>
            View Controller Scene
        </em>
        .
    </p>
    <p>
        Open the
        <em>
            Connections Inspector
        </em>
        and find the
        <em>
            collectionView
        </em>
        element within the
        <em>
            Outlets
        </em>
        section. Connect it to the collection view by
        <em>
            dragging
        </em>
        from the button next to it to the collection view control in the canvas.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectCollectionView.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectCollectionView-700x353.png"
            alt="ConnectCollectionView" width="700" height="353" class="aligncenter size-large wp-image-121275"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectCollectionView-700x353.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectCollectionView-480x242.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectCollectionView.png 1062w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <h3>
        Configure the Collection View Layout
    </h3>
    <p>
        You’ve got options here: you can set the initial layout and some of its
        attributes in
        <em>
            Interface Builder
        </em>
        , or you can set them programmatically.
    </p>
    <p>
        For SlidesMagic, you’ll take the programmatic approach.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add the following method to
        <code>
            ViewController
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1459782">
                    <td class="code" id="p145978code2">
                        <pre class="swift" style="font-family:monospace;">
                            fileprivate func configureCollectionView() { // 1 let flowLayout = NSCollectionViewFlowLayout()
                            flowLayout.itemSize = NSSize(width: 160.0, height: 140.0) flowLayout.sectionInset
                            = EdgeInsets(top: 10.0, left: 20.0, bottom: 10.0, right: 20.0) flowLayout.minimumInteritemSpacing
                            = 20.0 flowLayout.minimumLineSpacing = 20.0 collectionView.collectionViewLayout
                            = flowLayout // 2 view.wantsLayer = true // 3 collectionView.layer?.backgroundColor
                            = NSColor.black.cgColor }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s what you’re doing in this method:
    </p>
    <ol>
        <li>
            Creating an
            <code>
                NSCollectionViewFlowLayout
            </code>
            and setting its attributes and the
            <code>
                collectionViewLayout
            </code>
            property of the
            <code>
                NSCollectionView
            </code>
            .
        </li>
        <li>
            For optimal performance,
            <code>
                NSCollectionView
            </code>
            is designed to be layer-backed. So, you’re setting an ancestor’s
            <code>
                wantsLayer
            </code>
            property to
            <code>
                true
            </code>
            .
        </li>
        <li>
            Setting the collection view’s background color to black.
        </li>
    </ol>
    <p>
        You need to call this method when the view is created, so add this to
        the end of
        <code>
            viewDidLoad()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1459783">
                    <td class="code" id="p145978code3">
                        <pre class="swift" style="font-family:monospace;">
                            configureCollectionView()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/BlackView.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/BlackView-262x320.png"
            alt="BlackView" width="262" height="320" class="aligncenter size-medium wp-image-121354"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/BlackView-262x320.png 262w, https://koenig-media.raywenderlich.com/uploads/2015/11/BlackView-409x500.png 409w, https://koenig-media.raywenderlich.com/uploads/2015/11/BlackView.png 960w"
            sizes="(max-width: 262px) 100vw, 262px">
        </a>
    </p>
    <p>
        At this point, you have a black background and a layout.
    </p>
    <h2>
        Creating a Collection View Item
    </h2>
    <p>
        Now you need to create an
        <code>
            NSCollectionViewItem
        </code>
        subclass to display your data elements.
    </p>
    <p>
        Go to
        <em>
            File/New/File…
        </em>
        , select
        <em>
            macOS/Source/Cocoa Class
        </em>
        and click
        <em>
            Next
        </em>
        .
    </p>
    <p>
        Set the
        <em>
            Class
        </em>
        field to
        <em>
            CollectionViewItem
        </em>
        , the
        <em>
            Subclass of
        </em>
        field to
        <code>
            NSCollectionViewItem
        </code>
        , and check
        <em>
            Also create XIB for user interface
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/CreateColViewItems.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/CreateColViewItems.png"
            alt="CreateColViewItems" width="444" height="163" class="aligncenter size-full wp-image-121352">
        </a>
    </p>
    <p>
        Click
        <em>
            Next
        </em>
        , and in the save dialog, select
        <em>
            Controllers
        </em>
        from
        <em>
            Group
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
            CollectionViewItem.swift
        </em>
        and replace the entire class with this:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1459784">
                    <td class="code" id="p145978code4">
                        <pre class="swift" style="font-family:monospace;">
                            import Cocoa class CollectionViewItem: NSCollectionViewItem { &nbsp; //
                            1 var imageFile: ImageFile? { didSet { guard isViewLoaded else { return
                            } if let imageFile = imageFile { imageView?.image = imageFile.thumbnail
                            textField?.stringValue = imageFile.fileName } else { imageView?.image =
                            nil textField?.stringValue = "" } } } &nbsp; // 2 override func viewDidLoad()
                            { super.viewDidLoad() view.wantsLayer = true view.layer?.backgroundColor
                            = NSColor.lightGray.cgColor } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        In here, you do the following:
    </p>
    <ol>
        <li>
            Define the
            <code>
                imageFile
            </code>
            property that holds the model object to be presented in this item. When
            set, its
            <code>
                didSet
            </code>
            property observer sets the content of the item’s image and label.
        </li>
        <li>
            Change the background color of the item’s view.
        </li>
    </ol>
    <h2>
        Add Controls to the View
    </h2>
    <p>
        When you created
        <em>
            CollectionViewItem.swift
        </em>
        you selected “Also create a XIB” which produced the
        <em>
            CollectionViewItem.xib
        </em>
        nib file. For sake of order, drag the nib to the
        <em>
            Resources
        </em>
        group just below
        <em>
            Main.storyboard
        </em>
        .
    </p>
    <p>
        The
        <em>
            View
        </em>
        in the nib is the root view for a subtree of controls to be displayed
        in each item. You’re going to add an image view for the slide and a label
        for the file name.
    </p>
    <p>
        Open
        <em>
            CollectionViewItem.xib
        </em>
        .
    </p>
    <p>
        Add an
        <code>
            NSImageView
        </code>
        :
    </p>
    <ol>
        <li>
            From the
            <em>
                Object Library
            </em>
            , add an
            <em>
                Image View
            </em>
            to
            <em>
                View
            </em>
            .
        </li>
        <li>
            Click
            <em>
                Pin
            </em>
            from the
            <em>
                Auto Layout
            </em>
            toolbar to set its constraints.
        </li>
        <li>
            Set the
            <em>
                top
            </em>
            ,
            <em>
                leading
            </em>
            and
            <em>
                trailing
            </em>
            constraints to 0, the
            <em>
                bottom
            </em>
            to 30. Choose
            <em>
                Update Frames: Items of New Constraints
            </em>
            and click
            <em>
                Add 4 Constraints
            </em>
            .
        </li>
    </ol>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL1-700x410.png"
            alt="ImageAL1" width="700" height="410" class="aligncenter size-large wp-image-121359"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL1-700x410.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL1-480x281.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL1.png 1449w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL2.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL2-700x365.png"
            alt="ImageAL2" width="700" height="365" class="aligncenter size-large wp-image-121361"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL2-700x365.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL2-480x251.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ImageAL2.png 774w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Add a label:
    </p>
    <ol>
        <li>
            From the
            <em>
                Object Library
            </em>
            , add a
            <em>
                Label
            </em>
            below the
            <em>
                Image View
            </em>
            .
        </li>
        <p>
            <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/LabelInPlace.png">
                <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/LabelInPlace-700x330.png"
                alt="LabelInPlace" width="700" height="330" class="aligncenter size-large wp-image-121365"
                srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/LabelInPlace-700x330.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/LabelInPlace-480x226.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/LabelInPlace.png 757w"
                sizes="(max-width: 700px) 100vw, 700px">
            </a>
        </p>
        <li>
            Click the
            <em>
                Pin
            </em>
            button. Set the
            <em>
                top
            </em>
            ,
            <em>
                bottom
            </em>
            ,
            <em>
                trailing
            </em>
            and
            <em>
                leading
            </em>
            constraints to 0. Choose
            <em>
                Update Frames: Items of New Constraints
            </em>
            and click
            <em>
                Add 4 Constraints
            </em>
            .
        </li>
        <p>
            <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-20.11.30.png">
                <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-20.11.30-225x320.png"
                alt="Screen Shot 2015-12-09 at 20.11.30" width="225" height="320" class="aligncenter size-medium wp-image-122816"
                srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-20.11.30-225x320.png 225w, https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-20.11.30-351x500.png 351w, https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-20.11.30.png 562w"
                sizes="(max-width: 225px) 100vw, 225px">
            </a>
        </p>
    </ol>
    <p>
        Select the
        <em>
            Label
        </em>
        , and in the
        <em>
            Attributes Inspector
        </em>
        set the following attributes:
    </p>
    <ol>
        <li>
            <em>
                Alignment
            </em>
            to
            <em>
                center
            </em>
        </li>
        <li>
            <em>
                Text Color
            </em>
            to
            <em>
                white
            </em>
        </li>
        <li>
            <em>
                Line Break
            </em>
            to
            <em>
                Truncate Tail
            </em>
        </li>
    </ol>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ConfigLabel.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ConfigLabel-700x391.png"
            alt="ConfigLabel" width="700" height="391" class="aligncenter size-large wp-image-121369"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ConfigLabel-700x391.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConfigLabel-480x268.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConfigLabel.png 813w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <h2>
        Add a CollectionViewItem to the Nib and Connect the Outlets
    </h2>
    <p>
        Though the
        <em>
            File’s Owner
        </em>
        in the nib is of the type
        <code>
            CollectionViewItem
        </code>
        , it is simply a placeholder. When the nib is instantiated, it must contain
        a “real” single top-level instance of
        <code>
            NSCollectionViewItem
        </code>
        .
    </p>
    <p>
        Drag a
        <em>
            Collection View Item
        </em>
        from the
        <em>
            Object Library
        </em>
        and drop it into
        <em>
            Document Outline
        </em>
        . Select it, and in the
        <em>
            Identity Inspector
        </em>
        , set its
        <em>
            Class
        </em>
        to
        <code>
            CollectionViewItem
        </code>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/TopLevelObject.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/TopLevelObject-700x318.png"
            alt="TopLevelObject" width="700" height="318" class="aligncenter size-large wp-image-121406"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/TopLevelObject-700x318.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/TopLevelObject-480x218.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/TopLevelObject.png 1074w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        In the
        <em>
            CollectionViewItem.xib
        </em>
        , you need to connect the view hierarchy to the outlets of
        <em>
            CollectionViewItem
        </em>
        . In the xib:
    </p>
    <ol>
        <li>
            Select
            <em>
                Collection View Item
            </em>
            and show the
            <em>
                Connections Inspector
            </em>
            .
        </li>
        <li>
            Drag from the
            <code>
                view
            </code>
            outlet to the
            <em>
                View
            </em>
            in the
            <em>
                Document Outline
            </em>
        </li>
        <li>
            In the same way, connect the
            <code>
                imageView
            </code>
            and
            <code>
                textField
            </code>
            outlets to
            <em>
                Image View
            </em>
            and
            <em>
                Label
            </em>
            in the
            <em>
                Document Outline
            </em>
        </li>
    </ol>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/ConnectItemOutlets-650x263.png"
        alt="ConnectItemOutlets" width="650" height="263" class="aligncenter size-large wp-image-145759"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/ConnectItemOutlets-650x263.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/ConnectItemOutlets-480x194.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/10/ConnectItemOutlets.png 703w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <h2>
        Populate the Collection View
    </h2>
    <p>
        You need to implement the data source protocol so the view knows the answers
        to these questions:
    </p>
    <ol>
        <li>
            How many sections are in the collection?
        </li>
        <li>
            How many items are in each section?
        </li>
        <li>
            Which item is associated with a specified index path?
        </li>
    </ol>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add the following extension at the end of the file:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1459785">
                    <td class="code" id="p145978code5">
                        <pre class="swift" style="font-family:monospace;">
                            extension ViewController : NSCollectionViewDataSource { &nbsp; // 1 func
                            numberOfSections(in collectionView: NSCollectionView) -&gt; Int { return
                            imageDirectoryLoader.numberOfSections } &nbsp; // 2 func collectionView(_
                            collectionView: NSCollectionView, numberOfItemsInSection section: Int)
                            -&gt; Int { return imageDirectoryLoader.numberOfItemsInSection(section)
                            } &nbsp; // 3 func collectionView(_ itemForRepresentedObjectAtcollectionView:
                            NSCollectionView, itemForRepresentedObjectAt indexPath: IndexPath) -&gt;
                            NSCollectionViewItem { &nbsp; // 4 let item = collectionView.makeItem(withIdentifier:
                            "CollectionViewItem", for: indexPath) guard let collectionViewItem = item
                            as? CollectionViewItem else {return item} &nbsp; // 5 let imageFile = imageDirectoryLoader.imageFileForIndexPath(indexPath)
                            collectionViewItem.imageFile = imageFile return item } &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <ol>
        <li>
            When your app doesn’t support sections, you can omit this method because
            a single section will be assumed.
        </li>
        <li>
            This is one of two required methods for
            <code>
                NSCollectionViewDataSource
            </code>
            . Here you return the number of items in the specified section.
        </li>
        <li>
            This is the second required method. It returns a collection view item
            for a given
            <code>
                indexPath
            </code>
            .
        </li>
        <li>
            This method instantiates an item from a nib where its name equals the
            value of the
            <code>
                identifier
            </code>
            parameter. It attempts to reuse an unused item of the requested type,
            and if nothing is available it creates a new one.
        </li>
        <li>
            Gets the model object for the given
            <code>
                IndexPath
            </code>
            and sets the content of the image and the label.
        </li>
    </ol>
    <div class="note">
        <em>
            Note
        </em>
        : The ability of the collection view to recycle unused collection view
        items provides a scalable solution for large collections. Items associated
        with model objects that aren’t visible are the objects that get recycled.
    </div>
    <h3>
        Set the Data Source
    </h3>
    <p>
        Your next step is to define the data source.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and select the collection view.
    </p>
    <p>
        Open the
        <em>
            Connections Inspector
        </em>
        and locate
        <em>
            dataSource
        </em>
        in the
        <em>
            Outlets
        </em>
        section.
        <em>
            Drag
        </em>
        from the adjacent button to the
        <em>
            View Controller
        </em>
        in
        <em>
            Document Outline View
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/SetAsDataSource.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/SetAsDataSource-700x202.png"
            alt="SetAsDataSource" width="700" height="202" class="aligncenter size-large wp-image-121329"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/SetAsDataSource-700x202.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/SetAsDataSource-480x139.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/SetAsDataSource.png 1053w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Build and run, and your collection view should display images from the
        <em>
            Desktop Pictures
        </em>
        folder:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/OneSectionFinal.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/OneSectionFinal-409x500.png"
            alt="OneSectionFinal" width="409" height="500" class="aligncenter size-large wp-image-121409"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/OneSectionFinal-409x500.png 409w, https://koenig-media.raywenderlich.com/uploads/2015/11/OneSectionFinal-262x320.png 262w, https://koenig-media.raywenderlich.com/uploads/2015/11/OneSectionFinal.png 960w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <p>
        Voilà! It was worth all that work!
    </p>
    <h3>
        Troubleshooting
    </h3>
    <p>
        If you don’t see images, then you probably just missed something small.
    </p>
    <ol>
        <li>
            Are all the connections in the
            <em>
                Connections Inspector
            </em>
            set as instructed?
        </li>
        <li>
            Did you set the
            <code>
                dataSource
            </code>
            outlet?
        </li>
        <li>
            Did you use the right type for custom classes in the
            <em>
                Identity Inspector
            </em>
            .
        </li>
        <li>
            Did you add the top level
            <code>
                NSCollectionViewItem
            </code>
            object and change its type to
            <code>
                CollectionViewItem
            </code>
            ?
        </li>
        <li>
            Is the value for the
            <code>
                identifier
            </code>
            parameter in
            <code>
                makeItemWithIdentifier
            </code>
            identical to the nib name?
        </li>
    </ol>
    <h2>
        Loading Items When the Model Changes
    </h2>
    <p>
        To display images from a folder other than the system’s
        <em>
            Desktop Pictures
        </em>
        folder, select
        <em>
            File/Open Another Folder…
        </em>
        and choose a folder that has image formats such as
        <em>
            jpg
        </em>
        or
        <em>
            png
        </em>
        .
    </p>
    <p>
        But nothing seems to change in the window — it still displays the images
        from the
        <em>
            Desktop Pictures
        </em>
        folder. Although when you look at the console log, you can see the file
        names are from the new folder.
    </p>
    <p>
        To refresh the collection view’s visible items, you need to call its
        <code>
            reloadData()
        </code>
        method.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add this code to the end of
        <code>
            loadDataForNewFolderWithUrl(_:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1459786">
                    <td class="code" id="p145978code6">
                        <pre class="swift" style="font-family:monospace;">
                            collectionView.reloadData()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run. You’ll now have the correct images displayed in the window.
    </p>
    <h2>
        Going Multi-Section
    </h2>
    <p>
        SlidesMagic is doing some serious magic now. But you’re going to improve
        it by adding sections.
    </p>
    <p>
        First, you need to add a check box to the bottom of the view so you can
        toggle between single and multi-section.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        , and in the
        <em>
            Document Outline
        </em>
        view, select the scroll view’s bottom constraint. Open the
        <em>
            Size Inspector
        </em>
        and change its
        <em>
            Constant
        </em>
        to 30.
    </p>
    <p>
        This moves the collection view up to make room for the check box.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/change-constraint.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/change-constraint-480x194.png"
            alt="change-constraint" width="480" height="194" class="aligncenter size-medium wp-image-122825"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/change-constraint-480x194.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/change-constraint-700x282.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Now, drag a
        <em>
            Check Box Button
        </em>
        from the
        <em>
            Object Library
        </em>
        into the space below the collection view. Select it, and in the
        <em>
            Attributes Inspector
        </em>
        , set its
        <em>
            Title
        </em>
        to
        <em>
            Show Sections
        </em>
        , and its
        <em>
            State
        </em>
        to
        <em>
            Off
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSections.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSections-700x425.png"
            alt="ShowSections" width="700" height="425" class="aligncenter size-large wp-image-121428"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSections-700x425.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSections-480x292.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSections.png 1180w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Then, set its
        <em>
            Auto Layout
        </em>
        constraints by selecting the
        <em>
            pin button
        </em>
        and set the
        <em>
            top
        </em>
        constraint to 8 and the
        <em>
            leading
        </em>
        constraint to 20. Choose
        <em>
            Update Frames: Items of New Constraints
        </em>
        and click
        <em>
            Add 2 Constraints
        </em>
        .
    </p>
    <p>
        Build and run. It should look like this at the bottom:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSectionsBottom.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSectionsBottom-700x263.png"
            alt="ShowSectionsBottom" width="700" height="263" class="aligncenter size-large wp-image-121431"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSectionsBottom-700x263.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSectionsBottom-480x180.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSectionsBottom.png 960w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        When you click the box, the application needs to change the collection
        view’s appearance.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add the following method at the end of the
        <code>
            ViewController
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1459787">
                    <td class="code" id="p145978code7">
                        <pre class="swift" style="font-family:monospace;">
                            @IBAction func showHideSections(sender: NSButton) { let show = sender.state
                            // 1 imageDirectoryLoader.singleSectionMode = (show == NSOffState) // 2
                            imageDirectoryLoader.setupDataForUrls(nil) // 3 collectionView.reloadData()
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s what you’re doing:
    </p>
    <ol>
        <li>
            Setting single or multi-section mode according to the state of the box.
        </li>
        <li>
            You rearrange the model according to the selected mode. The
            <code>
                nil
            </code>
            value passed means you skip image loading — same images, different layout.
        </li>
        <li>
            Model changed, discard visible items and redisplay them.
        </li>
    </ol>
    <p>
        If you’re curious how images are distributed across sections, look up
        <code>
            sectionLengthArray
        </code>
        in
        <code>
            ImageDirectoryLoader
        </code>
        . The number of elements in this array sets the max number of sections,
        and the element values set the number of items in each section.
    </p>
    <p>
        Now, open
        <em>
            Main.storyboard
        </em>
        . In the
        <em>
            Document Outline
        </em>
        ,
        <em>
            Control-drag
        </em>
        from the
        <em>
            Show Sections
        </em>
        control over the
        <em>
            View Controller
        </em>
        . In the black pop-up window click
        <em>
            showHideSections:
        </em>
        to connect it. You can check if the connection was set properly in the
        <em>
            Connections Inspector
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectShowSections.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectShowSections-700x247.png"
            alt="ConnectShowSections" width="700" height="247" class="aligncenter size-large wp-image-121433"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectShowSections-700x247.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectShowSections-480x170.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectShowSections.png 954w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Build and run; check
        <em>
            Show Sections
        </em>
        and watch the layout change.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/SectionsShowing.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/SectionsShowing-409x500.png"
            alt="SectionsShowing" width="409" height="500" class="aligncenter size-large wp-image-121432"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/SectionsShowing-409x500.png 409w, https://koenig-media.raywenderlich.com/uploads/2015/11/SectionsShowing-262x320.png 262w, https://koenig-media.raywenderlich.com/uploads/2015/11/SectionsShowing.png 960w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <p>
        To get better visual separation between sections, open
        <em>
            ViewController.swift
        </em>
        and modify the layout’s
        <code>
            sectionInset
        </code>
        property in the
        <code>
            configureCollectionView()
        </code>
        method.
    </p>
    <p>
        Replace:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1459788">
                    <td class="code" id="p145978code8">
                        <pre class="swift" style="font-family:monospace;">
                            flowLayout.sectionInset = EdgeInsets(top: 10.0, left: 20.0, bottom: 10.0,
                            right: 20.0)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        With this:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1459789">
                    <td class="code" id="p145978code9">
                        <pre class="swift" style="font-family:monospace;">
                            flowLayout.sectionInset = EdgeInsets(top: 30.0, left: 20.0, bottom: 30.0,
                            right: 20.0)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run; check
        <em>
            Show Sections
        </em>
        , and note the additional spacing between sections.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/SectionInsets.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/SectionInsets-409x500.png"
            alt="SectionInsets" width="409" height="500" class="aligncenter size-large wp-image-121435"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/SectionInsets-409x500.png 409w, https://koenig-media.raywenderlich.com/uploads/2015/11/SectionInsets-262x320.png 262w, https://koenig-media.raywenderlich.com/uploads/2015/11/SectionInsets.png 960w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <h2>
        Add Section Headers
    </h2>
    <p>
        Another way to see section boundaries is to add a header or footer view.
        To do this, you need a custom
        <code>
            NSView
        </code>
        class and will need to implement a data source method to provide the header
        views to the collection view.
    </p>
    <p>
        To create the header view, select
        <em>
            File/New/File…
        </em>
        . Select
        <em>
            macOS/User Interface/View
        </em>
        and click
        <em>
            Next
        </em>
        .
    </p>
    <p>
        Enter
        <em>
            HeaderView.xib
        </em>
        as the file name and for
        <em>
            Group
        </em>
        select
        <em>
            Resources
        </em>
        .
    </p>
    <p>
        Click
        <em>
            Create
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderView.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderView-700x297.png"
            alt="HeaderView" width="700" height="297" class="aligncenter size-large wp-image-121443"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderView-700x297.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderView-480x204.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderView.png 1067w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Open
        <em>
            HeaderView.xib
        </em>
        and select the
        <em>
            Custom View
        </em>
        . Open the
        <em>
            Size Inspector
        </em>
        and change
        <em>
            Width
        </em>
        to 500 and
        <em>
            Height
        </em>
        to 40.
    </p>
    <p>
        Drag a label from the
        <em>
            Object Library
        </em>
        to the left-hand side of
        <em>
            Custom View
        </em>
        . Open the
        <em>
            Attributes Inspector
        </em>
        and change
        <em>
            Title
        </em>
        to
        <em>
            Section Number
        </em>
        and
        <em>
            Font Size
        </em>
        to
        <em>
            16
        </em>
        .
    </p>
    <p>
        Drag a second label to the right-hand side of
        <em>
            Custom View
        </em>
        and change
        <em>
            Title
        </em>
        to
        <em>
            Images Count
        </em>
        and
        <em>
            Alignment
        </em>
        to
        <em>
            Right
        </em>
        .
    </p>
    <p>
        Set the
        <em>
            Section Number
        </em>
        labels
        <em>
            Auto Layout
        </em>
        constraints by selecting the
        <em>
            pin button
        </em>
        and set the
        <em>
            top
        </em>
        constraint to 12 and the
        <em>
            leading
        </em>
        constraint to 20. Choose
        <em>
            Update Frames: Items of New Constraints
        </em>
        and click
        <em>
            Add 2 Constraints
        </em>
        .
    </p>
    <p>
        Next, set the
        <em>
            Images Count
        </em>
        labels
        <em>
            top
        </em>
        constraint to 11 and the
        <em>
            trailing
        </em>
        constraint to 20. Be sure to choose
        <em>
            Update Frames: Items of New Constraints
        </em>
        and click
        <em>
            Add 2 Constraints
        </em>
        .
    </p>
    <p>
        The header view should look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderControls.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderControls-700x202.png"
            alt="HeaderControls" width="700" height="202" class="aligncenter size-large wp-image-121450"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderControls-700x202.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderControls-480x138.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/HeaderControls.png 1290w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        With the interface ready for show time, the next task is to create a custom
        view subclass for the header view.
    </p>
    <p>
        Select
        <em>
            File/New/File…
        </em>
        to create a new file.
    </p>
    <p>
        Choose
        <em>
            macOS/Source/Cocoa Class
        </em>
        , name the class
        <code>
            HeaderView
        </code>
        , and then make it a subclass of
        <code>
            NSView
        </code>
        . Click Next, and for
        <em>
            Group
        </em>
        select
        <em>
            Views
        </em>
        . Click
        <em>
            Create
        </em>
        .
    </p>
    <p>
        Open
        <em>
            HeaderView.swift
        </em>
        and replace the contents of the class with the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14597810">
                    <td class="code" id="p145978code10">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 @IBOutlet weak var sectionTitle: NSTextField! @IBOutlet weak var
                            imageCount: NSTextField! &nbsp; // 2 override func draw(_ dirtyRect: NSRect)
                            { super.draw(dirtyRect) NSColor(calibratedWhite: 0.8 , alpha: 0.8).set()
                            NSRectFillUsingOperation(dirtyRect, NSCompositingOperation.sourceOver)
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        In here, you’re:
    </p>
    <ol>
        <li>
            Setting up outlets you’ll use to connect to the labels in the nib.
        </li>
        <li>
            Drawing a gray background.
        </li>
    </ol>
    <p>
        To connect the outlets to the labels, open
        <em>
            HeaderView.xib
        </em>
        and select the
        <em>
            Custom View
        </em>
        . Open the
        <em>
            Identity Inspector
        </em>
        and change the
        <em>
            Class
        </em>
        to
        <em>
            HeaderView
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-22.50.57.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-22.50.57-480x196.png"
            alt="Screen Shot 2015-12-09 at 22.50.57" width="480" height="196" class="aligncenter size-small wp-image-122895"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-22.50.57-480x196.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Screen-Shot-2015-12-09-at-22.50.57.png 520w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        In the
        <em>
            Document Outline
        </em>
        view,
        <em>
            Control-click
        </em>
        on the
        <em>
            Header View
        </em>
        . In the black pop-up window,
        <em>
            drag
        </em>
        from
        <em>
            imageCount
        </em>
        to the
        <em>
            Images Count
        </em>
        label on the canvas to connect the outlet.
    </p>
    <p>
        Repeat the operation for the second label, dragging from
        <em>
            sectionTitle
        </em>
        to the
        <em>
            Section Number
        </em>
        label in the canvas.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectHeaderControls.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectHeaderControls-700x242.png"
            alt="ConnectHeaderControls" width="700" height="242" class="aligncenter size-large wp-image-121459"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectHeaderControls-700x242.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectHeaderControls-480x166.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectHeaderControls.png 1329w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <h3>
        Implement the Data Source and Delegate Methods
    </h3>
    <p>
        Your header view is in place and ready to go, and you need to pass the
        header views to the collection view to implement
        <code>
            collectionView(_:viewForSupplementaryElementOfKind:at:)
        </code>
        .
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and add the following method to the
        <code>
            NSCollectionViewDataSource
        </code>
        extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14597811">
                    <td class="code" id="p145978code11">
                        <pre class="swift" style="font-family:monospace;">
                            func collectionView(_ collectionView: NSCollectionView, viewForSupplementaryElementOfKind
                            kind: String, at indexPath: IndexPath) -&gt; NSView { // 1 let view = collectionView.makeSupplementaryView(ofKind:
                            NSCollectionElementKindSectionHeader, withIdentifier: "HeaderView", for:
                            indexPath) as! HeaderView // 2 view.sectionTitle.stringValue = "Section
                            \(indexPath.section)" let numberOfItemsInSection = imageDirectoryLoader.numberOfItemsInSection(indexPath.section)
                            view.imageCount.stringValue = "\(numberOfItemsInSection) image files" return
                            view }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The collection view calls this method when it needs the data source to
        provide a header for a section. The method does the following:
    </p>
    <ol>
        <li>
            Calls
            <code>
                makeSupplementaryViewOfKind(_:withIdentifier:for:)
            </code>
            to instantiate a
            <code>
                HeaderView
            </code>
            object using the nib with a name equal to
            <code>
                withIdentifier
            </code>
            .
        </li>
        <li>
            Sets the values for the labels.
        </li>
    </ol>
    <p>
        At the end of
        <em>
            ViewController.swift
        </em>
        , add this
        <code>
            NSCollectionViewDelegateFlowLayout
        </code>
        extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14597812">
                    <td class="code" id="p145978code12">
                        <pre class="swift" style="font-family:monospace;">
                            extension ViewController : NSCollectionViewDelegateFlowLayout { func collectionView(_
                            collectionView: NSCollectionView, layout collectionViewLayout: NSCollectionViewLayout,
                            referenceSizeForHeaderInSection section: Int) -&gt; NSSize { return imageDirectoryLoader.singleSectionMode
                            ? NSZeroSize : NSSize(width: 1000, height: 40) } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The above method, although technically optional, is a must when you use
        headers because the flow layout delegate needs to provide the size of the
        header for every section.
    </p>
    <p>
        When not implemented, the header won’t show because zero size is assumed.
        Additionally, it ignores the specified width, effectively setting it to
        the collection view’s width.
    </p>
    <p>
        In this case, the method returns a size of zero when the collection view
        is in single section mode, and it returns 40 when in multiple sections
        mode.
    </p>
    <p>
        For the collection view to use
        <code>
            NSCollectionViewDelegateFlowLayout
        </code>
        , you must connect
        <code>
            ViewController
        </code>
        to the
        <code>
            delegate
        </code>
        outlet of
        <code>
            NSCollectionView
        </code>
        .
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and select the collection view. Open the
        <em>
            Connections Inspector
        </em>
        , and locate the
        <em>
            delegate
        </em>
        in the
        <em>
            Outlets
        </em>
        section.
        <em>
            Drag
        </em>
        from the button next to it to the view controller in the
        <em>
            Document Outline
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectTheDelegate.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectTheDelegate.png"
            alt="ConnectTheDelegate" width="319" height="383" class="aligncenter size-full wp-image-121461"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectTheDelegate.png 319w, https://koenig-media.raywenderlich.com/uploads/2015/11/ConnectTheDelegate-267x320.png 267w"
            sizes="(max-width: 319px) 100vw, 319px">
        </a>
    </p>
    <p>
        Build and run; check
        <em>
            Show Sections
        </em>
        and watch your header neatly define sections:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/WithHeaders.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/WithHeaders-409x500.png"
            alt="WithHeaders" width="409" height="500" class="aligncenter size-large wp-image-121462"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/WithHeaders-409x500.png 409w, https://koenig-media.raywenderlich.com/uploads/2015/11/WithHeaders-262x320.png 262w, https://koenig-media.raywenderlich.com/uploads/2015/11/WithHeaders.png 960w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <h2>
        Sticky Headers
    </h2>
    <p>
        New to macOS 10.12 are the
        <code>
            NSCollectionViewFlowLayout
        </code>
        properties
        <code>
            sectionHeadersPinToVisibleBounds
        </code>
        and
        <code>
            sectionFootersPinToVisibleBounds
        </code>
        .
    </p>
    <p>
        When
        <code>
            sectionHeadersPinToVisibleBounds
        </code>
        is set to
        <code>
            true
        </code>
        , the header view for the topmost visible section will stay pinned to
        the top of the scroll area instead of being scrolled out of view. As you
        scroll down, the header stays pinned to the top until the next section’s
        header pushes it out of the way. This behavior is referred to as “sticky
        headers” or “floating headers”.
    </p>
    <p>
        Setting
        <code>
            sectionFootersPinToVisibleBounds
        </code>
        to
        <code>
            true
        </code>
        behaves similarly, pinning footers to the bottom of the scroll area.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        and at the end of
        <code>
            configureCollectionView()
        </code>
        add the line:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14597813">
                    <td class="code" id="p145978code13">
                        <pre class="swift" style="font-family:monospace;">
                            flowLayout.sectionHeadersPinToVisibleBounds = true
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run. Check
        <em>
            Show Sections
        </em>
        and scroll up a bit so the first row partially scrolls out of view.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/CV-StickyHeaders.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/CV-StickyHeaders-650x362.png"
            alt="CV-StickyHeaders" width="650" height="362" class="aligncenter size-large wp-image-146534"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/CV-StickyHeaders-650x362.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/CV-StickyHeaders-480x267.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/10/CV-StickyHeaders.png 952w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Watch how the first section header is still visible and the first row
        shows through the section header.
    </p>
    <div class="note">
        <em>
            Note
        </em>
        : If your app needs to support OS X 10.11 as well, you will need to implement
        sticky headers “manually” by creating a subclass of
        <code>
            NSCollectionViewFlowLayout
        </code>
        and overriding the
        <code>
            layoutAttributesForElements(in:)
        </code>
        method. This is described in detail in our
        <a href="https://www.raywenderlich.com/132268/advanced-collection-views-os-x-tutorial"
        target="_blank">
            Advanced Collection Views in OS X Tutorial
        </a>
        .
    </div>
    <h2>
        Selection in Collection Views
    </h2>
    <p>
        To show an item as selected, you’ll set a white border, non-selected items
        will have no border.
    </p>
    <p>
        First, you need to make the collection view selectable. Open the
        <em>
            Main.storyboard
        </em>
        , select the
        <em>
            Collection View
        </em>
        and in the
        <em>
            Attributes Inspector
        </em>
        , check
        <em>
            Selectable
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/SelectionAttributes.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/SelectionAttributes.png"
            alt="SelectionAttributes" width="316" height="374" class="aligncenter size-full wp-image-121466"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/SelectionAttributes.png 316w, https://koenig-media.raywenderlich.com/uploads/2015/11/SelectionAttributes-270x320.png 270w"
            sizes="(max-width: 316px) 100vw, 316px">
        </a>
    </p>
    <p>
        Checking
        <em>
            Selectable
        </em>
        enables single selection, meaning you can click an item to select it.
        When you choose a different item, it deselects the previous item and selects
        the item you just picked.
    </p>
    <p>
        When you select an item:
    </p>
    <ol>
        <li>
            Its
            <code>
                IndexPath
            </code>
            is added to the
            <code>
                selectionIndexPaths
            </code>
            property of
            <code>
                NSCollectionView
            </code>
            .
        </li>
        <li>
            The
            <code>
                isSelected
            </code>
            property of the associated
            <code>
                NSCollectionViewItem
            </code>
            is set to
            <code>
                true
            </code>
            .
        </li>
    </ol>
    <p>
        Open
        <em>
            CollectionViewItem.swift
        </em>
        . Add the following at the end of
        <code>
            viewDidLoad()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14597814">
                    <td class="code" id="p145978code14">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 view.layer?.borderColor = NSColor.white.cgColor // 2 view.layer?.borderWidth
                            = 0.0
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <ol>
        <li>
            Sets white for the border when its width is greater than zero
        </li>
        <li>
            Sets
            <code>
                borderWidth
            </code>
            to
            <code>
                0.0
            </code>
            to guarantee that a new item has no border&nbsp;— i.e, not selected
        </li>
    </ol>
    <p>
        To set the
        <code>
            borderWidth
        </code>
        each time the
        <code>
            isSelected
        </code>
        property changes add the following code at the top of the
        <code>
            CollectionViewItem
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14597815">
                    <td class="code" id="p145978code15">
                        <pre class="swift" style="font-family:monospace;">
                            override var isSelected: Bool { didSet { view.layer?.borderWidth = isSelected
                            ? 5.0 : 0.0 } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Whenever
        <code>
            isSelected
        </code>
        is changed,
        <code>
            didSet
        </code>
        will add or remove the white border according the new value of the property.
    </p>
    <div class="note">
        <em>
            Note
        </em>
        : The
        <code>
            isSelected
        </code>
        property is not always the right way to test whether an item is selected
        or not. When an item is outside the collection view’s
        <code>
            visibleRect
        </code>
        the collection view isn’t maintaining an
        <code>
            NSCollectionViewItem
        </code>
        instance for this item. If this is the case than the collection view’s
        <code>
            item(at:)
        </code>
        method will return
        <code>
            nil
        </code>
        . A general way to check whether an item is selected or not is to check
        whether the collection view’s
        <code>
            selectionIndexPaths
        </code>
        property contains the index path in question.
    </div>
    <p>
        Build and run.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSelection.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSelection-409x500.png"
            alt="ShowSelection" width="409" height="500" class="aligncenter size-large wp-image-121470"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSelection-409x500.png 409w, https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSelection-262x320.png 262w, https://koenig-media.raywenderlich.com/uploads/2015/11/ShowSelection.png 960w"
            sizes="(max-width: 409px) 100vw, 409px">
        </a>
    </p>
    <p>
        Click an item and you’ll see highlighting. Choose a different image and
        you’ll see fully functional highlighting. Poof! Magic!
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
        Download the final version of
        <em>
            SlidesMagic
        </em>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/SlidesMagic8V3-Final.zip">
            here
        </a>
        .
    </p>
    <p>
        In this NSCollectionView tutorial, you went all the way from creating
        your first ever collection view, through discovering the intricacies of
        the data source API with sections, to handling selection. Although you
        covered a lot of ground, you’ve only started to explore the capabilities
        of collection views. Here are more great things to check out:
    </p>
    <ul>
        <li>
            “Data Source-less” collection views using Cocoa Bindings
        </li>
        <li>
            Different kind of items
        </li>
        <li>
            Adding and removing items
        </li>
        <li>
            Custom layouts
        </li>
        <li>
            Drag and drop
        </li>
        <li>
            Animations
        </li>
        <li>
            Tweaking
            <code>
                NSCollectionViewFlowLayout
            </code>
        </li>
        <li>
            Collapsible Sections (new in macOS 10.12)
        </li>
    </ul>
    <p>
        Some of these topics are covered in our
        <a href="https://www.raywenderlich.com/132268/advanced-collection-views-os-x-tutorial"
        target="_blank">
            Advanced Collection Views in OS X Tutorial
        </a>
        .
    </p>
    <p>
        The video, documents, and code in the list below are recommended to get
        an even better understanding of collection views:
    </p>
    <ul>
        <li>
            <a href="https://developer.apple.com/videos/play/wwdc2015-225/" target="_blank">
                WWDC 2015 – Session 225 – What’s New in NSCollectionView
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/mac/releasenotes/AppKit/RN-AppKitOlderNotes/#10_11CollectionView"
            target="_blank">
                AppKit Release Notes (OS X v10.11)
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/content/releasenotes/AppKit/RN-AppKit/#10_12NSCollectionView"
            target="_blank">
                AppKit Release Notes for macOS 10.12
            </a>
        </li>
        <li>
            <a href="https://developer.apple.com/library/prerelease/mac/samplecode/CocoaSlideCollection/Introduction/Intro.html"
            target="_blank">
                CocoaSlideCollection
            </a>
            – Sample code of WWDC Session 225 above. Written in Objective-C
        </li>
        <li>
            <a href="https://developer.apple.com/library/prerelease/mac/samplecode/Exhibition/Listings/Exhibition_ImageListController_swift.html"
            target="_blank">
                Exhibition
            </a>
            – Sample code from Apple, written in Swift using
            <code>
                NSCollectionViewGridLayout
            </code>
        </li>
    </ul>
</div>