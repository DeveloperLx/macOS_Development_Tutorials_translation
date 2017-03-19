# OS X教程：高级Collection Views

#### [原文地址](https://www.raywenderlich.com/132268/advanced-collection-views-os-x-tutorial) 翻译：[DeveloperLx](http://weibo.com/DeveloperLx)

<div class="content-wrapper">
    <p>
        <img src="https://koenig-media.raywenderlich.com/uploads/2016/05/CollectionViews-adv-feature-250x250.png"
        alt="Advanced Collection Views in OS X Tutorial" width="250" height="250"
        class="alignright size-full wp-image-132621 bordered">
    </p>
    <p>
        If you want to learn about the advanced capabilities of
        <code>
            NSCollectionView
        </code>
        , you’ve come to the right place. This is the second part of a tutorial
        that covered the basics, and in this Advanced Collection Views in OS X
        Tutorial, you step deeper into the encompassing world of collection views.
    </p>
    <p>
        In this OS X tutorial, you’ll learn how:
    </p>
    <ul>
        <li>
            To add, remove, move and reorder items
        </li>
        <li>
            To implement drag and drop with collection views
        </li>
        <li>
            To fine-tune selection and highlighting
        </li>
        <li>
            To use animation in collection views
        </li>
        <li>
            To implement sticky section headers
        </li>
    </ul>
    <h2>
        Prerequisites
    </h2>
    <p>
        You need basic knowledge of
        <code>
            NSCollectionView
        </code>
        , and you’ll need to know your way around the project from the
        <a href="https://www.raywenderlich.com/120494/collection-views-os-x-tutorial"
        title="Collection Views tutorial" target="_blank">
            Collection Views tutorial
        </a>
        .
    </p>
    <h2>
        Getting Started
    </h2>
    <p>
        <em>
            SlidesPro
        </em>
        is the app you’re going to build, and it picks up where the previous tutorial
        left off.
    </p>
    <p>
        Download the
        <em>
            SlidesPro
        </em>
        starter project
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesPro-Starter.zip">
            here
        </a>
        .
    </p>
    <p>
        Build and run.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProStarterScreen.png"
        rel="attachment wp-att-132276">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProStarterScreen-408x500.png"
            alt="SlidesProStarterScreen" width="408" height="500" class="aligncenter size-large wp-image-132276"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProStarterScreen-408x500.png 408w, https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProStarterScreen-261x320.png 261w, https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProStarterScreen-768x942.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProStarterScreen.png 960w"
            sizes="(max-width: 408px) 100vw, 408px">
        </a>
    </p>
    <h2>
        Add New Images to the Collection View
    </h2>
    <p>
        In this section, you’ll walk through the steps needed to add new items
        to the collection.
    </p>
    <h3>
        The Add Button
    </h3>
    <p>
        You’re not going to be able to add anything to that collection view until
        you make a way to do it. Good thing you’re a developer! What’s needed here
        is a button that displays a standard open panel from which you can choose
        images.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and drag a
        <em>
            Push Button
        </em>
        into the bottom of the collection view. In the
        <em>
            Attributes Inspector
        </em>
        , set its
        <em>
            Title
        </em>
        to
        <em>
            Add
        </em>
        , and uncheck
        <em>
            Enabled
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Slide-Button.png"
        rel="attachment wp-att-132280">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Slide-Button-625x500.png"
            alt="Add Slide Button" width="625" height="500" class="aligncenter size-large wp-image-132280"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Slide-Button-625x500.png 625w, https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Slide-Button-400x320.png 400w, https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Slide-Button-768x614.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Slide-Button.png 835w"
            sizes="(max-width: 625px) 100vw, 625px">
        </a>
    </p>
    <p>
        Select the
        <em>
            Editor \ Resolve Auto Layout Issues \ Add Missing Constraints
        </em>
        menu item to set the button’s
        <em>
            Auto Layout
        </em>
        constraints.
    </p>
    <p>
        Build and run and check if you’ve got a button.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Button-Added.png"
        rel="attachment wp-att-132282">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Button-Added-700x288.png"
            alt="Add Button Added" width="700" height="288" class="aligncenter size-large wp-image-132282"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Button-Added-700x288.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Button-Added-480x197.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Button-Added-768x316.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/Add-Button-Added.png 956w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <h3>
        Specify Where to Insert New Items
    </h3>
    <p>
        <em>
            SlidesPro
        </em>
        should be set up so that when you select an item, the new item is inserted
        starting at the index path of whatever image you’ve selected. Then this
        item and the rest of the section are pushed below the new items.
    </p>
    <p>
        Accordingly, the add button can only be enabled when an item is selected.
    </p>
    <p>
        In
        <code>
            ViewController
        </code>
        , add an
        <code>
            IBOutlet
        </code>
        for the button:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1322681">
                    <td class="code" id="p132268code1">
                        <pre class="swift" style="font-family:monospace;">
                            @IBOutlet weak var addSlideButton: NSButton!
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
        and connect the outlet to the button.
    </p>
    <p>
        You’ll need to track selection changes that will ultimately enable and
        disable the button inside of
        <code>
            highlightItems(_: atIndexPaths:)
        </code>
        , a
        <code>
            ViewController
        </code>
        method. When items are selected or deselected it’s called by the two
        <code>
            NSCollectionViewDelegate
        </code>
        methods.
    </p>
    <p>
        To do this, you just need to append one line to
        <code>
            highlightItems(_: atIndexPaths:)
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1322682">
                    <td class="code" id="p132268code2">
                        <pre class="swift" style="font-family:monospace;">
                            func highlightItems(selected: Bool, atIndexPaths: Set&lt;NSIndexPath&gt;)
                            { ....... ....... addSlideButton.enabled = collectionView.selectionIndexPaths.count
                            == 1 }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        With this line you enable the button only when one item is selected.
        <br>
        Build and run. Verify that the button is enabled only when an item is
        selected.
        <br>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/05/First_Run.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/05/First_Run-264x320.png"
            alt="First_Run" width="408" height="494" class="aligncenter size-medium wp-image-134402"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/05/First_Run-264x320.png 264w, https://koenig-media.raywenderlich.com/uploads/2016/05/First_Run-412x500.png 412w, https://koenig-media.raywenderlich.com/uploads/2016/05/First_Run.png 1440w"
            sizes="(max-width: 408px) 100vw, 408px">
        </a>
    </p>
    <h3>
        Insert the New Items
    </h3>
    <p>
        Adding new items to a collection view is a two-stage process. First, you
        add the items to the model then notify the collection view about the changes.
    </p>
    <div class="note">
        <em>
            Note
        </em>
        : When editing operations, such as add, remove and move, you must always
        update the model before you notify the collection view to tell it to update
        its layout.
    </div>
    <p>
        To update your model, you’ll need to append the following to the
        <code>
            ImageDirectoryLoader
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1322683">
                    <td class="code" id="p132268code3">
                        <pre class="swift" style="font-family:monospace;">
                            func insertImage(image: ImageFile, atIndexPath: NSIndexPath) { let imageIndexInImageFiles
                            = sectionsAttributesArray[atIndexPath.section].sectionOffset + atIndexPath.item
                            imageFiles.insert(image, atIndex: imageIndexInImageFiles) let sectionToUpdate
                            = atIndexPath.section sectionsAttributesArray[sectionToUpdate].sectionLength
                            += 1 sectionLengthArray[sectionToUpdate] += 1 if sectionToUpdate &lt; numberOfSections-1
                            { for i in sectionToUpdate+1...numberOfSections-1 { sectionsAttributesArray[i].sectionOffset
                            += 1 } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        This method inserts the new image to your data model and updates everything
        so that your model stays in a consistent state.
    </p>
    <p>
        Add the following methods to
        <code>
            ViewController
        </code>
        . The first method is called from the
        <code>
            IBAction
        </code>
        method that’s triggered by clicking the add button, and then it’s followed
        by the action method:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1322684">
                    <td class="code" id="p132268code4">
                        <pre class="swift" style="font-family:monospace;">
                            private func insertAtIndexPathFromURLs(urls: [NSURL], atIndexPath: NSIndexPath)
                            { var indexPaths: Set&lt;NSIndexPath&gt; = [] let section = atIndexPath.section
                            var currentItem = atIndexPath.item &nbsp; // 1 for url in urls { // 2 let
                            imageFile = ImageFile(url: url) let currentIndexPath = NSIndexPath(forItem:
                            currentItem, inSection: section) imageDirectoryLoader.insertImage(imageFile,
                            atIndexPath: currentIndexPath) indexPaths.insert(currentIndexPath) currentItem
                            += 1 } &nbsp; // 3 collectionView.insertItemsAtIndexPaths(indexPaths) }
                            &nbsp; @IBAction func addSlide(sender: NSButton) { // 4 let insertAtIndexPath
                            = collectionView.selectionIndexPaths.first! //5 let openPanel = NSOpenPanel()
                            openPanel.canChooseDirectories = false openPanel.canChooseFiles = true
                            openPanel.allowsMultipleSelection = true; openPanel.allowedFileTypes =
                            ["public.image"] openPanel.beginSheetModalForWindow(self.view.window!)
                            { (response) -&gt; Void in guard response == NSFileHandlingPanelOKButton
                            else {return} self.insertAtIndexPathFromURLs(openPanel.URLs, atIndexPath:
                            insertAtIndexPath) } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <ol>
        <li>
            This iterates over the
            <em>
                URLs
            </em>
            chosen in the
            <em>
                Open
            </em>
            panel.
        </li>
        <li>
            For each
            <em>
                URL
            </em>
            , an
            <code>
                ImageFile
            </code>
            instance is created and added to the model.
        </li>
        <li>
            This notifies the collection view.
        </li>
        <li>
            The
            <code>
                NSIndexPath
            </code>
            of the selected item defines where the insertion starts.
        </li>
        <li>
            This creates an
            <code>
                NSOpenPanel
            </code>
            and configures it to only allow the selection of image files and shows
            it.
        </li>
    </ol>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and connect the
        <code>
            addSlide(_:)
        </code>
        <code>
            IBAction
        </code>
        to the button.
    </p>
    <p>
        Build and run.
    </p>
    <p>
        Select the last image in Section 1 — on my system it’s the
        <em>
            Desert.jpg
        </em>
        slide.
    </p>
    <p>
        Click the
        <em>
            Add
        </em>
        button. In the
        <em>
            Open
        </em>
        panel navigate to the
        <em>
            My Private Zoo
        </em>
        folder inside the project’s root directory and select all files.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/MyPrivateZoo.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/MyPrivateZoo-700x408.png"
            alt="MyPrivateZoo" width="700" height="408" class="aligncenter size-large wp-image-132304"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/MyPrivateZoo-700x408.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/MyPrivateZoo-480x280.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/MyPrivateZoo.png 734w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Click
        <em>
            Open
        </em>
        . The app will insert the new images in Section 1, starting at item 2,
        where
        <em>
            Desert.jpg
        </em>
        was before the insertion.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/ZooBeforeAfter.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/ZooBeforeAfter-700x459.png"
            alt="ZooBeforeAfter" width="700" height="459" class="aligncenter size-large wp-image-132313"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/ZooBeforeAfter-700x459.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/ZooBeforeAfter-480x314.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/ZooBeforeAfter-768x503.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/ZooBeforeAfter.png 974w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <h2>
        Remove Items from the Collection View
    </h2>
    <p>
        To remove items in SlidesPro you’ll need a remove button, and it should
        sit next to the add button. The most logical implementation is that it
        should remove all selected items, hence, this button should be enabled
        only when one or more items are selected.
    </p>
    <p>
        And then there’s this detail: multi-selection must be enabled to allow
        you to work with more than one image at a time.
    </p>
    <p>
        This section will walk you through adding the button and enabling multi-select.
    </p>
    <h3>
        Enable Multi-Selection
    </h3>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and select the
        <em>
            Collection View
        </em>
        . In the
        <em>
            Attributes Inspector
        </em>
        , check
        <em>
            Allows Multiple Selection
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/MultipleSelection.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/MultipleSelection.png"
            alt="MultipleSelection" width="259" height="385" class="aligncenter size-full wp-image-132314"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/MultipleSelection.png 259w, https://koenig-media.raywenderlich.com/uploads/2016/04/MultipleSelection-215x320.png 215w"
            sizes="(max-width: 259px) 100vw, 259px">
        </a>
    </p>
    <p>
        Build and run and verify that multi-selection works.
    </p>
    <p>
        To expand or reduce a collection’s selection, press and hold the
        <em>
            shift
        </em>
        or
        <em>
            command
        </em>
        key while you click on various items. Multi-selections can reach across
        sections.
    </p>
    <h3>
        The Remove Button
    </h3>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        , and then drag a
        <em>
            Push Button
        </em>
        from the
        <em>
            Object Library
        </em>
        and place it to the left of the
        <em>
            Add
        </em>
        button.
    </p>
    <p>
        In the
        <em>
            Attributes Inspector
        </em>
        , set its
        <em>
            Title
        </em>
        to
        <em>
            Remove
        </em>
        , and uncheck
        <em>
            Enabled
        </em>
        .
        <br>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/05/RemoveButton.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/05/RemoveButton-480x314.png"
            alt="RemoveButton" width="480" height="314" class="aligncenter size-medium wp-image-134403"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/05/RemoveButton-480x314.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/05/RemoveButton-650x425.png 650w, https://koenig-media.raywenderlich.com/uploads/2016/05/RemoveButton.png 1600w"
            sizes="(max-width: 480px) 100vw, 480px">
        </a>
        <br>
        Set the button’s
        <em>
            Auto Layout
        </em>
        constraints by selecting the
        <em>
            Editor \ Resolve Auto Layout Issues \ Add Missing Constraints
        </em>
        menu item.
    </p>
    <p>
        Build and run.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/RemoveBtnAdded.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/RemoveBtnAdded-700x308.png"
            alt="RemoveBtnAdded" width="700" height="308" class="aligncenter size-large wp-image-132318"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/RemoveBtnAdded-700x308.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/RemoveBtnAdded-480x211.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/RemoveBtnAdded-768x338.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/RemoveBtnAdded.png 957w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Add an
        <code>
            IBOutlet
        </code>
        in
        <code>
            ViewController
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1322685">
                    <td class="code" id="p132268code5">
                        <pre class="swift" style="font-family:monospace;">
                            @IBOutlet weak var removeSlideButton: NSButton!
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
        and connect the outlet to the button.
    </p>
    <p>
        In
        <code>
            ViewController
        </code>
        , at the end of
        <code>
            highlightItems(_: atIndexPaths:)
        </code>
        , add the line to enable/disable the remove button.
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1322686">
                    <td class="code" id="p132268code6">
                        <pre class="swift" style="font-family:monospace;">
                            func highlightItems(selected: Bool, atIndexPaths: Set&lt;NSIndexPath&gt;)
                            { ....... ....... removeSlideButton.enabled = !collectionView.selectionIndexPaths.isEmpty
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run, then select an item. Both the add and remove buttons should
        become enabled. Add more items to the selection; the add button should
        become disabled while the remove button stays enabled.
    </p>
    <h3>
        Enable Removal of Items
    </h3>
    <p>
        Now you’ll add the code that removes items from the collection. As it
        is with adding, removing is a two-stage process where you must remove images
        from the model before notifying the collection view about the changes.
    </p>
    <p>
        To update the model, add the following method at the end of the
        <code>
            ImageDirectoryLoader
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1322687">
                    <td class="code" id="p132268code7">
                        <pre class="swift" style="font-family:monospace;">
                            func removeImageAtIndexPath(indexPath: NSIndexPath) -&gt; ImageFile {
                            let imageIndexInImageFiles = sectionsAttributesArray[indexPath.section].sectionOffset
                            + indexPath.item let imageFileRemoved = imageFiles.removeAtIndex(imageIndexInImageFiles)
                            let sectionToUpdate = indexPath.section sectionsAttributesArray[sectionToUpdate].sectionLength
                            -= 1 if sectionToUpdate &lt; numberOfSections-1 { for i in sectionToUpdate+1...numberOfSections-1
                            { sectionsAttributesArray[i].sectionOffset -= 1 } } return imageFileRemoved
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
            ViewController
        </code>
        , add the
        <code>
            IBAction
        </code>
        method that’s triggered when you click the
        <em>
            Remove
        </em>
        button:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1322688">
                    <td class="code" id="p132268code8">
                        <pre class="swift" style="font-family:monospace;">
                            @IBAction func removeSlide(sender: NSButton) { &nbsp; let selectionIndexPaths
                            = collectionView.selectionIndexPaths if selectionIndexPaths.isEmpty { return
                            } &nbsp; // 1 var selectionArray = Array(selectionIndexPaths) selectionArray.sortInPlace({path1,
                            path2 in return path1.compare(path2) == .OrderedDescending}) for itemIndexPath
                            in selectionArray { // 2 imageDirectoryLoader.removeImageAtIndexPath(itemIndexPath)
                            } &nbsp; // 3 collectionView.deleteItemsAtIndexPaths(selectionIndexPaths)
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s what happens in there:
    </p>
    <ol>
        <li>
            Creates an array to iterate over the selection in descending order regarding
            index paths, so you don’t need to adjust index path values during the iteration
        </li>
        <li>
            Removes selected items from the model
        </li>
        <li>
            Notifies the collection view that items have been removed
        </li>
    </ol>
    <p>
        Now open
        <em>
            Main.storyboard
        </em>
        and connect the
        <code>
            removeSlide(_:) IBAction
        </code>
        to the button.
    </p>
    <p>
        This is how the
        <em>
            Connections Inspector
        </em>
        of
        <em>
            View Controller
        </em>
        should look after adding the outlets and actions:
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProActionsOutlets.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProActionsOutlets.png"
            alt="SlidesProActionsOutlets" width="259" height="445" class="aligncenter size-full wp-image-132726"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProActionsOutlets.png 259w, https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesProActionsOutlets-186x320.png 186w"
            sizes="(max-width: 259px) 100vw, 259px">
        </a>
    </p>
    <p>
        Build and run.
    </p>
    <p>
        Select one or more images and click the
        <em>
            Remove
        </em>
        button to verify that it successfully removes the items.
    </p>
    <h2>
        Drag and Drop in Collection Views
    </h2>
    <p>
        One of the best things about OS X is that you can drag and drop items
        to move or copy them to different apps. Users expect this behavior, so
        you’d be wise to add it to anything you decide to put out there.
    </p>
    <p>
        With SlidesPro, you’ll use drag-and-drop to implement the following capabilities:
    </p>
    <ul>
        <li>
            Move items inside the collection view
        </li>
        <li>
            Drag image files from other apps into the collection view
        </li>
        <li>
            Drag items from the collection view into other apps
        </li>
    </ul>
    <p>
        To support drag-and-drop, you’ll need to implement the relevant
        <code>
            NSCollectionViewDelegate
        </code>
        methods, but you have to register the kind of drag-and-drop operations
        SlidesPro supports.
    </p>
    <p>
        Add the following method to
        <code>
            ViewController
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p1322689">
                    <td class="code" id="p132268code9">
                        <pre class="swift" style="font-family:monospace;">
                            func registerForDragAndDrop() { // 1 collectionView.registerForDraggedTypes([NSURLPboardType])
                            // 2 collectionView.setDraggingSourceOperationMask(NSDragOperation.Every,
                            forLocal: true) // 3 collectionView.setDraggingSourceOperationMask(NSDragOperation.Every,
                            forLocal: false) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        In here, you’ve:
    </p>
    <ol>
        <li>
            Registered for the dropped object types SlidesPro accepts
        </li>
        <li>
            Enabled dragging items within and into the collection view
        </li>
        <li>
            Enabled dragging items from the collection view to other applications
        </li>
    </ol>
    <p>
        At the end of
        <code>
            viewDidLoad()
        </code>
        , add:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13226810">
                    <td class="code" id="p132268code10">
                        <pre class="swift" style="font-family:monospace;">
                            registerForDragAndDrop()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run.
    </p>
    <p>
        Try to drag an item — the item will not move. Drag an image file from
        Finder and try to drop it on the collection view…nada.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/Screen-Shot-2016-05-08-at-4.34.29-PM.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/Screen-Shot-2016-05-08-at-4.34.29-PM.png"
            alt="What about left-clicking for 5 seconds...while kissing my elbow?"
            width="432" height="342" class="aligncenter size-full wp-image-133795">
        </a>
    </p>
    <p>
        I asked you to perform this test so you can see that items aren’t responding
        to dragging, and nothing related to drag-and-drop works. Why is that? You’ll
        soon discover.
    </p>
    <p>
        The first issue is that there needs to be some additional logic to handle
        the action, so append the following methods to the
        <code>
            NSCollectionViewDelegate
        </code>
        extension of
        <code>
            ViewController
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13226811">
                    <td class="code" id="p132268code11">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 func collectionView(collectionView: NSCollectionView, canDragItemsAtIndexes
                            indexes: NSIndexSet, withEvent event: NSEvent) -&gt; Bool { return true
                            } &nbsp; // 2 func collectionView(collectionView: NSCollectionView, pasteboardWriterForItemAtIndexPath
                            indexPath: NSIndexPath) -&gt; NSPasteboardWriting? { let imageFile = imageDirectoryLoader.imageFileForIndexPath(indexPath)
                            return imageFile.url.absoluteURL }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s what’s happening in here:
    </p>
    <ol>
        <li>
            When the collection view is about to start a drag operation, it sends
            this message to its
            <code>
                delegate
            </code>
            . The return value indicates whether the collection view is allowed to
            initiate the drag for the specified index paths. You need to be able to
            drag any item, so you return unconditionally
            <code>
                true
            </code>
            .
        </li>
        <li>
            Implementing this method is essential so the collection view can be a
            <em>
                Drag Source
            </em>
            . If the method in section one allows the drag to begin, the collection
            view invokes this method one time per item to be dragged. It requests a
            pasteboard writer for the item’s underlying model object. The method returns
            a custom object that implements
            <code>
                NSPasteboardWriting
            </code>
            ; in your case it’s
            <code>
                NSURL
            </code>
            . Returning
            <code>
                nil
            </code>
            prevents the drag.
        </li>
    </ol>
    <p>
        Build and run.
    </p>
    <p>
        Try to drag an item, the item moves… Hallelujah!
    </p>
    <p>
        Perhaps I spoke too soon? When you try to drop the item in a different
        location in the collection view, it just bounces back. Why? Because you
        did not define the collection view as a
        <em>
            Drop Target
        </em>
        .
    </p>
    <p>
        Now try to drag an item and drop it in Finder; a new image file is created
        matching the source
        <em>
            URL
        </em>
        . You
        <i>
            have
        </i>
        made progress because it works to drag-and-drop from
        <em>
            SlidesPro
        </em>
        to another app!
    </p>
    <h3>
        Define Your Drop Target
    </h3>
    <p>
        Add the following property to
        <code>
            ViewController
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13226812">
                    <td class="code" id="p132268code12">
                        <pre class="swift" style="font-family:monospace;">
                            var indexPathsOfItemsBeingDragged: Set&lt;NSIndexPath&gt;!
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Add the following methods to the
        <code>
            NSCollectionViewDelegate
        </code>
        extension of
        <code>
            ViewController
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13226813">
                    <td class="code" id="p132268code13">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 func collectionView(collectionView: NSCollectionView, draggingSession
                            session: NSDraggingSession, willBeginAtPoint screenPoint: NSPoint, forItemsAtIndexPaths
                            indexPaths: Set&lt;NSIndexPath&gt;) { indexPathsOfItemsBeingDragged = indexPaths
                            } &nbsp; // 2 func collectionView(collectionView: NSCollectionView, validateDrop
                            draggingInfo: NSDraggingInfo, proposedIndexPath proposedDropIndexPath:
                            AutoreleasingUnsafeMutablePointer&lt;NSIndexPath?&gt;, dropOperation proposedDropOperation:
                            UnsafeMutablePointer&lt;NSCollectionViewDropOperation&gt;) -&gt; NSDragOperation
                            { // 3 if proposedDropOperation.memory == NSCollectionViewDropOperation.On
                            { proposedDropOperation.memory = NSCollectionViewDropOperation.Before }
                            // 4 if indexPathsOfItemsBeingDragged == nil { return NSDragOperation.Copy
                            } else { return NSDragOperation.Move } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s a section-by-section breakdown of this code:
    </p>
    <ol>
        <li>
            An
            <code>
                optional
            </code>
            method is invoked when the dragging session is imminent. You’ll use this
            method to save the index paths of the items that are dragged. When this
            property is not
            <code>
                nil
            </code>
            , it’s an indication that the
            <em>
                Drag Source
            </em>
            is the collection view.
        </li>
        <li>
            Implement the delegation methods related to drop. This method returns
            the type of operation to perform.
        </li>
        <li>
            In
            <em>
                SlidesPro
            </em>
            , the items aren’t able to act as containers; this allows dropping between
            items but not dropping on them.
        </li>
        <li>
            When moving items inside the collection view, the operation is
            <code>
                Move
            </code>
            . When the
            <em>
                Dragging Source
            </em>
            is another app, the operation is
            <code>
                Copy
            </code>
            .
        </li>
    </ol>
    <p>
        Build and run.
    </p>
    <p>
        Drag an item. After you move it, you’ll see some weird gray rectangle
        with white text. As you keep moving the item over the other items, the
        same rectangle appears in the gap between the items.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/HeaderAsInterGapIndicator.gif">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/HeaderAsInterGapIndicator-700x404.gif"
            alt="HeaderAsInterGapIndicator" width="700" height="404" class="aligncenter size-large wp-image-132798"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/HeaderAsInterGapIndicator-700x404.gif 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/HeaderAsInterGapIndicator-480x277.gif 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/HeaderAsInterGapIndicator-768x444.gif 768w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        What is happening?
    </p>
    <p>
        Inside of
        <code>
            ViewController
        </code>
        , look at the
        <code>
            DataSource
        </code>
        method that’s invoked when the collection view asks for a supplementary
        view:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13226814">
                    <td class="code" id="p132268code14">
                        <pre class="swift" style="font-family:monospace;">
                            func collectionView(collectionView: NSCollectionView, viewForSupplementaryElementOfKind
                            kind: String, atIndexPath indexPath: NSIndexPath) -&gt; NSView { let view
                            = collectionView.makeSupplementaryViewOfKind(NSCollectionElementKindSectionHeader,
                            withIdentifier: "HeaderView", forIndexPath: indexPath) as! HeaderView view.sectionTitle.stringValue
                            = "Section \(indexPath.section)" let numberOfItemsInSection = imageDirectoryLoader.numberOfItemsInSection(indexPath.section)
                            view.imageCount.stringValue = "\(numberOfItemsInSection) image files" return
                            view }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        When you start dragging an item, the collection view’s layout asks for
        the interim gap indicator’s supplementary view. The above
        <code>
            DataSource
        </code>
        method unconditionally assumes that this is a request for a header view.
        Accordingly, a header view is returned and displayed for the inter-item
        gap indicator.
    </p>
    <p>
        None of this is going to work for you so replace the content of this method
        with:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13226815">
                    <td class="code" id="p132268code15">
                        <pre class="swift" style="font-family:monospace;">
                            func collectionView(collectionView: NSCollectionView, viewForSupplementaryElementOfKind
                            kind: String, atIndexPath indexPath: NSIndexPath) -&gt; NSView { // 1 let
                            identifier: String = kind == NSCollectionElementKindSectionHeader ? "HeaderView"
                            : "" let view = collectionView.makeSupplementaryViewOfKind(kind, withIdentifier:
                            identifier, forIndexPath: indexPath) // 2 if kind == NSCollectionElementKindSectionHeader
                            { let headerView = view as! HeaderView headerView.sectionTitle.stringValue
                            = "Section \(indexPath.section)" let numberOfItemsInSection = imageDirectoryLoader.numberOfItemsInSection(indexPath.section)
                            headerView.imageCount.stringValue = "\(numberOfItemsInSection) image files"
                            } return view }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s what you did in here:
    </p>
    <ol>
        <li>
            You set the
            <code>
                identifier
            </code>
            according to the
            <code>
                kind
            </code>
            parameter received. When it isn’t a header view, you set the
            <code>
                identifier
            </code>
            to the empty
            <code>
                String
            </code>
            . When you pass to
            <code>
                makeSupplementaryViewOfKind
            </code>
            an
            <code>
                identifier
            </code>
            that doesn’t have a matching class or nib, it will return
            <code>
                nil
            </code>
            . When a
            <code>
                nil
            </code>
            is returned, the collection view uses its default inter-item gap indicator.
            When you need to use a custom indicator, you define a nib (as you did for
            the header) and pass its identifier instead of the empty string.
        </li>
        <li>
            When it is a header view, you set up its labels as before.
        </li>
    </ol>
    <div class="note">
        <em>
            Note
        </em>
        : There is a bug in the Swift API regarding the method above, and the
        <code>
            makeItemWithIdentifier
        </code>
        and
        <code>
            makeSupplementaryViewOfKind
        </code>
        methods. The return value specified is
        <code>
            NSView
        </code>
        , but these methods may return
        <code>
            nil
        </code>
        so the return value should be
        <code>
            NSView?
        </code>
        — the question mark is part of the value.
    </div>
    <p>
        Build and run.
    </p>
    <p>
        Now you see an unmistakable aqua vertical line when you drag an item,
        indicating the drop target between the items. It’s a sign that the collection
        view is ready to accept the drop.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/InterItemAnimation.gif">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/InterItemAnimation.gif"
            alt="InterItemAnimation" width="641" height="345" class="aligncenter size-full wp-image-132804">
        </a>
    </p>
    <p>
        Well…it’s sort of ready. When you try to drop the item, it still bounces
        back because the delegate methods to handle the drop are not in place yet.
    </p>
    <p>
        Append the following method to
        <code>
            ImageDirectoryLoader
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13226816">
                    <td class="code" id="p132268code16">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 func moveImageFromIndexPath(indexPath: NSIndexPath, toIndexPath:
                            NSIndexPath) { &nbsp; // 2 let itemBeingDragged = removeImageAtIndexPath(indexPath)
                            &nbsp; let destinationIsLower = indexPath.compare(toIndexPath) == .OrderedDescending
                            var indexPathOfDestination: NSIndexPath if destinationIsLower { indexPathOfDestination
                            = toIndexPath } else { indexPathOfDestination = NSIndexPath(forItem: toIndexPath.item-1,
                            inSection: toIndexPath.section) } // 3 insertImage(itemBeingDragged, atIndexPath:
                            indexPathOfDestination) }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s what’s going on in there:
    </p>
    <ol>
        <li>
            Call this method to update the model when items are moved
        </li>
        <li>
            Remove the dragged item from the model
        </li>
        <li>
            Reinsert at its new position in the model
        </li>
    </ol>
    <p>
        Finish things off here by adding the following methods to the
        <code>
            NSCollectionViewDelegate
        </code>
        extension in
        <code>
            ViewController
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13226817">
                    <td class="code" id="p132268code17">
                        <pre class="swift" style="font-family:monospace;">
                            // 1 func collectionView(collectionView: NSCollectionView, acceptDrop
                            draggingInfo: NSDraggingInfo, indexPath: NSIndexPath, dropOperation: NSCollectionViewDropOperation)
                            -&gt; Bool { if indexPathsOfItemsBeingDragged != nil { // 2 let indexPathOfFirstItemBeingDragged
                            = indexPathsOfItemsBeingDragged.first! var toIndexPath: NSIndexPath if
                            indexPathOfFirstItemBeingDragged.compare(indexPath) == .OrderedAscending
                            { toIndexPath = NSIndexPath(forItem: indexPath.item-1, inSection: indexPath.section)
                            } else { toIndexPath = NSIndexPath(forItem: indexPath.item, inSection:
                            indexPath.section) } // 3 imageDirectoryLoader.moveImageFromIndexPath(indexPathOfFirstItemBeingDragged,
                            toIndexPath: toIndexPath) // 4 collectionView.moveItemAtIndexPath(indexPathOfFirstItemBeingDragged,
                            toIndexPath: toIndexPath) } else { // 5 var droppedObjects = Array&lt;NSURL&gt;()
                            draggingInfo.enumerateDraggingItemsWithOptions(NSDraggingItemEnumerationOptions.Concurrent,
                            forView: collectionView, classes: [NSURL.self], searchOptions: [NSPasteboardURLReadingFileURLsOnlyKey
                            : NSNumber(bool: true)]) { (draggingItem, idx, stop) in if let url = draggingItem.item
                            as? NSURL { droppedObjects.append(url) } } // 6 insertAtIndexPathFromURLs(droppedObjects,
                            atIndexPath: indexPath) } return true } &nbsp; // 7 func collectionView(collectionView:
                            NSCollectionView, draggingSession session: NSDraggingSession, endedAtPoint
                            screenPoint: NSPoint, dragOperation operation: NSDragOperation) { indexPathsOfItemsBeingDragged
                            = nil }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Here’s what happens with these methods:
    </p>
    <ol>
        <li>
            This is invoked when the user releases the mouse to commit the drop operation.
        </li>
        <li>
            Then it falls here when it’s a move operation.
        </li>
        <li>
            It updates the model.
        </li>
        <li>
            Then it notifies the collection view about the changes.
        </li>
        <li>
            It falls here to accept a drop from another app.
        </li>
        <li>
            Calls the same method in
            <code>
                ViewController
            </code>
            as
            <em>
                Add
            </em>
            with
            <em>
                URLs
            </em>
            obtained from the
            <code>
                NSDraggingInfo
            </code>
            .
        </li>
        <li>
            Invoked to conclude the drag session. Clears the value of
            <code>
                indexPathsOfItemsBeingDragged
            </code>
            .
        </li>
    </ol>
    <p>
        Build and run.
    </p>
    <p>
        Now it’s possible to move a single item to a different location in the
        same section. Dragging one or more items from another app should work too.
    </p>
    <h3>
        Fix the UI
    </h3>
    <p>
        The current implementation of drag-and-drop in SlidesPro doesn’t support
        drop across sections. Also, multi-selection is supported only for a drop
        outside SlidesPro. To disable in
        <em>
            UI
        </em>
        , these unsupported capabilities change the
        <code>
            else
        </code>
        part of the second
        <code>
            if
        </code>
        statement to:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13226818">
                    <td class="code" id="p132268code18">
                        <pre class="swift" style="font-family:monospace;">
                            func collectionView(collectionView: NSCollectionView, validateDrop draggingInfo:
                            NSDraggingInfo, proposedIndexPath proposedDropIndexPath: AutoreleasingUnsafeMutablePointer&lt;NSIndexPath?&gt;,
                            dropOperation proposedDropOperation: UnsafeMutablePointer&lt;NSCollectionViewDropOperation&gt;)
                            -&gt; NSDragOperation { if proposedDropOperation.memory == NSCollectionViewDropOperation.On
                            { proposedDropOperation.memory = NSCollectionViewDropOperation.Before }
                            if indexPathsOfItemsBeingDragged == nil { return NSDragOperation.Copy }
                            else { let sectionOfItemBeingDragged = indexPathsOfItemsBeingDragged.first!.section
                            // 1 if let proposedDropsection = proposedDropIndexPath.memory?.section
                            where sectionOfItemBeingDragged == proposedDropsection &amp;&amp; indexPathsOfItemsBeingDragged.count
                            == 1 { return NSDragOperation.Move } else { // 2 return NSDragOperation.None
                            } } }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <ol>
        <li>
            The drop is enabled only when the source and target sections match and
            exactly one item is selected.
        </li>
        <li>
            Otherwise, it prevents the drop by returning
            <code>
                .None
            </code>
        </li>
    </ol>
    <p>
        Build and run. Try dragging an item from one section to another. The drop
        indicator does not present itself, meaning a drop is impossible.
    </p>
    <p>
        Now drag a multi-selection. While inside the bounds of the collection
        view there is no drop indicator; however, drag it to
        <em>
            Finder
        </em>
        , and you’ll see that a drop is allowed.
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        If you tried to drag the selection outside the collection view, you might
        have noticed a highlight issue. You’ll come back to this in the upcoming
        section, “More Fun With Selection and Highlighting”.
    </div>
    <h2>
        More Fun With Selection and Highlighting
    </h2>
    <p>
        In the previous section, you noticed an issue with highlighting.
    </p>
    <p>
        For the sake of sanity in this discussion, the item being moved will be
        <em>
            Item-1
        </em>
        . After
        <em>
            Item-1
        </em>
        lands at a new position it stays highlighted, and the
        <em>
            Add
        </em>
        and
        <em>
            Remove
        </em>
        buttons are enabled, but the selection is empty.
    </p>
    <p>
        To confirm this is true, select any item —
        <em>
            Item-2
        </em>
        . It highlights as expected, but
        <em>
            Item-1
        </em>
        stays highlighted. It should have been deselected and the highlight removed
        when you selected
        <em>
            Item-2
        </em>
        .
    </p>
    <p>
        Click anywhere between the items to deselect everything.
        <em>
            Item-2’s
        </em>
        highlight goes away, the
        <em>
            Add
        </em>
        and
        <em>
            Remove
        </em>
        buttons are disabled, as they should be for no selection, but
        <em>
            Item-1
        </em>
        is
        <i>
            still
        </i>
        highlighted.
    </p>
    <div class="note">
        <em>
            Note:
        </em>
        The collection view tracks its selection in its
        <code>
            selectionIndexPaths
        </code>
        property. To debug, you can insert print statements to show the value
        of this property.
    </div>
    <p>
        So what’s going wrong here?
    </p>
    <p>
        Apparently, the collection view successfully deselects
        <em>
            Item-1
        </em>
        , but the
        <code>
            collectionView(_:didDeselectItemsAtIndexPaths: )
        </code>
        delegate method is not called to remove the highlight and disable the
        buttons.
    </p>
    <p>
        In
        <code>
            NSCollectionView.h
        </code>
        , the comments for the above method and its companion for the select action
        say, “Sent at the end of interactive selection…”. Hence, these notifications
        are sent only when you select/deselect via UI.
    </p>
    <p>
        Here’s your answer, Sherlock: The deselection behavior that should occur
        when you’re moving an item is performed programmatically via the
        <code>
            deselectItemsAtIndexPaths(_:)
        </code>
        method of
        <code>
            NSCollectionView
        </code>
        .
    </p>
    <p>
        You’ll need to override this method.
    </p>
    <p>
        Go to
        <em>
            File \ New \ File…
        </em>
        and create a new
        <em>
            Cocoa Class
        </em>
        by the name
        <em>
            CollectionView
        </em>
        make it a subclass of
        <em>
            NSCollectionView
        </em>
        and put it in the
        <em>
            Views
        </em>
        group.
    </p>
    <p>
        The template may add a
        <code>
            drawRect(_:)
        </code>
        — make sure to delete it.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/EmptyCollectionView.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/EmptyCollectionView-700x442.png"
            alt="EmptyCollectionView" width="700" height="442" class="aligncenter size-large wp-image-132325"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/EmptyCollectionView-700x442.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/EmptyCollectionView-480x303.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/EmptyCollectionView-768x485.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/EmptyCollectionView.png 978w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Add the following method to
        <code>
            CollectionView
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13226819">
                    <td class="code" id="p132268code19">
                        <pre class="swift" style="font-family:monospace;">
                            override func deselectItemsAtIndexPaths(indexPaths: Set&lt;NSIndexPath&gt;)
                            { super.deselectItemsAtIndexPaths(indexPaths) let viewController = delegate
                            as! ViewController viewController.highlightItems(false, atIndexPaths: indexPaths)
                            }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        The method calls its super implementation followed by a call to
        <code>
            highlightItems(_:atIndexPaths:)
        </code>
        of its delegate, allowing
        <code>
            ViewController
        </code>
        to highlight/unhighlight items and enable/disable buttons respectively.
    </p>
    <p>
        Open
        <em>
            Main.storyboard
        </em>
        and select the
        <em>
            Collection View
        </em>
        . In the
        <em>
            Identity Inspector
        </em>
        , change
        <em>
            Class
        </em>
        to
        <em>
            CollectionView
        </em>
        .
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/CollectionViewIB.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/CollectionViewIB-700x383.png"
            alt="CollectionViewIB" width="700" height="383" class="aligncenter size-large wp-image-132328"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/CollectionViewIB-700x383.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/CollectionViewIB-480x263.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/CollectionViewIB-768x421.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/CollectionViewIB.png 1057w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        Build and run.
    </p>
    <p>
        Move an item inside the collection to a different location. Nothing shows
        as highlighted and buttons disable as expected. Case closed.
    </p>
    <h2>
        Animation in Collection Views
    </h2>
    <p>
        <code>
            NSCollectionView
        </code>
        , as a subclass of
        <code>
            NSView
        </code>
        , can perform animations via the animator proxy. It’s as easy as adding
        a single word in your code before an operation such as removal of items.
    </p>
    <p>
        At the end of the
        <code>
            removeSlide(_:)
        </code>
        method in
        <code>
            ViewController
        </code>
        , replace this:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13226820">
                    <td class="code" id="p132268code20">
                        <pre class="swift" style="font-family:monospace;">
                            collectionView.deleteItemsAtIndexPaths(selectionIndexPaths)
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
                <tr id="p13226821">
                    <td class="code" id="p132268code21">
                        <pre class="swift" style="font-family:monospace;">
                            collectionView.animator().deleteItemsAtIndexPaths(selectionIndexPaths)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run.
    </p>
    <p>
        Select several items and click the
        <em>
            Remove
        </em>
        button. Watch as the items glide to take up their new positions on the
        screen.
    </p>
    <p>
        The default duration is a quarter of a second. To experience a really
        cool and beautiful effect, add a setting for the duration of the animation
        at a higher value. Place it above the line you just added:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13226822">
                    <td class="code" id="p132268code22">
                        <pre class="swift" style="font-family:monospace;">
                            NSAnimationContext.currentContext().duration = 1.0 collectionView.animator().deleteItemsAtIndexPaths(selectionIndexPaths)
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Build and run, and then remove some items. Cool effect, isn’t it?
    </p>
    <p>
        You can do the same for
        <code>
            insertItemsAtIndexPaths
        </code>
        when you’re adding items, as well as for
        <code>
            moveItemAtIndexPath
        </code>
        when moving an item.
    </p>
    <h2>
        Sticky Headers
    </h2>
    <p>
        When you scroll a collection view with section headers, the first element
        of a given section that vanishes at the top of the screen is its header.
    </p>
    <p>
        In this section, you’ll implement
        <em>
            Sticky Headers
        </em>
        , so the top-most section header will pin itself to the top of the collection
        view. It will hold its position until the next section header bumps it
        out of the way.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeadersScreen.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeadersScreen-700x500.png"
            alt="StickyHeadersScreen" width="700" height="500" class="aligncenter size-large wp-image-132329"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeadersScreen-700x500.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeadersScreen-448x320.png 448w, https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeadersScreen-768x549.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeadersScreen.png 956w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        To make this effect reality, you’ll subclass
        <code>
            NSCollectionViewFlowLayout
        </code>
        .
    </p>
    <p>
        Go to
        <em>
            File \ New \ File…
        </em>
        and create a new
        <em>
            Cocoa Class
        </em>
        named
        <em>
            StickyHeadersLayout
        </em>
        as a subclass of
        <em>
            NSCollectionViewFlowLayout
        </em>
        , and put it in the
        <em>
            Layout
        </em>
        group.
    </p>
    <p>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeaderSkeleton.png">
            <img src="https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeaderSkeleton-700x411.png"
            alt="StickyHeaderSkeleton" width="700" height="411" class="aligncenter size-large wp-image-132330"
            srcset="https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeaderSkeleton-700x411.png 700w, https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeaderSkeleton-480x282.png 480w, https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeaderSkeleton-768x451.png 768w, https://koenig-media.raywenderlich.com/uploads/2016/04/StickyHeaderSkeleton.png 960w"
            sizes="(max-width: 700px) 100vw, 700px">
        </a>
    </p>
    <p>
        In
        <code>
            ViewController
        </code>
        , change the first line of
        <code>
            configureCollectionView()
        </code>
        to:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13226823">
                    <td class="code" id="p132268code23">
                        <pre class="swift" style="font-family:monospace;">
                            let flowLayout = StickyHeadersLayout()
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Now implement sticky headers by adding the following method to the empty
        body of the
        <code>
            StickyHeadersLayout
        </code>
        class:
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13226824">
                    <td class="code" id="p132268code24">
                        <pre class="swift" style="font-family:monospace;">
                            override func layoutAttributesForElementsInRect(rect: NSRect) -&gt; [NSCollectionViewLayoutAttributes]
                            { &nbsp; // 1 var layoutAttributes = super.layoutAttributesForElementsInRect(rect)
                            &nbsp; // 2 let sectionsToMoveHeaders = NSMutableIndexSet() for attributes
                            in layoutAttributes { if attributes.representedElementCategory == .Item
                            { sectionsToMoveHeaders.addIndex(attributes.indexPath!.section) } } &nbsp;
                            // 3 for attributes in layoutAttributes { if let elementKind = attributes.representedElementKind
                            where elementKind == NSCollectionElementKindSectionHeader { sectionsToMoveHeaders.removeIndex(attributes.indexPath!.section)
                            } } &nbsp; // 4 sectionsToMoveHeaders.enumerateIndexesUsingBlock { (index,
                            stop) -&gt; Void in let indexPath = NSIndexPath(forItem: 0, inSection:
                            index) let attributes = self.layoutAttributesForSupplementaryViewOfKind(NSCollectionElementKindSectionHeader,
                            atIndexPath: indexPath) if attributes != nil { layoutAttributes.append(attributes!)
                            } } &nbsp; for attributes in layoutAttributes { // 5 if let elementKind
                            = attributes.representedElementKind where elementKind == NSCollectionElementKindSectionHeader
                            { let section = attributes.indexPath!.section let attributesForFirstItemInSection
                            = layoutAttributesForItemAtIndexPath(NSIndexPath(forItem: 0, inSection:
                            section)) let attributesForLastItemInSection = layoutAttributesForItemAtIndexPath(NSIndexPath(forItem:
                            collectionView!.numberOfItemsInSection(section) - 1, inSection: section))
                            var frame = attributes.frame &nbsp; // 6 let offset = collectionView!.enclosingScrollView?.documentVisibleRect.origin.y
                            &nbsp; // 7 let minY = CGRectGetMinY(attributesForFirstItemInSection!.frame)
                            - frame.height &nbsp; // 8 let maxY = CGRectGetMaxY(attributesForLastItemInSection!.frame)
                            - frame.height &nbsp; // 9 let y = min(max(offset!, minY), maxY) &nbsp;
                            // 10 frame.origin.y = y attributes.frame = frame &nbsp; // 11 attributes.zIndex
                            = 99 } } &nbsp; // 12 return layoutAttributes }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        Okay, there’s a lot happening in there, but it makes sense when you take
        it section by section:
    </p>
    <ol>
        <li>
            The super method returns an array of attributes for the visible elements.
        </li>
        <li>
            The
            <code>
                NSMutableIndexSet
            </code>
            first aggregates all the sections that have at least one visible item.
        </li>
        <li>
            Remove all sections from the set where the header is already in
            <code>
                layoutAttributes
            </code>
            , leaving only the sections with “Missing Headers” in the set.
        </li>
        <li>
            Request the attributes for the missing headers and add them to
            <code>
                layoutAttributes
            </code>
            .
        </li>
        <li>
            Iterate over
            <code>
                layoutAttributes
            </code>
            and process only the headers.
        </li>
        <li>
            Set the coordinate for the top of the visible area, aka scroll offset.
        </li>
        <li>
            Make it so the header never goes further up than one-header-height above
            the upper bounds of the first item in the section.
        </li>
        <li>
            Make it so the header never goes further down than one-header-height above
            the lower bounds of the last item in the section.
        </li>
        <li>
            Let’s break this into 2 statements:
            <ol>
                <li>
                    <code>
                        maybeY = max(offset!, minY)
                    </code>
                    : When the top of the section is above the visible area this pins (or
                    pushes down) the header to the top of the visible area.
                </li>
                <li>
                    <code>
                        y = min(maybeY, maxY)
                    </code>
                    : When the space between the bottom of the section to the top of the visible
                    area is less than header height, it shows only the part of the header’s
                    bottom that fits this space.
                </li>
            </ol>
        </li>
        <li>
            Update the vertical position of the header.
        </li>
        <li>
            Make the items “go” under the header.
        </li>
        <li>
            Return the updated attributes.
        </li>
    </ol>
    <p>
        Add the following method to
        <code>
            StickyHeadersLayout
        </code>
        :
    </p>
    <div class="wp_codebox">
        <table>
            <tbody>
                <tr id="p13226825">
                    <td class="code" id="p132268code25">
                        <pre class="swift" style="font-family:monospace;">
                            override func shouldInvalidateLayoutForBoundsChange(newBounds: CGRect)
                            -&gt; Bool { return true }
                        </pre>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <p>
        You always return
        <code>
            true
        </code>
        because you want the to invalidate the layout as the user scrolls.
    </p>
    <p>
        Build and run.
    </p>
    <p>
        Scroll the collection to see your sticky headers in action.
    </p>
    <h2>
        Where To Go From Here
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
            SlidesPro
        </em>
        <a href="https://koenig-media.raywenderlich.com/uploads/2016/04/SlidesPro-Final.zip">
            here
        </a>
        .
    </p>
    <p>
        In this Advanced Collection Views in OS X Tutorial you covered a lot of
        ground! You took the collection view from a rudimentary app to one that
        features the kinds of bells and whistles any Mac user would expect.
    </p>
    <p>
        After all your hard work, you’re able to add and remove items, reorder
        them, and troubleshoot and correct highlighting/selection issues. You took
        it to the next level by adding in animations and implemented sticky headers
        to give SlidesPro a very polished look.
    </p>
    <p>
        Most impressively, you now know how to build a functional, elegant collection
        view in OS X. Considering that the documentation for these is fairly limited,
        it’s a great skill to have.
    </p>
    <p>
        Some of the topics that were not covered neither here nor in the basic
        tutorial are:
    </p>
    <ul>
        <li>
            Creating custom layouts by subclassing directly
            <code>
                NSCollectionViewLayout
            </code>
        </li>
        <li>
            “Data Source-less” collection views using
            <em>
                <a href="https://www.raywenderlich.com/124490/cocoa-bindings-os-x-tutorial">
                    Cocoa Bindings
                </a>
            </em>
        </li>
    </ul>
    <p>
        One of the top resources recommended at the end of the
        <a href="https://www.raywenderlich.com/120494/collection-views-os-x-tutorial"
        target="_blank">
            basic tutorial
        </a>
        is this excellent video tutorial series
        <a href="https://www.raywenderlich.com/video-tutorials#CCVL" target="_blank"
        title="Custom Collection View Layout">
            Custom Collection View Layout
        </a>
        from Mic Pringle. Although it’s an iOS series, you can find lots of useful
        information that’s relevant to collection views in OS X as well.
    </p>
    <p>
        I hope you found this tutorial most helpful! Let’s talk about it in the
        forums. I look forward to your questions, comments and discoveries!
    </p>
</div>