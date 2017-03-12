# macOS NSTableView教程

#### [原文地址](https://www.raywenderlich.com/143828/macos-nstableview-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div class="note">
        <p>
            <em>
                更新记录：
            </em>
            这个macOS NSTableView的教程已被Warren Burton更新到Xcode 8及Swift 3。
            <a href="https://www.raywenderlich.com/118835/os-x-nstableview-tutorial">
                原教程
            </a>
            是由Ernesto García撰写的。
        </p>
    </div>
    <div id="attachment_148775" style="width: 260px" class="wp-caption alignright">
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-250x250.png"
            alt="Create awesome user interfaces with table views!" width="250" height="250"
            class="size-thumbnail wp-image-148775" srcset="https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-50x50.png 50w, https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/11/OSX-TableViews-feature-128x128.png 128w"
            sizes="(max-width: 250px) 100vw, 250px">
        </a>
        <p class="wp-caption-text">
        	使用table view创建超级棒的用户界面！
        </p>
    </div>
    <p>
    	在macOS应用中，table view是最普遍存在的控件之一，熟悉的例子有邮件信息的列表及Spotlight的搜索结果。它可以让你的Mac以一个迷人的方式，展现列成表格的数据。
    </p>
    <p>
        <code>
            NSTableView
        </code>
        使用行和列来排列数据。每一行代表给出数据集合中的一个单独的数据模型，每一列展示这个数据模型的一个特定的属性。
    </p>
    <p>
    	在这篇macOS的NSTableView教程中，你将使用一个table view来创建带有功能的文件浏览器，它将具有和Finder惊人的相似性。在你完成它之后，你将学到很多关于table view的知识，例如：
    </p>
    <ul>
        <li>
        	怎么填充一个table view。
        </li>
        <li>
        	怎么改变它的视觉风格。
        </li>
        <li>
        	怎么响应像是选择或双击用户的交互。
        </li>
    </ul>
    <p>
    	准备好创建你的第一个table view了么？继续阅读！
    </p>
    <h2>
    	开始吧
    </h2>
    <p>
        Download
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/FileViewer_starter-2.zip">
            the starter project
        </a>
        and open it in
        <em>
            Xcode
        </em>
        .
    </p>
    <p>
        Build and run to see what you’re starting with:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-empty.png">
            <img class="aligncenter size-full wp-image-118915" src="https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-empty.png"
            alt="window at start of tutorial" width="537" height="306" srcset="https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-empty.png 537w, https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-empty-480x274.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-empty-266x151.png 266w"
            sizes="(max-width: 537px) 100vw, 537px">
        </a>
    </p>
    <p>
        You have a blank canvas from which you’ll create a cool file viewer. The
        starter app already has some of the functionality you’ll need to work through
        this tutorial.
    </p>
    <p>
        With the application open, choose
        <em>
            File &gt; Open…
        </em>
        (or use the
        <em>
            Command+O
        </em>
        keyboard shortcut).
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-fileopen.png">
            <img class="aligncenter size-large wp-image-118916" src="https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-fileopen-700x403.png"
            alt="open a folder" width="700" height="403" srcset="https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-fileopen-700x403.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-fileopen-480x276.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/10/build-run-fileopen.png 726w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        From the new window that pops up, choose any folder you want and click
        the
        <em>
            Open
        </em>
        button. You’ll see something like this in Xcode’s console:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1438281">
                    <td class="code" id="p143828code1">
                        <pre class="none" style="font-family:monospace;">
                            Represented object: file:///Users/tutorials/FileViewer/FileViewer/
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This message shows the selected folder’s path, and the code in the starter
        project passes that URL to the view controller.
    </p>
    <p>
        If you’re curious and want to learn more about how things are implemented,
        here’s where you should look:
    </p>
    <ul>
        <li>
            <em>
                Directory.swift
            </em>
            : Contains the implementation of the
            <em>
                Directory
            </em>
            struct that reads the content of a directory.
        </li>
        <li>
            <em>
                WindowController.swift
            </em>
            : Contains the code that presents you with the folder selection panel
            and passes the selected directory to the
            <em>
                ViewController
            </em>
            .
        </li>
        <li>
            <em>
                ViewController.swift
            </em>
            : Contains the implementation of the
            <code>
                ViewController
            </code>
            class and is where you’ll spend some time today. It’s where you’ll create
            the table view and show the file list.
        </li>
    </ul>
    <h2>
        Creating the Table View
    </h2>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        in the
        <em>
            Project Navigator
        </em>
        . Select the
        <em>
            View Controller Scene
        </em>
        and drop a table view from the
        <em>
            Object Library
        </em>
        into the view. There’s a container in the view hierachy named
        <em>
            Table Container
        </em>
        all ready for you.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/add-table.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/add-table-650x430.png"
            alt="add a table in interface builder" width="650" height="430" class="aligncenter size-large wp-image-145671"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/add-table-650x430.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/add-table-480x318.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/10/add-table.png 1525w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Next, you need to add some constraints. Click the
        <em>
            Pin
        </em>
        button in the Auto Layout toolbar. In the popup that appears, set the
        all the edge constraints as follows:
    </p>
    <ul>
        <li>
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
            : 0.
        </li>
    </ul>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/11/constrain-table.png"
        alt="constrain the table to its container" width="362" height="500" class="aligncenter size-large wp-image-148614"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/11/constrain-table.png 576w, https://koenig-media.raywenderlich.com/uploads/2016/11/constrain-table-232x320.png 232w, https://koenig-media.raywenderlich.com/uploads/2016/11/constrain-table-362x500.png 362w"
        sizes="(max-width: 362px) 100vw, 362px">
    </p>
    <p>
        Be sure to set
        <em>
            Update Frames
        </em>
        to
        <em>
            Items of New Constraints
        </em>
        , then click
        <em>
            Add 4 Constraints
        </em>
        .
    </p>
    <p>
        Take a moment to have a look at the structure of a newly created table
        view. As you probably gathered from its name, it follows typical table
        structuring:
    </p>
    <ul>
        <li>
            It’s made up of rows and columns.
        </li>
        <li>
            Each row represents a single item within the data model collection.
        </li>
        <li>
            Each column displays specific attributes of the model.
        </li>
        <li>
            Each column can also have a header row.
        </li>
        <li>
            Header rows describe the data within a column.
        </li>
    </ul>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/11/tableStructure.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/11/tableStructure-268x320.png"
            alt="table view inner structure" width="268" height="320" class="aligncenter size-medium wp-image-148302"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/11/tableStructure-268x320.png 268w, https://koenig-media.raywenderlich.com/uploads/2016/11/tableStructure-419x500.png 419w, https://koenig-media.raywenderlich.com/uploads/2016/11/tableStructure.png 606w"
            sizes="(max-width: 268px) 100vw, 268px">
        </a>
    </p>
    <p>
        If you’re familiar with
        <code>
            UITableView
        </code>
        on iOS, you’re treading familiar waters, but they’re much deeper here
        in macOS. In fact, you might be surprised by the number of individual UI
        objects in the object hierarchy that make up an
        <code>
            NSTableView
        </code>
        .
    </p>
    <p>
        <code>
            NSTableView
        </code>
        is an older and more complex control than a
        <code>
            UITableView
        </code>
        , and it serves a different user interface paradigm, specifically, where
        the user has a mouse or trackpad.
    </p>
    <p>
        The main difference with
        <em>
            UITableView
        </em>
        is that you have the possibility of multiple columns and a header that
        can be used to interact with the table view, for example, ordering and
        selecting.
    </p>
    <p>
        Together,
        <code>
            NSScrollView
        </code>
        and
        <code>
            NSClipView
        </code>
        , respectively scroll and clip the contents of the
        <code>
            NSTableView
        </code>
        .
    </p>
    <p>
        There are two
        <code>
            NSScroller
        </code>
        objects — one each for vertical and horizontal scrolling across the table.
    </p>
    <p>
        There are also a number of column objects. An
        <code>
            NSTableView
        </code>
        has columns, and these columns have headers with titles. It’s important
        to note that users can resize and reorder columns, though you have the
        power to remove this ability by setting its default to disabled.
    </p>
    <h3>
        Anatomy of NSTableView
    </h3>
    <p>
        In Interface Builder, you’ve seen the complexity of the view hierarchy
        of the table view. Multiple classes cooperate to build the table structure,
        which usually ends up looking like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/Artboard-1.png">
            <img class="aligncenter size-large wp-image-120794" src="https://koenig-media.raywenderlich.com/uploads/2015/11/Artboard-1-700x377.png"
            alt="components of a table view" width="700" height="377" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/Artboard-1-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/11/Artboard-1-480x258.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/11/Artboard-1.png 1454w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        These are the key parts of an
        <code>
            NSTableView
        </code>
        :
    </p>
    <ul>
        <li>
            <em>
                Header View
            </em>
            : The header view is an instance of
            <code>
                NSTableHeaderView
            </code>
            . It’s responsible for drawing the headers at top of the table. If you
            need to display a custom header, you can use your own header subclasses.
        </li>
        <li>
            <em>
                Row View
            </em>
            : The row view displays the visual attributes associated with every row
            in the table view, like a selection highlight. Each row displayed in the
            table has its own instance of the row view. An important distinction to
            make is that rows do not represent your data; that the cell’s responsibility.
            It only handles visual attributes like selection color or separators. You
            can create new row subclasses to style your table view differently.
        </li>
        <li>
            <em>
                Cell Views
            </em>
            : The cell is arguably the most important object in a table view. At the
            intersection of a row and column, you find a cell. Each one is an
            <code>
                NSView
            </code>
            or
            <code>
                NSTableCellView
            </code>
            subclass, and its responsibility is to display the actual data. And guess
            what? You can create custom cell view classes to display the content however
            you’d like.
        </li>
        <li>
            <em>
                Column
            </em>
            : The columns are represented by the
            <code>
                NSTableViewColumn
            </code>
            class, which is responsible for managing width and behavior of the column,
            such as resizing and repositioning. This class is not a view, but a controller
            class. You use it to specify how columns should behave, but you don’t control
            the visual styles of the columns with it because the header, row and cell
            views have got things covered.
        </li>
    </ul>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            There are two modes of NSTableView. The first is a cell-based table view
            called an
            <code>
                NSCell
            </code>
            . It’s like an
            <code>
                NSView
            </code>
            , but older and lighter. It comes from earlier days of computing when
            the desktop needed optimizations in order to draw controls with minimal
            overhead.
        </p>
        <p>
            Apple recommends using view-based table views, but you’ll see
            <code>
                NSCell
            </code>
            in many of the controls in AppKit, so it’s worth knowing what it is and
            where it comes from. You can read more about
            <code>
                NSCell
            </code>
            in Apple’s
            <a title="Control and Cell Programming Topics" href="https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/ControlCell/Concepts/AboutControlsCells.html#//apple_ref/doc/uid/20000731-BBCEACEA"
            target="_blank">
                Control and Cell Programming Topics
            </a>
        </p>
    </div>
    <p>
        Well, now that was a nice little jog into the basic theory behind table
        view structure. Now that you’ve had all that, it’s time to go back to
        <em>
            Xcode
        </em>
        and get to work on your very own table view.
    </p>
    <h3>
        Playing With Columns in a Table View
    </h3>
    <p>
        By default, Interface Builder creates a table view with two columns, but
        you need three columns to display name, date and size file information.
    </p>
    <p>
        Go back to
        <em>
            Main.storyboard
        </em>
        .
    </p>
    <p>
        Select the table view in the
        <em>
            View Controller Scene
        </em>
        . Make sure that you select the table view and
        <i>
            not
        </i>
        the scroll view that contains it.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/add-table-column.png"
        alt="table in the view hierarchy" width="317" height="360" class="aligncenter size-full wp-image-145681"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/add-table-column.png 317w, https://koenig-media.raywenderlich.com/uploads/2016/10/add-table-column-282x320.png 282w"
        sizes="(max-width: 317px) 100vw, 317px">
    </p>
    <p>
        Open the
        <em>
            Attributes Inspector
        </em>
        . Change the number of
        <em>
            Columns
        </em>
        to 3. It’s as simple as that! Your table view now has three columns.
    </p>
    <p>
        Next, check the
        <em>
            Multiple
        </em>
        checkbox in the
        <em>
            Selection
        </em>
        section, because you want to select multiple files at once. Also check
        <em>
            Alternating Rows
        </em>
        in the
        <em>
            Highlight
        </em>
        section. When enabled, this tells the table view to use alternating row
        colors for its background, just like Finder.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-attributes.png"
        alt="configure table attributes" width="261" height="382" class="aligncenter size-full wp-image-145679">
    </p>
    <p>
        Rename the column headers so the text is more descriptive. Select the
        first column in the
        <em>
            View Controller Scene
        </em>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/configure-column.png"
        alt="configure-column" width="322" height="360" class="aligncenter size-full wp-image-145679"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/configure-column.png 322w, https://koenig-media.raywenderlich.com/uploads/2016/10/configure-column-286x320.png 286w"
        sizes="(max-width: 322px) 100vw, 322px">
    </p>
    <p>
        Open the
        <em>
            Attributes Inspector
        </em>
        and change the column
        <em>
            Title
        </em>
        to
        <em>
            Name
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-changetitle.png">
            <img class="aligncenter size-full wp-image-118863" src="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-changetitle.png"
            alt="change the header title in attributes" width="275" height="266" srcset="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-changetitle.png 275w, https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-changetitle-32x32.png 32w"
            sizes="(max-width: 275px) 100vw, 275px">
        </a>
    </p>
    <p>
        Repeat the operation for the second and third column, changing the
        <em>
            Title
        </em>
        to
        <em>
            Modification Date
        </em>
        and
        <em>
            Size
        </em>
        , respectively.
    </p>
    <div class="note">
        <p>
            <em>
                Note
            </em>
            : There is an alternative method for changing the column title. You can
            double-click directly on the header on the table view to make it editable.
            Both ways have exactly the same end result, so go with whichever method
            you prefer.
        </p>
    </div>
    <p>
        Last, if you can’t see the Size column yet, select the Modification Date
        column and resize to 200. It beats fishing around for the resize handle
        with your mouse. :]
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/date-column-size-1.png"
        alt="resize modification date if needed" width="260" height="129" class="aligncenter size-full wp-image-145687">
    </p>
    <p>
        Build and run. Here’s what you should see:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/post-column-naming.png"
        alt="table with configured headers" width="598" height="253" class="aligncenter size-full wp-image-145677"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/post-column-naming.png 598w, https://koenig-media.raywenderlich.com/uploads/2016/10/post-column-naming-480x203.png 480w"
        sizes="(max-width: 598px) 100vw, 598px">
    </p>
    <h3>
        Changing How Information is Represented
    </h3>
    <p>
        In its current state, the table view has three columns, each containing
        a cell view that shows text in a text field.
    </p>
    <p>
        But it’s kind of bland, so spice it up by showing the icon of the file
        next to the file name. Your table will look much cleaner after this little
        upgrade.
    </p>
    <p>
        You need to replace the cell view in the first column with a new cell
        type that contains an image and a text field.
    </p>
    <p>
        You’re in luck because Interface Builder has this type of cell built in.
    </p>
    <p>
        Select the
        <em>
            Table Cell View
        </em>
        in the
        <em>
            Name
        </em>
        column and delete it.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/delete-this-view-1.png"
        alt="delete this view" width="301" height="257" class="aligncenter size-full wp-image-145802">
    </p>
    <p>
        Open the
        <em>
            Object Library
        </em>
        and drag and drop an
        <em>
            Image &amp; Text Table Cell View
        </em>
        into either the first column of the table view or the
        <em>
            View Controller Scene
        </em>
        tree, just under the
        <em>
            Name
        </em>
        table view column.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/set-name-cell.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/set-name-cell-650x399.png"
            alt="add a new cell type in interface builder" width="650" height="399"
            class="aligncenter size-large wp-image-145676" srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/set-name-cell-650x399.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/set-name-cell-480x295.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/10/set-name-cell.png 1464w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Now you’re whipping things into shape!
    </p>
    <h3>
        Assigning Identifiers
    </h3>
    <p>
        Every cell type needs an assigned identifier. Otherwise, you’ll be unable
        to create a cell view that corresponds to a specific column when you’re
        coding.
    </p>
    <p>
        Select the cell view in the first column, and in the
        <em>
            Identity Inspector
        </em>
        change the
        <em>
            Identifier
        </em>
        to
        <em>
            NameCellID
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-identifier.png">
            <img class="aligncenter size-full wp-image-118867" src="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-identifier.png"
            alt="edit column identifiers" width="274" height="181">
        </a>
    </p>
    <p>
        Repeat the process for the cell views in the second and third columns,
        naming the identifiers
        <em>
            DateCellID
        </em>
        and
        <em>
            SizeCellID
        </em>
        respectively.
    </p>
    <h2>
        Populating the Table View
    </h2>
    <div class="note">
        <em>
            Note:
        </em>
        There are two ways that you can populate a tableview, either using the
        datasource and delegate protocols you’ll see in this macOS NSTableView
        tutorial, or via
        <a href="https://www.raywenderlich.com/141297/cocoa-bindings-macos" target="_blank">
            Cocoa bindings
        </a>
        . The two techniques are not mutually exclusive and you may use them together
        at times to get what you want.
    </div>
    <p>
        The table view currently knows nothing about the data you need to show
        or how to display it, but it does need to be looped in! So, you’ll implement
        these two protocols to provide that information:
    </p>
    <ul>
        <li>
            <code>
                NSTableViewDataSource
            </code>
            : tells the table view how many rows it needs to represent.
        </li>
        <li>
            <code>
                NSTableViewDelegate
            </code>
            : provides the view cell that will be displayed for a specific row and
            column.
        </li>
    </ul>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/population-diagram1.png">
            <img class="aligncenter size-large wp-image-118891" src="https://koenig-media.raywenderlich.com/uploads/2015/10/population-diagram1-700x394.png"
            alt="population flow of a table view" width="700" height="394" srcset="https://koenig-media.raywenderlich.com/uploads/2015/10/population-diagram1-700x394.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/10/population-diagram1-480x270.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/10/population-diagram1-266x151.png 266w, https://koenig-media.raywenderlich.com/uploads/2015/10/population-diagram1.png 701w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        The visualization process is a collaboration between the table view, delegate
        and data source:
    </p>
    <ol>
        <li>
            The table view calls the data source method
            <code>
                numberOfRows(in:)
            </code>
            that returns the number of rows the table will display.
        </li>
        <li>
            The table view calls the delegate method
            <code>
                tableView(_:viewFor:row:)
            </code>
            for every row and column. The delegate creates the view for that position,
            populates it with the appropriate data, and then returns it to the table
            view.
        </li>
    </ol>
    <p>
        Both methods must be implemented in order to show your data in the table
        view.
    </p>
    <p>
        Open
        <em>
            ViewController.swift
        </em>
        in the
        <em>
            Assistant editor
        </em>
        and
        <em>
            Control-drag
        </em>
        from the table view into the
        <code>
            ViewController
        </code>
        class implementation to insert an outlet.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/add-outlet.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/add-outlet-650x228.png"
            alt="add an outlet to the tableview" width="650" height="228" class="aligncenter size-large wp-image-145674"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/add-outlet-650x228.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/10/add-outlet-480x168.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/10/add-outlet.png 1197w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Make sure that the
        <em>
            Type
        </em>
        is
        <em>
            NSTableView
        </em>
        and the
        <em>
            Connection
        </em>
        is
        <em>
            Outlet
        </em>
        . Name the outlet
        <code>
            tableView
        </code>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-outlet-22.png">
            <img class="aligncenter size-full wp-image-118921" src="https://koenig-media.raywenderlich.com/uploads/2015/10/tableview-outlet-22.png"
            alt="define the outlet" width="263" height="154">
        </a>
    </p>
    <p>
        You can now refer to the table view in code using this outlet.
    </p>
    <p>
        Switch back to the
        <em>
            Standard Editor
        </em>
        and open
        <em>
            ViewController.swift
        </em>
        . Implement the required data source method in the
        <code>
            ViewController
        </code>
        by adding this code at the end of the class:
    </p>
    <pre class="swift" style="font-family:monospace;">extension ViewController<span style="color: #002200;">:</span> NSTableViewDataSource <span style="color: #002200;">{</span>
&nbsp;
  <span style="color: #a61390;">func</span> numberOfRows<span style="color: #002200;">(</span><span style="color: #a61390;">in</span> tableView<span style="color: #002200;">:</span> <span style="color: #400080;">NSTableView</span><span style="color: #002200;">)</span> <span style="color: #002200;">-</span>&gt; <span style="color: #a61390;">Int</span> <span style="color: #002200;">{</span>
    <span style="color: #a61390;">return</span> directoryItems?.<span style="color: #a61390;">count</span> ?? <span style="color: #2400d9;">0</span>
  <span style="color: #002200;">}</span>
&nbsp;
<span style="color: #002200;">}</span></pre>
    <p>
        This creates an extension that conforms to the
        <code>
            NSTableViewDataSource
        </code>
        protocol and implements the required method
        <code>
            numberOfRows(in:)
        </code>
        to return the number files in the directory, which is the size of the
        <code>
            directoryItems
        </code>
        array.
    </p>
    <p>
        Now you need to implement the delegate. Add the following extension at
        the end of
        <em>
            ViewController.swift
        </em>
        :
    </p>
    <pre class="swift" style="font-family:monospace;">extension ViewController<span style="color: #002200;">:</span> NSTableViewDelegate <span style="color: #002200;">{</span>
&nbsp;
  fileprivate <span style="color: #a61390;">enum</span> CellIdentifiers <span style="color: #002200;">{</span>
    <span style="color: #a61390;">static</span> <span style="color: #a61390;">let</span> NameCell <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"NameCellID"</span>
    <span style="color: #a61390;">static</span> <span style="color: #a61390;">let</span> DateCell <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"DateCellID"</span>
    <span style="color: #a61390;">static</span> <span style="color: #a61390;">let</span> SizeCell <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">"SizeCellID"</span>
  <span style="color: #002200;">}</span>
&nbsp;
  <span style="color: #a61390;">func</span> tableView<span style="color: #002200;">(</span>_ tableView<span style="color: #002200;">:</span> <span style="color: #400080;">NSTableView</span>, viewFor tableColumn<span style="color: #002200;">:</span> <span style="color: #400080;">NSTableColumn</span>?, row<span style="color: #002200;">:</span> <span style="color: #a61390;">Int</span><span style="color: #002200;">)</span> <span style="color: #002200;">-</span>&gt; <span style="color: #400080;">NSView</span>? <span style="color: #002200;">{</span>
&nbsp;
    <span style="color: #a61390;">var</span> image<span style="color: #002200;">:</span> <span style="color: #400080;">NSImage</span>?
    <span style="color: #a61390;">var</span> text<span style="color: #002200;">:</span> <span style="color: #a61390;">String</span> <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">""</span>
    <span style="color: #a61390;">var</span> cellIdentifier<span style="color: #002200;">:</span> <span style="color: #a61390;">String</span> <span style="color: #002200;">=</span> <span style="color: #bf1d1a;">""</span>
&nbsp;
    <span style="color: #a61390;">let</span> dateFormatter <span style="color: #002200;">=</span> DateFormatter<span style="color: #002200;">(</span><span style="color: #002200;">)</span>
    dateFormatter.dateStyle <span style="color: #002200;">=</span> .long
    dateFormatter.timeStyle <span style="color: #002200;">=</span> .long
&nbsp;
    <span style="color: #11740a; font-style: italic;">// 1</span>
    guard <span style="color: #a61390;">let</span> item <span style="color: #002200;">=</span> directoryItems?<span style="color: #002200;">[</span>row<span style="color: #002200;">]</span> <span style="color: #a61390;">else</span> <span style="color: #002200;">{</span>
      <span style="color: #a61390;">return</span> <span style="color: #a61390;">nil</span>
    <span style="color: #002200;">}</span>
&nbsp;
    <span style="color: #11740a; font-style: italic;">// 2</span>
    <span style="color: #a61390;">if</span> tableColumn <span style="color: #002200;">==</span> tableView.tableColumns<span style="color: #002200;">[</span><span style="color: #2400d9;">0</span><span style="color: #002200;">]</span> <span style="color: #002200;">{</span>
      image <span style="color: #002200;">=</span> item.icon
      text <span style="color: #002200;">=</span> item.name
      cellIdentifier <span style="color: #002200;">=</span> CellIdentifiers.NameCell
    <span style="color: #002200;">}</span> <span style="color: #a61390;">else</span> <span style="color: #a61390;">if</span> tableColumn <span style="color: #002200;">==</span> tableView.tableColumns<span style="color: #002200;">[</span><span style="color: #2400d9;">1</span><span style="color: #002200;">]</span> <span style="color: #002200;">{</span>
      text <span style="color: #002200;">=</span> dateFormatter.string<span style="color: #002200;">(</span>from<span style="color: #002200;">:</span> item.date<span style="color: #002200;">)</span>
      cellIdentifier <span style="color: #002200;">=</span> CellIdentifiers.DateCell
    <span style="color: #002200;">}</span> <span style="color: #a61390;">else</span> <span style="color: #a61390;">if</span> tableColumn <span style="color: #002200;">==</span> tableView.tableColumns<span style="color: #002200;">[</span><span style="color: #2400d9;">2</span><span style="color: #002200;">]</span> <span style="color: #002200;">{</span>
      text <span style="color: #002200;">=</span> item.isFolder ? <span style="color: #bf1d1a;">"--"</span> <span style="color: #002200;">:</span> sizeFormatter.string<span style="color: #002200;">(</span>fromByteCount<span style="color: #002200;">:</span> item.size<span style="color: #002200;">)</span>
      cellIdentifier <span style="color: #002200;">=</span> CellIdentifiers.SizeCell
    <span style="color: #002200;">}</span>
&nbsp;
    <span style="color: #11740a; font-style: italic;">// 3</span>
    <span style="color: #a61390;">if</span> <span style="color: #a61390;">let</span> cell <span style="color: #002200;">=</span> tableView.make<span style="color: #002200;">(</span>withIdentifier<span style="color: #002200;">:</span> cellIdentifier, owner<span style="color: #002200;">:</span> <span style="color: #a61390;">nil</span><span style="color: #002200;">)</span> <span style="color: #a61390;">as?</span> NSTableCellView <span style="color: #002200;">{</span>
      cell.textField?.stringValue <span style="color: #002200;">=</span> text
      cell.imageView?.image <span style="color: #002200;">=</span> image ?? <span style="color: #a61390;">nil</span>
      <span style="color: #a61390;">return</span> cell
    <span style="color: #002200;">}</span>
    <span style="color: #a61390;">return</span> <span style="color: #a61390;">nil</span>
  <span style="color: #002200;">}</span>
&nbsp;
<span style="color: #002200;">}</span></pre>
    <p>
        This code declares an extension that conforms to the
        <code>
            NSTableViewDelegate
        </code>
        protocol and implements the method
        <code>
            tableView(_:viewFor:row)
        </code>
        . It’s then called by the table view for every row and column to get the
        appropriate cell.
    </p>
    <p>
        There’s a lot going on the method, so here’s a step-by-step breakdown:
    </p>
    <ol>
        <li>
            If there is no data to display, it returns no cells.
        </li>
        <li>
            Based on the column where the cell will display (Name, Date or Size),
            it sets the cell identifier, text and image.
        </li>
        <li>
            It gets a cell view by calling
            <code>
                make(withIdentifier:owner:)
            </code>
            . This method creates or reuses a cell with that identifier. Then it fills
            it with the information provided in the previous step and returns it.
        </li>
    </ol>
    <p>
        Next up, add this code inside
        <code>
            viewDidLoad()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1438284">
                    <td class="code" id="p143828code4">
                        <pre class="swift" style="font-family:monospace;">
                            tableView.delegate
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #a61390;">
                                self
                            </span>
                            tableView.dataSource
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #a61390;">
                                self
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here you tell the table view that its data source and delegate will be
        the view controller.
    </p>
    <p>
        The last step is to tell the table view to refresh the data when a new
        directory is selected.
    </p>
    <p>
        First, add this method to the
        <code>
            ViewController
        </code>
        implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1438285">
                    <td class="code" id="p143828code5">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #a61390;">
                                func
                            </span>
                            reloadFileList
                            <span style="color: #002200;">
                                (
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            directoryItems
                            <span style="color: #002200;">
                                =
                            </span>
                            directory?.contentsOrderedBy
                            <span style="color: #002200;">
                                (
                            </span>
                            sortOrder, ascending
                            <span style="color: #002200;">
                                :
                            </span>
                            sortAscending
                            <span style="color: #002200;">
                                )
                            </span>
                            tableView.reloadData
                            <span style="color: #002200;">
                                (
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                }
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This helper method refreshes the file list.
    </p>
    <p>
        First, it calls the
        <code>
            directory
        </code>
        method
        <code>
            contentsOrderedBy(_:ascending)
        </code>
        and returns a sorted array with the directory files. Then it calls the
        table view method
        <code>
            reloadData()
        </code>
        to tell it to refresh.
    </p>
    <p>
        Note that you only need to call this method when a new directory is selected.
    </p>
    <p>
        Go to the
        <code>
            representedObject
        </code>
        observer
        <code>
            didSet
        </code>
        , and replace this line of code:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1438286">
                    <td class="code" id="p143828code6">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #a61390;">
                                print
                            </span>
                            <span style="color: #002200;">
                                (
                            </span>
                            <span style="color: #bf1d1a;">
                                "Represented object:
                                <span style="color: #2400d9;">
                                    \(
                                </span>
                                url)"
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
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
                <tr id="p1438287">
                    <td class="code" id="p143828code7">
                        <pre class="swift" style="font-family:monospace;">
                            directory
                            <span style="color: #002200;">
                                =
                            </span>
                            Directory
                            <span style="color: #002200;">
                                (
                            </span>
                            folderURL
                            <span style="color: #002200;">
                                :
                            </span>
                            url
                            <span style="color: #002200;">
                                )
                            </span>
                            reloadFileList
                            <span style="color: #002200;">
                                (
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        You’ve just created an instance of
        <code>
            Directory
        </code>
        pointing to the folder URL, and it calls the
        <code>
            reloadFileList()
        </code>
        method to refresh the table view data.
    </p>
    <p>
        Build and run.
    </p>
    <p>
        Open a folder using the menu
        <em>
            File &gt; Open…
        </em>
        or the
        <em>
            Command+O
        </em>
        keyboard shortcut and watch the magic happen! Now the table is full of
        contents from the folder you just selected. Resize the columns to see all
        the information about each file or folder.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/table-first-population.png"
        alt="your table now shows content" width="560" height="291" class="aligncenter size-full wp-image-145756"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/table-first-population.png 560w, https://koenig-media.raywenderlich.com/uploads/2016/10/table-first-population-480x249.png 480w"
        sizes="(max-width: 560px) 100vw, 560px">
    </p>
    <p>
        Nice job!
    </p>
    <h2>
        Table View Interaction
    </h2>
    <p>
        In this section, you’ll work with some interactions to improve the UI.
    </p>
    <h3>
        Responding to User Selection
    </h3>
    <p>
        When the user selects one or more files, the application should update
        the information in the bottom bar to show the total number of files in
        the folder and how many are selected.
    </p>
    <p>
        In order to be notified when the selection changes in the table view,
        you need to implement
        <code>
            tableViewSelectionDidChange(_:)
        </code>
        in the delegate. This method will be called by the table view when it
        detects a change in the selection.
    </p>
    <p>
        Add this code to the
        <em>
            ViewController
        </em>
        implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1438288">
                    <td class="code" id="p143828code8">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #a61390;">
                                func
                            </span>
                            updateStatus
                            <span style="color: #002200;">
                                (
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            &nbsp;
                            <span style="color: #a61390;">
                                let
                            </span>
                            text
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #a61390;">
                                String
                            </span>
                            &nbsp;
                            <span style="color: #11740a; font-style: italic;">
                                // 1
                            </span>
                            <span style="color: #a61390;">
                                let
                            </span>
                            itemsSelected
                            <span style="color: #002200;">
                                =
                            </span>
                            tableView.selectedRowIndexes.
                            <span style="color: #a61390;">
                                count
                            </span>
                            &nbsp;
                            <span style="color: #11740a; font-style: italic;">
                                // 2
                            </span>
                            <span style="color: #a61390;">
                                if
                            </span>
                            <span style="color: #002200;">
                                (
                            </span>
                            directoryItems
                            <span style="color: #002200;">
                                ==
                            </span>
                            <span style="color: #a61390;">
                                nil
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            text
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #bf1d1a;">
                                "No Items"
                            </span>
                            <span style="color: #002200;">
                                }
                            </span>
                            <span style="color: #a61390;">
                                else
                            </span>
                            <span style="color: #a61390;">
                                if
                            </span>
                            <span style="color: #002200;">
                                (
                            </span>
                            itemsSelected
                            <span style="color: #002200;">
                                ==
                            </span>
                            <span style="color: #2400d9;">
                                0
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            text
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #bf1d1a;">
                                "
                                <span style="color: #2400d9;">
                                    \(
                                </span>
                                directoryItems!.count) items"
                            </span>
                            <span style="color: #002200;">
                                }
                            </span>
                            <span style="color: #a61390;">
                                else
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            text
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #bf1d1a;">
                                "
                                <span style="color: #2400d9;">
                                    \(
                                </span>
                                itemsSelected) of
                                <span style="color: #2400d9;">
                                    \(
                                </span>
                                directoryItems!.count) selected"
                            </span>
                            <span style="color: #002200;">
                                }
                            </span>
                            <span style="color: #11740a; font-style: italic;">
                                // 3
                            </span>
                            statusLabel.stringValue
                            <span style="color: #002200;">
                                =
                            </span>
                            text
                            <span style="color: #002200;">
                                }
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This method updates the status label text based on the user selection.
    </p>
    <ol>
        <li>
            The table view property
            <code>
                selectedRowIndexes
            </code>
            contains the indexes of the selected rows. To know how many items are
            selected, it just gets the array count.
        </li>
        <li>
            Based on the number of items, this builds the informative text string.
        </li>
        <li>
            Sets the status label text.
        </li>
    </ol>
    <p>
        Now, you just need to invoke this method when the user changes the table
        view selection. Add the following code inside the table view delegate extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1438289">
                    <td class="code" id="p143828code9">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #a61390;">
                                func
                            </span>
                            tableViewSelectionDidChange
                            <span style="color: #002200;">
                                (
                            </span>
                            _ notification
                            <span style="color: #002200;">
                                :
                            </span>
                            Notification
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            updateStatus
                            <span style="color: #002200;">
                                (
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                }
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        When the selection changes this method is called by the table view, and
        then it updates the status text.
    </p>
    <p>
        Build and run.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/table-selection-label.png"
        alt="selection label now configured" width="606" height="351" class="aligncenter size-full wp-image-145757"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/table-selection-label.png 606w, https://koenig-media.raywenderlich.com/uploads/2016/10/table-selection-label-480x278.png 480w"
        sizes="(max-width: 606px) 100vw, 606px">
    </p>
    <p>
        Try it out for yourself; select one or more files in the table view and
        watch the informative text change to reflect your selection.
    </p>
    <h3>
        Responding to Double-Click
    </h3>
    <p>
        In macOS, a double-click usually means the user has triggered an action
        and your program needs to perform it.
    </p>
    <p>
        For instance, when you’re dealing with files you usually expect the double-clicked
        file to open in its default application and for a folder, you expect to
        see its content.
    </p>
    <p>
        You’re going to implement double-click responses now.
    </p>
    <p>
        Double-click notifications are not sent via the table view delegate; instead,
        they’re sent as an action to the table view target. But to receive those
        notifications in the view controller, you need to set the table view’s
        <code>
            target
        </code>
        and
        <code>
            doubleAction
        </code>
        properties.
    </p>
    <div class="note">
        <p>
            <em>
                Note
            </em>
            : Target-action is a pattern used by most controls in Cocoa to notify
            events. If you’re not familiar with this pattern, you can learn about it
            in the
            <a title="Target-Action" href="https://developer.apple.com/library/mac/documentation/General/Devpedia-CocoaApp-MOSX/TargetAction.html"
            target="_blank">
                Target-Action
            </a>
            section of Apple’s
            <em>
                Cocoa Application Competencies for macOS
            </em>
            documentation.
        </p>
    </div>
    <p>
        Add the following code inside
        <code>
            viewDidLoad()
        </code>
        of the
        <code>
            ViewController
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14382810">
                    <td class="code" id="p143828code10">
                        <pre class="swift" style="font-family:monospace;">
                            tableView.target
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #a61390;">
                                self
                            </span>
                            tableView.doubleAction
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #6e371a;">
                                #selector(tableViewDoubleClick(_:))
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This tells the table view that the view controller will become the target
        for its actions, and then it sets the method that will be called after
        a double-click.
    </p>
    <p>
        Add the
        <code>
            tableViewDoubleClick(_:)
        </code>
        method implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14382811">
                    <td class="code" id="p143828code11">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #a61390;">
                                func
                            </span>
                            tableViewDoubleClick
                            <span style="color: #002200;">
                                (
                            </span>
                            _ sender
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #a61390;">
                                AnyObject
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            &nbsp;
                            <span style="color: #11740a; font-style: italic;">
                                // 1
                            </span>
                            guard tableView.selectedRow &gt;
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #2400d9;">
                                0
                            </span>
                            ,
                            <span style="color: #a61390;">
                                let
                            </span>
                            item
                            <span style="color: #002200;">
                                =
                            </span>
                            directoryItems?
                            <span style="color: #002200;">
                                [
                            </span>
                            tableView.selectedRow
                            <span style="color: #002200;">
                                ]
                            </span>
                            <span style="color: #a61390;">
                                else
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            <span style="color: #a61390;">
                                return
                            </span>
                            <span style="color: #002200;">
                                }
                            </span>
                            &nbsp;
                            <span style="color: #a61390;">
                                if
                            </span>
                            item.isFolder
                            <span style="color: #002200;">
                                {
                            </span>
                            <span style="color: #11740a; font-style: italic;">
                                // 2
                            </span>
                            <span style="color: #a61390;">
                                self
                            </span>
                            .representedObject
                            <span style="color: #002200;">
                                =
                            </span>
                            item.url
                            <span style="color: #a61390;">
                                as
                            </span>
                            <span style="color: #a61390;">
                                Any
                            </span>
                            <span style="color: #002200;">
                                }
                            </span>
                            <span style="color: #a61390;">
                                else
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            <span style="color: #11740a; font-style: italic;">
                                // 3
                            </span>
                            <span style="color: #400080;">
                                NSWorkspace
                            </span>
                            .shared
                            <span style="color: #002200;">
                                (
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            .open
                            <span style="color: #002200;">
                                (
                            </span>
                            item.url
                            <span style="color: #a61390;">
                                as
                            </span>
                            URL
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                }
                            </span>
                            <span style="color: #002200;">
                                }
                            </span>
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s the above code broken out step-by-step:
    </p>
    <ol>
        <li>
            If the table view selection is empty, it does nothing and returns. Also
            note that a double-click on an empty area of the table view will result
            in an
            <code>
                tableView.selectedRow
            </code>
            value equal to -1.
        </li>
        <li>
            If it’s a folder, it sets the
            <code>
                representedObject
            </code>
            property to the item’s URL. Then the table view refreshes to show the
            contents of that folder.
        </li>
        <li>
            If the item is a file, it opens it in the default application by calling
            the
            <code>
                NSWorkspace
            </code>
            method
            <code>
                openURL()
            </code>
        </li>
    </ol>
    <p>
        Build and run and check out your handiwork.
    </p>
    <p>
        Double-click on any file and observe how it opens in the default application.
        Now choose a folder and watch how the table view refreshes and displays
        the content of that folder.
    </p>
    <p>
        Whoa, wait, did you just create a DIY version of Finder? Sure looks that
        way!
    </p>
    <h3>
        Sorting Data
    </h3>
    <p>
        Everybody loves a good sort, and in this next section you’ll learn how
        to sort the table view based on the user’s selection.
    </p>
    <p>
        One of the best features of a table is one- or two-click sorting by a
        specific column. One click will sort it in ascending order and a second
        click will sort in descending order.
    </p>
    <p>
        Implementing this particular UI is easy because
        <code>
            NSTableView
        </code>
        packs most of the functionality right out of the box.
    </p>
    <p>
        <em>
            Sort descriptors
        </em>
        are what you’ll use to handle this bit, and they are simply instances
        of the
        <code>
            NSSortDescriptor
        </code>
        class that specify the desired attribute and sort order.
    </p>
    <p>
        After setting up descriptors, this is what happens: clicking on a column
        header in the table view will inform you, via the delegate, which attribute
        should be used, and then the user will be able sort the data.
    </p>
    <p>
        Once you set the sort descriptors, the table view provides all the UI
        to handle sorting, like clickable headers, arrows and notification of which
        sort descriptor was selected. However, it’s your responsibility to order
        the data based on that information, and refresh the table view to reflect
        the new order.
    </p>
    <p>
        You’ll learn how to do that right now.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/11/Screen-Shot-2015-11-29-at-6.24.36-PM.png">
            <img class="aligncenter size-full wp-image-121566" src="https://koenig-media.raywenderlich.com/uploads/2015/11/Screen-Shot-2015-11-29-at-6.24.36-PM.png"
            alt="Woot!" width="294" height="299" srcset="https://koenig-media.raywenderlich.com/uploads/2015/11/Screen-Shot-2015-11-29-at-6.24.36-PM.png 294w, https://koenig-media.raywenderlich.com/uploads/2015/11/Screen-Shot-2015-11-29-at-6.24.36-PM-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/11/Screen-Shot-2015-11-29-at-6.24.36-PM-64x64.png 64w"
            sizes="(max-width: 294px) 100vw, 294px">
        </a>
    </p>
    <p>
        Add the following code inside
        <code>
            viewDidLoad()
        </code>
        to create the sort descriptors:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14382812">
                    <td class="code" id="p143828code12">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #11740a; font-style: italic;">
                                // 1
                            </span>
                            <span style="color: #a61390;">
                                let
                            </span>
                            descriptorName
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #400080;">
                                NSSortDescriptor
                            </span>
                            <span style="color: #002200;">
                                (
                            </span>
                            key
                            <span style="color: #002200;">
                                :
                            </span>
                            Directory.FileOrder.Name.rawValue, ascending
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #a61390;">
                                true
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #a61390;">
                                let
                            </span>
                            descriptorDate
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #400080;">
                                NSSortDescriptor
                            </span>
                            <span style="color: #002200;">
                                (
                            </span>
                            key
                            <span style="color: #002200;">
                                :
                            </span>
                            Directory.FileOrder.Date.rawValue, ascending
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #a61390;">
                                true
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #a61390;">
                                let
                            </span>
                            descriptorSize
                            <span style="color: #002200;">
                                =
                            </span>
                            <span style="color: #400080;">
                                NSSortDescriptor
                            </span>
                            <span style="color: #002200;">
                                (
                            </span>
                            key
                            <span style="color: #002200;">
                                :
                            </span>
                            Directory.FileOrder.Size.rawValue, ascending
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #a61390;">
                                true
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            &nbsp;
                            <span style="color: #11740a; font-style: italic;">
                                // 2
                            </span>
                            tableView.tableColumns
                            <span style="color: #002200;">
                                [
                            </span>
                            <span style="color: #2400d9;">
                                0
                            </span>
                            <span style="color: #002200;">
                                ]
                            </span>
                            .sortDescriptorPrototype
                            <span style="color: #002200;">
                                =
                            </span>
                            descriptorName tableView.tableColumns
                            <span style="color: #002200;">
                                [
                            </span>
                            <span style="color: #2400d9;">
                                1
                            </span>
                            <span style="color: #002200;">
                                ]
                            </span>
                            .sortDescriptorPrototype
                            <span style="color: #002200;">
                                =
                            </span>
                            descriptorDate tableView.tableColumns
                            <span style="color: #002200;">
                                [
                            </span>
                            <span style="color: #2400d9;">
                                2
                            </span>
                            <span style="color: #002200;">
                                ]
                            </span>
                            .sortDescriptorPrototype
                            <span style="color: #002200;">
                                =
                            </span>
                            descriptorSize
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This is what this code does:
    </p>
    <ol>
        <li>
            Creates a sort descriptor for every column, complete with a key (Name,
            Date or Size), that indicates the attribute by which the file list can
            be ordered.
        </li>
        <li>
            Adds the sort descriptors to each column by setting its
            <code>
                sortDescriptorPrototype
            </code>
            property.
        </li>
    </ol>
    <p>
        When the user clicks on any column header, the table view will call the
        data source method
        <code>
            tableView(_:sortDescriptorsDidChange:)
        </code>
        , at which point the app should sort the data based on the supplied descriptor.
    </p>
    <p>
        Add the following code to the data source extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p14382813">
                    <td class="code" id="p143828code13">
                        <pre class="swift" style="font-family:monospace;">
                            <span style="color: #a61390;">
                                func
                            </span>
                            tableView
                            <span style="color: #002200;">
                                (
                            </span>
                            _ tableView
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #400080;">
                                NSTableView
                            </span>
                            , sortDescriptorsDidChange oldDescriptors
                            <span style="color: #002200;">
                                :
                            </span>
                            <span style="color: #002200;">
                                [
                            </span>
                            <span style="color: #400080;">
                                NSSortDescriptor
                            </span>
                            <span style="color: #002200;">
                                ]
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            <span style="color: #11740a; font-style: italic;">
                                // 1
                            </span>
                            guard
                            <span style="color: #a61390;">
                                let
                            </span>
                            sortDescriptor
                            <span style="color: #002200;">
                                =
                            </span>
                            tableView.sortDescriptors.first
                            <span style="color: #a61390;">
                                else
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            <span style="color: #a61390;">
                                return
                            </span>
                            <span style="color: #002200;">
                                }
                            </span>
                            <span style="color: #a61390;">
                                if
                            </span>
                            <span style="color: #a61390;">
                                let
                            </span>
                            order
                            <span style="color: #002200;">
                                =
                            </span>
                            Directory.FileOrder
                            <span style="color: #002200;">
                                (
                            </span>
                            rawValue
                            <span style="color: #002200;">
                                :
                            </span>
                            sortDescriptor.key
                            <span style="color: #002200;">
                                !
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                {
                            </span>
                            <span style="color: #11740a; font-style: italic;">
                                // 2
                            </span>
                            sortOrder
                            <span style="color: #002200;">
                                =
                            </span>
                            order sortAscending
                            <span style="color: #002200;">
                                =
                            </span>
                            sortDescriptor.ascending reloadFileList
                            <span style="color: #002200;">
                                (
                            </span>
                            <span style="color: #002200;">
                                )
                            </span>
                            <span style="color: #002200;">
                                }
                            </span>
                            <span style="color: #002200;">
                                }
                            </span>
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
            Retrieves the first sort descriptor that corresponds to the column header
            clicked by the user.
        </li>
        <li>
            Assigns the
            <code>
                sortOrder
            </code>
            and
            <code>
                sortAscending
            </code>
            properties of the view controller, and then calls
            <code>
                reloadFileList()
            </code>
            . You set it up earlier to get a sorted array of files and tell the table
            view to reload the data.
        </li>
    </ol>
    <p>
        Build and run.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/10/sortable-columns.png"
        alt="sortable-columns" width="619" height="298" class="aligncenter size-full wp-image-145673"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/10/sortable-columns.png 619w, https://koenig-media.raywenderlich.com/uploads/2016/10/sortable-columns-480x231.png 480w"
        sizes="(max-width: 619px) 100vw, 619px">
    </p>
    <p>
        Click any header to see your table view sort data. Click again in the
        same header to alternate between ascending and descending order.
    </p>
    <p>
        You’ve built a nice file viewer using a table view. Congratulations!
    </p>
    <h2>
        Where to Go From Here?
    </h2>
    <div class="inline-video-ad" id="sub-banner-inline">
        <div class="inline-video-ad-wrapper">
            <a href="https://videos.raywenderlich.com/courses">
                <div class="col-wrapper">
                    <div class="col">
                        <img src="https://cdn3.raywenderlich.com/wp-content/themes/raywenderlich/images/global/video-yeti@2x.png"
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
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/10/FileViewer_final2.zip">
            here
        </a>
        .
    </p>
    <p>
        This macOS NSTableView tutorial covered quite a bit, and you should now
        feel much more confident in your ability to use table views to organize
        data. In addition, you also covered:
    </p>
    <ul>
        <li>
            The basics of table view construction, including the unique qualities
            of headers, rows, columns and cells.
        </li>
        <li>
            How to add columns to display more data.
        </li>
        <li>
            How to identify various components for later reference.
        </li>
        <li>
            How to load data in the table.
        </li>
        <li>
            How to respond to various user interactions.
        </li>
    </ul>
    <p>
        There is a lot more you can do with table views to build elegant UI for
        your app. If you’re looking to learn more about it, consider the following
        resources:
    </p>
    <ul>
        <li>
            Apple’s
            <a title="Table View Programming Guide for Mac" href="https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/TableView/Introduction/Introduction.html"
            target="_blank">
                Table View Programming Guide for Mac
            </a>
            .
        </li>
        <li>
            WWDC 2016 – Session 239 Video –
            <a href="https://developer.apple.com/videos/play/wwdc2016/239/" target="_blank">
                Crafting Modern Cocoa Apps
            </a>
            for a fast course in how to build a cutting edge table view.
        </li>
        <li>
            WWDC 2011 – Session 120 Video
            <a title="View Based NSTableView Basic to Advanced " href="https://developer.apple.com/videos/play/wwdc2011-120/"
            target="_blank">
                View Based NSTableView Basic to Advanced
            </a>
            .
        </li>
        <li>
            <a title="TableViewPlayGround" href="https://developer.apple.com/library/mac/samplecode/TableViewPlayground/Introduction/Intro.html#//apple_ref/doc/uid/DTS40010727"
            target="_blank">
                TableViewPlayGround
            </a>
            has Objective-C sample code to show how to create different kinds of custom
            table views.
        </li>
    </ul>
    <p>
        If you have any questions or comments on this tutorial, feel free to join
        the discussion below in the forums!
    </p>
</div>