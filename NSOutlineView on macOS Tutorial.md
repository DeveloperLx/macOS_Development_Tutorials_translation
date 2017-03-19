# OS X Stack Views：NSStackView

#### [原文地址](https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div class="note">
        <p>
            <em>
                Update 9/30/16:
            </em>
            This tutorial has been updated for Xcode 8 and Swift 3.
        </p>
    </div>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature-250x250.png"
        alt="NSOutlineView-feature" width="250" height="250" class="alignright size-thumbnail wp-image-126006"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/02/NSOutlineView-feature-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
        When writing applications, you often want to show data that has a list-like
        structure. For example, you might want to display a list of recipes. This
        can be easily done with a
        <code>
            NSTableView
        </code>
        . But what if you want to group the recipes by appetizer or main course?
        Now you have a problem, because table views have no sections. Your five-layer-dip
        recipe is right next to your linguine del mare recipe, which just won’t
        do!
    </p>
    <p>
        Thankfully,
        <code>
            NSOutlineView
        </code>
        provides a lot more functionality.
        <code>
            NSOutlineView
        </code>
        is a common component in macOS applications, and is a subclass of
        <code>
            NSTableView
        </code>
        . Like a table view, it uses rows and columns to display its content;
        unlike a table view, it uses a hierarchical data structure.
    </p>
    <p>
        To see an outline view in action, open Xcode with an existing project
        and have a look at the project navigator. Click on the triangle next to
        the project name to expand it. You’ll see a structure like the image below:
        beneath the project are groups, and inside the groups are Swift or Objective-C
        files.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Outline_Xcode.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Outline_Xcode.png"
            alt="Xcode's Outline View" width="242" height="228" class="aligncenter size-full wp-image-123488"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Outline_Xcode.png 484w, https://koenig-media.raywenderlich.com/uploads/2015/12/Outline_Xcode-340x320.png 340w"
            sizes="(max-width: 242px) 100vw, 242px">
        </a>
    </p>
    <p>
        In this NSOutlineView on macOS tutorial, you will learn how to use an
        outline view to show your own hierarchical data. To do this, you’ll write
        a RSS Reader-like application that loads RSS Feeds from a file and shows
        them in an outline view.
    </p>
    <h2>
        Getting Started
    </h2>
    <p>
        The starter project can be downloaded
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/Reader_Starter.zip"
        sl-processed="1">
            here
        </a>
        . Open the project and take a peek. Besides the files created by the template,
        there is a
        <em>
            Feeds.plist
        </em>
        , which is the file you’ll load the feeds from. You’ll take a closer look
        at it later, when creating the model classes.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        to see the prepared UI. On the left is a plain outline view, and beside
        it is a white area, which is the web view. Those are grouped using a horizontal
        stack view, which is pinned to the window edges. Stack views are the latest
        and greatest way to deal with Auto Layout, if you haven’t yet given them
        a try. You can learn all about them in
        <a href="http://www.raywenderlich.com/122295/os-x-stack-views-nsstackview"
        sl-processed="1">
            Marin’s great tutorial about NSStackViews
        </a>
        .
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/starter_ui-2"
        rel="attachment wp-att-124504" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Starter_UI-480x302.png"
            alt="Starter UI" width="480" height="302" class="aligncenter size-medium wp-image-124504"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Starter_UI-480x302.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Starter_UI-768x483.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/Starter_UI-700x440.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/Starter_UI.png 1564w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Your first task: complete the UI. To do this, double-click in the header
        to change the title. For the first column, change it to
        <em>
            Feed
        </em>
        ; change the second to
        <em>
            Date
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Header.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Header.png"
            alt="Change_Header" width="318" height="153" class="aligncenter size-full wp-image-123490"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Header.png 636w, https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Header-480x231.png 480w"
            sizes="(max-width: 318px) 100vw, 318px">
        </a>
    </p>
    <p>
        That was easy! Now select the outline view, in the document outline —
        you’ll find it under
        <em>
            Bordered Scroll View – Outline View \ Clip View \ Outline View
        </em>
        . In the
        <em>
            Attributes Inspector
        </em>
        , change
        <em>
            Indentation
        </em>
        to 5, enable
        <em>
            Floats Group Rows
        </em>
        and disable
        <em>
            Reordering
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/01/nsoutline-inspector-new.png"
        rel="attachment wp-att-124331" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/nsoutline-inspector-new-296x320.png"
            alt="nsoutline-inspector-new" width="296" height="320" class="aligncenter size-medium wp-image-124331"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/nsoutline-inspector-new-296x320.png 296w, https://koenig-media.raywenderlich.com/uploads/2016/01/nsoutline-inspector-new.png 463w"
            sizes="(max-width: 296px) 100vw, 296px">
        </a>
    </p>
    <p>
        Inside the document outline on the left, click on the triangle beside
        <em>
            Outline View
        </em>
        to expand it. Do the same for
        <em>
            Feed
        </em>
        and
        <em>
            Date
        </em>
        . Select the Table View Cell below
        <em>
            Date
        </em>
        .
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/date_selection"
        rel="attachment wp-att-124505" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Date_Selection-468x320.png"
            alt="Date_Selection" width="234" height="160" class="aligncenter size-medium wp-image-124505"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Date_Selection-468x320.png 468w, https://koenig-media.raywenderlich.com/uploads/2016/01/Date_Selection.png 638w"
            sizes="(max-width: 234px) 100vw, 234px">
        </a>
    </p>
    <p>
        Change the
        <em>
            Identifier
        </em>
        to
        <em>
            DateCell
        </em>
        in
        <em>
            Identity Inspector
        </em>
        .
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/change_cell_identifier-2"
        rel="attachment wp-att-124506" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Change_Cell_Identifier-480x301.png"
            alt="Change_Cell_Identifier" width="480" height="301" class="aligncenter size-medium wp-image-124506"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Change_Cell_Identifier-480x301.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Change_Cell_Identifier.png 530w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Now show the
        <em>
            Size Inspector
        </em>
        and change
        <em>
            Width
        </em>
        to 102. Repeat this step for the cell below Feed, changing the
        <em>
            Identifier
        </em>
        to
        <em>
            FeedCell
        </em>
        and
        <em>
            Width
        </em>
        to 320.
    </p>
    <p>
        Expand the cell below feed and select the text field named
        <em>
            Table View Cell
        </em>
        .
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/selected_textfield"
        rel="attachment wp-att-124507" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Selected_Textfield.png"
            alt="Selected_Textfield" width="438" height="190" class="aligncenter size-full wp-image-124507">
        </a>
    </p>
    <p>
        Use the Pin and Align menus on the Auto Layout toolbar to add an Auto
        Layout constraint of 2 points leading, plus another constraint to center
        the text field vertically. You will see the constraints in
        <em>
            Size Inspector
        </em>
        :
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/constraints-5"
        rel="attachment wp-att-124508" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Constraints-480x163.png"
            alt="Constraints" width="480" height="163" class="aligncenter size-medium wp-image-124508"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Constraints-480x163.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Constraints.png 490w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Now select the table cell again (above the text field in the layout hierarchy).
        Duplicate it by pressing
        <em>
            Cmd + C
        </em>
        and
        <em>
            Cmd + V
        </em>
        , then change the
        <em>
            Identifier
        </em>
        of the duplicate to
        <em>
            FeedItemCell
        </em>
        . Now you have 3 different cells, one for each type of entry that will
        be shown in the outline view.
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/finishedcells"
        rel="attachment wp-att-124510" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/FinishedCells.png"
            alt="FinishedCells" width="468" height="304" class="aligncenter size-full wp-image-124510">
        </a>
    </p>
    <p>
        Select
        <em>
            Date
        </em>
        , and in the
        <em>
            Identity Inspector
        </em>
        change the Identifier to
        <em>
            DateColumn
        </em>
        ; do the same for
        <em>
            Feed
        </em>
        and change it to
        <em>
            TitleColumn
        </em>
        :
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/titlecolumn"
        rel="attachment wp-att-124512" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/TitleColumn-480x255.png"
            alt="TitleColumn" width="480" height="255" class="aligncenter size-medium wp-image-124512"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/TitleColumn-480x255.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/TitleColumn.png 512w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        The final step is to give the outline view a delegate and a data source.
        Select the outline view and right- or control-click on it. Drag a line
        from
        <em>
            dataSource
        </em>
        to the
        <em>
            blue circle
        </em>
        that represents your view controller; repeat this to set the delegate.
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/add_delegate"
        rel="attachment wp-att-123505" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Add_Delegate-480x202.png"
            alt="Add_Delegate" width="480" height="202" class="aligncenter size-medium wp-image-123505"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Add_Delegate-480x202.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Add_Delegate-700x294.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/12/Add_Delegate.png 1172w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Run the project and you’ll see …
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/first_run-5"
        rel="attachment wp-att-123493" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/First_Run-480x318.png"
            alt="First_Run" width="480" height="318" class="aligncenter size-medium wp-image-123493"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/First_Run-480x318.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/First_Run-700x464.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        There’s an empty outline view and an error message in your console, saying
        you have an illegal data source. What’s wrong?
    </p>
    <p>
        Before you can fill the outline view and get rid of the error message,
        you need a data model.
    </p>
    <h2>
        Data Model
    </h2>
    <p>
        The data model for an outline view is a bit different than the one for
        a table view. Like mentioned in the introduction, an outline view shows
        a hierarchical data model, and your model classes have to represent this
        hierarchy. Every hierarchy has a top level or root object. Here this will
        be a RSS Feed; the name of the feed is the root.
    </p>
    <p>
        Press
        <em>
            Cmd + N
        </em>
        to create a new class. Inside the
        <em>
            macOS
        </em>
        section select
        <em>
            Cocoa Class
        </em>
        and click
        <em>
            Next
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/New_File_Template.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/New_File_Template-449x320.png"
            alt="New_File_Template" width="449" height="320" class="aligncenter size-medium wp-image-145290"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/New_File_Template-449x320.png 449w, https://koenig-media.raywenderlich.com/uploads/2016/04/New_File_Template-650x463.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/04/New_File_Template.png 1460w"
            sizes="(max-width: 449px) 100vw, 449px">
        </a>
    </p>
    <p>
        Name the class
        <code>
            Feed
        </code>
        and make it a subclass of
        <code>
            NSObject
        </code>
        . Then click
        <em>
            Next
        </em>
        and
        <em>
            Create
        </em>
        on the next screen.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Create_Feed_Class_2.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Create_Feed_Class_2-700x497.png"
            alt="Create_Feed_Class_2" width="350" height="248" class="aligncenter size-large wp-image-123495"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Create_Feed_Class_2-700x497.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/12/Create_Feed_Class_2-451x320.png 451w, https://koenig-media.raywenderlich.com/uploads/2015/12/Create_Feed_Class_2.png 1462w"
            sizes="(max-width: 350px) 100vw, 350px">
        </a>
    </p>
    <p>
        Replace the automatically generated code with:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1234631">
                    <td class="code" id="p123463code1">
                        <pre class="swift" style="font-family:monospace;">
                            import Cocoa &nbsp; class Feed: NSObject { let name: String &nbsp; init(name:
                            String) { self.name = name } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This adds a
        <code>
            name
        </code>
        property to your class and provides an init method that sets the property
        to a provided value. Your class will store its children in an array, but
        before you can do this, you need to create a class for those children.
        Using the same procedure as before, add a new file for the
        <code>
            FeedItem
        </code>
        class. Open the newly created
        <em>
            FeedItem.swift
        </em>
        and replace the content with the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1234632">
                    <td class="code" id="p123463code2">
                        <pre class="swift" style="font-family:monospace;">
                            import Cocoa &nbsp; class FeedItem: NSObject { let url: String let title:
                            String let publishingDate: Date &nbsp; init(dictionary: NSDictionary) {
                            self.url = dictionary.object(forKey: "url") as! String self.title = dictionary.object(forKey:
                            "title") as! String self.publishingDate = dictionary.object(forKey: "date")
                            as! Date } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This is another simple model class:
        <code>
            FeedItem
        </code>
        has a
        <code>
            url
        </code>
        that you will use to load the corresponding article into the web view;
        a
        <code>
            title
        </code>
        ; and a
        <code>
            publishingDate
        </code>
        . The initializer takes a dictionary as its parameter. This could be received
        from a web service or, in this case, from a plist file.
    </p>
    <p>
        Head back to
        <em>
            Feed.swift
        </em>
        and add the following property to
        <code>
            Feed
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1234633">
                    <td class="code" id="p123463code3">
                        <pre class="swift" style="font-family:monospace;">
                            var children = [FeedItem]()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This creates an empty array to store
        <em>
            FeedItem
        </em>
        objects.
    </p>
    <p>
        Now add the following class method to
        <code>
            Feed
        </code>
        to load the plist:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1234634">
                    <td class="code" id="p123463code4">
                        <pre class="swift" style="font-family:monospace;">
                            class func feedList(_ fileName: String) -&gt; [Feed] { //1 var feeds =
                            [Feed]() &nbsp; //2 if let feedList = NSArray(contentsOfFile: fileName)
                            as? [NSDictionary] { //3 for feedItems in feedList { //4 let feed = Feed(name:
                            feedItems.object(forKey: "name") as! String) //5 let items = feedItems.object(forKey:
                            "items") as! [NSDictionary] //6 for dict in items { //7 let item = FeedItem(dictionary:
                            dict) feed.children.append(item) } //8 feeds.append(feed) } } &nbsp; //9
                            return feeds }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The method gets a file name as its argument and returns an array of
        <code>
            Feed
        </code>
        objects. This code:
    </p>
    <ol>
        <li>
            Creates an empty
            <code>
                Feed
            </code>
            array.
        </li>
        <li>
            Tries to load an array of dictionaries from the file.
        </li>
        <li>
            If this worked, loops through the entries.
        </li>
        <li>
            The dictionary contains a key
            <em>
                name
            </em>
            that is used to inititalize
            <code>
                Feed
            </code>
            .
        </li>
        <li>
            The key
            <em>
                items
            </em>
            contains another array of dictionaries.
        </li>
        <li>
            Loops through the dictionaries.
        </li>
        <li>
            Initializes a
            <code>
                FeedItem
            </code>
            . This item is appended to the
            <code>
                children
            </code>
            array of the parent
            <code>
                Feed
            </code>
            .
        </li>
        <li>
            After the loop, every child for the
            <code>
                Feed
            </code>
            is added to the
            <code>
                feeds
            </code>
            array before the next
            <code>
                Feed
            </code>
            starts loading.
        </li>
        <li>
            Returns the
            <code>
                feeds
            </code>
            . If everything worked as expected, this array will contain 2
            <code>
                Feed
            </code>
            objects.
        </li>
    </ol>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        , and below the IBOutlet section add a property to store feeds:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1234635">
                    <td class="code" id="p123463code5">
                        <pre class="swift" style="font-family:monospace;">
                            var feeds = [Feed]()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Find
        <code>
            viewDidLoad()
        </code>
        and add the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1234636">
                    <td class="code" id="p123463code6">
                        <pre class="swift" style="font-family:monospace;">
                            if let filePath = Bundle.main.path(forResource: "Feeds", ofType: "plist")
                            { feeds = Feed.feedList(filePath) print(feeds) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Run the project; you should see something like this in your console:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1234637">
                    <td class="code" id="p123463code7">
                        <pre class="bash" style="font-family:monospace;">
                            <span style="color: #7a0874; font-weight: bold;">
                                [
                            </span>
                            <span style="color: #000000; font-weight: bold;">
                                &lt;
                            </span>
                            Reader.Feed: 0x600000045010
                            <span style="color: #000000; font-weight: bold;">
                                &gt;
                            </span>
                            ,
                            <span style="color: #000000; font-weight: bold;">
                                &lt;
                            </span>
                            Reader.Feed: 0x6000000450d0
                            <span style="color: #000000; font-weight: bold;">
                                &gt;
                            </span>
                            <span style="color: #7a0874; font-weight: bold;">
                                ]
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        You can see that you’ve successfully loaded two
        <code>
            Feed
        </code>
        objects into the
        <code>
            feeds
        </code>
        property — yay!
    </p>
    <h2>
        Introducing NSOutlineViewDataSource
    </h2>
    <p>
        So far, you’ve told the outline view that
        <code>
            ViewController
        </code>
        is its data source — but
        <code>
            ViewController
        </code>
        doesn’t yet know about its new job. It’s time to change this and get rid
        of that pesky error message.
    </p>
    <p>
        Add the following
        <em>
            extension
        </em>
        below your class declaration of
        <code>
            ViewController
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1234638">
                    <td class="code" id="p123463code8">
                        <pre class="swift" style="font-family:monospace;">
                            extension ViewController: NSOutlineViewDataSource { &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This makes
        <code>
            ViewController
        </code>
        adopt the
        <code>
            NSOutlineViewDataSource
        </code>
        protocol. Since we’re not using bindings in this tutorial, you must implement
        a few methods to fill the outline view. Let’s go through each method.
    </p>
    <p>
        Your outline view needs to know how many items it should show. For this,
        use the method
        <code>
            outlineView(_: numberOfChildrenOfItem:) -&gt; Int
        </code>
        .
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1234639">
                    <td class="code" id="p123463code9">
                        <pre class="swift" style="font-family:monospace;">
                            func outlineView(_ outlineView: NSOutlineView, numberOfChildrenOfItem
                            item: Any?) -&gt; Int { //1 if let feed = item as? Feed { return feed.children.count
                            } //2 return feeds.count }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This method will be called for every level of the hierarchy displayed
        in the outline view. Since you only have 2 levels in your outline view,
        the implementation is pretty straightforward:
    </p>
    <ol>
        <li>
            If
            <code>
                item
            </code>
            is a
            <code>
                Feed
            </code>
            , it returns the number of
            <code>
                children
            </code>
            .
        </li>
        <li>
            Otherwise, it returns the number of
            <code>
                feeds
            </code>
            .
        </li>
    </ol>
    <p>
        One thing to note:
        <code>
            item
        </code>
        is an optional, and will be
        <code>
            nil
        </code>
        for the root objects of your data model. In this case, it will be
        <code>
            nil
        </code>
        for
        <code>
            Feed
        </code>
        ; otherwise it will contain the parent of the object. For
        <code>
            FeedItem
        </code>
        objects,
        <code>
            item
        </code>
        will be a
        <code>
            Feed
        </code>
        .
    </p>
    <p>
        Onward! The outline view needs to know which child it should show for
        a given parent and index. The code for this is similiar to the previous
        code:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12346310">
                    <td class="code" id="p123463code10">
                        <pre class="swift" style="font-family:monospace;">
                            func outlineView(_ outlineView: NSOutlineView, child index: Int, ofItem
                            item: Any?) -&gt; Any { if let feed = item as? Feed { return feed.children[index]
                            } &nbsp; return feeds[index] }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This checks whether
        <code>
            item
        </code>
        is a
        <code>
            Feed
        </code>
        ; if so, it returns the
        <code>
            FeedItem
        </code>
        for the given index. Otherwise, it return a
        <code>
            Feed
        </code>
        . Again,
        <code>
            item
        </code>
        will be
        <code>
            nil
        </code>
        for the root object.
    </p>
    <p>
        One great feature of
        <code>
            NSOutlineView
        </code>
        is that it can collapse items. First, however, you have to tell it which
        items can be collapsed or expanded. Add the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12346311">
                    <td class="code" id="p123463code11">
                        <pre class="swift" style="font-family:monospace;">
                            func outlineView(_ outlineView: NSOutlineView, isItemExpandable item:
                            Any) -&gt; Bool { if let feed = item as? Feed { return feed.children.count
                            &gt; 0 } &nbsp; return false }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        In this application only
        <code>
            Feeds
        </code>
        can be expanded and collapsed, and only if they have children. This checks
        whether
        <code>
            item
        </code>
        is a
        <code>
            Feed
        </code>
        and if so, returns whether the child count of
        <code>
            Feed
        </code>
        is greater than 0. For every other item, it just returns false.
    </p>
    <p>
        Run your application. Hooray! The error message is gone, and the outline
        view is populated. But wait — you only see 2 triangles indicating that
        you can expand the row. If you click one, more invisible entries appear.
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/second_run"
        rel="attachment wp-att-123497" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Second_Run-480x318.png"
            alt="Second_Run" width="480" height="318" class="aligncenter size-medium wp-image-123497"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Second_Run-480x318.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Second_Run-700x464.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Did you do something wrong? Nope — you just need one more method.
    </p>
    <h2>
        Introducing NSOutlineViewDelegate
    </h2>
    <p>
        The outline view asks its delegate for the view it should show for a specific
        entry. However, you haven’t implemented any delegate methods yet — time
        to add conformance to
        <code>
            NSOutlineViewDelegate
        </code>
        .
    </p>
    <p>
        Add another extension to your
        <code>
            ViewController
        </code>
        in
        <em>
            ViewController.swift
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12346312">
                    <td class="code" id="p123463code12">
                        <pre class="swift" style="font-family:monospace;">
                            extension ViewController: NSOutlineViewDelegate { &nbsp; }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The next method is a bit more complex, since the outline view should show
        different views for
        <code>
            Feeds
        </code>
        and
        <code>
            FeedItems
        </code>
        . Let’s put it together piece by piece.
    </p>
    <p>
        First, add the method body to the extension.
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12346313">
                    <td class="code" id="p123463code13">
                        <pre class="swift" style="font-family:monospace;">
                            func outlineView(_ outlineView: NSOutlineView, viewFor tableColumn: NSTableColumn?,
                            item: Any) -&gt; NSView? { var view: NSTableCellView? // More code here
                            return view }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Right now this method returns
        <code>
            nil
        </code>
        for every
        <code>
            item
        </code>
        . In the next step you start to return a view for a
        <code>
            Feed
        </code>
        . Add this code above the
        <code>
            // More code here
        </code>
        comment:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12346314">
                    <td class="code" id="p123463code14">
                        <pre class="swift" style="font-family:monospace;">
                            //1 if let feed = item as? Feed { //2 view = outlineView.make(withIdentifier:
                            "FeedCell", owner: self) as? NSTableCellView if let textField = view?.textField
                            { //3 textField.stringValue = feed.name textField.sizeToFit() } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This code:
    </p>
    <ol>
        <li>
            Checks if
            <code>
                item
            </code>
            is a
            <code>
                Feed
            </code>
            .
        </li>
        <li>
            Gets a view for a
            <code>
                Feed
            </code>
            from the outline view. A normal
            <code>
                NSTableViewCell
            </code>
            contains a text field.
        </li>
        <li>
            Sets the text field’s text to the feed’s name and calls
            <code>
                sizeToFit()
            </code>
            . This causes the text field to recalculate its frame so the contents
            fit inside.
        </li>
    </ol>
    <p>
        Run your project. While you can see cells for a
        <code>
            Feed
        </code>
        , if you expand one you still see nothing.
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/third_run"
        rel="attachment wp-att-123506" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Third_Run-480x318.png"
            alt="Third_Run" width="480" height="318" class="aligncenter size-medium wp-image-123506"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Third_Run-480x318.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Third_Run-700x464.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        This is because you’ve only provided views for the cells that represent
        a
        <code>
            Feed
        </code>
        . To change this, move on to the next step! Still in
        <em>
            ViewController.swift
        </em>
        , add the following property below the
        <code>
            feeds
        </code>
        property:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12346315">
                    <td class="code" id="p123463code15">
                        <pre class="swift" style="font-family:monospace;">
                            let dateFormatter = DateFormatter()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Change
        <code>
            viewDidLoad()
        </code>
        by adding the following line after
        <code>
            super.viewDidLoad()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12346316">
                    <td class="code" id="p123463code16">
                        <pre class="swift" style="font-family:monospace;">
                            dateFormatter.dateStyle = .short
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This adds an
        <code>
            NSDateformatter
        </code>
        that will be used to create a nice formatted date from the
        <code>
            publishingDate
        </code>
        of a
        <code>
            FeedItem
        </code>
        .
    </p>
    <p>
        Return to
        <code>
            outlineView(_:viewForTableColumn:item:)
        </code>
        and add an
        <em>
            else-if
        </em>
        clause to
        <code>
            if let feed = item as? Feed
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12346317">
                    <td class="code" id="p123463code17">
                        <pre class="swift" style="font-family:monospace;">
                            else if let feedItem = item as? FeedItem { //1 if tableColumn?.identifier
                            == "DateColumn" { //2 view = outlineView.make(withIdentifier: "DateCell",
                            owner: self) as? NSTableCellView &nbsp; if let textField = view?.textField
                            { //3 textField.stringValue = dateFormatter.string(from: feedItem.publishingDate)
                            textField.sizeToFit() } } else { //4 view = outlineView.make(withIdentifier:
                            "FeedItemCell", owner: self) as? NSTableCellView if let textField = view?.textField
                            { //5 textField.stringValue = feedItem.title textField.sizeToFit() } }
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This is what you’re doing here:
    </p>
    <ol>
        <li>
            If
            <code>
                item
            </code>
            is a
            <code>
                FeedItem
            </code>
            , you fill two columns: one for the
            <code>
                title
            </code>
            and another one for the
            <code>
                publishingDate
            </code>
            . You can differentiate the columns with their
            <code>
                identifier
            </code>
            .
        </li>
        <li>
            If the
            <code>
                identifier
            </code>
            is
            <em>
                dateColumn
            </em>
            , you request a DateCell.
        </li>
        <li>
            You use the date formatter to create a string from the
            <code>
                publishingDate
            </code>
            .
        </li>
        <li>
            If it is not a
            <em>
                dateColumn
            </em>
            , you need a cell for a
            <code>
                FeedItem
            </code>
            .
        </li>
        <li>
            You set the text to the
            <code>
                title
            </code>
            of the
            <code>
                FeedItem
            </code>
            .
        </li>
    </ol>
    <p>
        Run your project again to see feeds filled properly with articles.
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/fourth_run"
        rel="attachment wp-att-123507" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Fourth_Run-480x318.png"
            alt="Fourth_Run" width="480" height="318" class="aligncenter size-medium wp-image-123507"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Fourth_Run-480x318.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/12/Fourth_Run-700x464.png 700w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        There’s one problem left — the date column for a
        <code>
            Feed
        </code>
        shows a static text. To fix this, change the content of the
        <code>
            if let feed = item as? Feed
        </code>
        if statement to:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12346318">
                    <td class="code" id="p123463code18">
                        <pre class="swift" style="font-family:monospace;">
                            if tableColumn?.identifier == "DateColumn" { view = outlineView.make(withIdentifier:
                            "DateCell", owner: self) as? NSTableCellView if let textField = view?.textField
                            { textField.stringValue = "" textField.sizeToFit() } } else { view = outlineView.make(withIdentifier:
                            "FeedCell", owner: self) as? NSTableCellView if let textField = view?.textField
                            { textField.stringValue = feed.name textField.sizeToFit() } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        To complete this app, after you select an entry the web view should show
        the corresponding article. How can you do that? Luckily, the following
        delegate method can be used to check whether something was selected or
        if the selection changed.
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12346319">
                    <td class="code" id="p123463code19">
                        <pre class="swift" style="font-family:monospace;">
                            func outlineViewSelectionDidChange(_ notification: Notification) { //1
                            guard let outlineView = notification.object as? NSOutlineView else { return
                            } //2 let selectedIndex = outlineView.selectedRow if let feedItem = outlineView.item(atRow:
                            selectedIndex) as? FeedItem { //3 let url = URL(string: feedItem.url) //4
                            if let url = url { //5 self.webView.mainFrame.load(URLRequest(url: url))
                            } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This code:
    </p>
    <ol>
        <li>
            Checks if the notification object is an NSOutlineView. If not, return
            early.
        </li>
        <li>
            Gets the selected index and checks if the selected row contains a
            <code>
                FeedItem
            </code>
            or a
            <code>
                Feed
            </code>
            .
        </li>
        <li>
            If a
            <code>
                FeedItem
            </code>
            was selected, creates a
            <code>
                NSURL
            </code>
            from the
            <code>
                url
            </code>
            property of the
            <code>
                Feed
            </code>
            object.
        </li>
        <li>
            Checks whether this succeeded.
        </li>
        <li>
            Finally, loads the page.
        </li>
    </ol>
    <p>
        Before you test this out, return to the
        <em>
            Info.plist
        </em>
        file. Add a new Entry called
        <em>
            App Transport Security Settings
        </em>
        and make it a
        <em>
            Dictionary
        </em>
        if Xcode didn’t. Add one entry,
        <em>
            Allow Arbitrary Loads
        </em>
        of type
        <em>
            Boolean
        </em>
        , and set it to
        <em>
            YES
        </em>
        .
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            Adding this entry to your plist causes your application to accept insecure
            connections to every host, which can be a security risk. Usually it is
            better to add
            <em>
                Exception Domains
            </em>
            to this entry or, even better, to use backends that use an encrypted connection.
        </p>
    </div>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Info_Plist.png"
        sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Info_Plist-700x38.png"
            alt="Change_Info_Plist" width="700" height="38" class="aligncenter size-large wp-image-123498"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Info_Plist-700x38.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/12/Change_Info_Plist-480x26.png 480w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Now build your project and select a
        <code>
            FeedItem
        </code>
        . Assuming you have a working internet connection, the article will load
        after a few seconds.
    </p>
    <h2>
        Finishing Touches
    </h2>
    <p>
        Your example application is now working, but there are at least two common
        behaviors missing: double-clicking to expand or collapse a group, and the
        ability to remove an entry from the outline view.
    </p>
    <p>
        Let’s start with the double-click feature. Open the
        <em>
            Assistant Editor
        </em>
        by pressing
        <em>
            Alt + Cmd + Enter
        </em>
        . Open
        <em>
            Main.storyboard
        </em>
        in the left part of the window, and
        <em>
            ViewController.swift
        </em>
        in the right part.
    </p>
    <p>
        Right-click on the outline view inside the
        <em>
            Document Outline
        </em>
        on the left. Inside the appearing pop-up, find
        <em>
            doubleAction
        </em>
        and click the small circle to its right.
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/assistanteditor-9"
        rel="attachment wp-att-124518" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/AssistantEditor-480x168.png"
            alt="AssistantEditor" width="600" height="210" class="aligncenter size-medium wp-image-124518"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/AssistantEditor-480x168.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/AssistantEditor-768x269.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/AssistantEditor-700x245.png 700w"
            sizes="(max-width: 600px) 100vw, 600px">
        </a>
    </p>
    <p>
        Drag from the circle inside
        <em>
            ViewController.swift
        </em>
        and add an
        <em>
            IBAction
        </em>
        named
        <code>
            doubleClickedItem
        </code>
        . Make sure that the sender is of type
        <code>
            NSOutlineView
        </code>
        and not
        <code>
            AnyObject
        </code>
        .
    </p>
    <p>
        <a href="https://www.raywenderlich.com/123463/nsoutlineview-macos-tutorial/addaction-2"
        rel="attachment wp-att-124520" sl-processed="1">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/AddAction-480x230.png"
            alt="AddAction" width="240" height="115" class="aligncenter size-medium wp-image-124520"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/AddAction-480x230.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/AddAction.png 504w"
            sizes="(max-width: 240px) 100vw, 240px">
        </a>
    </p>
    <p>
        Switch back to the Standard editor (
        <em>
            Cmd + Enter
        </em>
        ) and open
        <em>
            ViewController.swift
        </em>
        . Add the following code to the action you just created.
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12346320">
                    <td class="code" id="p123463code20">
                        <pre class="swift" style="font-family:monospace;">
                            @IBAction func doubleClickedItem(_ sender: NSOutlineView) { //1 let item
                            = sender.item(atRow: sender.clickedRow) &nbsp; //2 if item is Feed { //3
                            if sender.isItemExpanded(item) { sender.collapseItem(item) } else { sender.expandItem(item)
                            } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This code:
    </p>
    <ol>
        <li>
            Gets the clicked item.
        </li>
        <li>
            Checks whether this item is a
            <code>
                Feed
            </code>
            , which is the only item that can be expanded or collapsed.
        </li>
        <li>
            If the item is a
            <code>
                Feed
            </code>
            , asks the outline view if the item is expanded or collapsed, and calls
            the appropriate method.
        </li>
    </ol>
    <p>
        Build your project, then double-click a feed. It works!
    </p>
    <p>
        The last behavior we want to implement is allowing the user to press backspace
        to delete the selected feed or article.
    </p>
    <p>
        Still inside
        <em>
            ViewController.swift
        </em>
        , add the following method to your
        <code>
            ViewController
        </code>
        . Make sure to add it to the normal declaration and not inside an extension,
        because the method has nothing to do with the delegate or datasource protocols.
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12346321">
                    <td class="code" id="p123463code21">
                        <pre class="swift" style="font-family:monospace;">
                            override func keyDown(with theEvent: NSEvent) { interpretKeyEvents([theEvent])
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This method is called every time a key is pressed, and asks the system
        which key was pressed. For some keys, the system will call a corresponding
        action. The method called for the backspace key is
        <code>
            deleteBackward(_:)
        </code>
        .
    </p>
    <p>
        Add the method below
        <code>
            keyDown(_:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12346322">
                    <td class="code" id="p123463code22">
                        <pre class="swift" style="font-family:monospace;">
                            override func deleteBackward(_ sender: Any?) { //1 let selectedRow = outlineView.selectedRow
                            if selectedRow == -1 { return } &nbsp; //2 outlineView.beginUpdates() &nbsp;
                            outlineView.endUpdates() }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <ol>
        <li>
            The first thing this does is see if there is something selected. If nothing
            is selected,
            <code>
                selectedRow
            </code>
            will have a value of -1 and you return from this method.
        </li>
        <li>
            Otherwise, it tells the outline view that there will be updates on it
            and when these updates are done.
        </li>
    </ol>
    <p>
        Now add the following between
        <code>
            beginUpdates()
        </code>
        and
        <code>
            endUpdates()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12346323">
                    <td class="code" id="p123463code23">
                        <pre class="swift" style="font-family:monospace;">
                            //3 if let item = outlineView.item(atRow: selectedRow) { &nbsp; //4 if
                            let item = item as? Feed { //5 if let index = self.feeds.index( where:
                            {$0.name == item.name} ) { //6 self.feeds.remove(at: index) //7 outlineView.removeItems(at:
                            IndexSet(integer: selectedRow), inParent: nil, withAnimation: .slideLeft)
                            } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This code:
    </p>
    <ol start="3">
        <li>
            Gets the selected item.
        </li>
        <li>
            Checks if it is a
            <code>
                Feed
            </code>
            or a
            <code>
                FeedItem
            </code>
            .
        </li>
        <li>
            If it is a
            <code>
                Feed
            </code>
            , searches the index of it inside the
            <code>
                feeds
            </code>
            array.
        </li>
        <li>
            If found, removes it from the array.
        </li>
        <li>
            Removes the row for this entry from the outline view with a small animation.
        </li>
    </ol>
    <p>
        To finish this method, add the code to handle
        <code>
            FeedItems
        </code>
        as an else part to
        <code>
            if let item = item as? Feed
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12346324">
                    <td class="code" id="p123463code24">
                        <pre class="swift" style="font-family:monospace;">
                            else if let item = item as? FeedItem { //8 for feed in self.feeds { //9
                            if let index = feed.children.index( where: {$0.title == item.title} ) {
                            feed.children.remove(at: index) outlineView.removeItems(at: IndexSet(integer:
                            index), inParent: feed, withAnimation: .slideLeft) } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <ol start="8">
        <li>
            This code is similar to the code for a
            <code>
                Feed
            </code>
            . The only additional step is that here it iterates over all feeds, because
            you don’t know to which
            <code>
                Feed
            </code>
            the
            <code>
                FeedItem
            </code>
            belongs.
        </li>
        <li>
            For each
            <code>
                Feed
            </code>
            , the code checks if you can find a
            <code>
                FeedItem
            </code>
            in its
            <code>
                children
            </code>
            array. If so, it deletes it from the array and from the outline view.
        </li>
    </ol>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            Not only can you delete a row, but you can also add and move rows. The
            steps are the same: add an item to your data model and call
            <code>
                insertItemsAtIndexes(_:, inParent:, withAnimation:)
            </code>
            to insert items, or
            <code>
                moveItemAtIndex(_:, inParent:, toIndex:, inParent:)
            </code>
            to move items. Make sure that your datasource is also changed accordingly.
        </p>
    </div>
    <p>
        Now your app is complete! Build and run to check out the new functionality
        you just added. Select a feed item and hit the delete key–it’ll disappear
        as expected. Check that the same is true for the feed as well.
    </p>
    <h2>
        Where To Go From here?
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
        Congrats! You’ve created an RSS Feed Reader-type app with hierarchical
        functionality that allows the user to delete rows at will and to double-click
        to expand and collapse the lists.
    </p>
    <p>
        You can download the final project
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/Reader_Final.zip"
        sl-processed="1">
            here
        </a>
        .
    </p>
    <p>
        In this NSOutlineView on macOS tutorial you learned a lot about
        <code>
            NSOutlineView
        </code>
        . You learned:
    </p>
    <ul>
        <li>
            How to hook up an
            <code>
                NSOutlineView
            </code>
            in Interface Builder.
        </li>
        <li>
            How to populate it with data.
        </li>
        <li>
            How to expand/collapse items.
        </li>
        <li>
            How to remove entries.
        </li>
        <li>
            How to respond to user interactions.
        </li>
    </ul>
    <p>
        There is lots of functionality that you didn’t get chance to cover here,
        like support for drag and drop or data models with a deeper hierarchy,
        so if you want to learn more about
        <code>
            NSOutlineView
        </code>
        , take a look at the
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ApplicationKit/Classes/NSOutlineView_Class/"
        sl-processed="1">
            documentation
        </a>
        . Since it is a subclass of
        <code>
            NSTableView
        </code>
        , Ernesto García’s tutorial about
        <a href="http://www.raywenderlich.com/118835/os-x-nstableview-tutorial"
        sl-processed="1">
            table views
        </a>
        is also worth a look.
    </p>
    <p>
        I hope you enjoyed this NSOutlineView on macOS tutorial! If you have any
        questions or comments, feel free to join the forum discussion below.
    </p>
</div>