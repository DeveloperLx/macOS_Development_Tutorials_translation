# 绑定在macOS上的Cocoa

#### [原文地址](https://www.raywenderlich.com/141297/cocoa-bindings-macos) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div class="note">
        <p>
            <em>
                Update note:
            </em>
            This Cocoa Bindings on macOS tutorial has been updated to Xcode 8 and
            Swift 3 by Andy Pereira. The
            <a href="https://www.raywenderlich.com/124490/cocoa-bindings-os-x-tutorial">
                original
            </a>
            tutorial was written by Jake Gundersen.
        </p>
    </div>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-250x250.png"
        alt="Cocoa-Bindings-on-macOS" width="250" height="250" class="alignright size-thumbnail wp-image-129292"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
    </p>
    <p>
        Cocoa bindings, or simply
        <em>
            bindings
        </em>
        , free you up from having to spend hours writing
        <i>
            glue code
        </i>
        ; that is, creating links between the model and the view in the controller
        when using the Model-View-Controller (MVC) pattern.
    </p>
    <p>
        Cocoa bindings have a simple goal: write less code. You’ll discover as
        you work through this that they do indeed live up to this objective.
    </p>
    <p>
        In this Cocoa Bindings on macOS tutorial, you’ll create an app that displays
        search results from the App Store via the iTunes API as you learn how to
        use Cocoa bindings to do the following:
    </p>
    <ul>
        <li>
            Set the relationship within Interface Builder between a data model property
            and a UI element, such as a label or a button
        </li>
        <li>
            Set up default values
        </li>
        <li>
            Apply formatting, such as a currency or date format
        </li>
        <li>
            Change the data structure, e.g. when converting a value into a representing
            color
        </li>
    </ul>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/cb-rageface1-e1445168631127.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/10/cb-rageface1-e1445168631127-435x320.png"
            alt="cb-rageface1" width="435" height="320" class="aligncenter size-medium wp-image-118691"
            srcset="https://koenig-media.raywenderlich.com/uploads/2015/10/cb-rageface1-e1445168631127-435x320.png 435w, https://koenig-media.raywenderlich.com/uploads/2015/10/cb-rageface1-e1445168631127.png 644w"
            sizes="(max-width: 435px) 100vw, 435px">
        </a>
    </p>
    <h2>
        Getting Started
    </h2>
    <p>
        Although you won’t have to spend the next several of your hours coding,
        there’s still a fair amount of work ahead in
        <a href="http://www.raywenderlich.com/?s=Interface+Builder&amp;cof=FORID%3A10"
        target="_blank" title="Interface Builder">
            Interface Builder
        </a>
        using
        <a href="http://www.raywenderlich.com/?s=Auto+Layout&amp;cof=FORID%3A10"
        target="_blank" title="Auto Layout">
            Auto Layout
        </a>
        , so familiarity with both of these tools is a prerequisite.
    </p>
    <p>
        Download the starter project
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/09/AppResearchBindings-Starter.zip"
        title="here">
            here
        </a>
        .
    </p>
    <p>
        Build and run the project, and you’ll see it has a nice interface — but
        no data.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.01.30-PM-700x463.png"
        alt="First run" width="700" height="463" class="aligncenter size-large wp-image-125398"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.01.30-PM-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.01.30-PM-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.01.30-PM-768x508.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.01.30-PM.png 1133w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        You’ll also see there are a couple of files to help you along.
        <em>
            iTunesRequestManager.swift
        </em>
        contains a struct with two static methods. The first sends a query to
        the iTunes API and downloads a JSON payload that contains iOS apps results
        for a provided search string, while the second is a helper method to download
        an image asynchronously.
    </p>
    <p>
        The second file,
        <em>
            iTunesResults.swift
        </em>
        , defines a data model class that matches the data downloaded by the iTunes
        search method.
    </p>
    <div class="note">
        <p>
            <em>
                Note
            </em>
            : All variables in the
            <code>
                Result
            </code>
            class are defined as
            <em>
                dynamic
            </em>
            . This is because bindings rely on key-value coding, and therefore require
            the Objective-C runtime. Adding the
            <code>
                dynamic
            </code>
            keyword guarantees that access to that property is always dynamically
            dispatched using the Objective-C runtime.
        </p>
        <p>
            The class inherits from
            <em>
                NSObject
            </em>
            ; this is also a requirement for bindings. You’ll discover why a little
            later, when you add a variable to your view controller class.
        </p>
    </div>
    <h2>
        Searching via iTunes
    </h2>
    <p>
        First, you’re going to retrieve search results via the iTunes API and
        add them to an
        <code>
            NSArrayController.
        </code>
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and look at the objects in the
        <em>
            View Controller Scene
        </em>
        . Note that objects on which you’ll set bindings all have the labels
        <em>
            ‘(Bind)’
        </em>
        .
    </p>
    <h3>
        Setting Up an NSArrayController
    </h3>
    <p>
        The
        <code>
            NSArrayController
        </code>
        object manages the content of a
        <code>
            NSTableView
        </code>
        . This content often takes the form of an array of model objects.
    </p>
    <div class="note">
        <p>
            <em>
                Note
            </em>
            :
            <code>
                NSArrayController
            </code>
            offers much more than a simple array, including managing object selection,
            sorting and filtering. Cocoa Bindings make heavy use of this functionality.
        </p>
    </div>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        . Find an
        <code>
            NSArrayController
        </code>
        object in the
        <em>
            Object Library
        </em>
        , and drag it into the list of objects under the
        <em>
            View Controller Scene
        </em>
        grouping in the document outline:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/02/add-array-controller-430x500.png"
        alt="add array controller" width="430" height="500" class="aligncenter size-large wp-image-126104"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/02/add-array-controller-430x500.png 430w, https://koenig-media.raywenderlich.com/uploads/2016/02/add-array-controller-275x320.png 275w, https://koenig-media.raywenderlich.com/uploads/2016/02/add-array-controller.png 692w"
        sizes="(max-width: 430px) 100vw, 430px">
    </p>
    <p>
        Next, open the assistant editor and make sure
        <em>
            ViewController.swift
        </em>
        is the file you’re working on. Control-drag from the
        <em>
            Array Controller
        </em>
        object in the
        <em>
            Storyboard
        </em>
        to the
        <em>
            ViewController.swift
        </em>
        source to add an outlet to it, and name it
        <em>
            searchResultsController
        </em>
        :
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.39.36-PM-700x221.png"
        alt="add outlet" width="700" height="221" class="aligncenter size-large wp-image-125400"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.39.36-PM-700x221.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.39.36-PM-480x152.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.39.36-PM.png 721w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h3>
        Adding the Search Box and Button
    </h3>
    <p>
        Now you’re ready to use the search box and button to get a list of search
        results and add them to the
        <code>
            searchResultsController
        </code>
        object.
    </p>
    <p>
        Control-drag from the
        <em>
            search button
        </em>
        in the storyboard to the
        <em>
            ViewController.swift
        </em>
        source to create an action method. Select to create an
        <em>
            Action
        </em>
        connection and name it
        <em>
            searchClicked
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/09/addConnectionMethod.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/09/addConnectionMethod-650x195.png"
            alt="addConnectionMethod" width="650" height="195" class="aligncenter size-large wp-image-143260"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/09/addConnectionMethod-650x195.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/09/addConnectionMethod-480x144.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/09/addConnectionMethod.png 826w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Now add the following code inside
        <code>
            searchClicked(:_)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1412971">
                    <td class="code" id="p141297code1">
                        <pre class="swift" style="font-family:monospace;">
                            //1 if (searchTextField.stringValue == "") { return } //2 guard let resultsNumber
                            = Int(numberResultsComboBox.stringValue) else { return } //3 iTunesRequestManager.getSearchResults(searchTextField.stringValue,
                            results: resultsNumber, langString: "en_us") { results, error in //4 let
                            itunesResults = results.map { return Result(dictionary: $0) } &nbsp; //Deal
                            with rank here later &nbsp; //5 DispatchQueue.main.async { //6 self.searchResultsController.content
                            = itunesResults print(self.searchResultsController.content) } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Taking each line in turn:
    </p>
    <ol>
        <li>
            Check the text field; if it’s blank, don’t send that query to iTunes search
            API.
        </li>
        <li>
            Get the value in the dropdown. This number is passed to the API and controls
            how many search results to return. There’s a number of preconfigured options
            in the dropdown, but you can also type in other numbers — 200 is the maximum.
        </li>
        <li>
            Make a call to
            <code>
                getSearchResults(_:results:langString:completionHandler:)
            </code>
            . This passes in the number of results from the combo box and the query
            string you typed into the text field. It returns, via a completion handler,
            either an array of
            <code>
                Dictionary
            </code>
            result objects or an
            <code>
                NSError
            </code>
            object if there’s a problem completing the query. Note that the method
            already handles the JSON parsing.
        </li>
        <li>
            Here you use some Swift-style array mapping to pass the dictionary into
            an initialization method that creates a
            <code>
                Result
            </code>
            object. When done, the
            <code>
                itunesResults
            </code>
            variable contains an array of
            <code>
                Result
            </code>
            objects.
        </li>
        <li>
            Before you can set this new data on the
            <code>
                searchResultsController
            </code>
            , you need to make sure you’re on the main thread. Therefore you use
            <code>
                DispatchQueue.main.async
            </code>
            to get to the main queue. You haven’t set up any bindings, but once you
            have, altering the content property on the
            <code>
                searchResultsController
            </code>
            will update the
            <code>
                NSTableView
            </code>
            (and potentially other UI elements) on the current thread. Updating UI
            on a background thread is always a no-no.
        </li>
        <li>
            Finally you set the content property of the
            <code>
                NSArrayController
            </code>
            . The array controller has a number of different methods to add or remove
            objects it manages. Each time you search, you want to clear out the previous
            results and work with the results of the latest query. For now, print the
            content of
            <code>
                searchResultsController
            </code>
            to the console to verify that everything works as planned.
        </li>
    </ol>
    <p>
        Now, add the following
        <code>
            ViewController
        </code>
        extension:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1412972">
                    <td class="code" id="p141297code2">
                        <pre class="swift" style="font-family:monospace;">
                            extension ViewController: NSTextFieldDelegate { func control(_ control:
                            NSControl, textView: NSTextView, doCommandBy commandSelector: Selector)
                            -&gt; Bool { if commandSelector == #selector(insertNewline(_:)) { searchClicked(searchTextField)
                            } return false } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This invokes
        <code>
            searchClicked(_:)
        </code>
        when the user presses Enter in the text field, just as if you’d clicked
        the search button. This simply makes it easier to run a quick search using
        the keyboard.
    </p>
    <p>
        Build and run, type
        <em>
            flappy
        </em>
        into the search bar and press Enter or click the Search button. You should
        see something like the following show up in the console:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.04.46-PM-650x82.png"
        alt="Search result" width="650" height="82" class="alignnone size-large wp-image-142721"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.04.46-PM-650x82.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.04.46-PM-480x60.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.04.46-PM.png 1192w"
        sizes="(max-width: 650px) 100vw, 650px">
    </p>
    <h2>
        Your First Bindings
    </h2>
    <p>
        It’s time to get to the meat of this tutorial!
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/allthethings1.jpg">
            <img src="https://koenig-media.raywenderlich.com/uploads/2015/10/allthethings1.jpg"
            alt="allthethings1" width="400" height="300" class="aligncenter size-full wp-image-118939">
        </a>
    </p>
    <p>
        The first step is to bind the array controller to the table view.
    </p>
    <p>
        Open up
        <em>
            Main.storyboard
        </em>
        and select the table view titled
        <em>
            Search Results Table View (Bind)
        </em>
        . Open the
        <em>
            Bindings Inspector
        </em>
        : it’s the second-to-last-icon in the right pane, just before the
        <em>
            View Effects Inspector
        </em>
        .
    </p>
    <p>
        Expand the
        <em>
            Content
        </em>
        option under the
        <em>
            Table Contents
        </em>
        heading. Check the box next to
        <em>
            ‘Bind to ‘
        </em>
        and make sure
        <em>
            Search Results Controller
        </em>
        is displayed in the dropdown box. Finally, make sure the
        <em>
            Controller Key
        </em>
        is set to
        <em>
            arrangedObjects
        </em>
        , like so:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/TableViewBinding-170x320.png"
        alt="TableViewBinding" width="170" height="320" class="aligncenter size-medium wp-image-126033"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/TableViewBinding-170x320.png 170w, https://koenig-media.raywenderlich.com/uploads/2016/01/TableViewBinding-265x500.png 265w, https://koenig-media.raywenderlich.com/uploads/2016/01/TableViewBinding.png 520w"
        sizes="(max-width: 170px) 100vw, 170px">
    </p>
    <p>
        Build and run, and search for something you know will return a large number
        of results. You’ll see at most five results, unless you changed the number
        in the dropdown. Thanks to the bindings, the array controller automatically
        represents its content in the table view. However, they all say “Table
        View Cell”.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/arrayboundnotitlesintable-700x463.png"
        alt="arrayboundnotitlesintable" width="700" height="463" class="aligncenter size-large wp-image-126034"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/arrayboundnotitlesintable-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/arrayboundnotitlesintable-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/arrayboundnotitlesintable-768x508.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        You’re getting a bunch of duplicate hits because the text fields in the
        cells have no idea which properties on the data model they should read.
    </p>
    <h3>
        Binding Text Fields to Their Properties
    </h3>
    <p>
        Open up
        <em>
            Main.storyboard
        </em>
        and go to the
        <em>
            View Controller Scene
        </em>
        . Expand the objects in the table view until you find the text field named
        <em>
            Title TextField (Bind)
        </em>
        . Select this object and open the
        <em>
            Bindings Inspector
        </em>
        .
    </p>
    <p>
        Expand the
        <em>
            Value
        </em>
        option and bind to the
        <em>
            Table Cell View
        </em>
        object. Ensure the
        <em>
            Model Key Path
        </em>
        is
        <em>
            objectValue.trackName
        </em>
        .
    </p>
    <p>
        <code>
            objectValue
        </code>
        is a property on the table cell view that gets set by the
        <code>
            NSTableView
        </code>
        on each cell view object from its binding to the table.
    </p>
    <p>
        <code>
            objectValue
        </code>
        is, in this case, equal to the
        <code>
            Result
        </code>
        model object for that row.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/trackName.png"
        alt="trackName" width="248" height="215" class="aligncenter size-full wp-image-126070">
    </p>
    <p>
        Repeat the above process for
        <em>
            Publisher TextField (Bind)
        </em>
        by binding the value of this element to
        <em>
            objectValue.artistName
        </em>
        .
    </p>
    <p>
        Build and run, and search again. This time, the title and publisher show
        up:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/title-and-publisher-700x463.png"
        alt="title and publisher" width="700" height="463" class="aligncenter size-large wp-image-126071"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/title-and-publisher-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/title-and-publisher-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/title-and-publisher-768x508.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/title-and-publisher.png 1133w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h3>
        Adding in Rank
    </h3>
    <p>
        How about that missing rank column? Rank isn’t set on the data model object
        you get from iTunes. However, the order of the results from iTunes does
        tell you the order in which they display on a device when searching iTunes.
    </p>
    <p>
        With a little more work you can set the rank value.
    </p>
    <p>
        Add the following code in
        <code>
            ViewController
        </code>
        under the
        <code>
            //Deal with rank here later
        </code>
        comment:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1412973">
                    <td class="code" id="p141297code3">
                        <pre class="swift" style="font-family:monospace;">
                            .enumerated() .map({ index, element -&gt; Result in element.rank = index
                            + 1 return element })
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This code calls
        <code>
            enumerated()
        </code>
        in order to get the index and the object at the index. Then it calls
        <code>
            map(:_)
        </code>
        to set the rank value for each object and return an array with that result.
    </p>
    <p>
        Now, go back to
        <em>
            Main.storyboard
        </em>
        , select
        <em>
            Rank TextField (Bind)
        </em>
        and open the
        <em>
            Bindings Inspector
        </em>
        . In the
        <em>
            Value
        </em>
        section, bind to the
        <em>
            Table Cell View
        </em>
        . Make sure
        <em>
            Controller Key
        </em>
        is empty, and set
        <em>
            Model Key Path
        </em>
        to
        <code>
            objectValue.rank
        </code>
        .
    </p>
    <p>
        Build and run, and the app shows the rank in the first column of the table
        view:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/ranktitlepublisher-700x463.png"
        alt="ranktitlepublisher" width="700" height="463" class="aligncenter size-large wp-image-126072"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/ranktitlepublisher-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/ranktitlepublisher-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/ranktitlepublisher-768x508.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/ranktitlepublisher.png 1133w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Now you need to bind the
        <code>
            Result
        </code>
        object selected by the user to the rest of the UI.
    </p>
    <h2>
        Binding a Table View’s Selection
    </h2>
    <p>
        Binding to a selection in a table involves two steps:
    </p>
    <ol>
        <li>
            You first bind the
            <code>
                NSArrayController
            </code>
            to the table selection.
        </li>
        <li>
            Then you can bind the properties of the
            <code>
                selection
            </code>
            object in the
            <cdoe>
                NSArrayController to the individual labels and other properties.
            </cdoe>
        </li>
    </ol>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        . Select the
        <em>
            Search Results Table View (Bind)
        </em>
        and open the
        <em>
            Bindings Inspector
        </em>
        .
    </p>
    <p>
        Expand the
        <em>
            Selection Indexes
        </em>
        option in the
        <em>
            Table Content
        </em>
        section. Check
        <em>
            Bind to
        </em>
        the
        <em>
            Search Results Controller
        </em>
        object.
    </p>
    <p>
        Enter
        <em>
            selectionIndexes
        </em>
        into the
        <em>
            Controller Key
        </em>
        box. The table has a
        <code>
            selectionIndexes
        </code>
        property that contains a set of indexes that the user has selected in
        the table.
    </p>
    <p>
        In this case, I’ve set the table view to only allow a single selection.
        You could work with more than one selection if your app requires it, similar
        to how Finder lets you select multiple files.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/selectionIndexes.png"
        alt="selectionIndexes" width="248" height="262" class="aligncenter size-full wp-image-126073">
    </p>
    <p>
        The
        <code>
            NSArrayController
        </code>
        object has a
        <code>
            selection
        </code>
        property that returns an array of objects. When you bind the
        <code>
            selectionIndexes
        </code>
        property from the table view to the array controller, the
        <code>
            selection
        </code>
        property will be populated with the objects in the array controller that
        correspond to the indexes selected in the table.
    </p>
    <p>
        The next step is to bind the labels and other UI elements to the selected
        object.
    </p>
    <p>
        Find and select the
        <em>
            App Name Label (Bind)
        </em>
        . Bind its value to the
        <em>
            Search Results Controller
        </em>
        .
        <em>
            Controller Key
        </em>
        should be
        <em>
            selection
        </em>
        , and
        <em>
            Model Key Path
        </em>
        should be
        <em>
            trackName
        </em>
        .
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/mainTrackName.png"
        alt="mainTrackName" width="247" height="193" class="aligncenter size-full wp-image-126075">
    </p>
    <p>
        Build and run, select any app in the table view and its title will appear
        in the text field:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Main-Title-700x463.png"
        alt="Main Title" width="700" height="463" class="aligncenter size-large wp-image-126076"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Main-Title-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/Main-Title-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Main-Title-768x508.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/Main-Title.png 1133w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        You’ve seen how easy it can be to get data from your model into your UI.
        But what if the data needs to be formatted in some way, such as a currency
        or as a date?
    </p>
    <p>
        Luckily, there’s a built-in set of objects that make it easy to change
        the way a specific piece of data is displayed in a label.
    </p>
    <h2>
        Formatting Bound Data
    </h2>
    <p>
        Find the label titled
        <em>
            Price Label (Bind)
        </em>
        . Bind it to the
        <em>
            Search Results Controller
        </em>
        object, and ensure
        <em>
            Controller Key
        </em>
        is
        <em>
            selection
        </em>
        .
    </p>
    <p>
        Set
        <em>
            Model Key Path
        </em>
        to
        <em>
            price
        </em>
        . Next, find a
        <em>
            Number Formatter
        </em>
        in the Object Library. Drag it to the
        <code>
            NSTextFieldCell
        </code>
        named
        <em>
            Label
        </em>
        , just under the
        <em>
            Price
        </em>
        text field.
    </p>
    <p>
        Finally, select the
        <em>
            Number Formatter
        </em>
        , open the
        <em>
            Attributes Inspector
        </em>
        and change the
        <em>
            Style
        </em>
        to
        <em>
            Currency
        </em>
        .
    </p>
    <p>
        When you’re done, your storyboard and inspector should look like the following:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/09/currencyFormatter-1.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/09/currencyFormatter-1-650x321.png"
            alt="currencyFormatter" width="650" height="321" class="aligncenter size-large wp-image-143266"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/09/currencyFormatter-1-650x321.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/09/currencyFormatter-1-480x237.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/09/currencyFormatter-1.png 1259w"
            sizes="(max-width: 650px) 100vw, 650px">
        </a>
    </p>
    <p>
        Build and run, select any app from the list and the currencies should
        all display correctly:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/priceformatted-700x463.png"
        alt="priceformatted" width="700" height="463" class="aligncenter size-large wp-image-126078"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/priceformatted-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/priceformatted-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/priceformatted-768x508.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/priceformatted.png 1133w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <div class="note">
        <p>
            <em>
                Note
            </em>
            : Number formatters are very powerful. In addition to currencies, you
            can also control how many digits follow a decimal point, percentages, or
            have the number spelled out in words.
        </p>
        <p>
            There are formatter objects for dates, byte counts and several other less-common
            situations. If none of those suit your needs, you can even create your
            own custom formatters.
        </p>
    </div>
    <h3>
        Formatting as Bytes
    </h3>
    <p>
        You’ll be using a
        <em>
            Byte Count Formatter
        </em>
        next to show the file size.
    </p>
    <p>
        Find and select
        <em>
            File Size Label (Bind)
        </em>
        , open the
        <em>
            Bindings Inspector
        </em>
        and bind it to the
        <em>
            Search Results Controller
        </em>
        . Set
        <em>
            Controller Key
        </em>
        to
        <em>
            selection
        </em>
        and
        <em>
            Model Key Path
        </em>
        to
        <em>
            fileSizeInBytes
        </em>
        .
    </p>
    <p>
        Then find a
        <em>
            Byte Count Formatter
        </em>
        in the
        <em>
            Object Library
        </em>
        and attach it to the
        <em>
            NSTextFieldCell
        </em>
        . There’s no need to configure anything here; the default settings on
        a byte formatter will work just fine.
    </p>
    <p>
        You should see your byte count formatter in the document outline like
        so:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-formatter.png"
        alt="byte count formatter" width="349" height="124" class="aligncenter size-full wp-image-126083">
    </p>
    <p>
        Build and run, select an app in the list, and you’ll see file size using
        the proper units, such as KB, MB, and GB:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-final-700x463.png"
        alt="byte count final" width="700" height="463" class="aligncenter size-large wp-image-126084"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-final-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-final-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-final-768x508.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-final.png 1133w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        You’re quite used to binding things by now, so here’s a short list of
        the remaining keys you need to bind:
    </p>
    <ul>
        <li>
            Bind the
            <em>
                Artist Label (Bind)
            </em>
            to
            <em>
                artistName
            </em>
            .
        </li>
        <li>
            Bind the
            <em>
                Publication Date (Bind)
            </em>
            to
            <em>
                releaseDate
            </em>
            .
        </li>
        <li>
            Add a
            <em>
                Date Formatter
            </em>
            ; the default settings are fine.
        </li>
        <li>
            Bind the
            <em>
                All Ratings Count (Bind)
            </em>
            to
            <em>
                userRatingCount
            </em>
            .
        </li>
        <li>
            Bind the
            <em>
                All Ratings (Bind)
            </em>
            to
            <em>
                averageUserRating
            </em>
            .
        </li>
        <li>
            Bind the
            <em>
                Genre Label (Bind)
            </em>
            to
            <em>
                primaryGenre
            </em>
            .
        </li>
    </ul>
    <p>
        All these labels should be bound to the
        <em>
            Search Results Controller
        </em>
        and the
        <em>
            selection
        </em>
        controller key.
    </p>
    <p>
        For more precision in your UI, you can also bind the
        <em>
            Description Text View (Bind)
        </em>
        , the
        <em>
            Attributed String
        </em>
        binding, to the
        <em>
            itemDescription
        </em>
        Model Key Path. Make sure you bind the
        <code>
            NSTextView
        </code>
        , which is several levels down in the hierarchy,
        <i>
            not
        </i>
        the
        <code>
            NSScrollView
        </code>
        which is at the top.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/09/selecttextView.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/09/selecttextView-412x320.png"
            alt="selecttextView" width="360" height="280" class="aligncenter size-medium wp-image-143267"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/09/selecttextView-412x320.png 412w, https://koenig-media.raywenderlich.com/uploads/2016/09/selecttextView.png 602w"
            sizes="(max-width: 360px) 100vw, 360px">
        </a>
    </p>
    <p>
        Build and run, and you’ll see most of the UI populate:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/mostly-populated-700x421.png"
        alt="mostly populated" width="700" height="421" class="aligncenter size-large wp-image-126085"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/mostly-populated-700x421.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/mostly-populated-480x289.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/mostly-populated-768x462.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/mostly-populated.png 1200w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        Binding Images
    </h2>
    <p>
        The next step is to bind the image for the icon to the
        <em>
            Icon Image View
        </em>
        . This is a little trickier because the JSON doesn’t contain the actual
        image, but instead a URL for the image.
    </p>
    <p>
        <code>
            Result
        </code>
        includes a method to download the image file and make it available as
        an
        <code>
            NSImage
        </code>
        on the
        <code>
            artworkImage
        </code>
        property.
    </p>
    <h3>
        Just-in-Time Downloads
    </h3>
    <p>
        You don’t want to download all the icons at once — just the one for the
        current selection in the table. You’ll download a new icon whenever the
        selection changes.
    </p>
    <p>
        Add the following method to
        <em>
            ViewController
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1412974">
                    <td class="code" id="p141297code4">
                        <pre class="swift" style="font-family:monospace;">
                            //1 func tableViewSelectionDidChange(_ notification: NSNotification) {
                            //2 guard let result = searchResultsController.selectedObjects.first as?
                            Result else { return } //3 result.loadIcon() }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s the play-by-play:
    </p>
    <ol>
        <li>
            <code>
                tableViewSelectionDidChange(_:)
            </code>
            fires every time the user selects a different row in the table.
        </li>
        <li>
            The array controller property
            <code>
                selectedObjects
            </code>
            returns an array containing all the objects for the indexes of the rows
            selected in the table. In your case, the table will only permit a single
            selection, so this array always contains a single object. You store the
            object in the
            <code>
                result
            </code>
            object.
        </li>
        <li>
            Finally, you call
            <code>
                loadIcon()
            </code>
            . This method downloads the image on a background thread and then updates
            the
            <code>
                Result
            </code>
            objects
            <code>
                artworkImage
            </code>
            property when the image downloads on the main thread.
        </li>
    </ol>
    <h3>
        Binding the Image View
    </h3>
    <p>
        Now that your code is in place, you’re ready to bind the image view.
    </p>
    <p>
        Head back to
        <em>
            Main.storyboard
        </em>
        , select the
        <em>
            Icon Image View (Bind)
        </em>
        object and open the
        <em>
            Bindings Inspector
        </em>
        .
    </p>
    <p>
        Go to the
        <em>
            Value
        </em>
        section and bind to the
        <em>
            Search Results Controller
        </em>
        , set
        <em>
            Controller Key
        </em>
        to
        <em>
            selection
        </em>
        and
        <em>
            Model Key Path
        </em>
        to
        <em>
            artworkImage
        </em>
        .
    </p>
    <p>
        Did you notice the
        <em>
            Value Path
        </em>
        and a
        <em>
            Value URL
        </em>
        sections? Both of these bindings are intended for local resources only.
        You
        <i>
            can
        </i>
        connect them to a network resource, but that will block the UI thread
        until the resource has finished downloading.
    </p>
    <p>
        Build and run, search for
        <em>
            fruit
        </em>
        and then select a row. You’ll see the icon image appear once it has downloaded:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/icon-populated-700x421.png"
        alt="icon populated" width="700" height="421" class="aligncenter size-large wp-image-126088"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/icon-populated-700x421.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/icon-populated-480x289.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/icon-populated-768x462.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/icon-populated.png 1200w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        The collection view beneath the description text view is currently looking
        a little bare. Time to populate that with some screenshots.
    </p>
    <h3>
        Populating the Collection View
    </h3>
    <p>
        First you’ll bind the collection view to the
        <code>
            screenShots
        </code>
        property and then ensure the
        <code>
            screenShots
        </code>
        array populated correctly.
    </p>
    <p>
        Select the
        <em>
            Screen Shot Collection View (Bind)
        </em>
        . Open the
        <em>
            Bindings Inspector
        </em>
        and expand the
        <em>
            Content
        </em>
        binding in the
        <em>
            Content
        </em>
        group.
    </p>
    <p>
        Bind to the
        <em>
            Search Results Controller
        </em>
        , set
        <em>
            Controller Key
        </em>
        to
        <em>
            selection
        </em>
        and
        <em>
            Model Key Path
        </em>
        to
        <em>
            screenShots
        </em>
        .
    </p>
    <p>
        The
        <code>
            screenShots
        </code>
        array starts out empty.
        <code>
            loadScreenShots()
        </code>
        downloads the image files and populates the
        <code>
            screenShots
        </code>
        array with
        <code>
            NSImage
        </code>
        objects.
    </p>
    <p>
        Add the following line to
        <em>
            ViewController.swift
        </em>
        , in
        <code>
            tableViewSelectionDidChange(_:)
        </code>
        , right after
        <code>
            result.loadIcon()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1412975">
                    <td class="code" id="p141297code5">
                        <pre class="swift" style="font-family:monospace;">
                            result.loadScreenShots()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This populates the screenshot images and creates the right number of views.
    </p>
    <p>
        The next thing you need to do is set the right collection view item prototype.
        Although the collection view item scene is present in the storyboard, it’s
        not connected to the collection view. You’ll have to create this connection
        in code.
    </p>
    <p>
        Add the following code to the end of
        <code>
            viewDidLoad()
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
                <tr id="p1412976">
                    <td class="code" id="p141297code6">
                        <pre class="swift" style="font-family:monospace;">
                            let itemPrototype = self.storyboard?.instantiateController(withIdentifier:
                            "collectionViewItem") as! NSCollectionViewItem collectionView.itemPrototype
                            = itemPrototype
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now that the collection view knows how to create each item via the prototype,
        you need to provide the content for each item via a binding.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and select
        <em>
            Screen Shot Image View (Bind)
        </em>
        inside the
        <em>
            Collection View Item Scene
        </em>
        . You’ll find this floating next to the main view controller.
    </p>
    <p>
        Bind the
        <em>
            Value
        </em>
        option to the
        <em>
            Collection View Item
        </em>
        object. The controller key should be blank, and
        <em>
            Model Key Path
        </em>
        should be
        <em>
            representedObject
        </em>
        .
    </p>
    <p>
        The
        <code>
            representedObject
        </code>
        property represents the object in the collection view array for that item;
        in this case, it’s an
        <code>
            NSImage
        </code>
        object.
    </p>
    <p>
        Build and run, and you’ll see see the screenshots appearing below the
        description text:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/screenshots-700x421.png"
        alt="screenshots" width="700" height="421" class="aligncenter size-large wp-image-126089"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/screenshots-700x421.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/screenshots-480x289.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/screenshots-768x462.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/screenshots.png 1200w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        Great work! There’s just a few more features of Cocoa Bindings to cover
        before wrapping up.
    </p>
    <h2>
        Binding Other Properties
    </h2>
    <p>
        Your UI could use a bit of feedback. Users don’t like to stare at static
        screens when something is loading, and they’ll assume the worst when nothing
        happens in response to a user action.
    </p>
    <p>
        Instead of leaving a static screen, you’ll show a spinner to the user
        while the image downloads.
    </p>
    <h3>
        Seting Up a Progress Spinner
    </h3>
    <p>
        You can easily bind a progress spinner to a new property in the
        <code>
            ViewController
        </code>
        . Add the following property to
        <code>
            ViewController
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1412977">
                    <td class="code" id="p141297code7">
                        <pre class="swift" style="font-family:monospace;">
                            dynamic var loading = false
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Loading requires two things in order to work correctly: the
        <code>
            dynamic
        </code>
        keyword, and the parent class to be a subclass of
        <code>
            NSObject
        </code>
        . Bindings relies on KVO (Key Value Observing), and a Swift class that
        doesn’t inherit from NSObject wouldn’t be able to use KVO.
    </p>
    <p>
        Add the following line of code inside
        <code>
            searchClicked(:_)
        </code>
        , right before the line that executes the call to
        <code>
            getSearchResults(_:results:langString:completionHandler:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1412978">
                    <td class="code" id="p141297code8">
                        <pre class="swift" style="font-family:monospace;">
                            loading = true
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Locate the line in the same method that sets the
        <code>
            content
        </code>
        property on
        <code>
            searchResultsController
        </code>
        . Add the following code immediately before that line:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1412979">
                    <td class="code" id="p141297code9">
                        <pre class="swift" style="font-family:monospace;">
                            self.loading = false
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Next, open
        <em>
            Main.storyboard
        </em>
        and select
        <em>
            Search Progress Indicator (Bind)
        </em>
        . You’re going to bind two properties of the progress spinner:
        <code>
            hidden
        </code>
        and
        <code>
            animate
        </code>
        .
    </p>
    <p>
        First, expand the
        <em>
            Hidden
        </em>
        group, and bind to the
        <em>
            View Controller
        </em>
        .
        <em>
            Controller Key
        </em>
        should be blank, and
        <em>
            Model Key Path
        </em>
        should be
        <em>
            self.loading
        </em>
        .
    </p>
    <p>
        In this case, you want
        <code>
            hidden
        </code>
        to be false when
        <code>
            loading
        </code>
        is
        <code>
            true
        </code>
        , and vice versa. There’s an easy way to do that: use
        <code>
            NSValueTransformer
        </code>
        to flip the value of the boolean.
    </p>
    <div class="note">
        <p>
            <code>
                NSValueTransformer
            </code>
            is a class that helps you convert the form or value of data when moving
            between UI and data model.
        </p>
        <p>
            You can subclass this object in order to do much more complex conversions,
            you can learn more about NSValueTransformers in this tutorial:
            <a href="http://www.raywenderlich.com/21752/how-to-use-cocoa-bindings-and-core-data-in-a-mac-app"
            target="_blank" title="How to Use Cocoa Bindings and Core Data in a Mac App">
                How to Use Cocoa Bindings and Core Data in a Mac App
            </a>
            .
        </p>
    </div>
    <p>
        Choose
        <em>
            NSNegateBoolean
        </em>
        from the
        <em>
            Value Transformer
        </em>
        dropdown list.
    </p>
    <p>
        Bind the
        <em>
            Animate
        </em>
        value to the
        <em>
            View Controller
        </em>
        object. Set
        <em>
            Controller Key
        </em>
        as blank, and set
        <em>
            Model Key Path
        </em>
        as
        <em>
            self.loading
        </em>
        .
    </p>
    <p>
        This Boolean doesn’t need to be negated. The bindings look like this:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Binding-animating.png"
        alt="Binding animating" width="248" height="700" class="aligncenter size-full wp-image-126093"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Binding-animating.png 248w, https://koenig-media.raywenderlich.com/uploads/2016/01/Binding-animating-113x320.png 113w, https://koenig-media.raywenderlich.com/uploads/2016/01/Binding-animating-177x500.png 177w"
        sizes="(max-width: 248px) 100vw, 248px">
    </p>
    <p>
        Build and run; search for something that will return a large number of
        results so you have time to watch the spinner do its thing:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Spinner-animating-700x421.png"
        alt="Spinner animating" width="700" height="421" class="aligncenter size-large wp-image-126092"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Spinner-animating-700x421.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/Spinner-animating-480x289.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Spinner-animating-768x462.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/Spinner-animating.png 1200w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        Adding a Little More Detail
    </h2>
    <p>
        Cocoa Bindings can do more than what you’ve learned so far: you can bind
        colors and fonts to labels, enable and disable controls, and even set different
        values for labels depending on their state.
    </p>
    <p>
        Build and run your app, and you’ll notice that you see
        <em>
            No Selection
        </em>
        on all your labels before. This isn’t very nice for a user to see when
        they start your app.
    </p>
    <p>
        Find the label titled
        <em>
            Price Label (Bind)
        </em>
        , and expand
        <em>
            Value
        </em>
        . Under
        <em>
            No Selection Placeholder
        </em>
        , put
        <code>
            --
        </code>
        as shown below:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.37.50-PM.png"
        alt="Screen Shot 2016-08-30 at 12.37.50 PM" width="261" height="492" class="alignnone size-full wp-image-142725"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.37.50-PM.png 261w, https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.37.50-PM-170x320.png 170w"
        sizes="(max-width: 261px) 100vw, 261px">
    </p>
    <p>
        Build and run your app, and you’ll see that the
        <em>
            Price
        </em>
        label now has a nice placeholder value:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/08/Screen-Shot-2016-08-30-at-12.38.00-PM.png"
        alt="Screen Shot 2016-08-30 at 12.38.00 PM" width="212" height="191" class="alignnone size-large wp-image-142726">
    </p>
    <p>
        Set all labels that say
        <em>
            No Selection
        </em>
        to have a placeholder of your choice.
    </p>
    <div class="note">
        <p>
            <em>
                Note
            </em>
            : If you want the label to be blank, you can set the
            <em>
                No Selection Placeholder
            </em>
            to a
            <em>
                space
            </em>
            .
        </p>
    </div>
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
        That’s the basics of Cocoa Bindings on macOS. You’ve seen how easy it
        can be to connect data and UI.
    </p>
    <p>
        In this tutorial, you learned the following:
    </p>
    <ol>
        <li>
            How to use Interface Builder to quickly and easily bind objects to data.
        </li>
        <li>
            How to keep models and views in sync with the user’s current selection.
        </li>
        <li>
            How to use methods and bindings together to control behaviors and organize
            data.
        </li>
        <li>
            How to quickly build out UI features like progress spinners.
        </li>
    </ol>
    <p>
        You can download the final project
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/09/AppResearchBindings-Final.zip"
        target="_blank" title="">
            here
        </a>
        . Hopefully, you can save a lot of time (and code!) by adopting this technology.
    </p>
    <p>
        Each binding has a lot of little settings and options, many of which you
        didn’t explore in this tutorial. Check out
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/CocoaBindingsRef/Concepts/BindingsOptions.html"
        target="_blank" title="">
            this resource on Cocoa bindings
        </a>
        provided by Apple. It covers a lot of the details about what the options
        in the bindings windows do.
    </p>
    <p>
        I hope you enjoyed this Cocoa Bindings on macOS tutorial and picked up
        some new techniques to use to accelerate your development process. You’ve
        just opened up a whole new universe!
    </p>
</div>