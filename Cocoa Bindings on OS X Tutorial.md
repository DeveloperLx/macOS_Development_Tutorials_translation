# OS X教程：Cocoa Bindings

#### [原文地址](https://www.raywenderlich.com/124490/cocoa-bindings-os-x-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-250x250.png"
        alt="CocoaBindings-feature" width="250" height="250" class="alignright size-thumbnail wp-image-129292"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-250x250.png 250w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-320x320.png 320w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature.png 500w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2016/03/CocoaBindings-feature-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
        Cocoa bindings have a simple goal: write less code. You’ll discover as
        you work through this Cocoa Bindings on OS X tutorial that they do indeed
        live up to this objective.
    </p>
    <p>
        Cocoa bindings, aka
        <em>
            bindings
        </em>
        , fulfill a lot of responsibilities. Most importantly, they free you up
        from having to spend hours writing
        <em>
            glue code
        </em>
        — i.e. creating links between the model and the view in the controller
        when using the Model-View-Controller (MVC) pattern.
    </p>
    <p>
        If you’ve spent time in Cocoa or Cocoa Touch, you’ve no doubt written
        countless lines of boilerplate code to handle the passing of data between
        your model and UI layers. You’ve got your delegates, notifications and
        observers to let you know when a control has been altered, in addition
        to code that helps with the task of validating and transforming data.
    </p>
    <p>
        You may have wondered if there’s a better way.
    </p>
    <p>
        The great news is that there is. Cocoa bindings comprise a set of technologies
        that makes a lot of the code you’ve previously written, frankly, unnecessary.
    </p>
    <p>
        In this Cocoa Bindings on OS X tutorial, you’ll learn about how to use
        Cocoa bindings to:
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
        Once the relationship is set up within Interface Builder, any user-generated
        changes to your UI are
        <em>
            automatically pushed to your data model
        </em>
        , and any changes made to the data model are
        <em>
            automatically updated in the UI
        </em>
        .
    </p>
    <p>
        Although you won’t have to spend the next several of your hours coding,
        there’s still a fair amount of work ahead in
        <a href="http://www.raywenderlich.com/?s=Interface+Builder&amp;cof=FORID%3A10"
        target="_blank" title="Interface Builder" sl-processed="1">
            Interface Builder
        </a>
        using
        <a href="http://www.raywenderlich.com/?s=Auto+Layout&amp;cof=FORID%3A10"
        target="_blank" title="Auto Layout" sl-processed="1">
            Auto Layout
        </a>
        , so familiarity with both of these tools is a prerequisite.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/cb-rageface1-e1445168631127.png"
        sl-processed="1">
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
        In this tutorial, you’ll create an app that displays search results from
        the App Store via the iTunes API.
    </p>
    <p>
        First, download the starter project
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/AppResearchBindings-Starter-2.zip"
        title="here" sl-processed="1">
            here
        </a>
        .
    </p>
    <p>
        <em>
            Build and run
        </em>
        the project. You’ll see that there’s already a nice interface – but no
        data.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.01.30-PM-700x463.png"
        alt="Screen Shot 2016-01-31 at 6.01.30 PM" width="700" height="463" class="aligncenter size-large wp-image-125398"
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
            . This is because bindings rely on key-value coding, and hence require
            the Objective-C runtime. Adding the
            <code>
                dynamic
            </code>
            keyword guarantees that access to that property is always dynamically
            dispatched using the Objective-C runtime.
        </p>
        <p>
            Hence, you must remember that bindings rely on key-value coding and need
            to use the Objective-C runtime in order to work.
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
        First, you’re going to
        <em>
            retrieve search results via the iTunes API
        </em>
        and add it to an
        <code>
            NSArrayController.
        </code>
    </p>
    <p>
        <em>
            Open the storyboard
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
        Set Up an NSArrayController
    </h3>
    <p>
        <code>
            NSArrayController
        </code>
        is an object that manages the content of an
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
            offers much more than a simple array – including managing object selection,
            sorting and filtering. Cocoa Bindings make heavy use of this functionality.
        </p>
    </div>
    <p>
        Find an
        <code>
            NSArrayController
        </code>
        object in the
        <em>
            Object Library
        </em>
        . Drag it into the list of objects under the View Controller Scene grouping
        in the Document Outline:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/02/add-array-controller-430x500.png"
        alt="add array controller" width="430" height="500" class="aligncenter size-large wp-image-126104"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/02/add-array-controller-430x500.png 430w, https://koenig-media.raywenderlich.com/uploads/2016/02/add-array-controller-275x320.png 275w, https://koenig-media.raywenderlich.com/uploads/2016/02/add-array-controller.png 692w"
        sizes="(max-width: 430px) 100vw, 430px">
    </p>
    <p>
        Next, open the
        <em>
            Assistant Editor
        </em>
        and make sure
        <em>
            ViewController.swift
        </em>
        is the file being edited. Control-drag from the
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
        alt="Screen Shot 2016-01-31 at 6.39.36 PM" width="700" height="221" class="aligncenter size-large wp-image-125400"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.39.36-PM-700x221.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.39.36-PM-480x152.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Screen-Shot-2016-01-31-at-6.39.36-PM.png 721w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h3>
        Add Search Box and Button
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
        in the
        <em>
            Storyboard
        </em>
        to the
        <em>
            ViewController.swift
        </em>
        source. Select to create an
        <code>
            IBAction
        </code>
        , call it
        <code>
            searchClicked
        </code>
        , and then add the following code to the method:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1244901">
                    <td class="code" id="p124490code1">
                        <pre class="swift" style="font-family:monospace;">
                            @IBAction func searchClicked(sender: AnyObject!) { &nbsp; //1 if (searchTextField.stringValue
                            == "") { return } &nbsp; //2 if let resultsNumber = Int(numberResultsComboBox.stringValue)
                            { &nbsp; //3 iTunesRequestManager.getSearchResults(searchTextField.stringValue,
                            results: resultsNumber, langString: "en_us") { (results, error) -&gt; Void
                            in //4 let itunesResults = results.flatMap { $0 as? NSDictionary } .map
                            { return Result(dictionary: $0) } &nbsp; //Deal with rank here later &nbsp;
                            //5 dispatch_async(dispatch_get_main_queue()) { &nbsp; //6 self.searchResultsController.content
                            = itunesResults print(self.searchResultsController.content) } } } } &nbsp;
                            //7 override func controlTextDidEndEditing(obj: NSNotification) { //enter
                            pressed searchClicked(searchTextField) }
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
            Check the text field, if it’s blank, you don’t send that query to iTunes
            search API.
        </li>
        <li>
            Get the value in the dropdown. This is a number passed to the API that
            controls how many search results it should return. There’s a number of
            pre-configured options in the dropdown, but you can also type in other
            numbers — 200 is the maximum.
        </li>
        <li>
            Make a call to
            <code>
                getSearchResults(query:, results:, language:)
            </code>
            . This passes in the number of results from the combo box and the query
            string you typed into the text field. It returns, via a completion handler,
            an array of
            <code>
                NSDictionary
            </code>
            result objects or an
            <code>
                NSError
            </code>
            object if there’s a problem completing the query. Note that the method
            already handles parsing the JSON.
        </li>
        <li>
            Here you use some swift style array mapping to
            <i>
                a)
            </i>
            optionally cast the object to a dictionary, and
            <i>
                b)
            </i>
            pass the dictionary into an initialization method that creates a
            <code>
                Result
            </code>
            object from it. When that is done, the
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
            , you need to make sure you’re on the main thread, therefore you use
            <code>
                dispatch_async
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
            Here you set the content property of the
            <code>
                NSArrayController
            </code>
            . The array controller has a number of different methods to add or remove
            objects that it manages, but each time you run a search, you want to clear
            out whatever is there and start over with just the results of the latest
            query. For now, print the content of
            <code>
                searchResultsController
            </code>
            to the console to verify that everything is working.
        </li>
        <li>
            The last thing you’ll do is add a small method that will invoke the
            <code>
                searchClicked()
            </code>
            method when the user presses enter in addition to clicking the button.
            This just makes it easier to run a quick search.
        </li>
    </ol>
    <p>
        <em>
            Build and run now.
        </em>
        Type
        <em>
            flappy
        </em>
        into the search bar. You will see something like this show up in the console:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/02/console-700x102.png"
        alt="console" width="700" height="102" class="aligncenter size-large wp-image-126108"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/02/console-700x102.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/02/console-480x70.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/02/console-768x112.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        Your First Bindings
    </h2>
    <p>
        It’s time to get to the meat of this tutorial!
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/10/allthethings1.jpg"
        sl-processed="1">
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
        — it’s the second to last icon in the right pane, just before the
        <em>
            View Effects Inspector
        </em>
        .
    </p>
    <ol>
        <li>
            Expand the
            <em>
                Content
            </em>
            option under the
            <em>
                Table Contents
            </em>
            heading
        </li>
        <li>
            Check the box next to
            <em>
                ‘Bind to ‘
            </em>
            and make sure
            <em>
                SearchResultsController
            </em>
            is displayed in the dropdown box
        </li>
        <li>
            Make sure the
            <em>
                Controller Key
            </em>
            is set to
            <em>
                arrangedObjects
            </em>
        </li>
    </ol>
    <p>
        Like this:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/TableViewBinding-170x320.png"
        alt="TableViewBinding" width="170" height="320" class="aligncenter size-medium wp-image-126033"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/TableViewBinding-170x320.png 170w, https://koenig-media.raywenderlich.com/uploads/2016/01/TableViewBinding-265x500.png 265w, https://koenig-media.raywenderlich.com/uploads/2016/01/TableViewBinding.png 520w"
        sizes="(max-width: 170px) 100vw, 170px">
    </p>
    <p>
        <em>
            Build and run now.
        </em>
        You’ll see at most five results unless you changed the number in the dropdown.
        However, they all say ‘Table View Cell’.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/arrayboundnotitlesintable-700x463.png"
        alt="arrayboundnotitlesintable" width="700" height="463" class="aligncenter size-large wp-image-126034"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/arrayboundnotitlesintable-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/arrayboundnotitlesintable-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/arrayboundnotitlesintable-768x508.png 768w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h3>
        Binding Text Fields to Their Properties
    </h3>
    <p>
        You’re getting a bunch of duplicate hits because the text fields in the
        cells have no idea which properties on the data model they should read.
    </p>
    <p>
        Expand the objects in the table view until you find the text field named
        <em>
            Title TextField (Bind)
        </em>
        . Select this object and open the
        <em>
            Bindings Inspector
        </em>
        .
    </p>
    <ol>
        <li>
            Expand the
            <em>
                Value
            </em>
            option and bind to the
            <em>
                Table Cell View
            </em>
            object.
        </li>
        <li>
            The
            <em>
                Model Key Path
            </em>
            should be
            <em>
                objectValue.trackName
            </em>
            .
        </li>
    </ol>
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
        In other words,
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
        Repeat this process for
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
        <em>
            Build and run now.
        </em>
        Look at that – both the title and publisher show themselves.
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
        So, with a little more work you can set the rank value.
    </p>
    <p>
        Add the following code in
        <code>
            ViewController
        </code>
        under this comment:
        <code>
            //Deal with rank here later
        </code>
        .
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1244902">
                    <td class="code" id="p124490code2">
                        <pre class="swift" style="font-family:monospace;">
                            .enumerate() .map({ (index, element) -&gt; Result in element.rank = index
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
            enumerate()
        </code>
        in order to get the index and the object at the index. Then it calls
        <code>
            .map
        </code>
        to set the rank value for each object and return an array with that result.
    </p>
    <p>
        <em>
            Finally
        </em>
        , go back to the
        <em>
            Storyboard
        </em>
        , select
        <code>
            Rank TextField (Bind)
        </code>
        , open the
        <em>
            Bindings Inspector
        </em>
        and do the following:
    </p>
    <ol>
        <li>
            In the
            <em>
                Value
            </em>
            section, bind to the
            <code>
                Table Cell View
            </code>
        </li>
        <li>
            Make sure
            <em>
                Controller Key
            </em>
            is empty
        </li>
        <li>
            Set
            <em>
                Model Key Path
            </em>
            to
            <code>
                objectValue.rank
            </code>
        </li>
    </ol>
    <p>
        <em>
            Build and run
        </em>
        now.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/ranktitlepublisher-700x463.png"
        alt="ranktitlepublisher" width="700" height="463" class="aligncenter size-large wp-image-126072"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/ranktitlepublisher-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/ranktitlepublisher-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/ranktitlepublisher-768x508.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/ranktitlepublisher.png 1133w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        Binding a Table View’s Selection
    </h2>
    <p>
        Now it’s time to bind the
        <code>
            Result
        </code>
        object in the table that the user selects to the rest of the UI. Binding
        to a selection in a table involves two steps:
    </p>
    <ol>
        <li>
            You first bind the
            <code>
                NSArrayController
            </code>
            to the table selection
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
        Select the
        <em>
            Search Results Table View (Bind)
        </em>
        and open the
        <em>
            Bindings Inspector
        </em>
        to do the following steps:
    </p>
    <ol>
        <li>
            Expand the
            <em>
                Selection Indexes
            </em>
            option in the
            <em>
                Table Content
            </em>
            section
        </li>
        <li>
            Check
            <em>
                Bind to
            </em>
            the
            <em>
                SearchResultsController
            </em>
            object
        </li>
        <li>
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
            property that contains set of indexes that the user has selected in the
            table. Note that in this case, I’ve set the table view to only allow a
            single selection, but you could work with more than one selection if needed
            — think about the finder window and how you can select multiple files at
            a time.
        </li>
    </ol>
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
        .
    </p>
    <ol>
        <li>
            Bind to the
            <em>
                SearchResultsController
            </em>
        </li>
        <li>
            <em>
                Controller Key
            </em>
            should be
            <em>
                selection
            </em>
        </li>
        <li>
            <em>
                Model Key Path
            </em>
            should be
            <em>
                trackName
            </em>
        </li>
    </ol>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/mainTrackName.png"
        alt="mainTrackName" width="247" height="193" class="aligncenter size-full wp-image-126075">
    </p>
    <p>
        <em>
            Build and run.
        </em>
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Main-Title-700x463.png"
        alt="Main Title" width="700" height="463" class="aligncenter size-large wp-image-126076"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Main-Title-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/Main-Title-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Main-Title-768x508.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/Main-Title.png 1133w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        Formatting Bound Data
    </h2>
    <p>
        Now you know how easy it is to get data from your model into your UI,
        but what if the data needs to be formatted in some way, such as currency
        or a date?
    </p>
    <p>
        Luckily, there’s a built-in set of objects that make it easy to change
        the way a specific piece of data is displayed in a label.
    </p>
    <h3>
        Format as Price
    </h3>
    <p>
        Find the label titled
        <em>
            Price Label (Bind)
        </em>
        , setting it up like this:
    </p>
    <ol>
        <li>
            Bind it to the
            <em>
                SearchResultsController
            </em>
            object
        </li>
        <li>
            Make sure
            <em>
                Controller Key
            </em>
            is
            <em>
                selection
            </em>
        </li>
        <li>
            Set
            <em>
                Model Key Path
            </em>
            to
            <em>
                price
            </em>
        </li>
        <li>
            Next, find a
            <em>
                Number Formatter
            </em>
            in the
            <em>
                Object library
            </em>
            . Drag it over to
            <em>
                NSTextFieldCell
            </em>
            under the
            <code>
                Price
            </code>
            label.
        </li>
        <li>
            Select the
            <em>
                Number Formatter
            </em>
            and open the
            <em>
                Attributes Inspector
            </em>
            change the
            <em>
                Style
            </em>
            to
            <em>
                Currency
            </em>
            .
        </li>
    </ol>
    <p>
        Like this:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Number-Formatter-700x403.png"
        alt="Number Formatter" width="700" height="403" class="aligncenter size-large wp-image-126077"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Number-Formatter-700x403.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/Number-Formatter-480x276.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Number-Formatter-768x442.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/Number-Formatter.png 1390w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        <em>
            Build and run.
        </em>
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
            : Number formatters are very powerful – in addition to currencies, you
            can also control how many digits follow a decimal point, percentages, or
            have the number spelled out in words.
        </p>
        <p>
            There are also a bunch of other kinds of formatters. There are formatter
            objects for dates, for byte counts and several other less common ones.
        </p>
    </div>
    <h3>
        Format as Bytes
    </h3>
    <p>
        You’ll be using a
        <em>
            Byte Count Formatter
        </em>
        next.
    </p>
    <p>
        Find
        <em>
            File Size Label (Bind)
        </em>
        and set it up like so:
    </p>
    <ol>
        <li>
            Bind it to the
            <em>
                SearchResultsController
            </em>
        </li>
        <li>
            <em>
                Controller Key
            </em>
            is
            <em>
                selection
            </em>
        </li>
        <li>
            <em>
                Model Key Path
            </em>
            is
            <em>
                fileSizeInBytes
            </em>
        </li>
        <li>
            Then, find a
            <em>
                Byte Count Formatter
            </em>
            and attach it to the
            <em>
                NSTextFieldCell
            </em>
            . There’s no need to configure anything here, the default settings on
            a byte formatter will work.
        </li>
    </ol>
    <p>
        Like this:
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-formatter.png"
        alt="byte count formatter" width="349" height="124" class="aligncenter size-full wp-image-126083">
    </p>
    <p>
        <em>
            Build and run
        </em>
        now.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-final-700x463.png"
        alt="byte count final" width="700" height="463" class="aligncenter size-large wp-image-126084"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-final-700x463.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-final-480x317.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-final-768x508.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/byte-count-final.png 1133w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        You now know everything you need to know to bind the remaining labels,
        so here’s a short list of the keys you need to bind:
    </p>
    <p>
        All these labels should be bound to the
        <em>
            SearchResultsController
        </em>
        and the
        <em>
            selection
        </em>
        controller key.
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
        </li>
        <li>
            Add a
            <em>
                Date Formatter
            </em>
            , default settings are fine
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
        </li>
    </ul>
    <p>
        For more precision in your UI, you can also bind the
        <em>
            Description Text View (Bind)
        </em>
        , the
        <em>
            Attributed String
        </em>
        binding to the
        <em>
            itemDescription
        </em>
        Model Key Path. Make sure you bind the
        <code>
            NSTextField
        </code>
        , which is several levels down in the hierarchy, not the
        <code>
            NSScrollView
        </code>
        which is at the top.
    </p>
    <p>
        <em>
            Build and run
        </em>
        . You should see now that most of the UI is populated.
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
        . This is a little trickier because what you get from the JSON payload
        is not the image, but a URL location for the image.
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
        Download the Right Icon at the Right Time
    </h3>
    <p>
        You don’t want to download all the icons at once — just the one for the
        current selection in the table. You therefore need to invoke the method
        whenever the selection changes.
    </p>
    <p>
        Add the following code to
        <em>
            ViewController
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1244903">
                    <td class="code" id="p124490code3">
                        <pre class="swift" style="font-family:monospace;">
                            //1 func tableViewSelectionDidChange(notification: NSNotification) { //2
                            if let result = searchResultsController.selectedObjects.first as? Result
                            { //3 result.loadIcon() } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <ol>
        <li>
            <code>
                tableViewSelectionDidChange()
            </code>
            gets fired every time the user selects a different row in the table
        </li>
        <li>
            The array controller has a property,
            <code>
                selectedObjects
            </code>
            . It returns an array that contains all the objects for the indexes of
            the rows selected in the table. In your case, the table will only allow
            a single selection, so this array always contains a single object. You
            store the object in the
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
            property when the image is downloaded on the main thread.
        </li>
    </ol>
    <h3>
        Binding the Image View
    </h3>
    <p>
        Now that your code is in place, you’re ready to bind the image view. Head
        back to
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
        and set things up:
    </p>
    <ol>
        <li>
            Bind to the
            <em>
                SearchResultsController
            </em>
        </li>
        <li>
            Set
            <em>
                Controller Key
            </em>
            to
            <em>
                selection
            </em>
        </li>
        <li>
            Set
            <em>
                Model Key Path
            </em>
            to
            <em>
                artworkImage
            </em>
        </li>
    </ol>
    <p>
        You may notice that there is a
        <em>
            Value Path
        </em>
        and a
        <em>
            Value URL
        </em>
        section. Both of these bindings are intended to be used only with local
        resources. It is possible to connect them to a network resource, but if
        you do, the UI thread will be blocked until the resource is downloaded.
    </p>
    <p>
        <em>
            Build and run
        </em>
        , search for
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
    <h3>
        Populate the Collection View
    </h3>
    <p>
        The collection view beneath the description text view is currently looking
        a little bare — time to populate that with some screenshots. First you’ll
        bind the collection view to the
        <code>
            screenShots
        </code>
        property before ensuring that the
        <code>
            screenShots
        </code>
        array is correctly populated.
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
        group. Set it up thusly:
    </p>
    <ol>
        <li>
            Bind to the
            <em>
                SearchResultsController
            </em>
        </li>
        <li>
            <em>
                Controller Key
            </em>
            is
            <em>
                selection
            </em>
        </li>
        <li>
            <em>
                Model Key Path
            </em>
            is
            <em>
                screenShots
            </em>
        </li>
    </ol>
    <p>
        The
        <code>
            screenShots
        </code>
        array starts out empty. There’s a method named
        <code>
            loadScreenShots()
        </code>
        that is similar to the method that loads the icon. It’ll download the
        image files and populate the
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
        Add this line in
        <code>
            ViewController.swift
        </code>
        , in
        <code>
            tableViewSelectionDidChange()
        </code>
        right after the
        <code>
            result.loadIcon()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1244904">
                    <td class="code" id="p124490code4">
                        <pre class="swift" style="font-family:monospace;">
                            result.loadScreenShots()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This will populate the screenshot images and create the right number of
        views. The next thing you need to do is set the right collection view item
        prototype.
    </p>
    <p>
        Normally when you drag a collection view into a storyboard, you automatically
        create a collection view item and a segue. However, this feature is buggy
        in the latest Xcode and at the time of writing, it’s not working.
    </p>
    <p>
        Although the collection view item scene is present in the storyboard,
        it’s not connected to the collection view. Therefore you’ll have to create
        this connection in code.
    </p>
    <p>
        Add the following code to the end of
        <code>
            viewDidLoad
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
                <tr id="p1244905">
                    <td class="code" id="p124490code5">
                        <pre class="swift" style="font-family:monospace;">
                            let itemPrototype = self.storyboard?.instantiateControllerWithIdentifier("collectionViewItem")
                            as! NSCollectionViewItem collectionView.itemPrototype = itemPrototype
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now that the collection view knows how to create each item (via the prototype)
        you need to provide the content for each item, via a binding.
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
        . You’ll find this floating next to the main view controller. Here are
        the settings for this one:
    </p>
    <ol>
        <li>
            Bind the
            <em>
                Value
            </em>
            option to the
            <em>
                Collection View Item
            </em>
            object.
        </li>
        <li>
            The controller key should be blank
        </li>
        <li>
            <em>
                Model Key Path
            </em>
            should be
            <em>
                representedObject
            </em>
        </li>
    </ol>
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
        <em>
            Build and run
        </em>
        now.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/screenshots-700x421.png"
        alt="screenshots" width="700" height="421" class="aligncenter size-large wp-image-126089"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/screenshots-700x421.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/screenshots-480x289.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/screenshots-768x462.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/screenshots.png 1200w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        You can now see the screenshots appearing below the description text —
        great work! Just a few more features of Cocoa Bindings to cover before
        wrapping up.
    </p>
    <h2>
        Binding Other Properties
    </h2>
    <p>
        Thus far you’ve seen how you can bind model objects to labels and images
        for display to the user. However, you can also bind attributes such as
        fonts, colors, text styles and visibility to data in your model. This allows
        you to easily control the appearance of your UI directly through the model
        layer.
    </p>
    <h3>
        Set Up a Progress Spinner
    </h3>
    <p>
        Users don’t like to stare at static screens when something is loading
        — they tend to think the worst if there’s nothing to tell them something’s
        happening behind the scenes.
    </p>
    <p>
        Instead of leaving a static screen, you can show a spinner to the user,
        indicating that the app is busy working. An easy way to do this is to bind
        a progress spinner to a new property in the
        <code>
            ViewController
        </code>
        , so add the following property to
        <code>
            ViewController
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1244906">
                    <td class="code" id="p124490code6">
                        <pre class="swift" style="font-family:monospace;">
                            dynamic var loading = false
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Loading requires two things in order to work correctly. The
        <code>
            dynamic
        </code>
        keyword and that the parent class is a subclass of
        <code>
            NSObject
        </code>
        . Bindings relies on KVO (Key Value Observing). A swift class that doesn’t
        inherit from NSObject wouldn’t be able to use KVO.
    </p>
    <p>
        Add the following line of code in the function
        <code>
            searchClicked()
        </code>
        right before the line that executes the call to
        <code>
            getSearchResults()
        </code>
        .
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1244907">
                    <td class="code" id="p124490code7">
                        <pre class="swift" style="font-family:monospace;">
                            loading = true
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Locate the line that sets the
        <code>
            content
        </code>
        property on
        <code>
            searchResultsController
        </code>
        (
        <code>
            self.searchResultsController.content = itunesResults
        </code>
        ) and add the following immediately before it:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1244908">
                    <td class="code" id="p124490code8">
                        <pre class="swift" style="font-family:monospace;">
                            self.loading = false
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Next, select
        <em>
            Search Progress Indicator (Bind)
        </em>
        in
        <em>
            Main.storyboard
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
        group, and set it up like so:
    </p>
    <ol>
        <li>
            Bind to the
            <em>
                View Controller
            </em>
        </li>
        <li>
            <em>
                Controller Key
            </em>
            should be blank
        </li>
        <li>
            <em>
                Model Key Path
            </em>
            should be
            <em>
                self.loading
            </em>
        </li>
    </ol>
    <p>
        In this case you need to do one more thing, when loading is true, you
        actually want
        <code>
            hidden
        </code>
        to be false and vice versa. Luckily, there’s an easy way to do that —
        using
        <code>
            NSValueTransformer
        </code>
        to flip the value of the boolean.
    </p>
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
            target="_blank" title="How to Use Cocoa Bindings and Core Data in a Mac App"
            sl-processed="1">
                How to Use Cocoa Bindings and Core Data in a Mac App
            </a>
            .
        </p>
    </div>
    <p>
        Next, bind to the
        <em>
            Animate
        </em>
        value like this:
    </p>
    <ol>
        <li>
            Bind it to the
            <em>
                View Controller
            </em>
            object
        </li>
        <li>
            <em>
                Controller Key
            </em>
            should be blank.
        </li>
        <li>
            <em>
                Model Key Path
            </em>
            is
            <em>
                self.loading
            </em>
        </li>
    </ol>
    <p>
        This boolean doesn’t need to be negated.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Binding-animating.png"
        alt="Binding animating" width="248" height="700" class="aligncenter size-full wp-image-126093"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Binding-animating.png 248w, https://koenig-media.raywenderlich.com/uploads/2016/01/Binding-animating-113x320.png 113w, https://koenig-media.raywenderlich.com/uploads/2016/01/Binding-animating-177x500.png 177w"
        sizes="(max-width: 248px) 100vw, 248px">
    </p>
    <p>
        <em>
            Build and run
        </em>
        now. You might want to use a larger number of results so that there’s
        time to watch the spinner do its spin thing while results are retrieved.
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/Spinner-animating-700x421.png"
        alt="Spinner animating" width="700" height="421" class="aligncenter size-large wp-image-126092"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/Spinner-animating-700x421.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/Spinner-animating-480x289.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/Spinner-animating-768x462.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/Spinner-animating.png 1200w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        Adding a Little More Spice
    </h2>
    <p>
        Color is the spice of design, and right now things are looking a little
        drab. You won’t be surprised to learn that you can set color with Cocoa
        bindings!
    </p>
    <p>
        In this scenario, you’re dealing with apps that have a larger number of
        reviews, making them rank higher in the search results. More reviews tends
        to be a good sign, and users enjoy having a visual indicator of such a
        thing when they have to scroll through a long list and make split-second
        decisions.
    </p>
    <p>
        So, you’ll build out that visual cue.
    </p>
    <h3>
        Create a Ranking Method
    </h3>
    <p>
        First, you need to add a method that calculates the color of each result
        based on the number of reviews.
    </p>
    <p>
        Add this code to
        <code>
            ViewController
        </code>
        inside
        <em>
            ViewController.swift
        </em>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1244909">
                    <td class="code" id="p124490code9">
                        <pre class="swift" style="font-family:monospace;">
                            func setColorsOnData() { &nbsp; //1 let allResults = searchResultsController.arrangedObjects
                            &nbsp; //2 let sortDescriptor = NSSortDescriptor(key: "userRatingCount",
                            ascending: false) let sortedResults = allResults.sortedArrayUsingDescriptors([sortDescriptor])
                            as NSArray &nbsp; //3 for index in 0..&lt;sortedResults.count { &nbsp;
                            //4 let red = CGFloat(Float(index) / Float(sortedResults.count)) let green
                            = CGFloat(1.0 - (Float(index) / Float(sortedResults.count))) let color
                            = NSColor(calibratedRed: red, green: green, blue: 0.0, alpha: 1.0) &nbsp;
                            //5 if let result = sortedResults.objectAtIndex(index) as? Result { result.cellColor
                            = color } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s what you’re cooking up in there:
    </p>
    <ol>
        <li>
            Get the array from the array controller
        </li>
        <li>
            Create a sort descriptor that is based on the ‘userRatingCount’ key. It’s
            descending so that the largest number of reviews is first in the list.
            You then create a
            <code>
                sortedResults
            </code>
            array that contains the sorted list
        </li>
        <li>
            Iterate through the results
        </li>
        <li>
            Create a color; the objects at the beginning of the set will be the most
            green and the values at the end will be the most red
        </li>
        <li>
            Finally, you set the
            <code>
                cellColor
            </code>
        </li>
    </ol>
    <p>
        Next, you need to call that new method. Add this line to
        <code>
            searchClicked()
        </code>
        in
        <code>
            ViewController.swift
        </code>
        right after this line
        <code>
            self.arrayController.content = itunesResults
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p12449010">
                    <td class="code" id="p124490code10">
                        <pre class="swift" style="font-family:monospace;">
                            self.setColorsOnData()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <h3>
        Bind Font Color
    </h3>
    <p>
        Now, bind the font color of the rank column to that value.
    </p>
    <p>
        Select the
        <em>
            Rank TextField (Bind)
        </em>
        object and set it up like this:
    </p>
    <ol>
        <li>
            Bind to the
            <em>
                Text Color
            </em>
            value, the
            <em>
                Table Cell View
            </em>
            object.
        </li>
        <li>
            <em>
                Controller Key
            </em>
            should be blank
        </li>
        <li>
            Set
            <em>
                Model Key Path
            </em>
            to
            <em>
                objectValue.cellColor
            </em>
        </li>
    </ol>
    <p>
        <em>
            Build and run.
        </em>
    </p>
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/01/cell-color-700x421.png"
        alt="cell color" width="700" height="421" class="aligncenter size-large wp-image-126095"
        srcset="https://koenig-media.raywenderlich.com/uploads/2016/01/cell-color-700x421.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/01/cell-color-480x289.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/01/cell-color-768x462.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/01/cell-color.png 1200w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <p>
        You can now see that the rank numbers are color-coded, according to the
        number of reviews each app has.
    </p>
    <h2>
        Where to Go From Here
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
        That’s the gist of Cocoa Bindings, and you can see just how much easier
        it makes life when you need to connect data and UI. You learned:
    </p>
    <ol>
        <li>
            How to use Interface Builder to quickly and easily bind objects to data
        </li>
        <li>
            How to make keep models and views in sync with the user’s current selection
        </li>
        <li>
            How to use methods and bindings together to control behaviors and organize
            data
        </li>
        <li>
            How to quickly build out UI features like progress spinners
        </li>
    </ol>
    <p>
        You can download the final project
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/03/AppResearchBindings.zip"
        target="_blank" title="" sl-processed="1">
            here
        </a>
        . Hopefully, you can see how much time and code you can save by adopting
        this technology.
    </p>
    <p>
        Each binding has a lot of little settings and options, many of which we
        didn’t explore. One specific thing to take a look at is
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/CocoaBindingsRef/Concepts/BindingsOptions.html"
        target="_blank" title="" sl-processed="1">
            this resource
        </a>
        provided by Apple. It will cover a lot of the details about what the options
        in the bindings windows do.
    </p>
    <p>
        I hope you enjoyed this Cocoa Bindings on OS X tutorial and picked up
        some new techniques to use to accelerate your development process. You’ve
        just opened up a whole new universe! Let’s talk about it in the forums
        — I look forward to your questions, comments and findings.
    </p>
</div>