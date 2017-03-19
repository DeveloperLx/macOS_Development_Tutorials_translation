# NSCollectionView教程

#### [原文地址](https://www.raywenderlich.com/145978/nscollectionview-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

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
            <p>
                I wish you a pleasant journey with Collection View in your apps. I look
                forward to hearing your ideas, experiences and any questions you have in
                the forums below!
            </p>
        </div>
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
</div>