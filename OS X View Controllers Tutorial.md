# OS X View Controllers教程

#### [原文地址](https://www.raywenderlich.com/112811/os-x-view-controllers-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <div id="attachment_119460" style="width: 260px" class="wp-caption alignright">
        <img class="wp-image-119460 size-full" src="https://koenig-media.raywenderlich.com/uploads/2015/10/featured_image3.png"
        alt="" width="250" height="250" srcset="https://koenig-media.raywenderlich.com/uploads/2015/10/featured_image3.png 250w, https://koenig-media.raywenderlich.com/uploads/2015/10/featured_image3-32x32.png 32w, https://koenig-media.raywenderlich.com/uploads/2015/10/featured_image3-64x64.png 64w, https://koenig-media.raywenderlich.com/uploads/2015/10/featured_image3-96x96.png 96w, https://koenig-media.raywenderlich.com/uploads/2015/10/featured_image3-128x128.png 128w"
        sizes="(max-width: 250px) 100vw, 250px">
        <p class="wp-caption-text">
            Learn how to control the UI with this OS X View Controllers Tutorial!
        </p>
    </div>
    <p>
        When writing any code, it’s important to get clear separation of concerns
        — functionality should be split out into appropriate smaller classes. This
        helps keep code maintainable and easy to understand. Apple has designed
        the frameworks available on OS X around the Model-View-Controller design
        pattern, and as such has provided various controller objects&nbsp;that
        are responsible for managing the UI.
    </p>
    <p>
        View controllers are responsible for hooking up the model layer to the
        view layer, and have an incredibly important role in the architecture of
        your OS X app.
    </p>
    <p>
        In this OS X view controllers tutorial you’ll discover the wide range
        of functionality that is baked into vanilla view controllers, along with
        learning how you can create your own view controller subclasses to build
        up your app in an easy-to-understand manner. You’ll see how the life cycle
        methods allow you to hook into important events for the UI of your app,
        together with how view controllers compare with window controllers.
    </p>
    <p>
        To follow this tutorial you’ll need the most recent version of OS X and
        Xcode installed on your mac. There’s no starter project — you’ll build
        a great app from scratch! You might like to read Gabriel Miro’s excellent
        <a href="http://www.raywenderlich.com/111947/windows-and-window-controllers-in-os-x-tutorial"
        sl-processed="1">
            tutorial on windows and window controllers
        </a>
        before embarking upon this view controllers tutorial, but it’s not a requirement.
    </p>
    <p>
        Enough introduction — let’s kick off with some theory!
    </p>
    <h2>
        Introducing View Controllers
    </h2>
    <p>
        A view controller is responsible for managing a view and its subviews.
        In
        <em>
            OS X
        </em>
        , view controllers are implemented as subclasses of
        <code>
            NSViewController
        </code>
        .
    </p>
    <p>
        View controllers have been around for a while (Apple introduced them with
        OS X 10.5), but before OS X 10.10 they weren’t part of the responder chain.
        That means, for example, that if you had a button on a view controller’s
        view, the controller would not receive its events. After OS X 10.10, however,
        view controllers became very useful as building blocks for more complex
        user interfaces.
    </p>
    <p>
        View controllers allow you to split the content of your window into&nbsp;logical
        units. The view controllers take care of those smaller units, while the
        window controller handles&nbsp;window-specific tasks like resizing or closing
        the window. This makes your code way easier to organize.
    </p>
    <p>
        Another benefit is that view controllers are easy to reuse in other applications.
        If a File Browser with a hierarchical view on the left is controlled by
        a single view controller, you can use it in another application that needs
        a similar view. That’s time and energy saved, which you can now devote
        to drinking beer!
    </p>
    <h3>
        Window Controller or View Controller?
    </h3>
    <p>
        You may be wondering when to use only a window controller, and when to
        implement view controllers.
    </p>
    <p>
        Prior to&nbsp;OS X 10.10 Yosemite,
        <code>
            NSViewController
        </code>
        &nbsp;was not a very useful class. It did not provide any of the view
        controller functionality you could expect — for instance, that found in&nbsp;
        <code>
            UIViewController
        </code>
        .
    </p>
    <p>
        With the changes introduced since, like the view life cycle and the inclusion
        of the view controllers in the responder chain to receive events from its
        view, Apple is promoting the Model View Controller (MVC) pattern in the
        same way it’s currently doing with iOS Development. You should use view
        controllers to handle all the functionality of your views and subviews
        and the user interaction. Use window controllers to implement the functionality
        associated to the application windows, like setting up the root view controller,
        resizing, repositioning, setting the title, etc.
    </p>
    <p>
        This approach will help in building a complex user interface by dividing
        the different parts of the UI into several view controllers and using them
        like building blocks to form the complete user interface.
    </p>
    <h2>
        View Controllers in Action
    </h2>
    <p>
        In this tutorial, you’ll write an application called
        <em>
            RWStore
        </em>
        that lets you select different books from
        <a href="http://www.raywenderlich.com/store" sl-processed="1">
            raywenderlich.com store.
        </a>
        Let’s get started!
    </p>
    <p>
        Open Xcode and choose to create a new Xcode project, and select
        <em>
            OS X \ Application \ Cocoa Application
        </em>
        from the templates menu. Click
        <em>
            Next
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/SelectTemplate.png"
        sl-processed="1">
            <img class="size-medium wp-image-112816 aligncenter" src="https://koenig-media.raywenderlich.com/uploads/2015/08/SelectTemplate-450x320.png"
            alt="SelectTemplate" width="450" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/SelectTemplate-450x320.png 450w, https://koenig-media.raywenderlich.com/uploads/2015/08/SelectTemplate-700x498.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/SelectTemplate.png 731w"
            sizes="(max-width: 450px) 100vw, 450px">
        </a>
    </p>
    <p>
        Name your project
        <em>
            RWStore
        </em>
        . On the options screen, make sure that
        <em>
            Swift
        </em>
        is selected as Language and the
        <em>
            Use Storyboards
        </em>
        checkbox is checked. You don’t need Unit and UI Tests, so uncheck the
        corresponding checkboxes. Click
        <em>
            Next
        </em>
        and save your project.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/TemplateSettings.png"
        sl-processed="1">
            <img class="size-medium wp-image-112817 aligncenter" src="https://koenig-media.raywenderlich.com/uploads/2015/08/TemplateSettings-453x320.png"
            alt="TemplateSettings" width="453" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/TemplateSettings-453x320.png 453w, https://koenig-media.raywenderlich.com/uploads/2015/08/TemplateSettings-700x495.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/TemplateSettings.png 733w"
            sizes="(max-width: 453px) 100vw, 453px">
        </a>
    </p>
    <p>
        Download the project
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/resources.zip"
        sl-processed="1">
            resources
        </a>
        . The zip file contains images for the books and a
        <em>
            Products.plist
        </em>
        file containing an array of dictionaries with the information for a product,
        like the name, description, and price. You will also find a source code
        file named
        <em>
            Product.swift
        </em>
        . This file contains the
        <em>
            Product
        </em>
        class, that reads the product information from the plist file. You’re
        going to add these to RWStore.
    </p>
    <p>
        Select the
        <em>
            Assets.xcassets
        </em>
        folder in the
        <em>
            Project Navigator
        </em>
        and drop the downloaded images into the column containing the app icon.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/AddAssets.png"
        sl-processed="1">
            <img class="aligncenter wp-image-112818 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/08/AddAssets-e1445809411833-700x277.png"
            alt="AddAssets" width="700" height="277" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/AddAssets-e1445809411833-700x277.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/AddAssets-e1445809411833-480x190.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/AddAssets-e1445809411833.png 1058w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Drag and drop
        <em>
            Products.plist
        </em>
        and
        <em>
            Product.swift
        </em>
        into the
        <em>
            Project Navigator
        </em>
        on the left. Make sure that
        <em>
            Copy items if needed
        </em>
        is checked.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/AddProductsPlist.png"
        sl-processed="1">
            <img class="aligncenter wp-image-112820 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/08/AddProductsPlist-e1445809498824-700x322.png"
            alt="AddProductsPlist" width="700" height="322" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/AddProductsPlist-e1445809498824-700x322.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/AddProductsPlist-e1445809498824-480x220.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/AddProductsPlist-e1445809498824.png 1069w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Build and run the app. You should see the main window of your application.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/window-empty.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113611" src="https://koenig-media.raywenderlich.com/uploads/2015/09/window-empty.png"
            alt="window-empty" width="480" height="292">
        </a>
    </p>
    <p>
        It’s empty now, but don’t worry — this is just the starting point.
    </p>
    <h2>
        Creating the User Interface
    </h2>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        , select
        <em>
            View Controller Scene
        </em>
        , and drag a
        <em>
            pop-up button
        </em>
        into the view. You’ll use this
        <em>
            pop-up button
        </em>
        to display the list of products.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/add-popup.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113645" src="https://koenig-media.raywenderlich.com/uploads/2015/09/add-popup-700x264.png"
            alt="add-popup" width="700" height="264" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/add-popup-700x264.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/add-popup-480x181.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/add-popup.png 894w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Set its position using auto layout. The pop-up button should occupy the
        full width of the view and stay pinned to the top, so select the pop-up
        button and click the
        <em>
            Pin
        </em>
        button located in the bottom bar.
    </p>
    <p>
        In the pop-up that appears, select the trailing constraint and set its
        value to
        <em>
            Use Standard Value
        </em>
        . Repeat for the top and leading constraints.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/AddPopupButton.png"
        sl-processed="1">
            <img class="size-medium wp-image-112823 aligncenter" src="https://koenig-media.raywenderlich.com/uploads/2015/08/AddPopupButton-480x235.png"
            alt="AddPopupButton" width="480" height="235" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/AddPopupButton-480x235.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/AddPopupButton-700x343.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/08/AddPopupButton.png 785w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        To complete&nbsp;the UI, add a view to show the product details. Select
        a
        <em>
            container view
        </em>
        and drag it below the pop-up button.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/add-container.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113612" src="https://koenig-media.raywenderlich.com/uploads/2015/09/add-container-700x271.png"
            alt="add-container" width="700" height="271" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/add-container-700x271.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/add-container-480x186.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/add-container.png 872w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        A
        <em>
            container view
        </em>
        is a placeholder for another view that is not available in Interface Builder
        or is provided by another View Controller.
    </p>
    <p>
        Now we’ll set up the auto layout constraints for this view. Select the
        container view and click on the
        <em>
            Pin
        </em>
        button. Add
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
        , and
        <em>
            leading
        </em>
        constraints with a value of
        <em>
            0
        </em>
        . Click the
        <em>
            Add 4 constraints
        </em>
        button.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/container-constraints.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113613" src="https://koenig-media.raywenderlich.com/uploads/2015/09/container-constraints.png"
            alt="container-constraints" width="647" height="454" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/container-constraints.png 647w, https://koenig-media.raywenderlich.com/uploads/2015/09/container-constraints-456x320.png 456w"
            sizes="(max-width: 647px) 100vw, 647px">
        </a>
    </p>
    <p>
        Select the view of your view controller and click the
        <em>
            Resolve Auto Layout Issues
        </em>
        button to the right of the
        <em>
            Pin
        </em>
        button. Select
        <em>
            All Views in Controller/Update Frames
        </em>
        . Your view should look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/FinishedVC.png"
        sl-processed="1">
            <img class="size-medium wp-image-112828 aligncenter" src="https://koenig-media.raywenderlich.com/uploads/2015/08/FinishedVC-480x302.png"
            alt="FinishedVC" width="480" height="302" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/FinishedVC-480x302.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/FinishedVC.png 485w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Now you’ll&nbsp;create an action that will be called when the button selection
        changes. Open the
        <em>
            Assistant Editor
        </em>
        (you can also use the keyboard shortcut
        <em>
            [alt] + [cmd] + [Enter]
        </em>
        ) and make sure that
        <em>
            ViewController.swift
        </em>
        is open.
        <em>
            Control-drag
        </em>
        from the
        <em>
            pop-up button
        </em>
        into
        <em>
            ViewController.swift
        </em>
        and add an Action Connection. In the pop-up view, make sure the connection
        is an
        <em>
            Action
        </em>
        , the name is
        <em>
            valueChanged
        </em>
        , and the type is
        <em>
            NSPopUpButton
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/popup.action-drag.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113648" src="https://koenig-media.raywenderlich.com/uploads/2015/09/popup.action-drag-700x394.png"
            alt="popup.action-drag" width="700" height="394" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/popup.action-drag-700x394.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/popup.action-drag-480x270.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/popup.action-drag-266x151.png 266w, https://koenig-media.raywenderlich.com/uploads/2015/09/popup.action-drag.png 923w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/popup.action-nuevo.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113614" src="https://koenig-media.raywenderlich.com/uploads/2015/09/popup.action-nuevo.png"
            alt="popup.action-nuevo" width="603" height="403" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/popup.action-nuevo.png 603w, https://koenig-media.raywenderlich.com/uploads/2015/09/popup.action-nuevo-480x320.png 480w"
            sizes="(max-width: 603px) 100vw, 603px">
        </a>
    </p>
    <p>
        On the canvas, the view controller is connected to the container view
        with an
        <i>
            embed segue
        </i>
        . Your app will use a custom view controller, so you can delete the auto-generated
        one: select the view controller associated with the container view and
        press
        <em>
            delete
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/delete-viewcontroller.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113615" src="https://koenig-media.raywenderlich.com/uploads/2015/09/delete-viewcontroller-700x459.png"
            alt="delete-viewcontroller" width="700" height="459" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/delete-viewcontroller-700x459.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/delete-viewcontroller-480x314.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/delete-viewcontroller.png 983w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <h2>
        Tab View Controllers
    </h2>
    <p>
        Now we’ll add the view controller used to display the product info: a
        <em>
            Tab View Controller
        </em>
        . A
        <em>
            Tab View Controller
        </em>
        is a view controller subclass (
        <code>
            NSTabViewController
        </code>
        ); its view contains a tab view with two or more items and a container
        view. Behind every tab is another view controller whose content&nbsp;is
        used to fill the container view. Every time a new tab is selected, the
        Tab View Controller replaces the content with the view of the associated
        view controller.
    </p>
    <p>
        Select a
        <em>
            Tab View Controller
        </em>
        and drag it on on the canvas.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/drag-tabcontroller.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113616" src="https://koenig-media.raywenderlich.com/uploads/2015/09/drag-tabcontroller-700x385.png"
            alt="drag-tabcontroller" width="700" height="385" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/drag-tabcontroller-700x385.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/drag-tabcontroller-480x264.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/drag-tabcontroller.png 1050w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        The tab controller is now on the storyboard, but it’s not used yet. Connect
        it to the container view using an embed segue;
        <em>
            control-drag
        </em>
        from the container view to the Tab View Controller.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/control-drag-tabview.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113617" src="https://koenig-media.raywenderlich.com/uploads/2015/09/control-drag-tabview-700x344.png"
            alt="control-drag-tabview" width="700" height="344" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/control-drag-tabview-700x344.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/control-drag-tabview-480x236.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/control-drag-tabview.png 772w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Select
        <em>
            embed
        </em>
        in the menu that pops up.
        <br>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/Embed.png"
        sl-processed="1">
            <img class="size-full wp-image-112831 aligncenter" src="https://koenig-media.raywenderlich.com/uploads/2015/08/Embed.png"
            alt="Embed" width="130" height="33" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/Embed.png 130w, https://koenig-media.raywenderlich.com/uploads/2015/08/Embed-128x33.png 128w"
            sizes="(max-width: 130px) 100vw, 130px">
        </a>
    </p>
    <p>
        With this change, when the app runs the area of the container view is
        replaced with the view of the Tab View Controller. Double-click on the
        left tab of the Tab View and rename it
        <em>
            Overview
        </em>
        . Repeat to rename the right tab
        <em>
            Details
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/rename-tabs.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113618" src="https://koenig-media.raywenderlich.com/uploads/2015/09/rename-tabs.png"
            alt="rename-tabs" width="476" height="360" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/rename-tabs.png 476w, https://koenig-media.raywenderlich.com/uploads/2015/09/rename-tabs-423x320.png 423w"
            sizes="(max-width: 476px) 100vw, 476px">
        </a>
    </p>
    <p>
        Build and run the app.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/tabview-empty.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113620" src="https://koenig-media.raywenderlich.com/uploads/2015/09/tabview-empty.png"
            alt="tabview-empty" width="480" height="292">
        </a>
    </p>
    <p>
        Now the tab view controller is shown, and you can select between the two
        view controllers using the tabs. This isn’t noticeable yet because the
        two views are exactly the same, but internally the tab view controller
        is replacing them when you select a tab.
    </p>
    <h2>
        Overview View Controller
    </h2>
    <p>
        Next up you need to create the
    </p>
    <p>
        Go to
        <em>
            File\New\File…
        </em>
        , choose the
        <em>
            OS X\Source\Cocoa Class
        </em>
        , and click
        <em>
            Next
        </em>
        . Name the class
        <em>
            OverviewController
        </em>
        , make it a subclass of
        <em>
            NSViewController
        </em>
        , and make sure
        <em>
            Also Create XIB for user interface
        </em>
        is not selected. Click
        <em>
            Next
        </em>
        and save.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/add-overview.png"
        sl-processed="1">
            <img class="aligncenter wp-image-113621 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/09/add-overview-453x320.png"
            alt="add-overview" width="453" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/add-overview-453x320.png 453w, https://koenig-media.raywenderlich.com/uploads/2015/09/add-overview-700x495.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/add-overview.png 716w"
            sizes="(max-width: 453px) 100vw, 453px">
        </a>
    </p>
    <p>
        Return to
        <em>
            Main.storyboard
        </em>
        and select
        <em>
            Overview Scene
        </em>
        . Click the blue circle on the view and change the class to
        <em>
            OverviewController
        </em>
        in the
        <em>
            Identity Inspector
        </em>
        on the right.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/OverviewVC.png"
        sl-processed="1">
            <img class="size-medium wp-image-112832 aligncenter" src="https://koenig-media.raywenderlich.com/uploads/2015/08/OverviewVC-480x246.png"
            alt="OverviewVC" width="480" height="246" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/OverviewVC-480x246.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/08/OverviewVC.png 633w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Drag three
        <em>
            labels
        </em>
        onto the
        <em>
            OverviewController’s
        </em>
        view. Place the labels on the top left side of the view, one below each
        other. Add an
        <em>
            image view
        </em>
        on the top right corner of the view.
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            By default, the image view has no borders and can be a bit difficult to
            find in the view. To help during the layout process, you can set an image.
            With the image view selected, open the
            <em>
                Attributes Inspector
            </em>
            and select
            <em>
                games
            </em>
            in the
            <em>
                Image
            </em>
            field. This image will be replaced in runtime with the proper product
            image in the tutorial code
        </p>
    </div>
    <p>
        Select the top label. In the
        <em>
            Attributes Inspector
        </em>
        , change the font to System Bold and the size to 19.
    </p>
    <p>
        The view should now look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/overview-finished-ui.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113650" src="https://koenig-media.raywenderlich.com/uploads/2015/09/overview-finished-ui.png"
            alt="overview-finished-ui" width="459" height="340" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/overview-finished-ui.png 459w, https://koenig-media.raywenderlich.com/uploads/2015/09/overview-finished-ui-432x320.png 432w"
            sizes="(max-width: 459px) 100vw, 459px">
        </a>
    </p>
    <p>
        It’s time to use the superpowers of auto layout to make this view look
        great.
    </p>
    <p>
        Select the image view and click the
        <em>
            Pin
        </em>
        button on the bottom. Add constraints for top and trailing with the standard
        value, and constraints for width and height with a value of 180.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/image-constraints.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113624" src="https://koenig-media.raywenderlich.com/uploads/2015/09/image-constraints-700x377.png"
            alt="image-constraints" width="700" height="377" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/image-constraints-700x377.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/image-constraints-480x259.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/image-constraints.png 766w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Select the top label and add bottom, top, leading, and trailing constraints
        using the standard value.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/toplabel-constraints.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113625" src="https://koenig-media.raywenderlich.com/uploads/2015/09/toplabel-constraints-700x331.png"
            alt="toplabel-constraints" width="700" height="331" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/toplabel-constraints-700x331.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/toplabel-constraints-480x227.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/toplabel-constraints.png 957w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Select the label below and add constraints for trailing and leading using
        the standard value.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/middlelabel-constraints.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113626" src="https://koenig-media.raywenderlich.com/uploads/2015/09/middlelabel-constraints-700x370.png"
            alt="middlelabel-constraints" width="700" height="370" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/middlelabel-constraints-700x370.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/middlelabel-constraints-480x254.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/middlelabel-constraints.png 778w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Repeat for the last label, adding constraints for leading, trailing and
        bottom, using the standard value. For the top constraint, make sure that
        the image view is selected (so that the top is aligned to the image view
        instead of the super view), and use the standard value.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/bottomlabel-constraints.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113627" src="https://koenig-media.raywenderlich.com/uploads/2015/09/bottomlabel-constraints-700x336.png"
            alt="bottomlabel-constraints" width="700" height="336" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/bottomlabel-constraints-700x336.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/bottomlabel-constraints-480x230.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/bottomlabel-constraints.png 854w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <div class="note">
        <p>
            <em>
                Note:
            </em>
            If you can’t see the image view in the selection menu, you may need to
            make the label wider, so that the end of the label is under the image view.
        </p>
    </div>
    <p>
        Click on the
        <em>
            Resolve Auto Layout
        </em>
        button in the bottom bar and select
        <em>
            All Views in Controller/Update Frames
        </em>
        . Your view should look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/overview-after-layout.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113628" src="https://koenig-media.raywenderlich.com/uploads/2015/09/overview-after-layout.png"
            alt="overview-after-layout" width="457" height="293">
        </a>
    </p>
    <p>
        After all your hard work on the interface, it’s finally time to see the
        result, so build and run.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/build-run-overview1.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113651" src="https://koenig-media.raywenderlich.com/uploads/2015/09/build-run-overview1.png"
            alt="build-run-overview" width="480" height="335" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/build-run-overview1.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/build-run-overview1-459x320.png 459w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
    </p>
    <p>
        Click on the tabs and see how the tab view controller shows the appropriate
        view controller. It works right out of the box and without a single line
        of code!
    </p>
    <h2>
        Add Some Code
    </h2>
    <p>
        It’s time to get your hands dirty adding some code to show the products
        details in the view. In order to refer to the labels and image view from
        code you need to add an
        <em>
            IBOutlet
        </em>
        for each of them.
    </p>
    <p>
        First, open the
        <em>
            Assistant Editor
        </em>
        and make sure
        <em>
            OverviewViewController.swift
        </em>
        is selected.&nbsp;
        <em>
            Control-drag
        </em>
        from the top label into
        <em>
            OverviewController.swift
        </em>
        and add an outlet named
        <code>
            titleLabel
        </code>
        . Ensure&nbsp;the type is
        <em>
            NSTextField
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/title-outlet.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113630" src="https://koenig-media.raywenderlich.com/uploads/2015/09/title-outlet-700x335.png"
            alt="title-outlet" width="700" height="335" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/title-outlet-700x335.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/title-outlet-480x230.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/title-outlet.png 889w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Repeat the process with the other two labels and the image view to create
        the rest of the outlets with the following names:
    </p>
    <ol>
        <li>
            <code>
                priceLabel
            </code>
            for the label in the middle.
        </li>
        <li>
            <code>
                descriptionLabel
            </code>
            for the bottom label.
        </li>
        <li>
            <code>
                productImageView
            </code>
            for the image view.
        </li>
    </ol>
    <p>
        Like most UI elements, labels and image views are built of multiple subviews,
        so make sure that you have the correct view selected. You can see this
        when you look at the class for the outlet: for the image view it must be
        <em>
            NSImageView
        </em>
        , not
        <em>
            NSImageCell
        </em>
        . For the labels, it must be
        <em>
            NSTextField
        </em>
        , not
        <em>
            NSTextFieldCell
        </em>
        .
    </p>
    <p>
        To show the product information in the overview tab, open
        <em>
            OverviewController.swift
        </em>
        and add the following code inside the class implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1128111">
                    <td class="code" id="p112811code1">
                        <pre class="swift" style="font-family:monospace;">
                            //1 let numberformatter = NSNumberFormatter() //2 var selectedProduct:
                            Product? { didSet { updateUI() } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Taking this code bit-by-bit:
    </p>
    <ol>
        <li>
            <code>
                numberformatter
            </code>
            is an
            <code>
                NSNumberFormatter
            </code>
            object used to show the value of the price, formatted as currency.
        </li>
        <li>
            <code>
                selectedProduct
            </code>
            holds the currently selected product. Every time the value changes,
            <code>
                didSet
            </code>
            is executed, and with it
            <code>
                updateUI()
            </code>
            .
        </li>
    </ol>
    <p>
        Now add the&nbsp;
        <code>
            updateUI
        </code>
        method to
        <em>
            OverviewController.swift
        </em>
        .
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1128112">
                    <td class="code" id="p112811code2">
                        <pre class="swift" style="font-family:monospace;">
                            private func updateUI() { //1 if viewLoaded { //2 if let product = selectedProduct
                            { productImageView.image = product.image titleLabel.stringValue = product.title
                            priceLabel.stringValue = numberformatter.stringFromNumber(product.price)!
                            descriptionLabel.stringValue = product.descriptionText } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <ol>
        <li>
            Checks to see if the view is loaded.
            <code>
                viewLoaded
            </code>
            is a property of
            <code>
                NSViewController
            </code>
            , and it’s true if the view is loaded into memory. If the view is loaded,
            it’s safe to access all view-related properties, like the labels.
        </li>
        <li>
            Unwraps
            <code>
                selectedProduct
            </code>
            to see if there is a product. After that, the labels and image are updated
            to show the appropriate values.
        </li>
    </ol>
    <p>
        This method is already called when the product changes, but also needs
        to called as the view is ready to be displayed.
    </p>
    <h2>
        View Controller Life Cycle
    </h2>
    <p>
        Since view controllers are responsible for managing views, they expose
        methods that allow you to hook into events associated with the views. For
        example&nbsp;the point at which the views have loaded from the storyboard,
        or when the views are about to appear on the screen. This collection of
        event-based methods are known as the
        <em>
            view controller life cycle
        </em>
        .
    </p>
    <p>
        The life cycle of a view controller can be divided into three major parts:
        its creation, its lifetime, and finally its termination. Each part has
        methods you can override to do additional work.
    </p>
    <h3>
        Creation
    </h3>
    <ol>
        <li>
            <code>
                viewDidLoad()
            </code>
            is called once the view is fully loaded and can be used to do one-time
            initializations like the configuration of a number formatter, register
            for notifications, or API calls that only need to be done once.
        </li>
        <li>
            <code>
                viewWillAppear()
            </code>
            is called every time the view is about to appear on screen. In our application,
            it is called every time you select the Overview tab. This is a good point
            to update your UI or to refresh your data model.
        </li>
        <li>
            <code>
                viewDidAppear()
            </code>
            is called after the view appears on screen. Here you can start some fancy
            animations.
        </li>
    </ol>
    <h3>
        Lifetime
    </h3>
    <p>
        Once a view controller has been created, it then enters a period during
        which it it handles user interactions. It has three methods specific to
        this phase of its life:
    </p>
    <ol>
        <li>
            <code>
                updateViewConstraints()
            </code>
            is called every time the layout changes, like when the window is resized.
        </li>
        <li>
            <code>
                viewWillLayout()
            </code>
            is called before the
            <code>
                layout()
            </code>
            method of a view controller’s view is called. For example, you can use
            this method to adjust constraints.
        </li>
        <li>
            <code>
                viewDidLayout()
            </code>
            is called after
            <code>
                layout()
            </code>
            is called.
        </li>
    </ol>
    <p>
        In all three methods, you must call the&nbsp;
        <em>
            super
        </em>
        implementation at some point.
    </p>
    <h3>
        Termination
    </h3>
    <p>
        These are the counterpart methods to creation:
    </p>
    <ol>
        <li>
            <code>
                viewWillDisappear()
            </code>
            is called before the view disappears. Here you can stop your fancy animations
            you started in
            <code>
                viewDidAppear()
            </code>
            .
        </li>
        <li>
            <code>
                viewDidDisappear()
            </code>
            is called after the view is no longer on the screen. Here you can discard&nbsp;everything
            you no longer need. For example, you could invalidate a timer you used
            to upate your data model on a periodic time base.
        </li>
    </ol>
    <p>
        &nbsp;
    </p>
    <h3>
        Life cycle in practice
    </h3>
    <p>
        Now that you know the most important things about a view controller’s
        life cycle, it’s time for a short test!
    </p>
    <p>
        Question: Every time
        <em>
            OverviewController’s
        </em>
        view appears, you want to update the UI to take into account that a user
        selected a product when the Details tab was selected. Which method would
        be a good fit?
        <br>
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
                        <a href="" onclick="wpSpoilerSelect(&quot;spoilerDiv5a5c8001&quot;); return false;"
                        class="easySpoilerButtonOther" style="font-size:100%;color:#000000;background-color:#fcfcfc;background-image:none;border: 1px inset;border-style:solid;border-color:#cccccc; margin: 3px 0px 3px; padding: 4px; "
                        align="right" sl-processed="1">
                            Select
                        </a>
                        <a href="" onclick="wpSpoilerToggle(&quot;spoilerDiv5a5c8001&quot;,true,&quot;Show&quot;,&quot;Hide&quot;,&quot;fast&quot;,false); return false;"
                        id="spoilerDiv5a5c8001_action" class="easySpoilerButton" value="Show" align="right"
                        style="font-size:100%;color:#000000;background-color:#fcfcfc;background-image:none;border: 1px inset;border-style:solid;border-color:#cccccc; margin: 3px 0px 3px 5px; padding: 4px;"
                        sl-processed="1">
                            Show
                        </a>
                    </th>
                </tr>
                <tr>
                    <td class="easySpoilerRow" colspan="2" style="">
                        <div id="spoilerDiv5a5c8001" class="easySpoilerSpoils" style="display:none; white-space:wrap; overflow:auto; vertical-align:middle;">
                            <br>
                            There are two possible methods:
                            <code>
                                viewWillAppear()
                            </code>
                            and
                            <code>
                                viewDidAppear()
                            </code>
                            . The best solution is to use
                            <code>
                                viewWillAppear()
                            </code>
                            so that the user sees the updated UI at the moment the view appears. Using
                            <code>
                                viewDidAppear()
                            </code>
                            means that a user would see the UI appear first showing old data before
                            updating.
                            <br>
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
    </p>
    <p>
        &nbsp;
    </p>
    <p>
        Open
        <em>
            OverviewController.swift
        </em>
        and add this code inside the class implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1128113">
                    <td class="code" id="p112811code3">
                        <pre class="swift" style="font-family:monospace;">
                            override func viewWillAppear() { updateUI() }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This overrides the
        <code>
            viewWillAppear
        </code>
        to update the user interface before the view becomes visible.
    </p>
    <p>
        The number formatter currently uses default values, which doesn’t fit
        your needs. You’ll configure it to format numbers as currency values; since
        you only need to do this once, a good place is the method
        <code>
            viewDidLoad()
        </code>
        .
    </p>
    <p>
        In
        <code>
            OverviewController
        </code>
        add this code inside&nbsp;
        <code>
            viewDidLoad()
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1128114">
                    <td class="code" id="p112811code4">
                        <pre class="swift" style="font-family:monospace;">
                            numberformatter.numberStyle = .CurrencyStyle
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        For the next step, the main view controller needs to react on product
        selection and then inform the
        <code>
            OverviewController
        </code>
        about this change. The best place for this is in the
        <em>
            ViewController
        </em>
        class, because this controller owns the pop-up button. Open
        <em>
            ViewController.swift
        </em>
        and add a these properties inside the
        <em>
            ViewController
        </em>
        class implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1128115">
                    <td class="code" id="p112811code5">
                        <pre class="swift" style="font-family:monospace;">
                            private var products = [Product]() var selectedProduct: Product!
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The first property,
        <code>
            products
        </code>
        , is an array used to keep a reference to all the products. The second,
        <code>
            selectedProduct
        </code>
        , holds the product selected in the pop-up button.
    </p>
    <p>
        Find
        <code>
            viewDidLoad()
        </code>
        and add the following code inside:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1128116">
                    <td class="code" id="p112811code6">
                        <pre class="swift" style="font-family:monospace;">
                            if let filePath = NSBundle.mainBundle().pathForResource("Products", ofType:
                            "plist") { products = Product.productsList(filePath) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This loads the array of products from the plist file using the
        <code>
            Product
        </code>
        class added at the beginning of the tutorial, and keeps it in the
        <code>
            products
        </code>
        property. Now you can use this array to populate the pop-up button.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        , select
        <em>
            View Controller Scene
        </em>
        , and switch to the
        <em>
            Assistant Editor
        </em>
        . Make sure
        <em>
            ViewController.swift
        </em>
        is selected, and
        <em>
            Control-drag
        </em>
        from the pop-up button to
        <em>
            ViewController.swift
        </em>
        to create an outlet named
        <em>
            productsButton
        </em>
        . Make sure the type is
        <code>
            NSPopUpButton
        </code>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/popup-outlet.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113631" src="https://koenig-media.raywenderlich.com/uploads/2015/09/popup-outlet-700x174.png"
            alt="popup-outlet" width="700" height="174" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/popup-outlet-700x174.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/popup-outlet-480x120.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/popup-outlet.png 971w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Return to
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
                <tr id="p1128117">
                    <td class="code" id="p112811code7">
                        <pre class="swift" style="font-family:monospace;">
                            //1 productsButton.removeAllItems() //2 for product in products { productsButton.addItemWithTitle(product.title)
                            } //3 selectedProduct = products[0] productsButton.selectItemAtIndex(0)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This piece of code does the following:
    </p>
    <ol>
        <li>
            It removes all items in the pop-up button, getting rid of the Item1 and
            Item2 entries.
        </li>
        <li>
            It adds an item for every product, showing its title.
        </li>
        <li>
            It selects the first product and the first item of the pop-up button.
            This makes sure that everything is consistent.
        </li>
    </ol>
    <p>
        The final piece in this puzzle&nbsp;is reacting to the pop-up button selection
        changes. Find
        <code>
            valueChanged(_:)
        </code>
        and add the following lines:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1128118">
                    <td class="code" id="p112811code8">
                        <pre class="swift" style="font-family:monospace;">
                            if let bookTitle = sender.selectedItem?.title, let index = products.indexOf({$0.title
                            == bookTitle}) { selectedProduct = products[index] }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This code tries to get the selected book title and searches in the products
        for the index of the title. With this index, it sets
        <code>
            selectedProduct
        </code>
        to the correct product.
    </p>
    <p>
        Now you only need to inform
        <code>
            OverviewController
        </code>
        &nbsp;when the selected product&nbsp;changes. For this you need a reference
        to the
        <code>
            OverviewController
        </code>
        . You can get a reference within code, but first you have to add another
        property to
        <em>
            ViewController.swift
        </em>
        to hold that reference. Add the following code inside the
        <code>
            ViewController
        </code>
        implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1128119">
                    <td class="code" id="p112811code9">
                        <pre class="swift" style="font-family:monospace;">
                            private var overviewViewController: OverviewController!
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        You can get the instance of
        <code>
            OverviewController
        </code>
        inside
        <code>
            prepareForSegue(_:, sender:)
        </code>
        , which is called by the system when the view controllers are embedded
        in the container view. Add the following method to the
        <code>
            ViewController
        </code>
        implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p11281110">
                    <td class="code" id="p112811code10">
                        <pre class="swift" style="font-family:monospace;">
                            override func prepareForSegue(segue: NSStoryboardSegue, sender: AnyObject?)
                            { //1 let tabViewController = segue.destinationController as! NSTabViewController
                            //2 for controller in tabViewController.childViewControllers { //3 if controller
                            is OverviewController { overviewViewController = controller as! OverviewController
                            overviewViewController.selectedProduct = selectedProduct } else { //More
                            later } } }
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
            Gets a reference to the Tab View controller.
        </li>
        <li>
            Iterates over all its child view controllers.
        </li>
        <li>
            Checks if the current child view controller is an instance of
            <code>
                OverviewController
            </code>
            , and if it is, sets its
            <code>
                selectedProduct
            </code>
            property.
        </li>
    </ol>
    <p>
        Now add the following line in the method
        <code>
            valueChanged(_:)
        </code>
        , inside the
        <em>
            if let
        </em>
        block.
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p11281111">
                    <td class="code" id="p112811code11">
                        <pre class="swift" style="font-family:monospace;">
                            overviewViewController.selectedProduct = selectedProduct
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run to see how the UI updates when you select a different product.
    </p>
    <p>
        <img class="aligncenter wp-image-119457 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/10/OverviewRun-700x304.png"
        alt="" width="700" height="304" srcset="https://koenig-media.raywenderlich.com/uploads/2015/10/OverviewRun-700x304.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/10/OverviewRun-480x209.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/10/OverviewRun.png 854w"
        sizes="(max-width: 700px) 100vw, 700px">
    </p>
    <h2>
        Detail View Controller
    </h2>
    <p>
        Now we’ll create a view controller class for the Details tab.
    </p>
    <p>
        Go to
        <em>
            File\New\File…
        </em>
        , choose
        <em>
            OS X\Source\Cocoa Class
        </em>
        , and click
        <em>
            Next
        </em>
        . Name the class
        <em>
            DetailViewController
        </em>
        , make it a subclass of
        <em>
            NSViewController
        </em>
        , and make sure
        <em>
            Also Create XIB for user interface
        </em>
        is not selected. Click
        <em>
            Next
        </em>
        and save.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/create-detailviewcontroller.png"
        sl-processed="1">
            <img class="aligncenter wp-image-113634 size-medium" src="https://koenig-media.raywenderlich.com/uploads/2015/09/create-detailviewcontroller-455x320.png"
            alt="create-detailviewcontroller" width="455" height="320" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/create-detailviewcontroller-455x320.png 455w, https://koenig-media.raywenderlich.com/uploads/2015/09/create-detailviewcontroller-700x492.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/create-detailviewcontroller.png 715w"
            sizes="(max-width: 455px) 100vw, 455px">
        </a>
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and select
        <em>
            Details Scene
        </em>
        . In the
        <em>
            Identity Inspector
        </em>
        change the class to
        <code>
            DetailViewController
        </code>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-vcname.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113636" src="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-vcname.png"
            alt="detail-vcname" width="258" height="321" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-vcname.png 258w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail-vcname-257x320.png 257w"
            sizes="(max-width: 258px) 100vw, 258px">
        </a>
    </p>
    <p>
        Add an
        <code>
            image view
        </code>
        to the detail view. Select it and click on the
        <em>
            Pin
        </em>
        button to create its constraints. Set
        <em>
            width
        </em>
        and
        <em>
            height
        </em>
        constraints to a value of
        <em>
            180
        </em>
        , and a
        <em>
            top
        </em>
        constraint to the
        <em>
            standard
        </em>
        &nbsp;value.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-imageview-pin-constraints.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113637" src="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-imageview-pin-constraints-700x394.png"
            alt="detail-imageview-pin-constraints" width="700" height="394" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-imageview-pin-constraints-700x394.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail-imageview-pin-constraints-480x270.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail-imageview-pin-constraints-266x151.png 266w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail-imageview-pin-constraints.png 761w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Click on the
        <em>
            Align
        </em>
        button in the bottom bar and add a constraint to center the view
        <em>
            Horizontally in the Container
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-image-align-constraint.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113638" src="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-image-align-constraint-700x399.png"
            alt="detail-image-align-constraint" width="700" height="399" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-image-align-constraint-700x399.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail-image-align-constraint-480x274.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail-image-align-constraint-266x151.png 266w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail-image-align-constraint.png 752w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Add a label below the image view. Change the font to bold and the size
        to 19, then click on the
        <em>
            Pin
        </em>
        button to add constraints for
        <em>
            top
        </em>
        ,
        <em>
            leading
        </em>
        , and
        <em>
            trailing
        </em>
        , using the
        <em>
            standard
        </em>
        values.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-middlelabel-constraing.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113639" src="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-middlelabel-constraing-700x425.png"
            alt="detail-middlelabel-constraing" width="700" height="425" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-middlelabel-constraing-700x425.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail-middlelabel-constraing-480x292.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail-middlelabel-constraing.png 772w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Add another label below the previous one. Select it, and click on the
        <em>
            Pin
        </em>
        button first to and add also constraints for
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
        , using
        <em>
            standard
        </em>
        &nbsp;values.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-bottom-label-constraint.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113640" src="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-bottom-label-constraint-700x363.png"
            alt="detail-bottom-label-constraint" width="700" height="363" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-bottom-label-constraint-700x363.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail-bottom-label-constraint-480x249.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail-bottom-label-constraint.png 761w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Drag an
        <em>
            NSBox
        </em>
        under the last label. Select it and add constraints for
        <em>
            top
        </em>
        ,
        <em>
            leading
        </em>
        ,
        <em>
            trailing
        </em>
        and
        <em>
            bottom
        </em>
        , using
        <em>
            standard
        </em>
        values.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-box-constraints.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113641" src="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-box-constraints-700x413.png"
            alt="detail-box-constraints" width="700" height="413" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-box-constraints-700x413.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail-box-constraints-480x283.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail-box-constraints.png 762w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Open the
        <em>
            Attributes Inspector
        </em>
        and change the box font to
        <em>
            bold
        </em>
        and the size to
        <em>
            14
        </em>
        . Change the title to “Who is this Book For?”.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/NSBoxSettings.png"
        sl-processed="1">
            <img class="size-full wp-image-112840 aligncenter" src="https://koenig-media.raywenderlich.com/uploads/2015/08/NSBoxSettings.png"
            alt="NSBoxSettings" width="257" height="246" srcset="https://koenig-media.raywenderlich.com/uploads/2015/08/NSBoxSettings.png 257w, https://koenig-media.raywenderlich.com/uploads/2015/08/NSBoxSettings-32x32.png 32w"
            sizes="(max-width: 257px) 100vw, 257px">
        </a>
    </p>
    <p>
        An
        <code>
            NSBox
        </code>
        is a nice way to group related UI elements and to give this group a name
        you can see in
        <i>
            Xcode’s
        </i>
        <em>
            Identity Inspector
        </em>
        .
    </p>
    <p>
        To complete the UI, drag a label inside the content area of the
        <code>
            NSBox
        </code>
        . Select the label and click on the
        <em>
            Pin
        </em>
        button to add constraints for
        <em>
            top
        </em>
        ,
        <em>
            leading
        </em>
        ,
        <em>
            trailing
        </em>
        , and
        <em>
            bottom
        </em>
        , all using the
        <em>
            standard
        </em>
        value.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/detail.label-inbox-constraint.png"
        sl-processed="1">
            <img class="aligncenter size-large wp-image-113642" src="https://koenig-media.raywenderlich.com/uploads/2015/09/detail.label-inbox-constraint-700x424.png"
            alt="detail.label-inbox-constraint" width="700" height="424" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/detail.label-inbox-constraint-700x424.png 700w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail.label-inbox-constraint-480x291.png 480w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail.label-inbox-constraint.png 771w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        After updating the frames, the UI should look like this:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-finished-ui.png"
        sl-processed="1">
            <img class="aligncenter size-full wp-image-113643" src="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-finished-ui.png"
            alt="detail-finished-ui" width="457" height="395" srcset="https://koenig-media.raywenderlich.com/uploads/2015/09/detail-finished-ui.png 457w, https://koenig-media.raywenderlich.com/uploads/2015/09/detail-finished-ui-370x320.png 370w"
            sizes="(max-width: 457px) 100vw, 457px">
        </a>
    </p>
    <p>
        To create the outlets for those controls, open the
        <em>
            Assistant Editor
        </em>
        and make sure that
        <em>
            DetailsViewController.swift
        </em>
        is open. Add four IBOutlets, giving them the following names:
    </p>
    <ol>
        <li>
            <code>
                productImageView
            </code>
            for the NSImageView.
        </li>
        <li>
            <code>
                titleLabel
            </code>
            for the label with the bold font.
        </li>
        <li>
            <code>
                descriptionLabel
            </code>
            for the label below.
        </li>
        <li>
            <code>
                audienceLabel
            </code>
            for the label in the NSBox.
        </li>
    </ol>
    <p>
        With the outlets in place, add the implementation to show the product
        detail. Add the following code to
        <code>
            DetailViewController
        </code>
        class implementation:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p11281112">
                    <td class="code" id="p112811code12">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 var selectedProduct: Product? { didSet { updateUI() } } // 2 override
                            func viewWillAppear() { updateUI() } // 3 private func updateUI() { if
                            viewLoaded { if let product = selectedProduct { productImageView.image
                            = product.image titleLabel.stringValue = product.title descriptionLabel.stringValue
                            = product.descriptionText audienceLabel.stringValue = product.audience
                            } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        You’re probably familiar with this code already, because it’s very similar
        to the Overview view controller implementation. This code:
    </p>
    <ol>
        <li>
            Defines a
            <code>
                selectedProduct
            </code>
            property and updates the UI whenever it changes.
        </li>
        <li>
            Forces a UI update whenever the view appears (when the detail view tab
            is selected).
        </li>
        <li>
            Sets the product information (using
            <code>
                updateUI
            </code>
            ) in the labels and image view using the appropriate outlets.
        </li>
    </ol>
    <p>
        When the product selection changes, you need to change the selected product
        in the detail view controller so that it updates the UI. Open
        <em>
            ViewController.swift
        </em>
        and add a property to hold a reference to the the detail view controller.
        Just below the
        <code>
            overviewViewController
        </code>
        property, add the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p11281113">
                    <td class="code" id="p112811code13">
                        <pre class="swift" style="font-family:monospace;">
                            private var detailViewController: DetailViewController!
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Find
        <code>
            valueChanged(_:)
        </code>
        and add the following inside:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p11281114">
                    <td class="code" id="p112811code14">
                        <pre class="swift" style="font-family:monospace;">
                            detailViewController.selectedProduct = selectedProduct
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This updates the selected product property of the view controller when
        the pop-up selection changes.
    </p>
    <p>
        The last change is inside
        <code>
            prepareForSegue(_:, sender:)
        </code>
        . Find the comment
        <code>
            //More later
        </code>
        and replace with the following:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p11281115">
                    <td class="code" id="p112811code15">
                        <pre class="swift" style="font-family:monospace;">
                            detailViewController = controller as! DetailViewController detailViewController.selectedProduct
                            = selectedProduct
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This updates the
        <code>
            selectedProduct
        </code>
        when the detail view is embedded.
    </p>
    <p>
        Build and run, and enjoy your finished application!
    </p>
    <p>
        <img class="aligncenter wp-image-119456 size-large" src="https://koenig-media.raywenderlich.com/uploads/2015/10/FinalRun-635x500.png"
        alt="" width="635" height="500" srcset="https://koenig-media.raywenderlich.com/uploads/2015/10/FinalRun-635x500.png 635w, https://koenig-media.raywenderlich.com/uploads/2015/10/FinalRun-407x320.png 407w, https://koenig-media.raywenderlich.com/uploads/2015/10/FinalRun.png 700w"
        sizes="(max-width: 635px) 100vw, 635px">
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
        You can download the final project
        <a href="https://koenig-media.raywenderlich.com/uploads/2015/08/RWStore.zip"
        sl-processed="1">
            here
        </a>
        .
    </p>
    <p>
        In this OS X view controller tutorial you’ve learned the following:
    </p>
    <ul>
        <li>
            What a view controller is and how it compares to a window controller
        </li>
        <li>
            Creating a custom view controller subclass
        </li>
        <li>
            How to connect elements in your view to a view controller
        </li>
        <li>
            How to manipulate the view from the view controller
        </li>
        <li>
            The lifecycle of&nbsp;a view controller, and how to hook into the different
            events
        </li>
    </ul>
    <p>
        In addition to the functionality you’ve added to your custom view controller
        subclasses, there are many built-in subclasses provided for you. To see
        what built-in view controllers are available, take a look at the
        <a href="https://developer.apple.com/library/mac/documentation/Cocoa/Reference/NSViewController_Class/index.html#//apple_ref/swift/cl/c:objc(cs)NSViewController"
        target="_blank" sl-processed="1">
            documentation
        </a>
        .
    </p>
    <p>
        If you’re not already read it, you should take a look at Gabriel Miro’s
        excellent
        <a href="http://www.raywenderlich.com/111947/windows-and-window-controllers-in-os-x-tutorial"
        sl-processed="1">
            tutorial on windows and window controllers
        </a>
        .
    </p>
    <p>
        View controllers are one of the most powerful and useful aspects of architecting
        an OS X app, and there’s plenty more to learn. However, you’re now equipped
        with the knowledge to go out there and start playing around building apps
        — which you should do now!
    </p>
</div>